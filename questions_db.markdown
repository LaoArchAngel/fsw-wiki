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

**2. What is the difference between a block and a deadlock?**

`Answer`

A block is when one or more tasks are waiting on another task to release its lock on a shared resource.

A deadlock is when two or more tasks are waiting on each other to release locks on multiple shared resources. For example, task A has a lock on shared resource 1, but needs access to shared resource 2 and task B has a lock on shared resource 2, but needs access to shared resource 1. They are both waiting on each other and thus will never complete their work.

### Med Questions

### Hard Questions

---

## In-person questions

### Easy Questions

### Med Questions

### Hard Questions
