# HijackScan
白文件扫描器 非公开

windows pe 白文件利用扫描器 版本 1.6 (2021 07 30)

# 扫描支持：

支持x86 x64程序、支持cui gui程序、支持定义扫描文件的最大大小、支持定义等待进程时间、支持选择只扫描带签名的PE程序、支持选择可与system目录dll同名。

help : This tool scans files that could be used for hijacking.

| 选项 | 说明                     | 参数                       | 默认   |
| ---- | ------------------------ | -------------------------- | ------ |
| -p   | scan path                | D:\\                       | ——     |
| -w   | scan software x86 or x64 | “w32”、"w64" or "w32w64"   | w64    |
| -ui  | scan software cui or gui | "cui"、"gui" or "cuigui"   | cuigui |
| -st  | only scan signature      | “on” or ”off“              | off    |
| -sd  | scan system dir dll      | "on" or "off"              | on     |
| -ms  | set scan file max size   | ms < 100 ( Mb )            | 10     |
| -wt  | set wait for proc time   | 4999 < wt < 1000001 ( ms ) | 5000   |
| -s   | only scan no check file  | ——                         | ——     |


   For example : -p d:\\scan -w w64 -ui cuigui -st on -sd on -ms 10 -wt 5000  
   
   version 1.4

# 注意事项：

 ~~1 扫描时会将符合条件的程序添加到列表最后统一检测是否可能利用~~
 
 ~~2 检测阶段部分程序会报错弹窗卡住进程，需要手动处理弹窗~~
 
 3 测试成功的程序会输出到当前success目录下
 
 4 目录下的程序大部分情况是可以利用的，但并不是100%，需要最后人工审核
 
 ~~5 程序执行时，创建的进程或其他进程弹窗UAC时，会造成无法关闭错误弹窗 因为他们不是一个会话或桌面 hscan 不能捕捉或没有权限 来关闭窗口~~
 
 5 程序执行时，其他进程弹窗UAC时，会造成无法关闭错误弹窗 因为他们不是一个会话或桌面 hscan 不能捕捉或没有权限 来关闭窗口
 
 6 尽管已经做出了尽可能的窗口判断、进程判断，避免影响程序执行对计算机产生的影响，但是可能仍然会有无法预计的情况，因此建议再计算机使用-s先收集，再将temp目录中收集到的文件放在虚拟机中进行非-s操作
 
# 更新日志：

## v1.5
 
 添加-s选项 只收集到temp目录 不进行下一步创建进程注入判断白文件步骤
 
 修改输出信息格式 添加扫描结果

 创建的进程如有调用创建管理员权限进程前，将被阻止，避免弹窗UAC
 
 扫描时排出自身创建的success目录和temp目录 避免二次扫描
 
## v1.5
 
 修改输出信息格式 添加扫描结果
 
 避免遗留子进程 尝试结束进程所创建的子进程

## v1.4
 
 shellcode删除了创建注册表动作，改为调试打印输出
 
 程序兼容性助手（Program Compatibility Assistant）弹窗不再需要手动关闭
 
 windows features窗口（.NET Framework升级提示）不再需要手动关闭
 
 更改消息码来关闭消息窗口
 
## v1.3
 
 x86 增加申请内存创建新的线程执行shellcode创建注册表
 
 整理项目依赖 直接生成 顺序relese x86 -> relese x64
 
 添加-sd 选项 支持选择是否可与system32目录下DLL重名
 
 修复得到的字符串中含有不可见字符导致程序创建资源文件失败的问题
 
 修复路径中含有“../”时导致结果与预期不符的问题

## v1.2

 创建进程时 错误弹窗 "计算机类型不匹配" 不再需要手动关闭
 
 注入进程后 错误弹窗 "系统错误 找不到dll 无法继续执行... " 不再需要手动关闭

 PE文件添加Driver判断，不再尝试驱动类型的PE进程的创建 

 增加部分某些原因利用率极低的DLL到排出项目 减少success文件夹中不能利用的程序

 判断成功的条件增加，减少success文件夹中不能利用的程序

## v1.1 

 修复LoadLibraryExA flag 为 0x800时 仍然尝试创建劫持 （0x800 值load system目录 不能用于劫持）

 文件查询函数添加了更多判断，减少了无意义的尝试
 
 x64 增加申请内存创建新的线程执行shellcode创建注册表 （x86 需要读取文件到内存）
 
## v1.0 

扫描  64 32 gui cui 带签名可被劫持的白文件。
