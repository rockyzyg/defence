# defence
#协议约定
1、命名规则
   前端->后端 cs_Module_xxx
   后端->前端 sc_Module_xxx

1.1、common.proto 通用协议
transfer 包协议，使用的所有协议都使用此协议进行包装
 - name 要传输的协议名称
 - body 要传输的协议经编码后的二进制串
 - session 前端生成，当填写此字段时，后端回应的协议赋相同的值，前端可根据session将回应消息与请求消息做映射

cs_ping/sc_ping 
 - ping 协议

sc_err, 后端通知前端的通用处理协议，处理成功/失败
 - code 错误码，与errno.xlsx配置表对应
 - proto_name 关联的协议名称，通常是前端向后端发送的请求
 - content 错误提示，有些情况下可填写一些与配置表不同的内容，用于定位错误

sc_tips 后端通知生成弹出窗

1.2、login.proto 登录模块
cs_login_create 用于注册帐户，支持密码注册

cs_login_verify 登录协议，支持游客登录、密码登录、授权码登录
 - 游客登录时，创建一个新的帐户，帐户名及密码都随机，并通过sc_login_vistor_info协议通知前端游客的帐户与密码
 - 帐户创建成功并成功登录后，后端生成一个授权码并通知前端，前端缓存到本地，下次登录时使用授权码的方式进行登录，每次登录成功后，该授权码都会变更，并通知到前端

sc_login_auth_info 后端通知前端下次登录的授权码信息

sc_login_server_info 
 - 登录认证成功后，通知用户需要连接的游戏服的域名及端口，以及登录使用的key值

1.3、player.proto 玩家模块
cs_player_enter 前端请求进入游戏服

sc_player_role_data 用户连接游戏服成功后，将玩家的角色信息发送到前端

sc_player_account_info 玩家的帐户信息

cs_player_modify 前端请求修改帐户信息

sc_player_item_change 玩家道具变更通知，注：玩家的货币变更也是通过引协议通知


1.4、mail.proto 邮件模块
cs_mail_load_all 前端请求加载所有邮件

sc_mail_load_all 后端发送全量邮件列表

sc_mail_notice 新邮件通知

cs_mail_load_new 前端请求读取新邮件

sc_mail_load_new 通知前端新邮件列表

cs_mail_read 前端读取邮件，用于更新邮件状态

cs_mail_delete 前端删除邮件

cs_mail_get_attach 前端领取邮件附件


