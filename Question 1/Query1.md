Answer to question 1:
```
WITH RankedBooks AS (
  SELECT
    genre,
    title,
    rating,
    RANK() OVER (PARTITION BY genre ORDER BY rating DESC) AS rating_rank
  FROM books
)
SELECT
  b.genre,
  COUNT(b.title) AS book_number,
  MAX(CASE WHEN rb.rating_rank = 1 THEN rb.title END) AS highest_rated_title,
  MAX(CASE WHEN rb.rating_rank = 1 THEN rb.rating END) AS highest_rated,
  MAX(CASE WHEN rb.rating_rank = 2 THEN rb.title END) AS second_highest_rated_title,
  MAX(CASE WHEN rb.rating_rank = 2 THEN rb.rating END) AS second_highest_rated,
  AVG(b.rating) AS average_rating
FROM RankedBooks rb
JOIN books b ON rb.genre = b.genre
GROUP BY b.genre;
```
