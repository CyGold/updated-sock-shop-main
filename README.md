the automated deployment the sock-shop microservice 

# PRE-REQUISITE
-AWS account
-IAM user with administrator access
-ubuntu  t2.medium ec2 instance
-security group created that allows *ort 8080,222 all on i*V 4 inbound rules and the outbound rules with one two all traffic, one traffic on i*4 and the other on i*6
-key pair as seen in *(eks/05-08-eks-node-group-private.tf)*


connect to the ec2 instance and run the commands
#git clone *https://github.com/CyGold/updated-sock-shop-main.git em*
this clones the got repository to the instance
''' cd em '''
#chmod +x *installer.sh*
gives permission to the script
*./installer.sh*

runs the script which is responsible for the installation of jenkins, terraform, AWS CLI and 
#aws configure
this command is used for the configuration of AWS command line interface, input the required details with default region being eu-west-2 and the format as json
sign into jenkins using the ip address on port 8080 and input the password seen after running the command below:
#*sudo cat /var/lib/jenkins/secrets/initialAdminPassword* 

In jenkins dashboard, click on*manage %* and go to *security* and click the check box under *CSF*, back to the *manage %* menu and go to *credentials*, then *global* and *add credentials*
the first credential's file format id *username and password* which will include your github username and password, the next two are *AWS ACCESS KEY* and *AWS SECRET ACCESS KEY* with the file format as *secret text* and details required are from the IAM user created beforehand.
back to the jenkins dashboard, click on *new item* and give it any name of your choice and click on new pipeline, change the name of branch to main and the ## to cluster-jenkins, select the pipeline SCM as git and the previously created credential, click on ok and on the dashboard *build now*. this facilitates the creation of eks cluster
repeat the above step and the github file will remain as jenkinsfile,this facilitates the creation of prometheus, deploys the sock-shop microservice as well as the ingress rile to eks, as well as create ngnix controller and route 53 and sends an application for ssl certificate as seen in the screenshot below-


 