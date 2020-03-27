
// scroll to get all content.
window.scrollByPages(5);
// scroll to get all content.
window.scrollByPages(5);
// scroll to get all content.
window.scrollByPages(5);
// scroll to get all content.
window.scrollByPages(5);
// scroll to get all content.
window.scrollByPages(5);
// scroll to get all content.
window.scrollByPages(5);
// scroll to get all content.
window.scrollByPages(5);
// scroll to get all content.
window.scrollByPages(5);

setTimeout(function(){

var  i, l;
var x = document.querySelectorAll("a span strong");
l = x.length;
var total = 0; 
var item = ""; 
for (i = 0; i < l; i++) {
item = x[i].childNodes[0].data;
if (item.search("views") >= 0 ){
	var idx = item.search(" ");
	var a = item.substr(0,idx);
	var r = Number.parseInt(a);
	total = total + r;
}
}

console.log("post count" + l+ " with total " + total);
    
}, 5000);













