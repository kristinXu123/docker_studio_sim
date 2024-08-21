#<center>How to install UFACTORY Studio in Docker

**Introduction:**

Introduction: Implemented via docker: Control simulated UFACTORY robots in UFACTORY Studio without the need for a real robot arm!

**Preparation:**

 

# Method 1: Uploading packages to the ubuntu image
* Download and install docker, docker website:[Docker: Accelerated Container Application Development 2](https://www.docker.com/)


* Download and install UFACTORY Studio docker image, download link:[ Docker - Google ドライブ ](https://drive.google.com/drive/folders/1gae-RRkVPG7pH7n3KtrRHRkzKYW0GTbO)
                                                                                                                                 - 
If you follow the guidance, you will start the Lite 6 robot by default.

**Note: The following example is installed a new ubuntu image.**
##1.Download and install ubuntu  
```
`docker pull ubuntu`
```
##2.Create a Docker and open
**On Linux Ubuntu**
```
docker run -it --name uf_software ubuntu
```
**On Windows**

* If only use UFACTORY Studio
```
docker run -it --name uf_software -p 18333:18333 ubuntu
```
* If you want use not only the UFACTORY Studio but also the xArm SDK on Windows, please use this command:
```
docker run -it --name uf_software -p 18333:18333 -p 502:502 -p 503:503 -p 504:504 -p 30000:30000 -p 30001:30001 -p 30002:30002 -p 30003:30003  ubuntu
```

##3.Update the software of docker and install python environment.
```
apt update 
apt upgrade -y 
apt install -y net-tools wget screen sudo nano python3.12 python3-pip
```
##4.Create user and set the password
```
adduser uf 
usermod -aG sudo uf 
```
##5.Upload the package of software to docker. 
--uploady by yourself
##6.Upzie the UFactory Studio and scripts.
```
tar -xf uf_sim.gz 
cd uf_sim
sudo -u uf tar -xf studio.gz -C /home/uf/ 
sudo -u uf tar -xf xarmcontroller.gz -C /home/uf/ 
tar -xf xarm_scripts.gz -C / 
cd .. 
rm -rf uf_sim* 
```
##7.Start the UFactory Studio in docker
```
/xarm_scripts/xarm_start.sh 6 6
```


**Note: The version of studio launched now is 1.12.x, so you can upgrade the version by following these steps**
##8.Update software  and firmware version

* upload docker_sim_update* to docker container by yourself
* attach to docker container, and run command in docker container
```
//unzip

        unzip docker_sim_update_V2.4.0.zip
        cd docker_sim_update_*
        tar -xf xarmcontroller-x86_64-*.tar.gz
        tar -xf xarmstudio-x86_64-*.tar.gz --wildcards linux/xarm.tar.gz && tar -xf linux/xarm.tar.gz -C ./ && rm -rf linux
//update

        sudo -u uf cp -rf xarmcontroller/* /home/uf/xArm/
        sudo -u uf rm -rf xarm/software/python
        sudo -u uf cp -rf xarm/* /home/uf/.UFACTORY/xarm/
        sudo mkdir -p /usr/local/lib64
        cd /home/uf/.UFACTORY/xarm/software/xArm-Python-SDK
        /home/uf/.UFACTORY/xarm/software/python/bin/python3 setup.py install
```

##9.restart docker container

##10. Start the UFactory Studio in docker

```
/xarm_scripts/xarm_start.sh 6 6
```

**Note: The 6 6 means xArm 6, restarting the container choose the robot according to your preferences:**
```
5 5, xArm 5
6 6, xArm 6
7 7, xArm 7
6 9, Lite 6
6 12, 850
```

##11.Access the UFACTORY Studio
**On Linux Ubuntu**

Run a web browser and input 172.17.0.2:18333

**On Windows**

Run a web browser and input 127.0.0.1:18333

**If you need use xArm SDK**

Ubuntu Linux: the robot IP is 172.17.0.

Windows: the robot IP is 127.0.0.1

#Method2：Pulling docker_studio images 
##1.Get the docker image
    docker pull danielwang123321/uf-ubuntu-docker
##2.Create and run container
**On Linux Ubuntu**
    docker run -it --name uf_software danielwang123321/uf-ubuntu-docker
**On Windows**

* If only use UFACTORY Studio

    docker run -it --name uf_software -p 18333:18333 danielwang123321/uf-ubuntu-docker
    
* If you want use not only the UFACTORY Studio but also the xArm SDK on Windows, please use this command:

    docker run -it --name uf_software -p 18333:18333 -p 502:502 -p 503:503 -p 504:504 -p 30000:30000 -p 30001:30001 -p 30002:30002 -p 30003:30003  ubuntu

##3.Run the xArm robot firmware and UFACTORY Studio

    /xarm_scripts/xarm_start.sh 6 6

##4.Access the UFACTORY Studio

**On Linux Ubuntu**

Run a web browser and input 172.17.0.2:18333

**On Windows**

Run a web browser and input 127.0.0.1:18333

**If you need use xArm SDK**


Ubuntu Linux: the robot IP is 172.17.0


Windows: the robot IP is 127.0.0.1


