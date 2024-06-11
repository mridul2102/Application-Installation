
## Nagios Installation

```bash
sudo su
yum install httpd php -y
yum install gcc glibc glibc-common -y
yum install gd gd-devel -y
adduser -m nagios
groupadd nagioscmd
usermod -a -G nagioscmd nagios
usermod -a -G nagioscmd apache
mkdir ~/downloads
cd ~/downloads
wget https://assets.nagios.com/downloads/nagioscore/releases/nagios-4.0.8.tar.gz
wget https://nagios-plugins.org/download/nagios-plugins-2.0.3.tar.gz
tar zxvf nagios-4.0.8.tar.gz
cd nagios-4.0.8
./configure --with-command-group=nagioscmd
make all
make install
make install-init
make install-config
make install-commandmode
make install-webconf
service httpd restart
cd ~/downloads
tar zxvf nagios-plugins-2.0.3.tar.gz
cd nagios-plugins-2.0.3
./configure --with-nagios-user=nagios --with-nagios-group=nagios
make
make install
chkconfig --add nagios
chkconfig nagios on
/usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg
service nagios start
service httpd restart
echo "nagios is installed"

```
