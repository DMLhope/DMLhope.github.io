---
layout: post
title: deb包管理内容汇总
date: 2021-03-03
categories: note deb package
tags: deb package
cover: '../../../assets/img/20210303.jpg'
---

# 一、dpkg包管理器
dpkg是Debian系列发行版通用的软件包管理器，是apt、aptitude、gdebi、synaptic等软件包管理器的后端，它主要用于安装并管理本地的软件包。
## 1、安装软件包
`# dpkg -i 文件` 或 `# dpkg --install 文件`   
*安装本地软件包时推荐使用apt install代替dpkg -i，因为他可以自动修正依赖关系，请注意apt install后面跟的必须是文件的路径而不能只是文件名*
## 2、卸载软件包
`# dpkg -r 包名` 或 `# dpkg --remove 包名`
## 3、清除包配置
`# dpkg -P 包名` 或 `# dpkg--purge 包名`
## 4、列出软件包包含文件
`dpkg -L 包名` 或 `dpkg --listfiles 包名`
## 5、查找文件所在软件包
`dpkg -S [路径]文件` 或 `dpkg --search [路径]文件`  
*应当尽量输入文件的全路径，而不只是文件名，这样可以缩小查找范围*
## 6、列出软件包状态
`dpkg -l [包名]`
## 7、打印dpkg架构
`dpkg --add-architecture`
## 8、打印启用的异架构
`dpkg --print-foreign-architectures`
## 9、添加架构支持
`dpkg --add-architecture 架构`
## 10、移除架构支持
`dpkg --remove-architecture 架构`
 
# 二、apt包管理器
apt也是Debian系列发行版通用的软件包管理器，它以dpkg为后端，提供了比dpkg更加方便的软件包管理功能。使用apt-file必须首先安装apt-file工具，安装方式如下：
```
# apt install apt-file
# apt-file update
```
## 1、更新可用软件包列表
`# apt update`
## 2、搜索软件包
`# apt search 描述`
## 3、安装软件包
`# apt install [--reinstall] 包名[:体系架构][=版本号]` 或 `# apt install [--reinstall] 文件`  
*安装本地软件包时推荐使用apt install代替dpkg -i，因为他可以自动修正依赖关系，请注意apt install后面跟的必须是文件的路径而不能只是文件名；--reinstall表示重新安装该软件包，当你认为有已安装软件包被破坏时，可以使用该选项修正，而dpkg -V可以用来检测软件包的完整性*
## 4、卸载软件包
### (1)普通卸载
`# apt remove [--purge] 包名`
### (2)自动卸载
`# apt autoremove [--purge] [包名]`  
*使用remove将仅卸载当前指定软件包，且不卸载安装该软件包过程中为解决其依赖关系自动安装的软件包；使用autoremove将同时卸载指定软件包及安装该软件包过程中为解决其依赖关系自动安装的软件包；同时，autoremove可单独使用；使用--purge将清除其配置文件*
## 5、清除包配置
`# apt purge 包名`
## 6、列出所有已安装软件包
`apt list -i [-a]`  
*使用-a将列出已安装软件包的所有候选版本*
## 7、根据包名列出软件包
`apt list [-a] 包名`  
*使用-a将列出软件包的所有候选版本*
## 8、列出软件包包含文件
`apt-file list 包名` 或 `apt-file show 包名`
## 9、查找文件所在软件包
`apt-file search [路径]文件` 或 `apt-file find [路径]文件`
## 10、正向依赖关系分析
`apt depends 包名`
## 11、反向依赖关系分析
`apt rdepends 包名`
## 12、下载软件包
`apt download 包名`
## 13、系统升级
`# apt full-upgrade [-y]`  
*upgrade当然也是可行的选项，但该选项不会自动更正软件依赖问题，而dist-upgrade与full-upgrade的差别似乎是没有差别*
## 14、锁定软件包状态
`# apt-mark hold 包名`  
*这个可以用来解决 cn.wps.wps-office依赖于ttf-mscorefonts-installer导致的恶心问题，先apt autoremove --purge ttf-mscorefonts-installer，然后apt-mark hold ttf-mscorefonts-installer这样就可以永远保持ttf-mscorefonts-installer于未安装状态，而cn.wps.wps-office也不会报依赖关系问题*
 
# 三、aptitude包管理器
aptitude是一款以apt为后端，且支持终端/字符用户界面（TUI）的包管理器。经常被作者用来解决依赖关系问题。
## 1、解决依赖关系问题
`# aptitude install -f [包名]`
# 四、关于sources.list配置文件
sources.list决定了apt能够从什么位置获取到什么样的软件包。一个正确的软件源通常由源类型、源地址、版本号、软件类型四个部分组成。源地址通常可以在浏览器中直接打开，在打开的网页下面通常存在dists、pool、project等内容。  
`源类型 [选项1=值1,值2,…… 选项2=值3,值4,……] 源地址 版本号 软件类型1 软件类型2 ……`
## 1、指定软件源架构
`源类型 [arch=架构1,架构2,……] 源地址 版本号 软件类型1 软件类型2 ……`
## 2、信任软件源  
`源类型 [trusted=true] 源地址 版本号 软件类型1 软件类型2 ……`  
*可以用于临时解决签名、公钥等问题，不建议对不信任的软件源启用*
## 3、使用哈希而非文件名
`源类型 [by-hash=force] 源地址 版本号 软件类型1 软件类型2 ……`  
关于本章节的更多内容可以参见https://manpages.debian.org/buster/apt/sources.list.5.en.html
