<div align="center">

# **Jenkins**

</div>


open-source automation tool primarily used for continuous integration (CI) and continuous delivery (CD). It helps automate the process of building, testing, and deploying software, making it easier for developers to deliver high-quality software quickly and reliably.

## CI process:

    1. pulling code (Github or other).
    2. compile and building an image.
    3. testing - unit test/integration tests an more.
    4. packasging and prepering for deploy, like archive conteiner.

  <div align="center">

## **Installing Jenkins**

</div>

two ways to install jenkins:
        - plain installation using apt install.
        - hosted on apache (tomcat)

# install on tomcat

## install java

https://cloudinfrastructureservices.co.uk/how-to-install-apache-tomcat-server-on-ubuntu-22-04/

    Apache Tomcat is based on Java
    
        apt install openjdk-11-jdk

     verify the Java installation 
     
        java --version

## install Apache Tomcat

    create a dedicated user to run the Apache Tomcat server.

        useradd -m -U -d /opt/tomcat -s /bin/false tomcat

    download the latest version of Apache Tomcat from its official website 

        wget https://archive.apache.org/dist/tomcat/tomcat-10/v10.0.20/bin/apache-tomcat-10.0.20.tar.gz

    extract the downloaded file 

        tar -xvf apache-tomcat-10.0.20.tar.gz

    move the content of the extracted directory to the Apache Tomcat home directory.

        mv apache-tomcat-10.0.20/* /opt/tomcat

    change ownership of the Tomcat directory to tomcat.

        chown -R tomcat: /opt/tomcat
        
   set the execution permission on Tomcat binary file.     

       sh -c 'chmod +x /opt/tomcat/bin/*.sh'
    
    create a systemd service file to manage the Apache Tomcat service. 

        nano /etc/systemd/system/tomcat.service

    Add the following configuration:

        [Unit]
        Description=Apache Tomcat
        After=network.target
        
        [Service]
        Type=forking
        
        User=tomcat
        Group=tomcat
        
        Environment=JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
        Environment=CATALINA_PID=/opt/tomcat/tomcat.pid
        Environment=CATALINA_HOME=/opt/tomcat
        Environment=CATALINA_BASE=/opt/tomcat
        Environment="CATALINA_OPTS=-Xms512M -Xmx1024M -server -XX:+UseParallelGC"
        
        ExecStart=/opt/tomcat/bin/startup.sh
        ExecStop=/opt/tomcat/bin/shutdown.sh
        
        ExecReload=/bin/kill $MAINPID
        RemainAfterExit=yes
        
        [Install]
        WantedBy=multi-user.target
        
