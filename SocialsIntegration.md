# Google 

# Facebook 




## Issues 
- `Using facebook SDK on Android gives “User logged in as different Facebook user.” error` -> 
**Solution** 
  ```
  if(LoginManager.getInstance()!=null){
          LoginManager.getInstance().logOut();
      }
  Write before "registerCallback();" method
  ```




# Twitter 



