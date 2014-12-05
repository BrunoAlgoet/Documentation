#Cheatsheet

##General
---------
| Command | Description |
| ------- | ------ |
| clip < / "path" |  copy from file |
| ${een_variabele} | |
| $(een_commando) | |
| $? | effectieve resultaat weergeven |
| [ -n ] | een logische expressie / -n is testen of iets NIET leeg is. Vb: [ -n "${result}"] |
| !! | run command |
| dos2unix | Win to Unix   |
| sudo loadkeys be-latin7 | keyboard to azerty |
| ip a | = ifconfig |
| /etc/sysconfig/network-scripts/ifcfg-ADAPTERNAAM | Networkconfigfile |
| ss | socket statistics (filter t,u for tcp or udp) |
| Services: | ---------------------- |
| sudo systemctl status "naamservice" | check service |
| firewall: | ---------------------- |
| sudo firewall-cmd --list-all| show firewall config |
| iptables| software for firewall config |
| logs: | ---------------------- |
| sudo journalctl -u "servicename".service | journallog for certain service |
| sudo journalctl -xn | last journal events |
| journalctl -b -u smb.service | journal errors |

##SSH
---------
| Command | Description |
| ------- | ------ |
| https://help.github.com/articles/generating-ssh-keys/ | (=> useful link) |
| git clone git@github.com:GielDeBleser/Documentation.git | (=> clone with ssh) |

 if error at ssh-add ~/.ssh/id_rsa  -----> eval $(ssh-agent)


##Vagrant
---------

| Command | Description |
| ------- | ------ |
| vagrant up | bring vagrant box up / if needed ex; srv001 |
| vagrant halt | pauze vagrant box |
| vagrant destroy -f | vernietig vagrant box |
| vagrant ssh | ssh connection into vagrant box |
| vagrant status | shows running/stopped/destroyed vm's |

###Bats
| Command | Description |
| ------- | ------ |
| sudo yum install dos2unix | install dos2Unix |
| dos2unix runbats.sh | convert file from Windows to Unix|
| sudo bats/libexec/bats folderofbatsfile/batsfile.bats | run specific batsfile  |

##Markdown
---------
| Syntax | Description |
| ------- | ------ |
| [x] | "space"[x]"space" |
| [ ] | "space"["space"]"space" |
 
###Dns testing
---------
| Command | Description |
| ------- | ------ |
| systemctl status named | show status of named service |
| host 192.0.2.2 pu001 | Configure host by ip |
| host pu001 linuxlab.net | Configure host by name |
| sudo named checkconf | get checkconfiguration of named service |
| sudo named checkzone | get checkzone of named service |
| logs: | ---------------- |
| sudo journalctl -f -u named.service | journallog of named service |
| /etc/resolv.conf | dnsconfig-file |


##Trouble shoot tips
---------
- osi layer: From down to up
  * [5] Applicatie
  * [4] Transport
  * [3] Intranet
  * [2] Datalink
  * [1] Fys
