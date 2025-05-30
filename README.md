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

```Calculate average age of male customers:```
```sql
SELECT AVG(age) FROM customers WHERE gender = 'Male';
--  Database: movies

--  Create movies table
CREATE TABLE movies (
    movie_id INT PRIMARY KEY,
    title VARCHAR(255),
    release_date DATE,
    genre VARCHAR(50),
    rating VARCHAR(10),
    running_time VARCHAR(50)
);

--  Insert sample movie data
INSERT INTO movies (movie_id, title, release_date, genre, rating, running_time) VALUES
(1, 'The Shawshank Redemption', '1994-09-10', 'Drama', '9.3/10', '142 minutes'),
(2, 'The Godfather', '1972-03-24', 'Crime', '9.2/10', '175 minutes'),
(3, 'The Dark Knight', '2008-07-18', 'Action', '8.9/10', '152 minutes'),
-- ... (remaining movies omitted for brevity)
(15, 'Interstellar', '2014-11-05', 'Sci-Fi', '8.6/10', '169 minutes');

--  Create customers table
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    name VARCHAR(100),
    gender VARCHAR(10),
    email_id VARCHAR(255),
    age INT
);

-- Insert sample customer data
INSERT INTO customers (customer_id, name, gender, email_id, age) VALUES
(1, 'John Doe', 'Male', 'johndoe@exp.com', 30),
(2, 'Jane Doe', 'Female', 'janedoe@exp.com', 25),
-- ... (remaining customers omitted for brevity)
(15, 'Jane Black', 'Female', 'janeb@exp.com', 20);

--  Create bookings table
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
