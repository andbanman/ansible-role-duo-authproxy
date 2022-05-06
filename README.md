# ansible-role-duo-authproxy

Downloads and installs the latest version of Duo Authentication proxy.

```
duo_authproxy_conf       # [dict] configure the proxy, keys are [key] sections
                         # and nested key/value pairs are options in the secions
duo_authproxy_version    # [string] set the proxy version
duo_authproxy_reinstall  # [bool] remove existing installation and install again
```
