# ADB

基础：  
设备列表  
adb devices  
  
选择某个设备时  
adb -s 设备id  

安装和卸载  
adb install yourpackagename  参数 install -r 重新安装该程序，保存数据 -s 安装在SD卡内，而不是设备内部存储 -l锁定该程序  
adb uninstll yourpackagename  参数 -k 不删除数据和缓存    

设备信息  
adb shell getprop  
然后根据需要自己再取就可以了  

#cd system/sd/data //进入系统内指定文件夹  
#ls //列表显示当前文件夹内容   
#rm -r xxx //删除名字为xxx的文件夹及其里面的所有文件   
#rm xxx //删除文件xxx   
#rmdir xxx //删除xxx的文件夹  



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

6.命令窗口显示logcat  
adb logcat -s 标签名  

7.文件操作  
adb push 电脑路径 手机路径  
adb pull 手机路径 电脑路径  

8.获取root权限  
adb shell su

9.开启viewserver  
检验一台手机是否开启了View Server的办法为：  
adb shell service call window 3  
若返回值是：Result: Parcel(00000000 00000000 '........')" 说明View Server处于关闭状态  
若返回值是：Result: Parcel(00000000 00000001 '........')" 说明View Server处于开启状态  

若是一台可以打开View Server的手机（Android开发版手机 、模拟器or   按照本帖步骤给系统打补丁的手机），我们可以使用以下命令打开View Server：  
adb shell service call window 1 i32 4939  
使用以下命令关闭View Server：  
adb shell service call window 2 i32 4939  
   




