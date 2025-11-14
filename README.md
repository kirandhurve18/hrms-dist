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

NOTE : AFTER CHNAGING ANY FILE IN THE BACKEND YOU NEED TO RESTART THE INDEX.JS 
       FOR THE RUN COMMAND (Pm2 restart all )
       Check with -- pm2 list 



####  Docker setup for the server (backend)

Set up Docker's apt repository.

````
# Add Docker's official GPG key:
sudo apt update
sudo apt install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
Types: deb
URIs: https://download.docker.com/linux/ubuntu
Suites: $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}")
Components: stable
Signed-By: /etc/apt/keyrings/docker.asc
EOF

sudo apt update
````

````
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
````
````
sudo systemctl status docker
````
````
sudo systemctl start docker
````
# To install the latest version, run:

Install npm

````
apt update
apt install npm -y
npm install
````
````
install pm2 for daemon service running on server
````
````
npm install -g pm2
````
````
pm2 start server.js --name grocery-backend
````
````
pm2 save
````
````
pm2 startup
````
````
pm2 list
````
````
node -v 
npm -v
````
# Install Docker on server for docker file 

GO TO THE BACKEND FOLDER 

COMMAND TO BUILD DOCKER IMAGE 

````
docker build -t hrms-backend .
````
````
docker run -d --name <container-name> -p 3005:3005 <docker-image-name>
````
COMMAND TO RUN CONTAINER
````
docker run -d --name hrms-second -p 3005:3005 hrms-backens
````
Docker file for backend :
````
# 1. Use Official Node 20 Image
FROM node:20-alpine

# 2. Set working directory inside container
WORKDIR /app

# 3. Copy package.json and package-lock.json
COPY package*.json ./ 

# 4. Install only production dependencies

RUN npm install 

RUN npm install uuid 

RUN npm install pm2 -g

# 5. Copy the entire backend code
COPY . .

# 6. Expose backend port
EXPOSE 3000

# 7. Start the backend
CMD ["pm2-runtime", "index.js"]
````
