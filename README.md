# jenkins-aws-demo

# Step 1
Launching two ec2 instances, so that one can behave as master node, and the second one can behave as slave/agent node. For making these instances I am using terraform code, the same code I used previously, for this one, I defined one more security-group, for the agent node, in which I gave ingress rule only for ssh and deafualt egress rule. for the master node, I gave tcp, ssh, http/https inbound rule and default outbound rule. After launching the instances, we can see the public and private ip address for both the instances. 
<img width="960" alt="1" src="https://github.com/user-attachments/assets/3684db4a-a8e4-45fb-804d-a55c0dfd5d02" />

We can see both the instances are running.
<img width="960" alt="2" src="https://github.com/user-attachments/assets/d5d378b5-8a5d-4c33-919c-a1cd9bc09e72" />

# Step 2
Doing ssh into our master node/instance
<img width="673" alt="3" src="https://github.com/user-attachments/assets/e62ddc1c-c6c2-4ea6-a942-feaea30ab8df" />

Installing some required packages, enabling jenkins, and starting it, we can see it's loaded and active.
<img width="960" alt="4" src="https://github.com/user-attachments/assets/4c7a2dd0-7ccb-4477-992a-d3178cc153cb" />

We can run jenkins on the public ip of our master ec2 instance.
<img width="960" alt="5" src="https://github.com/user-attachments/assets/4e0f9bb6-2286-43c5-9699-fe2a9971b8fd" />
<img width="960" alt="6" src="https://github.com/user-attachments/assets/483b9d78-d5f2-4e89-b034-012ccdacb717" />
# jenkins desktop
<img width="960" alt="7" src="https://github.com/user-attachments/assets/d79156bb-0b0f-4fbd-8c30-49ed0e47790c" />
# step 3

Doing ssh into agent ec2 instance.
<img width="674" alt="8" src="https://github.com/user-attachments/assets/45db5c4d-f3a2-4357-841b-27ca7ad2ced2" />

# Step 4

Generating public and private rsa key pair, using "ssh keygen -t rsa" inside jenkins bash, which will help us to connect our master and slave.
<img width="960" alt="11" src="https://github.com/user-attachments/assets/b30bc7a4-2536-4626-8516-4b5efc0773f9" />

# step 5
 Setting the public key from master node into slave node authorized keys, using this command echo "PUBLIC_KEY_FROM_MASTER_HERE" >> /home/ec2-user/.ssh/authorized_keys.
 
<img width="960" alt="10" src="https://github.com/user-attachments/assets/4f9880c2-83be-4912-8609-905901ce7c03" />

Installing node in the agent node, because we want to run a nodejs application using our agent/slave node.

<img width="916" alt="15" src="https://github.com/user-attachments/assets/37656504-36f6-468f-ac05-d2e0e97a3cb7" />

We can check node version.

<img width="913" alt="16" src="https://github.com/user-attachments/assets/b360c0eb-cdbb-4802-b5ec-a00d1d2c4594" />

# Step 6

Till now what we did is, making two ec2 instances, one is master, the other one is agent. we created keys, and set public key in the agent node, it will work like the address or username, just for easy understanding I am using these terms. Now for using the agent node, we have to make a node on console running on our master node, and provide it our global credential, in which we will store our private key(which will work like password). This is my understanding, the overview what we our doing, and how we are connecting the nodes. 

So after setting the global config, I made the node.

<img width="960" alt="9" src="https://github.com/user-attachments/assets/d3cb09a2-d5d8-4740-9a5d-9fe0fdaba340" />

It failed at first, because while giving global config I used the wrong name, we should use ec2-user, than only it will authenticate our slave node, after doing this step also, my node was showing offline. the reason was, While making the ec2 instance for slave, I forget to gave the egress rule for internet, because on terraform we have to code it, so I forgot, but after enabling it and installing java My node is no more offline.

<img width="960" alt="12" src="https://github.com/user-attachments/assets/0f90f1b5-ce40-43d6-929f-99adda670066" />

Finally I got my agent connected successfully. Class assignment is over now module 4 and 5 is left.
<img width="960" alt="14" src="https://github.com/user-attachments/assets/9872ec97-085b-48cf-8be5-b7955ce3b326" />



<img width="960" alt="13" src="https://github.com/user-attachments/assets/411676db-a1b5-4080-87c5-6bd7a59558d5" />

# Step 7 

# Module 4 

Creating app.js, package,json and Jenkins file.


<img width="933" alt="17" src="https://github.com/user-attachments/assets/0dde4b15-164c-4ab8-b7dd-8090e94b92e1" />

# Step 8

Pushing it to github.
<img width="960" alt="18" src="https://github.com/user-attachments/assets/53a99680-c279-48a4-ae12-fc2218e78daf" />

# Step 9

Making my first job, "my-first-pipeline-krishna"

Configuring it, we have to select the option to get the jenkins file from our github repository, if the repository is private, do give your credentials, if it is public then it's fine, update your master/main brach, whatever convention you follow, and in the end give jenkins, because we are running it through jenkinsfile.

<img width="960" alt="19" src="https://github.com/user-attachments/assets/78373aa6-24e2-4bf2-9219-edc6183c1e35" />

# Step 10 

Building the job, at first it was failed, because I didnt gave "linux" as label while making my agent node, and in our jenkins file, we have specified, "agent label'linux'".

# Tip

check your console output to debug the error.

<img width="960" alt="21" src="https://github.com/user-attachments/assets/682bdeaf-728b-4138-a8d4-14e672711410" />

After adding 'linux' as a label for my agent node, my job built successfuly. We can see each part specified in the pipeline worked well.

<img width="960" alt="lf" src="https://github.com/user-attachments/assets/227cbeb7-550d-4537-9f10-682c8f2bc15f" />

<img width="960" alt="llf" src="https://github.com/user-attachments/assets/be458921-e7bc-4389-82ad-6783d907e890" />

<img width="960" alt="final" src="https://github.com/user-attachments/assets/16d391a6-3e73-470e-b4af-8a6a912ba5cb" />

# Step 11

Most important step, detroying resources after completing the task, that is I used terraform to make instances, so I can delete it in a go. 

<img width="960" alt="23" src="https://github.com/user-attachments/assets/f7cdda46-7f52-431d-835c-ed10f6c52b97" />

# Task completed.

# Module 6

To create a Jenkins pipeline that automatically builds, tests, and deploys a web application to a dedicated EC2 instance (the "App Server") using SSH.

To add this or to perform this step, we need to update couple of things.

# 1 Jenkinsfile

We need to update our jenkins file, so it can automate:- code, build, test, deploy, we need to add these stages in our Jenkinsfile.

# 2 Configure github webhook

We need to add a Webhook in our github repository, which can trigger Jenkinsfile on every push.

Rest of things will be same, as we are automating in this step. So by updating these 2 things we will be able to automate the steps mentioned above.

