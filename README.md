#Domain Name and VPS Setup Companion Guide
####Companion guide to go along with the video at https://youtu.be/PS8-bm_v1Zw
#####This guide is updated and correct as of July 26th

#####Hey everyone! This is the companion guide to go with the youtube video I made. I posted the link at the top of this readme. If anything in the guide looks different than the video, then go with this guide.

#####All of the instructions here are capable of being improved on. If you find a better way of doing anything at all, let me know. ALso, if anything is unclear, let me know as well and I will fix it right up!


# Domain Name Setup
#### video shows using google domains, but format is applicable for any domain service

###A Record
##### used for pointing your domain name at your server's ip address
##### used for creating subdomains (e.g. subdomain.example.com)

#### pointing domain at ip address
```
name will be @
data will be your ip address
```
#### creating subdomain
```
name will be your subdomain (e.g. test)
data wil be your ip address again
```
### CNAME
#####used for telling your domain server that 'www.example.com' is the same as 'example.com'
```
name will be www
data will be your domain name followed by a . (e.g. example.com.)
```

# Inititial VPS Admin Setup
```
1. adduser userName

2. gpasswd -a userName sudo

3. vi  /etc/ssh/sshd_config

4. find PermitRootLogin yes

5 change to PermitRootLogin no

6. service ssh restart

7. su userName
```

# Git Installation
```
1. sudo apt-get update

2. sudo apt-get install git
```

# Node Installation
```
1. sudo apt-get update

2. sudo apt-get install nodejs

3. sudo apt-get install npm

4. sudo ln -s /usr/bin/nodejs /usr/bin/node
```

# Install Mongo
http://docs.mongodb.org/manual/tutorial/install-mongodb-on-ubuntu/
```
1. sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10

2. echo "deb http://repo.mongodb.org/apt/ubuntu "$(lsb_release -sc)"/mongodb-org/3.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.0.list

3. sudo apt-get update

4. sudo apt-get install -y mongodb-org
```


# Passenger Installation
https://www.phusionpassenger.com/documentation/Users%20guide%20Nginx.html#installation
```
1. sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 561F9B9CAC40B2F7

2. sudo apt-get install apt-transport-https ca-certificates

3. sudo touch /etc/apt/sources.list.d/passenger.list

4. sudo vi /etc/apt/sources.list.d/passenger.list

5. deb https://oss-binaries.phusionpassenger.com/apt/passenger trusty main

6. sudo chown root: /etc/apt/sources.list.d/passenger.list

7. sudo chmod 600 /etc/apt/sources.list.d/passenger.list

8. sudo apt-get update

9. sudo apt-get install nginx-extras passenger

10. sudo vi /etc/nginx/nginx.conf
    - uncomment (delete #'s) on passenger_root and passenger_ruby

11. sudo service nginx restart
```



# Getting Nginx set up

#### Tell Nginx where we keep the files we want it to serve up to browsers
```
1. sudo mkdir /usr/share/nginx/www

2. cd /usr/share/nginx/www

3. sudo chown -R userName .

4. sudo chgrp -R www-data .

5. sudo chmod -R 750 .

6. sudo chmod g+s .

7. sudo vi /etc/nginx/sites-enabled/default

8. Add lines per the video
```

#Getting your Node app ready

```
1. add the following to your app.js file:

  if (app.get('env') === 'production') {
    app.listen(3000);
  }

2. create a folder name tmp in your node app directory

3. git clone your folder into /usr/share/nginx/www

4. sudo vi /etc/nginx/sites-enabled/default

5. Add lines per the video
```

# SCP Instructions (Transferring files from your computer to your VPS)
```
1. scp file_on_your_computer userName@yourIPAdress:path_where_you_want_file_placed
  - e.g scp ~/workspace/nodeapp me@example.com:/usr/share/nginx/www/
```
