VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
 

  config.vm.box = "hashicorp/precise32"

  config.vm.synced_folder "/Users/francescoparis/Documents/progetto/sinc", "/cartella", :mount_options => ["dmode=777", "fmode=777"]
	
  config.vm.define "client" do |client|
    client.vm.hostname = "client"
    


 client.ssh.forward_agent = true
 client.ssh.forward_x11 = true
 
 config.vm.provision :shell, :inline => 'apt-get update'
 config.vm.provision :shell, :inline => 'apt-get install build-essential ruby1.9.1-dev --no-upgrade --yes'
 config.vm.provision :shell, :inline => "gem install chef --version 11.16.4 --no-rdoc --no-ri --conservative"
 
 client.vm.provision :chef_solo do |chef|
      chef.add_recipe "apt"
      chef.add_recipe "java::default"     
      chef.add_recipe "glassfish::attribute_driven_domain"
      
     
     
     
      
      chef.json = {
      	
        "java" => {
        	"install_flavor" => "oracle",
        	"jdk_version" => 7,
        	"oracle" => {
        		"accept_oracle_download_terms" => true
        	}
        },
        "glassfish" => {
        "version" => "4.0.1",
        "package_url" => "http://dlc.sun.com.edgesuite.net/glassfish/4.0.1/promoted/glassfish-4.0.1-b01.zip",
        "base_dir" => "/usr/local/glassfish",
        "domains_dir" => "/usr/local/glassfish/glassfish/domains",
        "domains" => {
          "domain1" => {
            "config" => {
              "port" => 7070,
              "admin_port" => 4848,
              "username" => "admin",
              "password" => "admin",
              "remote_access" => true
            }
            
            
          }
        }
      }
       
    		
    		
  		}
        
        
        
        
      
  end

  
  client.vm.provision :shell, :inline => "echo  'configurazione client completata'"
  end


 
end
