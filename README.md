####################### Splunk Configuration on Server  ##############################

--------> Download splunk credentials (splunkclouduf.spl) fromsplunk cloud and store it on your server

sudo -i

wget -O splunkforwarder-9.4.1-e3bdab203ac8.x86_64.rpm "https://download.splunk.com/products/universalforwarder/releases/9.4.1/linux/splunkforwarder-9.4.1-e3bdab203ac8.x86_64.rpm"

sudo rpm -i splunkforwarder-9.4.1-e3bdab203ac8.x86_64.rpm

sudo /opt/splunkforwarder/bin/splunk enable boot-start

sudo /opt/splunkforwarder/bin/splunk start

sudo /opt/splunkforwarder/bin/splunk status

sudo aws s3 cp s3://marketplace-ui123/splunkclouduf.spl  /opt/splunkclouduf.spl

sudo /opt/splunkforwarder/bin/splunk install app /opt/splunkclouduf.spl -auth <username:password>

sudo /opt/splunkforwarder/bin/splunk restart

sudo /opt/splunkforwarder/bin/splunk add monitor -auth <username:password> /var/log/springboot


####################### Splunk Removal from Server  ##############################

ps aux | grep splunk

sudo pkill -f splunk

sudo rm -rf /opt/splunkforwarder

sudo rm -f /opt/splunkclouduf.spl
sudo rm -f /etc/init.d/splunk
sudo rm -f /etc/systemd/system/SplunkForwarder.service

id splunk && sudo userdel -r splunk

ps aux | grep splunk

rpm -qa | grep splunk

rm splunkforwarder-9.4.1-e3bdab203ac8.x86_64.rpm
