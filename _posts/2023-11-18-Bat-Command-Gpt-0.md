---
title: 使用GPT和New Bing制作简单的提高效率的BAT脚本命令
author: mordecaimaic
date: 2023-11-18 15:30:00 +0800
categories: [Chatgpt使用]
tags: [chatgpt, bat]     # TAG names should always be lowercase
image:
  path: /assets/images/chatgpt/chatgpt_cover.png
  alt: chatgpt_cover
---
# 场景需求
由于shadowrocket可以通过热点来分享代理，可以实现了使用shadowrocket来进行热点共享代理。

可以把一台开着shadowrocket代理的iphone手机，将代理功能分享给windows。但是由于有时候不需要用到代理，就需要在电脑的设置里面收到代理设置，有点麻烦。

所以想到了利用chatgpt来帮我写一个脚本，只需要点击鼠标，就可以实现代理的开关。

由于之前没有接触过像windows的一些脚本命令，所以对这方面并不是非常熟悉，但是我大概知道有一些类似Bat的命令，可以通过操作windos的注册列表，来修改系统设置。但是我对这类文件里面具体的语法，以及实现细节，并不了解，所以希望chatgpt给我帮忙。
# 询问chatgpt
我对chatgpt的最开始提出的问题是
``我要现在需要经常手动开关windows系统里面的手动代理设置，是一个具有重复性而且麻烦的功能，可以帮我写一个脚本程序，帮我实现这个网络代理开关的功能吗``

gpt认为，要实现这个功能，大概有三种方案
1.  PowerShell 脚本 (.ps1)
2.  Batch 文件 (.bat)
3.  VBScript 文件 (.vbs)

## Powershell脚本
然后chatgpt给我生成了一段代码，让我把这段代码保存并把后缀改成.ps1的文件，但是并不能够运行。
我并没有接触过这类型的脚本，在这里介绍一下powershell：
> PowerShell 是由 Microsoft 开发的一种命令行工具和脚本语言，用于在 Windows 操作系统上进行自动化任务和系统管理。它提供了强大的功能，允许用户通过命令行或脚本执行各种操作，包括文件管理、系统配置、网络设置等。PowerShell 使用直观的命令和脚本语法，使得用户能够更轻松地管理和自动化计算机任务

在多次尝试不成功后，我让gpt更换了一个给我写了一个bat脚本
## Bat文件
在这里介绍一下Bat文件，它是在windows系统里面非常有用，并且可以大提高工作效率的一类文件，可以帮助我们进行自动化工作。只需要将bat代码保存在.bat文件即可运行。

> Batch 文件（.bat）是一个批处理文件，是包含一系列计算机命令的文本文件。这些命令按照文件中的顺序执行，允许用户自动化和批量执行任务。批处理文件通常用于 Windows 系统，其命令语法简单，适用于执行基本的系统和文件操作。通过编辑和运行批处理文件，用户可以轻松地完成一系列计算机任务，而无需手动逐一输入每个命令。
> 
> 它是用于 Windows Command Prompt (cmd.exe) 的脚本文件。因此，.bat 文件主要与 Command Prompt（cmd）工具关联。
> 
> Batch 文件包含一系列命令，这些命令按顺序执行，允许用户自动化和批量执行一系列 Windows 命令。Batch 文件通常用于执行文件操作、系统配置、网络设置等基本任务。

```bat
@echo off
setlocal enabledelayedexpansion

rem 获取当前代理状态
reg query "HKCU\Software\Microsoft\Windows\CurrentVersion\Internet Settings" /v ProxyEnable > nul 2>&1
if %errorlevel% equ 0 (
    set /a "currentValue=1"
) else (
    set /a "currentValue=0"
)

rem 切换代理状态
if !currentValue! equ 1 (
    rem 代理是打开的，关闭代理
    reg add "HKCU\Software\Microsoft\Windows\CurrentVersion\Internet Settings" /v ProxyEnable /t REG_DWORD /d 0 /f > nul 2>&1
    echo 网络代理已关闭。
) else (
    rem 代理是关闭的，打开代理
    reg add "HKCU\Software\Microsoft\Windows\CurrentVersion\Internet Settings" /v ProxyEnable /t REG_DWORD /d 1 /f > nul 2>&1
    echo 网络代理已打开。
)

rem 刷新网络设置
netsh winhttp reset proxy > nul 2>&1

pause

```
但是似乎并不能运行，运行这个文件的时候，只能将网络代理关闭，但是并不能打开。我现在也没有弄清楚为什么不能执行开启代理的功能

# 使用New Bing
在尝试询问gpt虽然的到了解决方案，但是没有得到具体的解决途径的时候，又苦于没有研究过cmd和bat的基础语法，我转而想到了询问bing。
bing一开始给我的解决方案就是使用，bat命令行。经多几轮询问和代码优化后，我得到了想要的结果
```bat
@echo off
setlocal enabledelayedexpansion
rem 设置窗口大小为80列，25行
mode con cols=80 lines=25
rem 设置窗口标题为“Network Proxy Switch”
title Network Proxy Switch
rem 设置窗口字体颜色为白色，背景颜色为黑色
color f0
rem 获取代理设置的值
for /f "tokens=3 delims=: " %%a in ('REG QUERY "HKCU\Software\Microsoft\Windows\CurrentVersion\Internet Settings" /v ProxyEnable ^| find /i "ProxyEnable"') do (
  set "value=%%a"
)
rem 如果值为0，则开启手动设置代理
if "!value!"=="0x0" (
  reg add "HKCU\Software\Microsoft\Windows\CurrentVersion\Internet Settings" /v ProxyEnable /t REG_DWORD /d 1 /f >nul 2>nul
  echo Manual proxy setting is enabled
  rem 延时5秒
  ping -n 5 127.0.0.1 >nul
  rem 关闭窗口
  exit
)
rem 如果值为1，则关闭手动设置代理，但不清空代理地址和端口号
if "!value!"=="0x1" (
  reg add "HKCU\Software\Microsoft\Windows\CurrentVersion\Internet Settings" /v ProxyEnable /t REG_DWORD /d 0 /f >nul 2>nul
  echo Manual proxy setting is disabled
  rem 延时5秒
  ping -n 5 127.0.0.1 >nul
  rem 关闭窗口
  exit
)
```
将代码保存到.bat文件里里面，即可使用。

其中，最核心的语句是和注册列修改有关的。
例如下面这个语句的命令作用，是开启系统网络代理。
``reg add "HKCU\Software\Microsoft\Windows\CurrentVersion\Internet Settings" /v ProxyEnable /t REG_DWORD /d 1 /f >nul 2>nul
``

# 代码解释
如果想了解一下bat具体的语法以及实现，可以参考下面的解释
> 以下Bat代码的解释为AI生成
{: .prompt-info }
- reg add是一个命令，用于添加注册表的值。
- "HKCU\Software\Microsoft\Windows\CurrentVersion\Internet Settings"是一个键路径，指定要添加的子项或条目的完整路径。HKCU是HKEY_CURRENT_USER的缩写，表示当前用户的配置信息。
- /v ProxyEnable是一个选项，指定要添加的键值的名称。ProxyEnable是一个控制网络代理是否启用的键值。
- /t REG_DWORD是一个选项，指定要添加的键值的类型。REG_DWORD是一个32位的二进制数，可以用十六进制或十进制表示。
- /d 1是一个选项，指定要添加的键值的数据。1表示启用网络代理，0表示禁用网络代理3。
- /f是一个选项，用于强制覆盖现有的键值，不会提示用户确认。
- nul 2>nul是一个重定向符号，用于把输出结果重定向到空设备，不会在屏幕上显示任何信息。