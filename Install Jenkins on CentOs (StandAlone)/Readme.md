                                                            ## Install Jenkins on Centos ##
## [Install Java]

  - yum install java-11-openjdk-devel

## [Download Jenkins War File]
  
  - wget https://get.jenkins.io/war-stable/latest/jenkins.war


## [Start Jenkins]

  -  java -jar jenkins.war --httpPort=8080
 

  ** Optional (Run the Jenkins as Background Process) **

  ++ nohup java -jar jenkins.war --httpPort=8080 > jenkins.log 2>&1 &


## [Default password was saved at]

  - /root/.jenkins/secrets/initialAdminPassword
