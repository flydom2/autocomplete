`NGram Auto-complete `{.western}

\

`1. Configure MySql`{.western}

`$ cd /usr/local/mysql/bin/ `{.western}

``` {.western}
$ ./mysql -uroot -p

2. Create data base
$ create database test;
$ use test;
$ create table output(starting_phrase VARCHAR(250), following_word VARCHAR(250), count INT); 

3. Install docker
$ sudo apt-get update
$ sudo apt-get install wget
$ sudo curl -sSL https://get.daocloud.io/docker | sh
$ sudo docker info

4. Configure Hadoop
$ mkdir bigdata-hadoop
$ cd bigdata-hadoop
$ sudo docker pull joway/hadoop-cluster #pull docker image
$ git clone https://github.com/joway/hadoop-cluster-docker #clone github repository
$ sudo docker network create --driver=bridge hadoop #create hadoop network
$ cd hadoop-cluster-docker

5. Run docker and Hadoop
$ sudo ./start-container.sh
$ ./start-hadoop.sh

6. link MySql with HDFS
$ cd src
$ hdfs dfs -mkdir /mysql
$ hdfs dfs -put mysql-connector-java-*.jar /mysql/  #set hdfs path to mysql-connector*

7. Configure HDFS input/output
$ cd /src
$ hdfs dfs -mkdir -p input
$ hdfs dfs -rm -r /output  #remove old output
$ hdfs dfs -put bookList/*  input/ 

8. Change the following Mysql info. in Driver.java:
local_ip_address  : 
MySQL_port : 
your_password:
hdfs_path_to_mysql-connector: 

9. Run Ngram
$ cd ~/src
$ hadoop com.sun.tools.javac.Main *.java
$ jar cf ngram.jar *.class
$ hadoop jar ngram.jar Driver input /output 2 3 4 
  # 2: size of ngram 
  # 3: threshold，the word will be ignored if its count < threshold
  # 4: following_word_size

10. Set Auto-Complete User Interface
Follow the instruction: 
http://www.bewebdeveloper.com/tutorial-about-autocomplete-using-php-mysql-and-jquery







Author:
Kevin Chen
```
