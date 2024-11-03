# Golu's Pizza

## Introduction

Did you know that over 115 million kilograms of pizza are consumed daily worldwide? (Well, at least that’s what Wikipedia says…)

Meet Golu, an aspiring entrepreneur who stumbled upon a game-changing idea while scrolling through his Instagram feed. He knew he had to jump on an opportunity to create a unique pizza experience.

Golu believed that pizza alone wouldn’t attract the investment he needed to grow his new pizza empire. So, he combined his passion for pizza with a modern twist – he decided to **Uberize** it! Thus, **Pizza Runner** was born!

Golu set out to recruit enthusiastic “runners” to deliver fresh pizzas right from his humble headquarters (a.k.a. Golu's house). He even maxed out his credit card to hire freelance developers to create a mobile app for seamless order processing.

Join us as we explore the fascinating world of Golu's Pizza through data analysis!

## Project Overview

This project analyzes various aspects of Golu's Pizza business using SQL. It aims to provide insights into customer behavior, order patterns, and menu preferences to enhance business strategies and improve customer experience.

## Database Schema Overview

### Table 1: `runners`
The `runners` table captures the registration details for each delivery runner, including their unique identifier and the date they registered.

### Table 2: `customer_orders`
The `customer_orders` table records each pizza ordered by customers. It includes details such as the customer ID, pizza type, exclusions, extras, and the order time.

### Table 3: `runner_orders`
The `runner_orders` table tracks the assignments of runners for each order, including details about pickup times, distances, durations, and any cancellations that occurred.

### Table 4: `pizza_names`
The `pizza_names` table lists the types of pizzas available at Pizza Runner, associating each pizza with a unique identifier and its name.

## Analysis Goals

### A. Pizza Metrics
1. How many pizzas were ordered?
2. How many unique customer orders were made?
3. How many successful orders were delivered by each runner?
4. How many of each type of pizza was delivered?
5. How many Vegetarian and Meat Lovers pizzas were ordered by each customer?
6. What was the maximum number of pizzas delivered in a single order?
7. For each customer, how many delivered pizzas had at least one change, and how many had no changes?
8. How many pizzas were delivered that had both exclusions and extras?
9. What was the total volume of pizzas ordered for each hour of the day?
10. What was the volume of orders for each day of the week?

### B. Runner and Customer Experience
1. How many runners signed up for each 1-week period? (i.e., week starts 2021-01-01)
2. What was the average time in minutes it took for each runner to arrive at the Pizza Runner HQ to pick up the order?
3. Is there any relationship between the number of pizzas and how long the order takes to prepare?
4. What was the average distance traveled for each customer?
5. What was the difference between the longest and shortest delivery times for all orders?
6. What was the average speed for each runner for each delivery, and do you notice any trends for these values?
7. What is the successful delivery percentage for each runner?

## Getting Started

To run this project, you will need a SQL environment set up with access to the datasets mentioned above. Clone this repository and import the datasets into your SQL database.

```bash
git clone https://github.com/birhman/golus-pizza.git
cd golus-pizza
```

## Contributing

If you would like to contribute to this project, please fork the repository and submit a pull request. Your contributions are welcome!
