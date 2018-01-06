# createTable Operator
Specifies the `CREATE TABLE` Statement.

#### Supported by
- [MySQL](https://dev.mysql.com/doc/refman/5.7/en/create-table.html)
- [MariaDB](https://mariadb.com/kb/en/library/create-table/)
- [PostgreSQL](https://www.postgresql.org/docs/9.5/static/sql-createtable.html)
- [SQLite](https://sqlite.org/lang_createtable.html)
- [Oracle](https://docs.oracle.com/cd/B19306_01/server.102/b14200/statements_7002.htm)
- [SQLServer](https://docs.microsoft.com/en-us/sql/t-sql/statements/create-table-transact-sql)

# Allowed Types and Usage

## as Object:

Usage of `createTable` as **Object** with the following Syntax:

**Syntax:**

```javascript
$createTable: { ... }
```

**SQL-Definition:**
```javascript
CREATE
  { OR REPLACE[$orReplace]}-->(MariaDB)
  { TEMPORARY[$temp]}
  { UNLOGGED[$unlogged]}-->(PostgreSQL) TABLE { IF NOT EXISTS [$ine] | [$ifNotExists] } <$table>
  { ([$define])}
  { WITH [$with]}-->(PostgreSQL,SQLServer)
  { TABLESPACE [$tablespace]}
```

**Registered Helpers**

Name|Required|Public|SQL-Definition|Supported by
:---|:------:|:----:|:-------------|:-----------
[orReplace](./private/orReplace/)|*optional*|*private*| OR REPLACE [$orReplace]|`MariaDB` 
[temp](./private/temp/)|*optional*|*private*| TEMPORARY [$temp]|
[unlogged](./private/unlogged/)|*optional*|*private*| UNLOGGED [$unlogged]|`PostgreSQL` 
[ine](./private/ine/)|*optional*|*private*| IF NOT EXISTS  [$ine] |
[ifNotExists](./private/ifNotExists/)|*optional*|*private*| IF NOT EXISTS  [$ifNotExists] |
[table](./private/table/)|:heavy_check_mark:|*private*||
[define](./private/define/)|*optional*|*private*| ( [$define])|
[with](../../operators/with/)|*optional*|:heavy_check_mark:| WITH  [$with]|`PostgreSQL` `SQLServer` 
[tablespace](./private/tablespace/)|*optional*|*private*| TABLESPACE  [$tablespace]|

:bulb: **Example:**
```javascript
function() {
    return sql.$createTable({
        $temp: true,
        $table: 'my_temp_people_table',
        $define: {
            people_id: { $column: { $type: 'INT', $default: 0 } },
            first_name: { $column: { $type: 'VARCHAR', $size: 50, $notNull: true } },
            last_name: { $column: { $type: 'VARCHAR', $size: 50, $notNull: true } },
            bio: { $column: { $type: 'TEXT' } }
        }
    });
}

// SQL output
CREATE TEMPORARY TABLE my_temp_people_table (
    people_id INT DEFAULT 0,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    bio TEXT
)

// Values
{}
```
