### First install instance  : allow port like 80 for frontend :

# SETUP DATABASE:

# install MONGODB from link 

````
https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-ubuntu/
````

````
sudo apt-get install gnupg curl
curl -fsSL https://www.mongodb.org/static/pgp/server-8.0.asc | \
   sudo gpg -o /usr/share/keyrings/mongodb-server-8.0.gpg \
   --dearmor
echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-8.0.gpg ] https://repo.mongodb.org/apt/ubuntu noble/mongodb-org/8.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-8.0.list
sudo apt-get update
sudo apt-get install -y mongodb-org
sudo systemctl start mongod
````

Log into the database 
````
mongosh
````
````
show dbs
exit
````

# take a code 

install node , npm , git 

git clone 
install nginx 
systemctl enable nginx 
systemctl start nginx
npm install 
npm start 
npm build 
dist will created : copy the path of the dist made 
copy that path to the /var/www/html/
cp -r /home/ubuntu/hrms-dist/dist/hrms/* /var/www/html/

NOTE : IF YOU MADE ANY CHANGES IN THE FILES YOU AGAIN NEED TO RUN THE COMMAND FOR BUILD (npm build run) paste the dist in the /var/www/html/ , 
      restart the nginx .


# vim /etc/nginx/site-available/default

````
server {
    listen 80;
    server_name _;

    root /var/www/html/browser;
    index index.html index.htm;

    location / {
        try_files $uri $uri/ /index.html;
    }

    access_log /var/log/nginx/angular_access.log;
    error_log  /var/log/nginx/angular_error.log;
}
````

After editing servre configuration file :

nginx -t 
systemctl restart nginx

ufw list 
ufw reload 
ufw enable 
ufw allow 'Nginx Full'
ufw reload 


# for backend server setup :

Install node , npm , nginx ,  
Go to the cd backend
npm install
node index.js 
npm install -g pm2 
pm2 start server.js --name hrms-backend
pm2 startup systemd 
pm2 list 

