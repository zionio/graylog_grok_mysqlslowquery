[![license](https://img.shields.io/github/license/mashape/apistatus.svg?maxAge=2592000)](https://opensource.org/licenses/MIT)


# MySQL Slow Query LOG GROK pattern for Graylog

**Pattern:**

      "name":"MYSQLSLOWQUERYLOG",
      "pattern":"(?s) User@Host: (?:%{USERNAME:mysql_clientuser})(?:%{GREEDYDATA}) @ (?:%{DATA:mysql_clienthost}) \\[(?:%{DATA:mysql_clientip}\\]) %{GREEDYDATA} Query_time: %{NUMBER:mysql_querytime:float}(?:%{SPACE})Lock_time: %{NUMBER:mysql_locktime:float}(?:%{SPACE})Rows_sent: %{NUMBER:mysql_rowssent:int}(?:%{SPACE})Rows_examined: %{NUMBER:mysql_rowsexamined:int}(?:%{SPACE})(?:%{GREEDYDATA})SET timestamp=%{NUMBER:mysql_timestamp}\\;"

i.e.:

**message**

    # Time: 2016-10-05T12:14:29.634170+01:00
    # User@Host: user1[user1] @ localhost [127.0.0.1]  Id: 222521
    # Query_time: 12.000243  Lock_time: 0.000000 Rows_sent: 1  Rows_examined: 0
    SET timestamp=1475662469;
    select sleep(12);

**fields**

    mysql_clienthost: localhost
    mysql_clientip: 127.0.0.1
    mysql_clientuser: user1
    mysql_locktime: 0.000000
    mysql_querytime: 12.000243
    mysql_rowsexamined: 0
    mysql_rowssent: 1
    mysql_timestamp: 1475662469

