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

su - postgres
psql
create user animelib_development;
create user animelib_production;
create user animelib_test;
alter user animelib_development createdb;
alter user animelib_production createdb;
alter user animelib_test createdb;
alter user animelib_development with superuser;
alter user animelib_production with superuser;
alter user animelib_test with superuser;
alter user animelib_development with password 'XXXX';
alter user animelib_production with password 'XXXX';
alter user animelib_test with password 'XXXX';
```
Setting Up Nginx
```
server {
    listen 443 ssl http2;
    client_max_body_size 1G;
    server_name animelib.ru;
    keepalive_timeout 5;
    ssl_certificate /etc/ssl/animelib.crt;
    ssl_certificate_key /etc/ssl/animelib.key;
    root /root/animelib/public;
    try_files $uri/index.html $uri.html $uri @myapp;

    location @myapp {
        proxy_pass http://unix:/root/animelib/tmp/sockets/unicorn.socket;
        proxy_set_header  Host $http_host;
        proxy_set_header  X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header  X-Forwarded-Proto $scheme;
        proxy_set_header  X-Forwarded-Ssl on;
        proxy_set_header  X-Forwarded-Port $server_port;
        proxy_set_header  X-Forwarded-Host $host;
        proxy_redirect off;
    }

    error_page 500 502 503 504 /500.html;
    location = /500.html {
        root /root/animelib/public;
    }
}
```
