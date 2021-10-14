# Vertica Cheatsheet

## List schemas

``` SQL
SELECT schema_id, 
       schema_name,
       u.user_name AS owner,
       create_time,
       is_system_schema
FROM v_catalog.schemata s
JOIN v_catalog.users u
     ON s.schema_owner_id = u.user_id
ORDER BY schema_name;
```

## Get projections

``` SQL
GET_PROJECTIONS ( '[[database.]schema-name.]table' )
```
