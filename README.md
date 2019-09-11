参考视频地址：https://www.bilibili.com/video/av33611758/?p=5

## 修改主机名称

hostname master

## inventory 主机清单

测试从机存活

需要先实现master到node的ssh通信

修改node sshd_config 如下配置

PermitRootLogin 置为 yes
PubkeyAuthentication 置为 yes
PasswordAuthentication 置为 yes

vim /etc/ansible/hosts

ansible 192168.33.11 -m ping

ansible 配置文件 /etc/ansible/ansible.cfg


## 模块
ansible-doc command

ansible all -a 'chdir=/boot ls'

使用shell 模块对test1用户进行密码设置
ansible all -a 'useradd test1'
ansible all -m shell -a 'echo vagrant|passwd --stdin test1'

script 模块执行脚本

ansible all -m script -a './host.sh'

更新selinux
cp /etc/selinux/config ./
vim config
修改 SELINUX=disabled
将修改后的文件同步到各机器
ansible all -m copy -a 'src=./config dest=/etc/selinux/config backup=yes'