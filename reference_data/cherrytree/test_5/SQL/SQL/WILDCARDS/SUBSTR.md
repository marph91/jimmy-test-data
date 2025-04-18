
### **SUBSTR in Oracle SQL**
Used to retrieve a part of a string based on positions (similar to Python slicing).


-- Extracts value starting from the 3rd position from the left
SELECT SUBSTR(NAME, 3. FROM TABLENAME;


#### Example:
If `NAME = 'Cybersecurity'`, result = `'bersecurity'`


-- Extracts the last 3 characters (starting from the 3rd from the right)
SELECT SUBSTR(NAME, -3. FROM TABLENAME;


#### Example:
If `NAME = 'Cybersecurity'`, result = `'ity'`


-- Extracts 4 characters starting from the 2nd position
SELECT SUBSTR(NAME, 2, 4. FROM TABLENAME;


#### Example:
If `NAME = 'OracleSQL'`, result = `'racl'`
