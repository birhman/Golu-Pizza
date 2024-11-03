### 1.How many pizzas were ordered?

```sql
select count(order_id) as total_orders from customer_orders;
```

### 2.How many unique customer orders were made?

```sql
select count(distinct customer_id) as unique_customer_orders from customer_orders;
```

### 3.How many successful orders were delivered by each runner?

```sql
select runner_id, count(*) as orders_by_runner from runner_orders where cancellation is null group by runner_id;
```

### 4.How many of each type of pizza was delivered?

```sql
select pizza_id, count(*) as pizza_ordered 
from customer_orders c
join runner_orders r on c.order_id = r.order_id
where r.cancellation is null
group by c.pizza_id;
```

### 5.How many Vegetarian and Meatlovers were ordered by each customer?

```sql
select customer_id, pizza_name, count(*) as total_orders 
from customer_orders c
join pizza_names p on c.pizza_id = p.pizza_id
group by customer_id, p.pizza_name
ORDER BY customer_id, pizza_name;
```
### 6.What was the maximum number of pizzas delivered in a single order?

```sql
select 
    co.order_id, 
    count(*) as pizzas_delivered
from customer_orders co
join runner_orders ro ON co.order_id = ro.order_id
where ro.cancellation IS NULL
group by co.order_id
order by pizzas_delivered DESC
limit 1;
```
### 7.For each customer, how many delivered pizzas had at least 1 change and how many had no changes?

```sql
select customer_id, 
	sum(case when exclusions is not null or extras is not null then 1 else 0 end) as pizza_changed,
    sum(case when exclusions is null and extras is null then 1 else 0 end) as pizza_not_changed
from customer_orders co
join runner_orders ro on co.order_id = ro.order_id
where cancellation is null
group by customer_id;
```
### 8.How many pizzas were delivered that had both exclusions and extras?

```sql
select 
	sum(case when exclusions is not null and extras is not null then 1 else 0 end) as total_changed_pizzas
from customer_orders co
join runner_orders ro on co.order_id = ro.order_id
where ro.cancellation is null;
```

### 9.What was the total volume of pizzas ordered for each hour of the day?

```sql
select 
    hour(order_time) as order_hour,
    count(*) as total_pizzas_ordered
from customer_orders
group by order_hour
order by total_pizzas_ordered desc;
```    
### 10.What was the volume of orders for each day of the week?

```sql
select 
    dayname(order_time) as day_of_week,
    count(*) as pizzas_ordered
from customer_orders
group by day_of_week
order by field(day_of_week, 'Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday');
```
