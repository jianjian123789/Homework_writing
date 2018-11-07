[toc]
# 1.使用栏
## 1.1 Goto Anything
快捷键：ctrl+p  
能够快速匹配文件夹下需要的文件，使用@可以查找文件内容  
使用#可以查找文件内容  

ctrl+H：查找替换，enter查找下一个，shift+enter查找上一个 

ctrl+alt+p:新建一个模板【这个是自己定义的】

## 1.2 多行游标
快捷键：选中一个单词后按住CTRL+D一次或者多次，则可同时选中同词；或者如果不想选中某个同类词，则可以先按住CTRL+D后，再按CTRL+K进行取消；  

产生多行游标的方式2：选中一个单词，然后按住ALT+F3可以同时多选  

方式3：选中一个单词后，按住ctrl+A，然后再按ctrl+shift+L  

方式4：选中一个单词后，按住shfit键，同时按住鼠标右键进行拖拽  

然后按住ctrl+{/}进行缩进操作

按住ctrl+shift+v可以保持缩进状态下（或者符合语法状态下粘贴）

## 1.3 命令模式
ctrl+N：新建文件  
ctrl+~：打开控制台
ctrl+shift+P：启动命令模式 

对于编写了```print('fff')```的文件启动命令模式后，我们在命令模式下输入python，即可将该语法转化为python语法。   
也可以安装管理一些包 

## 1.4 package control安装主题
ctrl+shift+P ：启动命令模式 

输入list，可以查看以安装的模式

输入pci，启动包安装  

然后可以[查看package control网址](https://packagecontrol.io/)可以进行选择相应的主题

主题安装完后，**如果我们想要使用该主题，需要把该主题在默认配置信息中相应的内容拷取到用户配置信息中方可启用**  

自动补全功能：使用enter或者输入ctrl+shifp+p后，然后输入snippets以模板的方式产生编程   

启动命令行后，输入pci，然后在包管理中输入python，即可查看与python相关的包软件

安装advancedfile插件，可以提高保存文件速度：安装完成后，按住ctrl+alt+N，然后输入/路径/文件名即可保存  

安装httpRequest并使用参考：<https://www.imooc.com/video/5469>    

安装nettus fetch插件可以实现插件的更新操作：首先打开命令行输入pci，输入nettus fetch进行安装，安装好后打开命令行，输入fetch ，选择fetch manage进行包管理配置，  
然后在file里添加对应的包和对应包下载的地址
![image](EF24202966A84377B08950839A36334E)，然后输入ctrl+alt+N新建一个文件用来保存更新的下载文件，再输入![image](08CD5D45FA1B4AD18380A2412D3478D8)![image](2CC617142AFE44568843B5C44237AEBA)  
然后选择，即可下载文件并保存在文件中了。  

安装siderbar enhancement插件，实现对侧边栏的功能提升  

## 1.6使用安装包安装sublime插件
首先下载vitageEX安装包，然后将其解压【注意解压时是解压在当前文件夹下】，然后将解压的文件夹放到Packages下，
![image](949701144854416BAE91580BB615615A)  
，然后开启vi操作【由于default配置文件中是忽略了vi编辑器的操作，因此我们需要进行自定义user配置】：
![image](906F231B62C84AF6A0C05F65D3E3F5BF)  

## 1.7Vi编辑器快捷键
ctrl+shift+T:回复已关闭的标签  
设置字体：![image](57F14D0B65624FB9BF79B4540A47CFCD)  
u：撤销  
ctrl+y：恢复  
dG:从当前行删除到最后一行  
d1G：从当前行删除到第一行  
d^：从当前字符删除当行首  
d$:从当前字符删除当行末  
/hello：查找hello单词  
x：删除当前字符，3x：删除三个字符  X：删除当前前面的一个字符  
r：单字符替换  R：之后所有替换  

关闭行号：
![image](3F96161C2B1F48E98CCAB321E25901BB)

关闭自动补全：auto_match_enabled;关闭命令自动补全：auto_complete  
![image](278206F87A7843F3A425CCFC5B4D2783)  

开启背景线：hightlight_line
![image](B014C75A63F346A8B11AD827C14D690F)

配置键位设定:
![image](78DF46B55CBB483D89018FCD16EF5787)

安装python插件：
![image](4DF87F00C6FD48B99B057EEA62DFA47A)

查看已安装的包：
![image](93878A81CA414286B64EE025FEB4D872)

删除已安装的包：
ctrl+shift+P后，输入remove，选中remove package即可
![image](8FA0BC7AFECE479298E7884794D87919)

CTRL+B运行命令后，就相当于在命令终端下执行了python3 test.py这个文件
![image](7D4A0E4A32404AC683025DD5B054D7FD)  

配置sublime REPL插件过程(可以实现调试等一些功能)[参考链接](http://edu.51cto.com/course/9001.html?source=so)：  
首先打开sublime REPL的安装包路径进行配置如下文件：
![image](0641018E650846C6A2AEC6642CBEDD3B)
![image](9672E4E82B934963BAF8AD39BC602203)
![image](05F05015BD134034942B9040EA39079D)
![image](1716F6D3FC7C473F953A1CC7EE7E755B)  
然后在输入alt+shift+2实现分栏操作，一边代码一边调试：
![image](0E3A0DCAFD5E49F0AE3E8C0061F596B0)

安装sublime Tmpl：可以新建文件夹模板插件  
在setting-user中设置上自己的信息：
```
{
            "disable_keymap_actions": false, // "all"; "html,css"
            "date_format" : "%Y-%m-%d %H:%M:%S",
            "attr": {
                "author": "mx",
                "email": "mengxiang@xiangcloud.com.cn",
                "link": "http://www.xiangcloud.com.cn/"
            }
        }
```
然后我将Python的创建模板命令也做了修改，在key bindings-user中添加了以下信息，意思是ctrl+alt+p就可以创建一个新的Python模板  
```
    [ 
        {
            "caption": "Tmpl: Create python", "command": "sublime_tmpl",
            "keys": ["ctrl+alt+p"], "args": {"type": "python"}
        },
    ]
``` 
![image](8EEEA3429CDD40438244001B1649B978)

# 参考文献
[1.python环境搭建：参考视频]((http://edu.51cto.com/course/9001.html?source=so))   
[2.python文件搭建](https://blog.csdn.net/mx472756841/article/details/50535517)
