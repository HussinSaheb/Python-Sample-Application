required_plugins = ["vagrant-hostsupdater", "vagrant-berkshelf"]
required_plugins.each do |plugin|
    Vagrant::Plugin::Manager.instance.install_plugin("#{plugin}") unless Vagrant.has_plugin? plugin
end

Vagrant.configure("2") do |config|
  config.vm.define "dev" do |app|
    app.vm.box = "ubuntu/xenial64"
    app.vm.network "private_network", ip: "192.168.10.100"
    app.hostsupdater.aliases = ["development.local"]
    app.vm.synced_folder "./", "/home/ubuntu/python_app"
    app.vm.provision "chef_solo" do |chef|
      chef.add_recipe "python::default"
    end
    app.vm.provision "chef_solo" do |chef|
      chef.add_recipe "nginx::default"
    end
    
  end
end
