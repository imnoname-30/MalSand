# Requirements
Trước khi tiến hành cài đặt và cấu hình Cuckoo, bạn cần cài đặt một số gói phần mềm và thư viện bắt buộc.

## Cập nhật hệ thống và cài gói nền tảng

```bash
gloryu@ubuntu:~$ sudo apt-get update
gloryu@ubuntu:~$ sudo apt-get -y upgrade
```

## Cài đặt các thư viện Python (trên các bản phân phối dựa trên Ubuntu/Debian)

Thành phần máy chủ Cuckoo được viết hoàn toàn bằng Python, do đó cần phải cài đặt phiên bản Python phù hợp. Hiện tại, chúng tôi chỉ hỗ trợ đầy đủ Python 2.7. Các phiên bản Python cũ hơn và Python 3 hiện không được chúng tôi hỗ trợ (mặc dù việc hỗ trợ Python 3 nằm trong danh sách việc cần làm của chúng tôi với mức độ ưu tiên thấp).

Để cài đặt và chạy Cuckoo đúng cách, cần phải cài đặt các gói phần mềm sau từ kho lưu trữ apt:

```bash
gloryu@ubuntu:~$ sudo apt-get install python python-pip python-dev libffi-dev genisoimage
gloryu@ubuntu:~$ sudo apt-get install python-virtualenv python-setuptools  
gloryu@ubuntu:~$ sudo apt-get install libjpeg-dev zlib1g-dev swig
```

Để sử dụng giao diện web dựa trên Django, cần phải có MongoDB:

```bash
gloryu@ubuntu:~$ sudo apt-get install mongodb
```

Để sử dụng PostgreSQL làm cơ sở dữ liệu (đây là lựa chọn chúng tôi khuyến nghị), bạn cũng cần cài đặt PostgreSQL:

```bash
gloryu@ubuntu:~$ sudo apt-get install postgresql libpq-dev
```

## Virtualization Software

```bash
gloryu@ubuntu:~$ echo deb http://download.virtualbox.org/virtualbox/debian xenial contrib | sudo tee -a /etc/apt/sources.list.d/virtualbox.list
gloryu@ubuntu:~$ wget -q https://www.virtualbox.org/download/oracle_vbox_2016.asc -O- | sudo apt-key add -
gloryu@ubuntu:~$ sudo apt-get update
gloryu@ubuntu:~$ sudo apt-get install virtualbox-5.2
```

## Installing tcpdump

```bash
gloryu@ubuntu:~$ sudo apt-get install tcpdump apparmor-utils
gloryu@ubuntu:~$ sudo aa-disable /usr/sbin/tcpdump
```

Tcpdump yêu cầu quyền root, nhưng vì bạn không muốn Cuckoo chạy với quyền root, nên bạn cần gán các capability (quyền hạn) cụ thể của Linux cho tệp thực thi này:

```bash
gloryu@ubuntu:~$ sudo groupadd pcap
gloryu@ubuntu:~$ sudo usermod -a -G pcap gloryu
gloryu@ubuntu:~$ sudo chgrp pcap /usr/sbin/tcpdump
gloryu@ubuntu:~$ sudo setcap cap_net_raw,cap_net_admin=eip /usr/sbin/tcpdump
```

Bạn có thể kiểm tra kết quả của lệnh vừa rồi bằng cách:

```bash
gloryu@ubuntu:~$ getcap /usr/sbin/tcpdump
/usr/sbin/tcpdump = cap_net_admin,cap_net_raw+eip
```

### Installing M2Crypto

```bash
gloryu@ubuntu:~$ sudo pip install m2crypto==0.24.0
```
