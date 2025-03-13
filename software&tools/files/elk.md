<div align="center">

# **Elk Elasticsearch**

![Elk Elasticsearch](../pic/elk.gif)
</div>

## Installing

(installing of one server)

__* NOTICE__ for cluster installation. dont activate the system untill the all cluster is installed.


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
