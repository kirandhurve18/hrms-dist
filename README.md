## First install instance  : allow port like 80 for frontend :

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

vim /etc/nginx/site-available/default 
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
