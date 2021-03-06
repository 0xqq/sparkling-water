.. _sw_azure:

Running Sparkling Water on Databricks Azure Cluster
---------------------------------------------------

Sparkling Water, PySparkling and RSparkling can be used on top of Databricks Azure Cluster. This tutorial is
the **Scala Sparkling Water**.

For Pysparkling, please visit :ref:`pysparkling_azure` and
for RSparkling, please visit :ref:`rsparkling_azure`.

To start Sparkling Water ``H2OContext`` on Databricks Azure, the steps are:

1.  Login into Microsoft Azure Portal

2.  Create Databricks Azure Environment

    In order to connect to Databricks from Azure, please make sure you have created user inside Azure Active Directory and using that user for the Databricks Login.

3.  Add Sparkling Water dependency

    In order to create the Java library in Databricks, go to **Libraries**, select **Maven** as the library source and type the following into the coordinates field: ``sparkling-water-package_2.11:SUBST_SW_MINOR_VERSION``.

    .. figure:: ../images/databricks_sw_maven.png
        :alt: Uploading Sparkling Water assembly JAR

    You can configure each cluster manually and select which libraries should be attached or you can configure the library to be attached to all future clusters. It is advised to restart the cluster in case you attached the library to already running cluster to ensure the clean environment.

4.  Create the cluster

    - Make sure the assembly JAR is attached to the cluster

    - For Sparkling Water SUBST_SW_VERSION select Spark SUBST_SPARK_VERSION

    It is advised to always use the latest Sparkling Water and Spark version for the given Spark major version.

    .. figure:: ../images/databricks_cluster_creation.png
        :alt: Configured cluster ready to be started

5.  Create Scala notebook and attach it to the created cluster. To start ``H2OContext``, the init part of the notebook should be:

    .. code:: scala

        import org.apache.spark.h2o._
        val hc = H2OContext.getOrCreate(spark)

6.  And voila, we should have ``H2OContext`` running

    .. figure:: ../images/databricks_sw_h2o_context_running.png
        :alt: Running H2O Context

    Please note that accessing H2O Flow is not currently supported on Azure Databricks.