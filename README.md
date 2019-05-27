openvpn
=======

[![Build Status](https://travis-ci.org/andrelohmann/ansible-role-openvpn.svg?branch=master)](https://travis-ci.org/andrelohmann/ansible-role-openvpn)

Use this role to deploy an openvpn server. Benefit from the [andrelohmann.easy_rsa](https://github.com/andrelohmann/ansible-role-easy_rsa) role to create all necessary certs and keys.

Requirements
------------

It's strongly suggested, to store your ca somewhere secure and not on the openvpn server itself.

Copy the files ca.crt, server.crt, server.key, ta.key and the dh file to a directory from where they can be imported to the server (e.g. {{ playbook_dir }}/host_templates/{{ inventory_hostname }}/files/).

Role Variables
--------------

The following mandatory variables need to be set in group_vars/host_vars

    openvpn_import_directory: "host_templates/{{ inventory_hostname }}/files/" # Directoriy to Import cert and key files from
    openvpn_ca_crt_filename: "ca.crt"
    openvpn_server_crt_filename: "server.crt"
    openvpn_server_key_filename: "server.key"
    openvpn_ta_key_filename: "ta.key"
    openvpn_dh_filename: dh1024.pem
    openvpn_listen_ip: 0.0.0.0
    openvpn_listen_port: 1194
    openvpn_network: 172.16.0.0
    openvpn_netmask: 255.255.255.0
    openvpn_push_routes:
    - 'push "route 172.16.0.0 255.255.255.0"'
    openvpn_max_clients: 10
    openvpn_user: openvpn
    openvpn_group: openvpn
    openvpn_server_proto: "tcp/udp"
    openvpn_dev: "tun/tap"
    openvpn_additional_parameters:
    - resolv-retry infinite
    - nobind
    - user nobody
    - group nogroup
    - persist-key
    - persist-tun
    - remote-cert-tls server
    - cipher AES-128-CBC
    - comp-lzo
    - verb 3
    openvpn_static_clients:
    - name: clientOne
      ip: 172.16.0.10
    - name: clientTwo
      ip: 172.16.0.20
    - name: clientThree
      ip: 172.16.0.30

Example Playbook
----------------

    - hosts: openvpn
      roles:
         - { role: andrelohmann.openvpn }

License
-------

MIT

Author Information
------------------

https://github.com/andrelohmann
