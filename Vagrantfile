# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

options = {}
options[:ip_guest] = ENV['IP'] || "192.168.33.123"
options[:ansible_vars] = ENV['VARS']

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "raring64"
  config.vm.box_url = "http://goo.gl/ceHWg"
  config.vm.network :private_network, ip: options[:ip_guest]
  config.vm.synced_folder "./", "/var/www/phlybox", id: "vagrant-root", :nfs => true

  #
  # Auto updates the VirtualBox Guest Additions.
  # Needs vagrant-vbguest plugin installed. Install with:
  # $ vagrant gem install vagrant-vbguest
  #
  config.vbguest.auto_update = true
  config.vbguest.no_remote = false

#  config.vm.provider "virtualbox" do |vb|
#    vb.name = "marquee"
#  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "ansible/playbook.yml"
    ansible.extra_vars = options[:ansible_vars]
  end
end