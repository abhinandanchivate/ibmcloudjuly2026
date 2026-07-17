
## Change Database

```sql
\c smartmart_db
```

Connect using a specific user:

```sql
\c smartmart_db admin
```

Show current connection:

```sql
\conninfo
```

Show current database:

```sql
SELECT current_database();
```

## List Databases

```sql
\l
```

Or:

```sql
\list
```

## List Tables

```sql
\dt
```

List tables from all schemas:

```sql
\dt *.*
```

List tables in the `public` schema:

```sql
\dt public.*
```

## Describe Table

PostgreSQL does not use MySQL-style `DESCRIBE`. Use:

```sql
\d customers
```

Detailed table information:

```sql
\d+ customers
```

Other examples:

```sql
\d stores
\d employees
\d categories
\d products
\d orders
\d order_items
\d payments
```

## Show Table Columns

```sql
SELECT
    column_name,
    data_type,
    character_maximum_length,
    is_nullable,
    column_default
FROM information_schema.columns
WHERE table_name = 'customers'
ORDER BY ordinal_position;
```

## Show Primary Key Details

```sql
SELECT
    tc.table_name,
    kcu.column_name,
    tc.constraint_name
FROM information_schema.table_constraints AS tc
JOIN information_schema.key_column_usage AS kcu
    ON tc.constraint_name = kcu.constraint_name
    AND tc.table_schema = kcu.table_schema
WHERE tc.constraint_type = 'PRIMARY KEY'
  AND tc.table_name = 'customers';
```

For all tables:

```sql
SELECT
    tc.table_name,
    kcu.column_name,
    tc.constraint_name
FROM information_schema.table_constraints AS tc
JOIN information_schema.key_column_usage AS kcu
    ON tc.constraint_name = kcu.constraint_name
    AND tc.table_schema = kcu.table_schema
WHERE tc.constraint_type = 'PRIMARY KEY'
ORDER BY tc.table_name;
```

## Show Foreign Key Details

```sql
SELECT
    tc.constraint_name,
    tc.table_name,
    kcu.column_name,
    ccu.table_name AS referenced_table,
    ccu.column_name AS referenced_column
FROM information_schema.table_constraints AS tc
JOIN information_schema.key_column_usage AS kcu
    ON tc.constraint_name = kcu.constraint_name
    AND tc.table_schema = kcu.table_schema
JOIN information_schema.constraint_column_usage AS ccu
    ON ccu.constraint_name = tc.constraint_name
    AND ccu.table_schema = tc.table_schema
WHERE tc.constraint_type = 'FOREIGN KEY'
ORDER BY tc.table_name;
```

Foreign keys for one table:

```sql
SELECT
    tc.constraint_name,
    kcu.column_name,
    ccu.table_name AS referenced_table,
    ccu.column_name AS referenced_column
FROM information_schema.table_constraints AS tc
JOIN information_schema.key_column_usage AS kcu
    ON tc.constraint_name = kcu.constraint_name
JOIN information_schema.constraint_column_usage AS ccu
    ON tc.constraint_name = ccu.constraint_name
WHERE tc.constraint_type = 'FOREIGN KEY'
  AND tc.table_name = 'orders';
```

## Show All Constraints

```sql
SELECT
    table_name,
    constraint_name,
    constraint_type
FROM information_schema.table_constraints
WHERE table_schema = 'public'
ORDER BY table_name, constraint_type;
```

Constraints for one table:

```sql
SELECT
    constraint_name,
    constraint_type
FROM information_schema.table_constraints
WHERE table_name = 'employees';
```

## Show CHECK Constraints

```sql
SELECT
    conrelid::regclass AS table_name,
    conname AS constraint_name,
    pg_get_constraintdef(oid) AS constraint_definition
FROM pg_constraint
WHERE contype = 'c'
ORDER BY table_name;
```

For one table:

```sql
SELECT
    conname AS constraint_name,
    pg_get_constraintdef(oid) AS constraint_definition
FROM pg_constraint
WHERE conrelid = 'employees'::regclass
  AND contype = 'c';
```

## Show UNIQUE Constraints

```sql
SELECT
    table_name,
    constraint_name
FROM information_schema.table_constraints
WHERE constraint_type = 'UNIQUE'
  AND table_schema = 'public';
```

## Show Detailed Constraint Definitions

```sql
SELECT
    conrelid::regclass AS table_name,
    conname AS constraint_name,
    CASE contype
        WHEN 'p' THEN 'PRIMARY KEY'
        WHEN 'f' THEN 'FOREIGN KEY'
        WHEN 'u' THEN 'UNIQUE'
        WHEN 'c' THEN 'CHECK'
        WHEN 'x' THEN 'EXCLUSION'
    END AS constraint_type,
    pg_get_constraintdef(oid) AS definition
FROM pg_constraint
WHERE connamespace = 'public'::regnamespace
ORDER BY table_name, constraint_type;
```

## Show Indexes

```sql
\di
```

Indexes for one table:

```sql
SELECT
    indexname,
    indexdef
FROM pg_indexes
WHERE tablename = 'customers';
```

## List Schemas

```sql
\dn
```

Show current schema:

```sql
SELECT current_schema();
```

## List Views

```sql
\dv
```

## List Sequences

```sql
\ds
```

## List Functions

```sql
\df
```

## List Users and Roles

```sql
\du
```

## Show Table Records

```sql
SELECT * FROM customers;
```

Limit output:

```sql
SELECT * FROM customers
LIMIT 5;
```

## Expanded Display

Useful for wide records:

```sql
\x
```

Run a query:

```sql
SELECT * FROM customers LIMIT 1;
```

Disable expanded display:

```sql
\x
```

## Show Command History

```sql
\s
```

## Execute SQL File

```sql
\i /path/to/file.sql
```

Example:

```sql
\i /tmp/smartmart.sql
```

## Clear Screen

```sql
\! clear
```

For Windows:

```sql
\! cls
```

## Exit PostgreSQL

```sql
\q
```
