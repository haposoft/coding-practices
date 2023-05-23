Trong Laravel, "Query Builder" và "Eloquent" là hai công cụ mạnh mẽ được sử dụng để tạo và thao tác với các câu truy vấn trong cơ sở dữ liệu.
# Query builder
## Định nghĩa
- là một thành phần của Laravel cho phép bạn tạo và thực thi các câu truy vấn SQL một cách linh hoạt bằng cách sử dụng các phương thức PHP
- cung cấp một cú pháp dễ đọc và trực quan để xây dựng các truy vấn phức tạp mà không cần viết trực tiếp các câu truy vấn SQL
- Query Builder hỗ trợ nhiều tính năng như chọn cột, điều kiện, sắp xếp, tham số ràng buộc, ...

Ví dụ về Query Builder trong Laravel:
``` php
 $users = DB::table('users')
            ->select('name', 'email')
            ->where('active', true)
            ->orderBy('name', 'asc')
            ->get();

  ```
Ví dụ về Query Builder - lấy tạo sửa xóa :
```php
//create
DB::table('users')->insert([
    'name' => 'John Doe',
    'email' => 'john@example.com',
    'password' => bcrypt('password'),
]);

//update
DB::table('users')
    ->where('id', 1)
    ->update([
        'name' => 'Updated Name',
        'email' => 'updated@example.com',
    ]);

//delete
DB::table('users')->where('id', 1)->delete();

```

# Eloquent
## Định nghĩa
- là một ORM (Object-Relational Mapping) tích hợp trong Laravel.
- bạn có thể tương tác với các bảng trong cơ sở dữ liệu thông qua các mô hình (**models**) Laravel.
- Eloquent tự động ánh xạ các mô hình với các bảng tương ứng và cung cấp các phương thức và quan hệ để thao tác dữ liệu.

Ví dụ về Query Builder trong Laravel:
```php
class User extends Model
{
    protected $table = 'users';
}

User::all();
```
Ví dụ về Eloquent - lấy tạo sửa xóa :
```php
//create
$user = new User;
$user->name = 'John Doe';
$user->email = 'john@example.com';
$user->save();

//get
$users = User::all(); // Lấy tất cả các bản ghi trong bảng "users"
$user = User::find(1); // Lấy bản ghi có id = 1
$users = User::where('active', true)->get(); // Lấy các bản ghi thỏa điều kiện

//update
$user = User::find(1);
$user->name = 'Updated Name';
$user->save();

//delete
$user = User::find(1);
$user->delete();
```

Có thể tìm hiểu rõ hơn một số tính năng chính của ORM thông qua key word: Models; Relationships; Migrations; Eager Loading; Lazy Loading; Scopes; Events; Query Scopes; Soft Deletes; Seeding; Auto-populating; Object Casting; Event Handling, Polymorphic,...


# So sánh
- Query Builder tập trung vào việc tạo và thực thi các câu truy vấn SQL một cách linh hoạt và trực quan
- Eloquent tập trung vào việc làm việc với các đối tượng mô hình và cung cấp các phương thức và quan hệ để thao tác dễ dàng với dữ liệu.

### Tính linh hoạt
- Query Builder : xây dựng các câu truy vấn phức tạp hơn với các phương thức như join(), groupBy(), having() và union(), tùy chỉnh các phần tử của câu truy vấn một cách linh hoạt.
- Eloquent: cung cấp các quan hệ giữa các mô hình, cho phép bạn truy xuất dữ liệu từ các bảng liên quan một cách dễ dàng và tự nhiên.

### Đọc hiểu và bảo trì mã nguồn
- Query Builder : sử dụng cú pháp giống với SQL, nên việc đọc hiểu và bảo trì mã nguồn có thể dễ dàng hơn
- Eloquent: sử dụng các phương thức và quan hệ được định nghĩa trong mô hình, giúp mã nguồn trở nên dễ đọc, gọn gàng.

### Sự tiện lợi
- Query Builder : phù hợp cho các trường hợp cần tương tác với cơ sở dữ liệu mà không cần định nghĩa các mô hình riêng.
- Eloquent: đơn giản và tiện lợi cho việc thao tác với dữ liệu

# Khái niệm về eager loading và lazy loading

Trong Laravel, eager loading và lazy loading là 2 khái niệm quan trọng liên quan đến việc tải dữ liệu liên quan (related data) từ cơ sở dữ liệu.
Chúng giúp tối ưu hóa hiệu suất và giảm số lượng truy vấn cần thiết.

## Eager Loading
là một kỹ thuật cho phép ta tải toàn bộ dữ liệu liên quan (related data). Thay vì thực hiện nhiều truy vấn riêng lẻ cho mỗi mô hình liên quan
```php
$users = User::with('posts')->get();
//sử dụng phương thức with('posts') để eager load các bài đăng (posts) của mỗi người dùng
//Kết quả trả về là một collection của các đối tượng User, mỗi User chứa các thông tin người dùng và danh sách bài đăng liên quan.
```
## lazy loading
là một kỹ thuật cho phép ta tải dữ liệu liên quan chỉ khi cần thiết.

```php
$users = User::all();

foreach ($users as $user) {
    $posts = $user->posts; // Tải dữ liệu bài đăng của mỗi người dùng khi cần thiết
}

```

# N+1 Query 
- N+1 query xảy ra khi tìm nạp các mô hình liên quan dẫn đến nhiều truy vấn cơ sở dữ liệu, dẫn đến các vấn đề về hiệu suất.
- Thường gặp khi sử dụng lazy loading trong Laravel.

N+1 query xảy ra khi ta có một truy vấn để lấy danh sách các đối tượng gốc, sau đó trong vòng lặp ta truy cập vào thuộc tính liên quan của từng đối tượng. Khi đó, mỗi lần truy cập thuộc tính liên quan, Laravel sẽ thực hiện một truy vấn riêng để tải dữ liệu liên quan.

Ví dụ trên gặp vấn đề N+1 query
```php
$users = User::all();

foreach ($users as $user) {
    $posts = $user->posts; // Gây ra N+1 query problem
}

```
Để giải quyết vấn đề N+1 query, chúng ta có thể sử dụng eager loading

```php
$users = User::with('posts')->get();

foreach ($users as $user) {
    $posts = $user->posts; // Dữ liệu đã được tải trước (eager loaded)
}

```
