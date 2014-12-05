# Laboverslag opdracht 06: dhcp
=============================

### Opdracht omschrijving
-------------------------
Zet een DHCP-server op voor het private netwerk zoals beschreven in de DNS-opgave (IP 172.16.0.0/16). De configuratie
gebeurt (uiteraard) als een Ansible-rol met een template waarin â€œhard-codedâ€ waarden zoveel mogelijk vervangen zijn door
variabelen die ingevuld worden a.h.v. host_vars. Volgende functionaliteiten worden verwacht:
* Standaardinstellingen voor client-pcâ€™s opgeven, zoals subnetmasker, DNS-server, DNS-domein en default gateway
* Een subnet-declaratie opstellen, incl. specifieke instellingen voor client-pcâ€™s (idem als vorig punt)
* Een adres-pool definiÃ«ren
* Duur van een adreslease instellen

### Deliverables
-----------------

* Labo-verslag met
	â€“ Link naar jullie Bitbucket-repository
	â€“ Toelichting van de gekozen aanpak: welke stappen heb je ondernomen? Hoe heb je het resultaat getest?
	â€“ Gebruikte bronnen voor het uitwerken van de opdracht
* Demo
	â€“ Toon het resultaat van de acceptatietest (zoals hierboven beschreven)
	â€“ Toon de DHCP-configuratie op de server
	â€“ Toon je Ansible playbook en configuratie-template


### Hoe we tewerk zijn gegaan:
-----------------------------
1. Maak een nieuwe rol aan voor dhcp door een mappestructuur te creeren in roles met daarin de mappen: tasks, templates en handlers
2. Creer in task een main.yml file waarin je de dhcp-taken zet om de service te installeren en aan te zetten en de dhcpd.conf file als template op de server te zetten.
3. In de map handlers creeÃ«r je main.yml waarin je handlers zet voor je tasks. Wij gebruiken hier "restart dhcp"
4. Maak een host_vars map aan en declareer de variabelen uit je tasks/main.yml
5. Creer de files voor de dhcpd.config.j2 (algemene template voor dhcpconfiguratie) de map templates
6. Vul aan de hand van het dhcpd.conf.j2 bestand de hostvars voor de dhcpserver aan:
		* dhcp_subnets
		* dhcp_hosts



### Bronnen
------------
* https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Networking_Guide/sec-dhcp-configuring-server.html
* https://github.com/debops/ansible-dhcpd/blob/master/templates/etc/dhcp/dhcpd.conf.j2
* https://github.com/pdellaert/dhcp_server/blob/master/templates/dhcpd.conf.j2
* https://github.com/pdellaert/dhcp_server
* https://github.com/pdellaert/dhcp_server/blob/master/defaults/main.yml
* https://github.com/aaron868/management/blob/master/group_vars/all.yml
* https://galaxy.ansible.com/list#/roles/3


### Testen en Eindresultaat
------------------

* Geslaagde test:

- Via dynamisch dhcp:

![ViaDHCP](http://i.imgur.com/nC4BJMM.png)

- Via static dhcp

![FixedIp](http://i.imgur.com/ud96Fas.png)
![FixedIp](http://i.imgur.com/6eFfvlc.png)
