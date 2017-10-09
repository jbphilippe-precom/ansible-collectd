Role Name
=========

This role install Collectd and his plugins

Requirements
------------

Ubuntu Trusty & Xenial

ANSIBLE > v2.0

Role Variables
--------------

### Collectd Task:

    ansible-collectd
      - main.yml
      - collectd_install.yml
      - collectd_config.yml
      - collectd_install_plugin_apache.yml
      - collectd_install_plugin_nfs.yml
      - collectd_install_plugin_nginx.yml
      - collectd_install_plugin_postgresql.yml
      - collectd_install_plugin_libvirt.yml
      - collectd_install_plugin_varnish.yml
      - collectd_install_plugin_mongodb.yml
      - collectd_install_plugin_mysql.yml
      - collectd_install_plugin_redis.yml
      - collectd_install_plugin_cassandra.yml
      - collectd_install_plugin_nodejs.yml
      - collectd_install_plugin_tcpconns.yml
      - collectd_install_plugin_haproxy.yml
      - collectd_install_plugin_elasticsearch.yml
      - collectd_install_plugin_zookeeper.yml
      - collectd_install_plugin_kafka.yml
      - collectd_install_plugin_karaf.yml
      - collectd_install_plugin_activemq.yml


### variables:

    # Secrets
        # Postgresql
        collectd_postgresql_monitoring_passwd: < password_monitoring_user >
        # MongoDB
        collectd_mongodb_monitoring_password: < password_monitoring_user >
        mongodb_admin_password: < password_MongoDB_admin_user >
        # Mysql
        collectd_mysql_monitoring_password: < password_monitoring_user >
        mysql_root_password: < password_mysql_root_user >
        # Karaf
        karaf_jmx_user_password: < password_karaf_for_jmx_user >
        # ActiveMQ
        activemq_jmx_user_password: < password_activemq_for_jmx_user >

    # Default variable

    # Collectd
        collectd_service_name: collectd
        collectd_conf_path: /etc/collectd
        collectd_host_receives_data: metro02g.bserv1.local
        collectd_port: 25826
        collectd_interval: 60
        # Collectd server
        collectd_server: False
        collectd_list_host_receives_data:
          - ""
        collectd_listen_bind: 0.0.0.0
        collectd_listen_port: 25826
        collectd_forward: true

    # Postgresql plugin
        collectd_postgresql_monitoring_user: collectd
        collectd_postgresql_port: 5432
        collectd_postgresql_dblist:
          - < Name database postgresql 1 >
          - < Name database postgresql N >

    #MongoDB plugin
        collectd_mongodb_dblist:
          - < Name database mongodb 1 >
          - < Name database mongodb N >

    # Mysql plugin
        collectd_mysql_monitoring_user: collectd
        collectd_mysql_dblist:
          - < Name database mysql 1 >
          - < Name database mysql N >

    # Redis plugin
        collectd_redis_auth: ""
        collectd_redis_portlist:
          - < Port of local Redis instance 1 >
          - < Port of local Redis instance 2 >

    # ElasticSearch
        es_cluster_name: "elasticsearch"
        es_http_port: 9200
        es_host_name: localhost

    # Tcpconns plugin
        collectd_tcpconns_localport_list:
            - < Port 1 >
            - < Port 2 >
        collectd_tcpconns_remoteport_list:
            - < Port 1 >
            - < Port 2 >
    # Haproxy
        collectd_haproxy_monitor:
            - ""
        collectd_haproxy_ignore:
            - ""
        collectd_haproxy_python_path: "/usr/lib/python2.7"
        collectd_haproxy_socket: "/var/run/haproxy/admin.sock"

    # Zookeeper
        kafka_zookeeper_bind_port: "2181"
        collectd_zookeeper_instance_name: "prod"

    # kafka
        kafka_jmx_port: 9997

    # Karaf
        karaf_jmx_user: "jmxuser"
    # Activemq
        activemq_jmx_port: "11099"
        activemq_jmx_user: "jmx_user"

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too: Note: The group must be named "hosts" in inventory file

Inventory file example:

    [hosts]
    host01.btsys.local
    host02.btsys.local
    host03.btsys.local

Playbook example:

    - name: deploy collectd
      hosts: hosts
      become: yes
      vars:
        collectd_host_receives_data: "metro02g.bserv1.local"
        collectd_install_plugins_list:
          - postgresql
          - nginx
        collectd_postgresql_dblist:
          - Exemple1
          - Exemple2
      roles:
        - ../ansible-collectd

Plugins
-----------------

    Plugins available for variable collectd_install_plugins_list:
        - postgresql
        - nginx
        - apache
        - nfs
        - libvirt
        - varnish
        - mysql
        - mongodb
        - redis
        - nodejs
        - tcpconns
        - haproxy
        - elasticsearch
        - zookeeper
        - kafka
        - karaf
        - activemq

Tags
-----------------

    installation : Collectd install + plugins installation if specified
    add-plugins : Install collectd plugin for specific middleware

Exemple of launch
-----------------

      # Install collectd and plugins if var collectd_install_plugins_list is defined
      export ANSIBLE_HOST_KEY_CHECKING=False; ansible-playbook -i hosts playbook.yml --ask-vault-pass --ask-pass --ask-become-pass --tags installation
      # Just add plugins declared in collectd_install_plugins_list var
      export ANSIBLE_HOST_KEY_CHECKING=False; ansible-playbook -i hosts playbook.yml --ask-vault-pass --ask-pass --ask-become-pass --tags add-plugins

License
-------

BSD

Author Information
------------------

BSO ISL - sponge
