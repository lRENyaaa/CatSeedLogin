# CatSeedLogin 猫种子登陆
> 插件在Spigot API 1.13.2环境下开发的，
由于现在很多登录插件功能配置非常多，配置起来麻烦并且有很多用不到的功能。
crazylogin在高版本有各种匪夷所思的bug（总之我是被crazylogin从1.13.2的版本劝退自己开始造起了登陆插件）
authme配置文件对一些经验不足的服主配置起来极其麻烦，甚至有人从入门到弃坑
有人测试1.7.10 和 1.11版本的服务器可以用 理论上应该支持1.7 ~ 1.15 一般都是低版本向上兼容。
## 基础功能:
*  注册 登录 修改密码 管理员设置密码
*  防止英文id大小写登录bug
*  防止玩家登录之后,被别人顶下线
*  下线之后 “可配置” 秒内不能重新进入服务器（防止某些bug）
*  没有登录之前禁止移动,交互,攻击,发言,使用指令,传送,点击背包物品,丢弃物品,拾取物品
*  禁止同ip的帐号同时在线数量超过可配置数量
*  登录之前在配置文件指定的世界出生点,登录之后自动返回下线地点（可配置取消）
*  储存默认使用的是SQLite（也支持Mysql，需要配置文件sql.yml中配置打开）
*  密码加密储存,Crypt默认加密方式
*  进入游戏时游戏名的限制（由数字,字母和下划线组成 “可配置”长度的游戏名才能进入）
*  绑定邮箱，邮箱重置密码功能
## 下载
* 最新版 https://www.mcbbs.net/thread-847859-1-1.html
* 旧版 https://github.com/CatSeed/CatSeedLogin/tags
## 使用方式
* 下载到的文件放入plugins文件夹重启服务器
## 指令
### 登录
* /login 密码
* /l 密码
### 注册密码
* /register 密码 重复密码
* /reg 密码 重复密码
### 修改密码
* /changepassword 旧密码 新密码 重复新密码
* /changepw 旧密码 新密码 重复新密码
### 绑定邮箱
* /bindemail set 邮箱
* /bdmail set 邮箱
### 用邮箱收到的验证码完成绑定
* /bindemail verify 验证码
* /bdmail verify 验证码
### 忘记密码，请求服务器给自己绑定的邮箱发送重置密码的验证码
* /resetpassword forget
* /repw forget
### 用邮箱收到的验证码重置密码
* /bindemail re 验证码 新密码
* /bdmail re 验证码 新密码
### 管理指令
### 添加登陆之前允许执行的指令 (支持正则表达式)
* /catseedlogin commandWhiteListAdd 指令
### 删除登陆之前允许执行的指令 (支持正则表达式)
* /catseedlogin commandWhiteListDel 指令
### 查看登陆之前允许执行的指令 (支持正则表达式)
* /catseedlogin commandWhiteListInfo
### 设置相同ip限制 （默认数量2）
* /catseedlogin setIpCountLimit 数量
### 设置游戏名最小和最大长度 (默认最小是2 最大是15)
* /catseedlogin setIdLength 最短 最长
### 离开服务器重新进入间隔限制 单位：tick (1秒等于20tick) (默认60tick)
* /catseedlogin setReenterInterval 间隔
### 设置玩家登陆地点为你站着的位置 (默认登陆地点为world世界的出生点)
* /catseedlogin setSpawnLocation
### 设置自动踢出未登录的玩家 (默认120秒，小于1秒则关闭此功能)
* /catseedlogin setAutoKick 秒数
### 打开/关闭 限制中文游戏名 (默认打开)
* /catseedlogin limitChineseID
### 打开/关闭 登陆之前是否受到伤害 (默认登陆之前不受到伤害)
* /catseedlogin beforeLoginNoDamage
### 打开/关闭 登陆之后是否返回退出地点 (默认打开)
* /catseedlogin afterLoginBack
### 打开/关闭 登录之前是否强制在登陆地点 (默认打开)
* /catseedlogin canTpSpawnLocation
### 管理员强制删除账户
* /catseedlogin delPlayer 玩家名
### 管理员强制设置玩家密码
* /catseedlogin setPwd 玩家名 密码
### 重载配置文件
* /catseedlogin reload
## 权限
* catseedlogin.command.catseedlogin 管理员指令/catseedlogin 使用权限
## 配置文件
### settings.yml
> \#相同ip限制  
IpCountLimit: 2  
\#登录点,默认是world主世界出生点,推荐用指令设置  
SpawnLocation: 世界名:x轴:y轴:z轴:yaw:pitch  
\#是否限制中文ID  
LimitChineseID: true  
\#游戏ID最小长度  
MinLengthID: 2  
\#游戏ID最大长度  
MaxLengthID: 15  
\#登陆之前不受到伤害  
BeforeLoginNoDamage: true  
\#离开服务器重新进入的间隔限制 单位：tick（如果设置3秒则是60）  
ReenterInterval: 60  
\#登陆之后是否返回退出地点  
AfterLoginBack: true  
\#登录之前是否强制在登陆地点  
CanTpSpawnLocation: true  
\#登陆之前允许执行的指令 (支持正则表达式)  
CommandWhiteList:  
  \- /(?i)l(ogin)?(\z| .\*)  
  \- /(?i)reg(ister)?(\z| .\*)  
  \- /(?i)resetpassword?(\z| .\*)  
  \- /(?i)repw?(\z| .\*)  
  \- /(?i)worldedit cui  
\#设置自动踢出未登录的玩家 (默认120秒，小于1秒则关闭此功能)  
AutoKick: 120
### sql.yml
如果不使用mysql数据库储存，就请无视此配置  
> MySQL:  
\#是否开启数据库功能（false = 不开启）  
  Enable: false  
  Host: 127.0.0.1  
  Port: '3306'  
  Database: databaseName  
  User: root  
  Password: root  
### emailVerify.yml 
如果不使用邮箱一系列功能，就请无视此配置  
> \#是否开启邮箱系列的功能（false = 不开启）  
Enable: false  
EmailAccount: "763737569@qq.com"  
EmailPassword: "123456"  
EmailSmtpHost: "smtp.qq.com"  
EmailSmtpPort: "465"  
SSLAuthVerify: true  
\#发件人的名字  
 FromPersonal: "xxx服务器"  
### language.yml
语言文件  
内容省略...
## 开发者部分
### 事件
CatSeedPlayerLoginEvent
  
CatSeedPlayerRegisterEvent
### API
CatSeedLoginAPI
## 联系
[点击进入 QQ交流群839815243](http://shang.qq.com/wpa/qunwpa?idkey=91199801a9406f659c7add6fb87b03ca071b199b36687c62a3ac51bec2f258a3)
