We will be setting up a website, a web application which is a social networking site written by developers in Java Language. (Note: Stack is used for collection of sevices working together to create an experience)

Services
   NGINX
   TOMCAT
   RABBITMQ
   MEMCACHED
   MYSQL

1 - When user try to the app over URI or IP we will redirect to traffic to Load Balancer.

2 - NginX is a web service just like Apache httpd and it's commonly use to create the load balancing. 

3 - When request comes, NginX is going to route the request to the Tomcat.

4 - Apache Tomcat is a Java Web Application Service. If your web application is written  in Java, Tomcat is a very famous service to host it.So the application written by the developer will be sitting in this. IF you need external shared storage you can use NFS servers.

5 - Rabbit MQ is a message broker or also called a queuing agent to connet to applications together. You can stream data from this.

6 - The application accessed by the users and the user will login with credentials. When this happends the application will run an SQL query to access the user information stored in MySQL Database.

7 - Before the credentials goes to the MySQL database the request will go to memcache service. Memcache is a database caching so it will be connected to MySQL server. MySQL will store the user information when the first time the request comes to the database. It will be sent from MySQL to Tomcat and then it will be cached to Memcache server. When the following requests come, the cached data will be served by browser cache.


Required Tools
   Hypervisor (Oracle VM VirtualBox)
   Automation (Vagrant)
   CLI        (GIT Bash)
   IDE        (Sublime Text Editor, Notepad++, VisualStudio)

1 - We will be using a vagrant to automate our set up of VMs. We need VMs for NgineX, Tomcat, Memcache, Rabbit MQ and MySQL. Vagrant is gonna communicate with Virtual Box (hypervisor) to start VMs.
2 - We will be using bash script to set up our services (NginX, Apache Tomcat, Memcached, Rabbit MQ, MySQL)


Flow Of Execution
1 - Setup Tools mentioned in Prerequisites
2 - Clone Source Code
3 - cd into the vagrant dir
4 - power up the VMs
5 - Validate
6 - Setup All the services
  a.   NGINX
  b.   TOMCAT
  c.   RABBITMQ
  d.   MEMCACHED
  e.   MYSQL
  f.   App Build & Deploy
7 - Verification


