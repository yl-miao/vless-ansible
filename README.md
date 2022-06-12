# vless-ansible
Ansible Playbook for configuring VLESS+WebSocket+TLS+Web+(CDN)

### 1. reinstall a clean OS on the target machine before running the playbook if you need:

```bash
bash <(wget --no-check-certificate -qO- 'https://raw.githubusercontent.com/MoeClub/Note/master/InstallNET.sh') -d 10 -v 64 -p "自定义root密码" -port "自定义ssh端口"
```

remember to change the password to a secure one.

### 2. make sure python is present on the target machine:

```bash
apt update
apt upgrade
apt install python3 sshpass
ssh example_vless1.example.com
```

### 3. sample ansible host file on the host machine (/etc/ansible/hosts):

remember to configure the dns of example_vless1.example.com first.

```bash
[v2servers]
example_vless1.example.com  ansible_ssh_port=22 ansible_ssh_user='root' ansible_ssh_pass=''
example_vless2.example.com ansible_ssh_port=22 ansible_ssh_user='root' ansible_ssh_pass=''
```

### 4. on the host machine, install sshpass, clone this project, choose some html template as the pseudo site and clone into the "pseudo" folder:

```bash
git clone https://github.com/yl-miao/vless-ansible.git
cd vless-ansible
git clone pseudo_site_project
mv pseudo_site_project pseudo
```

### 5. remember to configure the variables in the 90-92 lines of the playbook before running:

```bash
uuid: your_uuid_here
path: /your_path_here
local_port: your_local_port_here
```

remember to configure the firewall to block the local_port on the target machine. 

### 6. Configure DNS, diable CDN, run the playbook, and turn on the CDN if you want.

Then, you can connect using the address (example_vless1.example.com), port (443), uuid (configured in the playbook) and path (configured in the playbook) to connect to your vless server.

We use Caddy 2 as the web server, it will automatically renew TLS certificates.
