# UserModel :  QAbstractListModel

用户列表模型

 存储就是一个 QList<UserPtr>:                                                                                                                                                                                      
                                                                                                                                                                                                                   
 ```cpp                                                                                                                                                                                                            
   // usermodel.cpp:45                                                                                                                                                                                             
   struct UserModelPrivate                                                                                                                                                                                         
   {                                                                                                                                                                                                               
       ...                                                                                                                                                                                                         
       QList<UserPtr> users;      // 唯一的“存储”,进程内                                                                                                                                                           
   };                                                                                                                                                                                                              
 ```            

 tryAddNssUser() 的 4 个调用点值得注意,因为它是“非 accounts 服务用户”唯一的进入方式:                                                                                                                               
                                                                                                                                                                                                                   
 1. UserInput.qml:395 —— 登录页“其他用户”手输用户名后 UserModel.tryAddNssUser(name)                                                                                                                                
 2. GreeterProxy::readyRead 的 LastLogin 消息 → setLastUser()(usermodel.cpp:355)                                                                                                                                   
 3. UserLoggedIn 消息(崩溃恢复) —— greeterproxy.cpp:687 有明确注释:                                                                                                                                                
    ```cpp                                                                                                                                                                                                         
      // TODO: persist users entered via "Other" so they survive in UserModel;                                                                                                                                     
      // then remove this fallback                                                                                                                                                                                 
    ```                                                                                                                                                                                                            
 4. updateUserLoginState() 遇到未知用户名时(登录/解锁成功但模型里没有)  
