0x00 漏洞背景

win10中任务调度服务导出的函数没有验证调用者的权限，任意权限的用户调用该函数可以获取系统敏感文件的写权限，进而提权。

0x01 漏洞影响

漏洞影响win10和windows server 2016。目前发布的EXP暂时只能用于x64系统。

0x02 漏洞详情

win10系统Task Scheduler任务调度服务中ALPC调用接口导出了SchRpcSetSecurity函数，该函数能够对一个任务或者文件夹设置安全描述符。

 HRESULT SchRpcSetSecurity(
   [in, string] const wchar_t* path,
   [in, string] const wchar_t* sddl,
   [in] DWORD flags
 );

该服务是通过svchost的服务组netsvcs所启动的，对应的dll是schedsvc.dll。

