# Pgpool-II Exporter

Prometheus exporter for [Pgpool-II](https://pgpool.net) metrics.

Supported Pgpool-II 3.6 and later.

## Building and running

### Build
```
$ make
```

### Running

Running using an environment variable:
```
$ export DATA_SOURCE_NAME="postgresql://user:password@hostname:port/dbname?sslmode=disable"
$ ./pgpool2_exporter <flags>
```
    
To see all available configuration flags:
```
$ ./pgpool2_exporter --help
```
    
 ### Flags

* `help` 
  Show context-sensitive help (also try --help-long and --help-man).
  
* `version`
  Print version information.
  
* `web.listen-address`
  Address on which to expose metrics and web interface. (default ":9719").

* `web.telemetry-path`
  Path under which to expose metrics. (default "/metrics")
  
* `log.level`
  Set logging level: one of debug, info, warn, error.

* `log.format` 
  Set the log format: one of logfmt, json.
  
### Docker

This package is available for Docker. The following environment variables configure the docker container:

* `POSTGRES_USERNAME`
  PostgreSQL user name. Default is `postgres`.

* `POSTGRES_PASSWORD`
  PostgreSQL user password. Default is `postgres`.
  
* `PGPOOL_SERVICE`
  Pgpool-II hostname. Default is `localhost`.
  
* `PGPOOL_SERVICE_PORT`
  Pgpool-II port number. Default is `9999`.

```
docker run --name pgpool2_exporter \
  --net=host --rm \
  -e POSTGRES_USERNAME=<username> \
  -e POSTGRES_PASSWORD=<password> \
  -e PGPOOL_SERVICE=<hostname> \
  -e PGPOOL_SERVICE_PORT=<port> \
  pgpool/pgpool2_exporter:latest
```
  
### Metrics

name | Pgpool-II Version | Description
:---|:---|:---
pgpool2_frontend_total | Pgpool-II 3.6+ | Number of total child processes
pgpool2_frontend_used | Pgpool-II 3.6+ | Number of used child processes
pgpool2_pool_nodes_status | Pgpool-II 3.6+ | Backend node Status (1 for up or waiting, 0 for down or unused)
pgpool2_pool_nodes_replication_delay | Pgpool-II 3.6+ | Replication delay
pgpool2_pool_nodes_select_cnt | Pgpool-II 3.6+ | SELECT query counts issued to each backend
pgpool2_pool_cache_cache_hit_ratio | Pgpool-II 3.6+ | Query cache hit ratio
pgpool2_pool_cache_num_cache_entries | Pgpool-II 3.6+ | Number of used cache entries
pgpool2_pool_cache_num_hash_entries | Pgpool-II 3.6+ | Number of total hash entries
pgpool2_pool_cache_used_hash_entries | Pgpool-II 3.6+ | Number of used hash entries
pgpool2_pool_backend_stats_select_cnt | Pgpool-II 4.2+ | | SELECT statement counts issued to each backend
pgpool2_pool_backend_stats_insert_cnt | Pgpool-II 4.2+ | | INSERT statement counts issued to each backend
pgpool2_pool_backend_stats_update_cnt | Pgpool-II 4.2+ | | UPDATE statement counts issued to each backend
pgpool2_pool_backend_stats_delete_cnt | Pgpool-II 4.2+ | | DELETE statement counts issued to each backend
pgpool2_pool_backend_stats_ddl_cnt | Pgpool-II 4.2+ | | DDL statement counts issued to each backend
pgpool2_pool_backend_stats_other_cnt | Pgpool-II 4.2+ | | other statement counts issued to each backend
pgpool2_pool_backend_stats_panic_cnt | Pgpool-II 4.2+ | | Panic message counts returned from backend
pgpool2_pool_backend_stats_fatal_cnt | Pgpool-II 4.2+ | | Fatal message counts returned from backend
pgpool2_pool_backend_stats_error_cnt | Pgpool-II 4.2+ | | Error message counts returned from backend
pgpool2_pool_health_check_stats_total_count | Pgpool-II 4.2+ | | Number of health check count in total
pgpool2_pool_health_check_stats_success_count | Pgpool-II 4.2 + | | Number of successful health check count in total
pgpool2_pool_health_check_stats_fail_count | Pgpool-II 4.2+ | | Number of failed health check count in total
pgpool2_pool_health_check_stats_skip_count | Pgpool-II 4.2+ | | Number of skipped health check count in total
pgpool2_pool_health_check_stats_retry_count | Pgpool-II 4.2+ | | Number of retried health check count in total
pgpool2_pool_health_check_stats_average_retry_count | Pgpool-II 4.2+ | | Number of average retried health check count in a health check session
pgpool2_pool_health_check_stats_max_retry_count | Pgpool-II 4.2+ | | Number of maximum retried health check count in a health check session
pgpool2_pool_health_check_stats_max_duration | Pgpool-II 4.2+ | | Maximum health check duration in Millie seconds
pgpool2_pool_health_check_stats_min_duration | Pgpool-II 4.2+ | | Minimum health check duration in Millie seconds
pgpool2_pool_health_check_stats_average_duration | Pgpool-II 4.2+ | | Average health check duration in Millie seconds
