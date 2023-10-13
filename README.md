# Diagram Repository
Repository for diagrams of personal projects.  Current diagrams are for in-home development environment that I am developing for myself. 

## Personal Development Environment
### Purpose:
To learn about each service in depth, through setting up an external service (single server or clustered servers), integration of various servers, and actual development on servers.

My number one priority is to learn about each service, however, not every service will remain available - this depends on if the service is necessary to other personal projects.  

### Sections:
1. ETL Service(s)
   1. Apache NiFi
2. Database Service(s)
   1. Elasticsearch
   2. PostgreSQL
   3. Apache Kafka
   4. Cassandra*
   5. JanusGraph*
3. Deployment Service(s)
   1. Jenkins
   2. Sonarqube
   3. Nexus
   4. Docker
   5. Kubernetes**
4. Analytical Service(s)
   1. Apache Spark
   2. Apache Livy
   3. JupyterLab
   4. Kibana
   5. Portainer
   6. Rancher**
   7. Provectus
   8. Prodigy
   9. MLFlow*
   10. LabelStudio*

---
### Table of Services and Resources

Section | Service              | CPU     | Memory | HDD    | Status
--------|----------------------|---------|--------|--------|--------
ETL     | NiFi (x3)            | 4 Cores | 16 GB  | 225 GB | Permanent
Database | Elasticsearch (x3)   | 2 Cores | 20 GB  | 1.1 TB | Permanent
Database | PostgreSQL           | 2 Cores | 8 GB   | 100 GB | Permanent
Database | Kafka (x3)           | 1 Core  | 6 GB   | 505 GB | Permanent
Database | Cassandra*           | -       | -      | -      | Not Built
Database | JanusGraph*          | -       | -      | -      | Not Built
Deployment | Jenkins              | 2 Cores | 4 GB   | 105 GB | Permanent
Deployment | Sonarqube            | 1 Core  | 4 GB   | 105 GB | Permanent
Deployment | Nexus                | 1 Core  | 4 GB   | 1 TB   | Permanent
Deployment | Kubernetes (x3)*     | 4 Cores | 30 GB  | 105 GB | Temporary
Analytics | Spark (x3)           | 2 Cores | 16 GB  | 225 GB | Permanent
Analytics | Livy                 | 1 Core  | 16 GB  | 225 GB | Peramnent
Analytics | JupyterLab           | 2 Cores | 8 GB   | 65 GB  | Permanent
Analytics | Kibana               | 2 Cores | 8 GB   | 65 GB  | Permanent
Analytics | Portainer (Container) | -       | -      | -      | Permanent
Analytics | Rancher (Container)  | - | - | - | Temporary
Analytics | Provectus (Container) | - | - | - | Permanent
Analytics | Prodigy              | - | - | - | Permanent
Analytics | MLFlow*              | - | - | - | Not Built
Analytics | LabelStudio*         | - | - | - | Not Built

*Service not yet created\
**Service created for learning purposes, will be removed in long run

---

### Diagram of Services Currently Developed
![image](https://github.com/j7breuer/diagrams/blob/master/images/dev_environment_diagram.png?raw=true)

---

### ETL Services
The main service used for ETLing is Apache NiFi, a java-based tool that performs well with scaling for big data migration, transformation, and routing tasks.

![image](https://github.com/j7breuer/diagrams/blob/master/images/etl_diagram.png?raw=true)

#### Apache NiFI
<a href="https://nifi.apache.org/">NiFi</a> is currently setup in a 3-node clustered mode for stability.  Prior to Elon's takeover of Twitter, <a href="https://nifi.apache.org/">NiFi</a> was used to stream tweets using the open source firehose endpoint, amounting to 150-300k tweets every 5 minutes.  <a href="https://nifi.apache.org/">NiFi</a> seamlessly handled the transformation, processing, and loading of all tweets and profiles into Elasticsearch.

Currently, <a href="https://nifi.apache.org/">NiFi</a> is used as a scheduler to listen RSS feeds for news article updates amongst popular News services and grab each article once published. 

----

### Database Services
The databases chosen are for predominantly text data as Elasticsearch's search capabilities are most relevant.

![image](https://github.com/j7breuer/diagrams/blob/master/images/db_diagram.png?raw=true)

#### Elasticsearch
<a href="https://www.elastic.co/elasticsearch/">Elasticsearch</a> is used to store all text data, both original data and post-processed data from analytics. <i>And also my favorite tool of them all :)</i>   The majority of all datasets are stored within <a href="https://www.elastic.co/elasticsearch/">Elasticsearch</a> for its search capabilities and scalability to handle large amounts of data.

#### PostgreSQL
<a href="https://www.postgresql.org/">PostgreSQL</a> is used to store simple tables of numeric data.

#### Kafka
<a href="https://kafka.apache.org/">Kafka</a> is categorized as a database but not used as such.  Kafka is utilized in this architecture to handle backpressure and potential bottlenecks in pipelines.  Most <a href="https://kafka.apache.org/">Kafka</a> topics sit in front of analytic post-processes (e.g., language translation).

#### Cassandra*
<a href="https://cassandra.apache.org/_/index.html">Cassandra</a> is not currently built but will be the back end for JanusGraph once built.

#### JanusGraph*
<a href="https://janusgraph.org/">JanusGraph</a> is not currently built but will exist to house graph databases of twitter data among other applicable datasets.

----

### Deployment Services
The deployment services were chosen to create a CI/CD pipeline and include Jenkins, Sonarqube, Nexus, Docker, and Kubernetes.  Together, they orchestrate, enforce coding standards, house artifacts, and deploy necessary repositories.

![image](https://github.com/j7breuer/diagrams/blob/master/images/deployment_diagram.png?raw=true)

#### Jenkins
<a href="https://www.jenkins.io/">Jenkins</a> is the chief orchestrator of all things CI/CD within this architecture.  <a href="https://www.jenkins.io/">Jenkins</a> is integrated with the Sonarqube server, Nexus server, and is in development to deploy to the Kubernetes cluster.  All repositories integrated with Jenkins have Jenkinsfiles at root.

#### Sonarqube
<a href="https://www.sonarsource.com/products/sonarqube/">Sonarqube</a> is the service used for code quality enforcement across repositories being deployed, both for best practices and quality gates.  All repositories integrated with Jenkins will also have a sonar-project.properties file connecting it with the service.

#### Nexus
<a href="https://www.sonatype.com/products/sonatype-nexus-repository">Nexus</a> is the internal repository manager for Docker images, 3rd party artifacts, PyPi, and any other files needed.

#### Docker
The <a href="https://www.docker.com/">Docker</a> server is used for prototyping builds.  Will eventually house all deployments of microservices and containers as Kubernetes is not needed beyond for learning purposes.

#### Kubernetes
<a href="https://kubernetes.io/">Kubernetes</a> is the deployment cluster for all containers and microservices but is only used for learning purposes.  The scale of development does not require Kubernetes and would be too costly to maintain and eat up resources of workstation.

----

### Analytical Services
The analytical services consist of analytics based servers as well as GUIs used to interface with other services (e.g., Kibana for Elasticsearch, Rancher for Kubernetes).

![image](https://github.com/j7breuer/diagrams/blob/master/images/analytics_diagram.png?raw=true)

#### Spark
<a href="https://spark.apache.org/">Spark</a> is set up in conjunction with Livy to enable external access to <a href="https://spark.apache.org/">Spark</a> from JupyterLab, NiFi, among other services.  <a href="https://spark.apache.org/">Spark</a> is still being integrated into the architecture but will be used for large-scale analytical post-processing of data.

#### Livy
<a href="https://livy.apache.org/">Livy</a> exists solely to expose the Spark cluster externally on the home network.

#### JupyterLab
<a href="https://jupyter.org/">JupyterLab's</a> server is utilized as a centralized location for mainly prototyping and scripting of analytics in Python and Scala.

#### Kibana
<a href="https://www.elastic.co/kibana">Kibana</a> is the user interface for interacting with Elasticsearch.  <a href="https://www.elastic.co/kibana">Kibana's</a> capabilities span across dashboard creation, data visualization, query terminal, scripting terminal, index monitoring and more.

#### Portainer
<a href="https://www.portainer.io/">Portainer</a> is a popular container deployed via Docker as a user interface for interacting with containers, volumes, images, and more.  <a href="https://www.portainer.io/">Portainer</a> is utilized to assess logs and metrics of containers deployed.

#### Rancher
<a href="https://www.rancher.com/">Rancher</a> is the user interface of choice that integrates with Kubernetes.  <a href="https://www.rancher.com/">Rancher</a> provides access to all pods across the cluster and their logs, resource allocation, and more.

#### Provectus
<a href="https://github.com/provectus/kafka-ui">Provectus</a> is the 3rd party Kafka user interface chosen to be able to create topics, monitor topics, and adjust settings if needed.

#### Prodigy
<a href="https://prodi.gy/">Prodigy</a> is the NLP annotation tool of choice, a tool that integrates seamlessly into spaCy.

####


















