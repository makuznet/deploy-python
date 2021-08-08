# Python app deployment
> This repo is a Django Python app deployment report

## List of commands
```bash
cd terraform-do
terraform init
terraform plan
terraform apply --auto-approve
ssh makuznet-at-gmail-com-py.devops.rebrain.srwx.net -l root
    apt update
    apt -y install curl git sudo
    adduser pyth # interactive Debian script using instead useradd command
    exit
ssh makuznet-at-gmail-com-py.devops.rebrain.srwx.net -l root
    usermod -aG sudo pyth
    getent group sudo
    su - pyth
    sudo echo "$USER ALL=(ALL:ALL) NOPASSWD: ALL" | sudo tee -a /etc/sudoers
    mkdir rworld
    cd rworld
        git clone https://github.com/gothinkster/django-realworld-example-app .
        cd ..
    # pyenv installation
    # prerequisites: python build dependencies
    sudo apt-get install make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev
    curl https://pyenv.run | bash # automatic pyenv installation
    source .bashrc # exec $SHELL didn't work for me
    pyenv versions # system is the only available
    pyenv install 3.9.5
    cd rworld
        pyenv virtualenv 3.9.5 rworld
        pyenv activate rworld # (rworld) pyth@domain-name:~/rworld$ invitation the expected (rworld) appeared at last!!!
        pip install -r requirements.txt # packages installation
        pip list    
        python manage.py # massive errors
        pyenv deactivate 
        pyenv uninstall rworld
        pyenv install 3.7.1
        pyenv virtualenv 3.7.1 rworld
        pyenv activate rworld
        pip install -r requirements.txt
        python manage.py # commands appeared
        sudo apt -y install postgresql postgresql-server-dev-11   # server-dev — developer's lib
        sudo -u postgres psql
            create database django_db;
            create user django with password 'netlab';
            alter role django set client_encoding to 'utf8';
            alter role django set default_transaction_isolation to 'read committed';
            alter role django set timezone to 'UTC';
            grant all privileges on database django_db to django;
            \q
        cd conduit
            cp settings.py settings.py.original
            vi settings.py    
                'ENGINE': 'django.db.backends.postgresql_psycopg2',
                'NAME': 'django_db',
                'USER' : 'django',
                'PASSWORD' : 'password',
                'HOST' : '127.0.0.1',
                'PORT' : '5432',
                :wq
            cd ..
        pip install psycopg2  # to get Python working with Postgres  
        pip list # psycopg2 added
        python manage.py migrate

        python manage.py createsuperuser # superpyth makuznet@gmail.com T1meism0ney
        python manage.py runserver 0.0.0.0:5000/admin # error 400

        cd conduit
            vi settings.py    
                ALLOWED_HOSTS = ['localhost', '127.0.0.1', 'http://makuznet-at-gmail-com-py.devops.rebrain.srwx.net']
                :wq
            cd ..
        
        python manage.py runserver 0.0.0.0:5000/admin # works makuznet@gmail.com T1meism0ney 

        cd conduit
            vi settings.py    
                STATIC_URL = '/static/'
                import os
                STATIC_ROOT = os.path.join(BASE_DIR, 'static/')
                :wq
            cd ..

        python manage.py collectstatic

        pip install gunicorn
        gunicorn --bind 0.0.0.0:8000 conduit.wsgi # access without css to makuznet-at-gmail-com-py.devops.rebrain.srwx.net/admin

        
        apt -y install nginx letsencrypt
        sudo letsencrypt certonly --webroot -w /var/www/html -d makuznet-at-gmail-com-py.devops.rebrain.srwx.net -m makuznet@gmail.com --agree-tos

ansible-playbook -i terraform-do/inventory.yml playbooks/main.yml
```        
### Letsencrypt
```bash
sudo apt -y install letsencrypt
```
#### getting an ssl certificate
```bash
sudo letsencrypt certonly --webroot -w /var/www/html -d makuznet-at-gmail-com-py.devops.rebrain.srwx.net -m makuznet@gmail.com --agree-tos
```
#### backing up /etc/letsencrypt
```bash
scp -r root@makuznet-at-gmail-com-py.devops.rebrain.srwx.net:/etc/letsencrypt ~/Documents/rebrain/python-deploy/
```

## Acknowledgments
This repo was inspired by [rebrainme.com](https://rebrainme.com) team

## See also 
- [RealWorld demo](https://demo.realworld.io/#/)
- [Django RealWorld example app](https://github.com/gothinkster/django-realworld-example-app)
- [pyenv](https://github.com/pyenv/pyenv)
- [python manage.py runserver: ADD TO ALLOWED_HOSTS](https://stackoverflow.com/questions/44184268/django-invalid-http-host-header-testserver-you-may-need-to-add-utestserver/44184583)
- [Digitalocean Django with Postgres, Nginx, and Gunicorn](https://www.digitalocean.com/community/tutorials/how-to-set-up-django-with-postgres-nginx-and-gunicorn-on-ubuntu-18-04)
- []()

## License
Follow all involved parties licenses terms and conditions.