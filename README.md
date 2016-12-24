# Ansible role Kong

[![Build Status](https://travis-ci.org/VEBERArnaud/ansible-role-kong.svg?branch=master)](https://travis-ci.org/VEBERArnaud/ansible-role-kong)

Installs Kong (> v0.9.X) on Ubuntu servers.

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

```yaml
ubuntu_flavor: xenial
```

```yaml
kong_apt_dependencies:
  - netcat
  - openssl
  - libpcre3
  - dnsmasq
  - procps
  - perl
```

```yaml
kong_source_ver: 0.9.7
```
```yaml
kong_source_deb: "https://github.com/Mashape/kong/releases/download/{{ kong_source_ver }}/kong-{{ kong_source_ver }}.{{ ubuntu_flavor }}_all.deb"
```
```yaml
kong_dest_deb: /tmp/kong.deb
```

```yaml
kong_user: kong
```
```yaml
kong_group: "{{ kong_user }}"
```

```yaml
kong_conf_dest: /etc/kong/kong.conf
```

```yaml
kong_log_dir: /var/log/kong
```

### Kong General configuration

```yaml
kong_conf_general_prefix: /usr/local/kong/
```
```yaml
kong_conf_general_log_level: notice
```
```yaml
kong_conf_general_anonymous_report: on
```

### Kong Nginx configuration

```yaml
kong_conf_nginx_proxy_listen_host: 0.0.0.0
```
```yaml
kong_conf_nginx_proxy_listen_port: 8000
```
```yaml
kong_conf_nginx_proxy_listen: "{{ kong_conf_nginx_proxy_listen_host }}:{{ kong_conf_nginx_proxy_listen_port }}"
```
```yaml
kong_conf_nginx_proxy_listen_ssl_host: 0.0.0.0
```
```yaml
kong_conf_nginx_proxy_listen_ssl_port: 8443
```
```yaml
kong_conf_nginx_proxy_listen_ssl: "{{ kong_conf_nginx_proxy_listen_ssl_host }}:{{ kong_conf_nginx_proxy_listen_ssl_port }}"
```
```yaml
kong_conf_nginx_admin_listen_host: 0.0.0.0
```
```yaml
kong_conf_nginx_admin_listen_port: 8001
```
```yaml
kong_conf_nginx_admin_listen: "{{ kong_conf_nginx_admin_listen_host }}:{{ kong_conf_nginx_admin_listen_port }}"
```
```yaml
kong_conf_nginx_nginx_worker_processes: auto
```
```yaml
kong_conf_nginx_nginx_daemon: on
```
```yaml
kong_conf_nginx_mem_cache_size: 128m
```
```yaml
kong_conf_nginx_ssl: on
```
```yaml
kong_conf_nginx_ssl_cert: ""
```
```yaml
kong_conf_nginx_ssl_cert_key: ""
```

### Kong Datastore configuration

```yaml
kong_conf_datastore_database: postgres
```
```yaml
kong_conf_datastore_pg_host: 127.0.0.1
```
```yaml
kong_conf_datastore_pg_port: 5432
```
```yaml
kong_conf_datastore_pg_user: kong
```
```yaml
kong_conf_datastore_pg_password: kong
```
```yaml
kong_conf_datastore_pg_database: kong
```
```yaml
kong_conf_datastore_pg_ssl: off
```
```yaml
kong_conf_datastore_pg_ssl_verify: off
```
```yaml
kong_conf_datastore_cassandra_contact_point: 127.0.0.1
```
```yaml
kong_conf_datastore_cassandra_port: 9042
```
```yaml
kong_conf_datastore_cassandra_keyspace: kong
```
```yaml
kong_conf_datastore_cassandra_consistency: ONE
```
```yaml
kong_conf_datastore_cassandra_timeout: 5000
```
```yaml
kong_conf_datastore_cassandra_ssl: off
```
```yaml
kong_conf_datastore_cassandra_ssl_verify: off
```
```yaml
kong_conf_datastore_cassandra_username: kong
```
```yaml
kong_conf_datastore_cassandra_password: kong
```
```yaml
kong_conf_datastore_cassandra_repl_strategy: SimpleStrategy
```
```yaml
kong_conf_datastore_cassandra_repl_factor: 1
```
```yaml
kong_conf_datastore_cassandra_data_centers: dc1:2,dc2:3
```

### Kong Clustering configuration

```yaml
kong_conf_clustering_cluster_listen_ip: 0.0.0.0
```
```yaml
kong_conf_clustering_cluster_listen_port: 7946
```
```yaml
kong_conf_clustering_cluster_listen: "{{ kong_conf_clustering_cluster_listen_ip }}:{{ kong_conf_clustering_cluster_listen_port }}"
```
```yaml
kong_conf_clustering_cluster_listen_rpc_ip: 127.0.0.1
```
```yaml
kong_conf_clustering_cluster_listen_rpc_port: 7373
```
```yaml
kong_conf_clustering_cluster_listen_rpc: "{{ kong_conf_clustering_cluster_listen_rpc_ip }}:{{ kong_conf_clustering_cluster_listen_rpc_port }}"
```
```yaml
kong_conf_clustering_cluster_advertise: ""
```
```yaml
kong_conf_clustering_cluster_encrypt_key: ""
```
```yaml
kong_conf_clustering_cluster_ttl_on_failure: 3600
```
```yaml
kong_conf_clustering_cluster_profile: wan
```

### Kong DNS Resolver configuration

```yaml
kong_conf_dns_resolver_dnsmasq: on
```
```yaml
kong_conf_dns_resolver_dnsmasq_port: 8053
```
```yaml
kong_conf_dns_resolver_dns_resolver: 8.8.8.8
```

### Kong Miscellaneous configuration

```yaml
kong_conf_miscellaneous_lua_ssl_trusted_certificate: ""
```
```yaml
kong_conf_miscellaneous_lua_ssl_verify_depth: 1
```
```yaml
kong_conf_miscellaneous_lua_code_cache: on
```
```yaml
kong_conf_miscellaneous_lua_package_path: ""
```
```yaml
kong_conf_miscellaneous_lua_package_cpath: ""
```

## Dependencies

None.

## Example Playbook

```yaml
- hosts: webservers

  roles:
    - role: veberarnaud.kong
      kong_conf_datastore_database: postgres
      kong_conf_datastore_pg_host: 127.0.0.1
      kong_conf_datastore_pg_port: 5432
      kong_conf_datastore_pg_user: pg_username
      kong_conf_datastore_pg_password: pg_password
      kong_conf_datastore_pg_database: kong_db
```

## License

MIT
