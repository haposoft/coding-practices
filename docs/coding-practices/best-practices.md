---
sidebar_position: 3
---

## if, elseif, else
- Bạn hãy chú ý đến các dấu ngoặc đơn, khoảng trắng và dấu ngoặc nhọn; các từ khóa như else và elseif phải được đặt dùng dòng với dấu ngoặc nhọn đóng của phần thân cấu trúc điều khiển phía trước và nên sử dụng elseif hơn là else if..
````php
//bad
<?php
 
if ($expr1) 
{
    // if body
} 
elseif ($expr2) 
{
    // elseif body
} 
else 
{
    // else body;
}

//good
<?php
 
if ($expr1) {
    // if body
} elseif ($expr2) {
    // elseif body
} else {
    // else body;
}
````
- Biểu thức ở giữa cặp dấu ngoặc đơn có thể được viết trên nhiều dòng, với mỗi dòng sẽ được thù lề thêm một cấp. Điều kiện đầu tiên sẽ phải được viết trên dòng tiếp theo. Dấu ngoặc đơn đóng và dấu ngoặc nhọn mở phải được viết trên cùng một dòng và ngăn cách bằng một khoảng trắng.
````php
//bad
<?php
 
if ( $expr1 && $expr2 ) {
    // if body
} elseif ( $expr3 && $expr4 ) {
    // elseif body
}
//good 
<?php
 
if (
    $expr1
    && $expr2
) {
    // if body
} elseif (
    $expr3
    && $expr4
) {
    // elseif body
}
````

## switch, case
- Bạn hãy để ý tới vị trí của các dấu ngoặc đơn, khoảng trắng và dấu ngoặc nhọn. Từ khóa case phải được thụt lề thêm một cấp so với từ khóa switch, và từ khóa break (hoặc từ khóa kết thúc như return) phải được thụt lề thêm một cấp so với case.
````php
//bad
<?php
 
switch ($expr) {
    case 0:
        echo 'First case, with a break';
    break;
    case 1:
        echo 'Second case, which falls through';
    case 2:
    case 3:
    case 4:
        echo 'Third case, return instead of break';
    return;
    default:
        echo 'Default case';
    break;
}

//good
<?php
 
switch ($expr) {
    case 0:
        echo 'First case, with a break';
        break;
    case 1:
        echo 'Second case, which falls through';
        // no break
    case 2:
    case 3:
    case 4:
        echo 'Third case, return instead of break';
        return;
    default:
        echo 'Default case';
        break;
}
````