# Movie Bookings SQL Project

## Project Overview
This project demonstrates essential SQL skills through managing and analyzing a movie bookings database. It involves creating and populating tables for movies, customers, and bookings, then performing various queries to extract meaningful insights.

***

## Project Title
**Movie Bookings Analysis**

***

## Level
Beginner to Intermediate

---

## Database
MySQL (movies database)

---

## Project Description
This project focuses on creating a relational database for a cinema booking system, including:

- Movies table with details such as title, genre, release date, rating, and running time.
- Customers table storing customer details like name, gender, age, and email.
- Bookings table capturing booking details including customer, movie, booking date, ticket quantity, timings, and cost.

Using these tables, the project performs queries to:
- Analyze customer demographics
- Track booking counts and revenues
- Retrieve top-rated movies
- Identify customer booking patterns
- Use aggregate functions, JOINs, GROUP BY, and CASE statements for business insights

---

## Objectives
- Set up the database with tables and insert data.
- Query data to find average age of customers by gender.
- Retrieve top-rated movies and ratings.
- Count bookings per movie and genre.
- Identify customers with the highest bookings.
- Calculate revenue over a date range.
- Classify customers into age groups.
- Perform advanced SQL queries using joins, subqueries, and window functions.

***

## Project Structure

1. **Database Setup**
   - Create `movies`, `customers`, and `bookings` tables.
   - Populate tables with sample data reflecting popular movies and customers.

2. **SQL Queries**
   - Analytical queries to retrieve business insights such as:
     - Average age of male customers
     - Top 4 movies by rating
     - Total bookings per genre
     - Customers with more than two bookings
     - Total revenue in a specified period
     - Customer classification based on age groups
     - And many more.

---
-- 🔄 Use the "movies" database
USE movies;

-- 🎬 Table: Movies
CREATE TABLE movies (
    movie_id INT PRIMARY KEY,
    title VARCHAR(255),
    release_date DATE,
    genre VARCHAR(50),
    rating VARCHAR(10),
    running_time VARCHAR(50)
);

-- 📥 Data: Movies
INSERT INTO movies (movie_id, title, release_date, genre, rating, running_time) VALUES
(1, 'The Shawshank Redemption', '1994-09-10', 'Drama', '9.3/10', '142 minutes'),
(2, 'The Godfather', '1972-03-24', 'Crime', '9.2/10', '175 minutes'),
(3, 'The Dark Knight', '2008-07-18', 'Action', '8.9/10', '152 minutes'),
(4, 'The Godfather Part II', '1974-03-25', 'Crime', '9.0/10', '202 minutes'),
(5, 'Pulp Fiction', '1994-10-14', 'Crime', '8.9/10', '154 minutes'),
(6, '12 Angry Men', '1957-09-13', 'Drama', '8.9/10', '120 minutes'),
(7, 'Schindlers List', '1993-12-15', 'Drama', '9.2/10', '195 minutes'),
(8, 'The Lord of the Rings: The Return of the King', '2003-12-17', 'Adventure', '8.9/10', '201 minutes'),
(9, 'The Lord of the Rings: The Fellowship of the Ring', '2001-12-10', 'Adventure', '8.8/10', '178 minutes'),
(10, 'The Lord of the Rings: The Two Towers', '2002-12-11', 'Adventure', '8.8/10', '201 minutes'),
(11, 'Inception', '2010-07-08', 'Action', '8.85/10', '148 minutes'),
(12, 'The Matrix', '1999-03-31', 'Action', '8.7/10', '136 minutes'),
(13, 'The Matrix Reloaded', '2003-05-15', 'Action', '7.9/10', '156 minutes'),
(14, 'The Matrix Revolutions', '2003-11-05', 'Action', '7.7/10', '128 minutes'),
(15, 'Interstellar', '2014-11-05', 'Sci-Fi', '8.6/10', '169 minutes');

-- 🧍 Table: Customers
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    name VARCHAR(100),
    gender VARCHAR(10),
    email_id VARCHAR(255),
    age INT
);

-- 📥 Data: Customers
INSERT INTO customers (customer_id, name, gender, email_id, age) VALUES
(1, 'John Doe', 'Male', 'johndoe@exp.com', 30),
(2, 'Jane Doe', 'Female', 'janedoe@exp.com', 25),
(3, 'Mary Smith', 'Female', 'marysmith@exp.com', 40),
(4, 'Michael Jones', 'Male', 'michaeljones@exp.com', 35),
(5, 'Sarah Brown', 'Female', 'sarahbrown@exp.com', 20),
(6, 'David Green', 'Male', 'davidgreen@exp.com', 25),
(7, 'Susan White', 'Female', 'susanwhite@exp.com', 30),
(8, 'Peter Black', 'Male', 'peterblack@exp.com', 35),
(9, 'Kate Blue', 'Female', 'kateblue@exp.com', 40),
(10, 'Alex Red', 'Male', 'alexred@exp.com', 20),
(11, 'Ben Green', 'Male', 'bengreen@exp.com', 25),
(12, 'Cindy White', 'Female', 'cindywhite@exp.com', 30),
(13, 'David Brown', 'Male', 'davidbrown@exp.com', 35),
(14, 'Peter Smith', 'Male', 'petersmith@exp.com', 40),
(15, 'Jane Black', 'Female', 'janeb@exp.com', 20);

-- 🎟️ Table: Bookings
CREATE TABLE bookings (
    booking_id INT PRIMARY KEY,
    customer_id INT,
    movie_id INT,
    booking_date DATE,
    ticket_quantity INT,
    timings TIME,
    cost INT
);

-- 📥 Data: Bookings
INSERT INTO bookings (booking_id, customer_id, movie_id, booking_date, ticket_quantity, timings, cost) VALUES
(1, 5, 1, '2023-06-01', 2, '18:00:00', 20),
(2, 15, 3, '2023-06-02', 3, '20:30:00', 30),
(3, 7, 7, '2023-06-02', 1, '16:15:00', 10),
(4, 6, 10, '2023-06-03', 2, '19:45:00', 20),
(5, 2, 5, '2023-06-03', 1, '21:00:00', 10),
(6, 13, 2, '2023-06-04', 4, '14:30:00', 40),
(7, 1, 9, '2023-06-04', 3, '17:45:00', 30),
(8, 3, 4, '2023-06-05', 2, '19:30:00', 20),
(9, 2, 12, '2023-06-05', 1, '13:45:00', 10),
(10, 4, 6, '2023-06-06', 1, '20:00:00', 10),
(11, 8, 8, '2023-06-07', 4, '15:30:00', 40),
(12, 11, 7, '2023-06-07', 3, '17:00:00', 30),
(13, 14, 13, '2023-06-08', 2, '16:45:00', 20),
(14, 12, 14, '2023-06-08', 1, '19:15:00', 10),
(15, 6, 4, '2023-06-09', 2, '21:30:00', 20),
(16, 9, 9, '2023-06-10', 1, '14:15:00', 10),
(17, 2, 2, '2023-06-10', 4, '17:30:00', 40),
(18, 3, 15, '2023-06-10', 3, '20:00:00', 30),
(19, 5, 6, '2023-06-11', 2, '13:45:00', 20),
(20, 7, 10, '2023-06-11', 1, '16:30:00', 10),
(21, 10, 1, '2023-06-12', 4, '18:45:00', 40),
(22, 11, 11, '2023-06-12', 3, '21:15:00', 30),
(23, 9, 13, '2023-06-14', 2, '15:00:00', 20),
(24, 8, 12, '2023-06-15', 1, '17:30:00', 10);
es

- Calculate average age of male customers:
```sql
SELECT AVG(age) FROM customers WHERE gender = 'Male';
-- 📁 Database: movies

-- 🎬 Create movies table
CREATE TABLE movies (
    movie_id INT PRIMARY KEY,
    title VARCHAR(255),
    release_date DATE,
    genre VARCHAR(50),
    rating VARCHAR(10),
    running_time VARCHAR(50)
);

-- 📥 Insert sample movie data
INSERT INTO movies (movie_id, title, release_date, genre, rating, running_time) VALUES
(1, 'The Shawshank Redemption', '1994-09-10', 'Drama', '9.3/10', '142 minutes'),
(2, 'The Godfather', '1972-03-24', 'Crime', '9.2/10', '175 minutes'),
(3, 'The Dark Knight', '2008-07-18', 'Action', '8.9/10', '152 minutes'),
-- ... (remaining movies omitted for brevity)
(15, 'Interstellar', '2014-11-05', 'Sci-Fi', '8.6/10', '169 minutes');

-- 👥 Create customers table
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    name VARCHAR(100),
    gender VARCHAR(10),
    email_id VARCHAR(255),
    age INT
);

-- 📥 Insert sample customer data
INSERT INTO customers (customer_id, name, gender, email_id, age) VALUES
(1, 'John Doe', 'Male', 'johndoe@exp.com', 30),
(2, 'Jane Doe', 'Female', 'janedoe@exp.com', 25),
-- ... (remaining customers omitted for brevity)
(15, 'Jane Black', 'Female', 'janeb@exp.com', 20);

-- 🎟️ Create bookings table
CREATE TABLE bookings (
    booking_id INT PRIMARY KEY,
    customer_id INT,
    movie_id INT,
    booking_date DATE,
    ticket_quantity INT,
    timings TIME,
    cost INT
);

-- 📥 Insert sample bookings data
INSERT INTO bookings (booking_id, customer_id, movie_id, booking_date, ticket_quantity, timings, cost) VALUES
(1, 5, 1, '2023-06-01', 2, '18:00:00', 20),
(2, 15, 3, '2023-06-02', 3, '20:30:00', 30),
-- ... (remaining bookings omitted for brevity)
(24, 8, 12, '2023-06-15', 1, '17:30:00', 10);

-- 📊 Queries
-- 1. Average age of male customers
SELECT AVG(age) FROM customers WHERE gender = 'Male';

-- 2. Top 4 highest-rated movies
SELECT * FROM movies ORDER BY rating DESC LIMIT 4;

-- 3. Movie titles and ratings above 8.5
SELECT title, rating FROM movies WHERE rating > 8.5;

-- 4. Highest rating by genre
SELECT genre, MAX(rating) FROM movies GROUP BY genre;

-- 5. Bookings count per genre
SELECT genre, COUNT(*) FROM movies JOIN bookings ON movies.movie_id = bookings.movie_id GROUP BY genre;

-- 6. Customers with more than 2 bookings
SELECT c.name FROM customers c JOIN bookings b ON c.customer_id = b.customer_id GROUP BY c.customer_id HAVING COUNT(*) > 2;

-- 7. Percentage of male customers
SELECT AVG(CASE WHEN gender = 'Male' THEN 1 ELSE 0 END) * 100 FROM customers;

-- 8. Customer with the most bookings
SELECT c.name, COUNT(*) AS booking_count FROM customers c  JOIN bookings b ON c.customer_id = b.customer_id GROUP BY c.customer_id ORDER BY booking_count DESC LIMIT 1;

-- 9. Customers who booked movie_id = 5
SELECT c.name, c.age FROM customers c JOIN bookings b ON c.customer_id = b.customer_id WHERE b.movie_id = 5;

-- 10. Bookings count per genre
SELECT m.genre, COUNT(b.booking_id) AS booking_count FROM movies m LEFT JOIN bookings b ON m.movie_id = b.movie_id GROUP BY m.genre;

-- 11. Average ticket quantity per movie
SELECT m.title, AVG(ticket_quantity) AS average_ticket_quantity FROM movies m JOIN bookings b ON m.movie_id = b.movie_id GROUP BY m.title;

-- 12. Customer names/emails for bookings on 2023-06-05
SELECT c.name, c.email_id FROM customers c JOIN bookings b ON c.customer_id = b.customer_id WHERE b.booking_date = '2023-06-05';

-- 13. Movies with highest rating
SELECT * FROM movies WHERE rating = (SELECT MAX(rating) FROM movies);

-- 14. Assign customer age groups
SELECT customer_id, name,
CASE
    WHEN age < 18 THEN 'Minor'
    WHEN age >= 18 AND age < 30 THEN 'Young Adult'
    WHEN age >= 30 AND age < 60 THEN 'Adult'
    ELSE 'Senior'
END AS age_group
FROM customers;

-- 15. Average rating for long-running movies
SELECT AVG(rating) AS average_rating FROM movies WHERE running_time > 178;

-- 16. Total revenue between specific dates
SELECT SUM(cost) AS total_revenue FROM bookings WHERE booking_date between '2023-06-04' and '2023-06-12';

-- 17. Bookings per date
SELECT booking_date, COUNT(*) FROM bookings GROUP BY booking_date;

-- 18. Total cost per customer
SELECT c.name, SUM(b.cost) AS total_cost FROM customers c JOIN bookings b ON c.customer_id = b.customer_id GROUP BY c.customer_id;

-- 19. Total bookings per movie (2 approaches)
SELECT m.title, COUNT(b.booking_id) AS total_bookings FROM movies m LEFT JOIN bookings b ON m.movie_id = b.movie_id GROUP BY m.movie_id, m.title;

SELECT m.title, (SELECT COUNT(*) FROM bookings b WHERE b.movie_id = m.movie_id) AS total_bookings FROM movies m;

-- 20. First booking customer (2 approaches)
SELECT c.customer_id, c.name FROM bookings b JOIN customers c ON b.customer_id = c.customer_id WHERE b.booking_date = (SELECT MIN(booking_date) FROM bookings);

SELECT c.customer_id, c.name FROM bookings b JOIN customers c ON b.customer_id = c.customer_id ORDER BY b.booking_date, b.timings LIMIT 1;

-- 21. Customers with booking counts
SELECT c.name, COUNT(b.booking_id) AS booking_count FROM customers c LEFT JOIN bookings b ON c.customer_id = b.customer_id GROUP BY c.customer_id ORDER BY booking_count DESC;

-- 22. Total seats booked after 8PM
SELECT SUM(CASE WHEN timings > '20:00:00' THEN ticket_quantity ELSE 0 END) AS total_seats_booked FROM bookings;

-- 23. Customer with most tickets
SELECT * FROM customers WHERE customer_id = (
    SELECT customer_id FROM bookings GROUP BY customer_id ORDER BY SUM(ticket_quantity) DESC LIMIT 1
);

-- Alternate approach
WITH customer_tickets AS (
    SELECT customer_id, SUM(ticket_quantity) AS total_tickets FROM bookings GROUP BY customer_id
)
SELECT c.customer_id, c.name, c.gender, c.email_id, c.age
FROM customers c
JOIN customer_tickets ct ON c.customer_id = ct.customer_id
WHERE ct.total_tickets = (SELECT MAX(total_tickets) FROM customer_tickets);
