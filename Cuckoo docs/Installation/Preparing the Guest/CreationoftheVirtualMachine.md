# Creation of the Virtual Machine

> [!NOTE]
> Môi trường và yêu cầu
>
> Hãy chắc chắn rằng bạn đã đăng nhập bằng tài khoản người dùng Cuckoo (`gloryu` trong ngữ cảnh này) và bạn đã:
> 
> - Đã đáp ứng NOTE và đã cài đặt [VMCloak](https://github.com/imnoname-30/Cuckoo-Setup-Old-version-Using-python2-python2.7-/blob/97fc8dc298067a234014a455f640e05e26b1e48a/Cuckoo%20docs/Installation/Preparing%20the%20Host/VMCloak.md)
> - Đang ở trong môi trường ảo của python (`cuckoo-test` trong ngữ cảnh này)
> - Đã đáp ứng NOTE và đã sở hữu image hợp lệ từ phần [Guest's image Prepare](https://github.com/imnoname-30/Cuckoo-Setup-Old-version-Using-python2-python2.7-/blob/97fc8dc298067a234014a455f640e05e26b1e48a/Cuckoo%20docs/Installation/Preparing%20the%20Guest/imagePrepare.md) (image trong phần này chỉ là ví dụ, các phiên bản tương đương đều có thể làm theo từ hướng dẫn option của `VMCloak`)

```bash
(cuckoo-test) gloryu@ubuntu:~$ vmcloak-vboxnet0
(cuckoo-test) gloryu@ubuntu:~$ vmcloak init --verbose --win7x86 win7x86base --cpus 2 --ramsize 2048 --paravirtprovider none --product ULTIMATE --serial-key XXXXX-XXXXX-XXXXX-XXXXX-XXXXX
(cuckoo-test) gloryu@ubuntu:~$ vmcloak clone win7x86base win7x86cuckoo
(cuckoo-test) gloryu@ubuntu:~$ vmcloak list deps
(cuckoo-test) gloryu@ubuntu:~$ vmcloak install win7x86cuckoo ie11
(cuckoo-test) gloryu@ubuntu:~$ vmcloak snapshot --count 1 win7x86cuckoo 192.168.56.101
(cuckoo-test) gloryu@ubuntu:~$ vmcloak list vms
```
