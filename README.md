# CXS_450_1_Project_1

**Configuring a Jupyter Data Science Notebook Servere on AWS**
----
**Configuring the AWS account**

* First we need to sign up for AWS (Amazon web services) at: http://aws.amazon.com

* Log in to AWS console

* Choose a region (It is recommended to choose a region that is grographicly closer to us) 

**Prepration to luanch a new Instance (EC2)**

* Set up our key pair 

   A.First we need to creat our ssh key pair locally using these set of commands at Gitbash:


`ssh-keygen`

Then hit Enter twise to accept the defult location 

`ls ~/.ssh` 

will give us the location of our ssh key, then type:

`cat ~/.ssh/id_rsa.pub`

This last command will give us the content of our generated key pair

Now we just need to copy this contenet, and go back to our AWS console.
    
    B.Import Key Pair

Click on the key pair section tab then choose Import key pair.

Choose a name for the key pair and copy the content to the Public Key Content part and hit Import


* Configuring our security group
 
 Hit the Create security Group tab
 
 We need to choose Add Rule to choose our own ports. Here we need
 
Type                 Port      source


ssh                  22        Anywhere



http                  8888      Anywhere


custom TCP Rule       2376      Anywhere


Custom TCP Rule       27016     Anywhere

Then hit Creat

Now we have everything to launch our instance.

**Launching the new EC2**

1. Choose Ubuntu Server (as our AMI) 
2. After that we choose our Instance type (Free Tier T2.micre) the second row
3. Skip third step configure Instance Detailes
4. On this step we change the storage size to 30G
5. We skip the step 5th and move over to the 6th step
6. Inthis Step we just choose the security groups thet we already created
7. Now we just review the changes thet we've done, choose the existing the key pair, and hit Launch

**Docker Installation**

We copy the public Ip of our new instance, and we go over to bash and copy it in this command:
`ssh ubuntu@PUBLICIPADDRESS`


in order to connect to the system we type y

now we are connected

Then we install Docker

` curl -sSL https://get.docker.com | sh`

Now we just need to copy past this part

`Sudo usermod -aG docker ubuntu`

we should log out now using:

`exit`

And log back in

We can make sure that everything works by this command:

`docker -v`

**Runing Jupyter**

To download jupyter we type this command:

`docker pull jupyter/datascience-notebook`

To verify we type this comman

`docker images`

To shorten the name of the image we do:

`docker tag IMAGEID dsnb`

`docker images`

Now we want to use this image we type:

`docker run -v /home/ubuntu:/home/jovyan -p 80:8888 -d jupyter/datascience-notebook`

To use it we open a new browser, and at the address bar we put the IP address of our AWS instance

Now we need a token to get that we run

`docker exec CONTAINERID jupyter notebook list`

We can copy the token and paste it to the password spot

Our Jupyter Notebook is ready to use
