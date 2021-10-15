# Vertica Cheatsheet

## Create schema and table

``` SQL
CREATE schema my_schema;

CREATE TABLE my_schema.performance_metrics (
        date DATE,
        channel VARCHAR,
        country VARCHAR,
        os VARCHAR,
        impressions INTEGER,
        clicks INTEGER,
        installs INTEGER,
        spend NUMERIC(12, 2),
        revenue NUMERIC(12, 2)
);
```

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

## Table used size

``` SQL
SELECT anchor_table_schema, anchor_table_name,
ROUND( SUM(used_bytes) / (1024^3), 2 ) AS used_gb
FROM v_monitor.projection_storage
GROUP BY anchor_table_schema, anchor_table_name
ORDER BY SUM (used_bytes) DESC;
```
