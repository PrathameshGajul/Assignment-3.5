Q1.Explain what is High availability of Namenode
Ans:
-Hadoop 1.0 NameNode has single point of failure (SPOF) problem- which means that if the NameNode fails, then that Hadoop Cluster will become out-of-the-way.
-This is anticipated to be a rare occurrence as applications make use of business critical hardware with RAS features (Reliability,Availability and Serviceability) for all the NameNode servers.
-In case, if NameNode failure occurs then it requires manual intervention of the Hadoop Administrators to recover the NameNode with the help of a secondary NameNode.
-NameNode SPOF problem limits the overall availability of the Hadoop Cluster in the following ways:
    a)If there are any planned maintenance activities of hardware or software upgrades on the NameNode then it will result in overall downtime of the Hadoop Cluster.
    b)If any unplanned event triggers, which results in the machine crashing, then the Hadoop cluster would not be available unless the Hadoop Administrator restarts the NameNode.
-Hadoop 2.0 overcomes this SPOF shortcoming by providing support for multiple NameNodes.
-It introduces Hadoop 2.0 High Availability feature that brings in an extra NameNode (Passive Standby NameNode) to the Hadoop Architecture which is configured for automatic failover.
-The main motive of the Hadoop 2.0 High Availability project is to render availability to big data applications 24/7 by deploying 2  Hadoop NameNodes –One in active configuration and the other is the Standby Node in passive configuration.
-Hadoop 2.0 High Availability allows users to configure Hadoop clusters with uncalled- for NameNodes so as to eliminate the probability of SPOF in a given Hadoop cluster. 
-The Hadoop Configuration capability allows users to build clusters horizontally with several NameNodes which can operate autonomously through a common data storage pool, thereby, offering better computing scalability when compared to Hadoop 1.0
-With HDP 2.0 High Availability, the complete Hadoop Stack i.e. HBase, Pig, Hive, MapReduce, Oozie are equipped to tackle the NameNode failure problem- without having to lose the job progress or any related data.
-Thus, any critical long running jobs that are scheduled to be completed at a specific time will not be affected by the NameNode failure.



Q2.Explain what is check pointing and how it is useful.
Ans:
-Checkpointing is an essential part of maintaining and persisting filesystem metadata in HDFS.
-It’s crucial for efficient NameNode recovery and restart, and is an important indicator of overall cluster health. 
-However, checkpointing can also be a source of confusion for operators of Apache Hadoop clusters.
-At a high level, the NameNode’s primary responsibility is storing the HDFS namespace.
-This means things like the directory tree, file permissions, and the mapping of files to block IDs. It’s important that this metadata are safely persisted to stable storage for fault tolerance.
-This filesystem metadata is stored in two different constructs: the fsimage and the edit log.
-The fsimage is a file that represents a point-in-time snapshot of the filesystem’s metadata.
-The edit log comprises a series of files, called edit log segments, that together represent all the namesystem modifications made since the creation of the fsimage.
-A typical edit ranges from 10s to 100s of bytes, but over time enough edits can accumulate to become unwieldy.
-A couple of problems can arise from these large edit logs.
-In extreme cases, it can fill up all the available disk capacity on a node, but more subtly, a large edit log can substantially delay NameNode startup as the NameNode reapplies all the edits.This is where checkpointing comes in.
-Checkpointing is a process that takes an fsimage and edit log and compacts them into a new fsimage.
-This way, instead of replaying a potentially unbounded edit log, the NameNode can load the final in-memory state directly from the fsimage.
-However, creating a new fsimage is an I/O- and CPU-intensive operation, sometimes taking minutes to perform.
-During a checkpoint, the namesystem also needs to restrict concurrent access from other users. So, rather than pausing the active NameNode to perform a checkpoint, HDFS defers it to either the SecondaryNameNode or Standby NameNode, depending on whether NameNode high-availability is configured. 



Q3.Explain what is HDFS federation.
Ans:
-Hadoop federation allows scaling the name service horizontally. It uses several namenodes or namespaces which are independent of each other.
-These independent namenodes are federated i.e. they don’t require inter coordination.
-These datanodes are used as common storage by all the namenodes.
-Each datanode is registered with all the namenodes in the cluster.
-These datanodes send periodic reports and responds to the commands from the name nodes.
-We have a block pool which is a set of blocks that belong to a single namespace.
-In a cluster, the datanodes stores blocks for all the block pools. Each block pool is managed independently.
-This enables the name space to generate block ids for new blocks without informing other namespaces.
-If one namenode fails for any reason, the datanode keeps on serving from other namenodes.
-One namespace and its block are collectively called Namespace Volume. When a namespace or a namenode is deleted the corresponding block pool at the datanode is deleted automatically. In the process of cluster up-gradation, each namespace volume is upgraded as a unit.
-Benefits of Hadoop Federation:
a)Scalability and Isolation
b)Generic Storage Service
c)Simple Design



Q4)What are the configuration files that are to be edited for sure while installing a hadoop cluster.
Ans:
The four files that need to be configured explicitly while setting up a single node hadoop cluster are:
a)Core-site.xml
b)HDFS-site.xml
c)YARN-site.xml
d)xml
Settings that need to be done in Core-site.xml are:
 -Configuring the name node address
 -Configuring the rack awareness factor
 -Selecting the type of security
Settings To Be Done In HDFS-site.xml are:
 -Configure port access
 -Manages ssl client authentication
 -Controls Network interface
 -Changes file permission
Settings in yarn-site.xml are:
 -WebAppProxy Configuration
 -MapReduce Configuration
 -NodeManager Configuration
 -ResourceManager Configuration
 -IPC Configuration



