# HijackScan
白文件扫描器 非公开

windows pe 白文件利用扫描器 版本 1.0 

# 扫描支持：

支持x86 x64程序

支持cui gui程序

支持定义扫描文件的最大大小

支持等待进程时间

只扫描具有签名的PE程序          （写死的）

扫描会带有system目录可以用dll项 （写死的）

-p  [ -p c:path  ]  scan path.              
-w  [ -w win64   ]  w32 or w64.            
-ui [ -ui cui    ]  cui or gui.            
-ms [ -ms 100000 ]  file max size.         
-wt [ -wt 5000   ]  wait for process time. 
 * -st [ -st        ]  file have signature.   
 * -sd [ -sd        ]  system dir dll.     

# 注意事项：
 1 扫描时会将符合条件的程序添加到列表最后统一检测是否可能利用
 
 2 检测阶段部分程序会报错弹窗卡住进程，需要手动处理弹窗
 
 3 测试成功的程序会输出到当前success目录下
 
 4 目录下的程序大部分情况是可以利用的，但并不是100%，需要最后人工审核
 
