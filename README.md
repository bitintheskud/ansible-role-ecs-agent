# Centos ECS Agent Ansible Role

This role allow configuration of ECS container agent on vanilla CentOS 7 hosts. 

## Requirements

* Ansible 2.2+
* Tested on CentOS 7.4.1708

## Role Variables

For more information see : 

http://docs.aws.amazon.com/AmazonECS/latest/developerguide/ecs-agent-config.html  

* `ecs_agent_loglevel`: `ECS_LOGLEVEL` (Default: info)
* `ecs_agent_cluster_name`: `ECS_CLUSTER` (Default: default)
* `ecs_agent_enable_iam_role`: `ECS_ENABLE_TASK_IAM_ROLE` (Default: true)
* `ecs_agent_enable_task_iam_role_network_host`: `ECS_ENABLE_TASK_IAM_ROLE_NETWORK_HOST` (Default: true)
* `ecs_agent_reserved_ports`: `ECS_RESERVED_PORTS` (Default: "[22, 2375, 2376, 51678]")
* `ecs_agent_container_stop_timeout`: `ECS_CONTAINER_STOP_TIMEOUT` (Default: 30s)
* `ecs_agent_auth_type`: `ECS_ENGINE_AUTH_TYPE` (Default: "")
* `ecs_agent_auth_data`: `ECS_ENGINE_AUTH_DATA` (Default: "")
* `ecs_agent_data_dir`: `ECS_DATADIR` (Default: "/data")
* `ecs_agent_log_file`: `ECS_LOGFILE` (Default: "/log/ecs_agent.log")

## Dependencies

Docker need to be installed and running. 

See :
 
* https://github.com/bitintheskud/ansible-role-docker-ce-centos.git

## Caveats

This role sets up the AWS ECS agent as recommended in the documentation, including adding iptables rules. However, bear in mind that this role will not handle saving the iptables rules for you (via `iptables-save` or other means). If you wish to save iptables rules to disk so they will survive a reboot and be present without an additional Ansible run, you should handle that outside of this role.

## Example Playbook

```yaml

---
- name: AWS ECS Agent Playbook
  hosts: all
  become: yes
  vars:
    - ecs_agent_cluster_name: MyClusterName
  roles:
    - ansible-role-ecs-agent
```
## To improve in next version

- Add travis build.
- Add support for log driver. See: https://github.com/open-guides/og-aws#ecs-tips
- Add support for cleaning options :

**ECS_ENGINE_TASK_CLEANUP_WAIT_DURATION**
This variable specifies the time to wait before removing any containers that belong to stopped tasks. The image cleanup process cannot delete an image as long as there is a container that references it. After images are not referenced by any containers (either stopped or running), then the image becomes a candidate for cleanup. By default, this parameter is set to 3 hours but you can reduce this period to as low as 1 minute, if you need to for your application.

**ECS_DISABLE_IMAGE_CLEANUP**
If you set this variable to true, then automated image cleanup is disabled on your container instance and no images are automatically removed.

**ECS_IMAGE_CLEANUP_INTERVAL**
This variable specifies how frequently the automated image cleanup process should check for images to delete. The default is every 30 minutes but you can reduce this period to as low as 10 minutes to remove images more frequently.

**ECS_IMAGE_MINIMUM_CLEANUP_AGE**
This variable specifies the minimum amount of time between when an image was pulled and when it may become a candidate for removal. This is used to prevent cleaning up images that have just been pulled. The default is 1 hour.

**ECS_NUM_IMAGES_DELETE_PER_CYCLE**
This variable specifies how many images may be removed during a single cleanup cycle. The default is 5 and the minimum is 1.



## License

Licensed under the MIT License. See the LICENSE file for details.
