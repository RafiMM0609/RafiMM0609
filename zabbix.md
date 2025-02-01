## how to un install zabbix

menggunakan debian/ubuntu

1. Stop layanan zabbix
```
sudo systemctl stop zabbix-server
sudo systemctl stop zabbix-agent
sudo systemctl stop zabbix-proxy  # Jika Anda menggunakan Zabbix Proxy
```
2. Hapus paket zabbix ( termasuk zabbix-mysql , zabbix-frontend)
```
sudo apt-get remove --purge zabbix-server-mysql zabbix-frontend-php zabbix-agent zabbix-proxy-mysql
```
3. hapus database zabbix
- masuk ke database mysql
```
mysql -u root -p
```
- lakukan query
```
DROP DATABASE zabbix;
DROP USER 'zabbix'@'localhost';
FLUSH PRIVILEGES;
exit;
```
4. Hapus file konfigurasi
```
sudo rm -rf /etc/zabbix
sudo rm -rf /var/lib/zabbix
sudo rm -rf /usr/share/zabbix
```
5. hapus pengguna(user) dan group zabbix
```
sudo userdel zabbix
sudo groupdel zabbix
```
6. Hapuse repository zabbix ( if exist )
```
sudo rm /etc/apt/sources.list.d/zabbix.list
sudo apt-get update
```
7. Bersihkan package nganggur
```
sudo apt-get autoremove
sudo apt-get autoclean
```
8. Reboot system
```
sudo reboot
```

### Tambahan

- Jika ditemui zabbix masi digunakan pada proses apapun
  - cari proses yang menggunakan user zabbix
    ```
    ps -u zabbix
    ```
  - copy pid dan bunuh paksa ( kill )
    ```
    sudo kill 1234232
    ```
  - jika ingin singkat saja pakai ini
    ```
    sudo pkill -u zabbix
    ```

### Cara verifikasi jika zabbix sudah terhapus
- 
```
dpkg -l | grep zabbix
```
- 
```
sudo find / -name "*zabbix*"
```
-
```
sudo systemctl list-unit-files | grep zabbix
```
