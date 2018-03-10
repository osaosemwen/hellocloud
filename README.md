# HelloCloud 
This is a Simple Docker Demo App 
clone this repo using 

$ git clone https://github.com/osaosemwen/hellocloud.git

The images from and write up from this webapp are taken from a US paper Chigago tribune of April 24 2015 (http://www.chicagotribune.com/news/history/chi-then-and-now-photos-the-aragon-and-apollo-20150424-htmlstory.html). This application shows images from the past and compares them to current ones. The emphasis is using a jquery, css, and jscripts for the slides to imitate what was published.

# Steps
Ensure docker is up and running on your system.

Ensure you have an account on docker hub.


Ensure you have an account on one of the clouds platforms, in my case google cloud platform.

# First

Build the docker image from the docker file with Nginx server using:

$ docker build . -t deu_paper

this tells the docker engine to build th docker image from the current directory, and tag it deu_paper. It follows the instruction you have in place in the docker file.

# Second
run the application on your docker machine and name it hellopaper

$ docker run -d -p 8484:80 --name hellopaper deu_paper

this command tells the docker machine to run the image and tag it as hellopaper, and make it available on port 8484, mapping it to port 80.

to check if it working use your 

 www.localhost:8484 or use your docker images ip in place of localhost.
 
 In my case it works and shows the website.
 
 you can also check to see the images deployed on docker using 
 
 $ docker ps

This will show you the image you just created, the port, its status and how long it has been available.

# Third

login to your docker hub in my case (osemike is my username) using:

$ docker login -u osemike

you will be prompted to enter your login password for the docker hub account, enter it to be granted access to docker hub. 

# Fourth 
Tag the image into what you want it to be on your docker hub, combining your username as shown below using:

$ docker tag deu_paper osemike/hellopaper

# Fifth

Push the image to the dockerhub using: 

$ docker push osemike/hellopaper

you can confirm that the image is pushed to your docker hub, by login in to your docker hub and checking for the images, you would see hellopaper.

# Sixth

login to your cloud platform, in this example - google cloud... and preferably spin up a cluster of minimum 3 instances on the kubernetes engine.

next deploy your application on the cloud, which you have pushed its image to now residing on your dockerhub using:

# Seventh 

Get access to the application by deploying exposing the deployment to port 80, and then adding a Loadbalancer to it, this will come in handy when you intend to scale your application (please refer to osaosemwen/cloudapplication-kubernetes for some examples on kubernetes basics): 

$ kubectl expose deployment/hellopaper --port=80 --name=hellomikesvc --type=LoadBalancer

service "hellomikesvc" exposed


# Eight 

Check for the services deployed on the kubernetes engine to see the external IP of the application using:

$ kubectl get svc

This may take a while "be patient", run the command again. you should see your external ip.

# Run your application with an external IP on the cloud.

When you have the external IP: use it to run your application as shown below in my case.

$ 35.220.98.212:80

for me this IP is temporary because I will clean up my deployment after, so it may not work for u. Its never safe to make use of IP for you application. preferrable to make use of DNS name (Alias or CNAME and map it to your application).

# Enjoy Thats it.

Thanks 

Ose Mike
