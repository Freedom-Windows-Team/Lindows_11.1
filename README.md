# **Lindows 11.1** 
##  

提示：Lindows 11.1 尚未完工，此文档仅起到预告的作用。开发过程中随时可能会对功能进行增减，请以最终成品为准。

```======================================================================================================================```

Windows中的种种限制让你感到不满？

没关系，我会出手！


由本人精心研制的Lindows 11.1完美破解了Windows中众多令人火冒三丈的霸道行为！给予电脑的使用者对其设备的绝对掌控权！

在拥有Windows的简单易用与强大的软件生态的同时，又拥有Linux的自由开放。

# 修改内容：

## 1. 真正的永久禁用驱动程序签名强制
![Screenshot 2023-08-27 151259](https://github.com/Freedom-Windows-Team/Lindows_11.1/assets/143358583/b9d0a844-b753-42eb-a90a-f9f644e0f1fb)

未签名的驱动程序不让安装？岂有此理？？？

本驱动程序100%无毒无害。我说的！

为何不让安装？

如此粗暴无理地认为所有没有数字签名的程序都有害简直是这个世界上最最愚蠢的事情。

反过来说，所有签了名的驱动就都一定安全吗？

这辈子从未见过比这更智障的设定。

我受不了了，我IDA动了。

经过上百小时的资料查询和反复的修改测试，过程中蓝屏超过50次，卡Logo10次，“正在准备自动修复”我见了不下20回！

现在，Lindows 11.1终于能够正常加载任何未签名的驱动以及未签名的系统内核啦！

从现在起，我的电脑我说了算！加载未签名驱动谁也别想拦我。

## 2. 真正的无条件开启wifi热点！
![Screenshot 2023-08-27 161337](https://github.com/Freedom-Windows-Team/Lindows_11.1/assets/143358583/1982e92d-dd62-43ca-8bd9-15625470a8e5)
![Screenshot 2023-08-27 161246](https://github.com/Freedom-Windows-Team/Lindows_11.1/assets/143358583/e759a80c-bfc9-4a8f-8233-d8d5178f71d0)

我本以为热点是必须要有网络连接才能开的，直到我有一次偶然间发现这个热点居然只要开启的一瞬间有网就OK！

开启之后再断开网络连接对热点没有影响！

且在搜寻了一些资料后得知这居然是微软人为加的限制。

我顿时火冒三丈，热点没有网络连接又咋滴？

局域网联机打游戏传文件不行吗？

尝试使用IDA修改系统文件却发现极为复杂的代码使我无从下手。

经过我的苦苦搜寻，终于让我发现了一个能够绕过这个限制强制开启热点的宝藏小工具！

在此大力感谢由True Software开发的My Public Wifi，使这一限制的破除成为可能！https://mypublicwifi.com/publicwifi/en/index.html

## 3. 可连接128人的超级强力永不宕机热点！
![image](https://github.com/Freedom-Windows-Team/Lindows_11.1/assets/143358583/8f5d0280-bbaf-431a-a4d9-af8faa030cf6)

经过我的不断钻研，终于成功通过修改注册表实现了最多可连接128人的超强wifi热点！

同时，我还完全禁用了热点无人连接或无internet访问时自动关闭的智障机制。

除非手动关闭，否则热点将与Windows同尽！
只要电脑依然处在开机状态，热点就永远不会断开连接！

做到了真正的永不宕机！

## 4. 杀系统进程不蓝屏！

Windows为了不让用户杀掉系统关键进程也是用心良苦啊！

杀完立即蓝屏。

然而通过修改系统文件的方式去除这个限制并不是一个好的打算，因为很多批处理作者都喜欢用这种方式手动触发蓝屏。

大家熟知的典中典一键光速蓝屏代码就是利用的这个原理：
```
wmic process where name="wininit.exe" delete
wmic process where name="smss.exe" delete
wmic process where name="svchost.exe" delete
wmic process where name="csrss.exe" delete
```
所以，如果我们完全干掉了杀系统进程蓝屏的机制，那所有利用这个机制实现手动触发蓝屏的批处理代码将全部无法正常运行！

正在我一筹莫展之际，好心的任务管理器TSK为大家提供了一个使用极为便捷的小工具：Notcritical.exe！https://space.bilibili.com/102499223

它可以方便快捷地将系统进程修改成普通进程，也可以把普通进程设置成系统进程。

只要用上它简单修改一下进程类型就能够完美做到杀死系统关键进程且不蓝屏了！

同时，利用杀系统进程实现手动触发蓝屏的批处理代码也都能正常运行。

## 5. 可使用RDP远程登陆无密码或密码为空的账户！

已通过修改组策略实现使用RDP远程登陆无密码账户。

此选项开箱立即生效无需手动设置！

## 6. 直接双击就能安装任何未签名的UWP应用！

众所周知，使用powershell命令可以安装未签名的UWP应用。
但这个方法还是太过繁琐。

直接给它设置个文件关联，双击就自动调用powershell绕过签名校验，岂不是更好？

## 7. 开箱默认允许执行未签名powershell脚本！

在powershell中输入命令可以设置允许执行未签名的脚本。
但是设置的过程很繁琐且极易踩坑。

为了简化这一过程，我索性直接在系统封装前把这个选项配置好，让用户少走弯路。

## 8. 完全卸载坑死人不赔钱的Windows Defender！

windows defender从不会在处理危险项目前询问用户的意见，且误报率极高！

更令人头疼的是想要卸载它简直是比登天还难！

经过我的不断钻研，终于让我发现了一个能够彻底干掉它的方式！

现在终于能够彻底摆脱掉这个烦人的家伙了！

## 8. 严禁在用户不知情的情况下发送任何调试数据给任何人！

Windows 11 总是喜欢在后台偷偷发各种调试数据给各个厂商。
且先不谈拖慢系统运行速度，这样的行为是对用户隐私极大的不尊重！

如果你使用网络监控软件进行监视，你会发现windows在你完全没有进行任何网页浏览的情况下偷偷地在网上传输了大量的数据！

大力感谢The PC Security Channel为众人揭露了这一细思极恐的秘密以及关键修改方案！https://youtu.be/IT4vDfA_4NI

## 9. 可加载第三方主题文件！

破解第三方主题，为第10项修改开路！

## 10. 顶级系统界面美化！

有和Linux一样的自由，同时也要有和Linux一样诱人的系统界面！

在此大力感谢Rectify 11为Lindows提供极为惊艳的系统主题。https://github.com/Rectify11/Installer

感谢Stardock开发的神器WindowFX给予Lindows 11.1极为诱人的窗口动画效果。https://www.stardock.com/products/windowfx/

## 11. 与Linux相媲美的超快运行效率！

我使用Rectify 11 2.5版本的镜像作为底板进行修改https://archive.org/details/Rectify11。

该镜像对windows中众多不必要的组件进行了精简，大幅提高系统运行效率。

我自己没有任何windows精简优化的经验，什么能删什么不能删我都不知道。
一旦删错便会导致各种难以挽回的错误。

因此我便挑了一个精简优化做的很优秀的现成品来做二次加工。

若Rectify 11团队对我这样的行为有任何意见请在github上提交issue告诉我，我收到后将会把相关资源下架。

# 软件开发相关
**若您想为Lindows 11.1开发软件，请仔细阅读本段内容**

在Lindows 11.1中做软件开发必然会比Windows轻松很多，少了很多烦人的限制。

尤其是对UWP或驱动的开发者而言。

但以此带来的副作用便是你将无法在任何其他基于NT技术构建的操作系统上运行你的程序。

所有使用你的软件的客户也都要安装Lindows 11.1

所以，为防止有人向你反馈诸如“做了套UI骗人的，散了散了。”之类的内容，你需要在安装程序中添加一个检测模块。

在检测到用户使用的不是Lindows 11.1时自动打开此Github仓库引导用户下载安装正确的操作系统来运行你的软件。

**注意：以下是重要的内容！**

在Lindows 11.1中，应用程序的安装包均以*.BAT的格式存储。

若要制作这样的安装包，请遵循以下步骤：

1. 将你的软件压缩进一个或多个*.zip压缩包。
2. 右键点击这个压缩包，在发送到……中找到Convert to BAT选项。
3. 在弹出一个深蓝色背景的窗口中勾选上Long Lines选项，除此之外的全部取消勾选，然后点击OK。
4. 右键生成的BAT文件选择编辑，你将会看到如下的代码：
   ![image](https://github.com/Freedom-Windows-Team/Lindows_11.1/assets/143358583/825a701b-e2ab-421b-b8cf-1a191585ad81)
5. 在第三行添加上Powershell Expand-Archive -LiteralPath [压缩文件名称] -DestinationPath [解压路径]
6. 若要添加Lindows检测器，请在第一行之后插入下列代码：
   ```
   检测模块尚未完工
   ```
7. 若有必要，可选择在第三行之前执行创建开始菜单快捷方式，控制面板卸载条目等操作。
   ```
控制面板添加卸载条目：
REG ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\Program_ID" /v DisplayName /t REG_SZ /d "My Program" /f
REG ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\Program_ID" /v DisplayVersion /t REG_SZ /d "v1.0" /f
REG ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\Program_ID" /v UninstallString /t REG_SZ /d "C:\Path\To\Uninstaller.bat" /f
REG ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\Program_ID" /v DisplayIcon /t REG_SZ /d "C:\Path\To\Icon.ico" /f
REG ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\Program_ID" /v NoModify /t REG_DWORD /d 0 /f
REG ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\Program_ID" /v ModifyPath /t REG_SZ /d "C:\Path\To\RepairTool.bat" /f

添加快捷方式：
echo.[InternetShortcut] >"C:\ProgramData\Microsoft\Windows\Start Menu\Programs\My Program\Program.URL"
echo.URL=C:\Path\To\Program.exe >>"C:\ProgramData\Microsoft\Windows\Start Menu\Programs\My Program\Program.URL"
echo.IconIndex=0 >>"C:\ProgramData\Microsoft\Windows\Start Menu\Programs\My Program\Program.URL"
echo.IconFile=C:\Path\To\Program.exe >>"C:\ProgramData\Microsoft\Windows\Start Menu\Programs\My Program\Program.URL"
```

关于修复与卸载的批处理脚本可以用Ibat界面上方的快速启动中的ECHO generator工具进行转换。

用记事本批量查找替换‘&@ECHO.’为‘>>"C:\Path\To\Uninstaller.bat"&@ECHO.’。

把文件中出现的首个‘>>"C:\Path\To\Uninstaller.bat"&@ECHO.’替换成‘>"C:\Path\To\Uninstaller.bat"&@ECHO.’。

在文件末尾添加‘>>"C:\Path\To\Uninstaller.bat"’，注意不要换行。

随后直接将代码粘贴进安装程序即可。

需要注意的是批处理有单行文本长度限制，超出限制的部分将不会被读取。

若出现转换后无法正常回写的状况，请尝试将所有的‘&@ECHO.’替换成‘\n@ECHO.’。

# 注意事项
