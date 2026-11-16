# DConfigManager

监听 UserModel::currentUserNameChanged 切换用户级 DConfig

用户相关但非账号数据的持久化,在 DConfig                                                                                                                                                                        
                                                                                                                                                                                                                   
 DConfigManager::userConfig(userName)(dconfigmanager.cpp:134)按用户名创建 org.deepin.dde.treeland.user 配置实例,存字体、showOnLock 等个性化偏好,由 dde-dconfig 落盘;它跟随 UserModel::currentUserNameChanged 切换  
 用户配置。这是“某个用户的桌面设置”,与账号注册无关,进程重启后可从 dconfig 恢复。
