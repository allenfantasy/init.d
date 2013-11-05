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
```

[ 用deployer登入 ]

```bash
sudo apt-get install git
git clone https://github.com/allenfantasy/init.d.git
cd ./init.d
./install_dev_env                             # 如果这一步速度很慢，则执行./replace_mirrors，再重新运行该指令
source ~/.bashrc
./install_ruby
rvm use 1.9.3 --default
source ~/.bashrc && rvm pkg install readline && rvm install 1.9.3 && rvm use 1.9.3 --default
./install_bundler
ssh-keygen -t rsa -C "dev@dongxi.example.com" # 然后按3次回车
more .ssh/id_rsa.pub                          # 得到key后在github账号设定中Add Key
ssh -T git@github.com                         # => Hi xxx! ...
```

设定postgres的账号密码（例子中用户blog，数据库blog_production）

```
sudo -u postgres psql
postgres=# create user blog with password 'secret'; 
postgres=# ALTER USER blog WITH SUPERUSER;
postgres=# create database blog_production owner blog;
```
