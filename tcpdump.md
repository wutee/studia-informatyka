## Proste Protokoły Sieciowe

*ARP - Address Resolution Protocol*, pozwalający na tłumaczenie adresów IP na adresy MAC. Pamięć podręczna została wyczyszczona:
```
m3:~% sudo arp -da
194.29.146.3 (194.29.146.3) deleted 194.29.146.253 (194.29.146.253) deleted 194.29.146.27 (194.29.146.27) deleted 194.29.146.247 (194.29.146.247) deleted 194.29.146.16 (194.29.146.16) deleted
1
```
Następnie na dwóch konsolach tcpdump i ping:
```
m3:~% sudo tcpdump -i en0 arp
m3:~% ping -c 1 test103
PING test103.iem.pw.edu.pl (194.29.146.242): 56 data bytes
64 bytes from 194.29.146.242: icmp_seq=0 ttl=64 time=7.967 ms
```
Zgodnie z oczekiwaniami, tcpdump zarejestrował pytanie i odpowiedź:
```
12:56:23.793059 ARP, Request who-has test103 tell m3, length 46 12:56:23.796889 ARP, Reply test103 is-at P103C, length 46
```

`v6% # ifconfig xl0 delete`
## DHCP
```
v6% # dhclient xl0
DHCPDISCOVER on xl0 to 255.255.255.255 port 67 interval 6 DHCPOFFER from 194.29.146.27
DHCPREQUEST on xl0 to 255.255.255.255 port 67
DHCPACK from 194.29.146.27
bound to 194.29.146.232 -- renewal in 21600 seconds.

```
## 4 UDP
```
v6% nc -u -l 6666
v6% sudo tcpdump -s 1400 -i lo0 -w udp.pcap port 6666
```
Następnie połączyliśmy się z nim i wysłaliśmy wiadomość
```
v6% nc -u localhost 6666 hi
hi im udp
not anymore
^C
```
k
## TCP
**tcpdump** - śledz ruch na wybranym porcie:
```
v6% nc -l 6666
v6% sudo tcpdump -s 1400 -i lo0 -w tcp.pcap port 6666
v6% nc localhost 6666 hi
bai
^C
4
``

