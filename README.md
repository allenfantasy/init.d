```
   ______              __           __
  /\__  _\          __/\ \__       /\ \
  \/_/\ \/     ___ /\_\ \ ,_\      \_\ \
     \ \ \   /' _ `\/\ \ \ \/      /'_` \
      \_\ \__/\ \/\ \ \ \ \ \_  __/\ \L\ \
      /\_____\ \_\ \_\ \_\ \__\/\_\ \___,_\
      \/_____/\/_/\/_/\/_/\/__/\/_/\/__,_ /
```

#### 配置新机过程：


[ 用root登入  非root用户要加sudo ]

```bash
adduser deployer —ingroup sudo
apt-get install openssh-server
mkdir /home/deployer/.ssh
```

[ 用deployer登入 ]

```bash
sudo apt-get install git
git clone https://github.com/allenfantasy/init.d.git
cd ./init.d
./install_dev_env                             # 如果这一步速度很慢，则执行./replace_mirrors，再重新运行该指令
source ~/.bashrc && rvm pkg install readline && rvm install 2.1.1 && rvm use 2.1.1 --default
./install_bundler
```

设定postgres的账号密码（例子中用户xxx，密码yyy，数据库xxx_production）

```
sudo -u postgres psql
postgres=# create user xxx with password 'yyy'; 
postgres=# ALTER USER xxx WITH SUPERUSER;
postgres=# create database xxx_production owner xxx;
```
