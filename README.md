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

Step2 - Setting up the Frontend & Backend individually

For frontend, you need to create `.env` file and put the following content (remember to change it based on your requirements):
```bash
REACT_APP_BACKEND_URL=http://localhost:3001
```

## How to run BE

Note: Make sure you have the .env file already added
```bash
cd backend
npm install
node index.js
```

## How to run FE
Note: Make sure you have the .env file already added
```bash
cd frontend
npm install
npm start
```
