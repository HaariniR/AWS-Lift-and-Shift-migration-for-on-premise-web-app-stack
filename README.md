# Deploying a multi-tier web application on AWS Cloud
- EC2 instances
     - I) RabbitMQ
     - II) Memcached
     - III) MYSQL - Mariadb server
     - IV) Tomcat - application server
   - Note: EC2 instances are provisioned automatically with user data scripts
- Route 53 
    For a private DNS hosting zone for the backend services. This will be referred to in application properties of tomcat web    application to communicate with the - backend
  - ELB 
    Elastic load balancer will act as the front end to receive all the incoming traffic and this will forward the request to tomcat   server. Endpoint of the ELB is associated with a domain name(Go daddy is used for domain registration and dns management) from which clients can access the application
  - Auto scaling group
    Auto scaling group is attached with tomcat instances to scale up and scale down the instances based on the incoming traffic
  - Git
    Source code of the web application is fetched from git hub repository
  - Maven
    Maven build tool is used to build the artifact
  - S3
    S3 bucket to store the artifact

- Process Flow:
When user access the hostname, ELB is referenced which will forward the traffic to tomcat server. Tomcat will communicate with the backend servers to retrieve information from the database using their dns names registered with route 53 private hosting zone. Based on the incoming traffic, application server instance will be scaled or scaled up by the auto scaling group.

- Refer image.png for overall process flow and
  demo document for step by step process

- Cons:
Manual process of 
  - building the artifact with maven and storing them in S3 buckets. 
  - deploying the artifact from S3 bucket to tomcat server

- Issues faced:
Application runs only on tomcat8, openjdk-8 environment. So if latest ubuntu releases higher than 18 is used, then application deployment will fail.
Connection with database will be successful only if private dns hosting ip address specified is correctly referenced in the application properties
