---
<a name="Back_To_Top"></a> Top
---

- ### [Inserting Data](#Inserting_Data)
- ### [Reading Data](#Reading_Data)
- ### [Updating Data](#Updating_Data)
- ### [Deleting Data](#Deleting_Data)

---

## <a name="Inserting_Data"></a>Inserting Data

```php
Route::get('/insert', function(){

    DB::insert('insert into posts(title, content) values(?, ?)', ['PHP with Laravel', 'Laravel is awesome']);
})
```

---

- [Top](#Back_To_Top)

---


## <a name="Reading_Data"></a>Reading Data


```php
Route::get('/read', function(){
    
    $results = DB::select('select * from posts where id = ?', [1]);

    //return var_dump($results);

    foreach($results as $post){
        return $post->title;
    }
})
```

---

- [Top](#Back_To_Top)

---


## <a name="Updating_Data"></a>Updating Data

The update method returns the affected row. 

```php
Route::get('/update', function(){

    $updated = DB::update('update posts set title = "Update title" where id = ?', [1]);
    return $updated;
})
```

---

- [Top](#Back_To_Top)

---


## <a name="Deleting_Data"></a>Deleting Data

Returns `1` if the record was successfully deleted, else returns `0`.

```php
Route::get('/delete', function(){

    $deleted = DB::delete('delete from posts where id = ?', [1]);
    return $deleted;
})
```

---

- [Top](#Back_To_Top)

---


![advanced-css](./images/#.png)