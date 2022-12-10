1. Loads all news from DB with single query.
2. Loads all category from DB with single query

|     NewsModel.php  |  |
|-----------------------------------------------------------------------------------------------------------------------|--|
|                                                                                                                       |  |
```php
    public function category()
    {
        return $this->belongsTo(Category::class, 'category_id','id');
    }
```


| SiteController.php |  |
|-----------------------------------------------------------------------------------------------------------------------|--|
|                                                                                                                       |  |

```php
    public function index(): Renderable
    {
        $news = News::with('category')->get();

        return view('newsBlade', [
            'news' => $news
        ]);
    }
```

|    newsBlade.php    |  |
|-----------------------------------------------------------------------------------------------------------------------|--|
|                                                                                                                       |  |
```html
    <table class="table table-bordered">
        <tr>
            <th>Post</th>
            <th>Category</th>
        </tr>
       @foreach ($news as $new)
        <tr>
            <td>{{ $new->title }}</td>
            <td>{{ $new->category?->title_uz }}</td>
        </tr>
       @endforeach
    </table>
```


|     ALL SQL QUERIES DEBUG    |  |
|-----------------------------------------------------------------------------------------------------------------------|--|
|                                                                                                                       |  |
```sql
    select * from `news`
    select * from `categories` where `categories`.`id` = 1 limit 1
    select * from `categories` where `categories`.`id` = 2 limit 1
    select * from `categories` where `categories`.`id` = 3 limit 1
    select * from `categories` where `categories`.`id` = 4 limit 1
```


|      DB STRUCTURE    |  |
|-----------------------------------------------------------------------------------------------------------------------|--|
|                                                                                                                       |  |
```sql
    SELECT * FROM `categories`
    id  title          status  created_date            updated_date       
    1   Category 001   1       2022-07-20 12:14:36     2022-07-20 12:14:36
    2   Category 002   1       2022-07-20 12:15:01     2022-07-20 12:15:01
    3   Category 003   1       2022-07-20 12:15:01     2022-07-20 12:15:01
    4   Category 004   1       2022-07-20 12:15:01     2022-07-20 12:15:01
    5   Category 005   1       2022-07-20 12:15:01     2022-07-20 12:15:01
    6   Category 006   1       2022-07-20 12:15:01     2022-07-20 12:15:01
    
    
    SELECT * FROM `news`
    id  title          status  created_date            updated_date          category_id
    1   My title 001   1       2022-07-20 12:14:36     2022-07-20 12:14:36   1
    2   My title 002   1       2022-07-20 12:15:01     2022-07-20 12:15:01   1
    3   My title 003   1       2022-07-20 12:15:01     2022-07-20 12:15:01   2
    4   My title 004   1       2022-07-20 12:15:01     2022-07-20 12:15:01   3
    5   My title 005   1       2022-07-20 12:15:01     2022-07-20 12:15:01   4
```



|      NEWS OBJECT AFTER QUERY   |  |
|-----------------------------------------------------------------------------------------------------------------------|--|
|  
```
Array
(
    [0] => backend\models\News Object
        (
            [id] => 1
            [title] => My title 001
            [status] => 1
            [category_id] => 1
            [created_date] => 2022-07-20 14:12:00
            [updated_date] => 2022-07-20 12:14:36
            [category] => Array
                (
                    [id] => 1
                    [title] => Category 001
                    [status] => 1
                    [created_date] => 2022-07-20 12:14:36
                    [updated_date] => 2022-07-20 12:14:36
                )

        )

        [1] => backend\models\News Object
        (
            [id] => 2
            [title] => My title 002
            [status] => 1
            [category_id] => 1
            [created_date] => 2022-07-20 14:12:00
            [updated_date] => 2022-07-20 12:14:36
            [category] => Array
                (
                    [id] => 1
                    [title] => Category 002
                    [status] => 1
                    [created_date] => 2022-07-20 12:14:36
                    [updated_date] => 2022-07-20 12:14:36
                )

        )
        
        [2] => backend\models\News Object
        (
            [id] => 3
            [title] => My title 003
            [status] => 1
            [category_id] => 1
            [created_date] => 2022-07-20 14:12:00
            [updated_date] => 2022-07-20 12:14:36
            [category] => Array
                (
                    [id] => 1
                    [title] => Category 003
                    [status] => 1
                    [created_date] => 2022-07-20 12:14:36
                    [updated_date] => 2022-07-20 12:14:36
                )
        )
)
..................
```
