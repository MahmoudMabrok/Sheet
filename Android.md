# ViewHolder 
- Your code might call `findViewById()` frequently during the scrolling of ListView, which can **slow down performance**. Even when the Adapter returns an inflated view for recycling, you still need to look up the elements and update them. A way around repeated use of f`findViewById()` is to use the "view holder" design pattern.

# Vector Drawable 
- Another very important reason of using vector graphics rather than raster is their **size**
- Using AppCompat and `app:srcCompat` is the most foolproof method of integrating vector drawables into your app.
- Using **Android Studio Vector Convertor**
you can simply right click your drawable folder, `select new->Vector asset` and point it to your local SVG file
