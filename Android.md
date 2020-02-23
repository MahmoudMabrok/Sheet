# ViewHolder 
- Your code might call `findViewById()` frequently during the scrolling of ListView, which can **slow down performance**. Even when the Adapter returns an inflated view for recycling, you still need to look up the elements and update them. A way around repeated use of f`findViewById()` is to use the "view holder" design pattern.
