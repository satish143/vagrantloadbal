Vagrant.configure("2") do |config|
  config.vm.define "lb1" do |lb1|
  lb1.vm.box = "centos/7"


lb1.vm.network "private_network", ip: "192.168.33.15"
#lb1.vm.network "public_network"
lb1.vm.provision "shell", inline: <<-SHELL
  sudo yum -y install epel-release    
 sudo yum -y install nginx
     sudo systemctl start nginx
     sudo systemctl enable nginx
echo "user nginx;
worker_processes auto;
error_log /var/log/nginx/error.log;
pid /run/nginx.pid;

# Load dynamic modules. See /usr/share/nginx/README.dynamic.
include /usr/share/nginx/modules/*.conf;

events {
    worker_connections 1024;
}

http {
    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile            on;
    tcp_nopush          on;
    tcp_nodelay         on;
    keepalive_timeout   65;
    types_hash_max_size 2048;

    include             /etc/nginx/mime.types;
    default_type        application/octet-stream;

    # Load modular configuration files from the /etc/nginx/conf.d directory.
    # See http://nginx.org/en/docs/ngx_core_module.html#include
    # for more information.
    include /etc/nginx/conf.d/*.conf;

upstream backend {
    server 192.168.33.16;
    server 192.168.33.17;
}

server {
    location / {
        proxy_pass http://backend;
    }
}

}" > nginx.conf
sudo cp nginx.conf /etc/nginx/
sudo systemctl restart nginx
SHELL

end
config.vm.define "wed1" do |wed1|
 wed1.vm.box = "centos/7"

wed1.vm.network "private_network", ip: "192.168.33.16"
#wed1.vm.network "public_network"

wed1.vm.provision "shell", inline: <<-SHELL
     sudo yum -y install httpd
     sudo systemctl start httpd
     sudo systemctl enable httpd
sudo echo "hello world" > index.html
sudo cp index.html /var/www/html

SHELL

end

config.vm.define "wed3" do |wed3|
wed3.vm.box = "centos/7"


wed3.vm.network "private_network", ip: "192.168.33.17"
#wed3.vm.network "public_network"

wed3.vm.provision "shell", inline: <<-SHELL
     sudo yum -y install httpd
      sudo systemctl start httpd
     sudo systemctl enable httpd
sudo echo "hello satish" > index.html
sudo cp index.html /var/www/html

SHELL

end
 
end

