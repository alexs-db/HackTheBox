# SQL Operators

Sometimes, expressions with a single condition are not enough to satisfy user requirements. SQL supports **Logical Operators** to use multiple conditions at once. The most common are AND, OR, and NOT.

## AND Operator

The AND operator takes two conditions and returns true only if both evaluate to true.

```sql
condition1 AND condition2
```

**Example:**
```sql
mysql> SELECT 1 = 1 AND 'test' = 'test';
```
Result: `1` (true - both conditions are true)

```sql
mysql> SELECT 1 = 1 AND 'test' = 'abc';
```
Result: `0` (false - second condition is false)

In MySQL, any non-zero value is true (returns 1), and 0 is false.

## OR Operator

The OR operator returns true when at least one condition evaluates to true.

```sql
mysql> SELECT 1 = 1 OR 'test' = 'abc';
```
Result: `1` (true - first condition is true)

```sql
mysql> SELECT 1 = 2 OR 'test' = 'abc';
```
Result: `0` (false - both conditions are false)

## NOT Operator

The NOT operator toggles a boolean value (true → false, false → true).

```sql
mysql> SELECT NOT 1 = 1;
```
Result: `0` (inverse of true)

```sql
mysql> SELECT NOT 1 = 2;
```
Result: `1` (inverse of false)

## Symbol Operators

AND, OR, and NOT can also be represented as `&&`, `||`, and `!` respectively.

```sql
mysql> SELECT 1 = 1 && 'test' = 'abc';  -- Result: 0
mysql> SELECT 1 = 1 || 'test' = 'abc';  -- Result: 1
mysql> SELECT 1 != 1;                    -- Result: 0
```

## Operators in Queries

**Example 1:** Select records where username is NOT 'john':
```sql
mysql> SELECT * FROM logins WHERE username != 'john';
```

**Example 2:** Select users with id > 1 AND username != 'john':
```sql
mysql> SELECT * FROM logins WHERE username != 'john' AND id > 1;
```

## Operator Precedence

SQL evaluates operations in this order (highest to lowest):

1. Division (`/`), Multiplication (`*`), Modulus (`%`)
2. Addition (`+`), Subtraction (`-`)
3. Comparison (`=`, `>`, `<`, `<=`, `>=`, `!=`, `LIKE`)
4. NOT (`!`)
5. AND (`&&`)
6. OR (`||`)

**Example:**
```sql
SELECT * FROM logins WHERE username != 'tom' AND id > 3 - 2;
```

Evaluation order:
1. `3 - 2` → `1`
2. `username != 'tom'` and `id > 1`
3. Apply AND to combine conditions
