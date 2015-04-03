## lamp stack in ubuntu via apt-get
```bash
sudo apt-get update
sudo apt-get install lamp-server^
```
## clone a repo example:
`git clone user@host:/path/to/repo`
## remotely adding ssh-key 
`ssh-copy-id -i ~/.ssh/id_rsa.pub user@host`
###### with different port than 22
`ssh-copy-id -i ~/.ssh/id_rsa.pub "user@host -p 48222"`
## when ssh-copy-id doesnt work, force it
`cat /root/.ssh/id_rsa.pub | ssh user@host 'cat > /root/.ssh/authorized_keys'`

also look in:
- cat /root/.ssh/id_rsa
- cat /root/.ssh/id_rsa.pub

## importing functions
```bash
for file in functions/* ; do
  if [ -f "$file" ] ; then
    . "$file"
  fi
done
```
## when git doesnt work
`rsync -azvP dir_name user@host:/path/to/repo`

## installing git flow
`apt-get install git-flow`
##git multiple results error
`git config --global --get-all user.name` 

## appending textfile to an existing file on a remote location
```bash
rsync -az path/config -e "ssh -p gitport" user@host:path/temp_config.txt
ssh user@host "cat path/temp_config.txt >> path/config"
ssh user@host "rm path/config/temp_config.txt"
```

## static ip address toekennen
sudo ifconfig eth1 192.168.1.136 netmask 255.255.255.0

## interface up forcen
`ifup eth0`

## ssh probleem
`tracepath ip`

## MySQL database commands
- `mysql --database=dbname --host=localhost --user=usr --password=pw`
- `DROP DATABASE dbname`
- `DROP USER 'user'@'localhost'`

## Deploying SSL keys
protect a key with a passphrase
`openssl rsa -des -in insecure.key -out secure.key`

Reverse it with
`openssl rsa -in secure.key -out insecure.key -passin pass:{your_pass_phrase_here}`

## Configuring a wireless router via DD WRT gui
- setup1 dissable
- DNS: 192.168.1.x
- WAN PORT enable
- DHCP: forward
- local ip: 192.168.1.x

wireless
- AP: mixed
- SSID: name_of_the_network
- bridged: enabled (unbriged will make WLAN & lan seperate vlans and a wpc wont see pc's)
- security WPA2PM
- TKIP + EAS
- pw: ***********
- 3600

dissable firewall

bridged: WLAN to LAN. Unbridged: seperate VLAN

dnsmasq: local DNS server for the network. Forwards querys upstream. DHCP intergrates with the DNS server and allows local machines with DHCP allocated addresses to appear in the DNS

##removing something from the start or end of a variable
```
path=/path/to/file/drive/file/path/
echo ${path#/path/to/file/drive/}
```
The #.. part strips off a leading matching string when the variable is expanded

You can strip matching strings (e.g., an extension) from the end of a variable using %...
```
path=/path/to/file/drive/file/path/
echo ${path%/file/path/}
```

##display error logs
example:
`tail -f /var/log/apache2/error.log`

##get root acces on a vagrant box
`sudo su -`

| Command | Description |
| ------- | ------ |
| $? |  Expands to the exit status of the most recently executed foreground pipeline |
| ${!een_variabele} | verwijst naar de waarde in een_variabele|
| set -x | bij het debuggen van scripts |
| bash -x | ook usefull bij debugging |
| tee | splits output naar een extra file bijvoorbeeld debug.log |
| less | less is more (for opening a file) |
| drush cc drush | in docroot clear cache |
| grep ^name | het dakje verankerd "name" zodat alleen maar de instanties die beginnen met "name" worden opgehaalt |
| grep name$ | zelfde als ^ maar dan voor achteraan de regel |

