 apt install apache2 apache2-utils
In browser http://localhost/
apt -y install subversion subversion-tools libapache2-mod-svn
go to path: ---/etc/apache2/mods-enabled
vim dav_svn.conf
set password for admin user:-------htpasswd -cm /etc/apache2/dav_svn.passwd admin
create a repo---- mkdir /opt/svn
svnadmin create /opt/svn/
chown -R www-data:www-data /opt/svn/
in browser ----http://localhost/svn/Testrepo/
svn checkout http://localhost/svn/Testrepo/ /home/bandaru/Music/Application1/
svn add Application1
svn import -m "adding new application" /home/bandaru/Music/Application1/ http://localhost/svn/Testrepo/
