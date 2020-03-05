# ViewHolder 
- Your code might call `findViewById()` frequently during the scrolling of ListView, which can **slow down performance**. Even when the Adapter returns an inflated view for recycling, you still need to look up the elements and update them. A way around repeated use of f`findViewById()` is to use the "view holder" design pattern.

# Vector Drawable 
- Another very important reason of using vector graphics rather than raster is their **size**
- Using AppCompat and `app:srcCompat` is the most foolproof method of integrating vector drawables into your app.
- Using **Android Studio Vector Convertor**
you can simply right click your drawable folder, `select new->Vector asset` and point it to your local SVG file


# Misc 

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

- Resources
    - [Manage touch events in a ViewGroup](https://developer.android.com/training/gestures/viewgroup.html)
    - [Mastering the Android Touch System](https://www.youtube.com/watch?v=EZAoJU-nUyI)
    - [Android UI Internal : Pipeline of View's Touch Event Handling](https://pierrchen.blogspot.com/2014/03/pipeline-of-android-touch-event-handling.html)
    - [231 Android onTouchEvent Part 1](https://www.youtube.com/watch?v=SYoN-OvdZ3M)



