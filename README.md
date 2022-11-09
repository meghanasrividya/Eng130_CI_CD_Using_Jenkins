# Eng130_CI_CD_Using_Jenkins
Continuous_Integration and Continous_Delivery/Continuous_Deployement using Jenkins
### What is Continuous Integration?
- Continuous Integrationis the practice of automating the build and testing of code every time a change is made — and committing that code back to a central repository.
### What is Continuos Delivery?
- Continuous Delivery is an extension of continuous integration to make sure that you can release new changes to your customers quickly in a sustainable way. This means that on top of having automated your testing, you also have automated your release process and you can deploy your application at any point of time by clicking on a button. In continuous Delivery the deployment is completed manually.
### What is the differnce between Continuous Delivery and Continuous Deployment?
- Simply put, CI is the process of integrating code into a mainline code base. In almost all scenarios today, CI is done using platforms designed specifically for the purpose. Implementing CI is, therefore, as simple as using the right tools.

- CD is more complicated. CD is about the processes that have to happen after code is integrated for app changes to be delivered to users. Those processes involving testing, staging and deploying code. There is no single type of tool that does all these things. These processes take different forms, depending on the culture of the team and the type of app it is creating.

- In actuality, then, CI and CD share little in common. Besides starting with the same word (“continuous”) and being different stages in modern software delivery pipelines, they don’t have much to do with one another.

![image](https://user-images.githubusercontent.com/97250268/200538257-222a3c2d-4449-46a2-bc8e-b3fe164af909.png)
### What are Webhooks?
- Webhook triggers the job in the jenkins with every commit and push from 
### What are Jenkins Stages

- It contains a collection of states such as build, deploy, test and release. These jobs or events are interlinked with each other. Every state has its jobs, which work in a sequence called a continuous delivery pipeline.

### How Jenkins Work

![image](https://user-images.githubusercontent.com/97250268/200784187-9856f62e-7127-4273-b038-2a8eb61a9d62.png)
-  Let's see how Jenkins works. The above diagram is representing the following functions:

- First of all, a developer commits the code to the source code repository. Meanwhile, the Jenkins checks the repository at regular intervals for changes.
- Soon after a commit occurs, the Jenkins server finds the changes that have occurred in the source code repository. Jenkins will draw those changes and will start preparing a new build.
- If the build fails, then the concerned team will be notified.
- If built is successful, then Jenkins server deploys the built in the test server.
- After testing, Jenkins server generates a feedback and then notifies the developers about the build and test results.
- It will continue to verify the source code repository for changes made in the source code and the whole process keeps on repeating.

### Benefits of using Jenkins
- It is an open source tool.
- It is free of cost.
- It does not require additional installations or components.Means it is easy to install.
- Easily configurable.
- It supports 1000 or more plugins to ease your work. If a plugin does not exist, you can write the script for it and share with community.
- It is built in java and hence it is portable.
- It is platform independent. It is available for all platforms and different operating systems. Like OS X, Windows or Linux.
- Easy support, since it open source and widely used.
- Jenkins also supports cloud based architecture so that we can deploy Jenkins in cloud based platforms.


![image](https://user-images.githubusercontent.com/97250268/200540931-912c8678-2ef6-42c7-b25b-8b41b5d1ac2c.png)
### Steps for Jenkins Pipeline

![image](https://user-images.githubusercontent.com/97250268/200653970-3178764d-579e-4dd1-a738-da2b70a90d04.png)

- Step 1: Create a new ssh key pair called eng130_jenkins_meghana- copy eng130_jenkins_meghana
- Step 1:Create a new CICD pipeline
- Step 3: Generate a new ssh key pair (ensure to generate it in .ssh folder on local host)
- copy file.pub to github repo(will show in minute)
- copy private file in jenkins
- create a new job to test the CI

![image](https://user-images.githubusercontent.com/97250268/200655307-a7f7e077-ba6c-4b05-9218-223356931880.png)


### Steps to create new job in Jenkins

- Enter an item name
- Select the free style project and click on ok
- In the description - give the description  of the job
- Check/click on `Discard old builds` and enter 3 for `Max # of builds to keep`
- Check/click on GitHub project and give the `Project URL` copy the Https link from the github and paste here
- Under the `Office 365 Connector` click `Restrict where this project can be run` and give the label expression `sparta-ubuntu-node`
- Under the `Source Code Management` click on Git , copy the ssh url from the github and paste  here
- For Credentials click on Add and select `Kind` to `SSH Username with private Key`
- Give the username:`eng130-meghana1-jenkins`
- Select `Enter directly` for the private key and copy paste the private key from the .ssh folder.(public key we have added to the github repo , private key should be copied here)
- Click on Add key
- Select the key the error should disappear.
- Select the master to main branch if you are using `main` branch
- Under the `Build Environment` check/click `Provide Node & npm bin/folder to Path`
- In the Build select `Execute with Shell` and give the commands that needs to be executed

### Steps For Continuos Integration:
- Create a dev branch and switch to the dev branch to makes the changes and push to the github
- Create a gitHub-webhook http://jenkinsserverip:8080/github-webhook to trigger with every commit/push from your local host to trigger this job
- Create a `meghana-test` job to test the dev branch as soon as the code is pushed and to trigger another job upon success(test pass)
- In the description give `Testing dev branch`
- Check `GitHub Project` and give the HTTPS url of the github
![image](https://user-images.githubusercontent.com/97250268/200664942-8e2a9d14-e46f-4c8f-be4a-c73c5fcd24c2.png)
- Under the `Office 365 Connector` check/click `Restrict where this project can be run` and give `sparta-ubuntu-node`(This is given to make the project run on agent node and not on master node`
- Under the `Source Code Management` select git and give the SSH url of the github and select the private key credentials and mention `*/dev` in the `Branch Specifier`
![image](https://user-images.githubusercontent.com/97250268/200666118-f9e19bce-4355-4ce4-9dde-b8f915f81ea4.png)
- Under the `Build Triggers` check/click `GitHub hook trigger for GITScm polling`
- Under the `Build Environment` check/click `Provide Node & npm bin/ folder to PATH`
![image](https://user-images.githubusercontent.com/97250268/200666744-81ab623b-e7bf-483b-ba8e-f0fd63dd5b96.png)
- Under the `Build` --> `Execute with Shell` -->write the commands to be executed
![image](https://user-images.githubusercontent.com/97250268/200667230-52949c05-6710-4e61-934c-6441733d596e.png)

- Under the `Post-build Actions` 
![image](https://user-images.githubusercontent.com/97250268/200667609-43c33d50-017e-4202-95ef-5b94ac38b838.png)
- Click `Apply and Save` 

#### Steps for Merging `main` and `dev` branches
- Create a job `meghana-merge-dev` to merge dev branch with main branch
- In the description give `Merging dev branch with dev branch`
- Follow the same steps as in creating `meghana-test` job until the `Build Environment` 
- In the `Build with execute shell` give the commands `git checkout main` and `git merge origin/dev`
- In the `Post-build Actions` select `Git Publisher` and give `Branch to push` :`main` and `Target remote name` :`origin`
- Click on `Apply` and `Save`

![image](https://user-images.githubusercontent.com/97250268/200811429-bdc32039-d9d1-4831-86f2-bc5501f97c75.png)

#### Steps for creating the deployement job:
 - Create an EC2 instance from node app AMI and specify the security groups (HTTP from port 80,ssh from MY IP and ssh from Jenkins IP)
 - Create a new job `meghana-CD` to deploy the app in the production environment
 - Follow the same steps as in creating `meghana-merge` job until build environment
 -  Select the SSH agent and add the .pem key
 - In the `Build with execute shell` write the following commands
  ![image](https://user-images.githubusercontent.com/97250268/200873449-644b9791-c904-4312-8730-a1d337a9b3fd.png)
 - click on Apply and save
#### Steps for connecting to MongoDB
 - Create EC2 instance from mongodb AMI and specify the security groups (SSH from MY IP and port:27017 from App IP)
 - Create a new job `meghana-mongodb` to connect to the app machine
 - Follow the same steps as in creating the `meghana-CD`
 - In the `Build with execute shell` write the below code
 ```ssh -A -o "StrictHostKeyChecking=no" ubuntu@54.74.33.255 << EOF
 export DB_HOST=mongodb://54.170.254.64:27017/posts >> ~/.bashrc
 sudo source ~./bashrc
 cd app
 sudo killall -9 node
 npm install
 sudo node seeds/seed.js


 nohup node app.js > /dev/null 2>&1 &

 
EOF
```
- Click on Apply and Save.

 ### Output : When you commit some changes in the local host in dev branch and push to github , `meghana-test` is triggered since the webhook from jenkins is linked to github.This inturn triggers `meghana-merge` job and merges the changes into main branch.`meghana-merge` job triggers the `meghana-CD` job and deploy the changes to the production environment.


