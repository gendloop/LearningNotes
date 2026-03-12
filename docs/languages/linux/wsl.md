# WSL

## 安装

1. 查看可用的Linux发行版本
    `wsl --list --online`
2. 安装指定版本
    `wsl --install -d Ubuntu-22.04`
3. 重启
4. 输入用户名username, 输入密码 password, 重复密码 retype password
5. 在文件管理器地址栏输入`\\wsl$`, 查看已安装版本
6. `win+R`运行`%userprofile%`, 创建`.wslconfig`文件, 配置代理

    ```bash
    [experimental]
    networkingMode=mirrored
    dnsTunneling=true
    firewall=true
    autoProxy=true
    ```

## sources.list

配置软件镜像源

### 阿里云镜像源

```bash
deb http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse
```

### 清华大学镜像源

```bash
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-backports main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-security main restricted universe multiverse
```

### 中科大镜像源

```bash
deb https://mirrors.ustc.edu.cn/ubuntu/ jammy main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ jammy-updates main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ jammy-backports main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ jammy-security main restricted universe multiverse
```

### 华为源地址

```bash
deb <https://repo.huaweicloud.com/ubuntu/> focal main restricted
deb <https://repo.huaweicloud.com/ubuntu/> focal-updates main restricted
deb <https://repo.huaweicloud.com/ubuntu/> focal universe
deb <https://repo.huaweicloud.com/ubuntu/> focal-updates universe
deb <https://repo.huaweicloud.com/ubuntu/> focal-backports main restricted universe
deb <https://repo.huaweicloud.com/ubuntu/> focal-security main restricted
deb <https://repo.huaweicloud.com/ubuntu/> focal-security universe
```

### 163源地址

```bash
deb <http://mirrors.163.com/ubuntu/> bionic main restricted universe multiverse
deb <http://mirrors.163.com/ubuntu/> bionic-security main restricted universe multiverse
deb <http://mirrors.163.com/ubuntu/> bionic-updates main restricted universe multiverse
deb <http://mirrors.163.com/ubuntu/> bionic-proposed main restricted universe multiverse
deb <http://mirrors.163.com/ubuntu/> bionic-backports main restricted universe multiverse
deb-src <http://mirrors.163.com/ubuntu/> bionic main restricted universe multiverse
deb-src <http://mirrors.163.com/ubuntu/> bionic-security main restricted universe multiverse
deb-src <http://mirrors.163.com/ubuntu/> bionic-updates main restricted universe multiverse
deb-src <http://mirrors.163.com/ubuntu/> bionic-proposed main restricted universe multiverse
deb-src <http://mirrors.163.com/ubuntu/> bionic-backports main restricted universe multiverse
```

## 重装

```powershell
wsl --uninstall
wsl --install Ubuntu
```

## References

1. [https://learn.microsoft.com/zh-cn/windows/wsl/install](https://learn.microsoft.com/zh-cn/windows/wsl/install)
