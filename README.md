# vless-ansible
Ansible Playbook for configuring VLESS+WebSocket+TLS+Web

sample ansible host file (/etc/ansible/hosts):

```bash
[v2servers]
example_vless1.example.com  ansible_ssh_port=22 ansible_ssh_user='root' ansible_ssh_pass=''
example_vless2.example.com ansible_ssh_port=22 ansible_ssh_user='root' ansible_ssh_pass=''
```

Configure DNS, diable CDN, run the playbook, and turn on the CDN if you want.
