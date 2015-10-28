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
`cat /root/.ssh/id_rsa.pub | ssh user@host 'cat >> /root/.ssh/authorized_keys'`

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

## Using nmap to scan all your open ports
This command will scan all of your local IP range (assuming your in the 192.168.1.0-254 range), and will perform service identification (-sV) and will scan all ports (-p 1-65535).
`nmap -sV -p 1-65535 192.168.1.1/24`

## postfix mail testen
`drush php-eval "print mail('bruno@dropsolid.com','Test subject from drush','Test message','From: drush@exampledrupalsite.com');"`
in /var/www/dynacodoor.com/docroot

## Give a dev permission to git clone
`usermod -a -G projectname devname`

## create ansible user password
`mkpasswd --method=SHA-512 'password'`

## install drush 7.0 with composer
first run
`composer global require drush/drush:dev-master`
then add `export PATH="$HOME/.composer/vendor/bin:$PATH"`
at the end of your /root/bash.bashrc file

## ansible debugging
`msg: failed to checksum remote file. Checksum error code: 3`
add trailing slash to destination

## Script debugging
Perl warning:
- `locale-gen en_US en_US.UTF-8 hu_HU hu_HU.UTF-8`
- `dpkg-reconfigure locales`

## Remove break lines in sublime text
- Replace with Ctrl+H
- Make sure regular expression are enabled alt+R
- Find what: `^\n`
- Replace With: (nothing, leave in blank)

## Run an Ansible playbook using a parallelism level of 10
- `ansible-playbook testplatform.yml -f 10 --extra-vars "@host_vars/jenrepo.yml"`

## Mount folder/filesystem through SSH
- `sshfs name@server:/path/to/folder /path/to/mount/point`

## Compare a remote file with a local file
- `ssh user@host cat /path/to/remotefile | diff /path/to/localfile -`

## stopwatch
- `time read (ctrl-d to stop)`

## Add repo to gitlab
`git remote add gitlab git@gitlab.com:GROEPNAAM/PROJECTNAAM.git`

`git push gitlab master`

## List directories 2 levels deep
`tree -d -L 2`

## find all git folders and remove them
`( find . -type d -name ".git" \`
  `&& find . -name ".gitignore" \`
 ` && find . -name ".gitmodules" ) | xargs rm -rf`

## rsync only folders
`rsync -av -f"+ */" -f"- *" /path/to/apache/logs/ root@www433.nixcraft.net.in:/path/to/apache/logs/`

## Git revert to a specific commit
`git revert 3d5575f8e4c97ddab8ad5d540fee4664c04db75d`

## Git make a new tag
first commit the changes then
`git tag 7.x-1.12`

## Remove a git tag from remote
`git tag -d 12345`
`git push origin :refs/tags/12345`

## Add to the end of the url to login to a new drupal site

`http://www.your-website-name.com/?q=user/login`

## drupal drush file sync

`drush core-rsync @project.staging:%files @project.local:%files`

## grabbing a remote db and pulling it locally

`ssh remoteserver "mysqldump -uuser -ppw project_staging" | mysql -uuser -ppw project_local`

## open a file with nano starting at a certain line

`nano +115 filename`

## Drop or truncate a mysql database
This will drop every table

`mysql -Nse 'show tables' DATABASE_NAME | while read table; do mysql -e "drop table $table" DATABASE_NAME; done`

this will truncate every table

`mysql -Nse 'show tables' DATABASE_NAME | while read table; do mysql -e "truncate table $table" DATABASE_NAME; done`

## Sed dry run

`sed 's#WORDTOREPLACE#REPLACEWITH#g' /path/to/file.sh`

## Sed replace one word with another

`sed -i 's#WORDTOREPLACE#REPLACEWITH#g' /path/to/file.sh`

## Iptables

```
iptables -L
iptables-save > /opt/iptables.tmp
nano /opt/iptables.tmp #make changes here
iptables-restore < /opt/iptables.tmp
```

## Send a test mail

`sendmail -t  < $dev.email`

## Useful docker commands

```
docker exec -it some-mysql bash
docker logs some-mysql
docker inspect some-mysql | grep IPAddress
```

## DigitalOcean list with images

`curl -X GET "https://api.digitalocean.com/v2/images?page=3" -H "Authorization: Bearer $TOKEN" | python -mjson.tool | less`

## Various useful commands

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
| ctrl-x e | Rapidly invoke an editor to write a long, complex, or tricky command |
| ctrl-l | Clear the terminal screen |
