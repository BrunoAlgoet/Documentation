#Samba troubleshooting checklist
## Testing network connectivity

* Check your cabling (virtualbox settings)
* Check IP-address: `ip a`
* Check routing: `ip route`
* Check the DNS-server: `cat /etc/resolv.conf`
* Ping the server's IP address and loopback address (127.0.0.1)
* Ping the client's IP address
* Ping the client using its DNS name
* Telnet to all the IP addresses on the server on port 139
* Check if the service is running and the ports are open: 
  - `sudo systemctl status smbd.service`
  - `sudo ss -tulpn`
  - `sudo ps -ef`
* Check the log files for error messages: `journalctl -b -u smb.service`
* Test local connection `wget http://localhost/`
* Test remote connection `sudo nmap -sS -p 80`
* Check the presence of a firewall running on either the server or client.
  - `sudo firewall-cmd --list-all`
  - `sudo iptables -L -n -v`

## Testing Samba Client / Server Connectivity

1. Check all the shares available on the network
   ```bash
   smbclient -l samba_server
   ```
   Check your SWAT configuration for invalid hosts allow, hosts deny and invalid users entries.
   Failure of this test may mean that Samba isn't running on the server at all and may need to be started.

2. Determine if the samba software is running correctly
   ```bash
   nmblookup -B samba-server-IP-address _SAMBA_
   ```
   This should return the server's IP address if is running correctly.

3. Determine whether the client is accepting Samba queries
   ```bash
    nmblookup -B client-IP-address "*"
    ```
   This should return the client's IP address if is running correctly. 
   If the test fails, check to see whether the client is running firewall software that could prevent communication. 
   Another source of the problem could be that the "Client for Microsoft Windows" or "File and Printer Sharing for Microsoft    Networks" settings on the client's NIC card haven't been selected. 

4. Broadcast a query message to the network, this returns answers from all locally connected clients and servers.
   ```bash
   nmblookup -d 2 "*"
   ```
   The test fails because either your client or server has an incorrect subnet mask configured on their NIC cards.

5. Test a command-line login to the Samba server
   ```bash
    smbclient //samba-server/tmp
    ```
   When prompted for a password, use the Linux password of the account with which you logged in. 
   A message that warns of an invalid or bad network name could mean that the tmp service on the Samba server isn't correctly    configured.
   Messages related to bad passwords could mean that the user's account doesn't exist, that their smbpasswd wasn't created,     or that the password entered is incorrect.

6. Check the permitions in the configuration
   ```bash
   sudo vi /etc/samba/smb.conf
   ```

7. Check the SELinux settings
   ```bash
   sestatus
   getsebool -a |grep samba
   ```
   Check if these are enabled: samba_export_all_rw, allow_smbd_anon_write, allow_httpd_anon_write, samba_enable_home_dirs

[used source: linuxhomenetworking](http://www.linuxhomenetworking.com/wiki/index.php/Quick_HOWTO_:_Ch12_:_Samba_Security_and_Troubleshooting#.VHd_GjHF-9I)
[used source: samba.org](https://www.samba.org/samba/docs/using_samba/ch09.html)
