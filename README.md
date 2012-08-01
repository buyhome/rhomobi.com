## RhoMobi

This is the source code of [Rhomobile开源中文社区](http://rhomobi.com) website.

## Install

* You need *Ruby 1.9.2+*, *Rubygems* and *Rails 3.2+* first.
* Install and start *Redis*, *MongoDB*, *memcached*, *Python*, *Pygments*
* You need *JDK 1.6+* first at all... for sunspot_solr-1.3.0(my QQ note.)


```bash
#非64位机器
wget -c http://rhomobi.com/jdk6_33.tar.gz
tar zxvf jdk6_33.tar.gz
chmod a+x jdk-1_6_0_33-linux-i586.bin
./jdk-1_6_0_33-linux-i586.bin

vi /etc/profile
export JAVA_HOME=/usr/java/jdk
export CLASSPATH=.:$JAVA_HOME/jre/lib/rt.jar:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
export PATH=$PATH:$JAVA_HOME/bin

```

#Redis install
直接make就可以执行

```bash
make

/data0/redis-2.4.15/src/redis-server /data0/redis-2.4.15/redis.conf

daemonize：是否以后台daemon方式运行
pidfile：pid文件位置
port：监听的端口号
timeout：请求超时时间
loglevel：log信息级别
logfile：log文件位置
databases：开启数据库的数量
save * *：保存快照的频率，第一个*表示多长时间，第三个*表示执行多少次写操作。在一定时间内执行一定数量的写操作时，自动保存快照。可设置多个条件。
rdbcompression：是否使用压缩
dbfilename：数据快照文件名（只是文件名，不包括目录）
dir：数据快照的保存目录（这个是目录）
appendonly：是否开启appendonlylog，开启的话每次写操作会记一条log，这会提高数据抗风险能力，但影响效率。
appendfsync：appendonlylog如何同步到磁盘（三个选项，分别是每次写都强制调用fsync、每秒启用一次fsync、不调用fsync等待系统自己同步）
```

#Node.js install
```bash
$ sudo apt-get install libssl-dev apache2-utils
$ cd ~/workspace
$ git clone git://github.com/ry/node.git
$ cd node
$ ./configure
$ make
$ sudo make install

```

and run:

```bash
easy_install pygments # 或者 pip install pygments
cp config/config.yml.default config/config.yml
cp config/mongoid.yml.default config/mongoid.yml
cp config/redis.yml.default config/redis.yml
cp config/thin.yml.default config/thin.yml
bundle install
bundle exec rake db:migrate
bundle exec rake db:seed
bundle exec sidekiq -c config/sidekiq.yml
bundle exec rake sunspot:solr:start
bundle exec rake assets:precompile
rails server thin -d

```
or,

```bash
rails s thin -d

```

or you can just this issue

```bash
bundle exec rspec spec
```

to prepare all the config files and start essential services.

## Deploy

```bash
$ cap deploy
$ cap production remote_rake:invoke task=db:setup
```

# Apply Google JSAPI

* http://code.google.com/intl/zh-CN/apis/loader/signup.html

## Memcached

Dalli requires memcached 1.4.x +

## Git

#Git install
```bash
wget http://www.codemonkey.org.uk/projects/git-snapshots/git/git-latest.tar.gz
tar xzvf git-latest.tar.gz
cd git-2011-11-30 ＃你的目录可能不是这个
autoconf
./configure
make
sudo make install
```

```bash
#设定哪些文件做了修改
git add *

#commit操作
git commit -m "添加备注"

#上机
git push origin master
```

## License

Copyright (c) 2011-2012 RhoMobi.

Released under the MIT license:

* [www.opensource.org/licenses/MIT](http://www.opensource.org/licenses/MIT)
