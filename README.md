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
- Webhooks allow interaction between web-based applications through the use of custom callbacks. The use of webhooks allows web applications to automatically communicate with other web-apps. Unlike traditional systems where one system (subject) keeps polling another system (observer) for some data, Webhooks allow the observer to push data into the subject’s system automatically whenever some event occurs.
- This eliminates the need for constant checking to be done by the subject.
### What are Jenkins Stages

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



