1. Loads all news from DB with single query.
2. Loads each category from DB with separate query

|     NewsModel.php  |  |
|-----------------------------------------------------------------------------------------------------------------------|--|
|                                                                                                                       |  |
```php
    public function getCategory(): \yii\db\ActiveQuery
    {
      return $this->hasOne(Categories::class, ['id' => 'category_id']);
    }
```


| SiteController.php |  |
|-----------------------------------------------------------------------------------------------------------------------|--|
|                                                                                                                       |  |

```php
    class SiteController extends Controller
    {
        public function actionNews()
        {
            $news = NewsModel::find()->all();
    
            return $this->render('newsView',[
                'news' => $news
            ]);
        }
    }
```

|    newsView.php    |  |
|-----------------------------------------------------------------------------------------------------------------------|--|
|                                                                                                                       |  |
```html
    <table class="table table-bordered">
        <tr>
            <th>Post</th>
            <th>Category</th>
        </tr>
        <?php foreach ($news as $new) { ?>
        <tr>
            <td><?= $new->title ?></td>
            <td><?= $new->category->title ?></td>
        </tr>
        <?php } ?>
    </table>
```


|     ALL SQL QUERIES DEBUG    |  |
|-----------------------------------------------------------------------------------------------------------------------|--|
|                                                                                                                       |  |
```sql
    SELECT * FROM `news`
    SELECT * FROM `categories` WHERE `id`=1
    SELECT * FROM `categories` WHERE `id`=2
    SELECT * FROM `categories` WHERE `id`=3
    SELECT * FROM `categories` WHERE `id`=4
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
