## Add user to droplet server

    adduser shiny

### Make user a super user with root privileges

    gpasswd -a shiny sudo

## Switch user 

    su - shiny


## Install Nginx & update the packages

    sudo apt-get update

    sudo apt-get -y install nginx

    sudo nano /etc/nginx/sites-enabled/default
  




## List of nginx commands

    sudo service nginx stop
    sudo service nginx start
    sudo service nginx restart


## Install R

# Add xenial to our sources list

    sudo sh -c 'echo "deb http://cran.rstudio.com/bin/linux/ubuntu xenial/" >> /etc/apt/sources.list'


# Add the public keys

      gpg --keyserver keyserver.ubuntu.com --recv-key E084DAB9
      gpg -a --export E084DAB9 | sudo apt-key add -
  

## Install R on our Droplet. 
### Install base R and the Dev version of R

    sudo apt-get update

    sudo apt-get -y install r-base r-base-dev



## Create swap space on server to allow for more room for packages

      sudo /bin/dd if=/dev/zero of=/var/swap.1 bs=1M count=1024
      sudo /sbin/mkswap /var/swap.1
      sudo /sbin/swapon /var/swap.1
      sudo sh -c 'echo "/var/swap.1 swap swap defaults 0 0 " >> /etc/fstab'


## Install Devtools 

    sudo apt-get -y install libcurl4-gnutls-dev libxml2-dev libssl-dev


## Install packages from CRAN and GitHub

    sudo su - -c "R -e \"install.packages('devtools', repos='http://cran.rstudio.com/')\""
    sudo su - -c "R -e \"devtools::install_github('daattali/shinyjs')\""

## Install RStudio Server

    sudo apt-get -y install gdebi-core

    wget https://download2.rstudio.org/rstudio-server-1.1.463-amd64.deb

    sudo gdebi rstudio-server-1.1.463-amd64.deb


## Install Shiny-Server


# Install the shiny package first

    sudo su - -c "R -e \"install.packages('shiny', repos='http://cran.rstudio.com/')\""

## Set Up Permission on Shiny Server


    sudo groupadd shiny-apps
    sudo usermod -aG shiny-apps ben
    sudo usermod -aG shiny-apps shiny
    sudo usermod -aG shiny-apps shiny
    cd /srv/shiny-server
    sudo chown -R dean:shiny-apps .
    sudo chmod g+w .
    sudo chmod g+s .

## Install Git 

    sudo apt-get -y install git
    git config --global user.email "you@example.com"
    git config --global user.name "Your Name"

#Make /srv/shiny-server a git repository

    cd /srv/shiny-server
    git init

## Add a git repository to our Shiny Server


    git remote add origin https://github.com/daattali/shiny-server.git
    git add .
    git commit -m "Initial commit"
    git push -u origin master


##Have shiny listen on two ports

    sudo /opt/shiny-server/bin/deploy-example multi-server

# Restart Shiny Server

    sudo service shiny-server restart


## Awesome urls

    sudo nano /etc/nginx/sites-enabled/default

#Add the following lines right after the line that reads server_name _;


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




## Restart Nginx


## Updated localhost:3000 to reflect your shiny-auth0 configuration file

## Add auth0 to the private Shiny-Server

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


## Restart Nginx to make the necessary changes take effect

    sudo service nginx restart

