# Ansible role Kong

[![Build Status](https://travis-ci.org/VEBERArnaud/ansible-role-kong.svg?branch=master)](https://travis-ci.org/VEBERArnaud/ansible-role-kong)

Installs Kong (> v0.9.X) on Ubuntu servers.

## Requirements

`None`.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

```yaml
ubuntu_flavor: xenial

kong_apt_dependencies:
  - netcat
  - openssl
  - libpcre3
  - dnsmasq
  - procps
  - perl

kong_source_ver: 0.9.7
kong_source_deb: "https://github.com/Mashape/kong/releases/download/{{ kong_source_ver }}/kong-{{ kong_source_ver }}.{{ ubuntu_flavor }}_all.deb"
kong_dest_deb: /tmp/kong.deb
kong_user: kong
kong_group: "{{ kong_user }}"
kong_conf_dest: /etc/kong/kong.conf
kong_log_dir: /var/log/kong
```

##### Kong `General` configuration

```yaml
kong_conf_general_prefix:   /usr/local/kong/
kong_conf_general_log_level: notice
kong_conf_general_anonymous_report: "on"

# kong_daemon_manager: [binary|supervisor]
#  binary: use the kong binary directly
#  supervisor: use supervisorctl module
kong_daemon_manager: "binary"

# Ensure kong is started
kong_service_start: false
# Allow kong restart/reload
kong_service_restart: false

# If you use kong with supervisord, provide the application name declared
kong_supervisor_app_name: kong
```

##### Kong `Nginx` configuration

```yaml
kong_conf_nginx_proxy_listen_host: 0.0.0.0
kong_conf_nginx_proxy_listen_port: 8000
kong_conf_nginx_proxy_listen: "{{ kong_conf_nginx_proxy_listen_host }}:{{ kong_conf_nginx_proxy_listen_port }}"
kong_conf_nginx_proxy_listen_ssl_host: 0.0.0.0
kong_conf_nginx_proxy_listen_ssl_port: 8443
kong_conf_nginx_proxy_listen_ssl: "{{ kong_conf_nginx_proxy_listen_ssl_host }}:{{ kong_conf_nginx_proxy_listen_ssl_port }}"
kong_conf_nginx_admin_listen_host: 0.0.0.0
kong_conf_nginx_admin_listen_port: 8001
kong_conf_nginx_admin_listen: "{{ kong_conf_nginx_admin_listen_host }}:{{ kong_conf_nginx_admin_listen_port }}"
kong_conf_nginx_nginx_worker_processes: auto
kong_conf_nginx_nginx_daemon: "on"
kong_conf_nginx_mem_cache_size: 128m
kong_conf_nginx_ssl: "on"
kong_conf_nginx_ssl_cert: ""
kong_conf_nginx_ssl_cert_key: ""
```

##### Kong `Datastore` configuration

```yaml
kong_conf_datastore_database: postgres
kong_conf_datastore_pg_host: 127.0.0.1
kong_conf_datastore_pg_port: 5432
kong_conf_datastore_pg_user: kong
kong_conf_datastore_pg_password: kong
kong_conf_datastore_pg_database: kong
kong_conf_datastore_pg_ssl: "off"
kong_conf_datastore_pg_ssl_verify: "off"
kong_conf_datastore_cassandra_contact_point: 127.0.0.1
kong_conf_datastore_cassandra_port: 9042
kong_conf_datastore_cassandra_keyspace: kong
kong_conf_datastore_cassandra_consistency: ONE
kong_conf_datastore_cassandra_timeout: 5000
kong_conf_datastore_cassandra_ssl: "off"
kong_conf_datastore_cassandra_ssl_verify: "off"
kong_conf_datastore_cassandra_username: kong
kong_conf_datastore_cassandra_password: kong
kong_conf_datastore_cassandra_repl_strategy: SimpleStrategy
kong_conf_datastore_cassandra_repl_factor: 1
kong_conf_datastore_cassandra_data_centers: dc1:2,dc2:3
```

##### Kong `Clustering` configuration

```yaml
kong_conf_clustering_cluster_listen_ip: 0.0.0.0
kong_conf_clustering_cluster_listen_port: 7946
kong_conf_clustering_cluster_listen: "{{ kong_conf_clustering_cluster_listen_ip }}:{{ kong_conf_clustering_cluster_listen_port }}"
kong_conf_clustering_cluster_listen_rpc_ip: 127.0.0.1
kong_conf_clustering_cluster_listen_rpc_port: 7373
kong_conf_clustering_cluster_listen_rpc: "{{ kong_conf_clustering_cluster_listen_rpc_ip }}:{{ kong_conf_clustering_cluster_listen_rpc_port }}"
kong_conf_clustering_cluster_advertise: ""
kong_conf_clustering_cluster_encrypt_key: ""
kong_conf_clustering_cluster_ttl_on_failure: 3600
kong_conf_clustering_cluster_profile: wan
```

##### Kong `DNS Resolver` configuration

```yaml
kong_conf_dns_resolver_dnsmasq: "on"
kong_conf_dns_resolver_dnsmasq_port: 8053
kong_conf_dns_resolver_dns_resolver: 8.8.8.8
```

##### Kong `Miscellaneous` configuration

```yaml
kong_conf_miscellaneous_lua_ssl_trusted_certificate: ""
kong_conf_miscellaneous_lua_ssl_verify_depth: 1
kong_conf_miscellaneous_lua_code_cache: "on"
kong_conf_miscellaneous_lua_package_path: ""
kong_conf_miscellaneous_lua_package_cpath: ""
```

## Dependencies

`None`.

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
