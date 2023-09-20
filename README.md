# CodeCraft SQL Mystery!

Hello and welcome to the event, the format will consist of splitting into groups of 4-5 and figuring out a whodunnit.
It is recommended that you firstly agree how you will run the session between yoursleves.
You can either have one person driving and sharing their screen, or you can take turns every couple of minutes. It is up to you!

Here is a link to the [schema diagram](https://mystery.knightlab.com/schema.png) for the mystery
Here is the link to the [page](https://mystery.knightlab.com/#experienced). 




Exercise:   
A crime has taken place and the detective needs your help. The detective gave you the crime scene report, but you somehow lost it. You vaguely remember that the crime was a ​murder​ that occurred sometime on ​Jan.15, 2018​ and that it took place in ​SQL City​. Start by retrieving the corresponding crime scene report from the police department’s database.

Here are some hints. There are many ways in which you can extract this data, this is just a handy guide to help you along the way 

If you need a cheat sheet of SQL syntax, you can expans rhe tag below
<details>
<summary><b>SQL cheat sheet</b></summary>

| Query Description                              | SQL Query                                                                  |
|------------------------------------------------|----------------------------------------------------------------------------|
| Retrieve all columns from a table              | `SELECT * FROM table_name;`                                                |
| Retrieve specific columns from a table         | `SELECT column1, column2 FROM table_name;`                                 |
| Retrieve distinct values from a column         | `SELECT DISTINCT column_name FROM table_name;`                             |
| Filter rows based on a condition               | `SELECT * FROM table_name WHERE condition;`                                |
| Provide alternative filter                     | `SELECT * FROM table_name WHERE condition OR condition`                    |
| Sort results in ascending order                | `SELECT * FROM table_name ORDER BY column_name ASC;`                       |
| Sort results in descending order               | `SELECT * FROM table_name ORDER BY column_name DESC;`                      |
| Inner Join between two tables                  | `SELECT * FROM table1 JOIN table2 ON table1.column = table2.column;`       |
| Left Join (Retrieve all from the left table)   | `SELECT * FROM table1 LEFT JOIN table2 ON table1.column = table2.column;`  |
| Right Join (Retrieve all from the right table) | `SELECT * FROM table1 RIGHT JOIN table2 ON table1.column = table2.column;` |


</details>



<details>
<summary><b>Step 1  - Getting the crime scene description</b></summary>


You will need to run a query on the crime_scene_report table using a ```SELECT``` and ```WHERE``` to find your description

<details>
<summary>Formatting the date</summary>

Formatted date is ```20180115```
</details>

<details>
<summary> Filtering by multiple filters</summary>

You will need to use a ```WHERE BY and AND``` selectors to get filter
</details>

<details>
<summary>Solution</summary>

```
SELECT * 
FROM crime_scene_report 
WHERE type = 'murder'
    AND city = 'SQL City' 
    AND date = 20180115
```
</details>
</details>

<details>
<summary><b>Step 2 - Finding Witneses</b></summary>
So we know that:

- The first witness lives at the last house on “Northwestern Dr”. 
- The second witness, named Annabel, lives somewhere on “Franklin Ave”.

You can run this in one query, but we will run it as 2 separate ones

<details>
<summary><b>Run a join on 2 tables: person and interview</b></summary>

The ways joins work is they match data on the columns which share a vaulue. In this case, we are matching the column 'id' in 'person' table with the column of 'person_id' in the interview table. 

`SELECT *
FROM interview i
JOIN person p 
    ON p.id = person_id`
</details>

<details>
<summary><b>Use the LIKE operator to search for a pattern in a column</b></summary>

``LIKE'%Annabel%' ``
</details>
<details>
<summary><b>First query (SOLUTION)</b></summary>

```
SELECT * 
FROM interview i 
JOIN person p ON p.id = person_id 
WHERE name LIKE'%Annabel%' 
    AND address_street_name = 'Franklin Ave'

```
</details>

<details>
<summary><b>Use an OR operator</b></summary>

Add `Northwestern Dr` using an OR keyword to your query
</details>

<details>
<summary><b>Solution</b></summary>

```
SELECT *
FROM interview i
JOIN person p ON p.id = person_id
WHERE (name LIKE '%Annabel%' AND address_street_name = 'Franklin Ave')
   OR (address_street_name = 'Northwestern Dr')
```
</details>

You now have a little reading to do, so look for the clues relating to the murder. 
</details>

<details>
<summary><b>Step 3 - We are off to exercise!</b></summary>

<details>
<summary><b>You will need a join </b></summary>

Run a join between between get_fit_now_member and get_fit_now_check_in
</details>

<details>
<summary><b>Use previously used operators</b></summary>

Use `WHERE, LIKE and AND` to filter your data
</details>

<details>
<summary><b>Solution</b></summary>

```
SELECT *
FROM get_fit_now_member m
JOIN get_fit_now_check_in c ON m.id = membership_id
WHERE check_in_date = '20180109'
  AND membership_status = 'gold'
  AND membership_id LIKE '48Z%'
```
</details>
</details>


<details>
<summary><b>Step 4 - The license....to kill?</b></summary>

Ok last query you can do this!!

<details>
<summary><b>We love the joins! </b></summary>

You will need to run a join on person and drivers_license
</details>

<details>
<summary><b>Use IN operator </b></summary>

Use an IN to look for person's ID thats either `28819` or `67318`.
</details>

<details>
<summary><b>Solution</b></summary>

```
SELECT *
FROM drivers_license d
JOIN person p ON p.license_id = d.id
WHERE p.id IN ('28819', '67318')
```
</details>


</details>


***


Complete the extra challenge if you have time - you should have all the tools now from your earlier work!

<details>
<summary><b>Step 1 - Finding the interview by person (SOLUTION ONLY) </b></summary>

```SQL
SELECT * 
FROM interview 
WHERE person_id = 67318
```

</details>

<details>
<summary><b>Step 2 - Look for the car (SOLUTION ONLY)</b></summary>

```SQL
SELECT id 
FROM drivers_license 
WHERE car_model = 'Model S' 
AND gender = 'female'
```
</details>

<details>
<summary><b>Step 3 - The event (SOLUTION ONLY)</b></summary>

```SQL
SELECT * 
FROM person 
WHERE license_id IN ('202298', '291182', '918773')
```
</details>
