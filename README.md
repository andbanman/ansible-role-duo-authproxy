# ansible-role-duo-authproxy

Downloads and installs the latest version of Duo Authentication proxy.

```
duo_authproxy_conf       # [dict] configure the proxy, keys are [key] sections
                         # and nested key/value pairs are options in the sections
duo_authproxy_version    # [string] set the proxy version
duo_authproxy_reinstall  # [bool] remove existing installation and install again
```

## Example RADIUS server and client configuration

Suppose you have an existing RADIUS server at 10.0.1.10 with clients in the subnet 10.0.2.0/24. To place Duo Authentication proxy between the existing server and client, add the proxy server as a client to the existing RADIUS and allow existing clients to authenticate to the proxy.

This Ansible variable

```yaml
duo_authproxy_conf:
  radius_client:
    host: 10.0.1.10
    secret: New-RADIUS-Secret
    pass_through_all: true
  radius_server_auto:
    ikey: iiiiiiiiiiiiiiiiiiii
    skey: ssssssssssssssssssssssssssssssssssssssss
    api_host: api-00000000.duosecurity.com
    radius_ip_1: 10.0.2.0/24
    radius_secret_1: Existing-RADIUS-Secret
    failmode: safe
    client: radius_client
    port: '1812'
```

generates this configuration

```
[radius_client]
host=10.0.1.10
secret=New-RADIUS-Secret
pass_through_all=true

[radius_server_auto]
ikey=iiiiiiiiiiiiiiiiiiii
skey=ssssssssssssssssssssssssssssssssssssssss
api_host=api-00000000.duosecurity.com
radius_ip_1=10.0.2.0/24
radius_secret_1=Existing-RADIUS-Secret
failmode=safe
client=radius_client
port=1812
```
