## lamp stack in ubuntu via apt-get
```bash
sudo apt-get update
sudo apt-get install lamp-server^
```
## clone a repo from hera exaple:
`git clone user@host:/path/to/repo`
## remotely adding ssh-key 
`ssh-copy-id -i ~/.ssh/id_rsa.pub user@host`
###### with different port than 22
`ssh-copy-id -i ~/.ssh/id_rsa.pub "root@192.168.0.104 -p 48222"`
## importing functions
```bash
for file in functions/* ; do
  if [ -f "$file" ] ; then
    . "$file"
  fi
done
```
## when git doesnt work
`rsync -azvP takeover-site user@host:/path/to/repo`

## installing git flow
`apt-get install git-flow`
##git multiple results error
`git config --global --get-all user.name` 

## appending textfile to an existing file
```bash
rsync -az etc/config/config -e "ssh -p $git_ssh_port" user@host:$checkout/config/temp_config.txt
ssh user@host "cat $checkout/config/temp_config.txt >> $checkout/config/config"
ssh user@host $git_ssh_user $git_host $git_ssh_port "rm $checkout/config/temp_config.txt"
```

| Command | Description |
| ------- | ------ |
| $? |  Expands to the exit status of the most recently executed foreground pipeline |
| ${!een_variabele} | verwijst naar de waarde in een_variabele|
| set -x | bij het debuggen van scripts |
| bash -x | ook usefull bij debugging |
| tee | splits output naar een extra file bijvoorbeeld debug.log |
| less | less is more (for opening a file) |

