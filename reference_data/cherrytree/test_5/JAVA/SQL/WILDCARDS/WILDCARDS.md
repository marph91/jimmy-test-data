


select * from tablename where name like   ‘a%’;

SELECT  *  FROM  TABLENAME  WHERE  NAME  LIKE ‘_ONDON’;

SELECT * FROM TABLENAME WHERE NAME LIKE  ‘[ABC] %’;          =>  It retrives the values from the table which starts from a,b or c letter.

SELECT * FROM TABLENAME WHERE NAME LIKE ‘[A-F]%’;          =>  It retrives the values from the table which starts from letters between A and F .

SELECT * FROM  TABLENAME WHERE NAME LIKE ‘{*&%^%}’              
| _ | Represents a single character |
| --- | --- |
| [] | Represents any single character within the brackets  |
| ^ | Represents any character not in the brackets  |
| - | Represents any single character within the specified range  |
| {} | Represents any escaped character  |
| % | Represents zero or more characters |
