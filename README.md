# Travel Memory Application on AWS

### Objective:

 - Set up the backend running on Node.js.

 - Configure the front end designed with React.

 - Ensure efficient communication between the front end and back end.

 - Deploy the full application on an EC2 instance.

 - Facilitate load balancing by creating multiple instances of the application.

 - Connect a custom domain through Cloudflare.

<img width="1521" height="744" alt="image" src="https://github.com/user-attachments/assets/2212c39c-eb0e-4219-ad28-f7bc257a3ac0" />

    "shortDescription":"India is a wonderful country with rich culture and good people.",
    "featured": true
}
```
Step1 - Setting up the EC2 instances for Frontend & Backend
Create the 2 EC2 instances (instance type - t2.micro), One is for the frontend and the other is for the backend.

Do the configuration of each instances at the time of creation using below script

#!/bin/bash 
sudo apt update
sudo bash
curl -s https://deb.nodesource.com/setup_18.x | sudo bash
sudo apt install nodejs -y
sudo cd /home/ubuntu/
sudo git clone https://github.com/UnpredictablePrashant/TravelMemory


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
