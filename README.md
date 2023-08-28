# **Lindows 11.1** 

### [Don't speak Chinese? Come over here! ](https://github.com/Freedom-Windows-Team/Lindows_11.1/tree/main#english-readme)


提示：Lindows 11.1 尚未完工，此文档仅起到预告的作用。开发过程中随时可能会对功能进行增减，请以最终成品为准。

**请认准唯一官方下载地址：https://github.com/Freedom-Windows-Team/Lindows_11.1/releases**

**允许任何人以Lindows 11.1为基础制作属于自己的定制版Windows，但是必须在Readme中明确标明使用了我的作品且必须明确告知用户他们下载的文件不是由Freedom Windows Team官方发行的原版Lindows 11.1！**

##  

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

虽然关于这一项修改网上已经有了不少的教程，但这些资料总是东说东的好西说西的好。
你几乎无法找到有哪两篇的步骤是一样的，搬运除外。
最坑的是90%的文章要么过时要么根本没效果纯属随口乱说蹭热度。

没办法，只能把我所能翻到的所有相关资料挨个试一遍了。

同时，还需要对多篇资料的内容进行整合，很多时候某篇漏说的关键信息在另一篇能补回来。

经过上百小时的资料查询和反复的修改测试，过程中蓝屏超过50次，卡Logo10次，“正在准备自动修复”我见了不下20回！

现在，Lindows 11.1终于能够正常加载任何未签名的驱动以及未签名的系统内核啦！

从现在起，我的电脑我说了算！加载未签名驱动谁也别想拦我。

在此感谢所有为我提供帮助的热心网友们！

Fangyzhai：
http://bbs.wuyou.net/forum.php?mod=viewthread&tid=433012
（帮助最大！！！）

菜菜：
https://zhuanlan.zhihu.com/p/590181211

金典教授：
https://www.bilibili.com/read/cv20303238/

hfiref0x的UPGDSED开源项目：
https://github.com/hfiref0x/UPGDSED/blob/master/src/main.c

我自己的最终方案，放出来让各位少走点弯路：
```
在C:\Windows\System32中找到如下的几个文件放入IDA修改
（IDA下载地址：https://www.hex-rays.com/ida-pro）

winload.exe:
ImgpValidateImageHash 函数开头改成 33 C0 C3
OslInitiallizeCodeIntegrity 函数开头改成 B0 01 C3

winload.efi:
ImgpValidateImageHash 函数开头改成 33 C0 C3
OslInitiallizeCodeIntegrity 函数开头改成 B0 01 C3

ntoskrnl.exe：
SeVelidateImageData 将函数内出现的首个mov eax, 0C0000428h改成mov eax, 0
SepInitializeCodeIntegrity 将函数内出现的首个mov ecx, edi改成xor ecx, ecx

打开LordPE并点击PE Editor（https://www.softpedia.com/get/Programming/File-Editors/LordPE.shtml）
选取刚刚修改过的文件中的任意一个
点击Checksum旁边的问号
点击Save
点击OK
对刚刚修改过的剩下两个文件重复上述操作修复校验和

winload.exe和winload.efi还需要复制到C:\Windows\System32\Boot中把那个里面的两个文件也替换掉。
```

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
![image](https://github.com/Freedom-Windows-Team/Lindows_11.1/assets/143358583/2b5a0c71-caf5-46c0-8202-e5fd33ce94de)

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

## 9. 严禁Lindows 11.1在用户不知情的情况下发送任何调试数据给任何人！

Windows 11 总是喜欢在后台偷偷发各种调试数据给各个厂商。
且先不谈拖慢系统运行速度，这样的行为是对用户隐私极大的不尊重！

如果你使用网络监控软件进行监视，你会发现windows在你完全没有进行任何网页浏览的情况下偷偷地在网上传输了大量的数据！

大力感谢The PC Security Channel为众人揭露了这一细思极恐的小秘密并提供了关键修改方案！https://youtu.be/IT4vDfA_4NI

## 10. 可加载第三方主题文件！

破解第三方主题，为第11项修改开路！

## 11. 顶级系统界面美化！

有和Linux一样的自由，同时也要有和Linux一样诱人的系统界面！

在此大力感谢Rectify 11为Lindows提供极为惊艳的系统主题。https://github.com/Rectify11/Installer

感谢神器WindowFX给予Lindows 11.1极为诱人的窗口动画效果。

## 12. 与Linux相媲美的超快运行效率！

我对windows中的很多不必要的组件都进行了精简，大幅提高系统运行效率。

电脑空闲时仅有61个活动进程，内存占用仅仅只有1.3GB。

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
5. 在第三行添加上```Powershell Expand-Archive -LiteralPath [压缩文件名称] -DestinationPath [解压路径]```。
6. 若要添加Lindows检测器，请在第一行之后插入下列代码：
   ```
   检测模块尚未完工
   ```
7. 若有必要，可选择在第三行之后执行创建开始菜单快捷方式，控制面板卸载条目等操作。
```
控制面板添加卸载条目：
REG ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\Program_ID" /v DisplayName /t REG_SZ /d "My Program" /f
REG ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\Program_ID" /v DisplayVersion /t REG_SZ /d "v1.0" /f
REG ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\Program_ID" /v UninstallString /t REG_SZ /d "C:\Path\To\Uninstaller.bat" /f
REG ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\Program_ID" /v DisplayIcon /t REG_SZ /d "C:\Path\To\Icon.ico" /f
REG ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\Program_ID" /v NoModify /t REG_DWORD /d 0 /f
REG ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\Program_ID" /v ModifyPath /t REG_SZ /d "C:\Path\To\RepairTool.bat" /f
```
```
添加快捷方式：
方法1：
echo.[InternetShortcut] >"C:\ProgramData\Microsoft\Windows\Start Menu\Programs\My Program\Program.URL"
echo.URL=C:\Path\To\Program.exe >>"C:\ProgramData\Microsoft\Windows\Start Menu\Programs\My Program\Program.URL"
echo.IconIndex=0 >>"C:\ProgramData\Microsoft\Windows\Start Menu\Programs\My Program\Program.URL"
echo.IconFile=C:\Path\To\Program.exe >>"C:\ProgramData\Microsoft\Windows\Start Menu\Programs\My Program\Program.URL"
方法2：
mklink "C:\ProgramData\Microsoft\Windows\Start Menu\Programs\My Program\Program.exe" "C:\Path\To\Program.exe"

```

关于修复与卸载的批处理脚本可以用Ibat界面上方的快速启动中的ECHO generator工具进行转换。(你可以在开始菜单中找到Ibat）

用Notepad++批量查找替换```&@ECHO.```为```>>"C:\Path\To\Uninstaller.bat"&@ECHO.```。

把文件中出现的首个```>>"C:\Path\To\Uninstaller.bat"&@ECHO.```替换成```>"C:\Path\To\Uninstaller.bat"&@ECHO.```。

在文件末尾添加```>>"C:\Path\To\Uninstaller.bat"```，注意不要换行。

随后直接将代码粘贴进安装程序即可。

需要注意的是批处理有单行文本长度限制，超出限制的部分将不会被CMD读取。

若出现转换后无法正常回写的状况，请尝试将所有的```&@ECHO.```替换成```\n@ECHO.```。

# 注意事项

使用Lindows 11.1之前，请务必确保您已具备基本的手工杀毒能力！

在Windows原本的安全政策被几乎完全破坏的系统中，Lindows 11.1将会拥有比其他任何基于NT技术构建的操作系统更多的安全漏洞。

完全依靠Lindows 11.1自带的一个火绒安全软件肯定是行不通的。

毕竟现在全世界那么多台装了windows的电脑当中有几台是用的Lindows 11.1？

因此，火绒是不可能对Lindows 11.1中额外的安全漏洞做任何准备的！

这些需要你自己去注意防范。

更何况我在Lindows 11.1中内嵌火绒的时候Lindows 11.1还不存在呢！

火绒要是真的要做适配岂不是要拿通过非正当途径泄露出去的Lindows 11.1内部测试版本去做适配？

.

当然，这个问题在Lindows 11.1普及到一定程度之前并不需要过多的担心。

还是那句话，现在全世界那么多台装了windows的电脑当中有几台是用的Lindows 11.1？

因此，也不会有哪个傻瓜黑客为了黑掉个位数级别的windows用户去专门为Lindows 11.1设计病毒程序。

**注意：我说不必过多的担心并不意味着不用担心！！！**

.

**警告：游戏玩家们请注意！**

由于Lindows 11.1修改了许多关键的系统文件，这可能会使你被众多游戏中的反作弊系统屏蔽。

若您的电脑上安装有任何联机游戏，请务必现在虚拟机中测试一下它们在Lindows 11.1中工作的情况，以防止意外发生！

大多数的单机游戏都不会有很变态的反作弊系统，因此如果你跟我一样玩单机游戏比较多那就可以不用担心这个问题了。

# 这是酷的，但它合法吗？

为避免版权相关的问题，本作将以补丁的形式发行，且不会修改windows激活相关的内容。

微软创造了Windows，因此微软持有Windows的著作权，我不去侵犯。

但是这个补丁的著作权，是我的！

应用补丁的方式如下：

先到[这里](https://archive.org/download/windows-11_21h2-22000-318/Windows%2011.iso)下载微软官方原版的Windows 11 21H1镜像。

从release页面下载最新的Lindows 11.1补丁。

将原版windows 11的iso与Patch.bat放置在同一目录下并运行Patch.bat。

稍后你将会获得完整的Lindows 11.1安装镜像。

# 如何在自己的电脑上安装Lindows 11.1

## 方案1：全新安装（推荐）

1. 在开始之前，先去设备管理器中查询电脑所使用的各种硬件的型号，尤其是网卡和显卡。
2. 到网上下载对应的驱动安装包，放在任何除C盘以外的地方。
3. 安装PowerISO。
4. 开始试用的按钮有个烦人的倒计时，软件打开5秒之后才让点击。
   若要跳过，可以先点击Enter registration code，然后再点击输入注册码界面左下角的Continue trial version。
5. 在PowerISO中打开Lindows 11.1的安装镜像。
6. 插入一个空白的U盘。
7. 点击Tools下面的Create Bootable USB Drive。
8. 在Destination里面选择你的U盘。
9. 点击右下角的Start。
10. 等待写入完成。
11. 将电脑关机。
12. 开机的同时狂按F2进入BIOS设置。
13. 用手机搜索你电脑的品牌开启Legacy Boot的方式。
14. 按照教程操作开启Legacy Boot并设置优先使用Legacy模式。（注：本人尚未在UEFI模式中测试过Lindows 11.1的表现，无法确定是否能够正常工作。）
15. 将电脑关机。
16. 开机的同时狂按F12进入启动菜单。
17. 选择从你的U盘启动。（注意避开任何带有UEFI字样的启动条目！）
18. 在看到Press any key to boot from CD/DVD……时，请立即按下键盘上的任意按键。
    具体按哪个按键无所谓，但必须要按，且在这段文字消失以前！
19. 若上述所有步骤均正确执行，此时你将会看到屏幕中间有四个蓝色的方块，且下方有一个白色的小圈圈在转。
    若此时看到的是你的电脑制造商的logo，那说明你在第14步的时候做错了。
20. 稍等片刻，你将进入系统的安装界面。
21. 点击Next。
22. 若你有Windows 11 Pro的密钥，请输入。否则请点击右下角的I don't have a product key。
23. 点击Custom。
24. 找到你C盘所在的分区并将其删除。
25. 找到System Reserved分区（如有）并点击删除。
26. 找到Recovery分区（如有）并点击删除。
27. 选中Unallocated Sapce并点击Next开始安装。
    此时有一定概率可能会出现安装错误。
    不用担心，重启电脑后从第15步开始再做一次就能解决掉90%的安装错误问题。
28. 进入桌面后打开文件资源管理器并找到之前下载好的驱动程序
29. Enjoy！

## 方案2：从Windows升级到Lindows 11.1

1. 从第3步开始跟随上方的全新安装的教程走完第22步以后停下。
2. 点击Upgrade。
3. 等待安装完成。
4. Enjoy！

# 语言设置

Lindows 11.1默认显示语言为英文，但它内置了中文的语言包。

无需另外下载安装，在设置里简单调一下就可以用。

设置中文方法如下：

1. 按下Win+R
2. 输入```ms-settings:```
3. 在左侧点击time and language
4. 点击Language & region
5. 在Windows display language里面选取‘中文（中华人民共和国）’选项
6. 注销并重新登录
7. 完成

设置成其他语言的方法相同

# 镜像大小问题

你主张精简windows，删掉不必要的组件，但为什么Lindows的iso大小比原版还大？
反向精简？？？

为了节省下载安装语言包和输入法的时间，
Lindows 11.1内置了windows中提供的所有语言的语言包和字体文件，就像MacOS一样。

除此之外，我们还内置了不少第三方的应用程序，导致Lindows 11.1的镜像比原版还要大。

但是，与微软捆绑软件时的做法不同的在于我们在捆绑第三方应用的同时又极为重视整个系统的整洁程度。

有大量我认为很好用但并不是这个世界上的所有人都需要的软件均以安装包的形式存放在系统当中。

它们就这样安静地呆在那里，不求不应，有求必应！

且支持一键批量删除，无需用户自己一个一个手动点击。

是不是既方便又快捷？

若有必要，你可以在[discussions](https://github.com/Freedom-Windows-Team/Lindows_11.1/discussions)中留言问我要一个精简版的Lindows 11.1镜像。

# 加入我们

若你想加入Lindows 11.1的开发，请前往[此处](https://github.com/Freedom-Windows-Team/Lindows_11.1/discussions/1)与我们交流。

#  

# English readme: 

Tip: Lindows 11.1 is not yet finished, this document only serves as a preview. Features may be added or removed at any time during the development process, please refer to the final product.

**Please validate the only official download address: https://github.com/Freedom-Windows-Team/Lindows_11.1/releases**

**Anyone is allowed to make their own customized version of Windows based on Lindows 11.1, but they must clearly indicate in Readme that they are using my work and they must clearly inform the user that the file they are downloading is not the original Lindows 11.1 officially released by Freedom Windows Team!**  

##  

Are you frustrated with all those stuped restrictions in Windows?

No problem, I'll step in!

Lindows 11.1, developed by myself, is a perfect hack for the many annoying and overbearing behaviors in Windows! It gives the computer user absolute control over his/her device!

While having the simplicity and powerful software ecosystem of Windows, it also has the freedom and openness of Linux.

## Modifications:

## 1. Real permanent disable of driver signature enforcement!
![Screenshot 2023-08-27 151259](https://github.com/Freedom-Windows-Team/Lindows_11.1/assets/143358583/b9d0a844-b753-42eb-a90a-f9f644e0f1fb)

An unsigned driver is not allowed to be installed? WTF is this?

This driver is 100% harmless. I said that!

Why won't it let me install it?

It is the most stupid thing in the world to assume that all programs that are not digitally signed are harmful in such a rude and irrational way.

On the other hand, are all signed drivers always safe?

I've never seen a more ignorant setup than this in my life.

I can't take it anymore, I want to crack this stuped thing immediately.

Although there have been quite a few tutorials on the internet about this tweak, the information never unite.
You can hardly find any two articles that follow the same steps, except for porting.
The worst part is that 90% of the articles are either outdated or simply have no effect at all.

I had no choice but to try all the relevant sources I could find one by one.

At the same time, it is also necessary to combine the contents of multiple articles, and in many cases, the key information that was omitted in one article can be added back in another.

After hundreds of hours of research and repeated experimenting, Lindows 11.1 is finally able to load any unsigned drivers and unsigned system kernel properly! 

During the process, I got more than 50 BSOD, stuck in bootstraps for more than 10 times, and I met no less than 20 times of "Preparing for automatic repair... "!

From now on, I am the boss of my computer! No one can ever stop me from loading any unsigned drivers.

Many thanks to all netizens who helped me with this!

Fangyzhai：
http://bbs.wuyou.net/forum.php?mod=viewthread&tid=433012
(most helpful!!!)

菜菜：
https://zhuanlan.zhihu.com/p/590181211

金典教授：
https://www.bilibili.com/read/cv20303238/

hfiref0x's UPGDSED open source project:
https://github.com/hfiref0x/UPGDSED/blob/master/src/main.c

My own ultimate solution, put it out for you guys to waste less time:
```
In C:\Windows\System32, find the following files and put them into the IDA for disassembling
(IDA download link: https://www.hex-rays.com/ida-pro)

winload.exe: 
Changed beginning of ImgpValidateImageHash to 33 C0 C3
Changed beginning of OslInitiallizeCodeIntegrity to B0 01 C3

winload.efi: 
Changed beginning of ImgpValidateImageHash to 33 C0 C3
Changed beginning of OslInitiallizeCodeIntegrity to B0 01 C3

ntoskrnl.exe:
Change the first mov eax, 0C0000428h that appears within SeVelidateImageData to mov eax, 0
Change the first mov ecx, edi that appears within SepInitializeCodeIntegrity to xor ecx, ecx.

Open LordPE and click on PE Editor (https://www.softpedia.com/get/Programming/File-Editors/LordPE.shtml)
Select any of the files you have just edited.
Click on the question mark next to Checksum.
Click Save
Click OK
Repeat the above procedure for the remaining two files you've just modified.

winload.exe and winload.efi need to be copied also to C:\Windows\System32\Boot and replace the two files in there as well.
```

## 2. Real unconditional enabling of wifi hotspot!
![Screenshot 2023-08-27 161337](https://github.com/Freedom-Windows-Team/Lindows_11.1/assets/143358583/1982e92d-dd62-43ca-8bd9-15625470a8e5)
![Screenshot 2023-08-27 161246](https://github.com/Freedom-Windows-Team/Lindows_11.1/assets/143358583/e759a80c-bfc9-4a8f-8233-d8d5178f71d0)

I used to believe that a hotspot requires an internet connection in order to turn it on, until once I discovered by accident that the hotspot actually works as long as there was internet access at the moment it was turning on!

Once it's turned on already, disconnecting the network has no effect on the hotspot!

And after some research, I realized that this is actually an artificial restriction added by Microsoft.

I was fired immediately, what does it matter if the hotspot does not have an internet connection?

Can't I just play games and transfer files over the local area network?

I tried to use IDA to modify the system files, but found that the extremely complex code makes me unable to start.

After a lot of research, I finally found a little tool that can bypass this restriction and force the hotspot to be turned on!

A big thank you to My Public Wifi, developed by True Software, for making the breaking of this limitation possible! https://mypublicwifi.com/publicwifi/en/index.html

## 3. A super powerful never-downtime hotspot that can connect up to 128 devices! 
![image](https://github.com/Freedom-Windows-Team/Lindows_11.1/assets/143358583/8f5d0280-bbaf-431a-a4d9-af8faa030cf6)

After my continuous research, I finally managed to achieve a super powerful wifi hotspot that can connect up to 128 users by modifying the registry!

At the same time, I also completely disabled the idiot mechanism that automatically shuts down the hotspot when no one connects to it or when there is no internet access.

The hotspot will finish with Windows unless it is manually turned off!
As long as the computer is still on, the hotspot never disconnects!

## 4. Killing system processes without BSOD!
![image](https://github.com/Freedom-Windows-Team/Lindows_11.1/assets/143358583/2b5a0c71-caf5-46c0-8202-e5fd33ce94de)

Windows is dedicated to preventing users from killing critical system processes!

You will get a BSOD as soon as you killed the process.

However, removing this restriction by modifying system files is not a good idea, because many batch creators like to use this method to manually trigger a BSOD.

This well-known quick one-click BSOD code makes use of this principle:
```
wmic process where name="wininit.exe" delete
wmic process where name="smss.exe" delete
wmic process where name="svchost.exe" delete
wmic process where name="csrss.exe" delete
```
So, if we completely destroy the mechanism that issues a BSOD when a system process are being killed, then all the batch code that makes use of this mechanism to achieve a manually triggered BSOD will all malfunction!

At the time I was stuck, the friendly 任务管理器TSK provides us with a very convenient gadget: Notcritical.exe! https://space.bilibili.com/102499223

It can be used to change a system process to an ordinary process, or change an ordinary process to a system process very easily.

Just use it to modify the process type, then you will be able to perfectly kill the system critical processes without getting a BSOD!

And at the same time, the batch code that achieves manual triggering the BSOD by killing the system processes also works properly.

## 5. RDP can remotely log in to accounts with no or empty passwords!

The option to enable remote login to accounts with no passwords or empty passwords with RDP via Group Policy has been implemented.

This option is available out-of-the-box and does not need to be set manually!

## 6. Install any unsigned UWP apps with just a double-click!

It is well known that you can install unsigned UWP apps via powershell command.
But this method is far too complicated.

Wouldn't it be better if we create a file association for it, and double-click on it will automatically call powershell to bypass the signature check?

## 7. Unsigned powershell scripts are allowed out of the box!
You can allow the execution of unsigned scripts by entering a command in powershell.
But it's very complicated and extremely tricky to set up. 

In order to simplify the process, I simply configured this option before the system is packaged, so that users can take a less complicated path.

## 8. Completely uninstall the pitiful Windows Defender!

windows defender never asks the user's opinion before dealing with dangerous programs and has a very high rate of false positives reporting!

What's more, uninstalling it is a pain in the ass!

After a lot of research, I finally found a methog to get rid of this fucking program!

Now we could finally get rid of it!

## 9. Strictly prohibit Lindows 11.1 from sending any debugging data to anyone without the user's awareness!

Windows 11 always likes to secretly send debugging data to various vendors in the background.
Without mentioning slowing down the system speed, such behavior is extremely disrespectful to the user's privacy!

If you use network surveillance software to monitor, you will discover that windows is secretly transferring a lot of data over the internet while you are not doing any web browsing at all!

Big thanks to The PC Security Channel for lifting the fog on this nifty little secret for the public and providing a great solution for this! https://youtu.be/IT4vDfA_4NI

## 10. Third party theme files can be loaded!

Broken the limit to third-party themes, which have paved the way for the 11th modification!

## 11. Premium system interface beautification!

Have the same freedom as Linux, but also have the same attractive system interface as Linux!

Big thanks to Rectify 11 for providing Lindows with an extremely stunning system theme. https://github.com/Rectify11/Installer

Thanks to WindowFX for giving Lindows 11.1 a very attractive window animation effect.

## 12. A super high efficiency comparable to Linux!

I have stripped down a lot of unnecessary components in windows which had imporved its efficiency dramatically.

There are only 61 active processes when the computer is idle, and the memory usage is only 1.3GB.

# Software development related
**If you want to develop software for Lindows 11.1, please read this section carefully**

Doing software development in Lindows 11.1 is definitely going to be a lot easier than Windows, with a lot less annoying restrictions.

Especially for UWP and driver developers.

However, a side effect of this is that you will not be able to run your program on any other NT-based operating systems.

All customers that use your software will have to install Lindows 11.1 as well!

So, to prevent people from giving you feedback such as, "They've only made a UI for scamming, just forget about it", you need to add a detection module to the installer.

If it detects that the user is not using Lindows 11.1, it will automatically open this Github repository and direct the user to download and install the correct operating system to run your software. 

**Note:** **Heads up, the following content is very important!**

In Lindows 11.1, installation packages for applications are stored in *.BAT format.

To make such an installation package, follow these steps:

1. Compress your software into one or more *.zip archives.
2. Right-click on this zip archive and find the Convert to BAT option in the Send to... menu. 
3. In the dark blue background window that pops up, check the Long Lines box, uncheck everything else, and then click OK.
4. Right click on the generated BAT file and select Edit, you will see the following code:
   ![image](https://github.com/Freedom-Windows-Team/Lindows_11.1/assets/143358583/825a701b-e2ab-421b-b8cf-1a191585ad81)
5. Add ```Powershell Expand-Archive -LiteralPath [zip file name] -DestinationPath [decompression path]``` to the third line.
6. To add the Lindows detector, insert the following code after the first line:
   ```
   Detection module not yet complete
   ```
7. If necessary, you can perform actions such as creating a start menu shortcut, control panel uninstall entry, etc. after the third line.
```
Uninstall entry in control panel：
REG ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\Program_ID" /v DisplayName /t REG_SZ /d "My Program" /f
REG ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\Program_ID" /v DisplayVersion /t REG_SZ /d "v1.0" /f
REG ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\Program_ID" /v UninstallString /t REG_SZ /d "C:\Path\To\Uninstaller.bat" /f
REG ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\Program_ID" /v DisplayIcon /t REG_SZ /d "C:\Path\To\Icon.ico" /f
REG ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\Program_ID" /v NoModify /t REG_DWORD /d 0 /f
REG ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\Program_ID" /v ModifyPath /t REG_SZ /d "C:\Path\To\RepairTool.bat" /f
```
```
Add shortcut：
Method 1：
echo.[InternetShortcut] >"C:\ProgramData\Microsoft\Windows\Start Menu\Programs\My Program\Program.URL"
echo.URL=C:\Path\To\Program.exe >>"C:\ProgramData\Microsoft\Windows\Start Menu\Programs\My Program\Program.URL"
echo.IconIndex=0 >>"C:\ProgramData\Microsoft\Windows\Start Menu\Programs\My Program\Program.URL"
echo.IconFile=C:\Path\To\Program.exe >>"C:\ProgramData\Microsoft\Windows\Start Menu\Programs\My Program\Program.URL"
Method 2：
mklink "C:\ProgramData\Microsoft\Windows\Start Menu\Programs\My Program\Program.exe" "C:\Path\To\Program.exe"

```

Batch scripts about repairing and uninstalling can be converted using the ECHO generator tool in the 快速启动 menu in Ibat at the top. (You can find Ibat in the start menu)

Use Notepad++ to find and replace ```&@ECHO.``` with ```>>"C:\Path\To\Uninstaller.bat"&@ECHO.```.

Replace the first ```>>"C:\Path\To\Uninstaller.bat"&@ECHO.``` that appears in the file with ```>"C:\Path\To\Uninstaller.bat"&@ECHO.```.

Add ```>>"C:\Path\To\Uninstaller.bat"``` to the end of the file, with a caution not to break lines.

Subsequently, just paste the code directly into the installer.

Note that there is a limit on the length of a single line of text in the batch program, and the part that exceeds the limit will not be read by CMD.

If you can't write back properly after conversion, please try to replace all ```&@ECHO.``` with ```\n@ECHO.```.

# Notices

Before using Lindows 11.1, please make sure that you have basic manual malware removal capabilities!

In a system where all Windows's original security policies have been almost completely broken, Lindows 11.1 will have more security vulnerabilities than any other NT-based operating system.

Relying entirely on Huorong Internet Security(火绒安全软件) that comes with Lindows 11.1 is certainly not going to work.

How many of the computers in the world that have Windows installed are using Lindows 11.1?

Therefore, it is impossible for Huorong to make any preparations for the additional security vulnerabilities in Windows 11.1!

You need to take care of these vulnerabilities yourself.

Not to mention that Lindows 11.1 didn't even exist when I embedded Huorong into Lindows 11.1!

If Huorong really wanted to do this adaptation, wouldn't it have to go with an internal beta version of Lindows 11.1 that was leaked in an unorthodox way?

.

Of course, this is not a problem that we need to be worried too much about before Lindows 11.1 becomes popularized to a certain extent.

As I said, how many computers in the world that have Windows installed are using Lindows 11.1?

Therefore, not a single idiot hacker is going to design a malware specifically for Lindows 11.1 in order to hack a single-digit number of Windows users.

**Note:** **When I say don't have to worry too much about it doesn't mean don't worry about it at all!!!**

.

**WARNING:** **Attention for gamers!**

Since Lindows 11.1 modifies many critical system files, this may cause you getting baned by anti-cheat systems in a number of games.

If you have any online games installed on your computer, be sure to test them now in a virtual machine to see how they work in Lindows 11.1 to prevent the unexpected!

Most single player games don't have very strict anti-cheat systems, so if you play a lot of single player games like I do then you can stop worrying about this.

# This is cool, but is it legal?

To avoid copyright related issues, this project will be released as a patch and will not modify any windows activation related content.

Microsoft created Windows, so Microsoft holds the copyright to Windows, which I won't violate.

But the copyright of this patch, is mine!

The way to apply the patch is as follows:

First go [here](https://archive.org/download/windows-11_21h2-22000-318/Windows%2011.iso) to download the official original Microsoft Windows 11 21H1 installation image.

Download the latest Lindows 11.1 patch from the release section.

Place the original windows 11 iso in the same directory with Patch.bat and execute Patch.bat.

After a while, you will obtain the full Lindows 11.1 installation image.

# How to install Lindows 11.1 on your own computer

## Method 1: Fresh Installation (Recommended)

1. Before you start, go to the Device Manager and look for the model of the various hardware used on your computer, especially for your network card and graphics card.
2. Google the corresponding driver installation package and place it anywhere except the C drive.
3. Install PowerISO.
4. Start Trial, but the Start Trial button has an annoying countdown timer and will not let you click it until 5 seconds after the software opens.
   To skip it, click Enter registration code, then click Continue trial version in the lower left corner of the enter registration code screen. 
5. Open the Lindows 11.1 installation image in PowerISO. 
6. Insert a blank USB flash drive.
7. Click Create Bootable USB Drive under Tools. 
8. Select your USB drive in Destination. 
9. Click Start in the lower right corner. 
10. Wait for the writing to complete.
11. Turn off your computer.
12. Press F2 at boot time to enter BIOS setup. 
13. Use your phone to search for how to enable Legacy Boot for your computer's brand. 
14. Follow the tutorial to enable Legacy Boot and configure it to use Legacy mode first. (Note: I have not yet tested the behavior of Windows 11.1 in UEFI mode and cannot be sure if it will work properly.)
15. Turn the computer off.
16. Press F12 at boot time to access the boot menu.
17. Choose to boot from your USB flash drive. (Be careful to avoid any boot entries with the word UEFI in them!)
18. When you see "Press any key to boot from CD/DVD...", press any key on your keyboard immediately.
    It doesn't matter which key you press, but something must be pressed, and before this text disappears!
19. If all of the above steps have been performed correctly, you will see four blue squares in the center of the screen and a small white circle spinning underneath.
    If you see your computer's manufacturer's logo, that means you did something wrong in step 14.
20. Wait a few moments and you will be taken to the system installation screen.
21. Click Next.
22. If you have a Windows 11 Pro key, enter it. Otherwise, click "I don't have a product key" in the lower right corner.
23. Click Custom.
24. Locate the partition where your C drive is located and delete it.
25. Locate the System Reserved partition (if any) and click Delete.
26. Locate the Recovery partition (if any) and click Delete.
27. Select "Unallocated Sapce" and click Next to start the installation.
    In some cases, an installation error may occur.
    Don't worry, reboot your computer and repeat the process from step 15 and you will be able to resolve 90% of these installation errors.
28. Go to your desktop, open File Explorer and find the driver packages that you have downloaded.
29. Enjoy!

## Option 2: Upgrade from Windows to Lindows 11.1

1. Follow the fresh install tutorial above from step 3 and stop after step 22.
2. Click Upgrade.
3. Wait for the installation to complete.
4. Enjoy!

# Language Settings

The default display language of Lindows 11.1 is English, but it has a built-in Chinese language pack.

You don't need to download it separately, just simply adjust it in the settings and you can use it.

To set the language to Chinese, follow the steps below:

1. Press Win+R
2. Type ```ms-settings:```
3. Click on time and language on the left side.
4. Click on Language & region 
5. Select '中文（中华人民共和国）' in the Windows display language.
6. Log out and log in again 
7. Done

Switching to any other languages is done in the same way.

# Image size issues

You claim to simplify windows by removing unnecessary components, but why is the size of the Lindows iso even larger than the original?
A backward simplification?

In order to save time downloading language packs and input methods. 
Lindows 11.1 has got all language packs and font files for all the languages provided in windows built-in, just like macOS.

In addition to that, we have built-in quite a few third-party applications, resulting in a large image that is even larger than the original. 

However, unlike Microsoft's approach of bundling software, we were extremely conscious of the cleanliness of the system while bundling third-party applications.

There's a lot of software that I think is great, but not everyone in the world needs, available as installers in the system.

They just stay there quietly, not asking no answering. 
But once you ask, they respond quickly!

Moreover, it supports batch deletion with a single click, so users don't need to manually click on them to remove them one by one.

Isn't it convenient?

If necessary, you can leave a message in [discussions](https://github.com/Freedom-Windows-Team/Lindows_11.1/discussions) to ask me for a compact version of Lindows 11.1 image.

# Join us

If you want to join the development of Lindows 11.1, please come over [here](https://github.com/Freedom-Windows-Team/Lindows_11.1/discussions/1) to communicate with us.
