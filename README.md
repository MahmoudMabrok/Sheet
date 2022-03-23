
# Sheet
# My posts 
- [MarryAppLinkedIN](https://www.linkedin.com/posts/mahmoud-mabrouk-fouad_android-kotlin-retrofit-activity-6733847314080768000-FIQX)
- [open source experiment](https://www.linkedin.com/posts/mahmoud-mabrouk-fouad_%D8%A7%D9%84%D8%AD%D8%A7%D8%AC%D8%A9-%D8%A7%D9%85-%D8%A7%D9%84%D8%A7%D8%AE%D8%AA%D8%B1%D8%A7%D8%B9-%D8%AA%D8%B9%D8%AF%D9%8A%D9%84-%D8%B9%D9%84%D9%89-%D8%AA%D8%B7%D8%A8%D9%8A%D9%82-%D8%A7%D9%88%D8%A8%D9%86-activity-6755904666443247617-v83Q)
- [kotlin-bestpractices-constants](https://www.linkedin.com/posts/mahmoud-mabrouk-fouad_android-kotlin-bestpractices-activity-6752301292313436160-fDP1)
- [certification aad](https://www.linkedin.com/posts/mahmoud-mabrouk-fouad_android-google-andela-activity-6779084378736746496-bNRT)
- [CV](https://www.linkedin.com/posts/mahmoud-mabrouk-fouad_mahmoudmabroukresume-activity-6808064496213491712-110u)
- [Learning android](https://www.linkedin.com/feed/update/urn:li:activity:6816832955021848576/?fbclid=IwAR0hDw7HxTAmJrYh1AXP3KNhXDnfr6D0y74XigxDRJL6ucFVwlGk67Ce5L8)
- [Quran App got 4th search](https://www.linkedin.com/posts/mahmoud-mabrouk-fouad_aepaesaesaevaetabraedaesabraehaesaexabraetaevaetaexabraewaepaesabraetaevaetaex-activity-6853449111337746432-diaS)
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

- Postman 
    ```
    Download Postman by running following command in your Linux system:

    wget https://dl.pstmn.io/download/latest/linux64 -O postman-linux-x64.tar.gz

    Extract the downloaded file by running the following command in /opt directory:

    sudo tar -xvzf postman-linux-x64.tar.gz -C /opt

    Finally, create a symbolic link running following command in terminal:

    sudo ln -s /opt/Postman/Postman /usr/bin/postman
    ```     
    
- Time doctor on linux 
  - downlaod it from here [website](https://www.timedoctor.com/download.html)    
  - make downloaded file excutable 
- Python
- `sudo apt-get install python3-distutils`, `sudo apt-get install python3-apt`
 
  

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
- 
  ```
  .gitignore will prevent untracked files from being added (without an add -f) to the set of files tracked by git, however git will continue to track any files that are already being tracked.

  To stop tracking a file you need to remove it from the index. This can be achieved with this command.

  git rm --cached <file>

  If you want to remove a whole folder, you need to remove all files in it recursively.

  git rm -r --cached <folder>

  ```
  - update 
    ```
    sudo add-apt-repository ppa:git-core/ppa -y
    sudo apt-get update
    sudo apt-get install git -y
    git --version
    ```
  
# Python 
- [dealing-with-multiple-python-versions-and-pip](https://stackoverflow.com/questions/2812520/dealing-with-multiple-python-versions-and-pip)  

# Resources 
- tool to localize strings [androidapptranslator](https://androidapptranslator.com/)

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
    - [android-feature-graphic-generator](https://www.norio.be/android-feature-graphic-generator/)
    
    
- Performance tools 
  - [nimbledroid](https://nimbledroid.com/)
  
- Script to add display 
```    
sudo xrandr --newmode "1680x1050_60.00"  146.25  1680 1784 1960 2240  1050 1053 1059 1089 -hsync +vsync
sudo xrandr --addmode VGA-1 "1680x1050_60.00"
```


# tools 
- [hex_to_base64](http://tomeko.net/online_tools/hex_to_base64.php)
- [Github analysis](https://yhype.me/dashboard)
