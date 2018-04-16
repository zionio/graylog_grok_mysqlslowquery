[![license](https://img.shields.io/github/license/mashape/apistatus.svg?maxAge=2592000)](https://opensource.org/licenses/MIT)


MySQL Slow Query Log GROK pattern for Graylog
=============================================

Pattern
-------

    "name":"MYSQLSLOWQUERYLOG",
    "pattern":"(?s) User@Host: (?:%{USERNAME:mysql_slow_clientuser})(?:%{GREEDYDATA}) @ (?:%{DATA:mysql_slow_clienthost}) \\[(?:%{DATA:mysql_slow_clientip}\\])%{SPACE}Id:%{SPACE}%{DATA:mysql_slow_id}(\\r|\\n)%{GREEDYDATA}Query_time: %{NUMBER:mysql_slow_querytime:float}(?:%{SPACE})Lock_time: %{NUMBER:mysql_slow_locktime:float}(?:%{SPACE})Rows_sent: %{NUMBER:mysql_slow_rowssent:int}(?:%{SPACE})Rows_examined: %{NUMBER:mysql_slow_rowsexamined:int}(?:%{SPACE})(?:%{GREEDYDATA})SET timestamp=%{NUMBER:mysql_slow_timestamp}\\;"

Example message
---------------

    # Time: 2016-10-05T12:14:29.634170+01:00
    # User@Host: user1[user1] @ localhost [127.0.0.1]  Id: 222521
    # Query_time: 12.000243  Lock_time: 0.000000 Rows_sent: 1  Rows_examined: 0
    SET timestamp=1475662469;
    select sleep(12);

Fields
------

    mysql_slow_clienthost: localhost
    mysql_slow_clientip: 127.0.0.1
    mysql_slow_clientuser: user1
    mysql_slow_locktime: 0.000000
    mysql_slow_id: 222521
    mysql_slow_querytime: 12.000243
    mysql_slow_rowsexamined: 0
    mysql_slow_rowssent: 1
    mysql_slow_timestamp: 1475662469

Input
-----

    A way to grab log lines: **Graylog Collector Sidecar** with Beats (Filebeat)

    [![screen2](http://imgbox.com/MqSjIBks)](https://images2.imgbox.com/ca/b1/MqSjIBks_o.png)


Installation
------------

Go to **Graylog Web Interface** -> **System** -> **Content Packs** then select *content_pack.json* file and upload it.

[![screen1](https://i.imgbox.com/HAsDC4FR.png)](https://i.imgbox.com/wP2n4HXH.png)