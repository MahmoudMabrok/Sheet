
## Process unexpectedly exit
downgrade version of gradle to `classpath 'com.android.tools.build:gradle:3.3.2'`

## [to ba labeled] 
  ```
  try to change the compileSdkVersion to:
  compileSdkVersion 28
  fontVariationSettings added in api level 28
  ```


##  `.ClassNotFoundException: android.view.View$OnUnhandledKeyEventListener`  --> 

##  `More than one file was found with OS independent path 'META-INF/atomicfu.kotlin_module'` 
```
android {
    compileSdkVersion 29

    compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }
  /*  packagingOptions {
        pickFirst 'META-INF/kotlinx-io.kotlin_module'
        pickFirst 'META-INF/atomicfu.kotlin_module'
        pickFirst 'META-INF/kotlinx-coroutines-io.kotlin_module'
        pickFirst 'META-INF/library_release.kotlin_module'
    }*/

}
```
