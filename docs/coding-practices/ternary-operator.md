---
sidebar_position: 2
---

# Ternary Operator

## Tại sao nên sử dụng if-else, switch-case thay vì toán tử 3 ngôi?

Cả if-else và toán tử ba ngôi đều có thể được sử dụng để thực hiện các phép so sánh và điều khiển luồng chương trình trong lập trình. Tuy nhiên, trong một số trường hợp, if-else có thể làm cho code của bạn trở nên dễ đọc hơn so với toán tử ba ngôi.

Dưới đây là một số lý do tại sao bạn nên sử dụng if-else thay vì toán tử ba ngôi:

- Độ dài và độ phức tạp của điều kiện: Nếu điều kiện của bạn khá dài hoặc phức tạp, việc sử dụng toán tử ba ngôi có thể làm cho code của bạn trở nên khó đọc và khó hiểu. Sử dụng if-else có thể giúp cho code của bạn trở nên dễ đọc và dễ hiểu hơn.

- Tính tổng quát: Nếu bạn muốn thực hiện nhiều hơn một hành động trong trường hợp điều kiện của bạn được đáp ứng, việc sử dụng if-else có thể dễ dàng hơn. Sử dụng toán tử ba ngôi trong trường hợp này có thể làm cho code của bạn trở nên khó đọc và khó hiểu.

- Khả năng mở rộng: Nếu bạn muốn mở rộng code của mình trong tương lai bằng cách thêm nhiều điều kiện hơn, việc sử dụng if-else có thể giúp cho việc thêm các điều kiện mới trở nên dễ dàng hơn.

```php
<?php

// Bad
function numberToWord($num) {
    return ($num == 1) ? "one" 
    : (($num == 2) ? "two" 
    : (($num == 3) ? "three" 
    : (($num == 4) ? "four" 
    : (($num == 5) ? "five" 
    : "Error: Invalid number"))));
}

// Good
function numberToWord($num) {
    if ($num == 1) {
        return "one";
    } else if ($num == 2) {
        return "two";
    } else if ($num == 3) {
        return "three";
    } else if ($num == 4) {
        return "four";
    } else if ($num == 5) {
        return "five";
    } else {
        return "Error: Invalid number";
    }
}

// Very Good
function numberToWord($num) {
    switch($num) {
        case 1:
            return "one";
            break;
        case 2:
            return "two";
            break;
        case 3:
            return "three";
            break;
        case 4:
            return "four";
            break;
        case 5:
            return "five";
            break;
        default:
            return "Error: Invalid number";
    }
}


```

Về cơ bản, cả hai cách đều đúng và giải quyết được bài toán. Tuy nhiên, sử dụng if-else sẽ giúp cho code dễ hiểu hơn, trong khi sử dụng toán tử 3 ngôi có thể làm cho code ngắn hơn và gọn hơn. Tuy nhiên, việc sử dụng toán tử 3 ngôi cũng nên được sử dụng một cách cẩn thận để tránh làm cho code trở nên khó hiểu.
