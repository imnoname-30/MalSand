# Guest's image Prepare

> [!NOTE]
> Trước khi tạo GuestVM, cần phải có image để tạo. Hãy đảm bảo đáp ứng yêu cầu trong phần [Supported sandbox environments](https://github.com/imnoname-30/Cuckoo-Setup-Old-version-Using-python2-python2.7-/blob/main/Cuckoo%20docs/About/Cuckoo.md#supported-sandbox-environments)

## Downloading an image

Như trong NOTE đề cập, cần phải có image phù hợp để tạo GuestVM.

```bash
gloryu@ubuntu:~$ sudo wget https://cuckoo.sh/win7ultimate.iso
```

Trong tài liệu cũ của Cuckoo, các liên kết dẫn đến các image của Windows 7 hiện không còn tồn tại (như bên trên). Điều này làm cho việc kiếm một image hợp lệ để cài đặt GuestVM trở nên rất khó khăn. Trong tài liệu này, giả định rằng bạn đã chuẩn bị được một image (`win7x86 ultimate` trong ngữ cảnh này) để thực hiện các bước tiếp theo.

## Mounting image

```bash
gloryu@ubuntu:~$ sudo mkdir /mnt/win7
gloryu@ubuntu:~$ sudo chown gloryu:gloryu /mnt/win7/
gloryu@ubuntu:~$ sudo mount -o ro,loop ~/disk/win7ultimate.iso /mnt/win7
```
