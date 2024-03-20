the automated deployment the sock-shop microservice 

PRE-REQUISITE
-AWS account
-IAM user with administrator access
-ubuntu  t2.medium ec2 instance
-security group created that allows *ort 8080,222 all on i*V 4 inbound rules and the outbound rules with one two all traffic, one traffic on i*4 and the other on i*6
-key pair as seen in *(eks/05-08-eks-node-group-private.tf)*


connect to the ec2 instance and run the commands
#git clone *https://github.com/CyGold/updated-sock-shop-main.git em*
this clones the got repository to the instance
#cd in em 
#chmod +x *installer.sh*
 
# gives permission to the script
*./installer.sh*

runs the script which is responsible for the installation of jenkins, terraform, AWS CLI and 
#aws configure
this command is used for the configuration of AWS command line interface, input the required details with default region being eu-west-2 and the format as json
sign into jenkins using the ip address on port 8080 and input the password seen after running the command below:
#*sudo cat /var/lib/jenkins/secrets/initialAdminPassword* 

In jenkins dashboard, click on*manage %* and go to *security* and click the check box under *CSF*, back to the *manage %* menu and go to *credentials*, then *global* and *add credentials*
the first credential's file format id *username and password* which will include your github username and password, the next two are *AWS ACCESS KEY* and *AWS SECRET ACCESS KEY* with the file format as *secret text* and details required are from the IAM user created beforehand.


 
go back to the jenkins dashboard and click on new item,give the item your *reffered name and select *i*eline and change the branch to main and the jenkinsfile default to cluster-jenkins,, scroll down and click on **ieline SCM git in*ut your re*o url and select the credential, click on okay and build now
youll see your **line is being created after that... the creation of eks cluster 
after which REA*TE but the chosen file is jenkins and the branch is main not master
this creates ssl certificate, *rometheus and grafana+++0