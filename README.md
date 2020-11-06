[![license](https://img.shields.io/github/license/mashape/apistatus.svg?maxAge=2592000)](https://opensource.org/licenses/MIT)


MySQL Slow Query Log GROK pattern for Graylog
=============================================

Pattern
-------

    "name":"MYSQLSLOWQUERYLOG",
    "pattern": "(?s) Time:%{SPACE}%{TIMESTAMP_ISO8601:mysql_slow_querydate}%{GREEDYDATA}User@Host: (?:%{USERNAME:mysql_slow_clientuser})\\[(?:%{DATA:mysql_slow_clientdbname})\\] @ (?:%{DATA:mysql_slow_clienthost}) \\[(?:%{DATA:mysql_slow_clientip})\\]%{SPACE}Id:%{SPACE}%{DATA:mysql_slow_id}%{GREEDYDATA}Query_time: %{NUMBER:mysql_slow_querytime:float}(?:%{SPACE})Lock_time: %{NUMBER:mysql_slow_locktime:float}(?:%{SPACE})Rows_sent: %{NUMBER:mysql_slow_rowssent:int}(?:%{SPACE})Rows_examined: %{NUMBER:mysql_slow_rowsexamined:int}(?:%{SPACE})(?:%{GREEDYDATA})SET timestamp=%{NUMBER:mysql_slow_timestamp};(\\r|\\n)%{DATA:mysql_slow_query};"

Example message
---------------

    # Time: 2020-11-06T23:04:23.313878Z
    # User@Host: root[root] @ localhost [127.0.0.1]  Id:     5
    # Query_time: 7.000540  Lock_time: 0.000000 Rows_sent: 1  Rows_examined: 0
    SET timestamp=1604703863;
    select 1 as uno, 2 as due, 3 as tre, 4 as quattro, sleep(7);

Fields
------

    mysql_slow_querydate: 2020-11-07 00:04:23 +01:00
    mysql_slow_clienthost: localhost
    mysql_slow_clientip: 127.0.0.1
    mysql_slow_clientuser: root
    mysql_slow_clientdbname: root
    mysql_slow_locktime: 0
    mysql_slow_id: 5
    mysql_slow_querytime: 7.000540
    mysql_slow_rowsexamined: 0
    mysql_slow_rowssent: 1
    mysql_slow_timestamp: 1604703863
    mysql_slow_query: select 1 as uno, 2 as due, 3 as tre, 4 as quattro, sleep(7)

Input
-----

A way to grab log lines: **Graylog Collector Sidecar** with Beats (Filebeat)

[![screen2](https://images2.imgbox.com/ca/b1/MqSjIBks_o.png)](https://images2.imgbox.com/ca/b1/MqSjIBks_o.png)


Installation
------------

Go to **Graylog Web Interface** -> **System** -> **Content Packs** then select *content_pack.json* file and upload it.

[![screen1](https://i.imgbox.com/HAsDC4FR.png)](https://i.imgbox.com/wP2n4HXH.png)

Check
-----

Created and tested on
`Graylog 3.3.8+e223f85 (Oracle Corporation 1.8.0_242 on Linux 3.10.0-1062.12.1.el7.x86_64)`
