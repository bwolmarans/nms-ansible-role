# Ansible Playbook and example for NMS, NGINX, NGINX Agent, and ACM

This is a set of roles for installing NGINX Management Suite (NMS) and NGINX+, NGINX Agent and also there is a role to install the NMS license, and a role to install API Connectivity Manager (ACM).  There are also some example playbooks to try out the roles.

Note: This role is still in active development. There may be unidentified issues and the role variables may change as development continues.

## Prerequisites

- Below are the required dependencies required by this role.
```shell
ansible-galaxy install nginxinc.nginx
ansible-galaxy collection install community.general
```

There are 4 roles defined in this project (located in `roles` directory):

1. install-nms <- this installs just NMS itself, on the NMS host
2. install-nginx-and-agent <- this installs NGINX (could be + or OSS, you can specify this in variables) and the Nginx agent, on a host that is going to process data traffic a'la NGINX.
3. install-nms-license <- this only installs the nms license, on the NMS host, and you need to get this from your myF5 trial
4. install-acm <- this only installs the ACM module on the NMS host


## Usage

1. Copy NGINX+ certs to this projects root. Or update the `nginx_license` certificate and keys paths located in `var/nginx-controller.yml` and `var/nginx-data.yml`
2. To modify NGINX Plus install/upgrade on the NMS Host, take a look at `var/nginx-controller.yml` to see variables.
3. To modify NGINX Plus install on the Data Plane Hosts, take a look at `var/nginx-data.yml` to see variables.
4. Anything related to NIM / NGINX Agent, look at variables in `var/nms.yml`. This is work in progress.
5. Update `inventory` file with your NMS Host and Data Plane Hosts. The expectation is at least one of each.
6. Then run `ansible-playbook -i inventory nms-and-agent-install-example.yml`, this does not do the license or ACM, you will do that next
7. `ansible-playbook -i inventory install-just-license.yml`
8. `ansible-playbook -i inventory install-just-acm.yml`
9. Now, go and log into NMS using admin/(you know the password!) and try out NIM and ACM
 
