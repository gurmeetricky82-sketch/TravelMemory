# Travel Memory Application on AWS

### Objective:

 - Set up the backend running on Node.js.

 - Configure the front end designed with React.

 - Ensure efficient communication between the front end and back end.

 - Deploy the full application on an EC2 instance.

 - Facilitate load balancing by creating multiple instances of the application.

 - Connect a custom domain through Cloudflare.

<img width="1521" height="744" alt="image" src="https://github.com/user-attachments/assets/2212c39c-eb0e-4219-ad28-f7bc257a3ac0" />

  
## Step1 - Setting up the EC2 instances for Frontend & Backend

Create the 2 EC2 instances (instance type - t2.micro), One is for the frontend and the other is for the backend.

Do the configuration of each instances at the time of creation using below script

```
#!/bin/bash 
sudo apt update
sudo bash
curl -s https://deb.nodesource.com/setup_18.x | sudo bash
sudo apt install nodejs -y
sudo cd /home/ubuntu/
sudo git clone https://github.com/UnpredictablePrashant/TravelMemory
```
<img width="1806" height="1118" alt="image" src="https://github.com/user-attachments/assets/c8492c70-0a20-4496-b1f4-17df65ac68e5" />
<img width="1876" height="862" alt="image" src="https://github.com/user-attachments/assets/52fe8817-cf46-4100-8066-58a22f525b28" />
<img width="1360" height="922" alt="image" src="https://github.com/user-attachments/assets/1ba495df-3aee-4fa7-9bba-036386682903" />

The Backend instances is up and running with:

Public IP 3.7.252.19
Private IP 172.31.15.182
Availability zone: ap-south-1
<img width="2208" height="878" alt="image" src="https://github.com/user-attachments/assets/059a1134-def7-4862-8ad6-7faca1cab5b5" />

The Frontend instances is up and running with

Public IP 13.203.228.5
Private IP 172.31.0.246
Availability zone: ap-south-1

<img width="2240" height="1124" alt="image" src="https://github.com/user-attachments/assets/e06e8ebe-a709-40a2-8b22-4aa4b390494b" />

The configuration we have done in both instances is successful as we can see the repo gets cloned.

## Step2 - Setting up the Frontend & Backend individually

Frontend Configuration

cd /home/ubuntu/TravelMemory/frontend
sudo npm install
nano src/url.js
export const baseUrl = "http://[backend IP]"

<img width="1534" height="202" alt="image" src="https://github.com/user-attachments/assets/8156e22b-9045-494d-ba33-a526c9b566fb" />

sudo npm start   

The frontend application is running at port 3000
<img width="950" height="444" alt="image" src="https://github.com/user-attachments/assets/21f50d33-00a8-4615-b518-6aaeb760d980" />

## Backend Configuration

cd /home/ubuntu/TravelMemory/backend/
nano .env
MONGO_URI='mongodb+srv://adarsh307kumar:<password>@travelmemory.wxwkpag.mongodb.net/travelmemory'
PORT=3000
sudo npm install

<img width="1700" height="172" alt="image" src="https://github.com/user-attachments/assets/dc94c432-7f38-460d-a649-a9d358ba5114" />

sudo node index.js  

The backend application at port 3000

<img width="2220" height="998" alt="image" src="https://github.com/user-attachments/assets/c31ff32e-655c-4c59-a12c-ab52e4cb6976" />

## Step3 - Setting up Reverse Proxy for the Frontend & Backend Both
## Backend Reverse proxy configuration

We are doing the reverse proxy using Nginx

sudo apt install nginx

sudo systemctl status nginx 

<img width="2328" height="790" alt="image" src="https://github.com/user-attachments/assets/75ff4fac-6ee0-4f41-9954-39a8336d1057" />
<img width="2334" height="786" alt="image" src="https://github.com/user-attachments/assets/3c6fbe4e-f270-4a19-854c-7851827f3446" />

<img width="1886" height="428" alt="image" src="https://github.com/user-attachments/assets/3a706802-9242-439e-a249-8814240c68e9" />

Now for the reverse proxy

sudo unlink /etc/nginx/sites-enabled/default

cd /etc/nginx/sites-available/
sudo nano custom_server.conf
server { 
listen 80;
location / {
proxy_pass http://my_server;
}}

ln -s /etc/nginx/sites-available/custom_server.conf /etc/nginx/sites-enabled/custom_server.conf

sudo service nginx configtest

sudo service nginx restart

<img width="2666" height="460" alt="image" src="https://github.com/user-attachments/assets/d7d35f3d-ea9d-4772-820b-6c34e77d60d5" />


