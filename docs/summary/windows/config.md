# Config

## 视觉效果配置

### 调整最佳性能

1. `Win+R`运行`SystemPropertiesPerformance.exe`
2. 点击`调整为最佳性能`, 再点击`自定义`
3. 依次勾选
    * `平滑屏幕字体边缘`
    * `拖动时显示窗口内容`
    * `显示缩略图, 而不是显示图标`
4. 点击`应用`

### 调整个性化

1. 桌面右键单击`个性化`
    * `顔色`
    * `透明效果`=>`关`

## 右键菜单

* 恢复 win10 右键菜单

    ```powershell
    reg add "HKCU\Software\Classes\CLSID\{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}\InprocServer32" /f /ve
    taskkill /f /im explorer.exe & start explorer.exe
    ```

* 恢复 win11 右键菜单

    ```powershell
    reg delete "HKCU\Software\Classes\CLSID\{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}" /f
    taskkill /f /im explorer.exe & start explorer.exe
    ```

## 登陆密码自动输入

1. `win + i` 打开 `设置`
=> `账户`=> `登陆选项`
=> `其他设置` => `为了提高....Windows Hello 登录(推荐)` => `关`
2. `win + r` 运行 `netplwiz` (Network Places Wizard)
 => <u>取消</u>勾选 `要使用本计算机, 用户必须输入用户名和密码`
=> 点击 `应用`
=> 弹出自动登陆提示框
=> 输入 $ Microsoft $**微软账户**的 `用户名(登陆邮箱)`和 `密码(登陆密码)`

## 磁盘分区

只能固定分四个盘

| **磁盘** | **名称** | **大小** |
| --- | --- | --- |
| C: | 系统盘 | 30% |
| D: | <font style="color:rgb(38, 38, 38);">数据盘</font> | <font style="color:rgb(38, 38, 38);">10%</font> |
| E: | <font style="color:rgb(38, 38, 38);">软件盘</font> | <font style="color:rgb(38, 38, 38);">30%</font> |
| F: | <font style="color:rgb(38, 38, 38);">备份盘</font> | <font style="color:rgb(38, 38, 38);">30%</font> |

* D 盘, F 盘内的所有数据 可随时删除

## 必需目录或文件

### 桌面

| **目录/文件** | **位置** | **来源** |
| --- | --- | --- |
| `Tools` | 行 1 列 中 1 | [https://github.com/gendloop/Tools](https://github.com/gendloop/Tools) |
| `MyRepos` | 行 1 列 中 2 | [https://github.com/gendloop/Tools/tree/main/MyRepos](https://github.com/gendloop/Tools/tree/main/MyRepos) |
| `WorkRepos` | 行 1 列 中 3 | [https://github.com/gendloop/Tools/tree/main/WorkRepos](https://github.com/gendloop/Tools/tree/main/WorkRepos) |
| `Private` | 行 1 列 中 4 | 坚果云盘 同步至本地 |
| `BaiduSyncdisk` | 行 1 列 中 5 | 百度云盘 同步空间 同步至本地 |
| `empty_recycle_bin.bat` | 行 1 列 右 1 | [https://github.com/gendloop/Tools/tree/main/Windows/Desktop](https://github.com/gendloop/Tools/tree/main/Windows/Desktop) |
| `scoop_apps_folder.bat` | 行 1 列 右 2 | [https://github.com/gendloop/Tools/tree/main/Windows/Desktop](https://github.com/gendloop/Tools/tree/main/Windows/Desktop) |
| `del_link.bat` | 行 1 列 右 3 | [https://github.com/gendloop/Tools/tree/main/Windows/Desktop](https://github.com/gendloop/Tools/tree/main/Windows/Desktop) |
| `shutdown.bat` | 行 1 列 右 4 | [https://github.com/gendloop/Tools/tree/main/Windows/Desktop](https://github.com/gendloop/Tools/tree/main/Windows/Desktop) |

### 启动项

| **启动项** | **添加方式** | **来源** |
| --- | --- | --- |
| `<font style="color:rgb(38, 38, 38);">linux-start.vbs</font>` | `<font style="color:rgb(38, 38, 38);">shell:startup</font>` | [https://github.com/gendloop/Tools/tree/main/Windows/StartUp](https://github.com/gendloop/Tools/tree/main/Windows/StartUp) |
| `AutoStartPortProxy` | 任务计划程序 | [https://github.com/gendloop/Tools/tree/main/Windows](https://github.com/gendloop/Tools/tree/main/Windows) |
| `AutoStartSyncthing` | 任务计划程序 | [https://github.com/gendloop/Tools/tree/main/Windows](https://github.com/gendloop/Tools/tree/main/Windows) |
| `AutoStartWifiHotSpot` | 任务计划程序 | [https://github.com/gendloop/Tools/tree/main/Windows](https://github.com/gendloop/Tools/tree/main/Windows) |

### E: 软件盘

* `OthersApps`
* `UserApps`

### F: 备份盘

* `Reflect`
