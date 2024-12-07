# aws-portfolio

## Setting up the EC2 instance
Login to the AWS EC2 Console at https://console.aws.amazon.com/ec2/ . \
In this example, I setting up an ubuntu instance. Memory can be decided according to the needs of your project. 
### Port information needed. 
- Port 22 (SSH): Essential for remote access to the EC2 instance using SSH.
- Port 80 (HTTP): Used for standard HTTP web traffic. 
- Port 443 (HTTPS): Used for secure HTTPS web traffic. 
### Allocate elastic IP address. 
You can do so by selecting 'Actions' in the top right of the EC2 Console and navigating to Networking > Associate Elastic IP.
## Set up the web server on the EC2 instance (Apache)
### To ssh into instance
```
cd C:\
ssh -i "web-key-pair.pem" ubuntu@ec2-35-93-135-127.us-west-2.compute.amazonaws.com
```
### Get apache on instance
```
sudo -i
apt-get update -y
apt-get install apache2 -y
```
### Create HTML file
```
cd /var/www/html
touch index.hmtl
vi index.html
```
### Enable and start the apache service
```
systemctl enable apache2
systemctl start apache2
```
You will now have the Apache Ubuntu Default Page hosted on your EC2 instance.
## Connect Route 53 url to EC2 web server
Copy your IPv4 address from your EC2 instance. \
Open the Route 53 console at https://console.aws.amazon.com/route53/ . \
In the navigation pane, choose 'Hosted zones'. \
Select 'Create record'. \
Specify the following values: 
- Routing policy
  - Choose the applicable routing policy. For more information, see Choosing a routing policy.
- Record name
  - Enter the domain name that you want to use to route traffic to your EC2 instance. The default value is the name of the hosted zone.
  - For example, if the name of the hosted zone is example.com and you want to use acme.example.com to route traffic to your EC2 instance, enter acme.
- Value/Route traffic to
  - Choose IP address or another value depending on the record type. Enter the IPv4 address we copied from your EC2 instance earlier.
- Record type
  - Choose A – IPv4 address.
- TTL (seconds)
  - Default value of 300.
## Connecting CodePipeline
### CodeCommit
As of July 25, 2024, new customers are no longer able to sign up for AWS CodeCommit. Existing customers can continue to use the service as normal.
### CodeBuild
