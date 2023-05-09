---
sidebar_position: 6
---

# Loop, If statements

## 1. Sử dụng biến có tên có ý nghĩa để giúp tăng độ đọc hiểu của code

```php
<?php

// Nen
for ($i = 0; $i < count($array); $i++) {
    $element = $array[$i];
    // Thực hiện tác vụ với $element
}

// Khong nen
for ($x = 0; $x < count($arr); $x++) {
    $y = $arr[$x];
    // Thực hiện tác vụ với $y
}
```

## 2. Tránh sử dụng các hàm có khả năng gây ra lỗi vượt quá bộ nhớ trong vòng lặp

```php
<?php

// Nen
$array = [1, 2, 3, 4, 5];
$count = count($array);
for ($i = 0; $i < $count; $i++) {
    // Thực hiện tác vụ với phần tử thứ $i của $array
}

// Khong nen
for ($i = 0; $i < count($array); $i++) {
    // Thực hiện tác vụ với phần tử thứ $i của $array
}
```

## 3. Sử dụng lệnh break hoặc continue để thoát khỏi vòng lặp khi điều kiện được đáp ứng

```php
<?php

// Nen
$array = [1, 2, 3, 4, 5];
foreach ($array as $value) {
    if ($value > 3) {
        break;
    }
    echo $value . "\n";
}

// Khong nen
foreach ($array as $value) {
    if ($value <= 3) {
        echo $value . "\n";
    }
}
```

## 4. Sử dụng vòng lặp do-while khi cần thực hiện một tác vụ ít nhất một lần

```php
<?php

// Nen
$i = 0;
do {
    echo $i . "\n";
    $i++;
} while ($i < 5);

// Khong nen
$i = 0;
while ($i < 5) {
    echo $i . "\n";
    $i++;
}
```

## 5. Sử dụng else là không cần thiết trong một số trường hợp

Sử dụng else là không cần thiết trong trường hợp sau:

```php
<?php
function test($a)
{
    if ($a) {
        return true;
    } else {
        return false;
    }
}

// vs.

function test($a)
{
    if ($a) {
        return true;
    }
    return false;    // else is not necessary
}

// or even shorter:

function test($a)
{
    return (bool) $a;
}
```

## 6. Return early

Để duy trì tính dễ đọc trong các hàm và phương thức, bạn nên return sớm nếu áp dụng các điều kiện đơn giản có thể được kiểm tra khi bắt đầu một phương thức:

```php
<?php
function foo($bar, $baz)
{
    if ($foo) {
        //assume
        //that
        //here
        //is
        //the
        //whole
        //logic
        //of
        //this
        //method
        return $value;
    } else {
        return null;
    }
}
```

It's better to return early.

```php
<?php
function foo($bar, $baz)
{
    if (!$foo) {
        return null;
    }

    //assume
    //that
    //here
    //is
    //the
    //whole
    //logic
    //of
    //this
    //method
    return $value;
}
```
