---
<a name="Back_To_Top"></a> Top
---

- ### [Migrations](#Migrations)
- ### [Creating & Dropping Migrations](#Creating_&_Dropping_Migrations)
- ### [Adding columns to existing tables](#Adding_columns_to_existing_tables)
- ### [More migration commands](#More_migration_commands)

---

## <a name="Migrations"></a>Migrations

### Login to backend container command line 

```
docker-compose exec vulacoin_be bash
```

### Create database from command line

```
php -uroot -p

create database new_db;
```

### Edit `.env` file

```
DB_DATABASE=new_db;
```

### Run `php artisan migrate` in the project directory

```
php artisan migrate
```

![guidelines](/images/00.png)


---

- [Top](#Back_To_Top)

---


## <a name="Creating_&_Dropping_Migrations"></a>Creating & Dropping Migrations

### We tell the command line tool that we want to create a table named posts.

```
 php artisan make:migration create_posts_table --create="posts"
 php artisan migrate
 ```

### Delete the last migration you did

```
php artisan migrate:rollback
```

---

- [Top](#Back_To_Top)

---


## <a name="Adding_columns_to_existing_tables"></a>Adding columns to existing tables


```
php artisan make:migration add_is_admin_column_to_posts_table --table="posts"
```

https://laravel.com/docs/9.x/migrations#indexes

```php
public function up()
{
    Schema::table('posts', function (Blueprint $table) {
        $table->tinyInteger('is_admin')->default('0');
    });
}
```

---

- [Top](#Back_To_Top)

---


## <a name="More_migration_commands"></a>More migration commands

### Delete/rollback all migrations

```
php artisan migrate:reset
```

### Refresh and re-run all migrations

```
php artisan migrate:refresh
```

### Show status of each migration

```
php artisan migrate:status
```

---

- [Top](#Back_To_Top)

---
