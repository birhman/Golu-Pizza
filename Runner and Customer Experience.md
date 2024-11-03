## 1.How many runners signed up for each 1 week period? (i.e. week starts 2021-01-01)

```sql
select week(registration_date, 0) as registered_week,
count(*) as total_registrations
from runners
where registration_date >= "2021-01-01"
group by registered_week;
```

## 2.What was the average time in minutes it took for each runner to arrive at the Pizza Runner HQ to pickup the order?

```sql
select 
    ro.runner_id, 
    round(avg(timestampdiff(minute, co.order_time, ro.pickup_time)), 2) as average_time
from customer_orders co
join runner_orders ro ON co.order_id = ro.order_id
group by ro.runner_id;
```

## 3.Is there any relationship between the number of pizzas and how long the order takes to prepare?

```sql
select co.order_id,count(co.pizza_id) no_of_orders, ROUND(AVG(TIMESTAMPDIFF(MINUTE, co.order_time, ro.pickup_time)), 2) AS average_time
from customer_orders co
join runner_orders ro on co.order_id = ro.order_id
where ro.cancellation is null
group by co.order_id
order by no_of_orders desc;
```
### Yes, there is a relationship between the number of pizzas ordered and the preparation time. Orders with more pizzas generally take longer to prepare, as seen with order 4 (3 pizzas, 29 minutes). However, single pizza orders consistently take around 10-15 minutes, suggesting efficiency at lower quantities.

## 4.What was the average distance travelled for each customer?

```sql
select customer_id, round(avg(distance), 2) as average_distance
from customer_orders co
join runner_orders ro on co.order_id = ro.order_id
group by customer_id;
```

## 5.What was the difference between the longest and shortest delivery times for all orders?

```sql
select 
    max(cast(substring(duration, 1, 2) as unsigned)) - 
    min(cast(substring(duration, 1, 2) as unsigned)) as duration_difference
from 
    runner_orders;
```

## 6.What was the average speed for each runner for each delivery and do you notice any trend for these values?

```sql
with timing as (
    select runner_id, order_id,
        cast(substring(duration, 1, 2) as unsigned) AS duration_minutes,
		distance
    from runner_orders
    where duration is not null and distance is not null
)
select 
    order_id, runner_id, 
    round(avg(distance / (duration_minutes/60)), 2) as "average_speed(Km/hr)"
from timing
group by order_id, runner_id
order by runner_id;
```
### The average speed for each runner varies significantly across deliveries, with some runners achieving speeds above 60 km/h. This suggests that factors like distance and delivery conditions affect speed. Analyzing the trends reveals potential areas for optimization in delivery routes and times to enhance overall efficiency.

## 7.What is the successful delivery percentage for each runner?

```sql
select 
    runner_id,
    (COUNT(case when cancellation is null then order_id end) / COUNT(order_id)) * 100 as successful_orders_percentage
from runner_orders
group by runner_id;
```
