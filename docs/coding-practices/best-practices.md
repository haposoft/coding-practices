---
sidebar_position: 3
---

# Khởi tạo biến (Variable Initialization)

## Biến nên được khởi tạo trước khi sử dụng

````php
<?php

// Acceptable
<?php

$movies = get_movies();

// EOF

cách viết trên có thể chấp nhận nhưng biến $movie nên được khai báo trước khi sử dụng

//or

<?php 

if ( $expr ) {
	 // .... 
} $movies = array ();
$movies = get_movie(); //EOF

Cách viết này cũng có thể chấp nhận được nhưng nên khởi tạo trước cả câu điều kiện If()

// Preferred
<?php

$movies = array();

if ($expr) {
	// ....
}

$movies = get_movies();

// EOF
````
# Lệnh khởi tạo/khai báo (Initialization/Declaration Order)
## Lệnh khởi tạo/khai báo
1. trình tự khởi tạo/khai báo
- Khởi tạo biến ở phạm vi global, tiếp đến là các constant và cuối cùng là các biến local
- Khởi tạo với các thuộc tính sau đó mới đến các hàm trong class
- Ưu tiên khởi tạo phương thức bằng public, sau đó đến protected và cuối cùng là private
- Nên sắp xếp theo bảng chữ cái tiếng anh
````php
<?php

//bad
<?php

define('ENVIRONMENT', 'PRODUCTION');

$id = 0;

global $app_config;

// EOF
Sai thứ tự, thứ tự đúng phải là phải khai báo biến $app_config đầu tiên, sau đó tiếp theo là khai báo biến môi trường ENVIRONMENT cuối cùng mới là khai báo biến $id

//good 
<?php

global $app_config;

define('ENVIRONMENT', 'PRODUCTION');

$id = 0;
// EOF

//bad
<?php

namespace MyCompany\Model;

class Office
{
	public function get_name() {
		// ...
	}

	private $name
}

// EOF
Sai vì khai báo function get_name() trước $name

// good
<?php

namespace MyCompany\Model;

class Office
{
    private $name
	public function get_name() {
		// ...
	}
}

// EOF

//bad
<?php

namespace MyCompany\Model;

class Office
{
	private $id;
	private $name;
	private $status;

	private function get_name() {
		// ...
	}

	public function get_id() {
		// ...
	}

	protected function get_status() {
		// ...
	}
}
// EOF
Sai vì không khai báo get_id() trước tiên sau đó mới đến get_status() cuối cùng mới là get_name()

//good 
<?php

namespace MyCompany\Model;

class Office
{
	private $id;
	private $name;
	private $status;

    public function get_id() {
		// ...
	}

    protected function get_status() {
		// ...
	}

	private function get_name() {
		// ...
	}	
}
// EOF
//Acceptable
<?php

global $db_connection,
	$app_config,
	$cache;

define('MODE', 1);
define('ENVIRONMENT', 'PRODUCTION');

$id = 0;
$firstname = '';
$lastname = '';

// EOF
Đoạn code này có thể chấp nhận được nhưng biến global và constant phải theo bảng chữ cái

//good
<?php

global $app_config,
	$cache,
	$db_connection;

define('ENVIRONMENT', 'PRODUCTION');
define('MODE', 1);

$id = 0;
$firstname = '';
$lastname = '';

// EOF
````
# Globals
- Globals không nên được sử dụng

````php
<?php
//Acceptable
<?php

$pdo = new PDO('mysql:host=localhost;dbname=test', $user, $pass);

function get_user($id) {
	global $pdo;
	// ...
}
// EOF
Có thể chấp nhận được, nhưng global nên tránh việc khởi tạo biến.

//good
<?php

function get_database_object() {
	return new PDO('mysql:host=localhost;dbname=test', $user, $pass);
}

function get_user($id) {
	$pdo = get_database_object();
	// ...
}

// EOF
````

# Explicit Expressions
- Nên sử dụng các biểu thức rõ ràng
````php
<?php
//Acceptable
<?php

if ($expr == true) {
	// ...
}

// EOF
Có thể chấp nhận được, nhưng '===' có thể được sử dụng ở đây để thay thế.
//Preferred
<?php

if ($expr === true) {
	// ...
}

// EOF
````
