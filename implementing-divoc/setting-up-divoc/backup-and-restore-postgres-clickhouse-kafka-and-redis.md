# Backup & Restore: Postgres, Clickhouse, Kafka, & Redis

## Overview

This is the generic solution for backup and restore. Depending on the backup strategy used, the tools might change.

## Backing up and restoring Postgres&#x20;

* The Ansible script will automatically configure pg\_basebackup, pgbackrest, wal-g and other recovery tools. For the sake of simplicity, we can use pg\_dump and pg\_restore.
* The following command takes a backup. This will create a compressed tarball backup in the directory mentioned:

{% hint style="info" %}
pg\_dump -h 192.168.0.100 -U postgres -F c remote\_db1 > remote\_db1.tar
{% endhint %}

* This can be scheduled using a cron as shown below:

{% hint style="info" %}
0 0 \* \* \* \<path to backup script>
{% endhint %}

* Pg\_basebackup is installed along with psql client

{% hint style="info" %}
sudo apt install postgresql-client
{% endhint %}

* You can restore from pg\_dump as follows:

{% hint style="info" %}
pg\_restore -h 192.168.0.100 -U postgres -F -C -d db1 < db1.tar
{% endhint %}

## Backing up and restoring Clickhouse

The plan is to use [clickhouse-backup](https://github.com/AlexAkulov/clickhouse-backup), which is open sourced under the liberal MIT license. This tool has the ability to create archived backups and upload them to NFS, S3, GCS, AZBlob, SFTP and other remote data repositories.

* Download the latest release from [https://github.com/AlexAkulov/clickhouse-backup/releases](https://github.com/AlexAkulov/clickhouse-backup/releases)
* Untar the archive

{% hint style="info" %}
tar -zxvf clickhouse-backup.tar.gz
{% endhint %}

* Create a configuration file as follows, call it config.ini

{% hint style="info" %}
general:\
&#x20; remote\_storage: none                   # REMOTE\_STORAGE, if \`none\` then \`upload\` and  \`download\` command will fail\
&#x20; max\_file\_size: 1073741824            # MAX\_FILE\_SIZE, 1G by default, useless when upload\_by\_part is true, use for split data parts files by archives \
&#x20; disable\_progress\_bar: true            # DISABLE\_PROGRESS\_BAR, show progress bar during upload and download, have sense only when \`upload\_concurrency\` and \`download\_concurrency\` equal 1\
&#x20; backups\_to\_keep\_local: 0              # BACKUPS\_TO\_KEEP\_LOCAL, how much newest local backup should keep, 0 mean all created backups will keep on local disk\
&#x20;                                                          \# you shall to run \`clickhouse-backup delete local \<backup\_name>\` command to avoid useless disk space allocations\
&#x20; backups\_to\_keep\_remote: 0          # BACKUPS\_TO\_KEEP\_REMOTE, how much newest backup should keep on remote storage, 0 mean all uploaded backups will keep on remote storage.\
&#x20;                                                          \# if old backup is required for newer incremental backup, then it will don't delete. Be careful with long incremental backup sequences.

log\_level: info                                     # LOG\_LEVEL\
&#x20; allow\_empty\_backups: false           # ALLOW\_EMPTY\_BACKUPS\
&#x20; download\_concurrency: 1               # DOWNLOAD\_CONCURRENCY, max 255\
&#x20; upload\_concurrency: 1                    # UPLOAD\_CONCURRENCY, max 255\
&#x20; restore\_schema\_on\_cluster: ""        # RESTORE\_SCHEMA\_ON\_CLUSTER, execute all schema related SQL queryes with \`ON CLUSTER\` clause as Distributed DDL, look to \`system.clusters\` table for proper cluster name\
&#x20; upload\_by\_part: true                        # UPLOAD\_BY\_PART\
&#x20; download\_by\_part: true                   # DOWNLOAD\_BY\_PART\
clickhouse:\
&#x20; username: default                            # CLICKHOUSE\_USERNAME\
&#x20; password: ""                                     # CLICKHOUSE\_PASSWORD\
&#x20; host: localhost                                 # CLICKHOUSE\_HOST\
&#x20; port: 9000                                        # CLICKHOUSE\_PORT, don't use 8123, clickhouse-backup doesn't support HTTP protocol\
&#x20; disk\_mapping: {}                              # CLICKHOUSE\_DISK\_MAPPING, use it if your system.disks on restored servers not the same with system.disks on server where backup was created\
&#x20; skip\_tables:                                     # CLICKHOUSE\_SKIP\_TABLES\
&#x20;   \- system.\*\
&#x20;   \- INFORMATION\_SCHEMA.\*\
&#x20;   \- information\_schema.\*\
&#x20; timeout: 5m                                    # CLICKHOUSE\_TIMEOUT\
&#x20; freeze\_by\_part: false                     # CLICKHOUSE\_FREEZE\_BY\_PART\
&#x20; secure: false                                   # CLICKHOUSE\_SECURE, use SSL encryption for&#x20;

connect

skip\_verify: false                               # CLICKHOUSE\_SKIP\_VERIFY\
&#x20; sync\_replicated\_tables: true         # CLICKHOUSE\_SYNC\_REPLICATED\_TABLES\
&#x20; log\_sql\_queries: true                      # CLICKHOUSE\_LOG\_SQL\_QUERIES, enable log clickhouse-backup SQL queries on \`system.query\_log\` table inside clickhouse-server\
&#x20; debug: false                                    # CLICKHOUSE\_DEBUG\
&#x20; config\_dir:      "/etc/clickhouse-server"              # CLICKHOUSE\_CONFIG\_DIR\
&#x20; restart\_command: "systemctl restart clickhouse-server" # CLICKHOUSE\_RESTART\_COMMAND, this command use when you try to restore with --rbac or --config options\
&#x20; ignore\_not\_exists\_error\_during\_freeze: true # CLICKHOUSE\_IGNORE\_NOT\_EXISTS\_ERROR\_DURING\_FREEZE, allow avoiding backup failures when you often CREATE / DROP tables and databases during backup creation, clickhouse-backup will ignore \`code: 60\` and \`code: 81\` errors during execute \`ALTER TABLE ... FREEZE\`\
azblob:\
&#x20; endpoint\_suffix: "core.windows.net" # AZBLOB\_ENDPOINT\_SUFFIX\
&#x20; account\_name: ""                                # AZBLOB\_ACCOUNT\_NAME\
&#x20; account\_key: ""                                   # AZBLOB\_ACCOUNT\_KEY\
&#x20; sas: ""                                         # AZBLOB\_SAS\
&#x20; use\_managed\_identity: false    # AZBLOB\_USE\_MANAGED\_IDENTITY\
&#x20; container: ""                               # AZBLOB\_CONTAINER\
&#x20; path: ""                                       # AZBLOB\_PATH\
&#x20; compression\_level: 1                 # AZBLOB\_COMPRESSION\_LEVEL\
&#x20; compression\_format: tar           # AZBLOB\_COMPRESSION\_FORMAT\
&#x20; sse\_key: ""                                 # AZBLOB\_SSE\_KEY\
&#x20; buffer\_size: 0                             # AZBLOB\_BUFFER\_SIZE, if less or eq 0 then calculated as max\_file\_size / 10000, between 2Mb and 4Mb\
&#x20; max\_buffers: 3                           # AZBLOB\_MAX\_BUFFERS\
s3:\
&#x20; access\_key: ""                               # S3\_ACCESS\_KEY\
&#x20; secret\_key: ""                                # S3\_SECRET\_KEY\
&#x20; bucket: ""                                      # S3\_BUCKET\
&#x20; endpoint: ""                                   # S3\_ENDPOINT\
&#x20; region: us-east-1                          # S3\_REGION\
&#x20; acl: private                                    # S3\_ACL\
&#x20; assume\_role\_arn: ""                      # S3\_ASSUME\_ROLE\_ARN\
&#x20; force\_path\_style: false                 # S3\_FORCE\_PATH\_STYLE\
&#x20; path: ""                                          # S3\_PATH\
&#x20; disable\_ssl: false                           # S3\_DISABLE\_SSL\
&#x20; compression\_level: 1                     # S3\_COMPRESSION\_LEVEL\
&#x20; compression\_format: tar              # S3\_COMPRESSION\_FORMAT\
&#x20; sse: ""                                            # S3\_SSE, empty (default), AES256, or aws:kms\
&#x20; disable\_cert\_verification: false  . # S3\_DISABLE\_CERT\_VERIFICATION\
&#x20; storage\_class: STANDARD           # S3\_STORAGE\_CLASS\
&#x20; concurrency: 1                              # S3\_CONCURRENCY\
&#x20; part\_size: 0                                   # S3\_PART\_SIZE, if less or eq 0 then calculated as max\_file\_size / 10000\
&#x20; debug: false                                 # S3\_DEBUG\
gcs:\
&#x20; credentials\_file: ""                       # GCS\_CREDENTIALS\_FILE\
&#x20; credentials\_json: ""                     # GCS\_CREDENTIALS\_JSON\
&#x20; bucket: ""                                     # GCS\_BUCKET\
&#x20; path: ""                                         # GCS\_PATH\
&#x20; compression\_level: 1                   # GCS\_COMPRESSION\_LEVEL\
&#x20; compression\_format: tar            # GCS\_COMPRESSION\_FORMAT\
&#x20; debug: false                                # GCS\_DEBUG\
cos:\
&#x20; url: ""                                           # COS\_URL\
&#x20; timeout: 2m                                # COS\_TIMEOUT\
&#x20; secret\_id: ""                                # COS\_SECRET\_ID\
&#x20; secret\_key: ""                             # COS\_SECRET\_KEY\
&#x20; path: ""                                       # COS\_PATH\
&#x20; compression\_format: tar          # COS\_COMPRESSION\_FORMAT\
&#x20; compression\_level: 1                # COS\_COMPRESSION\_LEVEL\
ftp:\
&#x20; address: ""                                # FTP\_ADDRESS\
&#x20; timeout: 2m                              # FTP\_TIMEOUT\
&#x20; username: ""                            # FTP\_USERNAME\
&#x20; password: ""                            # FTP\_PASSWORD\
&#x20; tls: false                                   # FTP\_TLS\
&#x20; path: ""                                     # FTP\_PATH\
&#x20; compression\_format: tar         # FTP\_COMPRESSION\_FORMAT\
&#x20; compression\_level: 1               # FTP\_COMPRESSION\_LEVEL\
&#x20; debug: false                             # FTP\_DEBUG\
sftp:\
&#x20; address: ""                               # SFTP\_ADDRESS\
&#x20; username: ""                            # SFTP\_USERNAME\
&#x20; password: ""                            # SFTP\_PASSWORD\
&#x20; key: ""                                       # SFTP\_KEY\
&#x20; path: ""                                     # SFTP\_PATH\
&#x20; concurrency: 1                         # SFTP\_CONCURRENCY    \
&#x20; compression\_format: tar         # SFTP\_COMPRESSION\_FORMAT\
&#x20; compression\_level: 1               # SFTP\_COMPRESSION\_LEVEL\
&#x20; debug: false                             # SFTP\_DEBUG\
api:\
&#x20; listen: "localhost:7171"            # API\_LISTEN\
&#x20; enable\_metrics: true               # API\_ENABLE\_METRICS\
&#x20; enable\_pprof: false                 # API\_ENABLE\_PPROF\
&#x20; username: ""                            # API\_USERNAME, basic authorization for API endpoint\
&#x20; password: ""                            # API\_PASSWORD\
&#x20; secure: false                            # API\_SECURE, use TLS for listen API socket\
&#x20; certificate\_file: ""                     # API\_CERTIFICATE\_FILE\
&#x20; private\_key\_file: ""                    # API\_PRIVATE\_KEY\_FILE\
&#x20; create\_integration\_tables: false # API\_CREATE\_INTEGRATION\_TABLES\
&#x20; allow\_parallel: false                  # API\_ALLOW\_PARALLEL, could allocate much memory and spawn go-routines, don't enable it if you not sure
{% endhint %}

* Ensure configuration under clickhouse and general section of the configuration file. The rest are not mandatory.&#x20;
* If automated remote upload functionality is needed, the appropriate section needs to be filled in: sftp, ftp, s3, GCS, AZBlob, etc.&#x20;
* The following command can be run:

{% hint style="info" %}
sh \<path-to-cllickhouse-backup-dir>/bin/clickhouse-backup create -C \<path to config.ini>
{% endhint %}

* The following is the list of possible commands which can be executed:

{% hint style="info" %}
COMMANDS:\
&#x20;tables          Print list of tables\
&#x20;create          Create new backup\
&#x20;create\_remote   Create and upload\
&#x20;upload          Upload backup to remote storage\
&#x20;list            Print list of backups\
&#x20;download        Download backup from remote storage\
&#x20;restore         Create schema and restore data from backup\
&#x20;restore\_remote  Download and restore\
&#x20;delete          Delete specific backup\
&#x20;default-config  Print default config\
&#x20;print-config    Print current config\
&#x20;clean           Remove data in 'shadow' folder from all \`path\` folders available from \`system.disks\`\
&#x20;server          Run API server\
&#x20;help, h         Shows a list of commands or help for one command
{% endhint %}

## Backing up and restoring Kafka

* Backup zookeeper state data

&#x20;     \- Go to file&#x20;

{% hint style="info" %}
kafka/config/zookeeper.properties&#x20;
{% endhint %}

&#x20;     \- Copy location of dataDir property (typically, /tmp/zookeeper)&#x20;

&#x20;     \- Run the following command:

{% hint style="info" %}
tar -czf /home/kafka/zookeeper-backup.tar.gz /tmp/zookeeper/\*
{% endhint %}

* Backup Kafka topics and messages

&#x20;     \- Go to the file kafka/config/server.properties

&#x20;     \- Copy location of log.dirs (typically, /tmp/kafka-logs)

&#x20;     \- Stop Kafka:&#x20;

{% hint style="info" %}
sudo systemctl stop kafka
{% endhint %}

&#x20;     \- Login as kafka user:&#x20;

{% hint style="info" %}
sudo -iu kafka
{% endhint %}

&#x20;     \- Run the following command:

{% hint style="info" %}
tar -czf /home/kafka/kafka-backup.tar.gz /tmp/kafka-logs/\*
{% endhint %}

* Restore zookeeper

&#x20;     \- sudo systemctl stop kafka&#x20;

&#x20;     \- sudo systemctl stop zookeeper&#x20;

&#x20;     \- sudo -iu kafka&#x20;

&#x20;     \- rm -r /tmp/zookeeper/\*&#x20;

&#x20;     \- tar -C /tmp/zookeeper -xzf /home/kafka/zookeeper-backup.tar.gz &#x20;

&#x20;       \--strip-components 2

* Restore kafka

&#x20;     \- rm -r /tmp/kafka-logs/\*&#x20;

&#x20;     \- tar -C /tmp/kafka-logs -xzf /home/kafka/kafka-backup.tar.gz --strip-components 2&#x20;

&#x20;     \- sudo systemctl start kafka&#x20;

&#x20;     \- sudo systemctl start zookeeper

* Verification of Restoration

&#x20;     \- \~/kafka/bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic

&#x20;        BackupTopic --from-beginning

## Backing up and restoring Redis&#x20;

Redis provides an in-built command to save a backup.

* Install redis-cli using

{% hint style="info" %}
sudo apt install redis-cli
{% endhint %}

* The following command takes a backup of the redis-server:

{% hint style="info" %}
echo save | redis-cli -u redis://\<user>:\<pass>@\<host>:\<port> >> /tmp/redis-backup.log
{% endhint %}

* This will save the backup as dump.rdb within:

{% hint style="info" %}
/var/lib/redis
{% endhint %}

Restoration can be done in the following way:

* Locate the redis data directory, typically:

{% hint style="info" %}
/var/lib/redis
{% endhint %}

* Move the dump.rdb file into this folder&#x20;
* Start redis server
* This will ensure that data is restored automatically

__

_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
