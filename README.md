# FORTIGATE
Cihaz Durumunu Kontrol Etme
get system status
Port Bilgilerini Görme
config system interface  -> show
SFP Durumunu Görme
get system interface transceiver
Route Tablosunu Görme
get router info routing-table ospf
get router info routing-table all
Komşu Router Bilgisi
get router info ospf neighbor
Port IP Tanımlama
config system interface
edit port1
set mode static (default olarak dhcp gelir)
set ip 10.10.10.1 255.255.255.0
end
İstenilen Servislere İzin Verme
config system interface
edit port1
set allowaccess ping http htpps ssh
İstenilen Cihaza Ulaşım Kontrolü
execute ping ip_adres
Fabrika Ayarlarına Dönme
execute factoryreset
Hatalı Girişte Kullanıcı Kilitleme
config system global
set admin-lockout-threshold 3 ( 3 hatalı girişte kilitle)
Kilitli Hesabın Aktif Olma Süresi
config system global
set admin-lockout-duration 10 ( 10 sn. kilitli kal)
MTU Ayarlarını Değiştirme
config system interface
edit port10
set mtu-override enable
set mtu 1400
end
Cihaz Yedeği Alma
admin -> configuration –> backup
Encryption açarak parola belirlenir. Geri yükleme yaparken aynı parola girilir.
Cihaz Yedekten Yükleme
admin -> configuration –> restore
Yeni Takılan HDD’yi Formatlama
execute formatlog disk
DHCP Ayarlama
config system dhcp server
edit
edit1
config exclude-range
edit
edit1
set start-ip 10.10.10.10
set end-ip 10.10.10.30
end
DHCP Kontrol Etme
show system dhcp server
PPPOE Modu
config system interface
edit port5
set mode pppoe
end
(ADSL modemi bridge moda alıp, firewall’un ilgili portuyla sonlandırılır. Kullanıcı adı ve şifre girilir)
Link Monitör
config system link-monitor
edit test
set srcintf port1
set server 10.10.10.1 (ISP ip adresi)
set protocol ping
set gateway-ip 10.10.10.1
set failtime 5
set interval 5
set update-cascade-interface enable
set update-static-route enable
set status enable
end
(1.interface kesilirse 2.den devam etmek için kullanılır.)
Port Birleştirme (Link Aggregate)
Arayüz =>   network -> interfaces -> Create new -> interface -> type -> 802.3ad Aggregate
CLI =>
config system interface
edit agg (İsteğe göre isim belirle)
set type aggregate
set member port1 port2
set vdom root
set ip 10.10.10.10/24
set allowaccess ping
end
Zone Oluşturma
config system zone
edit zone_adı
set interface port7 port8
end
VLAN Oluşturma
config system interface
edit vlan10
set interface port5
set type vlan
set vlanid 10
set ip 10.10.10.10/24
set allowaccess ping
end
Layer 2 Trafiğine İzin Verme
Defaultta Fortinet Layer 2 trafiğine izin vermez. STP trafiğini geçirmez. İzin vermek için;
config system interface
edit port1
set l2forward enable
set stpforward enable
end
AD Üzerinden Oturum Açan Kullanıcıları Görme
diagnose debug authd fsso list

VDOM Aktif Etme
config system global
set vdom-admin enable
end
y
HTTPS İçin TLS Aktif Etme
config system global
set admin-https-ssl-versions tlsv1.2 (versions’dan sonra ? basarak tls versiyonları görülür)
end
USB İle Kurulumu Engelleme
config system auto-install
set auto-install-config disable
set auto-install-image disable
end
Konsol Kablosu İle Şifre Sıfırlamayı Kapatma
config system global
set admin-maintainer-disable
(Şifre unutulduğunda cihaza konsol kablosu ile bağlanıp 60 sn içinde şifreyi sıfırlamayı kapatır)
Gelen-Giden Bandwitdh Trafiğini Ayarlama
config system interface
edit wan1 (istenilen interface)
set inbandwidth 1280
set outbandwidth 1280 (kbps)
SSL VPN Bağlantı Zaman Aşımı
Girilen süre kadar kullanılmazsa bağlantıyı sonlandırır.
Arayüz => VPN -> SSL VPN Setting -> Idle logout  (Aktif et) -> Inactive for (600 sn)
CLI =>
config vpn ssl settings
set idle-timeout 600
end
SSL VPN Doğrulama Zaman Aşımı
Kullanım olsada olmasada girilen süre sonunda bağlantıyı sonlandırıp tekrar doğrulama ister.
config vpn ssl settings
set auth-timeout 36000 (10 saat)
end





