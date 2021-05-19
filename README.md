# DevOps Collection for Ansible

这个`Collection`包括：

* 初始化服务器配置：[clay_wangzhi.sysinit](https://github.com/clay-wangzhi/ansible-role-sysinit)
* 安装配置 jenkins ：[clay_wangzhi.jenkins](https://github.com/clay-wangzhi/ansible-role-jenkins)

* 安装配置 mysql 主从：[clay_wangzhi.mysql](https://github.com/clay-wangzhi/ansible-role-mysql)
* 安装配置 tomcat ：[clay_wangzhi.tomcat](https://github.com/clay-wangzhi/ansible-role-tomcat)
* 安装配置 zabbix ：[docs](docs/ansible-install-zabbix.md)
  * 安装配置 zabbix-server ：[dj-wasabi.zabbix-server](https://github.com/dj-wasabi/ansible-zabbix-server)
  * 安装配置 zabbix-proxy ：[dj-wasabi.zabbix-proxy](https://github.com/dj-wasabi/ansible-zabbix-proxy)
  * 安装配置 zabbix-agent ：[dj-wasabi.zabbix-agent](https://github.com/dj-wasabi/ansible-zabbix-agent)
* 安装配置 elk ：[docs](docs/ansible-install-elk.md)
  * 安装配置 elasticsearch ：[elastic.elasticsearch](https://github.com/elastic/ansible-elasticsearch)
  * 安装配置 kibana ：[clay_wangzhi.kibana](https://github.com/clay-wangzhi/ansible-role-kibana)
  * 安装配置 logstash ：[clay_wangzhi.logstash](https://github.com/clay-wangzhi/ansible-role-logstash)
  * 安装配置 zookeeper ：[clay_wangzhi.zookeeper](https://github.com/clay-wangzhi/ansible-role-zookeeper) 
  * 安装配置 kafka ：[clay_wangzhi.kafka](https://github.com/clay-wangzhi/ansible-role-kafka)
  * 安装配置 filebeat ：[elastic.beats](https://github.com/elastic/ansible-beats)
* 二进制方式 安装配置 kubernetes 集群：https://github.com/easzlab/kubeasz

## Usage

Install this collection locally:

    ansible-galaxy collection install git+https://github.com/clay-wangzhi/ansible-collection-devops.git -p ./collections

Then you can use the roles from the collection in your playbooks:

    ---
    - hosts: all
    
      collections:
        - clay_wangzhi.devops
    
      roles:
        - kubernetes
        - helm
        - role: k8s_manifests
          vars:
            k8s_manifests_base_dir: ''
            k8s_manifests:
              - monitoring/prometheus
              - dir: docker-registry
                namespace: registry

> If you want to be more explicit, you can use the fully-qualified role name when referring to a role in this collection, like `geerlingguy.k8s.kubernetes` instead of just `kubernetes`. This could be helpful if, for example, you maintain a separate `kubernetes` role in another place on your local workstation.

### Pushing a new version

Before tagging a new version, make sure all the git submodules are up to date:

    git submodule update --recursive --remote

Then commit and push all changes, and make sure all tests are passing.

Then tag the new version of the collection and push the tag.

Once pushed, if tests pass, Travis CI will deploy the new collection version using the playbook in `scripts/deploy.yml`. That directory also contains the `galaxy.yml` template that will be used to build the collection metadata.

## Author

This collection was created in 2021 by Clay.

