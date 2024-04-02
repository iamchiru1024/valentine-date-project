# valentine-project using aws, terraform,jenkins,trivy,docker

1) Launch t2.micro ubuntu instance manually and allow all traffic.
2) Login to the instance and install teraform by using below commands.
   A. sudo apt update
   B.  wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
   C. echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
   D. sudo apt update
   E. sudo apt install terraform -y
   F.terraform --version
   G. sudo apt install unzip
   H.Install aws cli
     curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
     unzip awscliv2.zip
     sudo ./aws/install
	 aws configure  <provide your account security keys>
   
3)After installing terraform create new directory terraform-project and create Main.tf and provider.tf files in terraform-project directory that you created.Copy paste same files from my git.
  git clone https://github.com/iamchiru1024/valentine-date-project.git
  
4)In same directory run the below commands to create jenkins server
  a. terraform init
  b. terraform plan
  c. terraform apply
  
  A new ec2 instance will be created, use the public ip of the new instance to connect to jenkins GUI. url: <public-IP>:8080
  for initial login password do
cat /var/lib/jenkins/secrets/initialAdminPassword
install suggested plugins 
  
5)After Jenkins setup is completed. 
go to this path i jenkins GUI Dashboard>Manage Jenkins>Plugins and select available plugins , search for docker and install first 5 docker plugins.
6) Manage jenkins and click on tools, search for docker and give name as docker and select Install automatically and select download from docker.com
7) In manage jenkins search for credentials ,select system ,select Global credentials (unrestricted) ,select add credential,give docker hub username and password and ID as docker-cred
6)To create a pipeline go to manage jenkins,select New item and enter item name and then select pipeline and click OK
7) in the next page scroll down to bottom to see Pipeline option, In Definition dropbox select "pipeline script from SCM" then select Git for SCM and give below url in "Repository URL".
https://github.com/iamchiru1024/valentine-date-project.git

in "Branches to build" section change */master to  */main and save 
8)Now the final step click on Build Now to start the pipeline
9) Once the build is success paste the url in your favaroit browser  <public-IP of jenkins server>:8081/yes.html
