# Technical-paper
Technical paper NoSQL Database
# NoSQL Database
There are several popular NoSQL databases which have gained recognition and are usually considered before other NoSQL alternatives. There are several of these databases (Aerospike, Cassandra, Couchbase, CouchDB, HBase, MongoDB and Voldemort) by performing and introduce the first quality attribute based evaluation of NoSQL databases.
1.  Aerospike
2.  Cassandra
3.  CouchDB
4.  Couchbase
5.  MongoDB
## Aerospike
Aerospike is a (formerly known as Citrusleaf [1] and recently open-sourced)NoSQL shared-nothing key-value database which offers mainly AP (Availability and Partition-Tolerance) characteristics. Additionally, the developers claim that it provides high consistency  by trading off availability and consistency at low granularity in specific subsystems, restricting communication latencies, minimizing cluster size, maximizing consistency and availability during failover situations and automatic conflict resolution. Consistency is guaranteed by using synchronous writes to replicas, guaranteeing immediate consistency. This immediate consistency can be relaxed if the software architects view that as a necessity. Durability is ensured by guaranteeing the use of flash/SSD on every node and performing direct reads from flash, as well as replication on several different layers.

Failover can be handled in two different ways : focusing on High consistency on AP mode, or on Availability in CP (Consistency and Partition-Tolerance) mode. The former uses techniques to “virtually eliminate network based partitioning”, including fast heartbeats and consistent Paxos based cluster formation. These techniques favor Consistency over Availability to ensure that the system does not enter a state of network partition. If, however, partitioning occurs, Aerospike offers two conflict handling policies: one relies on the database’s auto-merging capabilities, and the other offloads the conflict to the application layer so that application developers can resolve the conflicts by themselves and re-write the right data back to the database. The second way that Aerospike manages failover is to provide Availability while in CP mode. In this mode, availability needs to be sacrificed by, for instance, forcing the minority quorum(s) to halt, thus avoiding data inconsistency if a network split occurs.

Aerospike is, henceforth, an in-memory database with disk persistence, automatic data partitioning and synchronous replication, offering cross data center replication and configurability in the failover handling mechanism, preferring full consistency or high consistency.

## Cassandra

Cassandra is similar to BigTable in what concerns the data model. The minimal unit of storage is a column, with rows consisting of columns or super columns (nested columns). Columns themselves consist of the name, value and timestamp, all of which are provided by the client. Since it is column-based, rows need not have the same number of columns .

Cassandra supports a SQL-like language called CQL, together with other protocols. Indexes and secondary indexes are supported, and atomicity is guaranteed at the level of one table row. Persistence is ensured by logging. Consistency is highly tunable according to the desired operation – the application developer can specify the desired level of consistency, trading off latency and consistency. Conflicts are resolved based on timestamps (the newest record is kept). The database operates in master-master mode [2], where no node is different from another, and combines disk-persistence with in-memory caching of results, resulting in high write throughput operations [2] The master-master architecture makes it easy for horizontal scalability to happen . There are several different partitioning techniques and replication can be automatically managed by the database .

#### CouchDB

Apache CouchDB is another open-source project, written in Erlang, and following a document-oriented approach [1]. Documents are written in JSON and are meant to be accessed with CouchDB’s specific implementation of MapReduce views written in Javascript.
This database uses a B-tree index [1], updated during data modifications. These modifications have ACID properties on the document level and the use of MVCC (Multi-Version Concurrency Control) enables readers to never block [1]. CouchDB’s document manipulation uses optimistic locks by updating an append-only B-tree for data storage, meaning that data must be periodically compressed. This compression, in spite of maintaining availability, may hinder performance.

Regarding fault-tolerant replication mechanisms, CouchDB supports both master-slave and master-master replication that can be used between different instances of CouchDB or on a single instance. Scaling in CouchDB is achieved by replicating data, a process which is performed asynchronously. It does not natively support sharding/partitioning [1]. Consistency is guaranteed in the form of strengthened eventual consistency [1], and conflict resolution is performed by selecting the most up to date version (the application layer can later try to merge conflicting changes, if possible, back into the document). CouchDB’s programming interface is REST-based [1, 57]. Ideally, CouchDB should be able to fit the whole dataset into the RAM of the cluster, as it is primarily a RAM-based database.

##### Couchbase

Couchbase is a combination of Membase (a key-value system with memcached compatibility) and CouchDB. It can be used in key-value fashion, but is considered a document store working with JSON documents (similarly to CouchDB) [1].
Documents, in Couchbase, have an intrinsic unique id and are stored in what are called data buckets. Like CouchDB, queries are built using MapReduce views in Javascript. The optimistic locking associated with an append-only B-tree is also implemented like in CouchDB. The default consistency level is eventual consistency (due to MapReduce views being constructed asynchronously). There is also the option of specifying that data should be indexed immediately [1].

A major difference when comparing Couchbase with CouchDB regards sharding [1]. Whereas CouchDB does not natively support sharding (there are projects, such as CouchDB Lounge [1] which enable this), Couchbase comes with transparent sharding off-the-shelf, with application transparency. Replication is also a major point of difference between the two databases, as couchbase supports intercluster and intracluster replication. The latter is performed within a cluster, guaranteeing immediate consistency. The former kind of replication ensures eventual consistency and is made asynchronously between geographically distributed clusters (conflict resolution is performed in the same way CouchDB does it). This database is mostly intended to run in-memory, so as to hold the whole dataset in RAM [1,3].

###### MongoDB

MongoDB is an open-source document-oriented database written in C++ and developed by the 10gen company. It uses JSON (data is stored and transferred in a binary, more compact form named BSON), allowing for a schemaless data model where the only requirement is that an id is always present [1].

MongoDB’s horizontal scalability is mainly provided through the use of automatic sharding. Replication is also supported using locks and the asynchronous master-slave model, meaning that writes are only processed by the master node and reads can be made from both the master node and from one of the slave nodes. Writes are propagated to the slave nodes by reading from the master’s oplog (operation log). Database clients can choose the kind of consistency models they wish, by defining whether reads from secondary nodes are allowed and from how many nodes the confirmation must be obtained.

Document manipulation is a strong focus of MongoDB, as the database provides different frameworks (e.g. MapReduce and Aggregation Framework) and ways of interacting with documents [1]. These can be queried, sorted, projected, iterated with cursors, aggregated, among other operations. The changes to a document are guaranteed to be atomic. Indexing can be used on one or several fields (implemented using B-trees), with the possibility of using two-dimensional spatial indexes for geometry-based data [1]. There are many different programming interfaces supported by MongoDB, with most popular programming languages having native bindings. A REST interface is also supported [1].



Reference link
* [kuzetsov S, Poskonin A (2014) Nosql data management systems. Program Comput Softw 40(6): 323–332.] (http://scholar.google.com/scholar_lookup?&title=Nosql%20data%20management%20systems&journal=Program%20Comput%20Softw&volume=40&issue=6&pages=323-332&publication_year=2014&author=Kuznetsov%2CS&author=Poskonin%2CA) 
* [Gudivada VN, Rao D, Raghavan VV (2014) Nosql systems for big data management In: Services (SERVICES), 2014 IEEE World Congress On, 190–197.. IEEE, Anchorage, AK, USA.] (http://scholar.google.com/scholar_lookup?&title=Nosql%20systems%20for%20big%20data%20management&pages=190-197&publication_year=2014&author=Gudivada%2CVN&author=Rao%2CD&author=Raghavan%2CVV)
*  [Cudré-Mauroux P, Enchev I, Fundatureanu S, Groth P, Haque A, Harth A, Keppmann FL, Miranker D, Sequeda JF, Wylot M (2013) Nosql databases for rdf: an empirical evaluation In: The Semantic Web–ISWC 2013, 310–325.. Springer, Berlin.](http://scholar.google.com/scholar_lookup?&title=Nosql%20databases%20for%20rdf%3A%20an%20empirical%20evaluation&pages=310-325&publication_year=2013&author=Cudr%C3%A9-Mauroux%2CP&author=Enchev%2CI&author=Fundatureanu%2CS&author=Groth%2CP&author=Haque%2CA&author=Harth%2CA&author=Keppmann%2CFL&author=Miranker%2CD&author=Sequeda%2CJF&author=Wylot%2CM)
* [Google](https://journalofbigdata.springeropen.com/articles/10.1186/s40537-015-0025-0) 
