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

## Troubleshooting
### Unable to connect
* Make sure to execute the command `dcup`
* Check for any error in the code with `dclf api`

## Zsh alias
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