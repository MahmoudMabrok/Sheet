# Simulate delay
- Helpful in case  the tested method use Handler (post, postDelayed)

``` KOTLIN
Robolectric.runUiThreadTasksIncludingDelayedTasks();
```
 Or
``` KOTLIN
Robolectric.pauseMainLooper();
Robolectric.getUiThreadScheduler().advanceBy(intervalMs);
Robolectric.unPauseMainLooper();
```
