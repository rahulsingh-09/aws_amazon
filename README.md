# Steps:-
1. Install Ansible on your master node
2. Edit /etc/ansible/hosts file and add your managed node ip's 
3. Ensure your hosts are pingable eg:-  "ansible -m ping all" 
4. Run web.yml playbook
5. Brouse URL ip:port
