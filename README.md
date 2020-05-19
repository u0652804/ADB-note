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

ref : 

1. check app is system or not : https://rdzhou.github.io/2017/12/20/How-to-Check-If-an-App-is-System-App-or-Not/

2. sign build and push apk file as a system app : https://connorlin.github.io/2016/04/27/%E8%AE%A9Android-Studio%E6%94%AF%E6%8C%81%E7%B3%BB%E7%BB%9F%E7%AD%BE%E5%90%8D(%E8%AF%81%E4%B9%A6)/

Build.grandle(app)

	android {
	    // add
	    signingConfigs {
		config {
		    keyAlias 'alias_name'
		    keyPassword '...'
		    storeFile file('keystoreFilePath')
		    storePassword '...'
		}
	    }
	    
	buildTypes {
        // add
        debug {
            signingConfig signingConfigs.config
        }
	
Adb cmd list	

	adb root # need root device
	adb remount
	adb push test.apk > /system/priv-app/test.apk 
	
	# if first push file fail => push again
	adb disable-verity
	
	adb reboot
