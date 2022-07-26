1. Create 10 000 dummy fake rows in "blog" table:

 ```php  
 Blog::factory(10000)->create();
```

<br/><br/>
2. Iteration with query builder's ```all()``` method.<br/>
   This method keeps all retreived data in memory then iterates through them.
<br/>
Memory usage: 43 Mb.

```php 
$blog = Blog::all()->filter(function ($model){
        return $model->id > 5;
    });
    
    foreach ($blog as $b) {
        echo $b->id . ' - ';
    }
```

<br/><br/>
3. Iteration with query builder's ```cursor()``` method: <br/>
   This method keeps one eloquent model in memory at a time, and removes it after iteration. <br/>

Memory usage: 23 Mb.

```php 
$blog = Blog::cursor()->filter(function ($model){
        return $model->id > 4;
    });

    foreach ($blog as $b) {
        echo $b->id . ' - ';
    }
```
<br/><br/>
4. For both case only one query will be executed:

```sql 
select * from `blog`
```
