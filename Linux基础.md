# Linux 常用命令与管理速查表

---

## 一、虚拟机安装与管理
- **安装虚拟机：**
  - 设置内存、镜像
  - 支持快照保存
  - 支持克隆

---

## 二、系统分区与挂载
- **分区（逻辑分区）**
- **格式化**
- **设备文件名**
- **挂载（空目录）**

---

## 三、系统安装
- 中文语言、设置时区
- 手动分区
- 选择初始安装的软件
- 设置密码
- `Ctrl+L` 清屏

---

## 四、网络配置
- `ifconfig` 查询/修改网卡信息
- 三种适配模式，对应不同网卡
- **secureCRT** 远程登录
- **WinSCP** 连接 Win 和 Linux

---

## 五、基础规则
- 区分大小写
- 所有内容以文件形式保存，无扩展名

---

## 六、常用目录说明

| 目录         | 说明                             |
| ------------ | -------------------------------- |
| bin          | 命令                             |
| sbin         | root 命令                        |
| usrbin       | 单用户命令                       |
| boot         | 启动文件（重置要备份）           |
| dev          | 硬件                             |
| etc          | 配置默认                         |
| home         | 非 root 用户根目录               |
| lib          | 函数库                           |
| lost+found   | 异常碎片放置                     |
| m开头        | 挂载点                           |
| usr/local    | 三方软件目录                     |
| proc/sys     | 内存信息                         |
| srv          | 服务数据                         |
| tmp          | 临时文件                         |
| usr          | Unix Software Resource 系统资源  |
| var          | 日志                             |

---

## 七、服务器操作建议
- 不允许关机，只能重启（重启前关闭服务）
- 非高峰期执行高负载命令
- 配置防火墙避免自己被踢出（可定时清空防火墙配置）
- 密码合理，定期更新
- 合理分配权限
- 定期备份

---

## 八、常用按键
- `Ctrl+L` 或 `clear` 清屏
- `Ctrl+C` 取消命令
- `y` (yes), `n` (no)

---

## 九、命令格式
- `命令 -选项 参数`

---

## 十、常用命令详解

### 1. ls — 列出文件
- `-a` 显示所有文件（含隐藏）
- `-l` 详细信息
- `-h` 人性化字节
- `-d` 只显示目录本身
- `-i` 显示 inode
- `/` 指定根目录

### 2. 文件类型显示
- `-` 普通文件
- `d` 目录
- `l` 软连接

### 3. 权限
- `r` 读
- `w` 写
- `x` 执行
- `u` 所有者
- `g` 所属组
- `o` 其他人

### 4. 目录操作
- `mkdir /` 创建目录
  - `-p` 递归创建
- `cd /` 切换目录
- `pwd` 显示当前目录
- `rmdir` 删除空目录

### 5. 文件操作
- `cp` 复制，`-r` 目录，`-p` 保留属性
- `mv` 移动或重命名
- `rm` 删除，`-r` 目录，`-f` 强制
- `touch` 新建文件

### 6. 文件浏览/显示
- `cat` 查看文件，`-n` 带行号
- `tac` 反向显示
- `more` 分页，`less` 加强版，可向上翻页与搜索
- `head/tail` 查看前/后N行，`tail -f` 动态刷新

### 7. 链接
- `ln` 创建硬链接
- `ln -s` 创建软链接

### 8. 权限修改
- `chmod` 修改权限
  - `u/g/o/a +/-= rwx`
  - `数字法 421`
  - `-R` 递归
- `chown` 修改所有者
- `chgrp` 修改组
- `umask` 查看/设置新建文件默认权限

---

## 十一、查找与搜索

### 1. find
- `find 路径 选项`
- `-name` 按文件名（*模糊，？单字符）
- `-iname` 不区分大小写
- `-size` 按大小
- `-user`/`-group` 按所属
- `-amin/-cmin/-mmin` 访问/属性/内容修改时间（分钟）
- `-a` and, `-o` or
- `-type` f/d/l
- `-exec` 辅助执行
- `-inum` 按 inode 查找

### 2. locate
- 本地数据库搜索，`-i` 不区分大小写
- `updatedb` 更新数据库

### 3. which/whereis
- `which` 查命令路径
- `whereis` 查命令路径、帮助文档、配置文件

### 4. grep
- `grep -选项 "关键词" 文件`
  - `-i` 不区分大小写
  - `-n` 输出行号
  - `-v` 排除
  - `--color=auto` 关键字高亮

---

## 十二、帮助与信息

- `man` 联机手册，`man -k` 搜索
- `info` 信息手册
- `whatis` 简要说明
- `apropos` 简要说明
- `--help` 显示帮助
- `help` shell 内置命令帮助

---

## 十三、用户与会话

- `who` 查看用户
- `w` 更详细
- `last` 查看登录日志
- `lastlog` 查看最近登录
- `logout` 退出登录

---

## 十四、压缩与打包

- `gzip` 压缩文件
- `gunzip` 解压
- `tar` 打包与解包
  - `-c` 打包，`-x` 解包
  - `-z` 针对zip，`-j` 针对bzip2
  - `-v` 详细信息，`-f` 指定文件
- `zip`/`unzip` 压缩/解压目录
- `bzip2`/`bunzip2` 高压缩比
- `-k` 保留原文件

---

## 十五、消息与邮件

- `write` 向在线用户发消息 (`Ctrl+D` 结束)
- `wall` 广播
- `mail` 离线邮件

---

## 十六、网络命令

- `ping` 网络连通测试，`-c` 次数
- `ifconfig` 网卡
- `traceroute` 跟踪路由
- `netstat` 网络状态
  - `-t` TCP, `-u` UDP, `-l` 监听, `-r` 路由, `-n` IP和端口, `-a` 全部

- `setup` 网络配置

---

## 十七、挂载与关机

- `mount` 挂载
- `umount` 卸载
- `shutdown` 关机
  - `-c` 取消关机，`-h` halt关机，`-r` 重启
  - 时间：`now`

---

## 十八、运行级别

- `id:3:initdefault;` 修改默认运行级别
- 0 关机，1 单用户，2 不完全多用户，3 完全多用户，4 未分配，5 图形界面，6 重启
- `runlevel` 显示当前运行级别

---

## 十九、vim 使用速查

- `u` 撤销
- `Esc` 命令模式
- 插入模式：a/i/o
- `:set nu` 显示行号，`:set nonu` 取消
- `gg` 第一行，`G` 最后一行，`:n` 第n行，`$` 行末，`0` 行首
- 删除：`x`/`nx` 单字符/n个，`dd` 整行，`D` 行尾，`ndd` n行，`dG` 到末尾，`:1,3d` 范围
- 复制：`yy`/`nyy`，粘贴：`p`/`P`
- 替换：`r` 单字符，`R` 连续
- 查找：`/内容`，`set ic` 忽略大小写，`n` 下一个
- 替换：`:%s/旧/新/g` 全文，`:1,55s/^旧/新/c` 询问
- 保存：`:w`，`:w 路径`，`:wq`，`:q!` 强退，`:wq!` root 强制保存
- 导入文件/命令：`:r 路径`，`:r!命令`
- 定义快捷键、ab替换、永久生效写入`/.vimrc`

---

## 二十、shell 基础

- 输出：`echo ""` 或 `''`
  - `-e` 支持特殊符号
- 脚本头：`#!/bin/Bash`
- 执行脚本：赋权限直接运行/`bash 文件名`
- 格式转换：`doc2unix`
- 历史命令：
  - `history` 查看
  - `-c` 清空，`-w` 保存
  - `!n` 执行第n条，`!!` 上一条，`!str` 匹配
- tab 补全
- `alias` 定义别名，`unalias` 删除
- 永久生效：`/root/.bashrc`

---

## 二十一、输入输出重定向

- 输出重定向：`>` 覆盖，`>>` 追加，`2>` 错误重定向，`&>` 全部重定向，`> /dev/null` 丢弃
- 输入重定向：`<`
- 统计：`wc`
- 命令顺序：`;` 连续，`&&` 且，`||` 或
- 复制磁盘：`dd if= 输入 of= 输出 bs=字节 count=次数`
- 管道符：`|`
- 通配符：`*`、`?`

---

## 二十二、软件包管理（dpkg & apt）

- `apt-get update` 更新软件源
- `apt-get upgrade` 更新软件包
- `apt-get install` 安装软件包
- `apt-get remove` 卸载
- `apt-get clean` 删除缓存
- 其他参数：
  - `-d` 仅下载
  - `-f` 修复依赖
  - `-m` 缺少依赖继续
  - `-q` 日志输出
  - `-purge` 完全卸载
  - `-reinstall` 重装
  - `-b` 下载源码编译
  - `-s` 模拟执行
  - `-y` 自动 yes
  - `-u` 升级列表
  - `-h` 帮助
  - `-v` 版本

- `apt-cache search/depends/show policy`
- 重要文件路径
  - `/etc/apt/sources.list` 软件源
  - `/var/lib/apt/lists/*` 包列表
  - `/var/cache/apt/archives` .deb 缓存

---

## 二十三、信息查询

- `man` 命令手册
- `date` 显示/设置时间
- `clear` 清屏

---

## 二十四、用户与权限管理

- `passwd` 修改密码
- `su` 切换用户
- `su -c "命令" 用户名` 执行单命令

---

## 二十五、文本与磁盘分析

- `echo`
- `df -h/-T` 磁盘空间
- `du -sh` 目录大小

---
## 二十六、用户管理

- 多用户系统需用户管理，防止操作冲突和保障安全。
- 关键配置文件：
  - `/etc/passwd`：用户信息（用户名、UID、GID、主目录、shell）。
  - `/etc/group`：组信息（组名、GID、成员）。
  - `/etc/skel`：新用户主目录模板。
- 常用命令：
  - 添加用户：`sudo adduser 用户名`
  - 改密码：`sudo passwd 用户名`
  - 改属性：`sudo usermod [参数] 用户名`
  - 删用户：`sudo userdel [-r] 用户名`
  - 添/删组：`sudo addgroup|delgroup 组名`
- 流程：添加用户→系统分配参数与复制配置→可随时修改、删除用户和组。

## 二十七、进程管理

### 1. 进程基础
- **进程**：程序的一次运行实例。
- **核心标识**：PID、PPID、UID、TTY。

### 2. 进程状态
- R: 运行
- S: 可中断睡眠
- D: 不可中断睡眠（I/O 等待，难杀）
- T: 暂停/调试
- Z: 僵尸（父进程未回收）
- 附加：< 高优先级，N 低优先级，s 会话首进程，+ 前台。

### 3. ps 常用
```bash
ps aux        # BSD 风格
ps -ef        # GNU 风格
ps -eLf       # 含线程
ps -eo pid,ppid,stat,%cpu,%mem,cmd
ps aux | grep nginx
ps -ef --forest
```
重点列：PID、%CPU、%MEM、STAT、TIME、COMMAND

### 4. top 常用
- **快捷键**：
  - P：CPU 排序
  - M：内存排序
  - T：累计 CPU 时间
  - 1：展开各 CPU
  - k：杀进程（输入 PID）
  - r：调整 nice
  - q：退出

### 5. pstree
```bash
pstree -ap
ps -ef --forest
```

### 6. /proc 常看
```bash
/proc/<PID>/status   # 状态
/proc/<PID>/fd       # 文件描述符
/proc/<PID>/smaps    # 内存映射
/proc/<PID>/io       # I/O
```

### 7. kill 用法
```bash
kill -15 <PID>    # 优雅终止
kill -9 <PID>     # 强杀（最后手段）
killall nginx
pkill -f pattern
pgrep -a nginx
```

### 8. 优先级
```bash
nice -n 10 cmd
renice -n 10 -p <PID>
```

### 9. 常见排障
- **CPU 高**：top → P → 查 PID → ps -L -p <PID>
- **内存高**：top → M → /proc/<PID>/smaps
- **僵尸**：找父进程回收或重启父进程
- **D 状态**：I/O 卡死，需排查硬件/网络

### 10. 总结
- 看（ps/top/pstree/proc）
- 判（状态/资源）
- 处置（kill/renice/排I/O）


## 二十八、文件系统

-   **文件系统类型**
    -   磁盘: ext4, xfs, btrfs, ntfs, vfat
    -   网络: NFS, SMB(CIFS)
    -   虚拟: procfs(/proc), sysfs(/sys), tmpfs
-   **ext4 要点**
    -   日志 journaling: 崩溃一致性
    -   extents + 延迟分配: 减少碎片
    -   支持大文件/兼容 ext3/2
-   **设备命名**
    -   /dev/sdX (通用 SCSI/SATA/USB)
    -   /dev/nvme0n1p1 (NVMe)
    -   /dev/mapper/... (LVM)
    -   /dev/loopX (回环)
-   **常用查看**
    -   lsblk -f, blkid, df -h, du -sh \*
-   **挂载**
    -   mount /dev/sdb1 /mnt/data
    -   fstab 推荐用 UUID
-   **目录结构 (FHS)**
    -   /etc 配置, /var 可变数据, /home 用户家目录
    -   /usr 软件与库, /bin\|/sbin 基础命令
    -   /tmp 临时, /opt 第三方, /boot 引导
    -   /dev 设备, /proc\|/sys 内核, /mnt\|/media 挂载点
-   **路径**
    -   绝对: /usr/bin
    -   相对: ../file
    -   \~ 家目录, cd -, pwd
-   **权限**
    -   r w x (文件: 读写执行; 目录: 读列写增删执行进入)
    -   chmod 754 f, chown u:g f
    -   特殊位: setuid, setgid, sticky
-   **Linux vs Windows**
    -   单根目录 vs 盘符 C/D
    -   区分大小写 vs 不区分
    -   / vs \\
    -   执行: 权限 vs 扩展名
    -   隐藏: . 开头 vs 属性
    -   换行: `\n `{=tex}vs `\r\n`{=tex}
-   **Swap**
    -   用于内存不足/休眠
    -   分区/文件均可
    -   swapon --show, free -h
-   **网络文件系统**
    -   mount -t nfs host:/dir /mnt/nfs
    -   mount -t cifs //host/share /mnt/share -o user=xx
  


### 1. file：判断文件类型
- `file name` → 显示文件类型  
- `file -i name` → 显示 MIME 类型  
- 示例：`file copy.c`

### 2. ln：链接
- **硬链接**：`ln src dest`（同 inode，不能跨文件系统）  
- **软链接**：`ln -s target link`（存路径，可跨系统，类似快捷方式）  
- 检查：`ls -li` 查看 inode，`readlink link` 查看软链目标  

特点对比：  
| 特性         | 硬链接 | 软链接 |
|--------------|--------|--------|
| 跨文件系统   | ✗      | ✓      |
| 目标改名     | 不受影响 | 链接失效 |
| 目标删除后   | 数据仍在 | 链接失效（同名重建会指向新文件） |

### 3. 压缩工具
- **gzip/gunzip**：单文件压缩，`.gz`  
  - `gzip -k file`，`gunzip file.gz`  
- **bzip2/bunzip2**：压缩比更高，`.bz2`  
- **zip/unzip**：归档+压缩，跨平台常用，`.zip`  
  - `zip -r pack.zip dir/`，`unzip pack.zip`

### 4. tar：归档/打包
- 常用参数：  
  - `-c` 创建，`-x` 解包，`-t` 列表  
  - `-v` 显示过程，`-f` 指定文件  
  - `-z` gzip，`-j` bzip2，`-J` xz，`--zstd` zstd  
- 示例：  
  - `tar -cvf a.tar file1 dir/`（打包）  
  - `tar -czvf a.tar.gz file1 dir/`（打包+gzip）  
  - `tar -xzvf a.tar.gz -C outdir/`（解压到指定目录）  
  - `tar -tvf a.tar.gz`（查看内容）

---
🔑 **重点记忆**：  
`file` → 类型判断  
`ln/ln -s` → 硬/软链接  
`gzip/bzip2/zip` → 压缩工具  
`tar -czvf / -xzvf` → 打包与解压




## 二十九、网络配置管理

### 网络配置方式
- **命令行 (CLI)**：适合服务器/远程环境，灵活稳定。  
- **图形界面 (GUI)**：适合桌面版 Linux，直观方便。

### 虚拟机网络模式
- **桥接 (Bridge)**：虚拟机与宿主机在同一局域网，独立 IP。  
- **NAT**：虚拟机通过宿主机上网，适合校园网/受限网络。  
- **Host-only**：仅与宿主机通信，无法上网。

### 命令行配置
1. 查看网卡：
   ```bash
   ifconfig   # 或 ip addr
   ```
2. 编辑 `/etc/network/interfaces`  
   - DHCP：
     ```ini
     auto ens33
     iface ens33 inet dhcp
     ```
   - Static：
     ```ini
     auto ens33
     iface ens33 inet static
     address 192.168.1.123
     netmask 255.255.255.0
     gateway 192.168.1.1
     ```
3. 配置 DNS：`/etc/resolv.conf`
   ```conf
   nameserver 8.8.8.8
   nameserver 114.114.114.114
   ```
4. 重启网络：
   ```bash
   sudo systemctl restart networking
   ```

### 图形界面配置
- 打开 **网络设置** → IPv4  
- 选择：
  - 自动获取 (DHCP)  
  - 手动设置：填写 IP、子网掩码、网关、DNS  

### 网络验证
1. 查看 IP：
   ```bash
   ifconfig
   ```
2. 测试网关：
   ```bash
   ping 192.168.1.1
   ```
3. 测试外网：
   ```bash
   ping www.baidu.com
   ```

### 常见问题
- **无法上网**：检查虚拟机网络模式 (桥接/NAT)。  
- **DNS 被覆盖**：使用 `systemd-resolved` 或在启动脚本写入。  
- **一直 ping 不通**：虚拟网络编辑器 → 还原默认设置 → 重配网络。 



## 三十、Shell 脚本

### 基础

-   Shell 脚本 = Shell 命令的有序集合。
-   解释型语言：逐行执行，无需编译。
-   脚本首行：`#!/usr/bin/env bash`
-   执行：
    -   `bash script.sh`
    -   `chmod +x script.sh && ./script.sh`

### 变量

-   定义：`name=value`（等号两边不能有空格）。
-   取值：`$name` 或 `${name}`。
-   取消：`unset name`。
-   数字运算：`$((expr))`
-   命令替换：`$(command)`（推荐）。
-   引号：总是用 `"$var"`，避免空格拆分。

### 变量类型

-   普通变量：仅当前 shell 有效。
-   环境变量：`export VAR=value` → 传给子进程。常见：`PATH`、`HOME`。
-   位置参数：
    -   `$0` 脚本名
    -   `$1`...`${10}` 参数
    -   `$#` 参数个数
    -   `$@` 所有参数（逐个保留，推荐）
    -   `$*` 所有参数（合并成一个字符串）
    -   `$?` 上一命令退出码
    -   `$$` 当前进程 PID
    -   `$!` 最近后台命令 PID

### 控制结构

``` bash
if [[ -f "$1" ]]; then
  echo "文件存在"
else
  echo "不存在"
fi

for arg in "$@"; do
  echo "参数: $arg"
done
```

### I/O

-   输入：`read -r var`
-   输出：`echo "text" > file`
-   追加：`>>`
-   错误输出：`2>`
-   合并输出：`>out.log 2>&1`

### 调试与规范

-   调试：`bash -x script.sh`
-   严格模式：`set -euo pipefail`
-   Lint 工具：`shellcheck`
-   引号与花括号：`"$@"`、`${var}`

### 示例：参数备份

``` bash
#!/usr/bin/env bash
set -euo pipefail
today=$(date +%F)
mkdir -p "backup-$today"
for f in "$@"; do
  [[ -e "$f" ]] && cp -a -- "$f" "backup-$today/"
done
```

## 三十一、Shell 功能语句

### 1. 说明性语句

-   `#` 开头至行尾，用于注释，不执行。
-   脚本开头常用 `#!/bin/bash` 指定解释器。

### 2. 功能性语句

#### (1) read 命令

-   从标准输入读取并赋值：`read var`
-   多变量：`read a b c`
-   带提示：`read -p "请输入：" var`

#### (2) expr 命令

-   整数运算：

    ``` sh
    expr 1 + 2      # 3
    expr 5 - 3      # 2
    expr 4 \* 2    # 8  (*需转义)
    expr 9 / 2      # 4
    expr 9 % 2      # 1
    ```

-   注意：运算符前后必须有空格。

### 3. 测试语句 test/\[ \]

#### (1) 字符串测试

-   `=` 相等，`!=` 不等
-   `-z s` 长度为0
-   `-n s` 长度非0

#### (2) 整数测试

-   `-eq` 等于，`-ne` 不等于
-   `-gt` 大于，`-lt` 小于
-   `-ge` 大于等于，`-le` 小于等于

#### (3) 文件测试

-   `-e file` 存在
-   `-d file` 目录
-   `-f file` 普通文件
-   `-L file` 符号链接
-   `-r/-w/-x file` 可读/写/执行
-   `-s file` 存在且非空
-   `f1 -nt f2` f1比f2新
-   `f1 -ot f2` f1比f2旧

------------------------------------------------------------------------

✅ 核心思路：注释(`#`) → 输入(`read`) → 运算(`expr`) → 判断(`test`)。

## 三十二、分支语句

### 1. if 基本用法

``` bash
if 条件; then
  命令
elif 其它条件; then
  命令
else
  命令
fi
```

-   `then` 可换行或用 `;`。
-   `fi` 必须成对。
-   判断依据是**命令退出状态**：0 真，非 0 假。

### 2. 条件表达式写法

-   `test expr` 或 `[ expr ]`

    ``` bash
    [ -f "$file" ]   # 普通文件
    [ "$n" -gt 0 ]   # 数字比较
    ```

-   `[[ expr ]]`（推荐，bash 专用）

    ``` bash
    [[ $s == a* ]]        # 模式匹配
    [[ $s =~ ^[0-9]+$ ]]  # 正则
    ```

-   算术求值 `(( expr ))`（整数）

    ``` bash
    (( n > 0 ))
    x=$((y*2+3))
    ```

### 3. 文件测试常用

-   `-e` 存在，`-f` 普通文件，`-d` 目录，`-L` 符号链接
-   `-r/-w/-x` 可读/写/执行，`-s` 大小 \> 0

### 4. 数字/字符串判断

``` bash
[ "$n" -eq 0 ]     # 数字等于
[ "$a" = "$b" ]    # 字符串相等
[[ $n -ge 0 && $n -le 100 ]]   # 范围
```

### 5. case 多路分支

``` bash
case $var in
  pat1|pat2) 命令 ;; 
  *)         默认 ;;
esac
```

-   模式以 `)` 结束，用 `;;` 结束分支。
-   `*` 表示默认情况。

### 6. 示例

``` bash
# 判断正负零
read -r n
if (( n == 0 )); then
  echo "== 0"
elif (( n > 0 )); then
  echo "> 0"
else
  echo "< 0"
fi

# 成绩分级
read -r score
if ! [[ $score =~ ^[0-9]+$ ]] || (( score<0 || score>100 )); then
  echo "Input error"; exit 1
fi
case $((score/10)) in
  10|9) echo "A" ;;
  8)    echo "B" ;;
  7|6)  echo "C" ;;
  *)    echo "D" ;;
esac
```

### 常见易错点 & 最佳实践

-   `[` 与 `]` 必须有空格，变量要加引号：`[ -n "$s" ]`
-   数字比较用 `-gt/-lt/...`；`>` `<` 在 `[` 中会被当重定向
-   复杂逻辑推荐 `[[ ... && ... ]]` 或分开多个 `[ ]`
-   `[[ ]]` 内不会分词/通配，更安全
-   `(( ))` 适合整数比较与运算
-   利用命令退出状态简化判断：`if grep -q x file; then ...`
-   输入校验常用 `[[ $x =~ ^regex$ ]]`
-   代码要注重可读性，复杂条件可拆行


## 三十三、循环语句

**1) for 基本用法**  
- 语法：`for 变量 in 单词表; do …; done`  
- 执行：变量依次取“单词表”中的每一项并执行循环体。  
```bash
# 打印 1..5
for v in {1..5}; do echo "$v"; done
```
- 命令替换：  
```bash
for f in *; do echo "$f"; done
```

**2) for 的 C 风格写法**  
- 语法：`for (( 初始化; 条件; 迭代 )); do …; done`  
```bash
for (( i=1; i<=5; i++ )); do echo "$i"; done
```

**3) while 基本用法**  
- 语法：`while 命令/表达式; do …; done`  
- 条件为真则执行，假则结束。  
```bash
i=0
while (( i < 10 )); do
  echo "$i"
  ((i++))
done
```

**4) 循环控制语句**  
```bash
# break：直接退出循环
for (( n=0; n<10; n++ )); do
  (( n == 3 )) && break
  echo "$n"
done

# continue：跳过当前迭代
i=0
while (( i < 10 )); do
  (( i == 3 )) && { ((i++)); continue; }
  echo "$i"
  ((i++))
done
```

**5) 常见易错点 & 最佳实践**  
- ✅ 遍历文件用 `*` 或 `./*`，**避免** `ls` 管道。  
- ✅ 变量引用要加引号：`"$var"`。  
- ✅ `[ ]` 条件内需空格：`[ "$i" -lt 10 ]`。  
- ✅ 数值比较：`-lt -gt` 或 `(( ))`；字符串比较：`[[ ]]`。  
- ✅ 更新循环变量时推荐 `((i++))`，避免旧式 `expr`。  
- ✅ 使用 `continue` 时别忘更新计数器，否则死循环。  
- ✅ 数值逻辑优先用 `(( ))`，字符串/文件判断用 `[[ ]]`。  
- ✅ 范围遍历推荐 `{a..b}` 或 `seq`。  
- ✅ 注意 `while` 的退出码等于循环体最后一条命令的退出码。  
- ✅ 脚本健壮性：可考虑 `set -u`、`set -e`。  

**6) 模板速拷**
```bash
# for（列表）
for x in list1 list2 list3; do
  echo "$x"
done

# for（文件）
for f in ./*; do
  [ -f "$f" ] || continue
  echo "file: $f"
done

# for（C 风格）
for ((i=0; i<10; i++)); do
  echo "$i"
done

# while
i=0
while (( i < 10 )); do
  echo "$i"
  ((i++))
done
```


## 三十四、Shell的函数

### 1. 函数定义与调用

-   **定义**：`name() { commands; }` 或
    `function name { commands; }`（Bash 专有）。
-   **调用**：直接写函数名即可，可传参。

### 2. 参数传递

-   `$1, $2, ...`：函数参数。
-   `$#`：参数数量。
-   `"$@"`：参数列表（推荐）。
-   `"$*"`：所有参数合并为一个字符串（不推荐）。

### 3. 返回值

-   **状态码**：`return <0..255>`，用 `$?`
    获取（代表成功/失败，不适合传递大数据）。
-   **数据结果**：用 `echo/printf` 打印，外部用 `$(func)` 捕获。

### 4. 变量作用域

-   **默认全局**：函数内部定义的变量默认全局可见。
-   **局部变量**：`local var=value`（仅在函数内部可见，Bash 支持）。

### 5. 常见易错点必坑

1.  把 `$?` 当成返回数据（错误，应使用 `echo` + 命令替换）。\
2.  忘记给 `$@` 和 `$1` 加引号，触发分裂或通配。\
3.  用 `return` 返回大数或字符串（会被截断到 0..255）。\
4.  未使用 `local`，导致变量污染全局作用域。\
5.  在 `/bin/sh` 下运行 Bash 专有语法（如 `local`、数组），导致报错。\
6.  在脚本顶层写 `return`（只能在函数或被 `source` 的脚本中用）。

### 6. 最佳实践

-   **固定 shebang**：`#!/usr/bin/env bash`。\
-   **始终加引号**：`"$@"`、`"$1"`。\
-   **使用 `local`**：减少副作用。\
-   **分离状态与数据**：用 `return` 表示对/错，用 `echo` 返回数据。\
-   **错误输出重定向到 stderr**：`echo "err" >&2`。\
-   **使用 shellcheck 检查**：避免低级错误。\
-   **保持函数单一职责**：便于组合与测试。\
-   **合理命名**：避免与内建/命令冲突，如 `test`、`echo`。

------------------------------------------------------------------------

## 三十五、GCC 编译与调试

### 1. 课程导航
* GNU 工具链：编译 (GCC)、调试 (gdb)、工程化 (make)。
* GCC 编译器：多语言、多平台、交叉编译常用。
* 编译四阶段：预处理 → 编译 → 汇编 → 链接。
* 常用后缀：.c/.h/.i/.s/.o/.a/.so。
* GCC 常用选项：-E/-S/-c/-o/-g/-O/-l/-L。
* 错误类型与定位：语法、头文件、库/链接、未定义符号。
* 调试：符号信息 + gdb 调试。

---

### 2. 四步编译流水线
| 阶段 | 命令 | 输入 | 输出 |
| ---- | ---- | ---- | ---- |
| 预处理 | gcc -E main.c -o main.i | .c | .i |
| 编译 | gcc -S main.i -o main.s | .i | .s |
| 汇编 | gcc -c main.s -o main.o | .s | .o |
| 链接 | gcc main.o -o app | .o + 库 | 可执行文件 |

---

### 3. 常见文件后缀
* .c 源码
* .h 头文件
* .i 预处理文件
* .s 汇编文件
* .o 目标文件
* .a 静态库
* .so 动态库

---

### 4. GCC 常用选项
* -E/-S/-c ：只执行到预处理/编译/汇编。
* -o <file>：指定输出名。
* -g：生成调试符号。
* -O0/-O1/-O2/-O3/-Ofast：优化等级。
* -Wall -Wextra -Werror：警告相关。
* -std=c11：设定语言标准。
* -I/-L/-l：指定头文件/库路径与库名。
* -DNAME[=VALUE]：宏定义。
* -m32/-m64：目标位宽。

---

### 5. 常见错误与对策
1. 语法错误：检查分号、类型，注意第一条报错。
2. 头文件错误：fatal error: xxx.h，检查路径/拼写，用 -I。
3. 链接错误：undefined reference，检查 -l/-L 顺序与库是否存在。
4. 运行时缺库：error while loading shared libraries，设置 LD_LIBRARY_PATH 或 -Wl,-rpath。
5. 未定义符号：确保函数声明与实现一致，源码/库完整编译。

---

### 6. gdb 调试常用命令
```bash
gdb ./app
(gdb) break main
(gdb) run
(gdb) next
(gdb) step
(gdb) print i
(gdb) backtrace
(gdb) continue
(gdb) quit
```

---

### 7. 静态库与动态库
* 静态库：ar rcs libmylib.a foo.o bar.o
* 动态库：gcc -fPIC -shared foo.o bar.o -o libmylib.so
* 使用：gcc main.o -L./lib -lmylib -o app

---

### 8. 易错点与最佳实践
#### 易错点
1. -g 写成 -j。
2. 忘记 -lxxx 或顺序错误。
3. 头文件拼错或路径错误。
4. 动态库找不到。
5. 宏/条件编译导致平台差异。

#### 最佳实践
* 调试构建：-g -O0 -Wall -Wextra -Werror -std=c11。
* 库顺序：对象文件在前，依赖库在后。
* 出错记录成“错题集”。
* 想看中间产物：-save-temps。
* 多文件工程：用 Makefile。

---

### 9. 小练习
1. 四阶段练习：生成 .i/.s/.o/app。
2. 链接练习：调用 sin/cos，不加 -lm 观察报错，再补上成功。
3. gdb 练习：设置断点、单步、打印变量、查看栈。


## 三十六、gdb 调试工具

### 1. 编译与启动

``` bash
gcc -g file.c -o prog   # 带调试信息编译
gdb ./prog              # 启动调试器
```

### 2. 常用命令

-   **list (l)**：查看源码（默认 10 行）\
-   **break (b)**：设置断点，如 `b 12` 或 `b main`\
-   **info break**：查看断点信息\
-   **run (r)**：启动程序\
-   **next (n)**：单步执行，跳过函数\
-   **step (s)**：单步进入函数\
-   **finish**：运行到当前函数返回\
-   **continue (c)**：继续执行直到下个断点\
-   **print (p)**：打印变量/表达式值\
-   **display**：每次停下自动显示变量\
-   **bt**：查看调用栈\
-   **quit (q)**：退出调试\
-   **help**：获取命令帮助

### 3. 使用流程示例

``` gdb
(gdb) break 12        # 在第 12 行设断点
(gdb) run             # 启动程序
(gdb) next            # 单步执行
(gdb) step            # 进入函数
(gdb) print a         # 查看变量值
(gdb) continue        # 自动执行到下断点
(gdb) quit            # 退出
```

### 4. 易错点

1.  忘记加 `-g`，无调试信息\
2.  优化级别过高导致断点/变量消失\
3.  断点打在不可断的行（如空行/大括号）\
4.  误用 `next` / `step`，进入/跳过错误\
5.  在非暂停状态下查看变量失败

### 5. 最佳实践

-   调试期用 `gcc -g -O0 -Wall`\
-   在可疑位置设置断点，结合 `print`/`display` 观察\
-   使用条件断点与 `watch` 提高效率\
-   利用 `bt` 分析调用栈，快速定位错误\
-   多练习，熟能生巧


