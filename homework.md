## SQL Questions 

First create a database called fringe_shows
```
  #terminal
  psql
  create database fringe_shows;
  \q
```

Populate the data using the script - fringeshows.sql
```
  #terminal
  psql -d fringe_shows -f fringeshows.sql
```

Using the SQL Database file given to you as the source of data to answer the questions.  Copy the SQL command you have used to get the answer, and paste it below the question, along with the result they gave.


## Section 1

  Revision of concepts that we've learnt in SQL today

  1. Select the names of all users.
  COMMAND:
    SELECT name FROM users;

  RESULT:
           name       
    ------------------
     Rick Henri
     Jay Chetty
     Keith Douglas
     Ashleigh Adams
     Euan Blackledge
     Chris Flint
     Nico di Lillo
     Joe Maher
     Marie Moyles
     Iain Stewart
     Megan Strachan
     Russell Williams
     Sam Werngren
     Natalie Simpson
     Davide de Lerma
     Josh Kearns
     Renwick Drysdale
     Brian Morrice

  2. Select the names of all shows that cost less than £15.
  COMMAND:
    SELECT name FROM shows WHERE price < 15;
  RESULT:
                 name             
    ------------------------------
     Le Haggis
     Paul Dabek Mischief 
     Best of Burlesque
     Two become One
     Urinetown
     Two girls, one cup of comedy

  3. Insert a user with the name "Val Gibson" into the users table.
  COMMAND:
    INSERT INTO users(name) VALUES ('Val Gibson');
  RESULT:
    id |    name    
    ----+------------
    19 | Val Gibson

  4. Insert a record that Val Gibson wants to attend the show "Two girls, one cup of comedy".
  COMMAND:
    INSERT INTO "shows_users" (show_id, user_id) VALUES (12, 19);
  RESULT:
    INSERT 0 1
     id | show_id | user_id 
    ----+---------+---------
     82 |      12 |      19

  5. Updates the name of the "Val Gibson" user to be "Valerie Gibson".
  COMMAND:
    UPDATE users SET name = 'Valerie Gibson' WHERE name = 'Val Gibson';
  RESULT:
    UPDATE 1
     id |      name      
    ----+----------------
     19 | Valerie Gibson

  6. Deletes the user with the name 'Valerie Gibson'.
  COMMAND:
    DELETE FROM users WHERE name = 'Valerie Gibson';
  RESULT:
           name       
    ------------------
     Rick Henri
     Jay Chetty
     Keith Douglas
     Ashleigh Adams
     Euan Blackledge
     Chris Flint
     Nico di Lillo
     Joe Maher
     Marie Moyles
     Iain Stewart
     Megan Strachan
     Russell Williams
     Sam Werngren
     Natalie Simpson
     Davide de Lerma
     Josh Kearns
     Renwick Drysdale
     Brian Morrice

  7. Deletes the shows for the user you just deleted.
  COMMAND:
    DELETE FROM shows_users WHERE user_id = 19;
  RESULT:
    DELETE 1
     id | show_id | user_id 
    ----+---------+---------
    (0 rows)


## Section 2

  This section involves more complex queries.  You will need to go and find out about aggregate funcions in SQL to answer some of the next questions.

  9. Select the names and prices of all shows, ordered by price in ascending order.
  COMMAND:
    SELECT name, price 
    FROM shows
    ORDER BY price ASC;
  RESULT:
                      name                   | price 
    -----------------------------------------+-------
     Two girls, one cup of comedy            |  6.00
     Best of Burlesque                       |  7.99
     Two become One                          |  8.50
     Urinetown                               |  8.50
     Paul Dabek Mischief                     | 12.99
     Le Haggis                               | 12.99
     Joe Stilgoe: Songs on Film – The Sequel | 16.50
     Game of Thrones - The Musical           | 16.50
     Shitfaced Shakespeare                   | 16.50
     Aaabeduation – A Magic Show             | 17.99
     Camille O'Sullivan                      | 17.99
     Balletronics                            | 32.00
     Edinburgh Royal Tattoo                  | 32.99
    (13 rows)

  10. Select the average price of all shows.
  COMMAND:
    SELECT AVG(price) FROM shows;

  RESULT:
             avg         
    ---------------------
     15.9569230769230769
    (1 row)

  11. Select the price of the least expensive show.
  COMMAND:
    SELECT MIN(price) FROM shows;

  RESULT:
     min  
    ------
     6.00
    (1 row)

  12. Select the sum of the price of all shows.
  COMMAND:
    SELECT SUM(price) FROM shows;

  RESULT:
      sum   
    --------
     207.44
    (1 row)

  13. Select the sum of the price of all shows whose prices is less than £20.
  COMMAND:
      SELECT SUM(price) FROM shows WHERE price < 20;

  RESULT:
      sum   
    --------
     142.45
    (1 row)

  14. Select the name and price of the most expensive show.
  COMMAND:
    SELECT price, name FROM shows
    ORDER BY price DESC
    LIMIT 1;

  RESULT:
     price |          name          
    -------+------------------------
     32.99 | Edinburgh Royal Tattoo
    (1 row)

  15. Select the name and price of the second from cheapest show.
  COMMAND:
    SELECT MIN(price) and name FROM shows
    WHERE price NOT IN (SELECT MIN(price) and name FROM shows );

  RESULT:
     min  
    ------
     7.99
    (1 row)

  16. Select the names of all users whose names start with the letter "N".

  17. Select the names of users whose names contain "er".


## Section 3

  The following questions can be answered by using nested SQL statements but ideally you should learn about JOIN clauses to answer them.

  18. Select the time for the Edinburgh Royal Tattoo.

  19. Select the number of users who want to see "Shitfaced Shakespeare".

  20. Select all of the user names and the count of shows they're going to see.

  21. SELECT all users who are going to a show at 17:15.
