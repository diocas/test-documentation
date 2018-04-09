# Running Spark on CERN Clusters

SWAN also allows to submit computations to Spark Clusters located at CERN. If you are interested in accessing these clusters, please let us know at [swan-admins@cern.ch](mailto:swan-admins@cern.ch), as you need to be added to a specific e-group.

### Selection of a Spark Cluster

In order to access a particular Spark cluster from SWAN, the first thing you need to do is select that cluster from the "Spark cluster" option of the form, when starting your SWAN session:

![][spark_clusters]

### Spark Connector

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


[spark_clusters]: ../images/spark_clusters.png "Choose Spark Cluster"
[spark_toolbar]: ../images/spark_toolbar.png "Spark Connector button"
[spark_auth]: ../images/spark_auth.png "Spark Connector authentication"
[spark_options]: ../images/spark_options.png "Spark Connector options"