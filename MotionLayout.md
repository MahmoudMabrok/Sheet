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
