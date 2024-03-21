# Project Overview:
The Socks Shop application is a popular microservices-based e-commerce platform that is used as a reference application for demonstrating modern cloud-native technologies. The application is composed of multiple microservices, each of which is responsible for a specific function, such as product catalog, shopping cart, and user authentication. The application is designed to be highly scalable, resilient, and fault-tolerant, making it an ideal candidate for deployment on Kubernetes.
The project will involve deploying the Socks Shop application on a Kubernetes cluster using an Infrastructure as Code (IaC) approach. This will include provisioning the necessary infrastructure resources on AWS, setting up a deployment pipeline, monitoring the performance and health of the application, and securing the infrastructure.
The project will be implemented using Terraform for infrastructure provisioning, GitHub Actions for the deployment pipeline, Kubernetes for container orchestration, Helm for package management, Prometheus for monitoring, ELK Stack for logging, and Ansible for security.

# PRE-REQUISITE
-AWS account
-IAM user with administrator access
-ubuntu  t2.medium ec2 instance
-security group created with this rules specified *inbound rules* +all traffic -ipv4
+ssh -ip4
+http - ipv4
+https - ipv4
*outbound rule* +all traffic - ipv4
+all traffic -ipv6
-key pair as seen in *(eks/05-08-eks-node-group-private.tf)*
-domin name (cygold.i.ng)


connect to the ec2 instance and run the command
` git clone *https://github.com/CyGold/updated-sock-shop-main.git em* `
this clones the got repository to the instance

` cd em ` 
changes directory to em

`chmod +x *installer.sh* `
gives permission to the script

` ./installer.sh `
runs the script which is responsible for the installation of jenkins, terraform, kubeCTL, helm and AWS CLI

` aws configure `
used for the configuration of AWS command line interface, input the required details with default region being eu-west-2 and the format as json

sign into jenkins using the ip address on port 8080 and input the password seen after running the command below:
` *sudo cat /var/lib/jenkins/secrets/initialAdminPassword* `

In jenkins dashboard, click on*manage %* and go to *security* and click the check box under *CSF*, back to the *manage %* menu and go to *credentials*, then *global* and *add credentials*
the first credential's file format id *username and password* which will include your github username and password, the next two are *AWS ACCESS KEY* and *AWS SECRET ACCESS KEY* with the file format as *secret text* and details required are from the IAM user created beforehand.
back to the jenkins dashboard, click on *new item* and give it any name of your choice and click on new pipeline, change the name of branch to main and the filename to cluster-jenkins, select the pipeline SCM as git and the previously created credential, click on ok and on the dashboard *build now*. this facilitates the creation of eks cluster
repeat the above step and the github file will remain as jenkinsfile,this facilitates the creation of prometheus, deploys the sock-shop microservice as well as the ingress rile to eks, as well as create ngnix controller and route 53 and sends an application for ssl certificate as seen in the screenshot below-
![ssl-cert](http:images\ssl-cert.jpg)

the next step is copy the name servers from route53 on aws to the domain name and save the name servers. this may take a few hours to apply the changes. also, the ssl certificate may remain pending until approved by aws.
copy the assigned grafana as well as the sock-shop urls to see the default pages
sign into grafana with username as admin and the password as prom-operator
once done, you can destroy both builds on jenkins and terminate the instance  

 
