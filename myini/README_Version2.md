## 选项：

按下对应的数字/字母键来更改选项

**1.** 目标  
目标 Windows 镜像，默认为当前在线系统  
如果脚本旁边有 wim 文件可用，它将被自动检测

**2.** 更新  
更新文件的位置

**3.** DISM  
自定义 dism.exe 的路径  
当当前主机操作系统低于 Windows NT 10.0 且未安装 ADK 时需要

**4.** 启用 .NET 3.5  
处理或跳过启用 .NET 3.5 功能

**5.** 清理系统镜像：是      **6.** 重置镜像基础：否  
在此选项中，操作系统镜像将被清理，已取代的组件将被"增量压缩"  
安全操作，但可能需要很长时间才能完成

**5.** 清理系统镜像：是      **6.** 重置镜像基础：是  
在此选项中，操作系统镜像将被重新设置基础，已取代的组件将被"删除"  
快速操作并进一步减少大小，但可能会破坏"重置此电脑"功能

**7.** 更新 WinRE.wim  
仅当目标是分发文件夹或 WIM 文件时可用  
启用或禁用在 install.wim 中更新 winre.wim

**7.** 选定的 Install.wim 索引  
仅当目标是分发文件夹或 WIM 文件时可用  
选择从 install.wim 更新特定索引或默认所有索引的选项

**K.** 保留索引  
仅当您在上述选项 8 中选择了特定索引时可用  
重建 install.wim 时仅保留选定索引或保留所有索引的选项

**M.** 挂载目录  
仅当目标是分发文件夹或 WIM 文件时可用  
用于更新 wim 文件的挂载目录，默认与脚本在同一驱动器上

**E.** 提取目录  
临时提取文件的目录，默认与脚本在同一驱动器上

## 配置选项（适用于高级用户）：

- 编辑 W10UI.ini 以更改主要选项的默认值：  
> Target（目标）  
Repo（存储库）  
DismRoot（DISM 根目录）  
Net35（.NET 3.5）  
Cleanup（清理）  
ResetBase（重置基础）  
WinRE（WinRE）  
_CabDir（CAB 目录）  
MountDir（挂载目录）

或在下方设置额外的手动选项：

* Net35Source  
指定包含 microsoft-windows-netfx3-ondemand-package.cab 的自定义"文件夹"路径

* ResetBase  
首先需要启用清理功能  
对于版本 26052 及更高版本，更改为 2 以在每个 LCU 后运行重新设置基础

* LCUwinre  
即使检测到 SafeOS 更新，也强制使用累积更新更新 winre.wim  
对于版本 22000-26050 自动启用，更改为 2 以禁用  
对于版本 26052 及更高版本被忽略并自动禁用

* LCUmsuExpand  
扩展累积更新并通过 update.mum 从松散文件安装，而不是直接添加 msu 文件  
仅适用于版本 22621 及更高版本  
对于版本 26052 及更高版本自动启用，更改为 2 以禁用

* UpdtBootFiles  
从累积更新更新 ISO 启动文件 bootmgr/bootmgr.efi/efisys.bin  
如果检测到，这也将更新新的 UEFI CA 2023 启动文件。有关详细信息，请参阅 KB5053484  
注意：如果此选项为"关闭"，两个默认文件 bootmgr.efi/bootmgfw.efi 将被更新

* SkipEdge  
1 = 不随启用包或累积更新安装 EdgeChromium  
2 = 替代解决方案仅跳过累积更新中的 EdgeChromium

* SkipWebView  
不随累积更新安装 Edge WebView

* wim2esd  
如果目标是分发文件夹，将 install.wim 转换为 install.esd  
警告：该过程将消耗大量的 CPU 和 RAM 资源

* wim2swm  
如果目标是分发文件夹，将 install.wim 分割成多个 install.swm 文件  
注意：如果 wim2esd/wim2swm 都为 1，install.esd 优先于分割的 install.swm

* ISO  
如果目标是分发文件夹，创建新的 iso 文件  

* ISODir  
iso 文件的文件夹路径，留空以在脚本当前目录中创建

* Delete_Source  
创建更新的 ISO 后保留或删除 DVD 分发文件夹

* AutoStart  
执行脚本后自动启动进程  
该选项也会在末尾自动退出而不提示

* UseWimlib  
检测并使用 wimlib-imagex.exe 导出 wim 文件，而不是 dism.exe

* WimCreateTime  
更改 install.wim 镜像创建时间以匹配最后修改时间  
此选项需要 wimlib-imagex.exe，但不需要启用 UseWimlib 选项本身

* AddDrivers  
将驱动程序添加到 install.wim 和 boot.wim / winre.wim  
> 这是基本功能支持，应仅与经过测试的兼容驱动程序一起使用  
它用于简单和启动关键驱动程序（芯片组、磁盘控制器、LAN/WiFi..），以便于安装，不适用于大型驱动程序或可能破坏设置的驱动程序  
它不会检查或验证驱动程序，只是指向 DISM 的驱动程序文件夹

使用方法：

启用"AddDrivers"选项

将要添加的驱动程序放在适当的子文件夹内：  
> ALL   / 驱动程序将添加到所有 wim 文件  
OS    / 驱动程序将仅添加到 install.wim  
WinPE / 驱动程序将添加到 boot.wim / winre.wim

* Drv_Source  
可选，为驱动程序指定不同的源文件夹路径  
该文件夹必须包含每个驱动程序目标的子文件夹，如上所述

- 注意：不要更改 W10UI.ini 的结构，只需在等号`=`后设置选项

- 要恢复旧行为并通过编辑脚本来更改选项，只需删除 W10UI.ini 文件

## 调试模式（适用于高级用户）：

* 创建集成过程的日志文件用于调试目的

* 在此模式下不会显示操作进度

* 使用方法：  
> 编辑脚本并将 set _Debug=0 更改为 1  
正确设置主要手动选项，特别是"target"和"repo"  
保存并以管理员身份运行脚本  
等待命令提示符窗口关闭并创建 W10UI_Debug.log
