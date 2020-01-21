# wpcfForDPS
Steps to Create Dharpara Primary School Website


Log into AWS console
From the drop down menu, select Cloudformation
Click on CREATE STACK (With new resources)
select "Use sample template" 
select "Wordpress Blog - with a local MySQL for storage"   
Specify stack details
Configure Stack options
Review before provisioning stack
Click Create stack

After stack was successfully created, click on outputs option and Click on the website url. It contains a message about  older PHP version
To update the php, SSH into Ec2 server and enter the following script one after another: 


Sudo su
yum update -y
yum install httpd php php-mysql -y
cd /var/www/html
echo "healthy" > healthy.html
wget https://wordpress.org/wordpress-5.1.1.tar.gz
tar -xzf wordpress-5.1.1.tar.gz
cp -r wordpress/* /var/www/html/
rm -rf wordpress
rm -rf wordpress-5.1.1.tar.gz
chmod -R 755 wp-content
chown -R apache:apache wp-content
wget https://s3.amazonaws.com/bucketforwordpresslab-donotdelete/htaccess.txt
mv htaccess.txt .htaccess
chkconfig httpd on
service httpd start


After running the script, go back to Cloudformation and click on outputs and click on the link again, It will forward to a wordpress.com site to log in. Where user will be able to customize the website.  


