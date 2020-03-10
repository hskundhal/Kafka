# Kafka incident for new DC implementation

root cause

zookeeper got wrong host file
 
 `dmesg -t` shows
 `ping timeout of 5 secs expired, recv timeout 5, last rx 4398127505, last ping 4398128760, now 4398130048
 connection2:0: detected conn error (1022)
 connection1:0: ping timeout of 5 secs expired, recv timeout 5, last rx 4398127506, last ping 4398128760, now 4398130049`

Java version mismatch with the confluent package.
