spark-cassandra-collabfiltering
===============================
This code goes with my [Datanami article](www.datanami.com/2014/12/11/apache-spark-java-8-big-data-team-2015/).

It illustrates MLLib on Spark using an example based on collaborative filtering  of employee ratings for companies.

It shows the exact same  Spark client functionality written in Java 7 and Java 8. The new  new Java 8 features that make Spark's functional style much easier

I use Cassandra providing the data to Spark, and there's a synthesized training/validation set  with accompanying spreadsheet to let you tweak parameters.

Here's how to get it working:

To setup (tested on Ubuntu 14.04):
- Install JDK Java8.
    ````sudo apt-get install oracle-java8-installer````
- Get [Spark](http://spark.apache.org/downloads.html).
    - Download 1.1.0 for Hadoop 2.4. We will not be using Hadoop even though this build supports it.
    - Untar the spark tarball. (E.g., in ````~/dev````)
    - Test the installation with 
    ````./bin/run-example SparkPi````
- See QuickStart in below for more instructions and tutorials on setup.

Get Eclipse:
- Download Eclipse Luna 4.4.1 Ubuntu 64 Bit (or 32 Bit) from [Eclipse.org](https://eclipse.org/downloads/). Only the latest Eclipse supports Java 8.
- Untar, run Eclipse.
- Set your Java 8 JDK as the default JDK.
- Install Maven2 Eclipse, 
    - *Menu Help -> Install New Software…*
    - Add [this repository](http://download.eclipse.org/technology/m2e/releases)
    - Check Maven Integration for Eclipse, then install.

Project 
- Right-click on ````pom.xml````, choose  *Maven-> install*.
- This will now download Spark jars; it will take a while.
- It will also set your Eclipse project's source level to Java 8.

Dataset
- ````ratings.csv```` is generated from ````ratings.ods````, which is a spreadsheet for  synthesizing data sets to test and fine tune your model. 
- Adjust ````ratings.ods```` and save as CSV. See ````readme.txt```` in data directory for instructions.
 
Cassandra
- Instructions for getting Cassandra: [here](http://www.datastax.com/documentation/cassandra/2.0/cassandra/install/installDeb_t.html)
- Run Cassandra:
````sudo /usr/bin/cassandra````
- We will be runnning Cassandra and Spark locally with console, rather than remotely in a cluster as daemon/service.
- Create schema by running attached SQL as follows:
    - In workspace root, run
     ````cqlsh -f ./collabfilter/src/sql/collab_filter_schema.sql````

Running tests:
-  Run ````collabfilter.CollabFilterCassandraDriver.main```` or  the ````CollabFilterTest```` unit test.

More references:
- QuickStart has [more on setup](https://spark.apache.org/docs/1.1.0/quick-start.html).
- You can find a [collaborative filtering tutorial for Spark](https://spark.apache.org/docs/1.1.0/mllib-collaborative-filtering.html)  and a [tutorial on the Spark-Cassandra Java connector](http://www.datastax.com/dev/blog/accessing-cassandra-from-spark-in-java) which I drew on.
- However, note that the example code in the Spark-Cassandra tutorial is outdated. The Java API class was [moved to](https://github.com/datastax/spark-cassandra-connector/commit/36ad9cd6c13600144e3e27533587db926e41af2e)  the  japi subpackage.
- Bug in Guava version. The ````pom.xml```` specifies Guava 15. This is because the Guava 14 used with the Spark-Cassandra connector is mismatched to the Guava 15 or above expected by Spark, which includes additional methods.

 


