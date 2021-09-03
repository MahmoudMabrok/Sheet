# Plugins 
## detekt 
```
plugins {
    id 'com.android.application'
    id 'kotlin-android'
    id("io.gitlab.arturbosch.detekt").version("1.18.1")
}

 detektPlugins "io.gitlab.arturbosch.detekt:detekt-formatting:1.18.1"

task detektFormat(type: io.gitlab.arturbosch.detekt.Detekt) {
    description = "Runs autocorrect enabled detekt build."
    source = files("src/main/java")
    config.from(files("$rootDir/Scripts/detekt-config.yml"))
    autoCorrect = true
    reports {
        html{
            enabled = true
            destination = file("build/reports/detekt-formatted.html")
        }
    }
}




```

- [detekt-config.yml](https://github.com/detekt/detekt/edit/main/detekt-core/src/main/resources/default-detekt-config.yml)


# Base 
```
  implementation "androidx.appcompat:appcompat:$rootProject.appCompatVersion"
    implementation "androidx.activity:activity-ktx:$rootProject.activityVersion"

    // Dependencies for working with Architecture components
    // You'll probably have to update the version numbers in build.gradle (Project)

    // Room components
    implementation "androidx.room:room-ktx:$rootProject.roomVersion"
    kapt "androidx.room:room-compiler:$rootProject.roomVersion"
    androidTestImplementation "androidx.room:room-testing:$rootProject.roomVersion"

    // Lifecycle components
    implementation "androidx.lifecycle:lifecycle-viewmodel-ktx:$rootProject.lifecycleVersion"
    implementation "androidx.lifecycle:lifecycle-livedata-ktx:$rootProject.lifecycleVersion"
    implementation "androidx.lifecycle:lifecycle-common-java8:$rootProject.lifecycleVersion"

    // Kotlin components
    implementation "org.jetbrains.kotlin:kotlin-stdlib-jdk7:$kotlin_version"
    api "org.jetbrains.kotlinx:kotlinx-coroutines-core:$rootProject.coroutines"
    api "org.jetbrains.kotlinx:kotlinx-coroutines-android:$rootProject.coroutines"

    // UI
    implementation "androidx.constraintlayout:constraintlayout:$rootProject.constraintLayoutVersion"
    implementation "com.google.android.material:material:$rootProject.materialVersion"

    // Testing
    testImplementation "junit:junit:$rootProject.junitVersion"
    androidTestImplementation "androidx.arch.core:core-testing:$rootProject.coreTestingVersion"
    androidTestImplementation ("androidx.test.espresso:espresso-core:$rootProject.espressoVersion", {
        exclude group: 'com.android.support', module: 'support-annotations'
    })
    androidTestImplementation "androidx.test.ext:junit:$rootProject.androidxJunitVersion"





ext {
    activityVersion = '1.1.0'
    appCompatVersion = '1.2.0'
    constraintLayoutVersion = '2.0.2'
    coreTestingVersion = '2.1.0'
    coroutines = '1.3.9'
    lifecycleVersion = '2.2.0'
    materialVersion = '1.2.1'
    roomVersion = '2.2.5'
    // testing
    junitVersion = '4.13.1'
    espressoVersion = '3.1.0'
    androidxJunitVersion = '1.1.2'
}


```

# retrofit family
    def retrofitVersion = '2.5.0'
    implementation "com.squareup.retrofit2:retrofit:$retrofitVersion"
    implementation "com.squareup.retrofit2:converter-gson:$retrofitVersion"
    implementation "com.squareup.retrofit2:adapter-rxjava2:$retrofitVersion"
    implementation 'com.squareup.okhttp3:logging-interceptor:3.8.0'
    // Gson
    implementation 'com.google.code.gson:gson:2.8.6'
    
# ViewModel
    implementation "androidx.lifecycle:lifecycle-viewmodel-ktx:2.2.0"
    implementation "androidx.lifecycle:lifecycle-process:2.2.0"    
    implementation "androidx.fragment:fragment-ktx:1.2.5"
    implementation "androidx.lifecycle:lifecycle-extensions:2.0.0"


# Changing Styles
 `implementation 'com.airbnb.android:paris:1.4.0'`
 
# country code
    implementation 'com.hbb20:ccp:2.3.7'
    
# PinView
    implementation 'com.chaos.view:pinview:1.4.3'
# Glide 
```
  implementation 'com.github.bumptech.glide:glide:4.11.0'
  annotationProcessor 'com.github.bumptech.glide:compiler:4.11.0'
  ```
