---
title: DM-worker Configuration File
summary: Learn the configuration file of DM-worker.
category: reference
---

# DM-worker Configuration File

This document introduces the basic configuration of DM worker, which provision DM-worker's deployment in most scenarios. Refer to [DM-worker Advanced Configuration File](/reference/tools/data-migration/configure/dm-worker-configuration-file-full.md) to see more parameters in detail.

## Configuration file template

```toml
# Worker Configuration.

# Log configuration.
log-file = "dm-worker.log"

# DM-worker listen address.
worker-addr = ":8262"

# Represents a MySQL/MariaDB instance or a replication group.
source-id = "mysql-replica-01"

# Server id of slave for binlog replication.
# Each instance (master and slave) in replication group should have different server id.
server-id = 101

# flavor: mysql/mariadb
flavor = "mysql"

# The directory that used to store relay log.
relay-dir = "./relay_log"

[from]
host = "127.0.0.1"
user = "root"
password = "Up8156jArvIPymkVC+5LxkAT6rek"
port = 3306
```

## Configuration parameters

### Global

| Parameter        | Description                           | Default value |
| :------------ | :--------------------------------------- | :---------|
| `log-file` | Specifies the log file directory. If not specified, the logs are printed onto the standard output. |
| `worker-addr` | Specifies the address of DM-worker which provides services. You can omit the IP address and specify the port number only, such as ":8262".| |
| `source-id` | Uniquely identifies a MySQL or MariaDB instance, or a replication group | |
| `server-id` | Identifies the server ID of MySQL slave, used when pulling binlogs from MySQL. In a replication group, each instance (master and slave included) must have a unique server ID. In v1.0.2 and later versions, the `server_id` is automatically generated by DM. | |
| `flavor` | Indicates the release type of MySQL: `"Percona"`, `"mysql"` or `"mariadb"`. In v1.0.2 and later versions, DM automatically detects and fills in the release type. | `"mysql"`|
| `relay-dir` | Specifies the relay log directory. | `"./relay_log"` |

### `[from]`

The `[from]` section contains parameters that affect the connection to the upstream database.

| Parameter        | Description                           |
| :------------ | :--------------------------------------- |
| `host` | The host name of the upstream database. |
| `port` | The port number of the upstream database. |
| `user` | The username used to connect to the database. |
| `password` | The password used to connect to the database. Note: Use the password encrypted by dmctl.