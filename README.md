# Описание репозитория :book:
*Здесь будут собраны решения задач по SQL с сайта LeetCode* :books:  

# [*182. Duplicate Emails*](https://leetcode.com/problems/duplicate-emails/description/) :white_check_mark:
```sql
select email
from person
group by email
having count(person.email) > 1;
```
