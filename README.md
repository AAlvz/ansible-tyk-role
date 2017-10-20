# Ansible Role: Tyk API Gateway

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

```yaml
tyk_gateway_port: 8080
```

The port in which Tyk's API gateway is going to be listening on. The default configuration of Tyk is the 8080 port.

```yaml
redishost: localhost
```

The host ip in which RedisDB is located. The default configuration is set to localhost.

```yaml
redisport: 6379
```

The port in which RedisDB is set to listen to request. The default configuration of RedisDB is the 6379 port.

```yaml
target_host: "127.0.0.1"
```
The ip to which tyk is going to redirect the incoming requests.



```yaml
config_file:
```

A list of  attributes to setup keyless APIs basic configuration. If left empty, you will need to supply your own APIs basic configuration.  In the following example:

```yaml
config_file:
  users_api:
    api_name: "Users API"
    listen_path: "/users"
    target_url: "http://{{ target_host }}:3000/users"
    api_id: "1"
    org_id: "1"
  .
  .
  .
  file_name:
    api_name: "Example API"
    listen_path: "/example/api/path/request"
    target_url: "http://{{ target_host }}:port/example/path"
    api_id: "UUID"
    org_id: "UUID"
```

- N number of file_name are written as the amount of APIs are going to be set up.
  - api_name:  The name of the API.
  - listen_path: The base path Tyk should listen to.
  - target_url: The url which Tyk is going to redirect to.
  - api_id: The unique ID for the API.
  - org_id: The ID linked to key generation.

## Dependencies

- RedisDB

## Example Playbook

```yaml
- hosts: server
  roles:
    - { role: tyk }
```
