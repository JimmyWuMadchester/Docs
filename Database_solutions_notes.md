# Data management solutions compared

I myself am a little bit confused about how RDBMS, hadoop, SQL and NoSQL etc. all fit in a bigger picture. 
Therefore, I'm going to explore most of the frequently mentioned and used ones. What are they? And when
do we use them? What's the typical applications of them?

I'll start with gathering notes from other resources. And hopefully in the end, writing an article myself to
best put the puzzels together.

--Update: I found this blog [http://blog.nahurst.com/visual-guide-to-nosql-systems](http://blog.nahurst.com/visual-guide-to-nosql-systems) very helpful showing the overview and big picture of the most mainstream database systems already.

## Hadoop

Hadoop a file system and not a database.

[Hadoop is basically 2 things](https://stackoverflow.com/a/16930049/5098156), a FS (Hadoop Distributed File System) and a computation framework (MapReduce). HDFS allows you store huge amounts of data in a distributed (provides faster read/write access) and redundant (provides better availability) manner. And MapReduce allows you to process this huge data in a distributed and parallel manner. But MapReduce is not limited to just HDFS. Being a FS, HDFS lacks the random read/write capability. It is good for sequential data access. And this is where HBase comes into picture. It is a NoSQL database that runs on top your Hadoop cluster and provides you random real-time read/write access to your data.

# NoSQL

NoSQL databases are often very fast, do not require fixed table schemas, avoid join operations by storing 
denormalized data, and are designed to scale horizontally. The most popular NoSQL systems include MongoDB, 
Couchbase, Riak, Memcached, Redis, CouchDB, Hazelcast, Apache Cassandra, and HBase,[25] which are all 
open-source software products.

# Apache Kafka vs Apache Storm

[real-time-system --> Kafka --> Storm --> NoSql --> BI(optional)](https://stackoverflow.com/a/21808667/5098156)
