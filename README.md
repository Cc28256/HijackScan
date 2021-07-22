# HijackScan
白文件扫描器 非公开

windows pe 白文件利用扫描器 版本 1.1

# 扫描支持：

支持x86 x64程序

支持cui gui程序

支持定义扫描文件的最大大小

支持等待进程时间

支持选择只扫描带签名的PE程序

扫描会带有system目录可以用dll项 （写死的）

[ -p c:path  ]  scan path.     

[ -w win64   ]  w32 or w64.            

[ -ui cui    ]  cui or gui.          

[ -ms 100000 ]  file max size.      

[ -wt 5000   ]  wait for process time. 

[ -st        ]  file have signature.   

 * [ -sd        ]  system dir dll.     

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
 
 X64 增加申请内存创建新的线程执行shellcode创建注册表 （X32 需要读取文件到内存）
