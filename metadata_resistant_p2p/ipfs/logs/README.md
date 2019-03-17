## log files

This folder contains logs from packets received by DHT nodes running in the network which are relevant for the purpose of privacy and metadata research.

`ipfs-cli` is a good high level tool to log and filter through events from several ipfs subsystems.

```
$ ipfs log tail >> '$(date +%F_%T)'.log
$ ipfs log level <subsystem> debug 
```

Interesting subsystems to log events are:

- `bitswap` 
- `blockservice` 

- `transport`
- `dht`
- `dht.pb` 
- `bitswap_network`
- `blockstore`


Some interesting filter commands that might reveal information about user behavior (e.g. what content is being requested, stored and by whom)

A. Filters all packets from the routing protocol for content lookup (i.e. what peers are requesting)

```

$ cat 01_2019-02-08_15\:04\:19.log | grep -e 'handleGetValue' -e 'handlePutValue'

{"TraceID":8906013756250657346,"SpanID":632482766161050178,"ParentSpanID":0,"Operation":"handleGetValue","Start": "2019-02-08T14:45:13.465300855Z","Duration":244962,"Tags":{"system":"dht"},"Logs":[{"Timestamp":"2019-02-08T14:45:13.465320834Z","Fields":[{"Key":"peerID","Value":"QmdKmRt7mf1EZRE2C5RZbigKu577n1bJon4kbUyrEHmVkw"}]}]}

```


B. Filters all packets from the routing protocol for content storage (i.e. what peers are storing)

```

$ cat 01_2019-02-08_15\:04\:19.log | grep -e 'handlePutValue'

{"TraceID":8906013756250657346,"SpanID":632482766161050178,"ParentSpanID":0,"Operation":"handleGetValue","Start": "2019-02-08T14:45:13.465300855Z","Duration":244962,"Tags":{"system":"dht"},"Logs":[{"Timestamp":"2019-02-08T14:45:13.465320834Z","Fields":[{"Key":"peerID","Value":"QmdKmRt7mf1EZRE2C5RZbigKu577n1bJon4kbUyrEHmVkw"}]}]}

```
