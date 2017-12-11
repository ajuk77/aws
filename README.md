# aws
AWS repository holds all the solutions related to amazon webs services

Steps to execute the project

References: http://blog.cloudera.com/blog/2012/12/how-to-run-a-mapreduce-job-in-cdh4/

Cluster Configuration emr - 5.0.0 (Core Hadoop Cluster - Select the first option)
Location : N. Virginia  

Steps:
1) Build the java code and generate the executable jar 

2) upload the jar and input file on S3

3) Provision a cluster on AMAZON EMR

4) ssh to master instance of EMR using hadoop@"MASTER-URL"

5) Copy the jar from S3 to local instance
   aws s3 cp s3://testuseraj/jar/logprocessor-1.0.jar ./

6) Copy the input file from S3 to local instance
   aws s3 cp s3://testuseraj/input/bank.txt ./
 
7) create a directory in hadoop file system
   hadoop fs -mkdir /gaps

8) Copy the input file into HDFS
   hadoop fs -put ./bank.txt /gaps
   
9) Run the code
   hadoop jar ./logprocessor-1.0.jar com.cs.mapreduce.logprocessor.LogAnalyzer /gaps/bank.txt /gaps/output
 
10) Merge the output
    hdfs dfs -getmerge /gaps/output/ ./out.csv
 
11) Upload the out to S3
    aws s3 cp ./out.csv s3://testuseraj/output/

12) Create a manifest file to identify the text files you want to import. (Refer the file from visualization-aws folder)

13) Upload manifest file to Amazon s3
    https://s3.amazonaws.com/testuseraj/manifest.json

14) On the Amazon QuickSight start page, choose Manage data.

15) Create new dataset by choosing Amazon s3 icon.

16) For DataSource name , type a name for the daa source.

17) Upload a manifest file

18)Choose connect.


