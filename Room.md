# Room 
The Room **persistence library** provides an abstraction layer over **SQLite** to allow for more robust database access while harnessing the full power of **SQLite**.

# Issues & cases 
## 1.Sorting 
I have faced case that data was displayed with different order of its insertion in database(i.e It was comming from api and stored with Room)
``` kotlin
@Entity(tableName = "Movies")
data class MovieItem(
    val adult: Boolean?,
    val backdrop_path: String?,
    @PrimaryKey
    val id: Int)

```
I was using [MoviesApi](https://www.themoviedb.org/documentation/api)  to get `TopRated` and `Popular` movies I have discovered that **Room sort** rows by default using `primary key` while data in api not sorted. 

## Solution 
use addition auto generated id as primary key to keep track insertion order of movies 
so it became 
``` kotlin
 @Entity(tableName = "Movies")
 data class MovieItem(
    @PrimaryKey(autoGenerate = true)
    val idAUTO: Int,
    val adult: Boolean?,
    val backdrop_path: String?,
    val id: Int)
```

# 2.Triggers 
when any updates is occurs with Table it notifies all listener even if they not concerned with this updates  
for example 
``` kotlin
 @Query("SELECT * FROM Movies WHERE isTop = 1")
    fun getTop(): LiveData<List<MovieItem>>
```
here it this `dao`method used to retrieve movies with some specific condition but it will be notified even if this list of movies not changed as Room trigger with any change (i.e insert,update or delete)

## Solution
[medium article](https://medium.com/androiddevelopers/7-pro-tips-for-room-fbadea4bfbd1#5e38)
a brife for solution [Will be added]


# 3.using Same Entity for two Tables
I was need to store list of favourite movies, there was some ideas to do this
1. add a **field** in Entity to specify it as Favourite and use a query to get these favourite 
2. **duplicate** same Entity as different table 

Let's analyze both

## First 
- It uses same table so no speed ovherhead 
- but if we clear this table data for any reason, Favourite also been deleted.

## Second 
- data will be saved even if movies was deleted 
- a new table is created which is *overhead* also overhead to convert Movie into Favourite

To Convert `Movie` into `Favourite`, I have used 
``` kotlin 
  val str = Gson().toJson(viewModel.moviesSelected, MovieItem::class.java)
        val fav = Gson().fromJson<FavouriteItem>(str, FavouriteItem::class.java)
        if (fav != null) {
            viewModel.addFavourite(fav)
            context?.show("${fav.title} Added")
        }
```
