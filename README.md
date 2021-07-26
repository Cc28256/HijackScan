# HijackScan
白文件扫描器 非公开

windows pe 白文件利用扫描器 版本 1.3 (2020 07 26)

# 扫描支持：

支持x86 x64程序

支持cui gui程序

支持定义扫描文件的最大大小

支持等待进程时间

支持选择只扫描带签名的PE程序

支持选择可与system目录dll同名

help : This tool scans files that could be used for hijacking.
[ -p  ]	scan path                   :	[ ]D:\\scan                         
[ -w  ]	scan software x86 or x64    :	[ ]w32      [*]w64      [ ]w32w64	
[ -ui ]	scan software cui or gui    :	[ ]cui      [ ]gui      [*]cuigui 	
[ -st ]	only scan signature         :	[ ]on       [*]off                  
[ -sd ]	scan system dir dll         :	[*]on       [ ]off                  
[ -ms ]	set scan file max size      :	[*]10   ( Mb )						
[ -wt ]	set wait for proc time      :	[*]5000 ( ms )                      
 [*] Stands for default.
   For example : -p d:\\scan -w w64 -ui cuigui -st on -sd on -ms 10 -wt 5000  
   version 1.3

# 注意事项：
 1 扫描时会将符合条件的程序添加到列表最后统一检测是否可能利用
 
 2 检测阶段部分程序会报错弹窗卡住进程，需要手动处理弹窗
 
 3 测试成功的程序会输出到当前success目录下
 
 4 目录下的程序大部分情况是可以利用的，但并不是100%，需要最后人工审核
 
# 更新日志：

## v1.0 

扫描  64 32 gui cui 带签名可被劫持的白文件。

## v1.1 

 修复LoadLibraryExA flag 为 0x800时 仍然尝试创建劫持 （0x800 值load system目录 不能用于劫持）

 文件查询函数添加了更多判断，减少了无意义的尝试
 
 x64 增加申请内存创建新的线程执行shellcode创建注册表 （x86 需要读取文件到内存）
 
## v1.2

 创建进程时 错误弹窗 "计算机类型不匹配" 不再需要手动关闭
 
 注入进程后 错误弹窗 "系统错误 找不到dll 无法继续执行... " 不再需要手动关闭

 PE文件添加Driver判断，不再尝试驱动类型的PE进程的创建 

 增加部分某些原因利用率极低的DLL到排出项目 减少success文件夹中不能利用的程序

 判断成功的条件增加，减少success文件夹中不能利用的程序

## v1.3
 
 x86 增加申请内存创建新的线程执行shellcode创建注册表
 
 整理项目依赖 直接生成 顺序relese x86 -> relese x64
 
 添加-sd 选项 支持选择是否可与system32目录下DLL重名
 
 修复得到的字符串中含有不可见字符导致程序创建资源文件失败的问题
 
 修复路径中含有../时导致结果与预期不符的问题
