## How to create an authenticated shiny-server using Nginx, auth0, Name Cheap, and Digital Ocean

### SSH into your droplet

### Update the packages for the first time

    sudo apt-get update

### Add user to droplet server

    adduser shiny

#### Make user a super user with root privileges

    gpasswd -a shiny sudo

### Switch user 

    su - shiny


### Install Nginx & update the packages
```
    sudo apt-get update

    sudo apt-get -y install nginx

    sudo nano /etc/nginx/sites-enabled/default
```  

### List of nginx commands

### Stop the nginx server
    sudo service nginx stop
    
### Start the nginx server

    sudo service nginx start
    
### Restart the nginx server    
    sudo service nginx restart


### Install R

#### First we need to add xenial to our sources list in our server

    sudo sh -c 'echo "deb http://cran.rstudio.com/bin/linux/ubuntu xenial/" >> /etc/apt/sources.list'


### Next we need to add the public keys for R

      gpg --keyserver keyserver.ubuntu.com --recv-key E084DAB9
      gpg -a --export E084DAB9 | sudo apt-key add -
  

### Now we can install R on our Droplet. 


### Install base R and the Dev version of R


### Update our packages again

    sudo apt-get update

    sudo apt-get -y install r-base r-base-dev



### Create swap space on server to allow for more room for packages

      sudo /bin/dd if=/dev/zero of=/var/swap.1 bs=1M count=1024
      sudo /sbin/mkswap /var/swap.1
      sudo /sbin/swapon /var/swap.1
      sudo sh -c 'echo "/var/swap.1 swap swap defaults 0 0 " >> /etc/fstab'


### Let's install the dependencies for us to use 'devtools' in R 

    sudo apt-get -y install libcurl4-gnutls-dev libxml2-dev libssl-dev


### Install packages from CRAN and GitHub (devtools, shinyjs)

    sudo su - -c "R -e \"install.packages('devtools', repos='http://cran.rstudio.com/')\""
    sudo su - -c "R -e \"devtools::install_github('daattali/shinyjs')\""

### Install RStudio Server  [Download R-Studio Server](https://www.rstudio.com/products/rstudio/download-server/) if you have not already.

    sudo apt-get -y install gdebi-core

    wget https://download2.rstudio.org/rstudio-server-1.1.463-amd64.deb

    sudo gdebi rstudio-server-1.1.463-amd64.deb


### Install Shiny-Server   [Download Shiny-Server](https://www.rstudio.com/products/shiny/download-server/) if you have not already.

     wget https://download3.rstudio.org/ubuntu-14.04/x86_64/shiny-server-1.5.9.923-amd64.deb
     
     sudo gdebi shiny-server-1.5.9.923-amd64.deb


#### Install the shiny package first
We need to install the shiny package first, this allows us to run the shiny server and our applications

    sudo su - -c "R -e \"install.packages('shiny', repos='http://cran.rstudio.com/')\""

##### Set Up Permissions on Shiny Server


    sudo groupadd shiny-apps
    sudo usermod -aG shiny-apps ben
    sudo usermod -aG shiny-apps shiny
    sudo usermod -aG shiny-apps shiny
    cd /srv/shiny-server
    sudo chown -R dean:shiny-apps .
    sudo chmod g+w .
    sudo chmod g+s .

### Install Git 

    sudo apt-get -y install git
    git config --global user.email "you@example.com"
    git config --global user.name "Your Name"

### Make /srv/shiny-server a git repository

    cd /srv/shiny-server
    git init

### Add a git repository to our Shiny Server


    git remote add origin https://github.com/daattali/shiny-server.git
    git add .
    git commit -m "Initial commit"
    git push -u origin master


### Have shiny listen on two ports

    sudo /opt/shiny-server/bin/deploy-example multi-server

### Restart Shiny Server

    sudo service shiny-server restart


### Create some awesome urls so we do not have to remember port numbers

    sudo nano /etc/nginx/sites-enabled/default

### Add the following lines right after the line that reads server_name _;


    location /shiny/ {
      proxy_pass http://127.0.0.1:3838/;
      proxy_http_version 1.1;
      proxy_set_header Upgrade $http_upgrade;
      proxy_set_header Connection "upgrade";
      rewrite ^(/shiny/[^/]+)$ $1/ permanent;

    }

    location /rstudio/ {
      proxy_pass http://127.0.0.1:8787/;
      proxy_http_version 1.1;
      proxy_set_header Upgrade $http_upgrade;
      proxy_set_header Connection "upgrade";
    }


    location /private-shiny/ {
      proxy_pass http://127.0.0.1:4949/;
      proxy_http_version 1.1;
      proxy_set_header Upgrade $http_upgrade;
      proxy_set_header Connection "upgrade";
      rewrite ^(/shiny/[^/]+)$ $1/ permanent;

    }




### Restart Nginx for the changes to take effect

    sudo service nginx restart
    
    
### Updated localhost:3000 to reflect your shiny-auth0 configuration file

### Add auth0 to the private Shiny-Server

        # auth0 server
        location /private-shiny/ {
          proxy_set_header    Host $host;

          # This points to our shiny-auth0 authentication proxy,
          # change localhost:3000 to suit the configuration of
          # your shiny-auth0 config
          proxy_pass          http://localhost:3000;
          proxy_redirect      http://localhost:3000/ $scheme://$host/;

          proxy_http_version  1.1;
          # The following lines enable WebSockets proxying, do not remove them
          # as they are used by Shiny Server to improve user experience
          #proxy_set_header Upgrade $http_upgrade;
          #proxy_set_header Connection $connection_upgrade;

          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection "upgrade";

          proxy_connect_timeout 7d;
          proxy_send_timeout 7d;
          proxy_read_timeout 7d;
       }


### Restart Nginx to make the necessary changes take effect

    sudo service nginx restart

