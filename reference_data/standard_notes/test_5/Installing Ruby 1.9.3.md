### Install essentials:

sudo apt-get update -y
sudo apt-get install build-essential zlib1g-dev libssl-dev libreadline-dev  git-core curl libyaml-dev libcurl4-dev libsqlite3-dev apache2-dev -y
sudo apt-get install apache2-prefork-dev libapr1-dev libaprutil1-dev

### Remove existing versions of Ruby:

sudo rm -rf /opt/ruby

curl --remote-name http://ftp.ruby-lang.org/pub/ruby/1.9/ruby-1.9.3-p194.tar.gz
tar zxf ruby-1.9.3-p194.tar.gz
cd ruby-1.9.3-p194/
sudo ./configure
sudo make
sudo make install