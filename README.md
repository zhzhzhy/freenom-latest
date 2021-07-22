<div align="center">
<h1>Freenom：freenom域名自动续期</h1>

[![Build Status](https://img.shields.io/badge/build-passed-brightgreen?style=for-the-badge)](https://scrutinizer-ci.com/g/luolongfei/freenom/build-status/master)
[![Php Version](https://img.shields.io/badge/php-%3E=7.2-brightgreen.svg?style=for-the-badge)](https://secure.php.net/)
[![Scrutinizer Code Quality](https://img.shields.io/badge/scrutinizer-9.31-brightgreen?style=for-the-badge)](https://scrutinizer-ci.com/g/luolongfei/freenom/?branch=master)
[![MIT License](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=for-the-badge)](https://github.com/luolongfei/freenom/blob/master/LICENSE)

Documentation: [English version](https://github.com/luolongfei/freenom/blob/master/README_EN.md) | 中文版
</div>

[📃  前言](#--前言)

[🍭  效果](#--效果)

[🎁  事前准备](#--事前准备)

[📪  配置发信邮箱](#--配置发信邮箱)

<hr>

*（下面三种部署方式，选择其中一种即可）*

[⛵  通过 Docker 方式部署](#--方式一通过-docker-部署最简单的方式)（最简单的方式，推荐）

[🕹  通过腾讯云函数（SCF）部署](#--方式二通过腾讯云函数scf部署)

[🚧  直接拉取源码部署](#--方式三直接拉取源码部署)

<hr>

[📋  捐赠名单 Donate List](#--捐赠名单-donate-list)

[❤  捐赠 Donate](#--捐赠-donate)

[🚁  我正在用的 VPS](#--我正在用的-VPS)

[🍺  信仰](#--信仰)

[🌚  作者](#--作者)

[📰  更新日志](#--更新日志) （每次新版本发布，可以参考此日志决定是否更新）

[🎉  鸣谢](#--鸣谢)

[🥝  开源协议](#--开源协议)

<h5>注意：GitHub 官方不允许使用 GitHub Action 做签到或者续期类应用，否则会封禁项目甚至封号，故为项目能长期维护下去，应 GitHub 官方要求，
本项目已经移除 Action 方式的应用，望周知。已经 fork 使用的，可以尽快将项目转移到自己的 VPS 上，推荐通过 Docker 部署，
或者直接搬运到腾讯云函数部署。本项目依然长期维护。</h5>

### 📃  前言
众所周知，Freenom是地球上唯一一个提供免费顶级域名的商家，不过需要每年续期，每次续期最多一年。由于我申请了一堆域名，而且不是同一时段申请的，
所以每次续期都觉得折腾，于是就写了这个自动续期的脚本。

### 🍭  效果
![邮件示例](https://s2.ax1x.com/2020/01/31/139Rrd.png "邮件内容")

无论是续期成败或者脚本执行出错，都会收到的程序发出的邮件。如果是续期成败相关的邮件，邮件会包括未续期域名的到期天数等内容。
邮件参考了微信发送的注销公众号的邮件样式。

### 🎁  事前准备
- 发信邮箱：为了方便理解又称机器人邮箱，用于发送通知邮件。目前支持`Gmail`、`QQ邮箱`以及`163邮箱`，程序会自动判断发信邮箱类型并使用合适的配置。
- 收信邮箱：用于接收机器人发出的通知邮件。推荐使用`QQ邮箱`，`QQ邮箱`唯一的好处只是收到邮件会在`QQ`弹出消息。
- VPS：随便一台服务器都行，系统推荐`Centos7`，另外PHP版本需在`php7.2`及以上。如果你没有 VPS，可以考虑一下 [🚁  我正在用的 VPS](#--我正在用的-VPS) ，最便宜的机器`9.9美元`一年。
- 没有了

### 📪  配置发信邮箱
下面分别介绍`Gmail`、`QQ邮箱`以及`163邮箱`的设置，你只用看自己需要的部分。注意，`QQ邮箱`与`163邮箱`均使用账户加授权码的方式登录，
`谷歌邮箱`使用账户加密码的方式登录，请知悉。另外还想吐槽一下，国产邮箱你得花一毛钱给邮箱提供方发一条短信才能拿到授权码。

*（点击即可展开或收起）*

<details>
    <summary>设置Gmail</summary>
<br>
  
1、在`设置>转发和POP/IMAP`中，勾选
- 对所有邮件启用 POP 
- 启用 IMAP

![gmail配置01](https://s2.ax1x.com/2020/01/31/13tKsg.png "gmail配置01")

然后保存更改。

2、允许不够安全的应用

登录谷歌邮箱后，访问 [谷歌权限设置界面](https://myaccount.google.com/u/0/lesssecureapps?pli=1&pageId=none) ，启用允许不够安全的应用。

![gmail配置02](https://s2.ax1x.com/2020/01/31/1392KH.png "gmail配置02")

另外，若遇到提示
> 不允许访问账户

登录谷歌邮箱后，去 [gmail的这个界面](https://accounts.google.com/b/0/DisplayUnlockCaptcha) 点击允许。这种情况较为少见。

***

</details>

<details>
    <summary>设置QQ邮箱</summary>
<br>

在`设置>账户>POP3/IMAP/SMTP/Exchange/CardDAV/CalDAV服务`下，开启`POP3/SMTP服务`

![qq邮箱配置01](https://s2.ax1x.com/2020/01/31/13cIKA.png "qq邮箱配置01")

此时坑爹的QQ邮箱会要求你用手机发送一条短信给腾讯，发送完了点一下`我已发送`

![qq邮箱配置02](https://s2.ax1x.com/2020/01/31/13c4vd.png "qq邮箱配置02")

然后你就能看到你的邮箱授权码了，使用邮箱账户加授权码即可登录，记下授权码

![qq邮箱配置03](https://s2.ax1x.com/2020/01/31/13cTbt.png "qq邮箱配置03")

![qq邮箱配置04](https://s2.ax1x.com/2020/01/31/13coDI.png "qq邮箱配置04")

***

</details>

<details>
    <summary>设置163邮箱</summary>
<br>

在`设置>POP3/SMTP/IMAP`下，开启`POP3/SMTP服务`和`IMAP/SMTP服务`并保存

![163邮箱配置01](https://s2.ax1x.com/2020/01/31/13WKZn.png "163邮箱配置01")

![163邮箱配置02](https://s2.ax1x.com/2020/01/31/13WQI0.png "163邮箱配置02")

现在点击侧边栏的`客户端授权密码`，并获取授权码，你看到画面可能和我不一样，因为我已经获取了授权码，所以只有`重置授权码`按钮，这里自己根据网站提示申请获取授权码，网易和腾讯一样恶心，需要你用手机给它发一条短信才能拿到授权码

![163邮箱配置03](https://s2.ax1x.com/2020/01/31/13WMaq.png "163邮箱配置03")

163 邮箱送信后，接收方如果没收到可以在垃圾邮件里面找一下。

***

</details>

#### Telegram bot

上面介绍了三种邮箱的设置方法，如果你不想使用邮件推送，也可以使用 Telegram bot，灵活配置。在`.env`文件中，
将`TELEGRAM_BOT_ENABLE`的值改为`true`，即可启用 Telegram bot，同样的，将`MAIL_ENABLE`的值改为`false`即可关闭邮件推送方式。
Telegram bot 有两个配置项，一个是`chatID`（对应`.env`文件中的`TELEGRAM_CHAT_ID`），
通过使用你的 Telegram 账户发送`/start`给`@userinfobot`即可以获取自己的id，
另一个是`token`（对应`.env`文件中的`TELEGRAM_BOT_TOKEN`），你的 Telegram bot 令牌，你会创建 Telegram bot 就知道怎么获取，
不多赘述。如何创建一个 Telegram bot 请参考：[官方文档](https://core.telegram.org/bots#6-botfather)

***

*与通知相关的设置到此就完成了，下面开始讲本项目的三种使用方式，一种是通过 Docker，另一种是通过腾讯云函数，再一种是直接拉取源码部署，推荐使用 Docker 方式，无需纠结环境。*

### ⛵  方式一：通过 Docker 部署（最简单的方式）

<hr>

Docker 仓库地址为： [https://hub.docker.com/r/luolongfei/freenom](https://hub.docker.com/r/luolongfei/freenom) ，同样欢迎 star 。
此镜像支持的架构为`linux/amd64`，`linux/arm64`，`linux/ppc64le`，`linux/s390x`，`linux/386`，`linux/arm/v7`，`linux/arm/v6`，
理论上支持`群晖`、`威联通`、`树莓派`以及各种类型的`VPS`。

#### 1、安装 Docker

##### 1.1 以 root 用户登录，执行一键脚本安装 Docker

升级源并安装软件（下面两行命令二选一，根据你自己的系统）

Debian / Ubuntu
```shell
apt-get update && apt-get install -y wget vim
```
CentOS
```shell
yum update && yum install -y wget vim
```

执行此命令等候自动安装 Docker
```shell
wget -qO- get.docker.com | bash
```

说明：请使用 KVM 架构的 VPS，OpenVZ 架构的 VPS 不支持安装 Docker，另外 CentOS 8 不支持用此脚本来安装 Docker。
更多关于 Docker 安装的内容参考 [Docker 官方安装指南](https://docs.docker.com/engine/install/) 。

##### 1.2 对 Docker 的一些命令操作

查看 Docker 安装版本等信息
```shell
docker version
```

启动 Docker 服务
```shell
systemctl start docker
```

查看 Docker 运行状态
```shell
systemctl status docker
```

将 Docker 服务加入开机自启动
```shell
systemctl enable docker
```

#### 2、通过 Docker 部署域名续期脚本

##### 2.1 用 Docker 创建并启动容器

命令如下
```shell
docker run -d --name freenom --restart always -v $(pwd):/conf -v $(pwd)/logs:/app/logs luolongfei/freenom
```
或者，如果你想自定义脚本执行时间，则命令如下
```shell
docker run -d --name freenom --restart always -v $(pwd):/conf -v $(pwd)/logs:/app/logs -e RUN_AT="11:24" luolongfei/freenom
```
 上面这条命令只比上上条命令多了个` -e RUN_AT="11:24"`，其中`11:24`表示在北京时间每天的 11:24 执行续期任务，你可以自定义这个时间。
 这里的`RUN_AT`参数同时也支持 CRON 命令里的时间形式，比如，` -e RUN_AT="9 11 * * *"`，表示每天北京时间 11:09 执行续期任务，
 如果你不想每天执行任务，只想隔几天执行，只用修改`RUN_AT`的值即可。
 
 **注意：不推荐自定义脚本执行时间。因为你可能跟很多人定义的是同一个时间点，这样可能导致所有人都是同一时间向 Freenom 的服务器发起请求，
 使得 Freenom 无法稳定提供服务。而如果你不自定义时间，程序会自动指定北京时间 06 ~ 23 点全时段随机的一个时间点作为执行时间，
 每次重启容器都会自动重新指定。**

<details>
    <summary>点我查看上方 Docker 命令的参数解释</summary>
<br>

| 命令 | 含义 |
| :--- | :--- |
| docker run | 开始运行一个容器 |
| -d 参数 | 容器以后台运行并输出容器 ID |
| --name 参数 | 给容器分配一个识别符，方便将来的启动，停止，删除等操作 |
| --restart 参数 | 配置容器启动类型，always 即为 docker 服务重新启动时自动启动本容器 |
| -v 参数 | 挂载卷（volume），冒号后面是容器的路径，冒号前面是宿主机的路径（只支持绝对路径），`$(pwd)`表示当前目录 |
| -e 参数 | 指定容器中的环境变量 |
| luolongfei/freenom | 这是从 docker hub 下载回来的镜像完整路径名 |

</details>

至此，你的自动续期容器就跑起来了，执行`ls -a`后你就可以看到在你的当前目录下，有一个`.env`文件和一个`logs`目录，`logs`目录里面存放的是程序日志，
而`.env`则是配置文件，现在直接执行`vim .env`将`.env`文件里的所有配置项改为你自己的并保存即可。然后重启容器，如果配置正确的话，便很快可以收到相关邮件。

<details>
    <summary>点我查看 .env 文件中部分配置项的含义</summary>
<br>

| 变量名 | 含义 | 默认值 | 是否必须 | 备注 |
| :---: | :---: | :---: | :---: | :---: |
| FREENOM_USERNAME | Freenom 账户 | - | 是 | 只支持邮箱账户，如果你是使用第三方社交账户登录的用户，请在 Freenom 管理页面绑定邮箱，绑定后即可使用邮箱账户登录 |
| FREENOM_PASSWORD | Freenom 密码 | - | 是 | 某些特殊字符可能需要转义，详见`.env`文件内注释 |
| MULTIPLE_ACCOUNTS | 多账户支持 | - | 否 | 多个账户和密码的格式必须是“`<账户1>@<密码1>\|<账户2>@<密码2>\|<账户3>@<密码3>`”，注意不要省略“<>”符号，否则无法正确匹配。如果设置了多账户，上面的`FREENOM_USERNAME`和`FREENOM_PASSWORD`可不设置 |
| MAIL_USERNAME | 机器人邮箱账户 | - | 是 | 支持`Gmail`、`QQ邮箱`以及`163邮箱`，尽可能使用`163邮箱`或者`QQ邮箱`而非`Gmail`。因为谷歌的安全机制，每次在新设备登录 `Gmail` 都会先被限制，需要手动解除限制才行。具体的配置方法参考「 [配置发信邮箱](#--配置发信邮箱) 」 |
| MAIL_PASSWORD | 机器人邮箱密码 | - | 是 | `Gmail`填密码，`QQ邮箱`或`163邮箱`填授权码 |
| TO | 接收通知的邮箱 | - | 是 | 你自己最常用的邮箱，推荐使用`QQ邮箱`，用来接收机器人邮箱发出的域名相关邮件 |
| MAIL_ENABLE | 是否启用邮件推送功能 | true | 否 | `true`：启用<br>`false`：不启用<br>默认启用，如果设为`false`，不启用邮件推送功能，则上面的`MAIL_USERNAME`、`MAIL_PASSWORD`、`TO`变量变为非必须，可不设置 |
| TELEGRAM_CHAT_ID | 你的`chat_id` | - | 否 | 通过发送`/start`给`@userinfobot`可以获取自己的`id` |
| TELEGRAM_BOT_TOKEN | 你的`Telegram bot`的`token` | - | 否 ||
| TELEGRAM_BOT_ENABLE | 是否启用`Telegram Bot`推送功能 | false | 否 | `true`：启用<br>`false`：不启用<br>默认不启用，如果设为`true`，则必须设置上面的`TELEGRAM_CHAT_ID`和`TELEGRAM_BOT_TOKEN`变量 |
| NOTICE_FREQ | 通知频率 | 1 | 否 | `0`：仅当有续期操作的时候<br>`1`：每次执行 |

*更多配置项含义，请参考`.env`文件中的注释。*

</details>

> 如何验证你的配置是否正确呢？
>

修改并保存`.env`文件后，执行`docker restart freenom`重启容器，等待 5 秒钟左右，然后执行`docker logs freenom`查看输出内容，
观察输出内容中有`执行成功`字样，则表示配置无误。如果你还来不及配置送信邮箱等内容，可先停用邮件功能。

##### 2.2 后期容器处理常用命令

查看容器在线状态及大小
```shell
docker ps -as
```

查看容器的运行输出日志
```shell
docker logs freenom
```

重新启动容器
```shell
docker restart freenom
```

停止容器的运行
```shell
docker stop freenom
```

移除容器
```shell
docker rm $name
```

查看 docker 容器占用 CPU，内存等信息
```shell
docker stats --no-stream
```

*有关容器部署的内容结束。*

### 🕹  方式二：通过腾讯云函数（SCF）部署

<hr>

#### 1、下载 SCF 版本的压缩包

此版本为特别版，支持通过腾讯云函数部署，与主分支版本不兼容，版本号为`v0.3_scf`，下载地址：
[https://github.com/luolongfei/freenom/archive/refs/tags/v0.3_scf.zip](https://github.com/luolongfei/freenom/archive/refs/tags/v0.3_scf.zip)

下载后解压到你能找到的任意目录，你将得到一个文件夹，后期将通过文件夹的形式上传到腾讯云函数。

#### 2、创建腾讯云函数

直接访问腾讯云函数控制台创建云函数： [https://console.cloud.tencent.com/scf/list-create](https://console.cloud.tencent.com/scf/list-create) ，
按照下图所示的说明进行创建。如果无法看清图片，可访问： [https://github.com/luolongfei/freenom/blob/master/resources/screenshot/scf.png](https://github.com/luolongfei/freenom/blob/master/resources/screenshot/scf.png) 
或者 [https://z3.ax1x.com/2021/06/01/2nKCF0.png](https://z3.ax1x.com/2021/06/01/2nKCF0.png) 查看原图。 

[![scf01](https://z3.ax1x.com/2021/06/01/2nKCF0.png)](https://imgtu.com/i/2nKCF0)

按照上图所示部署完成后，可以点击云函数的名称进入云函数管理画面，管理画面往下翻可看到`部署`与`测试`按钮，点击`测试`，稍等几秒钟，即可看到输出日志，
根据输出日志判断配置以及部署是否正确。

[![scf02](https://z3.ax1x.com/2021/06/01/2nGZ3q.png)](https://imgtu.com/i/2nGZ3q)

*有关腾讯云函数部署的内容结束。*

### 🚧  方式三：直接拉取源码部署

<hr>

所有操作均在Centos7系统下进行，其它Linux发行版大同小异
#### 1、获取源码
创建文件夹
```shell script
mkdir -p /data/wwwroot/freenom && cd /data/wwwroot/freenom
```
clone 本仓库源码
```shell script
git clone https://github.com/luolongfei/freenom.git ./
```

#### 2、修改配置
复制配置文件模板
```shell script
cp .env.example .env
```
编辑配置文件
```shell script
vim .env
```
```shell script
# 注意事项
# .env 文件里每个项目都有详细的说明，这里不再赘述，简言之，你需要把里面所有项都改成你自己的。需要注意的是多账户配置的格式：
# e.g. MULTIPLE_ACCOUNTS='<账户1>@<密码1>|<账户2>@<密码2>|<账户3>@<密码3>'
# （注意不要省略“<>”符号，否则无法正确匹配）
# 当然，若你只有单个账户，只配置 FREENOM_USERNAME 和 FREENOM_PASSWORD 就够了，单账户和多账户的配置会被合并在一起读取并去重。

# 编辑完成后，按“Esc”回到命令模式，输入“:wq”回车即保存并退出，不会用 vim 编辑器的可以谷歌一下:)
```

#### 3、添加计划任务

##### 3.1 安装 crontabs 以及 cronie
```shell script
yum -y install cronie crontabs
```
验证 crond 是否安装及启动
```shell script
yum list cronie && systemctl status crond
```
验证crontab是否安装
```shell script
yum list crontabs $$ which crontab && crontab -l
```

##### 3.2 打开任务表单，并编辑
```shell script
crontab -e
```
```shell script
# 任务内容如下
# 此任务的含义是在每天早上 9点 执行 /data/wwwroot/freenom/ 路径下的 run 文件，最佳实践是将这个时间修改为一个非整点的时间，防止与很多人在同一时间进行续期操作导致 freenom 无法稳定提供服务
# 注意：某些情况下，crontab 可能找不到你的 php 路径，下面的命令执行后会在 freenom_crontab.log 文件输出错误信息，你应该指定 php 路径：把下面的 php 替换为 /usr/local/php/bin/php （根据实际情况，执行 whereis php 即可看到 php 执行文件的真实路径）
00 09 * * * cd /data/wwwroot/freenom/ && php run > freenom_crontab.log 2>&1
```

##### 3.3 重启crond守护进程（每次编辑任务表单后都需此步，以使任务生效）
```shell script
systemctl restart crond
```
若要检查`计划任务`是否正常，你可以将上面的任务执行时间设置在几分钟后，然后等到任务执行完成，
检查`/data/wwwroot/freenom/`目录下的`freenom_crontab.log`文件内容，是否有报错信息。常见的错误信息如下：
- /bin/sh: php: command not found
- /bin/sh: /usr/local/php: Is a directory

*（点击即可展开或收起）*
<details>
    <summary>解决方案</summary>
<br>

>
> 执行
> ```shell script
> whereis php
> ```
> ```shell script
> # 上面的命令可确定 php 执行文件的位置，一般输出为“php: /usr/local/php /usr/local/php/bin/php”，选长的那个即：/usr/local/php/bin/php
> ```
> 
> 现在我们知道 php 执行文件的路径是`/usr/local/php/bin/php`（根据你自己系统的实际情况，可能不同），然后修改表单任务里的命令，把
> 
> `00 09 * * * cd /data/wwwroot/freenom/ && php run > freenom_crontab.log 2>&1`
> 
> 改为
> 
> `00 09 * * * cd /data/wwwroot/freenom/ && /usr/local/php/bin/php run > freenom_crontab.log 2>&1`
> 
> 更多参考：[点这里](https://stackoverflow.com/questions/7397469/why-is-crontab-not-executing-my-php-script)
>

</details>

当然，如果你的`计划任务`能正确找到`php路径`，没有错误，那你什么也不用做。

*至此，所有的配置都已经完成，下面我们验证一下整个流程是否走通。*

##### 3.4 验证
你可以先将`.env`中的`NOTICE_FREQ`的值改为1（即每次执行都推送通知），然后执行
```shell script
cd /data/wwwroot/freenom/ && php run
```
不出意外的话，你将收到一封关于域名情况的邮件。

***

遇到任何问题或 Bug 欢迎提 [issue](https://github.com/luolongfei/freenom/issues) （请按模板格式提`issue`，以便我快速复现你的问题，否则问题会被忽略），
如果`Freenom`改变算法导致此项目失效，请提 [issue](https://github.com/luolongfei/freenom/issues) 告知，我会及时修复，本项目长期维护。
欢迎`star`~

### 📋  捐赠名单 Donate List
非常感谢「 [这些用户](https://github.com/luolongfei/freenom/wiki/Donate-List) 」对本项目的捐赠支持！

### ❤  捐赠 Donate
如果你觉得本项目真的有帮助到你并且想回馈作者，感谢你的捐赠。
#### PayPal: [https://www.paypal.me/mybsdc](https://www.paypal.me/mybsdc)
> Every time you spend money, you're casting a vote for the kind of world you want. -- Anna Lappe

![pay](https://s2.ax1x.com/2020/01/31/1394at.png "Donate")

![每一次你花的钱都是在为你想要的世界投票。](https://s2.ax1x.com/2020/01/31/13P8cF.jpg)

**你的 star 或者`小额打赏`是我长期维护此项目的动力所在，由衷感谢每一位支持者，“每一次你花的钱都是在为你想要的世界投票”。
另外，将本项目推荐给更多的人，也是一种支持的方式，用的人越多更新的动力越足。**

### 🚁  我正在用的 VPS

走我的 Aff 地址购买，我可以获得一点返利，也算是一种支持方式，介意者复制官网地址访问即可。

| 名称 | 购买地址 | 备注 |
| :---: | :--- | :--- |
| 搬瓦工 | [https://bwh81.net/aff.php?aff=24499&pid=104](https://bwh81.net/aff.php?aff=24499&pid=104) （日本软银 VPS 限量版，`65美元`一年，优惠码：`BWH3HYATVBJW`） <br> [https://bwh81.net/aff.php?aff=24499&pid=94](https://bwh81.net/aff.php?aff=24499&pid=94) （CN2 GIA LIMITED EDITION，`DC 6`机房，`46.8美元`一年） <br> [https://bwh81.net/aff.php?aff=24499&pid=71](https://bwh81.net/aff.php?aff=24499&pid=71) （CN2 GIA 丐版，`DC 9`机房，`37.79美元`一年） | 稳定大厂，它们家`限量版 GIA`很香。目前是我的主力机型。 |
| Vultr | [https://www.vultr.com/?ref=7429134](https://www.vultr.com/?ref=7429134) （最低`2.5美元`每月） <br> [https://www.vultr.com/?ref=8399703-6G](https://www.vultr.com/?ref=8399703-6G) （新用户可得`100美元`体验金） | 随开随停，很方便。 |
| PacificRack | [https://pacificrack.com/portal/aff.php?aff=1150&pid=11](https://pacificrack.com/portal/aff.php?aff=1150&pid=11) （`9.9美元`一年） | 最便宜的机型`9.9美元`一年，QuadraNet 机房，我用了两年了目前感觉很稳。 |

### 🍺  信仰

![南京市民李先生](https://s2.ax1x.com/2020/02/04/1Bm3Ps.jpg "南京市民李先生")
> 
> 认真是我们参与这个社会的方式，认真是我们改变这个社会的方式。  ——李志

### 🌚  作者
- 主程序以及框架：[@luolongfei](https://github.com/luolongfei)
- 英文版文档：[@肖阿姨](#)

### 📰  更新日志

此处省略了很多较为久远的记录，以前的日志只记录了比较大的变更，以后的日志会尽可能详尽一些。

#### [Unreleased]

##### Added

- 支持通过 Server酱 以及 企业微信 推送通知

##### Changed

- 多个账户的续期结果通知合并为同一条消息
- 整合各种送信方式，优化相关逻辑
- 支持交互式安装，免去手动修改配置的繁琐操作

#### [v0.3](https://github.com/luolongfei/freenom/releases/tag/v0.3) - 2021-05-27

##### Added

- 追加 Docker 版本，支持通过 Docker 方式部署，简化部署流程

#### [v0.2.5](https://github.com/luolongfei/freenom/releases/tag/v0.2.5) - 2020-06-23

##### Added

- 支持在 Github Actions 上执行（应 GitHub 官方要求，已移除此功能）

#### [v0.2.2](https://github.com/luolongfei/freenom/releases/tag/v0.2.2) - 2020-02-06

##### Added

- 新增通过 Telegram bot 送信
- 各种送信方式支持单独开关

#### [v0.2](https://github.com/luolongfei/freenom/releases/tag/v0.2) - 2020-02-01

##### Added

- 支持多个 Freenom 账户进行域名续期

##### Changed

- 进行了彻底的重构，框架化
- 优化邮箱模块，支持自动选择合适的邮箱配置


*（版本在 v0.1 到 v0.2 期间代码有过很多次变更，之前没有发布版本，故此处不再赘述相关变更日志）*

#### [v0.1](https://github.com/luolongfei/freenom/releases/tag/v0.1) - 2018-8-13

##### Added

- 初版，开源，基础的续期功能

### 🎉  鸣谢
- [PHPMailer](https://github.com/PHPMailer/PHPMailer/) （邮件发送功能依赖此库）
- [guzzle](https://github.com/guzzle/guzzle) （Curl库）
- [秋水逸冰](https://teddysun.com/569.html) （本项目 Docker 相关文档有参考秋水逸冰的文章）

### 🥝  开源协议
[MIT](https://opensource.org/licenses/mit-license.php)
