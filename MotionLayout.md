# MotionLayout 
a subclass from ConstraintLayout, added to Cl 2.0 

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

