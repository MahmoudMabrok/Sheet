document.querySelectorAll('button[data-control-name="people_connect"]').forEach (function(r){
setTimeout(function(){
c = c +1 ; 
r.click();} , 100 * c);
})
