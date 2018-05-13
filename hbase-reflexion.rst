
hbase reflexions
=================

.. post:: May 13, 2018
   :tags: phoenix, spark, hive, solr
   :category: database

hbase looks a powerfull tool in complement of hive. While hive is wel suited
for ETL and data historisation, it cannot offer sub-second access to thousand
of users.

Hbase comes with a powerful compagnion aka Phoenix that provides many features,
while keeping the hbase features intact. Phoenix provides a jdbc driver to
hbase. This distinction adds many improvements:

1. it offers sql, joins, secondary indexes, transactions, sequences on top of hbase.

2. it simplifies hive, spark, solr, and general programming access to hbase
   data.

JDBC overview
-------------

jdbc access can be done with `kerberos <https://community.hortonworks.com/questions/47138/phoenix-query-server-connection-url-example.html>`_ on the form 

.. code-block:: java

   "jdbc:phoenix:thin:url=<scheme>://<server-hostname>:<port>;authentication=SPNEGO;principal=my_user;keytab=/home/my_user/my_user.keytab"

Hive integration
----------------

Phoenix tables can be mounted into hive thanks to a `recent plugin`_. In comparaison
to hbase plugin, this allows fast join to hive table (to be tested). However,
this plugin needs phoenix 4.8.0+ and HDP ships with phoenix 4.7.0 and need to
be updated. Also there is some details
`in this blog <https://superuser.blog/upgrading-apache-phoenix-hdp/>`_ or `in this gist <https://gist.github.com/phaneesh/16f77539d1f1249aa9b0e5a847ce48a0>`_


Spark integration
-----------------

Spark can read and write from phoenix `here on SOF <https://stackoverflow.com/questions/40329968/apache-spark-ways-to-read-and-write-from-apache-phoenix-in-java>`_ or `here on official <https://phoenix.apache.org/phoenix_spark.html>`_. The good point is it can be done from scala or python.

Solr integration
----------------

Solr integration with hbase is a good idea: hbase contains the truth and solr allows fast lookup to discover it. However, setting up solr on top of hbase is a pain. Phoenix simplifies drastically that :
`here <https://nicholasmaillard.wordpress.com/2014/12/27/phoenix-to-solr-in-20-minutes/>`_


.. _recent plugin: https://phoenix.apache.org/hive_storage_handler.html
