Problem:
Let's we have a datacenter which runs variety of Application services such as Tomcat, LAMP Stack or DB services such as Postgre, Oracle running on Physical/Virtual machines. Related with this services there are several teams managing the architecture. This cause; complex management, scaling problem and high Opex and Capex. Besides that the processes are manual and time consuming.

Solution: 
Cloud computing is the solution for this but we need to lift and shift our on-site deployment. (IAAC - for automation)


AWS Services
   EC2 Instances (VMs for TOMCAT, RABBITMQ, MEMCACHED, MYSQL) 
   ELB (For replacement of NginX LB)
   Autoscaling
   S3/EFS Storage (Shared Storage)
   Route 53 (DNS)
   ACM 


On-premise Topology
1 - When user try to the app over URI or IP we will redirect to traffic to Load Balancer.
2 - NginX is a web service just like Apache httpd and it's commonly use to create the load balancing. 
3 - When request comes, NginX is going to route the request to the Tomcat.
4 - Apache Tomcat is a Java Web Application Service. If your web application is written  in Java, Tomcat is a very famous service to host it.So the application written by the developer will be sitting in this. IF you need external shared storage you can use NFS servers.
5 - Rabbit MQ is a message broker or also called a queuing agent to connet to applications together. You can stream data from this.
6 - The application accessed by the users and the user will login with credentials. When this happends the application will run an SQL query to access the user information stored in MySQL Database.
7 - Before the credentials goes to the MySQL database the request will go to memcache service. Memcache is a database caching so it will be connected to MySQL server. MySQL will store the user information when the first time the request comes to the database. It will be sent from MySQL to Tomcat and then it will be cached to Memcache server. When the following requests come, the cached data will be served by browser cache.


Cloud Topology
1 - DNS 53 will direct the traffic over HTTPS to our ELB. Since we will need a Domain name, ACM will be use to validate the domain.
2 - ELB will direct the traffic to tomcat instances over the port 8080.
3 - We need EC2 instances for Tomcat, Memcache, Rabbit MQ, MySQL
    We also need 3 sequrity group to allow communication between services.
4 - We need Amazon S3 bucket to store software artifact


Flow Of Execution
1 - Login to AWS Account
2 - Create Key Pairs
3 - Create Security Groups
4 - Launch Instances with user data [BASH SCRIPTS]
5 - Update IP to name mapping in route 53
6 - Build application from the source code
7 - Upload to S3 Bucket
8 - Download artifact to Tomcat EC2 Instance
9 - Setup ELB with HTTPS [Certificate from ACM]
10- Map ELB Endpoint to website name in GoDaddy DNS
11- Verify