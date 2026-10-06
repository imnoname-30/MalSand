# Terminal thứ 3

> [!NOTE]
> - Đã thực hiện toàn bộ các chỉ mục `About` và `Installion`.
> - Đang ở trong môi trường ảo của python (`cuckoo-test` trong ngữ cảnh này).

Terminal thứ 3 này sẽ chỉ phục vụ cho `rooter`.

> [!NOTE]
> Cho rằng nội dung từ mục `About` cho đến hết `Installing` đều nằm trong 1 Terminal và thực hiện từ đầu đến giờ.

--- Mở terminal thứ 3 (LƯU Ý: nhưng vẫn phải cùng một sesion)---

Nếu chưa vào lại môi trường ảo (`cuckoo-test` trong ngữ cảnh này:

```bash
3rdTerminal
gloryu@ubuntu:~$
```

Vào lại môi trường ảo bằng `workon`:

```bash
3rdTerminal
gloryu@ubuntu:~$ workon cuckoo-test
(cuckoo-test) gloryu@ubuntu:~$
```

Mở `rooter`

```bash
3rdTerminal
cuckoo rooter --sudo --group gloryu
```
