# ADB-note

### close APPs by ADB

reference : https://stackoverflow.com/questions/33898029/adb-how-to-tap-close-from-recent-apps-to-completelty-through-adb-one-liner-comm

1. 

       input keyevent KEYCODE_APP_SWITCH

2. 

       input keyevent 20
       
3. 

       input keyevent DEL       

### adb shell am

reference : https://gist.github.com/tsohr/5711945
