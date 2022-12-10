1. Create 10 000 dummy fake rows in "blog" table:

 ```php  
 Blog::factory(10000)->create();
```

2. Test iteration with query builder's ```all()``` method.&nbsp;
   This method keeps all retreived data in memory then iterates through them.
&nbsp;
Memory usage: 43 Mb.

```php 
$blog = Blog::all()->filter(function ($model){
        return $model->id > 5;
    });
    
    foreach ($blog as $b) {
        echo $b->id . ' - ';
    }
```


3. Test iteration with query builder's ```cursor()``` method: &nbsp;
   This method keeps one eloquent model in memory at a time, and removes it after iteration. &nbsp;

Memory usage: 23 Mb.

```php 
$blog = Blog::cursor()->filter(function ($model){
        return $model->id > 4;
    });

    foreach ($blog as $b) {
        echo $b->id . ' - ';
    }
```

4. For both case only one query will be executed:

```sql 
select * from `blog`
```
