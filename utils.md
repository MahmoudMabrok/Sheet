var c = 1; 

document.querySelectorAll('button[data-control-name="people_connect"]').forEach (function(r){
setTimeout(function(){
c = c +1 ; 
r.click();} , 1500 * c);
});

window.loaction.reload();

```



import org.jsoup.Jsoup
import org.jsoup.nodes.Document
import java.io.BufferedReader
import java.io.InputStreamReader
import java.lang.StringBuilder
import java.net.URL
import java.net.URLConnection


fun main() {

    val links = listOf("https://www.youtube.com/playlist?list=PL2-FkZlJhxqVXZO1c6gKgsAdiet0zcOAO" ,
        "https://github.com/MahmoudMabrok/QuranyApp")
    links.forEach {
        // print header
        println("Link : $it")
        // start working
        parse(it)
    }

}

fun extractPageTextFromUrl(url:String): String {
    val oracle = URL(url)
    val yc: URLConnection = oracle.openConnection()
    yc.readTimeout = 60 * 1000
    yc.connectTimeout = 60 * 1000
    val input = BufferedReader(InputStreamReader(yc.getInputStream()))
    val sb  = StringBuilder()
    while (input.readLine().also { it?.let { str ->  sb.append(str) } } != null){}
    input.close()
    return sb.toString()
}

fun parse(baseLink: String) {
  /*  println("Start Download Page")
    val text = extractPageTextFromUrl(baseLink)
    println("End Download")
    println("Start Pasing Page")*/
    val doc: Document = Jsoup.connect(baseLink).get()
    doc.hasText()
    println(" doc.hasText()${ doc.hasText()} foc ${doc.title()} ${doc.documentType()}")
    val items = doc.select("td")
    println("Items : ${items.size}")
    items.forEach {
        // print header
        println("Item : $it")
        val img = it.select("imge#img")
        val imgLink = img.attr("src")
        println("Image : $img , Link $imgLink")
    }
}







```

# Youtube Linker 

```
let data = [] 
document.querySelectorAll('a.yt-simple-endpoint.style-scope.ytd-playlist-video-renderer').forEach(function(element){
let title = element.querySelector("#video-title")["title"];
let url = element["href"];
console.log("link " + url + " title " + title );
data.push({group:"الدورة التأهيلية الثالثة عشر للحياة الزوجية
", name: title , url: url});
});

let stro = JSON.stringify(data);

```

