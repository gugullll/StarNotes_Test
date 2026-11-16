# user

单个用户对象
 ### 内存里的 User 有哪些字段(user.cpp:12-26)                                                                                                                                                                      
                                                                                                                                                                                                                   
 ```cpp                                                                                                                                                                                                            
   bool loggedIn, noPasswdLogin; quint64 uid, gid;                                                                                                                                                                 
   QString userName, fullName, homeDir, passwordHint, limitTime;                                                                                                                                                   
   QUrl icon; QLocale locale; AccountTypes identity;                                                                                                                                                               
   AccountsUserPtr inter;                                    // 指向 accounts 服务对象                                                                                                                             
   std::shared_ptr<WSocket> waylandSocket;                    // 该用户独立的 Wayland socket                                                                                                                       
 ```                                                                                                                                                                                                               
                                                                                                                                                                                                                   
 其中只有 inter 指向的数据是持久的;这些是纯运行期状态,退出即丢:                                                                                                                                                    
                                                                                                                                                                                                                   
 - loggedIn:由 logind SessionNew/SessionRemoved 驱动;启动时用 clearUserLoginState() + LoginStateQuery 重建                                                                                                         
 - waylandSocket:只在 Treeland::ActivateWayland() 通过 D-Bus 拿到 fd 后注入(treeland.cpp:601)                                                                                                                      
 - limitTime:由 updateUserLimits() 塞进来(当前仓库内无外部写入方) 
