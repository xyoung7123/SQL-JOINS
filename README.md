# SQL-JOINS
Joining Tables using SQL on BigQuery Sandbox
INNER JOIN on Google Cloud Database using SQL

--Finding out the Columns in the Order Table
SELECT
order_id, customer_id, warehouse_id, order_date
FROM
`my-1st-bigdata-project.order.or`

--Finding out the columns in the warehouse Table
SELECT
warehouse_id, maximum_cpacity, employee_total, state
FROM
`my-1st-bigdata-project.warehouse.wh`

--INNER JOIN 
SELECT 
`my-1st-bigdata-project.warehouse.wh`.employee_total,
`my-1st-bigdata-project.warehouse.wh`.maximum_capacity,
`my-1st-bigdata-project.warehouse.wh`.state,
`my-1st-bigdata-project.order.or`.order_date
FROM
`my-1st-bigdata-project.warehouse.wh`
INNER JOIN
`my-1st-bigdata-project.order.or`
ON
`my-1st-bigdata-project.warehouse.wh`.warehouse_id = `my-1st-bigdata-project.order.or`.warehouse_id

[orders dataset.csv](https://github.com/xyoung7123/SQL-JOINS/files/9077939/orders.dataset.csv)
[warehouse_orders.csv](https://github.com/xyoung7123/SQL-JOINS/files/9077940/warehouse_orders.csv)
