# Installing Cuckoo

> [!NOTE]
> Môi trường và yêu cầu
>
> Hãy chắc chắn rằng bạn đã đăng nhập bằng tài khoản người dùng Cuckoo (`gloryu` trong ngữ cảnh này) và bạn đã:
> 
> Cài đặt tất cả các phụ thuộc hệ thống từ phần [phụ thuộc của Cuckoo](https://github.com/imnoname-30/Cuckoo-Setup-Old-version-Using-python2-python2.7-/blob/main/Cuckoo%20docs/Installation/Preparing%20the%20Host/Requirements.md#c%C3%A0i-%C4%91%E1%BA%B7t-c%C3%A1c-th%C6%B0-vi%E1%BB%87n-python-tr%C3%AAn-c%C3%A1c-b%E1%BA%A3n-ph%C3%A2n-ph%E1%BB%91i-d%E1%BB%B1a-tr%C3%AAn-ubuntudebian)
> 
> Đáp ứng các yêu cầu để chạy [Cuckoo](https://github.com/imnoname-30/Cuckoo-Setup-Old-version-Using-python2-python2.7-/blob/main/Cuckoo%20docs/About/Cuckoo.md#cuckoo-requirements)

## Create a user

> Tài liệu này sẽ sử dụng luôn user khi tạo hostVM nên không tạo user mới.

Nếu bạn đang sử dụng VirtualBox, hãy đảm bảo rằng người dùng mới thuộc nhóm "vboxusers" (hoặc nhóm mà bạn đã sử dụng để chạy VirtualBox):

```bash
gloryu@ubuntu:~$ sudo usermod -a -G vboxusers gloryu
```

## Install Cuckoo

### Cài `virtualenv` + `virtualenvwrapper` (dùng **pip3**, không phải pip2)

Lưu thành file cuckoo-setup-virtualenv.sh:

```bash
gloryu@ubuntu:~$ nano cuckoo-setup-virtualenv.sh
```

Copy toàn bộ đoạn script dưới đây:

```bash
#!/usr/bin/env bash
# Run as: sudo -u cuckoo ./cuckoo-setup-virtualenv.sh

set -euo pipefail

sudo apt-get update
sudo apt-get -y install python3-pip

add_once() {
    local line="$1"
    grep -qxF "$line" ~/.bashrc 2>/dev/null || echo "$line" >> ~/.bashrc
}

python3 -m pip install --user --upgrade "pip<21" "setuptools<50" "wheel<0.34"

python3 -m pip install --user "packaging<21" "pbr<6"

python3 -m pip install --user --no-build-isolation virtualenv "virtualenvwrapper==4.8.4" "stevedore<3"

python3 -m pip completion --bash >> ~/.bashrc 2>/dev/null || true

add_once 'export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3'
add_once 'export WORKON_HOME=~/.virtualenvs'
add_once 'export PIP_VIRTUALENV_BASE=~/.virtualenvs'
add_once 'source ~/.local/bin/virtualenvwrapper.sh'

export WORKON_HOME=~/.virtualenvs
```

Lưu bằng cách: `Ctrl + x` → `y` → `Enter`

```bash
gloryu@ubuntu:~$ chmod +x cuckoo-setup-virtualenv.sh
gloryu@ubuntu:~$ ./cuckoo-setup-virtualenv.sh
gloryu@ubuntu:~$ source ~/.bashrc
```

### Tạo venv Python 2.7 riêng cho Cuckoo và cài Cuckoo bằng **pip2**

```bash
gloryu@ubuntu:~$ mkvirtualenv -p python2.7 cuckoo-test
```

> Sau lệnh này, prompt sẽ đổi thành `(cuckoo-test) gloryu@ubuntu:~$ ` — nghĩa là bạn **đang ở trong venv**. Bên trong venv, lệnh `pip` chính là `pip2` của venv đó (đã tự động cô lập, không cần gõ `pip2` tường minh nữa vì venv chỉ có một pip duy nhất):

```bash
(cuckoo-test) gloryu@ubuntu:~$ pip install -U pip setuptools
(cuckoo-test) gloryu@ubuntu:~$ pip install "M2Crypto==0.35.2"
(cuckoo-test) gloryu@ubuntu:~$ pip install -U cuckoo
```

Kiểm tra Cuckoo cài đúng chưa:

```bash
(cuckoo-test) gloryu@ubuntu:~$ cuckoo --d
(cuckoo-test) gloryu@ubuntu:~$ cuckoo community
```
