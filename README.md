
SITUATION:

 Creating database using AWS RDS with terraform on custom VPC created by Team1.
   Region: us-east-1
   Terraform version: 0.11.14
   Database engine: Aurora(mysql) 
   Engine version: 5.6.10a 
  

TASK:
  task _ picture
  To perform above task, we created data_source file in our repository to pull VPC information from Team1's backend using their backend key. 

       * (data_source picture)

Added multiple regions to test
used interpolation and variables to code our db_cluster file

Use dynamodb lock so that multiple team members can't run terraform apply at the same time. 

commands used to run our code: (run commands under the main repo)
terraform init
source sentenv.sh comfigurations/regions/us-east-1.tfvars
terraform apply -var-file configurations/us-east-1.tfvars

created output.tf file to include our DB name, region, endpoints of our DB for Team3. 


challanges:
using Team1's backend in tfvars files
other teams making the same mistake with backend breaking the statefile.
waiting on other teams 
RDS creating but endpoints taking long to create. 


ACTION:
  
  Fixed our .tfvars file to have the correct information (our backend (S3)). This resolved 1st issue we had.
  communicated with other teams whenever state file was broken. 
  Team1 had to fix their state file couple times, then were able to continue with our task

  Created an EC2 instance on public subnet of the VPC that was created by Team1. This way our database and the instance would be on the same VPC. 

  installed mariadb, using endpoint of RDS connect to database server. Commands used:
     mysql -h <RDS endpoint> -u <mysqlusername> -p 


RESULT: +

Created RDS successfully with the outputs as below:


    * (picture of latest output)
