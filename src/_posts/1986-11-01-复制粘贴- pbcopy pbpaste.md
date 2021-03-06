---
layout: post
title: "复制粘贴: pbcopy pbpaste"
tags: CLI
categories: Tooles
---




*pbcopy 接受命令行中的标准输出 作为剪切板的内容.*
*pbpaste 将剪贴板中的内容输出到标准输出.*



读取&写入 系统剪切板的目录. 
支持 Unix管道操作: 
- `ls ~ | pbcopy //  复制所有用户目录下的文件`
- `pbcopy < blog.txt // 复制 blog.txt 里面的内容 而不是blog.txt.`








`pbpaste|sed -e 's#^# #'|awk '1; BEGIN {print "  "}'|awk '1; END {print "  "}'|awk '1; END {print " {:.language-ruby}"}'|pbcopy`





pbcopy   复制
pbpaste  粘贴






**open ** *open 打开文件/目录/应用.  也就是命令行里面的双击.*
对目录使用open会在直接将你带到该目录所在的Finder窗口。使用open进去到当前的目录非常地有用。

请记住Finder和终端之间的一体化是双向的—如果你把Finder中的文件拖拽到终端中，在命令行中会粘贴出文件的完整路径



打开程序
- `open /Applications/Safari.app/`
- `open /Applications/zsh.app`

打开照片
- `open /Users/v/Desktop/HHKB.jpg`

用特定程序打开 -a
- `open /Users/v/Desktop/HHKB.jpg -a /Applications/Preview.app`


用TextEdit 直接编辑文件
- `open /Users/v/Desktop/test.js -e`








**pbcopy pbpaste**
这两个命令能让你从命令行中复制和粘贴文本
也就是说这两个命令得益于管道、重定向，并能在脚本中与其他命令一起使用.


`ls ~ | pbcopy`
…home目录中的所有文件复制到剪切板中。


使用pbcopy和管道是获得命令输出的一种很棒的方式，而不用滚动到上面再小心地来选择。
$ pbpaste \>\> tasklist.txt




**mdfind**
古老是find目录.
但是 mac 自带的 杀手级搜索工具 spotlight .

mdfind带来了一些便利，这使得它比那些老的命令更杰出。例如，使用-onlyin标识可以限制只搜索单个目录：
`mdfind -onlyin ~/Documents essay`

mdfind数据库应该在后台更新，但是你也可以使用mdutil（还有Spotlight）分析解决问题。如果Spotlight没有正常工作，mdutil -E将删除索引，并重头开始创建。你也可以使用mdutil -i完全关闭索引。







**screencapture**
可以获得多种不同类型的截图。
它类似于Grab.app和快捷键cmd+shift+3和cmd+shift+4，可是它更加的灵活。


`$ screencapture -C -M image.png`
用鼠标选择一个窗口，然后捕获它的内容不带窗口的影子，并把图像复制到剪切板上：

`$ screencapture -c -W`
延迟10秒后捕获屏幕，并在预览中打开新的图像：

`$ screencapture -T 10 -P image.png`
用鼠标选择屏幕的一部分，捕获它的内容，然后保存为pdf：

`$ screencapture -s -t pdf image.pdf`
要查看更多选项，输入screencapture —help








**launchctl**
让你与OS X初始化脚本launchd交互，用启动守护进程和启动代理，你可以控制开机时的启动服务。你甚至可以设置脚本定期执行或者每隔一段时间后在后台运行，类似于Linux中的计划任务。



例如，如果你想Apache服务器在你打开电脑时自动启动，只要简单的输入如下：

$ sudo launchctl load -w
/System/Library/LaunchDaemons/org.apache.httpd.plist


运行launchctl list会展示出当前加载的启动脚本。sudo launch unload [path/to/script]()将会停止并卸载正在运行的脚本，添加-w标识将从启动序列中永久删除这些脚本。我想要在Adobe软件和Microsoft软件创建的所有自动升级“助手”上运行一次。


Launchd脚本存储在下面的位置：
	~/Library/LaunchAgents  
	/Library/LaunchAgents        
	/Library/LaunchDaemons
	/System/Library/LaunchAgents
	/System/Library/LaunchDaemons






**say**
say把文本转换成语音，它使用OS X给VoiceOver使用的TTS引擎。没有任何选项，say仅仅是地读出你输入的内容：


`say "Never trust a computer you can't lift."`
say命令可以用于代替控制台日志和警告声音。例如，你可以设置Automator脚本或Hazel脚本进行批文件处理，然后用say提示任务已完成。
但是say最有意思的应用相当地邪恶：如果你用ssh来访问朋友或同事的Mac，你可以默默地登录他们的机器并通过命令行干扰他们。给他们一个Siri的惊喜。
通过改变系统偏好设置中的听写与语音的默认设置，你可以改变say的声音和语言！







**brew**

brew使你能很容易接触到上千个开源社区免费的实用工具和插件。例如，brew install imagemagick将会帮你配置好ImageMagick，一个非常强大的实用工具，从播放gif动画到几十种不同类型图片之间的转换它都能完成。brew install node将为你安装NodeJS，它是时下非常流行的开发和运行服务器端JavaScript应用的工具。
你也可以这样使用Homebrew：brew install archey将会为你安装Archey，一个很酷且轻量级的脚本，它可以在一个彩色的苹果logo旁边显示出你Mac的规格。













`echo "hello\nworld"`
输出两行内容到 终端.  换行符号 n

`➜  Desktop echo "hello\nworld" | sed 's/^/ /; 1{x;p;x;}; $G; 1s/^$/ /; $s/^$/ /'`

hello
world

`➜  Desktop echo "hello\nworld" | sed 's/^/ /; 1{x;p;x;}; $G' | sed '1s/^$/ /; $s/^$/ /'`
	hello
	world


`➜  Desktop echo "hello\nworld" | sed 's/^/ /; 1{x;p;x;}; $G' | sed '1s/^$/ /; $s/^$/ /' | sed '$G' | sed '$s/^$/ {: .language-ruby}/'`

{: .language-ruby}




KM 里实际运行的 脚本
1. 按 ⌘C 进行复制
2. 运行下面脚本
`pbpaste | sed 's/^/ /; 1{x;p;x;}; $G' | sed '1s/^$/ /; $s/^$/ /' | sed '$G' | sed '$s/^$/ {: .language-ruby}/' | pbcopy`




## 问题: 中文变成乱码.
其实是 编码问题...
解决方法
















