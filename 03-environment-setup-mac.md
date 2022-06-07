---
<a name="Back_To_Top"></a> Top
---

- ### [MySQL on Mac](#MySQL_on_Mac)
- ### [Tools and installing Laravel](#Tools_and_installing_Laravel)

---

## <a name="MySQL_on_Mac"></a>MySQL on Mac

`brew install mysql`

`mysql --version`

`mysql -u root -p`

---

- [Top](#Back_To_Top)

---


## <a name="Tools_and_installing_Laravel"></a>Tools and installing Laravel

`brew cleanup`
`brew doctor`
`brew install composer`

Installation:

`composer create-project laravel/laravel example-app`
`cd example-app`
`php artisan serve --port=8003`

Laravel Installer as a global Composer dependency:

`composer global require laravel/installer`
`laravel new example-app`
`cd example-app`
`php artisan serve --port=8003` 

For this to work need to edit paths:

`sudo nano /etc/paths`
`/Users/warwicknortier/.composer/vendor/bin`

---

- [Top](#Back_To_Top)

---
