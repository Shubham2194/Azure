#Lets integrate Sonar Qube with Report plugin With Azure-devOps


Step1 :
Create a VM and configure SOnarqube as Docker container 

ssh to the VM
mkdir sonarqube && nano deploy-sonar.sh
'''sh
#!/bin/bash

docker run -itd --name sonar-devops -p 9000:9000 sonarqube:lts-community
'''

Step2 :  Check if its running
docker ps

![image](https://github.com/user-attachments/assets/1f3da6a2-a07d-4b47-800c-a2801e96a970)

Step 3: 
Setup reverse proxy ,certbot and DNS

- sudo apt install nginx -y
- sudo nano /etc/nginx/sites-available/default  and add nginx file:
'''yaml
server {
       listen [::]:80;
       server_name xyz.subdomain.com;

    location / {
        proxy_pass http://localhost:9000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}


'''
We need to map the subdomain name with our DNS now(we are using route 53)
Find your server IP by: 
curl ifconfig.me (copy the IP) and Goto route53 console
Create an A record and add Subdomain name and IP in value


![image](https://github.com/user-attachments/assets/a1287c96-6564-4b6f-bfc4-cb6de60554da)


Now lets install install certbot for free certificate installation on subdomain

RUN :
sudo apt-get install certbot -y &&  sudo apt-get install python3-certbot-nginx -y
After the installation ,configure Certificate 
RUN : sudo certficate and complete the asked queries

![image](https://github.com/user-attachments/assets/5264fdfb-8ad6-4974-83d3-0112413b80a8)

It will deploy cert on the choosen subdomain

Step 4: 
Lets access sonarqube on subdomain

![image](https://github.com/user-attachments/assets/609cc985-6b17-4bc5-9642-36f365c58df5)

Intially the username and password will be
admin
admin
Then change the password

We have Configured sonarqube !!


Step 5:
Install sonarqube plugin on azure devops

Go to azure devops console 

Marketplace > browse marketplace

![image](https://github.com/user-attachments/assets/390df439-ef74-4633-9ffd-60fba34d6229)


Search for sonar and install it for free and choose you organistaion where you want to configure Sonar plugin

![image](https://github.com/user-attachments/assets/8a9d1ef7-240c-47b3-aabf-d2ce7e973424)

