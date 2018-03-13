# RecommendationSystem

Based on Docker:https://docs.docker.com/docker-for-mac/

mkdir bigdata

$ cd bigdata

$ sudo docker pull joway/hadoop-cluster 

$ git clone https://github.com/joway/hadoop-cluster-docker

$ sudo docker network create --driver=bridge hadoop #搭建一个bridge供hadoop各节点通信

$ cd hadoop-cluster-docker

$ sudo ./start-container.sh

$ ./start-hadoop.sh

#Until this step we have entered the HADOOP model.

cd RecommenderSystem

hdfs dfs -mkdir /input

hdfs dfs -put input/* /input

hdfs dfs -rm -r /dataDividedByUser

hdfs dfs -rm -r /coOccurrenceMatrix

hdfs dfs -rm -r /Normalize

hdfs dfs -rm -r /Multiplication

hdfs dfs -rm -r /Sum

cd src/main/java/

hadoop com.sun.tools.javac.Main *.java

jar cf recommender.jar *.class

hadoop jar recommender.jar Driver /input /dataDividedByUser /coOccurrenceMatrix /Normalize /Multiplication /Sum

hdfs dfs -cat /Sum/*

#args0: original dataset

#args1: output directory for DividerByUser job

#args2: output directory for coOccurrenceMatrixBuilder job

#args3: output directory for Normalize job

#args4: output directory for Multiplication job

#args5: output directory for Sum job

hdfs dfs -ls /

#http://localhost:50070/explorer.html#/
