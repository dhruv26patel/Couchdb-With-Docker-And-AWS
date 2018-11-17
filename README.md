# CouchDB with AWS (Ubuntu Instance) 
The couchdb instance is running on a docker container hosted on AWS Ec2 instance. 

### Prerequisits
1. Lauch a Ubuntu Ec2 instance which can be a t2.mico (free tire). Make sure you have allowed the ports which you intent to run couchdb on. For purpose of this example we will be using port 5986.
2. SSH into the ec2 instance using Public DNS name. 
3. Install docker using the following steps: 
```
sudo apt-get update
sudo apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 9DC858229FC7DD38854AE2D88D81803C0EBFCD88
sudo apt-add-repository 'deb [arch=amd64] https://download.docker.com/linux/ubuntu xenial main stable'
sudo apt-get update
sudo apt-get install -y docker-ce
```
4. To ececute Docker commands we need to create a user and add it to the docker group which can be done using the folowing steps
```
sudo adduser <username>
sudo usermod -aG docker <username>
```
5. You can change between user using the following commands and whoami (command which display the current user) 
```
su - <username>
whoami
```
6. You can search dockerhub for the available images that will allow you to make a docker container using a simple commmand 
```
docker search couchdb
```
##### Comments: Usually you go with the image without any extensions so in this case couchdb which will be the first one listed. The reason we choose it that it is more secure and stable since it is from the service provider. We have to also keep in mind that we are communicating from within docker to the host (AWS instance) so for them to communicate with each other they should be sharing information through ports. In our case are mapping using the same port from host as well as container but you can have them expose different port as well. 
9. To run the couchdb on the 5986 we will need to run the following command: 
```
docker run -p 5986:5986 -d couchdb

or if you wat host port to be 8080 and container port to be 5986  

docker run -p 8080:5986 -d couchdb    

-p: publish the port of container and the host (AWS server) 
-d: To run couchdb in the background as a service
```
10. You should now be able to use the instance Public IP IPv4 address and append the port and be able to see the welome page.
```
<Public IP IPv4>:5986
```
