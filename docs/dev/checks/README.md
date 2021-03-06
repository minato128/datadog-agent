# Developer Guide for Checks

This section of the docs will help you understanding how checks work and how to
provide custom or new ones.

Existing checks live in the [integrations-core](https://github.com/DataDog/integrations-core) and [integrations-extras](https://github.com/DataDog/integrations-extras) repositories.

## Configuration

Every check has its own YAML configuration file. The file has one mandatory key,
`instances` and one optional, `init_config`.

### init_config

This section contains any global configuration options for the check, i.e. any
configuration that all instances of the check can share. Python checks can access
these configuration options via the `self.init_config` dictionary.

There is no required format for the items in `init_config`, but most checks just
use simple key-value configuration, e.g.

Example:
```yaml
init_config:
  default_timeout: 4
  idle_ttl: 300
```

### instances

This section is a list, with each item representing one "instance" — i.e. one
running invocation of the check. For example, when using the HTTP check, you
can configure multiple instances in order to monitor multiple HTTP endpoints:

```yaml
instances:
  - server_url: https://backend1
    user: user1
    password: password
    interval: 60
  - server_url: https://backend2
    token: <SOME_AUTH_TOKEN>
    timeout: 20
```

Each instance, like the `init_config` section, may contain data in any format.
It's up to the check author how to structure configuration data.

Each instances of a check are completely independent from one another and might
run at different intervals.

## Python Checks

### API

Read more about the [Python Checks API](python/check_api.md).

### Built-in packages

The Agent provides a set of python packages that are built-in and only available
within the embedded CPython interpreter:

- [aggregator](python/aggregator.md)
- [datadog-agent](python/datadog_agent.md)


## Core Checks (or Go Checks)

TODO
