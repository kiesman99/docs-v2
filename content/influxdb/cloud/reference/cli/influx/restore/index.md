---
title: influx restore
description: The `influx restore` command restores backup data and metadata from an InfluxDB backup directory.
influxdb/cloud/tags: [restore]
menu:
  influxdb_cloud_ref:
    parent: influx
weight: 101
related:
  - /influxdb/cloud/reference/cli/influx/#provide-required-authentication-credentials, influx CLI—Provide required authentication credentials
  - /influxdb/cloud/reference/cli/influx/#flag-patterns-and-conventions, influx CLI—Flag patterns and conventions
---

{{% note %}}
#### Available with InfluxDB OSS 2.x only
The `influx restore` command works with **InfluxDB OSS 2.x**, but does not work with **InfluxDB Cloud**.
For information about restoring data in InfluxDB Cloud, see
[InfluxDB Cloud durabilty](/influxdb/cloud/reference/internals/durability/) and
[contact InfluxData Support](mailto:support@influxdata.com).
{{% /note %}}

The `influx restore` command restores backup data and metadata from an InfluxDB OSS backup directory.

### The restore process
When restoring data from a backup file set, InfluxDB temporarily moves existing
data and metadata while `restore` runs.
After `restore` completes, the temporary data is deleted.
If the restore process fails, InfluxDB preserves the data in the temporary location.

_For information about recovering from a failed restore process, see
[Restore data](/influxdb/v2.0/backup-restore/restore/#recover-from-a-failed-restore)._

## Usage

```
influx restore [flags]
```

## Flags

| Flag |                   | Description                                                           | Input type | {{< cli/mapped >}}    |
|:-----|:------------------|:----------------------------------------------------------------------|:----------:|:----------------------|
| `-c` | `--active-config` | CLI configuration to use for command                                  | string     |                       |
| `-b` | `--bucket`        | Name of the bucket to restore (mutually exclusive with `--bucket-id`) | string     |                       |
|      | `--bucket-id`     | ID of the bucket to restore (mutually exclusive with `--bucket`)      | string     |                       |
|      | `--configs-path`  | Path to `influx` CLI configurations (default `~/.influxdbv2/configs`) | string     | `INFLUX_CONFIGS_PATH` |
|      | `--full`          | Fully restore and replace all data on server                          |            |                       |
| `-h` | `--help`          | Help for the `restore` command                                        |            |                       |
|      | `--hide-headers`  | Hide table headers (default `false`)                                  |            | `INFLUX_HIDE_HEADERS` |
|      | `--host`          | HTTP address of InfluxDB (default `http://localhost:8086`)            | string     | `INFLUX_HOST`         |
|      | `--json`          | Output data as JSON (default `false`)                                 |            | `INFLUX_OUTPUT_JSON`  |
|      | `--new-bucket`    | Name of the bucket to restore to                                      | string     |                       |
|      | `--new-org`       | Name of the organization to restore to                                | string     |                       |
| `-o` | `--org`           | Organization name (mutually exclusive with `--org-id`)                | string     |                       |
|      | `--org-id`        | Organization ID (mutually exclusive with `--org`)                     | string     |                       |
|      | `--skip-verify`   | Skip TLS certificate verification                                     |            | `INFLUX_SKIP_VERIFY`  |
| `-t` | `--token`         | API token                                                             | string     | `INFLUX_TOKEN`        |

## Examples

{{< cli/influx-creds-note >}}

- [Restore and replace all data](#restore-and-replace-all-data)
- [Restore backup data to an existing bucket](#restore-backup-data-to-an-existing-bucket)
- [Create a bucket and restore data to it](#create-a-bucket-and-restore-data-to-it)

##### Restore and replace all data
```sh
influx restore --full /path/to/backup/dir/
```

##### Restore backup data to an existing bucket
```sh
influx restore \
  --bucket example-bucket \
  /path/to/backup/dir/
```

##### Create a bucket and restore data to it
```sh
influx restore \
  --new-bucket new-example-bucket \
  /path/to/backup/dir/
```

