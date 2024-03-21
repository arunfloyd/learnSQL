
  ===> Open the postSQL using TERIMINAL  in Ubuntu
           
           -> sudo -i -u postgres 
  ===> then get inside the Postgres 
           
           -> psql
  ==> QUit from it 
   
           ->  \q
  ==> To create a database 

           -> CREATE DATABASE database_name        
 ==> Drop Database or delete it

           -> DROP DATABASE database_name          
 ==> Connect the database to the mongodb

           -> \c database_name 
 ==> Create Table without Constraints   

           -> CREATE TABLE table_name(
              Column name + data type 
              )
        Eg: 

           -> CREATE TABLE person (
              id int,
              first_name VARCHAR(50),
              last_name VARCHAR(50),
              gender VARCHAR(6),
              date_of_birth TIMESTAMP
          )             
==> Create Table With Postgres
      
            -> CREATE TABLE table_name(
              Column name + data type + constraints if any
              )

           Eg:- 

             -> CREATE TABLE person (
                id BIGSERIAL NOT NULL PRIMARY KEY,
                first_name VARCHAR(50) NOT NULL,
                last_name VARCHAR(50) NOT NULL,
                gender VARCHAR(7) NOT NULL,
                date_of_birth DATE NOT NULL,
                email VARCHAR(150)  );


             )   

 ==> To See all the tables in it 

           -> \d
  ==> To See Only  the tables in it 

            -> \dt
 ==> To see the Specific table 

           -> \d table_name             
 ==> To delete the Table 

           -> DROP TABLE table_name
===> Insert records into tables
           
           -> INSERT INTO table_name (

            table_colum names which the values should add

           )
           VALUES(values corresponding to the table_column);

            
        Eg:-

           -> INSERT INTO person(
            first_name ,
            last_name,
            gender ,
            date_of_birth,
            email
            )
            VALUES('Arun','Vinod K','MALE','10/04/2001',email);

  ==> TO use the file of SQL

           -> \i the path of the file          
        
        Eg:- 
            \i /home/arunfloyd/Desktop/Works/Bro Camp/Week-16/postgreSQL/person.sql
  
  ==> Show the all tables values 

          -> SELECT * FROM table_name;

  ==> Show only a single Column 

          -> SELECT tables_column-name,tables_column2-name,... FROM table_name
                     
  ==> Show the values according to a specific ORDER BY

          -> SELECT * FROM table_name ORDER BY table_column1_name (Default order is Ascending)

                                Ascending = ASC
                                Desending = DESC         
            Eg :- 
                SELECT * FROM person ORDER BY first_name;                                 

  ==> Show the DISTINCT Values Only            

         -> SELECT DISTINCT * FROM table_name ORDER BY table_column1_name      

         Eg :- 
         
            SELECT DISTINCT "country of birth"  FROM person ORDER BY "country of birth";                 

  ==> Condition using WHERE Clause and AND for filtering
    
         -> SELECT * FROM table_name WHERE the condition can be given here AND other condition 

            --Either Conditions 
         -> SELECT * FROM table_name WHERE the condition can be given here AND (First condition OR Second Condition )
          

         Eg: -

               -- Using WHERE
            1. SELECT * FROM person WHERE gender = 'Male';
               -- Using WHERE AND 
            2. SELECT * FROM person WHERE gender = 'Male' AND "country of birth"= 'China';
               -- Using WHERE AND OR 
            3.SELECT * FROM person  WHERE gender = 'Male' AND ("country of birth"= 'China' OR "country of birth"='Poland');     
               --Using WHERE AND OR AND
            4. SELECT * FROM person WHERE gender = 'Male' AND ("country of birth"= 'China' OR "country of birth"='Poland') AND last_name = 'Pietersma'   
        
  ==> Comparison Operators 
     -> We can use this in all data types

         -> Not Equal to  ---  SELECT 1<>2; [true]

         -> Equal to ---  ---  SELECT 1=2; [False]

         -> Less than or equal to --- SELECT 1<=2; [True]


  ==> IN Keyword take a array of values and return the results

     Eg:-
        -> SELECT * FROM person WHERE "country of birth" IN ('China','Brazil');

  ==> BETWEEN Keyword to select the datas from a range 

     Eg :-

        -> SELECT * FROM person WHERE "date of birth" BETWEEN DATE '2001-01-01' AND '2024-01-01';
   

  ==> Like and iLike  used to match the patterns of text 
   ->Like is Case sensitive and iLike is not 

     Eg:-
      
       -> SELECT * FROM person WHERE email LIKE '%@gmail.com'
       ->  SELECT * FROM person WHERE email LIKE '---------@%' ;

       -> SELECT * FROM person WHERE first_name ILIKE 'p%' ;

  ==> GROUP BY  keyword
     -> To select a group of items to do the operation

       Eg:- 
         
          -> SELECT "country of birth",COUNT(*) FROM person GROUP BY "country of birth";
          -> SELECT "country of birth",COUNT(*) FROM person GROUP BY "country of birth" ORDER BY "country of birth";
 
  ==> HAVING keyword
     -> To specify any condition  

      Eg:-
         
         ->SELECT "country of birth",COUNT(*) FROM person GROUP BY "country of birth" HAVING COUNT(*)>20 ORDER BY "country of birth";
         ->SELECT "country of birth",COUNT(*) FROM person GROUP BY "country of birth" HAVING COUNT(*)>20 AND COUNT(*)<40 ORDER BY "country of birth";

  ===> MAX , MIN and AVERAGE Keyword       

     Eg:-
      
       -> SELECT MAX(price) FROM car;
       -> SELECT MIN(price) FROM car;
       -> SELECT AVG(price) FROM car;

  ===> ROUND keyword 

     Eg:-
       
       -> SELECT ROUND(AVG(price)) FROM car;
   
  ===> SUM operation
   
     Eg:-
       
       -> SELECT SUM(price) FROM car
   
   ===> Basic Of Arithmetic Operators     

      Eg:-
         
        -> SELECT 10+2 
        -> SELECT 10*2 
        -> SELECT 10/2
        -> SELECT 10^2 (Power)
        -> SELECT 5!  (Factorial)
        -> SELECT 10%3 (Modulus)

   ===> Column name as ALIAS using AS keyword 
     
      Eg:-

        -> SELECT id,make,model,price AS original_price,ROUND(price*.10,2) AS discount ,ROUND(price-(price * .10),2) AS Final_Price FROM car
   
   ===> COALESCE Keyword 
        -> To give some default values when there is no such value present.

      Eg:-
         
         -> SELECT COALESCE(email,'Email not provided') FROM person;

   ===> NULLIF Keyword       

      Eg:-

         -> SELECT 10 / NULLIF(0,2);
         -> SELECT COALESCE (10 / NULLIF ( 0, 0), 0)
          

   ===> TIMESTAMP and DATES
    
      Eg:-

         -> SELECT NOW();   ---> 2024-03-20 16:30:15.804443+05:30
         -> SELECT NOW()::DATE;  ---> 2024-03-20

   ===> Adding and Substracting With Dates 

      Eg:-

         -> SELECT NOW() -INTERVAL '10 YEARS';  ---> 2014-03-20 16:38:53.513771+05:30
         -> SELECT NOW()::DATE +INTERVAL '12 DAYS';  ---> 2024-04-01
   
   ===> Extracting Fields From TimeStamp

      Eg:-
       
        -> SELECT EXTRACT (MONTH FROM NOW())  ---> 3
        -> SELECT EXTRACT (MONTH FROM NOW())  ---> 2024
   
   ===> Age Function  

      Eg:-

        -> SELECT first_name ,AGE(NOW(),"date of birth") AS age FROM person;

   ===> PRIMARY KEYS 
         => Uniquely identify a record in any tables      
         
   ===> To delete a constraint from the existing table

          ->  ALTER TABLE table_name DROP CONSTRAINT constraint_name
      
   ===> To add the constraint to a existing table 

          -> ALTER TABLE table_name ADD PRIMARY KEY(fields_to_be_primary)

   ===> Unique Constraints 
         => Can only have the unique values in the column;

         -> ALTER TABLE table_name ADD UNIQUE (field_name) 
         -> ALTER TABLE table_name ADD CONSTRAINT create_a_name UNIQUE (field_name)
 

   ==> Check Constraints 
        => It allows to add a constraint based on  a boolean condition 

         -> ALTER TABLE table_name ADD CONSTRAINT create_a_name CHECK (the_condition_can_here)

      Eg:-
         -> ALTER TABLE person ADD CONSTRAINT gender_constraints CHECK (gender='Female' OR gender ='Male');

   ==> Delete from the table 
        
         -> DELETE FROM table_name WHERE mention_what_to_delete
      
      Eg:-
         -> DELETE FROM person WHERE first_name = 'Ayn';

         -> DELETE FROM person WHERE first_name = 'Ayn' AND gender ='Male';

   ===> Upadate the records of the table     
     
         -> UPDATE table_name SET field_name = updating_value WHERE mention_the_row
      
      Eg:-

        -> UPDATE person SET email ='arun@gmail.com' WHERE first_name = 'Nealy';
        -> UPDATE person SET email ='arun@gmail.com',last_name = 'Near' WHERE first_name = 'Nealy';

         
   ===> On Conflict Do Nothing 

      Eg:- 

       -> INSERT INTO person (first_name, last_name, email, gender, "date of birth", "country of birth") 
          VALUES ('Shelba', 'Laver',   null, 'Female', '2023-04-28', 'Philippines') ON CONFLICT(id) DO NOTHING;
  
   ===> Upsert 

      Eg;- 

       -> INSERT INTO person (first_name, last_name, email, gender, "date of birth", "country of birth") 
          VALUES ('Shelba', 'Laver',   null, 'Female', '2023-04-28', 'Philippines') ON CONFLICT(id) DO UPDATE
          SET email = EXCLUDED.first_email;

   ===> Relationship / Foreign Key 
         -> A foreign Key is a column that refernces a primary key in another table 
   
   ===> Adding Relationship between Tables 
    
       Eg:-

         ->UPDATE person SET car_id =4 WHERE id = 5;

   ==> INNER JOINS
       -> It link the two table where the primary key and the foreign key are found in the same table. 
       -> Combine two tables if there is a foreign key which is present on the tables then it will combine and create a new record  

       Eg:-

         -> SELECT * FROM person JOIN car ON person.car_id = car.id;
         -> SELECT person.first_name ,car.make ,car.model ,car.price FROM person JOIN car ON person.car_id = car.id; 
      
   ==> LEFT JOINS
        -> It is a type of join operation that returns all records from the left table (table1) and
           the matched records from the right table (table2).
        -> If there are no matching records in the right table, NULL values are returned for the columns from the right table.

        Eg;- 

         -> SELECT * FROM person LEFT JOIN car ON person.car_id = car.id; 

   ==> Delete Records Within Foreign Keys
     -> If we try to delete a value which was having the foreign key it doesnt works.
     -> So to do so we have to delete the refered value first and then do the same.

   ==> Exporting Query Results to CSV 

     -> \copy (Query for making the result to be exported) TO location_to_save_with_filename DELIMITER ',' CSV HEADER;

    Eg:-

     -> \copy (SELECT * FROM person LEFT JOIN car ON person.car_id = car.id);

   ==> Restart the Sequence

     -> ALTER SEQUENCE name_of_the_sequence RESTART WITH any_number

     Eg:-

     -> ALTER SEQUENCE person_id_seq RESTART WITH 10
        
   ==> Download a new Extension 
       
       -> CREATE EXTENSION IF NOT EXISTS 'Extension Name'
    Eg:-

       -> CREATE EXTENSION IF NOT EXISTS "uuid-ossp"; 
   ==> Use the Extension 

     Eg:- 

       -> SELECT uuid_generate_v4();
       
 ===> Additional Work Outs

      Eg:- 

        -> SELECT make,model,MIN(PRICE) FROM car GROUP BY make,model;
        -> SELECT make,SUM(price) FROM car GROUP BY make;

   => Promotional Offers 

      Eg:-To get the discount amount and the amount after the discount

       -> SELECT id,make ,model,price,ROUND(price*.10),ROUND(price -(price* .10),2) FROM car;  