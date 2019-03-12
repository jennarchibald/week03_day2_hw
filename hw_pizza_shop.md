# Homework: Pizza Shop

## Today

Today we created a program that tracks pizza orders. We created a Ruby class (`PizzaOrder`) and a database table (pizza\_orders) which is able to persist objects of this type. Currently, our database table is structured as follows...

| first_name | last_name | topping         | quantity |
|------------|-----------|-----------------|----------|
| Luke       | Skywalker | Pepperoni       | 2        |
| Leia       | Organa    | Ham & Pineapple | 1        |

Our table stores a combination of pizza and customer details. This isn't ideal for a number of reasons. If a single customer makes many orders then their details appear in our database many times. Firstly, this is not efficient. It would be much nicer if we could create a customer once and then attribute many orders too them. This would also help to protect us against typos as we would only have to submit a new customer once.

## Tomorrow

Tomorrow we are going to refactor our program. We will add another class, `Customer`, which will also have the full set of CRUD actions. This class will be responsible for the customer details, while `PizzaOrders` will be responsible for the pizza order that is being processed.

We will also extract some of the database connection code into a new class, `SqlRunner`.

Once completed, our tables should be structured as follows...

### customers

| id | first_name | last_name |
|----|------------|-----------|
| 1  | Luke       | Skywalker |
| 2  | Leia       | Organa    |

### pizza_orders

| id | topping         | quantity | customer_id |
|----|-----------------|----------|-------------|
| 1  | Pepperoni       | 2        | 1           |
| 2  | Ham & Pineapple | 1        | 2           |
| 3  | Meat Feast      | 1        | 1           |

## Task

Your task this evening is to read over the completed end\_code for tomorrow's lesson, understand it as much as possible, and answer the following questions.

1) What is the relationship between customers and pizza\_orders?

one to many - one customer to many pizza orders.

2) At what point is the id of a `PizzaOrder` created?

when a pizza order is saved into the pizza_orders database it gains an id

3) At what point do we assign a value to the `@id` instance variables of our objects?

@id is assigned in the save function when the database returns the id assigned.

4) Name 2 things that the `Customer`'s `@id` property is used for.

-refencing a unique customer (in case other variables are co-incidentally the same for 2 or more customers)
-setting up a relationship between a customer and their orders by assigning a customer_id to a PizzaOrder object when it is created.


5) Why might it be important to check if `options['id']` is `nil` in our `initialize` method before assigning `@id` the value of `options[‘id’].to_i?`

<!-- nil.to_i is 0 -->

if options['id'] is nil then options['id'].to_i is 0 so the id would be set to 0. if we created multiple instances at one time then they would share id's, which should be unique.

6) What are the responsibilities of `SqlRunner`?

SqlRunner connects to the database, prepares queries using sql given, and executes them using values given before closing the database connection

7) How does `SqlRunner` improve the quality of our code?

SqlRunner prevents us from repeating the same steps every time we with to interact with the database.
