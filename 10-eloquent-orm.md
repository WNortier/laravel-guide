---
<a name="Back_To_Top"></a> Top
---

- ### [Reading Data](#Reading_Data)
- ### [Retrieving Data](#Retrieving_Data)
- ### [Inserting or saving data](#Inserting_or_saving_data)
- ### [Creating data and configuring mass assignment](#Creating_data_and_configuring_mass_assignment)
- ### [Updating with eloquent](#Updating_with_eloquent)
- ### [Deleting data](#Deleting_data)
- ### [Soft Deletes](#Soft_Deletes)

---

## <a name="Reading_Data"></a>Reading Data

```
php artisan make:model Post
```

This creates a post model which assumes you have a table named `posts` and a primaryKey named `id`

```php
namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;

class Post extends Model
{
    use HasFactory;
    
    protected $table = 'posts';
    protected $primaryKey = 'id';
}
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


## <a name="Inserting_or_saving_data"></a>Inserting or saving data

*routes/web.php*
```php
Route::get('/basicInsert', function(){
    $post = new Post;

    $post->title = "New Eloquent title insert";
    $post->content = "Wow eloquent is really cool, look at this content";
    $post->save();
});
```

You can also update a post

*routes/web.php*
```php
Route::get('/basicUpdate', function(){
    $post = Post::find(1);

    $post->title = "New Eloquent title insert";
    $post->content = "Wow eloquent is really cool, look at this content";
    $post->save();
});
```


---

- [Top](#Back_To_Top)

---


## <a name="Creating_data_and_configuring_mass_assignment"></a>Creating data and configuring mass assignment

```php
namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;

class Post extends Model
{
    use HasFactory;
    
    protected $table = 'posts';
    protected $primaryKey = 'id';
    protected $fillable = ['title', 'content'];
}
```

*routes/web.php*
```php
Route::get('/create', function(){
    Post::create(['title'=>'the create method', 'content'=>'I\'m learning alot']);
});
```

---

- [Top](#Back_To_Top)

---

## <a name="Updating_with_eloquent"></a>Updating with eloquent

*routes/web.php*
```php
Route::get('/update', function(){
    Post::where('id', 2)->where('is_admin', 0)->update(['title'=>'new title', 'content'=>'i love my instructor']);
});
```

---

- [Top](#Back_To_Top)

---


## <a name="Deleting_data"></a>Deleting data

*routes/web.php*
```php
Route::get('/delete', function(){
    $post = Post::find(2);
    $post->delete();

    Post::where('is_admin', 0)->delete();
});
```

#### Method 2

*routes/web.php*
```php
Route::get('/delete', function(){
    Post::destroy([4,5]); // deletes posts with id 4 and 5
});
```

---

- [Top](#Back_To_Top)

---


## <a name="Soft_Deletes"></a>Soft Deletes

Soft deletes can put a timestamp on a new column called `deleted_at` which lets laravel know that its not deleted until you force it to delete

Step 1: We need to import the class SoftDeletes

```php
namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\SoftDeletes;

class Post extends Model
{
    use HasFactory;
    use SoftDeletes;

    protected $table = 'posts';
    protected $primaryKey = 'id';
    protected $fillable = ['title', 'content'];
    protected $dates = ['deleted_at'];
}
```

```
php artisan make:migration add_deleted_at_column_to_posts_table --table=posts
```

Step 2: Edit migration file

```php
public function up()
{
    Schema::table('posts', function (Blueprint $table) {
        $table->softDeletes();
    });
}

public function down()
{
    Schema::table('posts', function (Blueprint $table) {
        $table->dropColumn('deleted_at');
    });
}
```

*routes/web.php*
```php
Route::get('/softdelete', function(){
    Post::find(1)->delete();
});
```

## Read Softdeletes

*routes/web.php*
```php
Route::get('/readsoftdelete', function(){
    // $posts = Post::withTrashed()->where('id', 1)->get(); // return all posts including trashed posts
    // return $posts;

    $posts = Post::onlyTrashed()->where('is_admin', 0)->get(); // return only trashed posts
    return $posts;
});
```

## Restore Softdeletes

*routes/web.php*
```php
Route::get('/restore', function(){
    Post::onlyTrashed()->where('is_admin', 0)->restore();
});
```

## Delete a softdelete permanently

*routes/web.php*
```php
Route::get('/forceDelete', function(){
    Post::onlyTrashed()->where('is_admin', 0)->forceDelete();
});
```
---

- [Top](#Back_To_Top)

---
