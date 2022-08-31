1. install dhcp
```
$ yum install dhcp
```
2. Open the file `/etc/sysconfig/dhcpd`, add the name of the specific interface to the list of DHCPDARGS, for example if the interface is eth0, then add:
```
DHCPDARGS=eth0
```
3. copy the sample configuration file as the main configuration file
```
$ cp /usr/share/doc/dhcp-4.2.5/dhcpd.conf.example /etc/dhcp/dhcpd.conf 
```
4. edit file
```
$ vim /etc/dhcp/dhcpd.conf
```
```
option domain-name "tecmint.lan";
option domain-name-servers ns1.tecmint.lan, ns2.tecmint.lan;
default-lease-time 3600; 
max-lease-time 7200;
authoritative;

subnet 192.168.56.0 netmask 255.255.255.0 {
        option routers                  192.168.56.1;
        option subnet-mask              255.255.255.0;
        option domain-search            "tecmint.lan";
        option domain-name-servers      192.168.56.1;
        range   192.168.56.10   192.168.56.100;
        range   192.168.56.120  192.168.56.200;
}
```
for static allocation
```
host ubuntu-node {
	 hardware  ethernet 00:f0:m4:6y:89:0g;
	 fixed-address 192.168.56.105;
 }

5. start and enable service
```
$ systemctl enable --now dhcpd
```
