
# Setup WSL Ubunti

## setup packages

```bash
sudo apt install -y openssh-server build-essential gcc gdb rsync zip ninja-build 
```



## allow password auth

```bash
sudo sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
```

## allow your user to login

```bash
if [[ $(cat /etc/ssh/sshd_config | grep "AllowUsers `whoami`") == "" ]]; then
sudo bash -c 'echo "AllowUsers '$(whoami)'">>/etc/ssh/sshd_config'
fi
```

## allow your user to sudo without password

```bash
if [[ $(sudo cat /etc/sudoers | grep "`whoami` ALL=(ALL) NOPASSWD:ALL") == "" ]]; then
sudo bash -c 'echo "'$(whoami)' ALL=(ALL) NOPASSWD:ALL">>/etc/sudoers'
fi
```

## setup sshd server ssh keys

```bash
sudo ssh-keygen -A
```

## start sshd service

```bash
sudo service ssh start
```

## setup clang

```bash
sudo bash -c "$(wget -O - https://apt.llvm.org/llvm.sh)"
sudo ln -sf $(ls /usr/bin/clang++-* | head -n 1) /usr/bin/clang++
sudo ln -sf $(ls /usr/bin/clang-* | head -n 1) /usr/bin/clang
```

## setup cmake
```bash
wget  https://github.com/microsoft/CMake/releases/download/v3.17.3587832/cmake-3.17.3587832-MSVC_2-Linux-x64.sh
sudo bash -c $(pwd)/'cmake-3.17.3587832-MSVC_2-Linux-x64.sh --skip-license --prefix=/usr/'
```


