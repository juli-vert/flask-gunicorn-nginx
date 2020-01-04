# flask-gunicorn-nginx
How to deploy a web api with Flask Gunicorn and Nginx  

## Requirements 
* sudo apt-get install python3-pip python3-dev build-essential libssl-dev libffi-dev python3-setuptools python3-venv  
* sudo apt-get install nginx  
* sudo apt-get install uwsgi uwsgi-core  

## Steps  
1. Create an user to run the wsgi server, let's call it "runner"  
> useradd runner  
passwd runner  
usermod -a -G www-data runner  
usermod --shell /bin/bash runner  
2. Create a folder *whenever*, for this tutorial we will create it in the root directory and give runner/www-data the ownership  
> cd /  
mkdir site  
chown -R runner site  
chgrp -R www-data site  
3. Create a virtual env inside the site folder and activate it
> cd site  
python3 -m venv myvenv  
source /site/myenv/bin/activate
4. Install the required python modules  
> pip3 install Flask  
pip3 install gunicorn
5. Clone this repository  
> git clone https://github.com/julivert82/flask-gunicorn-nginx
6. Leave the virtual env  
> deactivate
7. Place the files following the structure described below  
8. Run the wsgi server as a daemon  
> sudo systemctl start app  
sudo systemctl enable app  
**_You can check the status at any time running the cmd: sudo systemctl status app_**
9. Enable the new nginx site  
> sudo ln -s /etc/nginx/sites-available/app /etc/nginx/sites-enabled  
sudo nginx -t  
sudo systemctl restart nginx

## Folder structure:
/  
|_ /site  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|_ testapp.py  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|_ wsgi.py  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|_ /templates  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|_ template.html  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|_ /static  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|_ nginx.png  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|_ gunicorn.png  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|_ flask.png  
|_ /etc  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|_ /systemd  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|_ /system  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|_ app.service  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|_ /nginx  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|_ /sites-available  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|_ nginxsite  
