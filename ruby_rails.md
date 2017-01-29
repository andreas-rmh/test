# Ruby
## Install
```bash
apt-get install git-core curl zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev python-software-properties libffi-dev

# From source
- Download sources
./configure 
make && make install

cd ext/zlib
ruby extconf.rb
make && make install

- Same for ext/openssl


## Install with ruby-install
wget -O ruby-install-0.6.0.tar.gz https://github.com/postmodern/ruby-install/archive/v0.6.0.tar.gz
tar -xzvf ruby-install-0.6.0.tar.gz
cd ruby-install-0.6.0/
sudo make install

mkdir /opt/rubies
ruby-install --rubies-dir /opt/rubies --latest ruby 2.3.1

## Use with chruby
wget -O chruby-0.3.9.tar.gz https://github.com/postmodern/chruby/archive/v0.3.9.tar.gz
tar -xzvf chruby-0.3.9.tar.gz
cd chruby-0.3.9/
make install

cat >> ~/.$(basename $SHELL)rc <<EOF
source /usr/local/share/chruby/chruby.sh
source /usr/local/share/chruby/auto.sh
EOF

exec $SHELL 

# Rails 
## Install (rails-5.0.0.rc1)
gem install rails --pre --no-ri --no-rdoc

## Create project
rails new myapp --database=postgresql
```
