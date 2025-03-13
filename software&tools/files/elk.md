<div align="center">

# **Elk Elasticsearch**

![Elk Elasticsearch](../pic/elk.gif)
</div>

## Installing Elasticsearch

(installing of one server)

### Prerequisites:

Ubuntu Server (for hosting the ELK).

### 1. follow the steps on: 

        https://www.fosstechnix.com/how-to-install-elastic-stack-on-ubuntu-22-04/

    On the server:

        sudo apt update
        sudo apt install apt-transport-https
        sudo apt install openjdk-11-jdk

  verify installation of Jave:

        java -version       

  define the environment variable:

        sudo nano /etc/environment

  Paste the below variable into the file:

        JAVA_HOME="/usr/lib/jvm/java-11-openjdk-amd64"

  (good practice is to varify Java is installed):

        which jave

  Load the environment variable:

        source /etc/environment

  verify JAVA_HOME variable:

        echo $JAVA_HOME
  
  Download and install the public signing key:

        wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo gpg --dearmor -o /usr/share/keyrings/elasticsearch-keyring.gpg

  Save the repository definition to /etc/apt/sources.list.d/elastic-8.x.list:

        echo "deb [signed-by=/usr/share/keyrings/elasticsearch-keyring.gpg] https://artifacts.elastic.co/packages/8.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-8.x.list

  Install the Elasticsearch:

        sudo apt-get update
        sudo apt-get install elasticsearch

__* NOTICE__ for cluster installation. dont activate the system untill the all cluster is installed.

  Start elacticsearch services

        sudo systemctl start elasticsearch

  Enable elacticsearch at system startup          

        sudo systemctl enable elasticsearch

  To check the status of elasticsearch

        sudo systemctl status elasticsearch

Configure Elasticsearch:

  configuration file

        sudo nano /etc/elasticsearch/elasticsearch.yml

  Go to Network section and uncomment network.host and replace your system IP with

        network.host: 0.0.0.0

  add this line discovery.seed_hosts: [ ] in discovery section

        discovery.seed_hosts: [ ]

  go to the BEGIN SECURITY AUTO CONFIGURATION and here you need to replace this true with false as shown in below:

        xpack.security.enabled: false

  restart for configuration to take change:

        sudo systemctl restart elasticsearch

  Checking the elasticsearch (if work):

     
        curl -X GET "localhost:9200"

     Or

        http://<ELK_server_IP>:9200

__* NOTICE__ best practice is to install __Logstash__ and __Kibana__ on seperate mechine (server).

## Installing Logstash

  On the server:

        sudo apt update
        sudo apt-get install logstash

   Start the Logstash service:

        sudo systemctl start logstash

  Enable the Logstash service:

        sudo systemctl enable logstash

  check the status of the service

        sudo systemctl status logstash

### Configure logstash

        sudo nano /etc/logstash/logstash.yml

## Installing Kibana

  On the server:

        sudo apt update
        sudo apt-get install kibana

  Start the Kibana service:

        sudo systemctl start kibana

  Enable the Kibana service:

        sudo systemctl enable kibana

  Let’s check the status of kibana:

        sudo systemctl status kibana

### Configure Kibana 

  open the kibana.yml configuration file for editing:

        sudo nano /etc/kibana/kibana.yml

  Uncomment this below lines and localhost replace with 0.0.0.0 (means any ip_address):

        server.port: 5601

        server.host: "localhost"

        elasticsearch.hosts: ["http://localhost:9200"]

  restart kibana

        sudo systemctl restart kibana

  To access Kibana, open a web browser and browse to the following address:

        http://ip_address:5601

check connectivity of Kibana. 

        enter thekibana webpage --> Management --> Stack Management --> Index Management 
        (turn On: include hidden indices, include rollup indices)
        
## Installing Filebeat

Acts as an agent that collects and sends logs to the ELK stack (Elasticsearch, Logstash, Kibana). It is a lightweight, resource-efficient tool that you install on the source systems where the logs are generated (like web servers, application servers, or any other machine producing logs).

  Install on each of the source:

        sudo apt-get install filebeat

### Configure Filebeat

Filebeat, by default, sends data to Elasticsearch. Filebeat can also be configured to send event data to Logstash.

  Open configuration file using below command:

        sudo nano /etc/filebeat/filebeat.yml

  Under the Elasticsearch output section, comment out the following lines:

        # output.elasticsearch:
        # Array of hosts to connect to.
        # hosts: ["localhost:9200"]

  Under the Logstash output section, uncomment in the following two lines:

        output.logstash
        hosts: ["localhost:5044"]

  Enable the Filebeat system module:

        sudo filebeat modules enable system

  Load the index template:

        sudo filebeat setup --index-management -E output.logstash.enabled=false -E 'output.elasticsearch.hosts=["0.0.0.0:9200"]'

  Start and enable the Filebeat service:

        sudo systemctl start filebeat
        sudo systemctl enable filebeat

  Verify Elasticsearch Reception of Data:

        curl -XGET http://43.205.98.238:9200/_cat/indices?v

   Or

        http://43.205.98.238:9200/_cat/indices?v

__trubelshoot__

  check logs at:

        tail -f /var/log/filebeat
