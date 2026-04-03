# Troubleshooting

## 重装系统时遇到`选中的磁盘具有MBR分区表`

1. 进入到弹出该错误窗口时的位置, 记该错误窗口为$W$
2. 按下`Shift+F10`, 会弹出命令行窗口
    1. 输入`diskpart`, 回车
    2. 输入`list disk`, 回车
    3. 输入`select disk 0`, 回车
    4. 输入`clean`, 回车
    5. 输入`convert mbr`
    6. 关闭该命令行窗口
3. 然后就又回到$W$处, 点击`刷新`

## 系统盘为动态磁盘时如何改为基本盘

1. 备份数据
2. 准备好U盘, 重装系统 ...
3. 至磁盘分区步骤, 按下`Shift+F10`, 依次输入
    1. `diskpart`
    2. `list disk`
    3. `select disk 0` (0, _disk number_)
    4. `detail disk`
    5. `select volume=0` (0, _volume number_)
    6. `delete volume`
    7. `select disk 0`
    8. `convert basic`

## 主机开机后显示器无显示, USB不通电

尝试以下方法

1. 检查显示器连接: 主机和显示器的HDML线是否松动或损坏
2. 检查内存条: 关机断电, 取出内存条, 刮擦金属片并重新安装
3. 释放静电: 关机断电, 长按电源键3次, 每次10秒以上释放静电, 然后重新连接电源开机

## Edge浏览器无法登陆

1. 设置代理为直连
2. `Win+R`打开
    1. `网络和Internet`
    2. `代理`
    3. 手动设置代理 => `设置`
    4. 使用代理服务器 => `关` => `保存`
3. 重新登陆即可

## References

1. [最新Win11系统怎么删除开机密码Win11取消登录密码图文教程-知乎.html](https://www.yuque.com/attachments/yuque/0/2023/html/22048361/1699451571910-40719255-2a0b-4a4b-9763-78202d1769b9.html)
2. [Windows无法安装到这个磁盘选中的磁盘具有MBR分区表-知乎.html](https://www.yuque.com/attachments/yuque/0/2023/html/22048361/1699453574988-cb076f67-e5a7-49be-822f-9cb31c4631d5.html)
