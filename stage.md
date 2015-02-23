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
## installing git flow
`apt-get install git-flow`
##git multiple results error
`git config --global --get-all user.name` 

| Command | Description |
| ------- | ------ |
| $? |  Expands to the exit status of the most recently executed foreground pipeline |
| ${!een_variabele} | verwijst naar de waarde in een_variabele|
| set -x | bij het debuggen van scripts |
| bash -x | ook usefull bij debugging |
| tee | splits output naar een extra file bijvoorbeeld debug.log |

