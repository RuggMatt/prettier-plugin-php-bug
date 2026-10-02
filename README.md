# Minimum Repro

The PHP Prettier plugin removes required parentheses from a nested ternary
expression when a full ternary is followed by a shorthand ternary (`?:`, also
known as the Elvis operator). This changes valid PHP into an expression that
PHP rejects.

## Expected

The following should remain as is.

```php

echo (1 ? "1" : 2) ?: 3;
```

## Actual

The formatter removes the parenthesis, causing a runtime error

```php

echo 1 ? "1" : 2 ?: 3;

```

When running the above code, the following error occurs:

```
PHP Fatal error:  Unparenthesized `a ? b : c ?: d` is not supported. Use either `(a ? b : c) ?: d` or `a ? b : (c ?: d)` in <path> on line 3
```