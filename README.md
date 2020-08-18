Prereq: Ensure you have installed db server on controlled node and created a demo user
# Steps:-
1. Install Ansible on your master node
2. Edit /etc/ansible/hosts file and add your managed node ip's 
[all:vars]
ansible_ssh_common_args='-o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null'
[myhost]
myweb-server ansible_host=3.129.245.78(Web server ip ie:-public ip of managed node)
[database]
mydb-server ansible_host=172.31.29.227(Data base ip ie:- private ip of managed node )
3. Ensure your hosts are pingable eg:-  "ansible -m ping myhost" 
4. Run web.yml playbook
5. Brouse URL publicip:port(8080)
