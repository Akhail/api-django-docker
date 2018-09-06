# Real Estate API

## Django commands
* __dcup__: Run containers
* __dce api manage makemigrations__: Generate migrations from models
* __dce api manage migrate__: Create migrations on database
* __dce api manage shell__: Open interactive console ipython
* __dce api manage makemessages__: Generate i18n messages
* __dce api manage createsuperuser__: Create superuser

## Steps to launch local server
1. __dcup__: Run containers
2. __dce api manage migrate__: Create migrations on database
3. __dce api manage createsuperuser__: Create superuser
4. __dcrestart__: Sure reload the django server

## Steps to launch production server
1. Allow port 22, 80 and 443 on firewall
    1. `sudo ufw disable;`
    1. `sudo ufw reset;`
    1. `sudo ufw default deny incoming;`
    1. `sudo ufw default allow outgoing;`
    1. `sudo ufw allow OpenSSH; # is optional only for ssh`
    1. `sudo ufw allow 80/tcp;`
    1. `sudo ufw allow 443/tcp;`
    1. `sudo ufw status; # check port 22, 80, 443 is open`
    1. `sudo ufw enable;`
1. Create production env `cp example.env .env`
1. Change .config/uwsgi.ini project var to your project name
1. Create certificate with letsencrypt
1. Config your app in settings ALLOWED_HOSTS and set debug var with `os.getenv('DEBUG', False)`
1. Set your database settings with 
1. Run containers __pdcup api__ or __pdcup api db__ use postgres in docker
1. __pdce api manage collectstatic__: Collect statics files
1. __pdce api manage migrate__: Create migrations on database
1. __pdce api manage createsuperuser__: Create superuser *is optional*

### Postgres config
```python
    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.postgres',
            'NAME':  os.getenv('DB_NAME',os.path.join(BASE_DIR, 'db.sqlite3')),
            'USER':  os.getenv('DB_USER'),
            'PASSWORD': os.getenv('DB_PASS'),
            'HOST': os.getenv('DB_HOST'),
            'PORT': os.getenv('DB_PORT')
        }
    }
```
### Lets encrypt docker
```bash
docker run -it --rm --name certbot \  
    -v "/etc/letsencrypt:/etc/letsencrypt" \  
    -v "/var/lib/letsencrypt:/var/lib/letsencrypt" \  
    -p 80:80 -p 443:443 \  
    certbot/certbot certonly --standalone \  
    --email email@email.com \  
    --agree-tos -d domain -d www.domain
```

## Troubleshooting
### Unable to connect
* Make sure to execute the command `dcup`
* Check for any error in the code with `dclf api`

### Error 400 bad request
* Set correctly ALLOWED_HOSTS example `ALLOWED_HOSTS=['domain','domain2']`

### Internal Server Error
* View logs with pdcl (production), dcl (develop) and sure not raised exceptions

## Zsh alias develop
```bash

alias dco='docker-compose -f .docker/docker-compose.yml'
alias dcb='docker-compose -f .docker/docker-compose.yml build'
alias dce='docker-compose -f .docker/docker-compose.yml exec'
alias dcps='docker-compose -f .docker/docker-compose.yml ps'
alias dcrestart='docker-compose -f .docker/docker-compose.yml restart'
alias dcrm='docker-compose -f .docker/docker-compose.yml rm'
alias dcr='docker-compose -f .docker/docker-compose.yml run'
alias dcstop='docker-compose -f .docker/docker-compose.yml stop'
alias dcup='docker-compose -f .docker/docker-compose.yml up -d'
alias dcdn='docker-compose -f .docker/docker-compose.yml down'
alias dcl='docker-compose -f .docker/docker-compose.yml logs'
alias dclf='docker-compose -f .docker/docker-compose.yml logs -f'
alias dcpull='docker-compose -f .docker/docker-compose.yml pull'
alias dcstart='docker-compose -f .docker/docker-compose.yml start'

```

## Zsh alias develop
```bash

alias pdco='docker-compose -f .docker/docker-compose.yml -f .docker/docker-compose.override.yml'
alias pdcb='docker-compose -f .docker/docker-compose.yml -f .docker/docker-compose.override.yml build'
alias pdce='docker-compose -f .docker/docker-compose.yml -f .docker/docker-compose.override.yml exec'
alias pdcps='docker-compose -f .docker/docker-compose.yml -f .docker/docker-compose.override.yml ps'
alias pdcrestart='docker-compose -f .docker/docker-compose.yml -f .docker/docker-compose.override.yml restart'
alias pdcrm='docker-compose -f .docker/docker-compose.yml -f .docker/docker-compose.override.yml rm'
alias pdcr='docker-compose -f .docker/docker-compose.yml -f .docker/docker-compose.override.yml run'
alias pdcstop='docker-compose -f .docker/docker-compose.yml -f .docker/docker-compose.override.yml stop'
alias pdcup='docker-compose -f .docker/docker-compose.yml -f .docker/docker-compose.override.yml up -d'
alias pdcdn='docker-compose -f .docker/docker-compose.yml -f .docker/docker-compose.override.yml down'
alias pdcl='docker-compose -f .docker/docker-compose.yml -f .docker/docker-compose.override.yml logs'
alias pdclf='docker-compose -f .docker/docker-compose.yml -f .docker/docker-compose.override.yml logs -f'
alias pdcpull='docker-compose -f .docker/docker-compose.yml -f .docker/docker-compose.override.yml pull'
alias pdcstart='docker-compose -f .docker/docker-compose.yml -f .docker/docker-compose.override.yml start'

```