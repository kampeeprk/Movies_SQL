![image](https://github.com/stlionnn/Movies_SQL/assets/98281969/7671e792-8aee-447e-810d-814ae14b3703)![image](https://github.com/stlionnn/Movies_SQL/assets/98281969/a5151cfb-059d-4e94-9d33-1c92cdfc2472)# Movies_SQL

## Answer the business question

### 1. How many unique movies and directors exist in the dataset?
````sql
SELECT 
  COUNT(DISTINCT(id)) AS unique_movie
FROM movies
````
**Answer:**

![Screenshot 2023-06-13 101403](https://github.com/stlionnn/Movies_SQL/assets/98281969/9bdf3016-9f90-4ed5-abf4-0b30b69e68ca)

````sql
SELECT 
  COUNT(DISTINCT(id)) AS unique_director
FROM directors
````
**Answer:**

![Screenshot 2023-06-13 101548](https://github.com/stlionnn/Movies_SQL/assets/98281969/d320c830-0aeb-4818-873c-19cf1a7d77b2)

***

### 2. How much average budget do they spend on making movies? (2-digit answer)
````sql
SELECT 
  round(AVG(budget),2) AS average_movie_budget
FROM movies
````
**Answer:**

![Screenshot 2023-06-13 102111](https://github.com/stlionnn/Movies_SQL/assets/98281969/e29fa9e0-9fad-447c-a2d9-8eec5a105f82)

***

### 3. Top 5 movies order by vote average which vote count more than average
````sql 
SELECT 
  title, vote_average, vote_count 
FROM movies
WHERE vote_count > 
  (SELECT AVG(vote_count) FROM movies)
ORDER BY vote_average DESC
LIMIT 5
````
**Answer:**

![image](https://github.com/stlionnn/Movies_SQL/assets/98281969/3a5c15df-c2d1-4325-a96b-48adf371a19e)

***

### 4. How many movies does the name start with "the"?
````sql 
SELECT 
  COUNT(title) 
FROM movies
WHERE title LIKE 'The %'
````
**Answer:**

![image](https://github.com/stlionnn/Movies_SQL/assets/98281969/a7e0fe4d-7833-4ccb-bc53-5c49d33a7d87)

***
### 5. Directors and titles of movies that receive the top 5 revenue
````sql 
SELECT 
  title, 
  name as director_name, 
  revenue 
FROM movies m
JOIN directors d 
ON m.director_id = d.id 
ORDER BY revenue DESC 
LIMIT 5
````
**Answer:**

![image](https://github.com/stlionnn/Movies_SQL/assets/98281969/ca2bf523-a2d3-41dc-893a-d3205d15b60a)

***
### 6. Find the Top 5 losing movies, including the director's name.
````sql 
SELECT 
  title, 
  name as director_name, 
  (revenue-budget) net_profit 
FROM movies m
JOIN directors d 
ON m.director_id = d.id
ORDER BY net_profit ASC
LIMIT 5
````
**Answer:**

![image](https://github.com/stlionnn/Movies_SQL/assets/98281969/ae1c5bc7-086d-4581-9b28-7c5731bda471)

***
### 7. Top 10 movies by rating that directed by Steven Spielberg before 2010.
````sql 
SELECT 
	title, 
	vote_average, 
	release_date 
FROM movies m
JOIN directors d 
ON m.director_id = d.id
WHERe name = 'Steven Spielberg' and release_date < 2010
ORDER BY vote_average DESC
LIMIT 10
````
**Answer:**

![image](https://github.com/stlionnn/Movies_SQL/assets/98281969/d1df6adf-19f3-43b8-824a-00401bfed7a4)

***
### 8. The movie title and director that have a vote average score higher than average.
````sql 
WITH movie_and_director AS 
  (
  SELECT 
    title,
    name, 
    vote_average 
  FROM movies m 
  JOIN directors d 
  ON m.director_id = d.id
  WHERE vote_average > (SELECT AVG(vote_average) FROM movies)
  )

SELECT 
  COUNT(DISTINCT title) AS vote_more_than_avg_movie 
FROM movie_and_director
````
**Answer:**

![image](https://github.com/stlionnn/Movies_SQL/assets/98281969/da56cf87-70b3-4af7-834c-603cbd86b6ff)

***
### 9. Directors who directed more than 10 movies and generated revenue of more than $500 million
````sql 
WITH movie_and_director AS 
  (
  SELECT 
    COUNT(title) number_of_movie, 
    name, 
    revenue 
  FROM movies m
  JOIN directors d 
  ON m.director_id = d.id 
  GROUP BY name
  ORDER BY number_of_movie DESC)

SELECT 
  name as director_name, 
  number_of_movie, revenue 
FROM movie_and_director
WHERE number_of_movie >= 10 and revenue > 500000000
````
**Answer:**

![image](https://github.com/stlionnn/Movies_SQL/assets/98281969/f813264c-00dc-4566-9bca-83733d527e72)

***




























