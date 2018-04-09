In this new interface, we also added new functionalities related to Spark, i.e. connection to CERN’s Spark Clusters and a Monitoring tool. Please read below on how to use them.

### Running Spark Locally

As before, you can use an instance of Spark that is local to your SWAN session. In order to do so, Python notebooks have a [SparkConf](https://spark.apache.org/docs/latest/api/python/pyspark.sql.html#pyspark.sql.SparkConf) variable pre-defined (_swan\_spark\_conf_). Therefore, if you would like to create a [SparkContext](https://spark.apache.org/docs/latest/api/python/pyspark.html#pyspark.SparkContext), you can do:

    from pyspark import SparkContext
    sc=SparkContext.getOrCreate(conf=swan_spark_conf)
    

### Running Spark on CERN Clusters

SWAN also allows to submit computations to Spark Clusters located at CERN. If you are interested in accessing these clusters, please let us know at [swan-admins@cern.ch](mailto:swan-admins@cern.ch), as you need to be added to a specific e-group.

#### Selection of a Spark Cluster

In order to access a particular Spark cluster from SWAN, the first thing you need to do is select that cluster from the "Spark cluster" option of the form, when starting your SWAN session:

![][spark_clusters]

#### Spark Connector

Once your session is started, you will be able to access the Spark cluster you selected from a Python notebook. Please note that you can only connect to the cluster from one notebook at a time. You can shut down a notebook and then connect from another one. You can also restart the kernel of your current notebook if you want to kill the current connection and re-connect from the same notebook.

You will notice that, if you selected a cluster before starting your session, a new Spark button will appear in the toolbar:

![][spark_toolbar]

Once the kernel is ready, you will be able to click on it. When you do, a panel will appear on the right. For now, you will need to type your password, so that we get a kerberos ticket to access the cluster (you only need to do this once per session). In the near future, this step will disappear.

![][spark_auth]

After entering your password, you will see the configuration menu. Here you can add extra Spark configuration options, such as number of cores or memory to use in the Spark executors.

![][spark_options]

When specifying the value of an option, you can use environment variables with the following syntax: {VAR_NAME}.

You can inline-edit an option already added, by clicking in the option name or value. To remove it, click in the X that appears when hovering over it. If it finds any problem with your configuration, it will display a warning. Hover over the highlighted option to read the reason.

After clicking on "Connect", the connection will be established. This may take some time, but you can follow the logs to see what is happening. Once the connection process has finished, there will be two new variables available in your notebook for you to use:

*   **sc** = [SparkContext](https://spark.apache.org/docs/latest/api/python/pyspark.html#pyspark.SparkContext)
*   **spark** = [SparkSession](https://spark.apache.org/docs/latest/api/python/pyspark.sql.html#pyspark.sql.SparkSession)

You are now ready to start submitting your Spark jobs!

SWAN also provides automatic saving of Spark configuration options: any option added in the configuration menu will be saved in the notebook metadata. This means that every time you open that notebook and use the Spark connector, the configurations will load automatically, so that you do not have to type them again! If you modify them, the changes will be saved.

### Spark Monitoring

If you are running Spark jobs, either locally or on a cluster, you can now keep track of their execution right from inside the notebook. This functionality is provided by the Spark Monitor, which will show an interactive monitoring display in the notebook anytime you run a cell that triggers a Spark computation.

![][spark_monitor]

With this tool you can see in detail the jobs, including stages, and the tasks that are running. You can also see the resource allocation and access the Spark UI.

To make this work, SWAN exports to the notebook a SparkConf object in the variable _swan\_spark\_conf_. You need to use this variable as the conf source, like so:

    sc = SparkContext(conf = swan_spark_conf)
    

To add more configurations, add them to this this SparkConf object, by issuing:

    swan_spark_conf.set(option_name, option_value)
    

Keep in mind that we add a jar in spark.driver.extraClassPath option. If you need to add more paths to this option, don’t forget to concatenate, like this:

    extra_class = swan_spark_conf.get('spark.driver.extraClassPath') + ':/another_file.jar'
    swan_spark_conf.set('spark.driver.extraClassPath', extra_class)


[spark_clusters]: images/spark_clusters.png "Choose Spark Cluster"
[spark_toolbar]: images/spark_toolbar.png "Spark Connector button"
[spark_auth]: images/spark_auth.png "Spark Connector authentication"
[spark_options]: images/spark_options.png "Spark Connector options"
[spark_monitor]: images/spark_monitor.png "Spark Monitor"
