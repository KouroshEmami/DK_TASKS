Answer to question 1:
```
WITH RankedBooks AS (
  SELECT
    genre,
    title,
    rating,
    DENSE_RANK() OVER (PARTITION BY genre ORDER BY rating DESC) AS rating_rank
  FROM books
)
SELECT
  genre,
  COUNT(DISTINCT title) AS book_number,
  MAX(CASE WHEN rating_rank = 1 THEN title END) AS highest_rated_title,
  MAX(CASE WHEN rating_rank = 1 THEN rating END) AS highest_rated,
  MAX(CASE WHEN rating_rank = 2 THEN title END) AS second_highest_rated_title,
  MAX(CASE WHEN rating_rank = 2 THEN rating END) AS second_highest_rated,
  AVG(rating) AS average_rating
FROM RankedBooks
GROUP BY genre;
```
