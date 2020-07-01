Initially installation
```
apt-get update && apt-get upgrade
apt-get install git nginx libpq-dev
```

Installing RVM and Ruby
```
curl -sSL https://rvm.io/mpapis.asc | gpg --import -
curl -sSL https://rvm.io/pkuczynski.asc | gpg --import -
curl -sSL https://get.rvm.io | bash -s stable
source /etc/profile
rvm install 2.6.6 && rvm use 2.6.6
```

Installing Redis
```
wget http://download.redis.io/releases/redis-6.0.4.tar.gz
tar xzf redis-6.0.4.tar.gz
cd redis-6.0.4
make
```

Installing NVM
```
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
nvm install 12.16.3
```

Installing Yarn
```
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
apt update && apt install --no-install-recommends yarn
```

Installing PostgreSQL
```
sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
apt-get update
apt-get install postgresql
```
