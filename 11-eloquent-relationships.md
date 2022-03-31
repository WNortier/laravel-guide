---
<a name="Back_To_Top"></a> Top
---

- ### [One to one relationship](#One_to_one_relationship)
- ### [The inverse relation](#The_inverse_relation)
- ### [One to many relationship](#One_to_many_relationship)
- ### [Many to many relations](#Many_to_many_relations)
- ### [Querying intermediate table](#Querying_intermediate_table)
- ### [Has many through relation](#Has_many_through_relation)

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

*models/user*
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

## <a name="The_inverse_relation"></a>The inverse relation

Inversely, we can also find the user whos post it is.

*routes/web.php*
```php
    Route::get('/post/{id}/user', function($id){
        return Post::find($id)->user->name;
    });
```

*models/post*
```php
    public function user(){
        return $this->belongsTo('App\Models\User');
    }
```

---

- [Top](#Back_To_Top)

---

## <a name="One_to_many_relationship"></a>One to many relationship

With a one to many relationship we can find all the posts of a particular user.

*routes/web.php*
```php
    Route::get('/user/{id}/posts', function($id){
        $user = User::find($id);

        foreach($user->posts as $post) {
            echo $post->title . "<br>";
        }
    });
```

*models/user*
```php
    public function posts(){
        return $this->hasMany('App\Models\Post');
    }
```

---

- [Top](#Back_To_Top)

---


## <a name="Many_to_many_relations"></a>Many to many relations

A pivot table is a lookup table that can be used to relate 2 other tables. Laravel has a lot of conventions for when working with a pivot table. If we follow those conventions we don't need to make a lot of customizations.

We're setting up a relationship between the `users` table and the `roles` table

*Step 1:* Create the `roles` table (`users` table already exists)

`php artisan make:model Role -m`

*migrations/create_roles_table.php*
```php
    public function up()
        {
            Schema::create('roles', function (Blueprint $table) {
                $table->id();
                $table->string('name'); // add name column
                $table->timestamps();
            });
        }
```

*Step 2* Create users roles table

`php artisan make:migration create_users_roles_table --create=role_user`

*migrations/create_users_roles_table.php*

```php
    public function up()
    {
        Schema::create('role_user', function (Blueprint $table) {
            $table->id();
            $table->integer('user_id'); //add user_id foreign key
            $table->integer('role_id'); //add role_id foreign key
            $table->timestamps();
        });
    }
```

### In the model you can define the table name as well as the foreign keys if you didn't follow the Laravel convention of singular and all lower case. 

*models/user*
```php
    public function roles(){
        // return $this->belongsToMany('App\Models\Role', 'user_roles', 'role_id', 'user_id');
        return $this->belongsToMany('App\Models\Role');
    }
```

*routes/web.php*
```php
    Route::get('/user/{id}/role', function($id){

        $user = User::find($id)->roles()->orderBy('id', 'desc')->get();

        return $user;

        // $user = User::find($id);

        // foreach($user->roles as $role) {
        //     echo $role->name . "<br>";
        // }
    });
```

---

- [Top](#Back_To_Top)

---


## <a name="Querying_intermediate_table"></a>Querying intermediate table

*models/user*
```php
    public function roles(){
        return $this->belongsToMany('App\Models\Role')->withPivot('created_at');
    }
```

*routes/web.php*
```php
    Route::get('user/pivot', function(){
        $user = User::find(1);

        foreach($user->roles as $role){
            return $role->pivot->created_at;
        }
    });
```

---

- [Top](#Back_To_Top)

---


## <a name="Has_many_through_relation"></a>Has many through relation

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