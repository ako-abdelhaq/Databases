# Databases: Relational Databases and SQL


This course is one of five self-paced courses on the topic of Databases by Stanford University available on edx.org. This course provides an introduction to relational databases and comprehensive coverage of SQL, the long-accepted standard query language for relational database systems. Topics include : SELECT statement, Subqueries, JOIN operators, Data modification statements, and more.

This repository contains my solutions to the Database SQL course.

<br>

  

## Exercises

 
 

### 1) Movie-Rating

Here's the schema of this exercise:

******Movie ( mID, title, year, director )******
English: There is a movie with ID number mID, a title, a release year, and a director.  
  
******Reviewer ( rID, name )******
English: The reviewer with ID number rID has a certain name.  
  
******Rating ( rID, mID, stars, ratingDate )******
English: The reviewer rID gave the movie mID a number of stars rating (1-5) on a certain ratingDate.

<br>

Click [here][1] to see the database.<br>
Click [here][2] to see the schema and data (You have to download the file and preview it on the browser).
  
<br>
<br>



### 2) Social-Network

Here's the schema of this exercise:

**Highschooler ( ID, name, grade )**
English: There is a high school student with unique ID and a given first name in a certain grade.  
  
**Friend ( ID1, ID2 )**
English: The student with ID1 is friends with the student with ID2. Friendship is mutual, so if (123, 456) is in the Friend table, so is (456, 123).  
  
**Likes ( ID1, ID2 )**
English: The student with ID1 likes the student with ID2. Liking someone is not necessarily mutual, so if (123, 456) is in the Likes table, there is no guarantee that (456, 123) is also present.

<br>

Click [here][3] to see the database.<br>
Click [here][4] to see the schema and data (You have to download the file and preview it on the browser).

<br>
<br>
<br>



## Solutions

[SQL Movie-Rating Query Exercises (9 Questions)](https://github.com/ako-abdelhaq/Databases/blob/master/Relational%20Databases%20and%20SQL%20-%20edX/Answers/Movie-Rating%20Query%20Exercises%20(9%20Questions).md)

[SQL Movie-Rating Query Exercises Extras](https://github.com/ako-abdelhaq/Databases/blob/master/Relational%20Databases%20and%20SQL%20-%20edX/Answers/Movie-Rating%20Query%20Exercises%20Extras.md)

[SQL Social-Network Query Exercises (9 Questions)](https://github.com/ako-abdelhaq/Databases/blob/master/Relational%20Databases%20and%20SQL%20-%20edX/Answers/Social-Network%20Query%20Exercises%20(9%20Questions).md)

[SQL Social-Network Query Exercises Extras](https://github.com/ako-abdelhaq/Databases/blob/master/Relational%20Databases%20and%20SQL%20-%20edX/Answers/Social-Network%20Query%20Exercises%20Extras.md)

[SQL Movie-Rating Modification Exercises (3 Questions)](https://github.com/ako-abdelhaq/Databases/blob/master/Relational%20Databases%20and%20SQL%20-%20edX/Answers/Movie-Rating%20Modification%20Exercises%20(3%20Questions).md)

[SQL Social-Network Modification Exercises (3 Questions)](https://github.com/ako-abdelhaq/Databases/blob/master/Relational%20Databases%20and%20SQL%20-%20edX/Answers/Social-Network%20Modification%20Exercises%20(3%20Questions).md)



<br/>
<br/>

										           AKO 2022

  

[1]: https://github.com/ako-abdelhaq/Databases/blob/master/Relational%20Databases%20and%20SQL%20-%20edX/Movie-rating/rating.sql
[2]: https://github.com/ako-abdelhaq/Databases/blob/master/Relational%20Databases%20and%20SQL%20-%20edX/Movie-rating/moviedata.html

[3]: https://github.com/ako-abdelhaq/Databases/blob/master/Relational%20Databases%20and%20SQL%20-%20edX/Social-network/social.sql
[4]: https://github.com/ako-abdelhaq/Databases/blob/master/Relational%20Databases%20and%20SQL%20-%20edX/Social-network/socialdata.html
