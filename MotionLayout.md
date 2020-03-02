# MotionLayout 
a subclass from ConstraintLayout, added to Cl 2.0 
# At xml 
`androidx.constraintlayout.motion.widget.MotionLayout`



# Features 
- control transitions 

# `<OnSwipe>`
- add `motion:onTouchUp="stop"` to make Transition stop when user stop touching screen 
- `dragDirection`: direction that progress of Transition increase. 

# Constraint 
- used to specify what attributes should be changed of this View 
- can be `Layout`,`CustomAttribute` 
- `Layout`: change postions of view 
- `CustomAttribute`: change any attribute of view (attributes that view support such as `BackgroundColor`,.. etc)
    ```
      <CustomAttribute
                    motion:attributeName="BackgroundColor"
                    motion:customColorValue="#D81B60" />
    ```
    - `attributeName`: name of attribute
    - `customColorValue`: type of value and its values (supported is`customColorValue`,`customIntegerValue`,`customStringValue`,`customDimension`,`customBoolean`,`customFloatValue`).


# ImageFilterView 
ImageFilterView (which is a subclass to AppCompatImageView) 
- custome attributes allowed
    - saturation : 0 = grayscale, 1 = original, 2 = hyper saturated
    - contrast : 1 = unchanged, 0 = gray, 2 = high contrast
    - warmth : 1 = neutral, 2 = warm (red tint), 0.5 = cold (blue tint)
    - crossfade (with app:altSrc)


# Integration with existing view 
main idea is to control progress of Transition using Progress of existing view for 
- AppBar we can listen to `onOffsetChanged` to change progress 
``` kotlin 
class CollapsibleToolbar @JvmOverloads constructor(
        context: Context, attrs: AttributeSet? = null, defStyleAttr: Int = 0
) : MotionLayout(context, attrs, defStyleAttr), AppBarLayout.OnOffsetChangedListener {

    override fun onOffsetChanged(appBarLayout: AppBarLayout?, verticalOffset: Int) {
        progress = -verticalOffset / appBarLayout?.totalScrollRange?.toFloat()!!
        // start from 0 to 1 when it be collapsed
        println("Progress $progress")
    }

    override fun onAttachedToWindow() {
        super.onAttachedToWindow()
        // parent here as  AppBarLayout that contains CollapsibleToolbar using `include`
        (parent as? AppBarLayout)?.addOnOffsetChangedListener(this)
    }
}
```
- Drawer menue listen to `onDrawerSlide` to change progress 
``` kotlin
class DrawerContent @JvmOverloads constructor(
        context: Context, attrs: AttributeSet? = null, defStyleAttr: Int = 0
) : MotionLayout(context, attrs, defStyleAttr), DrawerLayout.DrawerListener {
    override fun onDrawerStateChanged(newState: Int) {
    }

    override fun onDrawerSlide(drawerView: View, slideOffset: Float) {
        progress = slideOffset
        println("Progress $progress")
    }

    override fun onDrawerClosed(drawerView: View) {
    }

    override fun onDrawerOpened(drawerView: View) {
    }

    override fun onAttachedToWindow() {
        super.onAttachedToWindow()
        (parent as? DrawerLayout)?.addDrawerListener(this)
    }
}
```

# Notes 
- view must have **id** to be displayed even if view has all constraints. 
- **KeyPosition** is used to specify changes in width, height and x,y coordinates
- So, if you want to have a keyframe that specifies something at the start of any transition, use framePosition = 1 instead.

# Attribtutes 
- **percentWidth**: amount of change in width of view
- **percentX**:amount of change in X position of view
