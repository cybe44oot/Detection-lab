# Detection-lab

### SIEM Implementation and Log Analysis Lab

 This lab will cover setting up a basic SIEM solution, collecting logs, and performing analysis. Feel free to customize it as needed!
SIEM Implementation and Log Analysis Lab.

Table of Contents

  1. Introduction
  2.  Prerequisites
  3.  Lab Setup
        Step 1: Install SIEM Solution
        Step 2: Configure Log Sources
        Step 3: Collect Logs
        Step 4: Analyze Logs
    4. Conclusion

## Introduction

This lab provides a hands-on experience in implementing a Security Information and Event Management (SIEM) system. Participants will learn how to set up a SIEM, configure log sources, collect logs, and perform basic log analysis to identify security incident.

## Prerequisites

    Basic understanding of networking and security concepts.
    A computer with at least 8 GB of RAM.
    Virtualization software (e.g., VirtualBox, VMware).
    A Linux distribution (e.g., Ubuntu) for the SIEM server.
    Administrative access to install software.

## Lab Setup
Step 1: Install SIEM Solution

 1:   Choose a SIEM Solution: For this lab, we'll use ELK Stack (Elasticsearch, Logstash, Kibana).

 2: Install Elasticsearch

    wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-8.x.x-linux-x86_64.tar.gz
    
tar -xzf elasticsearch-8.x.x-linux-x86_64.tar.gz

cd elasticsearch-8.x.x

./bin/elasticsearch

3: Install logstash

wget https://artifacts.elastic.co/downloads/logstash/logstash-8.x.x-linux-x86_64.tar.gz

tar -xzf logstash-8.x.x-linux-x86_64.tar.gz

cd logstash-8.x.x

 4: Install Kibana

wget https://artifacts.elastic.co/downloads/kibana/kibana-8.x.x-linux-x86_64.tar.gz

tar -xzf kibana-8.x.x-linux-x86_64.tar.gz

cd kibana-8.x.x

./bin/kibana

Step 2: Configure Log Sources

   1: Configure a Sample Log Source: We will create a sample application that generates logs. You can create a simple Python script:

    import logging
import time

logging.basicConfig(filename='sample.log', level=logging.INFO)

while True:
    logging.info("Sample log entry")
    time.sleep(5)

    2: Send Logs to Logstash: Create a Logstash configuration file (logstash.conf):

    input {
    file {
        path => "/path/to/sample.log"
        start_position => "beginning"
    }
}
output {
    elasticsearch {
        hosts => ["http://localhost:9200"]
        index => "logs-%{+YYYY.MM.dd}"
    }
}

step 3: collect logs 

1: start logstash 
./bin/logstash -f logstash.conf

2: Verify Logs in Elasticsearch: Open your browser and navigate to http://localhost:9200/_cat/indices?v to see the logs indexed.

Step 4: Analyze Logs

 1: Open Kibana: Navigate to http://localhost:5601 in your browser.

2: Create an Index Pattern: Go to "Management" > "Index Patterns" and create a new index pattern for logs-*.

3: Visualize Logs: Use Kibana's Discover feature to query and visualize your logs. Create basic visualizations (e.g., line charts, pie charts) to analyze log trends.

## Conclusion

In this lab, you learned how to set up a basic SIEM using the ELK Stack, configure log sources, collect logs, and perform initial log analysis. This foundational knowledge can be expanded upon for more advanced security monitoring and incident response tasks.
