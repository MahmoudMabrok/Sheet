var c = 1; 

document.querySelectorAll('button[data-control-name="people_connect"]').forEach (function(r){
setTimeout(function(){
c = c +1 ; 
r.click();} , 1500 * c);
})
