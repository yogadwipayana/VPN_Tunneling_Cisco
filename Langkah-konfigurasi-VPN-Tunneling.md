# VPN_Tunneling_Cisco

TutoriaL konfigurasi VPN Tunneling di router menggunakan Cisco Packect Tracer

--Instal License keamaman
enable
configure terminal
license boot module c1900  technology-package securityk9
yes
exit
reload
yes

--Crypto konfigurasi
enable
configure terminal
crypto isakmp policy 10
encryption aes 256
authentication pre-share
group 5
exit
crypto isakmp key _rahasia_ (buat sama seperti tujuan) addres 209.165.100.1 (ip tujuan)
crypto ipsec transform-set _rnd-hq_ (asal-tujuan) esp-aes 256 esp-sha-hmac
crypto map IPSEC-MAP 10 ipsec-isakmp
("ada note muncul")
set peer 209.165.100.1
set pfs group5
set security-association lifetime second 86400
set transform-set _rnd-hq_ (asal-tujuan)
match address 100
exit

--konfigurasi ke ISP
int se0/0/0 (sesuaikan)
crypto map IPSEC-MAP 
("ada pesan aktif")
exit
access-list 100 permit ip _192.168.2.0_ (ip asal) 0.0.0.255 _192.168.1.0_ (ip tujuan) 0.0.0.255
exit

--pengecekan
sh ip int br
("ip yes NVRAM")
show crypto isakmp policy
show crypto isakmp sa
(uji koneksi terlebih dahulu)
show crypto isakmp sa
("dst src")
show crypto map
("peer access list 100")
