# Kafka replication increase or decrease

 Generate partitions map first
`kafka-reassign-partitions --zookeeper localhost:2181,localhost2:2181,localhost3:2181 --broker-list "1001,1002,1003" --topics-to-move-json-file topics.json --generate > partitions.json`


Verify that partitions for existing replicas are in same way as generated plan (partitions.json), else you can fix it via using current distribution map of kafka partitions from below command
`kafka-topics --bootstrap-server localhost:9092 --topic cmo --describe`

Edit partitions.json and Add replicas in generated parition map according to replication increase or remove replicas from partition map based on replication decrease.

Now its time to execute the partitions.json.
`kafka-reassign-partitions --zookeeper localhost:2181 --reassignment-json-file partitions.json --execute`

Monitor CPU , Disk IO and Memory for kafka brokers, if replciation is increased then there will be use of resources.

Verify that change is done with below
`kafka-reassign-partitions --zookeeper localhost:2181 --reassignment-json-file partitions.json --verify`


# Incident
while increasing replication on prod instances , due to high volume , disk io got stuck at 100% and kafka nodes came down one by one with OOM errors in logs.
This caused partition reassignment stuck in repartitioning and not going away. Everything came back up and started running but particular topic still in repartitioning mode.
Solution : Cancel re-partition
--Proceess: -------------------
$ zookeeper-shell localhost:2181,localhost2:2181,localhost3:2181
$ delete /admin/reassign_partitions
$ close
$ quit

Future to try
-------------
Use a Throttle & extend the Timeout
--throttle <Long: throttle>            The movement of partitions will be
                                         throttled to this value (bytes/sec).
                                         Rerunning with this option, whilst a
                                         rebalance is in progress, will alter
                                         the throttle value. The throttle
                                         rate should be at least 1 KB/s.
--timeout <Long: timeout>              The maximum time in ms allowed to wait
                                         for partition reassignment execution
                                         to be successfully initiated
                                         (default: 10000)
