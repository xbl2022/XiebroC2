## 特点

- 被控端(Client)由Golang编写，兼容WIndows、Linux、MacOS上线（未来会考虑移动端上线）

- 团队服务器(Teamserver)由.net 8.0 编写、AOT编译，内存占用低，无需安装任何依赖，几乎可以兼容全平台系统

- 控制端(Controller)支持反弹shell，文件管理、进程管理、网络流量监控、内存加载、自定义UI背景色等功能

- 支持内存注入PE文件(windows端的RunPE，Linux端的memfd)，即文件不落地执行木马，中转第三方C2/RAT

- 支持内存执行.net 程序集（execute-assembly、inline-assembly)

- 支持通过lua扩展UI控件、Session命令，载荷生成（类似于CobaltStrike的cna脚本）

- 支持Teamserver托管二进制文件、文本、图片(类似SimpleHttpServer)

- 支持团队服务器自定义配置文件,自定义Telegram的chat ID/Token上线通知

- 控制端(Controller)UI轻量级交互界面，内存占用大约是CobaltStrike的60分之一，是Metasploit的10分之一

- 用Golang编译后的客户端体积较大，因此免杀效果较差（Golang的编译器特征已经被部分AV/EDR厂商标黑了）

  

  

## 支持平台

**Client(Session)**

|    Windows（x86_x64）    | Linux(x86_x64) | MacOS |
| :----------------------: | :------------: | :---: |
|        Windows11         |     ubuntu     | AMD64 |
|        Windows10         |     Debian     | i386  |
|       Windows8/8.1       |     CentOS     |  M1   |
|         Windows7         |    ppc64le     |  M2   |
|        Windwos-XP        |      mips      |       |
| Windows Server 2000-2022 |     s390x      |       |



## 快速使用

控制端（Controler）需要运行在.Net Framework4.8以上（Windows10/11无需安装，win7需要下载: [.net framworkd4.8下载](https://dotnet.microsoft.com/zh-cn/download/dotnet-framework/thank-you/net48-offline-installer)）

修改TeamServerIP和TeamServerPort为VPS的IP和端口，然后保存为profile.json

```json
{
    "TeamServerIP": "192.168.31.81",
    "TeamServerPort": "8880",
    "Password": "123456",
    "StagerPort": "4050",
    "Telegram_Token": "",
    "Telegram_chat_ID": "",
    "Fork": true,
    "Process64": "C:\\windows\\system32\\notepad.exe",
    "Process86": "C:\\Windows\\SysWOW64\\notepad.exe",
    "WebServers": [],
    "listeners": [],
    "s_Reflection_dll_x64": ""
}
```

服务端：

```bash
Teamserver.exe -c profile.json
```

控制端

```

```



demo

<video src="https://private-user-images.githubusercontent.com/89376703/305162512-771c2e88-afd8-493d-a575-7e10149837dd.mp4" width="640" height="480" controls></video>



## 命令列表




| Commands         |               Usage                |                   Description                    |
| :--------------- | :--------------------------------: | :----------------------------------------------: |
| nps              |     nps  <powershell command>      |        Unmanaged run powershell in memory        |
| Inline-assembly  | inline-assembly <FilePath> <args>  |           Inline execute .net assembly           |
| execute-assembly | execute-assembly <FilePath> <args> | Fork child process execute loader .net  assembly |
| runpe            |      runpe <FilePath> <args>       |          loader C/C++ PE in the memory           |
| shell            |        shell <cmd command>         |                 Execute  command                 |
| powershell       |  powershell <powershell command>   |            Execute powershell command            |
| checkAV          |              checkAV               |             Detect AV/EDR processes              |
| upload           | upload <uploadFilePath> <FilePath> |            Upload File to the target             |
| memfd            |      memfd <FilePath> <args>       |        PE loader in the memory for Linux         |
| help             |                help                |                View command list                 |
| cls              |                cls                 |                   Clear screen                   |



## 计划进行

- 用C/C++/C#/Rust编写多阶段加载器（Multi-stage loader），体积尽量控制在150kb以内。

- 目前正反向代理和端口转发未开放，未来考虑完善和开发这个功能。

- 正在开发WebSocket/RUDP/SMB协议的Session模式，Beacon模式仅考虑开发HTTP/HTTPS/DNS。
- 考虑开发shellcode(raw)、Powershell、VBscript、Hta、Jscript等载荷。

- 编写lua更多的，集成更多的内网渗透插件。

- 目前Golang的控制台隐藏问题还无法得到很好的方案，如果您知道如何解决请联系我。



## 更新



## 免责声明

本工具仅用于渗透测试交流和研究，强烈不建议您用于任何的实际用途（包括黑灰产交易和割韭菜）


