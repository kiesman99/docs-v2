---
title: influx - InfluxDB command line interface
seotitle: influx - InfluxDB command line interface
description: >
  The `influx` CLI includes commands to manage many aspects of InfluxDB,
  including buckets, organizations, users, tasks, etc.
menu:
  influxdb_cloud_ref:
    name: influx
    parent: Command line tools
weight: 101
influxdb/cloud/tags: [cli]
---

The `influx` command line interface (CLI) includes commands to manage many aspects of InfluxDB,
including buckets, organizations, users, tasks, etc.

For information about setting up and configuring the `influx` CLI, see [Download, install, and use the influx CLI](/influxdb/cloud/sign-up/#optional-download-install-and-use-the-influx-cli).

## Usage

```
influx [flags]
influx [command]
```

### Provide required authentication credentials
To avoid having to pass your InfluxDB **host**, **API token**, and **organization**
with each command, store them in an `influx` CLI configuration (config).
`influx` commands that require these credentials automatically retrieve these
credentials from the active config.

Use the [`influx config create` command](/influxdb/cloud/reference/cli/influx/config/create/)
to create an `influx` CLI config and set it as active:

```sh
influx config create --config-name <config-name> \
  --host-url http://localhost:8086 \
  --org <your-org> \
  --token <your-api-token> \
  --active
```

For more information about managing CLI configurations, see the
[`influx config` documentation](/influxdb/cloud/reference/cli/influx/config/).

## Commands

| Command                                                      | Description                                          |
|:-------                                                      |:-----------                                          |
| [apply](/influxdb/cloud/reference/cli/influx/apply)           | Apply an InfluxDB template                           |
| [auth](/influxdb/cloud/reference/cli/influx/auth)             | API token management commands             |
| [backup](/influxdb/cloud/reference/cli/influx/backup)         | Back up data                                         |
| [bucket](/influxdb/cloud/reference/cli/influx/bucket)         | Bucket management commands                           |
| [completion](/influxdb/cloud/reference/cli/influx/completion) | Generate completion scripts                          |
| [config](/influxdb/cloud/reference/cli/influx/config)         | Configuration management commands                    |
| [dashboards](/influxdb/cloud/reference/cli/influx/dashboards) | List dashboards                                      |
| [delete](/influxdb/cloud/reference/cli/influx/delete)         | Delete points from InfluxDB                          |
| [export](/influxdb/cloud/reference/cli/influx/export)         | Export resources as a template                       |
| [help](/influxdb/cloud/reference/cli/influx/help)             | Help about any command                               |
| [org](/influxdb/cloud/reference/cli/influx/org)               | Organization management commands                     |
| [ping](/influxdb/cloud/reference/cli/influx/ping)             | Check the InfluxDB `/health` endpoint                |
| [query](/influxdb/cloud/reference/cli/influx/query)           | Execute a Flux query                                 |
| [secret](/influxdb/cloud/reference/cli/influx/secret)         | Manage secrets                                       |
| [setup](/influxdb/cloud/reference/cli/influx/setup)           | Create default username, password, org, bucket, etc. |
| [stacks](/influxdb/cloud/reference/cli/influx/stacks)         | Manage InfluxDB stacks                               |
| [task](/influxdb/cloud/reference/cli/influx/task)             | Task management commands                             |
| [telegrafs](/influxdb/cloud/reference/cli/influx/telegrafs)   | Telegraf configuration management commands           |
| [template](/influxdb/cloud/reference/cli/influx/template)     | Summarize and validate an InfluxDB template          |
| [user](/influxdb/cloud/reference/cli/influx/user)             | User management commands                             |
| [v1](/influxdb/cloud/reference/cli/influx/v1)                 | Work with the v1 compatibility API                   |
| [version](/influxdb/cloud/reference/cli/influx/version)       | Print the influx CLI version                         |
| [write](/influxdb/cloud/reference/cli/influx/write)           | Write points to InfluxDB                             |

## Flags

| Flag |                | Description                                 |
|:---- |:---            |:-----------                                 |
| `-h` | `--help`       | Help for the `influx` command               |
|      | `--http-debug` | Inspect communication with InfluxDB servers |

### Flag patterns and conventions
The `influx` CLI uses the following patterns and conventions:

- [Mapped environment variables](#mapped-environment-variables)
- [Shorthand and longhand flags](#shorthand-and-longhand-flags)
- [Flag input types](#flag-input-types)

#### Mapped environment variables
`influx` CLI flags mapped to environment variables are listed in the **Mapped to** column.
Mapped flags inherit the value of the environment variable.
To override environment variables, set the flag explicitly in your command.

#### Shorthand and longhand flags
Many `influx` CLI flags support both shorthand and longhand forms.

- **shorthand:** a shorthand flag begins with a single hyphen followed by a single letter (for example: `-c`).
- **longhand:** a longhand flag starts with two hyphens followed by a multi-letter,
  hyphen-spaced flag name (for example: `--active-config`).

Commands can use both shorthand and longhand flags in a single execution.

#### Flag input types
`influx` CLI flag input types are listed in each the table of flags for each command.
Flags support the following input types:

##### string
Text string, but the flag can be used **only once** per command execution.

##### stringArray
Single text string, but the flag can be used **multiple times** per command execution.

##### integer
Sequence of digits representing an integer value.

##### duration
Length of time represented by an integer and a duration unit
(`1ns`, `1us`, `1µs`, `1ms`, `1s`, `1m`, `1h`, `1d`, `1w`).
