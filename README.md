# Create react app and deploy it for development and production environment on the EC2 instance

#### Description:

- Launch an EC2 server.
- Install the dependencies to run the react app.
- Create a react app and deploy it on the server for development and production environment.

#### Step-1: Launch an EC2 server

Firstly, log in to the AWS management console.

![Img-1](https://user-images.githubusercontent.com/74168188/178555843-f062573f-166c-4b06-b947-d2d11da46507.png)

After login, navigate to the search bar, type EC2, and select EC2

![Img-2](https://user-images.githubusercontent.com/74168188/178555883-5e169bfd-d205-4b99-9992-8dca7e957ff2.png)

Now, the EC2 dashboard will appear. Click Instances

![Img-3](https://user-images.githubusercontent.com/74168188/178555921-6213742a-726c-4532-923e-3edc4c4d1413.png)

Click the Launch instances button.

![Img-4](https://user-images.githubusercontent.com/74168188/178555939-529e74f0-6ece-43dc-aa1c-98d6b7f2deda.png)

To launch an EC2 instance, a few details are required, i.e., instance name, OS image (AMI), instance type, etc.

![5](https://user-images.githubusercontent.com/74168188/179711692-29904cac-6b33-4876-9fb0-07a4765d4d82.png)
![Img-6](https://user-images.githubusercontent.com/74168188/178556050-f90b180a-0dca-48fb-b30b-8365f9ac8f28.png)
![Img-7](https://user-images.githubusercontent.com/74168188/178556073-b0a18233-2e38-4dbd-926d-f7e411f7fa06.png)

Select a key pair to attach with the instance to log in with that key. If you do not have key pair, then create a new key pair by clicking Create a new key pair. Moreover, according to usage, download key pair in .pem or .ppk format.

![8](https://user-images.githubusercontent.com/74168188/179713553-227871ba-db62-496f-b361-2cf1ef3ff50e.png)

Now, to allow traffic from the internet, we need to create a rule in network settings.

![9](https://user-images.githubusercontent.com/74168188/179716719-a040568f-8b89-43df-817c-f39b35b19337.png)

We are good to go to launch an instance for this. Click the Launch instance button. If everything is correctly set up, you will find a success message on the screen. Click on the instance id to navigate to the EC2 dashboard.

![Img-11](https://user-images.githubusercontent.com/74168188/178556301-ac2e5bdd-7efa-4ad4-99d9-b669e599eefd.png)

Now, take the public IP from the EC2 dashboard and use it to login inside the instance using ssh. First move to the directory where the key is downloaded. In my case it's in downloads directory.

![12](https://user-images.githubusercontent.com/74168188/179716794-50844da9-ac7d-4599-8d95-1e653f87d932.png)

Finally, it will be logged in successfully if everything is configured correctly.

#### Step-2: Install the dependencies to run the react app.

First, we need to install nodejs. npm comes with nodejs bundled. For nodejs, use below commands:
```
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt-get install -y nodejs
```

![13](https://user-images.githubusercontent.com/74168188/179720815-92a33f24-83a2-4aed-aa0c-a5fa0b7c28bf.png)
![14](https://user-images.githubusercontent.com/74168188/179720992-b54165f1-65d8-4a96-838c-1ddaa744bc12.png)
![15](https://user-images.githubusercontent.com/74168188/179721130-662d3cd1-a868-4779-a976-db75d49f2c63.png)
![16](https://user-images.githubusercontent.com/74168188/179741220-996e1ba3-f774-46e2-84ba-790513ae1ccb.png)

To check nodejs is successfully installed or not use ```node -v```

![17](https://user-images.githubusercontent.com/74168188/179741532-8f2e1597-a542-4693-ae08-facd3d630b2b.png)

Also, npm is already installed.

![18](https://user-images.githubusercontent.com/74168188/179742147-b31454f7-ddcb-42c0-8cb6-7197600e82a8.png)

As you can see npm version is 8.13.2 but latest version is 8.14.0 so we have to update npm version using ```sudo npm install -g npm@8.14.0```

![19](https://user-images.githubusercontent.com/74168188/179751261-b2900fad-593b-4e56-98d1-29ab356ac6f3.png)

#### Step-3: Create a react app and deploy it on the server for development and production environment.

Now, time to create a react app

But before this create a directory with any name then move to that directory after this run ```sudo npx create-react-app <APP_NAME>```
If we run command from /home/ubuntu/ then might get error of permission denied.

![20](https://user-images.githubusercontent.com/74168188/179753396-664262cb-97c3-42ed-b64c-eac91265298c.png)
![21](https://user-images.githubusercontent.com/74168188/179753481-d2dbd6ae-7ea5-46ad-a6fd-9b74a27bd0ff.png)

So, to deploy for development environment enter to directory with APP_NAME then run ```sudo npm start```

![22](https://user-images.githubusercontent.com/74168188/179756353-d66bd029-0c4e-4686-8e16-15938f175b7c.png)
![23](https://user-images.githubusercontent.com/74168188/179756429-44f20508-d324-43cc-970f-4aaff5de8e02.png)
![24](https://user-images.githubusercontent.com/74168188/179756440-9f709120-e3fb-4ea4-80c8-b551d063b4de.png)

As mentioned in above screenshot, locally it can be accessed by hitting **http://localhost:3000** and **http://INSTANCE_PRIVATE_IP:3000** but to provide access to developer we have two options: 

  #### Option-1:
  We have to create a rule in security group for port no. 3000 after that it can be accessed using **INSTANCE_PUBLIC_IP:3000**
  
  For this click **Security** as show in screenhot below then on secuity group that start from **sg-......**
  
  ![25](https://user-images.githubusercontent.com/74168188/179758967-76e85786-dc66-433a-89b8-2bee52a43c12.png)
  
  Here, click **Edit inbound rules** then on **Add rule**
  
  ![26](https://user-images.githubusercontent.com/74168188/179759062-c29fcf22-e5da-4508-9d9d-adc338039067.png)
  ![27](https://user-images.githubusercontent.com/74168188/179759294-f978d884-caa9-40ad-a764-4e96bdf1acf9.png)
  
  add rule for 3000 port from anywhere i.e. 0.0.0.0/0 then click **Save rules**
  
  ![28](https://user-images.githubusercontent.com/74168188/179760275-4b1e1549-ecb7-497a-8306-a1b6f4e11cc3.png)
  
  Now try to hit ```<INSTANCE_PUBLIC_IP>:3000```
  
  ![29](https://user-images.githubusercontent.com/74168188/179760337-0eaa2956-f798-49ca-ba1b-0db96d1d0ded.png)
  
  As you can see we can able to access remotely.
  
  #### Option-2:
  We can use nginx reverse proxy
  
  For this, install nginx using ```sudo apt install nginx -y``` but before this update the list of packages using ```sudo apt update```
  
  ![30](https://user-images.githubusercontent.com/74168188/179898309-322485e9-f2ce-419e-9746-365c14020b4d.png)
  ![31](https://user-images.githubusercontent.com/74168188/179898391-38c72a4f-4bd3-4226-a02f-fa95a0bbacbb.png)
  
  To check nginx is successfully installed or not use ```nginx -v```
  
  ![32](https://user-images.githubusercontent.com/74168188/179899358-0d5122d6-0d63-40e6-b4fe-6a539ce7d92c.png)
  
  Now, let's do reverse proxy. For this, create a conf file inside **/etc/nginx/sites-available/** directory with any name
  
  Here what we will do copy the default conf file with any name then make changes accordingly
  
  ![33](https://user-images.githubusercontent.com/74168188/179900145-2df1fda8-6955-460a-8317-b3049eb24c6c.png)
  
  Now press i to insert then comment unessary things and add below part in server block then press Esc key and type ```:wq!``` to write and quit.
  ```
  location / {
                proxy_pass http://localhost:3000;
  }
  ```
  ![34](https://user-images.githubusercontent.com/74168188/179904980-d1d57de0-4a79-45e2-94b0-095f2ab7ffdc.png)
  ![35](https://user-images.githubusercontent.com/74168188/179905013-bca9590a-9d04-4ed7-82f6-37aed0a65a54.png)
  
  Next, let's enable the file by creating a link from sites-available to the sites-enabled directory, which Nginx reads from during startup:
  
  ![36](https://user-images.githubusercontent.com/74168188/179904340-0e774f38-172e-45a3-be65-311e9a5d4cca.png)
  
  To check that there are no syntax errors in any of your Nginx files, use ```sudo nginx -t```
  
  ![37](https://user-images.githubusercontent.com/74168188/179906269-9afbb7a4-574b-4c6f-8474-477e8be16d55.png)
  
  Time to restart Nginx server using ```sudo systemctl restart nginx```
  
  ![38](https://user-images.githubusercontent.com/74168188/179905887-083ee32a-62ec-48ed-9923-4d90e661097f.png)
  
  Before hitting EC2_PUBLIC_IP:81 don't forgot to run ```sudo npm start``` to start server for dev env.
  
  ![42](https://user-images.githubusercontent.com/74168188/179915576-4bcbf06a-125a-469f-8827-01402af84b04.png)
  ![43](https://user-images.githubusercontent.com/74168188/179915597-eb2f0cc8-937b-4fb3-a646-22b09038da9e.png)
  ![44](https://user-images.githubusercontent.com/74168188/179915620-df5d33c7-215b-43f1-bbf1-7f0062c1d2a5.png)
  
  Now, let's try to hit EC2_PUBLIC_IP:81
  
  ![39](https://user-images.githubusercontent.com/74168188/179906298-015b521a-16e1-4491-b09b-694cec69aa2e.png)
  
  As you can see we are not getting the result one thing we missed is we have not created a firewall rule for port no. 81.
  
  For this navigate to security group attached with instance then click **Edit inbound rules** then on **Add rule** after that click **Seve rules**
  
  ![40](https://user-images.githubusercontent.com/74168188/179907946-04f16832-2b69-4c39-9876-f44542d07535.png)
  ![41](https://user-images.githubusercontent.com/74168188/179915063-0810447d-950b-42f6-83a3-65a5b035122f.png)
  
  As you can see its working fine we are getting results.
  
  ![45](https://user-images.githubusercontent.com/74168188/179916307-c4bc42a3-e76e-4ada-8a3e-91de145b0067.png)
  
Now, to deploy for production environment enter to directory with APP_NAME then run ```sudo npm run build``` it will create a build folder.

Copy all files from build directory to ```/var/www/html/```

![47](https://user-images.githubusercontent.com/74168188/179917987-573fb14d-b6c4-43f2-b64a-69adb5f2aab7.png)

Again we also have to create firewall rule for port 80 as http works on port 80.

![48](https://user-images.githubusercontent.com/74168188/179918392-bdc6b353-03d4-4623-8334-29fd44b0c37a.png)

Now, try to hit EC2_PUBLIC_IP:80 or only EC2_PUBLIC_IP

![49](https://user-images.githubusercontent.com/74168188/179918624-b2a53a67-ada7-4a67-91a8-01b709893450.png)

### Thank you
