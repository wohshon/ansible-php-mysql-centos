##Building a simple LAMP stack and deploying Application using Ansible Playbooks.
-------------------------------------------

(Modified from Ansible examples - lamp_simple_rhel7, supported on aws ec2

- roles/web/templates/ 
modified original jinjia templates to pick the correct ip address. Original
example uses default ipv4 address. 
In this branch, `tag_node_type_db` group vars is used; `ec2_private_ip_address` is used to retrieved ip 

- roles/db/tasks 
added commands to remove anonymous users in mysql and to flush privileges

)

These playbooks require Ansible 1.2.

These playbooks are meant to be a reference and starter's guide to building
Ansible Playbooks. These playbooks were tested on CentOS 7.x so we recommend
that you use CentOS or RHEL to test these modules.

RHEL7 version reflects changes in Red Hat Enterprise Linux and CentOS 7:
1. Network device naming scheme has changed
2. iptables is replaced with firewalld
3. MySQL is replaced with MariaDB

This LAMP stack can be on a single node or multiple nodes. The inventory file
'hosts' defines the nodes in which the stacks should be configured.


Instances in ec2 are tagged as `node-type=app` or `node-type=db` so the dynamic inventory will autogenerate these group of tags: `tag_node_type_app` or `tag_node_type_db`

Create a corresponding `tag_node_type_db` group vars to replace the `dbservers` group vars as well as any references to the `dbservers` group


Once done, you can check the results by browsing to http://192.168.223.123/index.php.
You should see a simple test page and a list of databases retrieved from the
database server.
