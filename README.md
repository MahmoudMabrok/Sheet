
# Sheet
[![HitCount](http://hits.dwyl.com/MahmoudMabrok/Sheet.svg)](http://hits.dwyl.com/MahmoudMabrok/Sheet)

# Installation Guide
  - Flutter 
    - Linux
      - install SDK [link](https://flutter.dev/docs/development/tools/sdk/releases?tab=linux).
      - add it to path by ```export PATH="$PATH:`pwd`/flutter/bin"``` or 
      - ```sudo nano /etc/profile``` then add ``` if [ "`id -u`" -eq 0 ]; then
           PATH="..."
        else
           PATH="/usr/local/bin:...:[PATH_TO_FLUTTER_GIT_DIRECTORY]/flutter/bin"
        fi
        export PATH ```.
      - it may need to configure Dart sdk.
      - you will find it at `flutter/bin/cache/dart-sdk`

- Java
  - Linux 
    - There are two imp Oracle & OpenJdk we will use 
    - install 
         ```
            sudo apt update
            sudo apt install openjdk-8-jdk // we can replace 8 with any version 8,10,11.
         ```
    - query version `java --version`
    - make as default one by `sudo update-alternatives --config java` this show selection and choose it.
    - add `JAVA_HOME`
        - copy path to jdk by type last command `sudo update-alternatives --config java`
        - type `sudo nano /etc/environment`
        - add to end of it `JAVA_HOME="THE PATH YOU HAVE COPIED"`
        - type`source /etc/environment`
        - verify by `echo $JAVA_HOME`.

- Android Studio 
  - Linux
    - Download .tar file
    - Extract it 
    - go to `bin` directory 
    - open terminal and type `./studio.sh`
    - Contiune process. 
# Android 
- `Process unexpectedly exit.` => downgrade version of gradle to `classpath 'com.android.tools.build:gradle:3.3.2'`
- 
  ```
  try to change the compileSdkVersion to:
  compileSdkVersion 28
  fontVariationSettings added in api level 28
  ```
- `.ClassNotFoundException: android.view.View$OnUnhandledKeyEventListener`  --> 

# libararies 
- [ReadMoreTextView](https://github.com/MahmoudMabrok/ReadMoreTextView)
- [Android-Image-Slider](https://github.com/smarteist/Android-Image-Slider)
# Git 
- initial setup 
  ```
  $ git config --global user.name "John Doe"
  $ git config --global user.email johndoe@example.com
  ```
- un-commit last commit `git reset --soft HEAD^`

# Resources 

- Firebase 
    - [English Cousre](https://www.youtube.com/playlist?list=PLGCjwl1RrtcTXrWuRTa59RyRmQ4OedWrt).
    - [Arabic Cousre](https://www.youtube.com/playlist?list=PLb6ZzJ93PVwpsrq-MPzdHzoI5BXfMoIj)

- Android Room
    - [English Cousre](https://www.youtube.com/playlist?list=PLJJzW__bab3SF33vwvlA_F7PPN6NxkHdQ
    )
    - [overview in arabic](https://www.youtube.com/watch?v=A9lZusQtX4w
    )


- Icons, Vectors 
    - [canva](https://www.canva.com).
    - [icons8](https://icons8.com).
    - [vecteezy](https://www.vecteezy.com).
    - [iconfinder](https://www.iconfinder.com)
    
    
- Performance tools 
  - [nimbledroid](https://nimbledroid.com/)
