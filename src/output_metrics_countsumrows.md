# CountSumRows statistics

In the output generated by ad-hoc or snapshot-diff mode, a third group that optionally can be shown are the 'countsumrows' statistics. 
These statistics are taken from the YSQL (normally port 13000) http endpoint. 
If no SQL interaction did happen between YSQL/postgres and DocDB, there will be no statistics shown.

- If a statistic has a zero count in both the begin and end snapshot, it will be skipped.
- If a statistic has a non-zero count in both the begin and end snapshot, and subtracting the values leads to zero, it will be skipped.
- if a statistic has a lower value in the end snapshot than in the begin snapshot, currently the statistics will be shown, and might get negative.

This is how countsumrows statistic output looks like:
```
192.168.66.80:13000  handler_latency_yb_ysqlserver_SQLProcessor_InsertStmt                                1 avg:          18.552 tot:          18.552 ms, avg:               1 tot:               1 rows
192.168.66.80:13000  handler_latency_yb_ysqlserver_SQLProcessor_SingleShardTransactions                   1 avg:          18.552 tot:          18.552 ms, avg:               1 tot:               1 rows
192.168.66.80:13000  handler_latency_yb_ysqlserver_SQLProcessor_Single_Shard_Transactions                 1 avg:          18.552 tot:          18.552 ms, avg:               1 tot:               1 rows
192.168.66.80:13000  handler_latency_yb_ysqlserver_SQLProcessor_Transactions                              1 avg:          18.552 tot:          18.552 ms, avg:               1 tot:               1 rows
```
Explanation:

| hostname:port        | statistic name                                                       | count | sum / snapshot time (s) | sum total    | sum unit | rows / count | rows total  |
|----------------------|----------------------------------------------------------------------|-------|-------------------------|--------------|----------|--------------|-------------|
| 192.168.66.80:13000  | handler_latency_yb_ysqlserver_SQLProcessor_InsertStmt                | 1     | avg: 18.552             | tot: 18.552  | ms       | avg:  1      | tot: 1 rows |
| 192.168.66.80:13000  | handler_latency_yb_ysqlserver_SQLProcessor_SingleShardTransactions   | 1     | avg: 18.552             | tot: 18.552  | ms       | avg:  1      | tot: 1 rows |
| 192.168.66.80:13000  | handler_latency_yb_ysqlserver_SQLProcessor_Single_Shard_Transactions | 1     | avg: 18.552             | tot: 18.552  | ms       | avg:  1      | tot: 1 rows |
| 192.168.66.80:13000  | handler_latency_yb_ysqlserver_SQLProcessor_Transactions              | 1     | avg: 18.552             | tot: 18.552  | ms       | avg:  1      | tot: 1 rows |