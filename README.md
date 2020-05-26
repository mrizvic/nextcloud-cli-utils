# NEXTCLOUD CLI UTILS

## IDEA
Utilities are created during administration of several nextcloud instances.

## REQUIREMENTS
mysql-client, jq, curl

## INSTALLATION
One might need to adjust paths inside scripts for example edit `showconf` and change location of `/var/www/nextcloud/config/config.php` to suit your installation.

Create entry in `~/.my.cnf` file to describing connection to nextcloud mysql server:
```
$ cat <<EOF > ~/.my.cnf
[mysql]
user=ncDBuser
password=yourNCdbPassword
database=ncDBname
host=localhost
prompt="(\d)\u# "
EOF
```

Specify nextcloud database name in `~/.nextclouddb`
```
$ echo "ncDBname" > ~/.nextclouddb
```

Test if connectiont to database works:
```
$ mysql
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 2254
Server version: 10.3.17-MariaDB-log MariaDB Server

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

(ncDBname)root# STATUS
--------------
mysql  Ver 15.1 Distrib 10.3.17-MariaDB, for Linux (x86_64) using readline 5.1

Connection id:          2254
Current database:       ncDBname
Current user:           ncDBuser@localhost
SSL:                    Not in use
Current pager:          stdout
Using outfile:          ''
Using delimiter:        ;
Server:                 MariaDB
Server version:         10.3.17-MariaDB-log MariaDB Server
Protocol version:       10
Connection:             Localhost via UNIX socket
Server characterset:    utf8mb4
Db     characterset:    utf8mb4
Client characterset:    utf8mb4
Conn.  characterset:    utf8mb4
UNIX socket:            /var/lib/mysql/mysql.sock
Uptime:                 2 hours 47 min 28 sec

Threads: 17  Questions: 111922  Slow queries: 0  Opens: 104  Flush tables: 1  Open tables: 98  Queries per second avg: 11.138
--------------

(ncDBname)root# SHOW TABLES;
+-----------------------------+
| Tables_in_ncDBname          |
+-----------------------------+
| oc_accounts                 |
| oc_activity                 |
| oc_activity_mq              |
| oc_addressbookchanges       |
--snip--
| oc_vcategory                |
| oc_vcategory_to_object      |
| oc_whats_new                |
+-----------------------------+
85 rows in set (0.001 sec)
```

Copy scripts to `~/bin` or `/usr/local/bin` or similar location.

## USAGE
Start by running `nc_help` and then suit yourself :)

```
$ ./nc_help
Nextcloud scripts located in /opt/scripts:
------------------------------------------------------------------------------------------
clearbruteforces         "Clear entry from oc_bruteforce_attempts table"
cloudsend.sh             "Uses curl to send files to a shared Nextcloud/Owncloud folder"
editconf                 "edit nextcloud config.php"
ncc                      "nextcloud cli command (occ)"
showaudit                "Parse and list nextcloud audit.log entries"
showbruteforces          "Show oc_bruteforce_attempts table"
showconf                 "Show nextcloud config.php"
showfailedlogin          "Show failed logins from nextcloud.log"
showlog                  "Parse and list nextcloud.log entries"
showslowlog              "Show mysql slow.log entries"
showtagslike             "Show tagged files"
showusage                "Show disk usage on nextcloud/data directory"
------------------------------------------------------------------------------------------
```
## Disclaimer
Use at your own risk. I cannot be held responsible for any misinterpretation of output presented to anyone using code from this repository.

## Coffee
If you find this useful you can buy me a coffee :) https://ko-fi.com/markor


