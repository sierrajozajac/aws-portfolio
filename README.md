# aws-portfolio

To ssh into instance
```
cd C:\
ssh -i "web-key-pair.pem" ubuntu@ec2-35-93-135-127.us-west-2.compute.amazonaws.com
```
Get apache on instance
```
sudo -i
apt-get update -y
apt-get install apache2 -y
```

Create HTMl file
```
cd /var/www/html
touch index.hmtl
vi index.html
```

Enable and start the apache service
```
systemctl enable apache2
systemctl start apach2
```
