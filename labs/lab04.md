# ISTA-322 ASP.NET MVC Lab 4
## Charles Carter
### September 22, 2017

1. Create a new ASP.NET MVC application in Visual Studio. Place the project in your **\ISTA-322\labs\lab04** directory. Name the project **MvcMusicStore**. Add unit tests. Change authentication to individual user accounts.

2. Add a new model named **Album** as follows:
```
public class Album
{
public virtual int AlbumId { get; set; }
public virtual int GenreId { get; set; }
public virtual int ArtistId { get; set; }
public virtual string Title { get; set; }
public virtual decimal Price { get; set; }
public virtual string AlbumArtUrl { get; set; }
public virtual Genre Genre { get; set; }
public virtual Artist Artist { get; set; }
}
```

3. Add a new model named **Artist** as follows:
```
public class Artist
{
public virtual int ArtistId { get; set; }
public virtual string Name { get; set; }
}
```

4. Add a new model named **Genre** as follows:
```
public class Genre
{
public virtual int GenreId { get; set; }
public virtual string Name { get; set; }
public virtual string Description { get; set; }
public virtual List<Album> Albums { get; set; }
}
```

5. Compile your application, correcting your errors.

6. Add a controller using the scaffold **MVC 5 Controller with Views, Using Entity Framework**.

    1. Name the controller **StoreManagerController**
    1. Name the model class **Album (MvcMusicStore.Models)**
    1. Name the data context class **MvcMusicStore.Models.MusicStoreDB**
    1. Generate views, reference script libraries, and use a layout page.

7. Create a new MusicStoreDbInitializer class in your Models folder, inserting the Seed method shown  below.

```
    public class MusicStoreDbInitializer : System.Data.Entity.DropCreateDatabaseAlways<MusicStoreDB>
    {
        protected override void Seed(MusicStoreDB context)
        {
            context.Artists.Add(new Artist {Name = "Al Di Meola"});
            context.Genres.Add(new Genre { Name = "Jazz" });
            context.Albums.Add(new Album {
                Artist = new Artist { Name="Rush" },
                Genre = new Genre { Name="Rock" },
                Price = 9.99m,
                Title = "Caravan" }
            );
            base.Seed(context);
        }
    }
```
8. In the **Global.asax.cs** file, in the **Application_Start()** method, add the following using directives:
```
    using System.Data.Entity;
    using MvcMusicStore.Models;
```
9. In the **Global.asax.cs** file, in the **Application_Start()** method, add the following line:
```
    Database.SetInitializer(new MusicStoreDbInitializer());
```
10. Rebuild your application and correct all errors.

11. Using **Debug, Start Without Debugging**, navigate to the StoreManager with a URL similar to this:
```
    http://localhost:50718/StoreManager
```
12. Navigate to the Edit menu, using a URL similar to the one below, and edit the album.
```
    http://localhost:50718/StoreManager/Edit/1
```

