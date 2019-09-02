## Setting up single sign-on with ADFS and SAML 

Updating the SSL certificate of the ADFS also means that the SAML federation metadata gets updated with the new certificate signature, and need to be imported in simplesaml

## Get authenticated cURL from your browser
```
chrome console -> network -> copy -> copy all as cURL
```

## Printer issue 

We had a situation where the DHCP handed out 192.168.0.255 to someone over wireless and it prevented this person from accessing the printers. When manually switching the IP address to another one, everything worked as expected.

## Fix borken screen
```
sudo service lightdm restart
For gnome you hit Alt + F2 and in the dialog enter r and Enter
```
## Setup ssh tunnel (solr admin)

`ssh -L localhost:8080:127.0.0.1:8983 user@hostname -N -C`

## Generate ssh-key 
`ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`

## remotely adding ssh-key 
`ssh-copy-id -i ~/.ssh/id_rsa.pub user@host`
###### with different port than 22
`ssh-copy-id -i ~/.ssh/id_rsa.pub "user@host -p 48222"`
## when ssh-copy-id doesnt work, force it
`cat /root/.ssh/id_rsa.pub | ssh user@host 'cat >> /root/.ssh/authorized_keys'`

also look in:
- cat /root/.ssh/id_rsa
- cat /root/.ssh/id_rsa.pub

## importing bash functions
```bash
for file in functions/* ; do
  if [ -f "$file" ] ; then
    . "$file"
  fi
done
```
## show the history changes of a file
`git log -p filename`

## appending textfile to an existing file on a remote location
```bash
rsync -az path/config -e "ssh -p gitport" user@host:path/temp_config.txt
ssh user@host "cat path/temp_config.txt >> path/config"
ssh user@host "rm path/config/temp_config.txt"
```

## wierd redirect in Drupal that is not in the redirect module or htaccess

devel module aanzetten en naar variable editor gaan in drupal. Daar een search doen. path:
url.com/devel/variable/edit

## ssh probleem
`tracepath ip`

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

##get root acces on a vagrant box
`sudo su -`

## Using nmap to scan all your open ports
This command will scan all of your local IP range (assuming your in the 192.168.1.0-254 range), and will perform service identification (-sV) and will scan all ports (-p 1-65535).
`nmap -sV -p 1-65535 192.168.1.1/24`

## postfix mail testen
`drush php-eval "print mail('bruno@dropsolid.com','Test subject from drush','Test message','From: drush@exampledrupalsite.com');"`
in docroot

```
Via Telnet:
telnet localhost 25
ehlo localhost
mail from: username@example.com
rcpt to: example@mail.com
data
Subject: My Telnet Test Email
```

## Add user to a group
`usermod -a -G projectname devname`

## create ansible user password
`mkpasswd --method=SHA-512 'password'`

## install drush 7.0 with composer
first run
`composer global require drush/drush:dev-master`
then add `export PATH="$HOME/.composer/vendor/bin:$PATH"`
at the end of your /root/.bashrc file

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

## Mount folder/filesystem through SSH
- `sshfs name@server:/path/to/folder /path/to/mount/point`

## Compare a remote file with a local file
- `ssh user@host cat /path/to/remotefile | diff /path/to/localfile -`

## stopwatch
- `time read (ctrl-d to stop)`

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

## Switch to a different branch which you do not have locally
```
git fetch gitlab hera
git checkout -t gitlab/hera
```

## Jenkins build bootstrap error spam
Voeg volgend lijntje toe aan docroot/sites/default/settings.php
`include DRUPAL_ROOT . '/sites/all/modules/contrib/domain/settings.inc';`

## Php test mail
```php
<?php 
    ini_set( 'display_errors', 1 );
    error_reporting( E_ALL );
    $from = "infra@dropsolid.com";
    $to = "bruno@dropsolid.com";
    $subject = "PHP Mail Test script";
    $message = "This is a test to check the PHP Mail functionality";
    $headers = "From:" . $from;
    mail($to,$subject,$message, $headers);
    echo "Test email sent";
?>

//run from terminal

php -r 'ini_set( 'display_errors', 1 ); error_reporting( E_ALL ); $from = "infra@dropsolid.com"; $to = "bruno@dropsolid.com"; $subject = "PHP Mail Test script"; $message = "This is a test to check the PHP Mail functionality"; $headers = "From:" . $from; mail($to,$subject,$message, $headers); echo "Test email sent";'
```
If this works but Drupal is still not sending mails, check if email reroute is not enable in Drupal.

## Decent Drupal errors instead of whitepage, add in settings.php
```
error_reporting(E_ALL);
ini_set('display_errors', TRUE);
ini_set('display_startup_errors', TRUE);
```
## ~/.bashrc settings
```bash
# Key bindings, up/down arrow searches through history
bind '"\e[A": history-search-backward'
bind '"\e[B": history-search-forward'
bind '"\eOA": history-search-backward'
bind '"\eOB": history-search-forward'

# Directory listing and file system
alias l='ls -l --si --time-style=long-iso'
alias la='ls -la --si --time-style=long-iso'
alias ll='ls -l  --si --time-style=long-iso'
alias lh='ls -lh  --si --time-style=long-iso'
```

## clear varnish
`ssh user@host  'curl -X BAN localhost'`

## Synchronize the System Clock
`apt-get install ntp ntpdate`

## domain name migratie: add in .htaccess as first rules in the rewite block, before Drupal can do anything internally

```bash
  RewriteCond %{HTTP_HOST} ^(www\.)?domain.com  [NC]
  RewriteRule ^ http://www.newdomain.com [R=301,L]
```

## making sure varnish is working

* inspect element -> network -> reload
* choose a random file
* check X-Cache-Hits variable is > 0
* run cron jobs on the site
* check if X-Cache-Hits is reset

## Checking varnish port

* check /etc/default/varnish for 
```
DAEMON_OPTS="-a :6081 \
             -T localhost:6082 \
```
* check if the port is open with netstat -tulpn
* check from the outside with nmap -PN IP -v
* check the firewall with iptables -L

## Journalctl
```bash
journalctl --list-boots
journalctl -b -1
```
showing journal entries for a user unit `journalctl --user-unit ssh-agent.service` 

instead of a system unit `journalctl --unit NetworkManager.service`

## drupal console
```bash
curl http://drupalconsole.com/installer -L -o drupal.phar
mv drupal.phar /usr/local/bin/drupal
chmod 777 /usr/local/bin/drupal
drupal list
```

## Drush alias problem checklist

does the user have the right permissions on the server
```bash
drush @project sql-conf
drush sa --with-db @project
```

## Drupal change max upload size

In de .htaccess van de site
```bash
<IfModule mod_php5.c>
...
php_value upload_max_filesize 10M
php_value post_max_size 20M
...
</IfModule>
```

## Drupal 8 settings file adjustments

```php
$settings[hash_salt] = '$ZELFDE_HASH_ALS_IN_DE_FILE';
$config_directories[CONFIG_SYNC_DIRECTORY] = 'config/sync';
$config_directories[CONFIG_STAGING_DIRECTORY] = 'config/staging';
```

van de directories nog een folder sync aanmaken

## backups intern

Git repo in srv, juiste checkout doen en dan rsync

```
rsync -azvPn --exclude=.git . /path/to/www/project
rsync -azvP --exclude=.git . /path/to/www/project
```
## list open files

lsof used in many Unix-like systems to report a list of all open files and the processes that opened them

## Symphony / php code in browser instead of the site

```
apt-get install libapache2-mod-php5
a2enmod php5
a2enmod rewrite
```

## htaccess with htpasswd to allow localhost and server ip

had to define custom error 401 reponse for the htaccess rules to work with Drupal

```
Order Deny,Allow
Deny from all
Allow from localhost
Allow from 178.208.33.158
Allow from 127.0.0.1
Satisfy Any
ErrorDocument 401 "Unauthorized"
```

## Redirect to content of different domain without changing the url

<noframes><p>Your user agent does not support frames or is currently configured not to display frames. However you may visit <a href="http://app4acc.iec-iab.be/">the page that was supposed to be here</a></p></noframes>

Header
X-Frame-Options:SAMEORIGIN

## 503 Bad gateway

Connections were being closed and not opened fast enough by Apache when logged in, this caused Varnish to fallback to error 503 on slow requests (because backend not responding)

Changed keepalive and connection reuse settings in apache and nginx to avoid this behaviour

Nginx
in /etc/nginx.conf
```
tcp_nodelay on;
keepalive_timeout 65;
```
apache
in /etc/apache2/apache2.conf
```
Timeout 300
KeepAlive Off
MaxKeepAliveRequests 100
KeepAliveTimeout 5
```
## Varnish cli cache clear/purge

2.x
```
varnishadm -T 127.0.0.1:6082 -S varnish_secret_file purge.url "url.tld"
```
3.x
```
varnishadm "ban req.http.host == url.tld"
```
## Varnish 503 Service unavailable error

FetchError   c Invalid Gzip data: incorrect header check
https://www.drupal.org/project/agrcache/issues/1464966


## Drupal sql mode fix

see https://www.drupal.org/files/issues/drupal-mysql57SupportBrokenDueToSQLModes-2545480-e641385.patch
```
$databases['default']['default'] ['init_commands'] = ['sql_mode' => "SET sql_mode = 'REAL_AS_FLOAT,PIPES_AS_CONCAT,ANSI_QUOTES,IGNORE_SPACE,STRICT_TRANS_TABLES,STRICT_ALL_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER'",];
```

## Sendgrid list mails per day

```
curl -s -X "GET" "https://api.sendgrid.com/v3/stats?start_date=2019-08-01&end_date=2019-08-30" -H "Authorization: Bearer ***KEY***" -H "Content-Type: application/json" | jq -r '.[] | [.date, .stats[].metrics.requests] | @tsv'
```

## Various useful commands

| Command | Description |
| ------- | ------ |
| $? |  Expands to the exit status of the most recently executed foreground pipeline |
| ${!een_variabele} | verwijst naar de waarde in een_variabele|
| set -x | bij het debuggen van scripts |
| bash -x | ook usefull bij debugging |
| tee | splits output naar een extra file bijvoorbeeld debug.log |
| grep ^name | het dakje verankerd "name" zodat alleen maar de instanties die beginnen met "name" worden opgehaalt |
| grep name$ | zelfde als ^ maar dan voor achteraan de regel |
| ctrl-x e | Rapidly invoke an editor to write a long, complex, or tricky command |
| ctrl-l | Clear the terminal screen |

## Troubleshooting high shared memory

```
du -aLh /proc/*/map_files/ /proc/*/fd/ | sort -h | tail -n 10
```
https://unix.stackexchange.com/questions/431982/what-could-be-using-6gb-of-my-swap
