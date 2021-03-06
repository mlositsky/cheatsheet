# Vertica Cheatsheet

## Create schema and table

``` SQL
CREATE SCHEMA my_schema;

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
        CONSTRAINT pk PRIMARY KEY (date, channel, country, os) ENABLED
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

## Import(copy) csv data

``` SQL
COPY table_name FROM '/path/to/data.csv' PARSER fcsvparser();
```

## Get projections

``` SQL
SELECT GET_PROJECTIONS ( '[[database.]schema-name.]table' )
```

## Table used size

``` SQL
SELECT anchor_table_schema, anchor_table_name,
ROUND( SUM(used_bytes) / (1024^1), 2 ) AS used_kb
FROM v_monitor.projection_storage
GROUP BY anchor_table_schema, anchor_table_name
ORDER BY SUM (used_bytes) DESC;
```
