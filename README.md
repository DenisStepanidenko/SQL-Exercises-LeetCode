# Описание репозитория :book:
*Здесь будут собраны решения задач по SQL с сайта LeetCode* :books:  

# [*182. Duplicate Emails*](https://leetcode.com/problems/duplicate-emails/description/) :white_check_mark:
```sql
select email
from person
group by email
having count(person.email) > 1;
```

# [*183. Customers Who Never Order*](https://leetcode.com/problems/customers-who-never-order/description/) :white_check_mark:
```sql
select name Customers
from customers
where customers.id NOT IN(select orders.customerId from orders left join customers c on c.id = orders.customerId where orders.customerId IS NOT NULL group by orders.customerId);
```

# [*181. Employees Earning More Than Their Managers*](https://leetcode.com/problems/employees-earning-more-than-their-managers/description/) :white_check_mark:
```sql
select e1.name Employee
from employee e1
where salary > (select salary from employee e2 where e2.id = e1.managerId)
```

# [*595. Big Countries*](https://leetcode.com/problems/big-countries/description/) :white_check_mark:
```sql
select world.name,
        world.population,
        world.area
from world
where (area >= 3000000) OR (population >= 25000000)
```
# [*1757. Recyclable and Low Fat Products*](https://leetcode.com/problems/recyclable-and-low-fat-products/description/) :white_check_mark:
```sql
select products.product_id
from products
where low_fats = 'Y' AND recyclable = 'Y'
```

# [*584. Find Customer Referee*](https://leetcode.com/problems/find-customer-referee/description/) :white_check_mark:
```sql
select customer.name
from customer
where (referee_id NOT IN(2)) OR (referee_id IS NULL)
```

# [*1148. Article Views I*](https://leetcode.com/problems/article-views-i/description/) :white_check_mark:
```sql
select distinct 
views.author_id id
from views
where views.author_id IN (select views.author_id from views where views.author_id = views.viewer_id)
order by views.author_id
```

# [*1683. Invalid Tweets*](https://leetcode.com/problems/invalid-tweets/description/) :white_check_mark:
```sql
select tweets.tweet_id
from tweets
where length(content) > 15
```

# [*1378. Replace Employee ID With The Unique Identifier*](https://leetcode.com/problems/replace-employee-id-with-the-unique-identifier/description/) :white_check_mark:
```sql
select unique_id,
       name
from employees
         left join EmployeeUNI c on employees.id = c.id;
```

# [*1068. Product Sales Analysis I*](https://leetcode.com/problems/product-sales-analysis-i/description/) :white_check_mark:
```sql
select product.product_name,
       year,
       price
from sales
left join product on product.product_id = sales.product_id
```

# [*1581. Customer Who Visited but Did Not Make Any Transactions*](https://leetcode.com/problems/customer-who-visited-but-did-not-make-any-transactions/description/) :white_check_mark:
```sql
select visits.customer_id , count(*) count_no_trans
from visits
left join transactions on transactions.visit_id = visits.visit_id
where transactions.transaction_id IS NULL
group by customer_id
```
# [*197. Rising Temperature*](https://leetcode.com/problems/rising-temperature/description/) :white_check_mark: 
```sql
select weather1.id
from weather weather1 
left join weather weather2 on weather2.recordDate = weather1.recordDate - Interval '1 days' 
where weather2.recordDate IS NOT NULL AND weather2.temperature < weather1.temperature
```

# [*1661. Average Time of Process per Machine*](https://leetcode.com/problems/average-time-of-process-per-machine/description/) :white_check_mark:
```sql
-- Write your PostgreSQL query statement below
select distinct 
        machine_id,
        round(   (select (select sum(difference) from (select activityStart.machine_id,
                            (activityEnd.timestamp - activityStart.timestamp)::numeric difference         
from activity activityStart
left join activity activityEnd on activityEnd.activity_type = 'end' AND activityStart.activity_type = 'start' AND (activityStart.process_id = activityEnd.process_id) AND (activityStart.machine_id = activityEnd.machine_id)
where activityEnd.timestamp IS NOT NULL AND activityStart.machine_id = activiyMain.machine_id) t) / (select count(distinct process_id) from activity)) ,3)processing_time
from activity activiyMain
```

# [*577. Employee Bonus*](https://leetcode.com/problems/employee-bonus/description/) :white_check_mark:
```sql
select employee.name,
       b.bonus
from employee
left join bonus b on b.empId = employee.empId
where (b.bonus < 1000 OR b.bonus IS NULL)
```

# [*1280. Students and Examinations*](https://leetcode.com/problems/students-and-examinations/description/) :white_check_mark:
```sql
select students.student_id,
       students.student_name,
       subjects.subject_name,
       (select count(*) from examinations e where e.student_id = students.student_id and e.subject_name = subjects.subject_name) attended_exams
from students cross join subjects
order by students.student_id, subjects.subject_name
```

# [*570. Managers with at Least 5 Direct Reports*](https://leetcode.com/problems/managers-with-at-least-5-direct-reports/description/) :white_check_mark:
```sql
select employee.name
from  employee
where employee.id IN (select managerId
from (select  count(*) coun,
        employee.managerId
from employee
where (employee.managerId IS NOT NULL)
group by employee.managerId)
where coun >= 5)
```

# [*1934. Confirmation Rate*](https://leetcode.com/problems/confirmation-rate/description/) :white_check_mark:
```sql
(select user_id,
       confirmation_rate
from (select s2.user_id,
       (select round(0::numeric , 2) from(select s1.user_id,
       count(action)
from signups s1
left join confirmations c1 on c1.user_id = s1.user_id
group by s1.user_id) where count = 0 AND s2.user_id = user_id) confirmation_rate
from signups s2)
where confirmation_rate IS NOT NULL)

union

(select c2.user_id,
       round((select count(action) from confirmations c3 where c2.user_id = c3.user_id AND c3.action = 'confirmed')::numeric / (select count(action) from confirmations c4 where c4.user_id = c2.user_id) ::numeric , 2) confirmation_rate
from confirmations c2
group by c2.user_id)
```







