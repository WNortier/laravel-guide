---
<a name="Back_To_Top"></a> Top
---

- ### [Migrations](#Migrations)
- ### [Creating & Dropping Migrations](#Creating_&_Dropping_Migrations)

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


[Table Lookups -> nwId](https://github.com/WNortier/nextworld/blob/master/nextworld-platform-tutorials/01-build-an-application/00-build-an-application-overview.md#3_TABLE_LOOKUPS)
