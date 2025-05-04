
# Spring Boot with Apache Kafka Setup Guide

This guide provides step-by-step instructions to set up Apache Kafka for use with a Spring Boot application, including starting Zookeeper and Kafka servers, and using Offset Explorer to manage Kafka topics and messages.

## Table of Contents
- [Download Apache Kafka](#download-apache-kafka)
- [Extract Kafka Files](#extract-kafka-files)
- [Navigate to Kafka Folder](#navigate-to-kafka-folder)
- [Set JDK Path](#set-jdk-path)
- [Start Zookeeper and Kafka](#start-zookeeper-and-kafka)
- [Install Offset Explorer](#install-offset-explorer)
- [Configure Offset Explorer](#configure-offset-explorer)

## Download Apache Kafka
Download Apache Kafka from the official website.

- **URL**: [https://kafka.apache.org/downloads](https://kafka.apache.org/downloads)

## Extract Kafka Files
Extract the downloaded Kafka zip file and copy the contents into a folder.

- **Example Folder**: `C:\Kafka\kafka_2.13-3.9.0\`

## Navigate to Kafka Folder
Open PowerShell and navigate to the Kafka folder.

```powershell
cd C:\Kafka\kafka_2.13-3.9.0\
```

## Set JDK Path
Set the `JAVA_HOME` environment variable to point to your JDK installation.

```powershell
$env:JAVA_HOME="C:\Program Files\Java\jdk-21"
```

Alternatively, set it permanently in your system environment variables:

```
JAVA_HOME=C:\Program Files\Java\jdk-21
```

## Start Zookeeper and Kafka
Run the following commands in separate PowerShell windows to start Zookeeper and Kafka servers.

1. **Start Zookeeper**:
   ```powershell
   .\bin\windows\zookeeper-server-start.bat .\config\zookeeper.properties
   ```

2. **Start Kafka**:
   ```powershell
   .\bin\windows\kafka-server-start.bat .\config\server.properties
   ```

## Install Offset Explorer
Download and install Offset Explorer (formerly Kafka Tool) to manage Kafka clusters.

- **Website**: [https://www.kafkatool.com/](https://www.kafkatool.com/)
- **Download**: Select `offsetexplorer_64bit` and install it.

## Configure Offset Explorer
Open Offset Explorer and configure a new Kafka cluster.

1. **Cluster Configuration**:
   - **Cluster Name**: Full Stack Project Local Kafka
   - **Bootstrap Server**: `localhost:9092`
   - **Kafka Cluster Version**: 3.3

2. **Create a Topic**:
   - Navigate to the cluster and create a new topic.

3. **Add Data to Partition**:
   - Go to the topic’s partition.
   - Add a message with a key and value:
     - **Example**:
       - **Key**: `message`
       - **Value**: `Welcome to Full Stack Java Developer, Pune`
   - In properties, change the data type from `Byte Array` to `String`.

4. **Retrieve Messages**:
   - Use the play icon in Offset Explorer to run and retrieve the message.

