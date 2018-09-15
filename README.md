# serpstat
Serpstat test task

Необходимо написать сценарий (установки), который одновременно установит на 10 одинаковых серверов c CentOS7:
- php7 с модулями (bcmatch, imagik, pdo, amqp);
- phpmyadmin;
- nginx;
- mysql 5.6;
- redis.

Скрипт должен выполняться с вашего компьютера. Скрипт может быть написан на чём угодно, можно использовать любые инструменты.

#############################################

1. aws_keys.yml should have:
 aws_access_key: ***************  
 aws_secret_key: *******************************  

2. generate key pair in AWS console and place pem file in the folder with playbooks,  for example "lab.pem"

3. Add following lines to /etc/ansible/ansible.conf
host_key_checking = False
private_key_file = /home/user/serpstat/lab.pem

3. launch playbook:
ansible-playbook -i hosts --ask-vault-pass aws_provisioning.yml
and login to PMA using  link:   http://EC2PublicIP
user: pma
password: qwerty123

4. To terminate EC2 instances use playbook:
ansible-playbook -i hosts --ask-vault-pass ec2_down.yml 

5. You can create as many servers as you need. Set 
count: <integer>   
in  vars of aws_provisioning.yml
