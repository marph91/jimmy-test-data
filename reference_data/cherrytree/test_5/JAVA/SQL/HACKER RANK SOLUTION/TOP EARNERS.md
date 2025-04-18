SELECT MAX(salary * months),Count(*) FROM Employee WHERE salary*months = (SELECT MAX(salary*months ) from Employee);


Sub query