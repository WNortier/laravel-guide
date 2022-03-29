---
<a name="Back_To_Top"></a> Top
---

- ### [One to one relationship](#One_to_one_relationship)

---

## <a name="One_to_one_relationship"></a>One to one relationship

Relationships are functions that relate tables to tables. For example in a One to One relationship we could say that a user has one post. Or in a One to Many the user has many posts. 

To set this up we need to create a foreign key and also write a function in the parent model. 

*migrations/create_posts_table.php*
```php
    public function up()
    {
        Schema::create('posts', function (Blueprint $table) {
            $table->id();
            $table->integer('user_id')->unsigned(); // Add user_id column with unsigned() for only positive numbers
            $table->string('title');
            $table->string('content');
            $table->timestamps();
        });
    }
```

In the parent model we write the function that will run the query.

```php
    public function post(){
        return $this->hasOne('App\Models\Post');
    }
```

This is going to go to the posts table because we gave it a name space.

It's got to look for the column `user_id` automatically. This is by default OK by default is going to do it.

Now if you want to specify a different column you put it as a second parameter here coma `the_user_id`, for example.

If the `id` field was named differently you can also specify its name as a third parameter.

*routes/web.php*
```php
use App\Models\User;

Route::get('/user/{id}/post', function($id){
    return User::find($id)->post;
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

- ### [1 TEMPLATE](#1_TEMPLATE)

## <a name="1_TEMPLATE"></a>1 TEMPLATE

---

- [Top](#Back_To_Top)

---

![advanced-css](./images/#.png)