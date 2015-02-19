## remotely adding ssh-key 
`ssh-copy-id -i ~/.ssh/id_rsa.pub root@192.168.0.186`
### with different port than 22
`ssh-copy-id -i ~/.ssh/id_rsa.pub "root@192.168.0.104 -p 48222"`
