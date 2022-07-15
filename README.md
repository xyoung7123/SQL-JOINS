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

-- JOIN Statement with Subqueries
SELECT `my-1st-bigdata-project.warehouse.wh`.warehouse_id,
CONCAT(`my-1st-bigdata-project.warehouse.wh`.state, ':' , `my-1st-bigdata-project.warehouse.wh`.warehouse_alias ) 
AS warehouse_name,
COUNT(`my-1st-bigdata-project.order.or`.order_id) AS no_of_orders,
(
  SELECT
COUNT(*)
FROM `my-1st-bigdata-project.order.or`) AS Total_orders,
 CASE 
 WHEN COUNT(`my-1st-bigdata-project.order.or`.order_id)/(SELECT COUNT(*) 
 FROM `my-1st-bigdata-project.order.or`) <=0.20
 THEN "fulfilled 0-20% of Orders"
WHEN COUNT(`my-1st-bigdata-project.order.or`.order_id)/(SELECT COUNT(*) 
FROM `my-1st-bigdata-project.order.or`) > 0.20
AND COUNT(`my-1st-bigdata-project.order.or`.order_id)/(SELECT COUNT(*) 
FROM `my-1st-bigdata-project.order.or`) <=0.60
THEN "fulfilled 21-60% of Orders"
ELSE "fulfilled more than 60% of Orders"
END AS Fulfillment_summary
FROM
`my-1st-bigdata-project.warehouse.wh`
LEFT JOIN 
`my-1st-bigdata-project.order.or`
ON `my-1st-bigdata-project.warehouse.wh`.warehouse_id = `my-1st-bigdata-project.order.or`.warehouse_id
GROUP BY `my-1st-bigdata-project.warehouse.wh`.warehouse_id, warehouse_name
HAVING COUNT(`my-1st-bigdata-project.order.or`.order_id) > 0


[orders dataset.csv](https://github.com/xyoung7123/SQL-JOINS/files/9077939/orders.dataset.csv)
[warehouse_orders.csv](https://github.com/xyoung7123/SQL-JOINS/files/9077940/warehouse_orders.csv)
