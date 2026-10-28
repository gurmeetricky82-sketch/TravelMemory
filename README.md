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

Now we can access the backend at port 80 because of the reverse proxy

<img width="1364" height="290" alt="image" src="https://github.com/user-attachments/assets/eea2df32-eadb-4b52-8e44-705a7fef88a4" />

## Frontend Reverse proxy configuration

Follow the same steps as we did in Backend reverse configuration After doing that frontend will be running at port 80

<img width="1910" height="1204" alt="image" src="https://github.com/user-attachments/assets/2cf69fcc-4cf1-4e69-9a6e-344db4f6a146" />

## Step4 - Scaling the Appliacation

Create multiple instances of both the frontend and backend servers.

Add these instances to a load balancer to ensure efficient distribution of incoming traffic.

Launching the extra instances to distribute the load using taking snapshots of frontend & backend both.

<img width="2242" height="686" alt="image" src="https://github.com/user-attachments/assets/0b5ab33c-3dae-429c-b19b-98ef50b91c3c" />
<img width="2768" height="1212" alt="image" src="https://github.com/user-attachments/assets/8349ab4c-c92b-41d3-a03d-503823e6a27a" />

You can find the snapshots in AMIs (Amazon Machine Images)
<img width="2748" height="530" alt="image" src="https://github.com/user-attachments/assets/0fde0fd7-1c94-44f3-8119-50131df3cdcf" />
<img width="2782" height="1082" alt="image" src="https://github.com/user-attachments/assets/6a3e9d68-a89b-4c14-8d09-7b1a4ea50ed6" />

Then will be launching the instance using the AMIs we have saved earlier.
<img width="2832" height="1228" alt="image" src="https://github.com/user-attachments/assets/6e8a59c7-90f0-428e-b222-72f1679651f3" />

## Frontend
<img width="2766" height="1210" alt="image" src="https://github.com/user-attachments/assets/d47ba734-fdc4-443a-b26b-2ea2a235f425" />

<img width="2136" height="1166" alt="image" src="https://github.com/user-attachments/assets/ec350cf0-a767-4826-b1aa-224d8feeb529" />
<img width="2280" height="1132" alt="image" src="https://github.com/user-attachments/assets/47755cfd-7e26-414e-b5af-6fb669e7b76c" />

We are able to see the same data and configuration.
<img width="1560" height="1146" alt="image" src="https://github.com/user-attachments/assets/30d79d2d-1b70-44ea-9c54-1178a46ccf5c" />
<img width="1658" height="322" alt="image" src="https://github.com/user-attachments/assets/df46544f-a1e3-4b83-81cd-1a77f058d008" />

For Load balancing we need to create Target Groups to collect the instances of frontend ( i.e adarsh_mern_frontend & adarsh_mern_frontend2) and backend (adarsh_mern_backend & adarsh_mern_backend2)

EC2 > Target groups > Create target group

<img width="2368" height="1188" alt="image" src="https://github.com/user-attachments/assets/dc4ccc9c-80b3-4e6f-843d-c2fa17163712" />
<img width="2394" height="1188" alt="image" src="https://github.com/user-attachments/assets/b037d0c0-7c1c-4b46-942e-9dd599c4c3af" />
<img width="2756" height="386" alt="image" src="https://github.com/user-attachments/assets/894559de-cfa9-4f4f-a0bf-aee89d1937f2" />

For creating the load balancer based on target groups

EC2 > Load balancers > Create Application Load Balancer

<img width="2368" height="1234" alt="image" src="https://github.com/user-attachments/assets/16bfd7fb-5007-45ed-997c-5a8c54b74b74" />

balancer is mapped to multi AZs
<img width="2140" height="730" alt="image" src="https://github.com/user-attachments/assets/b8431ceb-bfcc-45e4-a787-85435eec918b" />

Adding the Target group we have created for the backend instances.

<img width="2362" height="574" alt="image" src="https://github.com/user-attachments/assets/5f122445-8873-48fd-844a-af3c349be38f" />

Same for the Frontend Loadbalancer

<img width="2646" height="1116" alt="image" src="https://github.com/user-attachments/assets/63732c29-992f-4093-86d5-7a64aba1642c" />
<img width="2600" height="1226" alt="image" src="https://github.com/user-attachments/assets/4e482e24-6f52-47aa-9d07-471602b12ef0" />
<img width="2620" height="1218" alt="image" src="https://github.com/user-attachments/assets/0f6cf0af-926c-4ac2-9386-915ff04256b2" />

Both the Load Balancers are active.









