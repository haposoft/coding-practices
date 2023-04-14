---
sidebar_position: 2
---

# Control Structure

## 1. Switch case và match

Switch case sử dụng loose comparison. Để khắc phục điều này, từ bản PHP8.0, chúng ta có thể sử dụng match.

```php
function runA(): void {
    echo 'runA is running' . PHP_EOL;
}
function runDefault(): void {
    echo 'runDefault is running' . PHP_EOL;
}

$type = true;

// Bad
switch ($type) {
    case 2:
        runA();
        break;
    default:
        runDefault();
}
// Output: runA is running

// Good
match ($type) {
    2 => runA(),
    default => runDefault(),
};
// Output: runDefault is running
```
