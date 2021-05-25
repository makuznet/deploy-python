## Video lesson commands
```bash
# root user
# root user home directory
# pyenv installation 1.2.8.5 see a link below
pyenv install 2.7.15 # install python
# pyenv for a particular dir
mkdir /tmp/test1
cd /tmp/test1
pyenv virtualenv 2.7.15 test1
pyenv local test1
python -V
mkdir /tmp/test2
cd /tmp/test2
pyenv virtualenv 3.7.1 test2
pyenv local test2 
pip install django # for test2 dir
pip list # list of installed packages
pyenv global system # use python system version

# Real World app
cd tmp
mkdir rworld
cd rworld
git clone https://github.com/gothinkster/django-realworld-example-app .
pyenv versions
pyenv virtualenv 3.7.1 app # let's give realworld the name 'app'
pyenv local app # use this env for rworld dir
pip install -r requirements.txt # packages installation
pip list
python manage.py # shows all commands that are going to be executed
cd conduit
    vi settings.py # Django config file
        /database # find database section
cd ..
python manage.py migrate # migrate database
python manage.py runserver # run builtin server to check the app
# http://yourdomainname.net:8000/api        
# the coolest thing in Django is an admin page
# http://yourdomainname.net:8000/admin
# to get to admin page
    python manage.py create createsuperuser # why email 

# This part was given without any explanation:
apt install tmux
cd /tmp/rworld 
    tmux
    # apply cd command to have (app) sign at the beginning of the line
    python manage.py runserver
cd /etc/nginx/sites-enabled
    vi default
        server {
            listen 80 default_server;

            root /home/node/nodejs.org/build/;

            index index.html index.htm index.nginx-debian.html;

            server_name _;

            location / {
                proxy_pass http://127.0.0.1:8000;
            }
        }

# For some reason narration was changed to uwsgi
pip install uwsgi
# then google search was done for nginx uwsgi_pass
# http://nginx.org/ru/docs/http/ngx_http_uwsgi_module.html

# uwsgi
# https://uwsgi-docs.readthedocs.io
cd /tmp/rworld 
uwsgi --http :8000 --module conduit.wsgi
```