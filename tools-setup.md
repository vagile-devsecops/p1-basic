Download java 21 on redhat on aws ec2
 1.sudo yum update -y
 2.sudo dnf install java-21-openjdk-devel -y

 verify java version command "java-version"
   echo $JAVA_HOME
    7  readlink -f $(which java)
    8  sudo vi /etc/profile -----export JAVA_HOME=/usr/lib/jvm/java-21-openjdk/bin/java
                                 export PATH=$JAVA_HOME/bin:$PATH

    9  source /etc/profile
   10  echo $JAVA_HOME


<role rolename="manager-script"/>
 <role rolename="manager-gui"/>
 <user username="tomcat" password="tomcat" roles="manager-script,manager-gui"/>
