# Performance testing on kafka

`kafka-producer-perf-test --topic test1 --num-records 1000000 --throughput 10000 --producer-props bootstrap.servers=kafka03:9092 batch.size=1000 acks=0 linger.ms=100000 buffer.memory=4294967296  request.timeout.ms=300000 --record-size 1000`

```48952 records sent, 9778.7 records/sec (9.33 MB/sec), 68.0 ms avg latency, 430.0 ms max latency.
50949 records sent, 10017.5 records/sec (9.55 MB/sec), 61.9 ms avg latency, 352.0 ms max latency.
50949 records sent, 10003.7 records/sec (9.54 MB/sec), 55.4 ms avg latency, 109.0 ms max latency.
50949 records sent, 10001.8 records/sec (9.54 MB/sec), 55.6 ms avg latency, 115.0 ms max latency.
50949 records sent, 9999.8 records/sec (9.54 MB/sec), 63.8 ms avg latency, 474.0 ms max latency.
50949 records sent, 10003.7 records/sec (9.54 MB/sec), 55.1 ms avg latency, 110.0 ms max latency.```

throughput 10000 limits messages per second.

Test1 topic will be created if default topic creation is enabled.

