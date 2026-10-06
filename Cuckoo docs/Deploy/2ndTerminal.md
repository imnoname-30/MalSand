# Configuration

> [!NOTE]
> - Đã thực hiện toàn bộ các chỉ mục `About` và `Installion`.
> - Đang ở trong môi trường ảo của python (`cuckoo-test` trong ngữ cảnh này).

và

> [!NOTE]
> Cho rằng nội dung từ mục `About` cho đến hết `Installing` đều nằm trong 1 Terminal và thực hiện từ đầu đến giờ.

  --- Mở terminal thứ 2 (LƯU Ý: nhưng vẫn phải cùng một sesion)---
```bash
2nd terminal
(cuckoo-test) gloryu@ubuntu:~$ sudo sysctl -w net.ipv4.conf.vboxnet0.forwarding=1
(cuckoo-test) gloryu@ubuntu:~$ sudo sysctl -w net.ipv4.conf.ens100.forwarding=1
```

Hai lệnh bên trên không khả năng config vĩnh viễn.

Nếu muốn config vĩnh viễn, mở `/etc/sysctl.conf` và dán 
```bash
2nd terminal
(cuckoo-test) gloryu@ubuntu:~$ sudo sysctl -w net.ipv4.conf.vboxnet0.forwarding=1
(cuckoo-test) gloryu@ubuntu:~$ sudo sysctl -w net.ipv4.conf.ens33.forwarding=1
```

xuống dưới cùng của file.

Cách làm:

```bash
sudo nano /etc/sysctl.conf
```

Đưa con trỏ xuống dưới cùng và dán hai lệnh bên trên.

Tiếp theo, network routing
```bash
2nd terminal
(cuckoo-test) gloryu@ubuntu:~$ sudo iptables -t nat -A POSTROUTING -o *your interface name* -s 192.168.56.0/24 -j MASQUERADE
(cuckoo-test) gloryu@ubuntu:~$ sudo iptables -P FORWARD DROP
(cuckoo-test) gloryu@ubuntu:~$ sudo iptables -A FORWARD -m state --state RELATED,ESTABLISHED -j ACCEPT
(cuckoo-test) gloryu@ubuntu:~$ sudo iptables -A FORWARD -s 192.168.56.0/24 -j ACCEPT
```

Trong câu lệnh đầu tiên

```bash
(cuckoo-test) gloryu@ubuntu:~$ sudo iptables -t nat -A POSTROUTING -o *your interface name* -s 192.168.56.0/24 -j MASQUERADE
```

`your interface name` là interface thường bắt đầu bằng `ens`. Hoặc nhìn vào địa chỉ IPv4 của interface, nó sẽ thường bắt đầu như `192.168.x.x`. Sử dụng lệnh `ip a` để kiểm tra. sau khi có được thì thay vào `your interface name`, ví dụ:

```bash
(cuckoo-test) gloryu@ubuntu:~$ sudo iptables -t nat -A POSTROUTING -o ens100 -s 192.168.56.0/24 -j MASQUERADE
```

Sau khi route toàn bộ, kiểm tra bằng lệnh

```bash
2nd terminal
(cuckoo-test) gloryu@ubuntu:~$ (cuckoo-test) gloryu@ubuntu:~$ sudo iptables -vnL
Chain INPUT (policy ACCEPT 0 packets, 0 bytes)
 pkts bytes target     prot opt in     out     source               destination         

Chain FORWARD (policy DROP 0 packets, 0 bytes)
 pkts bytes target     prot opt in     out     source               destination         
    0     0 ACCEPT     all  --  *      *       0.0.0.0/0            0.0.0.0/0            state RELATED,ESTABLISHED
    0     0 ACCEPT     all  --  *      *       192.168.56.0/24      0.0.0.0/0           

Chain OUTPUT (policy ACCEPT 0 packets, 0 bytes)
 pkts bytes target     prot opt in     out     source               destination
```

kết quả sẽ tương đương như vậy.

Sau đó

```bash
2nd terminal
(cuckoo-test) gloryu@ubuntu:~$ while read -r vm ip; do cuckoo machine --add $vm $ip; done < <(vmcloak list vms)
```

## Configure các tệp Cuckoo của Host

```bash
2nd terminal
(cuckoo-test) gloryu@ubuntu:~$ nano ~/.cuckoo/conf/virtualbox.conf
```

Kéo xuống phần machine, xoá `cuckoo1`.

```bash
2nd terminal
(cuckoo-test) gloryu@ubuntu:~$ nano ~/.cuckoo/conf/routing.conf
```

Thay đổi mục `internet`: `internet = ens100` (`ens100` trong ngữ cảnh này).

```bash
2nd terminal
(cuckoo-test) gloryu@ubuntu:~$ nano ~/.cuckoo/conf/reporting.conf
```

Kéo xuống mục `[mongodb]`, thay đổi `enable`: `enable = yes`.

Khởi động lại cuckoo sau khi configurem, cuckoo sẽ đọc lại các tệp được configure.
```bash
2nd terminal
(cuckoo-test) gloryu@ubuntu:~$ cuckoo
```
