# Hadoop Installation on Windows – Complete Step-by-Step Guide

## 1. Prerequisite
You must have **Java JDK 1.8** installed.

Check your Java version in CMD:
```bash
java -version
If Java is not installed, download JDK 1.8 from Oracle:

https://www.oracle.com/java/technologies/javase/javase-jdk8-downloads.html

Download and extract Java into:
C:\Java\jdk1.8.0_181
(Do NOT install inside Program Files.)

## 2. Download Hadoop

Download Hadoop 3.1.3 from:

https://hadoop.apache.org/releases.html

Extract it to:
C:\hadoop-3.1.3
Rename the folder to:
C:\hadoop

## 3. Configure System Environment Variables
Add User Variable

Variable name: HADOOP_HOME
Variable value: C:\hadoop

Add to System PATH

Edit Path → Add:
%HADOOP_HOME%\bin

## 4. Hadoop Configuration Files

All config files are located at:
C:\hadoop\etc\hadoop
Edit the following files using Notepad++:

4.1 core-site.xml
<configuration>
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://localhost:9000</value>
    </property>
</configuration>


4.2 mapred-site.xml
Create mapred-site.xml if not present.
<configuration>
    <property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
    </property>
</configuration>

5. Create Data Directories

Create folder:
C:\hadoop\data

Inside it create:
C:\hadoop\data\namenode
C:\hadoop\data\datanode

6. hdfs-site.xml
<configuration>
    <property>
        <name>dfs.replication</name>
        <value>1</value>
    </property>

    <property>
        <name>dfs.namenode.name.dir</name>
        <value>C:\hadoop\data\namenode</value>
    </property>

    <property>
        <name>dfs.datanode.data.dir</name>
        <value>C:\hadoop\data\datanode</value>
    </property>
</configuration>

7. yarn-site.xml
<configuration>
    <property>
        <name>yarn.nodemanager.aux-services</name>
        <value>mapreduce_shuffle</value>
    </property>

    <property>
        <name>yarn.nodemanager.auxservices.mapreduce.shuffle.class</name>
        <value>org.apache.hadoop.mapred.ShuffleHandler</value>
    </property>
</configuration>

8. hadoop-env.cmd
Replace %JAVA_HOME% with your Java path:
set JAVA_HOME=C:\Java\jdk1.8.0_181

9. Add Windows-Specific Hadoop Binaries

Hadoop requires Windows native files.

Download from:
https://github.com/s911415/apache-hadoop-3.1.3-winutils

Extract and copy the bin folder.
Replace this folder:
C:\hadoop\bin

10. Verify Hadoop Installation

Check Hadoop version:
hadoop version

If you see no errors → Hadoop is installed successfully.

11. Format Hadoop NameNode

Run:hdfs namenode -format

12. Start Hadoop Services

Open CMD → go to:
cd C:\hadoop\sbin

Start HDFS:
start-dfs.cmd

Start YARN:
start-yarn.cmd

Ensure all 4 Hadoop windows are running.

13. Access Hadoop Web Interfaces
Resource Manager (YARN UI)

http://localhost:8088/cluster

HDFS Overview

http://localhost:9870/dfshealth.html#tab-overview





