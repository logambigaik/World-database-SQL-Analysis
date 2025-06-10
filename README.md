
# 🌍 World Database SQL Analysis

This project explores and analyzes the **MySQL `world` database**, which contains information about countries, cities, and their populations, life expectancy, and related metadata. The goal is to extract meaningful insights through SQL queries using various techniques like filtering, aggregation, joins, and sorting.

---

## 📁 Dataset Overview

We used the built-in `world` database that comes with MySQL. It includes the following tables:

- **country** – Contains country-level information including population, life expectancy, and region.
- **city** – Holds data for cities such as name, country code, district, and population.
- **countrylanguage** – (Not used here, but contains languages spoken per country.)

---

## 📊 SQL Tasks Performed

### 🔍 Exploring the Database
```sql
USE world;
DESC country;
```

### 🗺️ List of Cities
- Get distinct cities with their country codes and districts:
```sql
SELECT DISTINCT CountryCode, Name, District FROM city;
```

### 🇺🇸 Count of Cities in the USA
```sql
SELECT COUNT(DISTINCT city.Name) AS CitiesInUSA, country.Name 
FROM city 
JOIN country ON city.CountryCode = country.Code 
WHERE country.Name = 'United States';
```

### Alternate Method
```sql
SELECT COUNT(DISTINCT Name) AS CitiesInUSA 
FROM city 
WHERE CountryCode IN (
    SELECT Code FROM country WHERE Name = 'United States'
);
```

### 🧬 Country with the Highest Life Expectancy
Scenario: *As part of a global health initiative, we identify the country with the highest life expectancy.*
```sql
SELECT Name AS CountryName, LifeExpectancy 
FROM country 
WHERE LifeExpectancy = (SELECT MAX(LifeExpectancy) FROM country);
```

### 🏙️ City Name Filters and Patterns
- Cities starting with 'New':
```sql
SELECT Name FROM world.city WHERE Name LIKE 'New%';
```

- Cities starting with 'Be', sorted by population:
```sql
SELECT * FROM world.city 
WHERE Name LIKE 'Be%' 
ORDER BY Population DESC;
```

### 🌆 City Population Queries
- Top 10 most populous cities:
```sql
SELECT * FROM world.city 
ORDER BY Population DESC 
LIMIT 10;
```

- Cities with population > 2 million:
```sql
SELECT * FROM world.city 
WHERE Population > 2000000 
ORDER BY Population DESC;
```

- Cities with population between 500K and 1M:
```sql
SELECT Name, CountryCode, Population 
FROM world.city 
WHERE Population BETWEEN 500000 AND 1000000 
ORDER BY Population DESC;
```

### 🔠 Alphabetical City Listings
```sql
SELECT Name FROM world.city ORDER BY Name ASC;
```

### 🏙️ Largest and Smallest Cities by Population
- Most populous city:
```sql
SELECT Name AS CityName, CountryCode, Population 
FROM world.city 
ORDER BY Population DESC 
LIMIT 1;
```

- 10 least populous cities:
```sql
SELECT Name AS CityName, CountryCode, Population 
FROM world.city 
ORDER BY Population ASC 
LIMIT 10;
```

### 🔁 Repeated City Names
- Cities grouped by name with their occurrence count:
```sql
SELECT Name AS CityName, COUNT(Name) AS OccurrenceCount 
FROM world.city 
GROUP BY Name 
ORDER BY Name ASC;
-- HAVING COUNT(Name) > 3 (Uncomment to filter)
```

### 🌎 Most Popular Country
```sql
SELECT Name AS CountryName, Population 
FROM world.country 
ORDER BY Population DESC 
LIMIT 1;
```

---

## 📦 Technologies Used

- MySQL
- SQL Workbench / CLI

---

## ✅ Objectives

- Practice SQL skills on a real-world schema.
- Analyze population distributions, city trends, and country metrics.
- Use pattern matching, joins, subqueries, and aggregations.

---

## 📌 How to Use

1. Clone the repository.
2. Load the `world` database into MySQL.
3. Run the queries in the `.sql` or `.md` files in your SQL editor.
