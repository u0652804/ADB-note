# ADB-note

### close APPs by ADB

reference : https://stackoverflow.com/questions/33898029/adb-how-to-tap-close-from-recent-apps-to-completelty-through-adb-one-liner-comm

       input keyevent 187 # KEYCODE_APP_SWITCH

       input keyevent 20

       input keyevent DEL       

### adb shell am

reference : https://gist.github.com/tsohr/5711945

start activity
  
    adb shell am start -n per.noah.todaylanuchertest/.MainActivity

### list service

    adb shell service list

### list cpu cost

    adb shell dumpsys cpuinfo

### get memory usage cost on a app  

    adb shell dumpsys meminfo per.noah.dynamiclayout -d
    
### Windows make shell to Android

Create a shell file and edit it e.g. hello.sh
    
    #!/system/bin/sh 
    echo "starting"
    while [ 1 ] 
    do     
        echo "run"     
	sleep 3
    done

Save file and push it to Android storage

    adb push hello.sh /sdcard/

Execute shell file in Android device

    adb shell sh /sdcard/hello.sh
    
If you edit the file in Windows, then the execution will occur bug like 

    /sdcard/hello.sh[3]: syntax error: 'while' unmatched
    
Fix the bug :

1. open and edit the shell file by Notpad++

2. 編輯 -> 換行格式 -> 轉換成Unix格式 (Windows edit type : CR+LF; Android know type : LF)

3. Push and execute the shell file again


### open url with browser by ADB cmd

    adb shell am start -a android.intent.action.VIEW -d https://www.google.com/

## install system app with .apk file

	$ adb push test.apk /sdcard/
	$ adb root
	$ adb disable-verity
	$ adb remount
	$ adb shell
	# mount -o remount,rw -t yaffs2 /dev/block/mtdblock3 /system 
	# cat /sdcard/test.apk > /system/app/test.apk 
	# mount -o remount,ro -t yaffs2 /dev/block/mtdblock3 /system
	# exit
	$ exit
	
	adb reboot
