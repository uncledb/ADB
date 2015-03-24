# ADB

0.安装和卸载  
adb install yourpackagename  参数 install -r 重新安装该程序，保存数据 -s 安装在SD卡内，而不是设备内部存储 -l 锁定该程序
adb uninstll yourpackagename  参数 -k 不删除数据和缓存

1.获得当前的Activity  
adb shell dumpsys activity top | findstr ACTIVITY  

2.清除数据：  
adb shell pm clear com.your.packagename  
adb uninstall com.your.packagename  

3.使用adb截图 - 可封bat 一键截图  
adb shell /system/bin/screencap -p /sdcard/screenshot.png（保存到SDCard）  
adb pull /sdcard/screenshot.png d:/screenshot.png（保存到电脑）  
---bat---  
for /f "tokens=2,*" %%i in ('reg query "HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\Shell Folders" /v   "Desktop"') do (  
set desk=%%j  
)  
adb shell /system/bin/screencap -p /sdcard/screenshot.png  
adb pull /sdcard/screenshot.png %desk%/screenshot.png  
echo adb pull /sdcard/screenshot.png C:/Users/admin/Desktop/screenshot.png  


4.检测CPU  
1).使用android提供的adb shell dumpsys cpuinfo |grep packagename >/addressu.txt来获取  
2).使用top命令 adb shell top |grep packagename>/addressu.txt 来获取  

5.adb端口冲突怎么办?  
netstat -aon|findstr "5037"   找出pid  
kill 'pid'  

