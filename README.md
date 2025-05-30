# Movie Bookings SQL Project

## Project Overview
This project demonstrates essential SQL skills through managing and analyzing a movie bookings database. It involves creating and populating tables for movies, customers, and bookings, then performing various queries to extract meaningful insights.

---

## Project Title
**Movie Bookings Analysis**

---

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

---

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

## Sample Query Examples

- Calculate average age of male customers:
```sql
SELECT AVG(age) FROM customers WHERE gender = 'Male';
