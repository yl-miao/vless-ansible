# vless-ansible
Ansible Playbook for configuring VLESS+WebSocket+TLS+Web+(CDN).

### 0. (OPTIONAL) Reinstall a clean OS on the [target machine] before running the playbook if you need:

```bash
wget --no-check-certificate -O AutoReinstall.sh https://git.io/AutoReinstall.sh && bash AutoReinstall.sh
```

### 1. Install Ansible on the [host machine]:

https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html

Also, install rsync on the [host machine]:

```bash
sudo apt install rsync
```

### 2. Make sure python is present on the [target machine]:

```bash
apt update
apt upgrade
apt install python3
```

### 3. Sample ansible host file on the [host machine] (/etc/ansible/hosts):

remember to configure the DNS of example_vless1.example.com first.

```bash
[v2servers]
example_vless1.example.com  ansible_ssh_port=22 ansible_ssh_user='root' ansible_ssh_pass=''
example_vless2.example.com ansible_ssh_port=22 ansible_ssh_user='root' ansible_ssh_pass=''
```

### 4. On the [host machine], install sshpass, clone this project, choose some html template as the pseudo site (such as https://github.com/aamahi/Green-Leaf-Tea-Shop-HTML-Template) and clone into the "pseudo" folder, and get ssh fingerprint of the [target machine]:

```bash
git clone https://github.com/yl-miao/vless-ansible.git
cd vless-ansible
git clone pseudo_site_project
mv pseudo_site_project pseudo
apt install sshpass
ssh example_vless1.example.com
```

### 5. Remember to configure the variables in the 94-96 lines of the playbook (v2.yaml) on the [host machine] before running:

```bash
uuid: your_uuid_here
path: /your_path_here
local_port: your_local_port_here
```
(remember to configure the firewall to block the local_port on the target machine. local_port should not be 443 since we have Caddy V2.)

### 6. Configure DNS, diable CDN, run the playbook on the [host machine], and turn on the CDN if you want.

```bash
ansible-playbook vless.yaml
```

Then, you can connect to your vless server using the address (example_vless1.example.com), port (443), uuid (configured in the playbook) and path (configured in the playbook).

We use Caddy 2 as the web server, it will automatically renew TLS certificates.

#### [Warning]:

Right now this only supports [target machines] of Debian/Ubuntu/Raspbian. Any firewall rules will be disabled on the [target machine] after performing this Ansible Playbook.
