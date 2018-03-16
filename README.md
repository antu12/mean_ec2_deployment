# MEAN EC2(Amazon Linux AMI) Deployment Tutorial
---------------------
### After Setting Up an AMI instance
* ```sudo yum install gcc-c++ openssl-devel make```
* ```wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.31.0/install.sh | bash```
* ```nvm install [version]```
### Install Git
* ```sudo yum install git```
### Install Mongo
* ```sudo nano /etc/yum.repos.d/mongodb-org-3.6.repo```
* Paste the following code, save and exit
  ```
  [mongodb-org-3.6]
  name=MongoDB Repository
  baseurl=https://repo.mongodb.org/yum/amazon/2013.03/mongodb-org/3.6/x86_64/
  gpgcheck=1
  enabled=1
  gpgkey=https://www.mongodb.org/static/pgp/server-3.6.asc
  ```
* ```sudo yum install -y mongodb-org```
* ```sudo service mongod start```
### Install and use NGINX as a proxy to your server
* ```sudo yum install nginx```
* ```sudo service nginx start```
* ```sudo nano /etc/nginx/conf.d/myapp.com.conf```
* Paste the following code, save and exit
  ```
  server {
      listen 80;

      server_name #YOUR SERVER NAME#

      location / {
          proxy_pass #RUNNING APP, example : http://localhost:3000#;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection 'upgrade';
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
      }
  }
  ```
### Install and configure Jenkins
