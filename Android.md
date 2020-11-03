# ViewHolder 
- Your code might call `findViewById()` frequently during the scrolling of ListView, which can **slow down performance**. Even when the Adapter returns an inflated view for recycling, you still need to look up the elements and update them. A way around repeated use of f`findViewById()` is to use the "view holder" design pattern.

# Vector Drawable 
- Another very important reason of using vector graphics rather than raster is their **size**
- Using AppCompat and `app:srcCompat` is the most foolproof method of integrating vector drawables into your app.
- Using **Android Studio Vector Convertor**
you can simply right click your drawable folder, `select new->Vector asset` and point it to your local SVG file


# Misc 
- ENABLE MultiDex
    - multiDexEnabled true
    - implementation 'com.android.support:multidex:1.0.3'
    - `class MyApplication : MultiDexApplication() {...}`
    - 
    ``` kotlin 
    class MyApplication : SomeOtherApplication() {

        override fun attachBaseContext(base: Context) {
            super.attachBaseContext(base)
            MultiDex.install(this)
        }
    }
    ```


- WakefulBroadcastReceiver 
    - This helper is for an old pattern of implementing a BroadcastReceiver that receives a device wakeup event and then passes the work off to a Service, while ensuring that the device does not go back to sleep during the transition.

    - This class takes care of creating and managing a partial wake lock for you; you must request the WAKE_LOCK permission to use it.
    - This class was **deprecated in API level 26.1.0.**
    As of Android O, background check restrictions make this class no longer generally useful. (It is generally not safe to start a service from the receipt of a broadcast, because you don't have any guarantees that your app is in the foreground at this point and thus allowed to do so.) Instead, developers should use **android.app.job.JobScheduler** to schedule a job, and this **does not require** that the app hold a **wake lock** while doing so (the system will take care of holding a wake lock for the job).

- For exact timing, you should absolutely be using AlarmManagerCompat and specifically, setExactAndAllowWhileIdle() which fires an alarm at exactly the specified time on all API levels.

# Touch Handling
- when touch event is fired **all views got notified**
- Then everyone is given a **chance to handle the event**, starting with the **view** on top and going all the way back to the **Activity**
- If a View (or a ViewGroup) *has an OnTouchListener*, then the touch event is handled by **OnTouchListener.onTouch()**. Otherwise it is handled by **onTouchEvent()**. If *onTouchEvent()* returns **true** for any touch event, then the handling **stops there**. No one else down the line gets a chance at it.
- The **ViewGroup** will notify **any children** it has of the touch event, including any ViewGroup children.
- Be aware that Event Listener is called before Event Handler,
- if Event Listener returns true, Event Handler won't be called



- Resources
    - [Manage touch events in a ViewGroup](https://developer.android.com/training/gestures/viewgroup.html)
    - [Mastering the Android Touch System](https://www.youtube.com/watch?v=EZAoJU-nUyI)
    - [Android UI Internal : Pipeline of View's Touch Event Handling](https://pierrchen.blogspot.com/2014/03/pipeline-of-android-touch-event-handling.html)
    - [231 Android onTouchEvent Part 1](https://www.youtube.com/watch?v=SYoN-OvdZ3M)
    
- Images 

<div>
<img src="https://user-images.githubusercontent.com/13488900/75970538-292dc100-5ed9-11ea-8200-eaeb39817269.png" /> 
<img src="https://user-images.githubusercontent.com/13488900/75976189-9db92d80-5ee2-11ea-97bd-c7b600233e23.png" />       
</div>    

- Code 
    ``` java
    public class MyViewGroup extends ViewGroup {

        private int mTouchSlop;

        ...

        ViewConfiguration vc = ViewConfiguration.get(view.getContext());
        mTouchSlop = vc.getScaledTouchSlop();

        ...

        @Override
        public boolean onInterceptTouchEvent(MotionEvent ev) {
            /*
             * This method JUST determines whether we want to intercept the motion.
             * If we return true, onTouchEvent will be called and we do the actual
             * scrolling there.
             */


            final int action = MotionEventCompat.getActionMasked(ev);

            // Always handle the case of the touch gesture being complete.
            if (action == MotionEvent.ACTION_CANCEL || action == MotionEvent.ACTION_UP) {
                // Release the scroll.
                mIsScrolling = false;
                return false; // Do not intercept touch event, let the child handle it
            }

            switch (action) {
                case MotionEvent.ACTION_MOVE: {
                    if (mIsScrolling) {
                        // We're currently scrolling, so yes, intercept the
                        // touch event!
                        return true;
                    }

                    // If the user has dragged her finger horizontally more than
                    // the touch slop, start the scroll

                    // left as an exercise for the reader
                    final int xDiff = calculateDistanceX(ev);

                    // Touch slop should be calculated using ViewConfiguration
                    // constants.
                    if (xDiff > mTouchSlop) {
                        // Start scrolling!
                        mIsScrolling = true;
                        return true;
                    }
                    break;
                }
                ...
            }

            // In general, we don't want to intercept touch events. They should be
            // handled by the child view.
            return false;
        }

        @Override
        public boolean onTouchEvent(MotionEvent ev) {
            // Here we actually handle the touch event (e.g. if the action is ACTION_MOVE,
            // scroll this container).
            // This method will only be called if the touch event was intercepted in
            // onInterceptTouchEvent
            ...
        }
    }

    ```
# Sign in with Apple using Firebase 
- enable apple as sign in method from firebase console 
- code 
      
``` kotlin

        // make provider 
        val provider = OAuthProvider.newBuilder("apple.com")
        provider.scopes = arrayOf("email", "name").toMutableList()

        // sign out if already logged (recommended)
        val user = FirebaseAuth.getInstance().currentUser
            if (user == null) {
                login(provider)
            } else {
                FirebaseAuth.getInstance().signOut()
                AuthUI.getInstance()
                    .signOut(this)
                    .addOnCompleteListener {
                        login(provider)
                    }
            }

        // login 
        FirebaseAuth.getInstance().startActivityForSignInWithProvider(this, provider.build())
                .addOnSuccessListener { authResult ->
                    // Sign-in successful!

                    authResult.user?.display()

                    authResult.user?.getIdToken(true)?.addOnSuccessListener {
                        Log.d(TAG, "token ${it.token}")
                    }


                }
                .addOnFailureListener { e ->
                    Log.w(TAG, "activitySignIn:onFailure", e)
                }

```

# Exo-Player 
- 
```
    implementation 'com.google.android.exoplayer:exoplayer-core:2.11.8'
    implementation 'com.google.android.exoplayer:exoplayer-dash:2.11.8'
    implementation 'com.google.android.exoplayer:exoplayer-ui:2.11.8'

    implementation 'com.github.HaarigerHarald:android-youtubeExtractor:master-SNAPSHOT'

```
- 
```

class VideoController(val video_view: PlayerView) {
    private var playWhenReady = true
    private var currentWindow = 0
    private var playbackPosition: Long = 0

    var player: ExoPlayer? = null


    fun initializePlayer(ctx: Context, url:String? ) {
        player = SimpleExoPlayer.Builder(ctx).build()
        video_view.player = player
        val mediaSource = buildMediaSource(ctx,Uri.parse(url ?: ""))
        player?.playWhenReady = playWhenReady
        player?.seekTo(currentWindow, playbackPosition)
        player?.prepare(mediaSource, false, false)
    }

    private fun buildMediaSource(ctx: Context, uri: Uri): MediaSource {
        //todo what userAgment?
        val dataSourceFactory: DataSource.Factory =
            DefaultDataSourceFactory(ctx, "exoplayer-codelab")

        return ProgressiveMediaSource.Factory(dataSourceFactory)
            .createMediaSource(uri)
    }

    fun releasePlayer() {
        if (player != null) {
            playWhenReady = player!!.playWhenReady
            playbackPosition = player!!.currentPosition
            currentWindow = player!!.currentWindowIndex
            player!!.release()
            player = null
        }
    }

}

```

- 
```
  object : YouTubeExtractor(requireContext()) {
            @SuppressLint("StaticFieldLeak")
            override fun onExtractionComplete(
                ytFiles: SparseArray<YtFile>,
                vMeta: VideoMeta
            ) {
                if (ytFiles != null) {
                    val itag = 22
                    val downloadUrl = ytFiles[itag].url
                    videoController.initializePlayer(requireContext(),downloadUrl)
                }
            }
        }.extract(url2, true, true)


```

# Edit text 
## hide underline text
` android:background="@null"`

## do action when click on IME ACTION 
```kotlin

    private fun doOnIME(
        view: EditText,
        actionType: Int,
        action: () -> Unit
    ) {
        view.setOnEditorActionListener { _, actionId, _ ->          
            if (actionId == actionType) {
                // do Action
                action()

            }
            return@setOnEditorActionListener true
        }
    }
```

# facenook integration 
- get base64 from [here](https://tomeko.net/online_tools/hex_to_base64.php)
- add it to `Facebook console ->  Settings -> Basic -> Android -> Key hashes`
- for `Class Name` -> we add ***Launcher activity**
- use this to accept request as tester/developer with facebook app [requests](https://developers.facebook.com/requests/)

# check if user has installed a recording app 
``` kotlin
    val apps: List<PackageInfo> = context.packageManager.getInstalledPackages(0)
        val recordingApps = apps.filter {
            Logger.log("MiscUtils isHaveRecordingAppRunning: installed ${it.packageName} ")
            it.packageName.contains("recorder") or
                    it.applicationInfo.name.toLowerCase(Locale.ENGLISH).contains("recorder")
        }
        return recordingApps.isNotEmpty()
```
