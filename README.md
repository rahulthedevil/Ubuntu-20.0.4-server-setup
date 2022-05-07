# Ubuntu-20.0.4-server-setup

## Bash codes that I use to install things for the server

```bash
sudo apt update
sudo apt install nginx
```

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
```
or
```bash
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
```

```bash
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
```

```bash
nvm install --lts
```

```bash
npm install pm2 -g
```

## Git auto deployment using hooks

### In server
```bash
cd /var mkdir repo && cd repo mkdir site.git && cd site.git git init --bare
cd hooks
cat > post-receive
#!/bin/sh git --work-tree=/var/www/domain.com --git-dir=/var/repo/site.git checkout -f

chmod +x post-receive
```

### In local
```bash
cd /my/workspace mkdir project && cd project git init
git remote add live ssh://user@mydomain.com/var/repo/site.git
git add . git commit -m "My project is ready"
git push live master
```
