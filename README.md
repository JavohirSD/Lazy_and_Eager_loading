

| SiteController.php |  |
|-----------------------------------------------------------------------------------------------------------------------|--|
|                                                                                                                       |  |


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

|    newsView.php    |  |
|-----------------------------------------------------------------------------------------------------------------------|--|
|                                                                                                                       |  |

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


|     NewsModel.php  |
|-----------------------------------------------------------------------------------------------------------------------|--|
|                                                                                                                       |  |

    public function getCategory(): \yii\db\ActiveQuery
    {
      return $this->hasOne(Categories::class, ['id' => 'category_id']);
    }

|      SQL QUERIES DEBUG    |  |
|-----------------------------------------------------------------------------------------------------------------------|--|
|                                                                                                                       |  |

    SELECT * FROM `news`
    SELECT * FROM `categories` WHERE `id`=1
    SELECT * FROM `categories` WHERE `id`=2
    SELECT * FROM `categories` WHERE `id`=3
    SELECT * FROM `categories` WHERE `id`=4



|///////////////////////////////////////////      DB STRUCTURE DEBUG    ////////////////////////////////////////////////////|  |
|-----------------------------------------------------------------------------------------------------------------------|--|
|                                                                                                                       |  |

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
