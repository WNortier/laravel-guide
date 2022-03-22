---
<a name="Back_To_Top"></a> Top
---

- ### [Reading Data](#Reading_Data)
- ### [Retrieving Data](#Retrieving_Data)

---

## <a name="Reading_Data"></a>Reading Data

```
php artisan make:model Post
```

*routes/web.php*
```php
use App\Models\Post;

Route::get('/read', function(){
    $posts = Post::all();

    foreach($posts as $post) {
        return $post->content;
    }
});
```

---

- [Top](#Back_To_Top)

---


## <a name="Retrieving_Data"></a>Retrieving Data

*routes/web.php*
```php
use App\Models\Post;

Route::get('/findwhere', function(){
    $posts = Post::all();
    $posts = Post::where('id', 3)->orderBy('id', 'desc')->take(1)->get();
    return $posts;
});


Route::get('/findmore', function(){
    // $posts = Post::findOrFail(1);
    $posts = Post::where('users_count', '<', 50)->firstOrFail();
    return $posts;
});
```

---

- [Top](#Back_To_Top)

---

- ### [1 TEMPLATE](#1_TEMPLATE)

## <a name="1_TEMPLATE"></a>1 TEMPLATE

---

- [Top](#Back_To_Top)

---

![advanced-css](./images/#.png)