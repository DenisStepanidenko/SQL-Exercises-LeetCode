# Описание репозитория :book:
*Здесь будут собраны решения задач по SQL с сайта LeetCode* :books:  

# [*182. Duplicate Emails*](https://leetcode.com/problems/duplicate-emails/description/) :white_check_mark:
```sql
select email
from person
group by email
having count(person.email) > 1;
```

# [183. Customers Who Never Order](https://leetcode.com/problems/customers-who-never-order/description/) :white_check_mark:
```sql
select name Customers
from customers
where customers.id NOT IN(select orders.customerId from orders left join customers c on c.id = orders.customerId where orders.customerId IS NOT NULL group by orders.customerId);
```

# [181. Employees Earning More Than Their Managers](https://leetcode.com/problems/employees-earning-more-than-their-managers/description/) :white_check_mark:
```sql
select e1.name Employee
from employee e1
where salary > (select salary from employee e2 where e2.id = e1.managerId)
```

# [595. Big Countries](https://leetcode.com/problems/big-countries/description/) :white_check_mark:
```sql
select world.name,
        world.population,
        world.area
from world
where (area >= 3000000) OR (population >= 25000000)
```
# [1757. Recyclable and Low Fat Products](https://leetcode.com/problems/recyclable-and-low-fat-products/description/) :white_check_mark:
```sql
select products.product_id
from products
where low_fats = 'Y' AND recyclable = 'Y'
```

# [584. Find Customer Referee](https://leetcode.com/problems/find-customer-referee/description/) :white_check_mark:
```sql
select customer.name
from customer
where (referee_id NOT IN(2)) OR (referee_id IS NULL)
```

# []()







