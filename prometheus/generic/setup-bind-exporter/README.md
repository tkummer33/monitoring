setup-bind-exporter
=========

This role will instantiate a bind-exporter container on targeted hosts. The statistics page has to be enabled and available locally on targeted hosts. 

Requirements
------------

Docker must be available and running on the targeted hosts.
The statistics page has to be enabled and available locally on targeted hosts.
The docs about stats page are available here: https://kb.isc.org/docs/aa-01123

Role Variables
--------------
Default values of variables:
```
bind_exporter_image: 'prometheuscommunity/bind-exporter'
bind_exporter_image_version: 'latest'
bind_exporter_port: '9119'
bind_stats_port: '8053'

provision_state: "started"
```
`bind_exporter_image` - The bind exporter image to deploy.
`bind_exporter_image_version` - The image tag to deploy.
`bind_exporter_port` - The port to expose on the target hosts.
`bind_stats_port` - The port on which bind stats are available
`provision_state` - Options: [absent, killed, present, reloaded, restarted, **started** (default), stopped]


Dependencies
------------
```
python >= 2.6
docker-py >= 0.3.0
The docker server >= 0.10.0
```

Example Playbook
----------------
```
- name: Setup node exporters
  hosts: prometheus_bind
  become: True
  vars:
    provision_state: "started"
  roles:
    - prometheus/generic/setup-bind-exporter
```

How to enable stats page
------------------------
Below is configuration snippet from /etc/named.conf which enables statistics page on local port 8053

```
statistics-channels {
  inet 127.0.0.1 port 8053 allow { 127.0.0.1; };
};
```

License
-------

BSD
