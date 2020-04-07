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
