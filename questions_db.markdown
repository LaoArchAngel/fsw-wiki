# Database Design/Programming Interview Questions

Questions related to database design, SQL queries, stored procedures, indexes, and other database objects.

---

## Phone Screen Questions

### Easy Questions

**1. What is the difference between an inner join and outer join?  What is an example of each?**

`Answer`
An **inner join** between two tables will only return a result record if there is a matching value in both the two tables on the column being joined.
An **outer join** between two tables will return a result record for every source record in the "outer" side of the join.  

`Examples`
1. Inner join: If you want to see all orders that have at least one line item, do an inner join between orders and line items
2. Outer join: If you want to see all orders, whether they have a line item or not, do a (left) outer join from orders to line items
3. Outer join: If you want to see all security groups, whether there are any users in the group or not, use an outer join from security group to user

`Tips`
1. Bonus points if interviewee asks to specify what type of outer join - e.g. left, right, or full outer join

### Med Questions

### Hard Questions
---

## In-person questions

### Easy Questions

### Med Questions

### Hard Questions

---

## Whiteboard questions

### Easy Questions

### Med Questions

### Hard Questions
