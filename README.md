1. Install bind 
```
$ yum install bind bind-utils
```
2. add forward zone
```
$ cat /etc/named/zones/db.example.com
```
```
$TTL 1W
@	IN	SOA	ns1.example.com.	root (
			2019070700	; serial
			3H		; refresh (3 hours)
			30M		; retry (30 minutes)
			2W		; expiry (2 weeks)
			1W )		; minimum (1 week)
	IN	NS	ns1.example.com.
	IN	MX 10	smtp.example.com.
;
;
ns1.example.com.		IN	A	192.168.1.5
smtp.example.com.		IN	A	192.168.1.5
;
helper.example.com.		IN	A	192.168.1.5
helper.ocp4.example.com.	IN	A	192.168.1.5
;
api.ocp4.example.com.		IN	A	192.168.1.5 
api-int.ocp4.example.com.	IN	A	192.168.1.5 
;
*.apps.ocp4.example.com.	IN	A	192.168.1.5 
;
bootstrap.ocp4.example.com.	IN	A	192.168.1.96 
;
master0.ocp4.example.com.	IN	A	192.168.1.97 
master1.ocp4.example.com.	IN	A	192.168.1.98 
master2.ocp4.example.com.	IN	A	192.168.1.99 
;
worker0.ocp4.example.com.	IN	A	192.168.1.11 
worker1.ocp4.example.com.	IN	A	192.168.1.7 
;
```
3. Create reverse records
```
cat $ /etc/named/zones/reverse.example.com
```
```
$TTL 1W
@	IN	SOA	ns1.example.com.	root (
			2019070700	; serial
			3H		; refresh (3 hours)
			30M		; retry (30 minutes)
			2W		; expiry (2 weeks)
			1W )		; minimum (1 week)
	IN	NS	ns1.example.com.
;
5.1.168.192.in-addr.arpa.	IN	PTR	api.ocp4.example.com. 
5.1.168.192.in-addr.arpa.	IN	PTR	api-int.ocp4.example.com. 
;
96.1.168.192.in-addr.arpa.	IN	PTR	bootstrap.ocp4.example.com. 
;
97.1.168.192.in-addr.arpa.	IN	PTR	master0.ocp4.example.com. 
98.1.168.192.in-addr.arpa.	IN	PTR	master1.ocp4.example.com. 
99.1.168.192.in-addr.arpa.	IN	PTR	master2.ocp4.example.com. 
;
11.1.168.192.in-addr.arpa.	IN	PTR	worker0.ocp4.example.com. 
7.1.168.192.in-addr.arpa.	IN	PTR	worker1.ocp4.example.com. 
;
```
