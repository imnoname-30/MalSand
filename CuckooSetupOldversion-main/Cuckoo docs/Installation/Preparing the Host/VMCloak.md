# Installing VMCloak

> [!NOTE]
> Môi trường và yêu cầu
>
> Hãy chắc chắn rằng bạn đã đăng nhập bằng tài khoản người dùng Cuckoo (`gloryu` trong ngữ cảnh này) và bạn đã:
> 
> - Cài đặt tất cả các phụ thuộc hệ thống từ phần [phụ thuộc của Cuckoo](https://github.com/imnoname-30/Cuckoo-Setup-Old-version-Using-python2-python2.7-/blob/main/Cuckoo%20docs/Installation/Preparing%20the%20Host/Requirements.md#c%C3%A0i-%C4%91%E1%BA%B7t-c%C3%A1c-th%C6%B0-vi%E1%BB%87n-python-tr%C3%AAn-c%C3%A1c-b%E1%BA%A3n-ph%C3%A2n-ph%E1%BB%91i-d%E1%BB%B1a-tr%C3%AAn-ubuntudebian) (`genisoimage` là dependency của VMCloak)
> - Đang ở trong môi trường ảo của python (`cuckoo-test` trong ngữ cảnh này)

Cuckoo sử dụng máy ảo để thực hiện các phân tích của mình. VMCloak là một công cụ tuyệt vời giúp tạo và cấu hình các máy ảo đó.

## Installing VMCloak

```bash
(cuckoo-test) gloryu@ubuntu:~$ pip install -U vmcloak
```

Tại thời điểm tạo ra tài liệu này, phiên bản của VMCloak được sử dụng là 0.4.8
