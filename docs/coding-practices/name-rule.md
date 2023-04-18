---
sidebar_position: 2
---

# Name Rules

## 1. Controller

Quy tắc đặt tên:

- Tên controller phải bắt đầu bằng một danh từ tiếng Anh và viết hoa.
- Danh từ phải ở dạng số ít.
- Không chứa dấu cách.
- Luôn kết thúc bằng Controller.

```php
// Bad
UsersController, use_controller, UsersControllers

// Good
UserController
```

## 2. Route

Quy tắc đặt tên:

- route phải là một danh từ tiếng Anh.
- Danh từ phải ở dạng số nhiều.
- Không chứa dấu cách.

```php
<?php

use App\Http\UserController;

// Bad

Route::get('user', 'UserController');
Route::get('user/1', 'UserController');
Route::get('user_s', 'UserController');

// Good
Route::get('users', 'UserController');
```

## 3. Named route

Quy tắc đặt tên:

- Tên route phải phải là một danh từ tiếng Anh.
- Không chứa dấu cách.
- Phải đặt kiểu snake_case 🐍 và dấu chấm

```php
<?php

use App\Http\UserController;

// Bad

Route::get('users', 'UserController')->name('user-index');

// Good
Route::get('users', 'UserController')->name('user.index');
Route::get('users', 'UserController')->name('user.show_active');
```

## 4. Model

Quy tắc đặt tên:

- Tên Model phải phải là một danh từ tiếng Anh.
- Không chứa dấu cách.
- Phải là danh từ số ít

```php
<?php

namespace App\Models;

// Bad

class Users {
    ...
}

// Good
class User {
    ...
}
```

## 5. Relationship

Quy tắc đặt tên:

- Tên Relationship phải phải là một danh từ tiếng Anh.
- Không chứa dấu cách.
- hasOne hoặc belongsTo relationship sẽ là số ít
- Tất cả các relationships khác sẽ là số nhiều

```php
<?php

namespace App\Models;

class Tour extends Model
{
    // Bad

    public function review()
    {
        return $this->hasMany(Review::class);
    }

    public function places()
    {
        return $this->belongsTo(Place::class);
    }

    // Good
    public function reviews()
    {
        return $this->hasMany(Review::class);
    }

    public function place()
    {
        return $this->belongsTo(Place::class);
    }
}
```

## 6. Table (Tên bảng)

Quy tắc đặt tên:

- Tên Table phải phải là một danh từ tiếng Anh.
- Không chứa dấu cách.
- Phải là số nhiều

```php
<? php

class CreateUsersTable extends Migration
{
    public function up()
    {
        // Bad
        Schema::create('user', function (Blueprint $table) {
            ...
        });

        // Good
        Schema::create('users', function (Blueprint $table) {
            ...
        });
    }

    public function down()
    {
        // Bad
        Schema::dropIfExists('user');

        // Good
        Schema::dropIfExists('users');
    }
}
```

## 7. Tên cột trong bảng

Quy tắc đặt tên:

- Tên cột phải phải là một danh từ tiếng Anh.
- Không chứa dấu cách.
- Kiểu snake_case

```php
<? php

class CreateUsersTable extends Migration
{
    public function up()
    {
        // Bad
        Schema::create('users', function (Blueprint $table) {
            $table->string('fullName', 255)->nullable();
            $table->string('Password', 255)->nullable();
        });

        // Good
        Schema::create('users', function (Blueprint $table) {
            $table->string('full_name', 255)->nullable();
            $table->string('password', 255)->nullable();
        });
    }

    public function down()
    {
        Schema::dropIfExists('users');
    }
}
```

## 8. Variable

Quy tắc đặt tên:

- Tên biến phải phải là một danh từ tiếng Anh.
- Không chứa dấu cách.
- camelCase 🐫

```php
<? php

//Bad
$full_name, $FULL_NAME, $FullName

//Good
$fullName, $articlesWithAuthor
```

## 9. Blade view files

Quy tắc đặt tên:

- Tên view files phải phải là một danh từ tiếng Anh.
- Không chứa dấu cách.
- kebab_case

```php
//Bad
showFiltered.blade.php
show_filtered.blade.php

//Good
show-filtered.blade.php
```

## 10. Config

Quy tắc đặt tên:

- Tên Config phải phải là một danh từ tiếng Anh.
- Không chứa dấu cách.
- snake_case  🐍

```php
<?php

return [
    // Bad
    "users-per-page" => 10,
    "toursPerPage" => 10,

    // Good
    "users_per_page" => 10,
    "tours_per_page" => 10,
];
