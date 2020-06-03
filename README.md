Initially installation
```
apt-get update && apt-get upgrade
apt-get install git nginx
```

Installing RVM and Ruby
```
curl -sSL https://rvm.io/mpapis.asc | gpg --import -
curl -sSL https://rvm.io/pkuczynski.asc | gpg --import -
curl -sSL https://get.rvm.io | bash -s stable
source /etc/profile
rvm install 2.6.6 && rvm use 2.6.6
```
