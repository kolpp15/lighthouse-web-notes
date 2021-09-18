# W5D1 Notes

## SQL
- Andy's example: elephantsql
- SQL is not case sensitive
  - HOWEVER, we caps SQL language to differentiate between SQL command and ours

## Single table SQL
- when counting all, usually use * in case of missing column (ie. email address)
```sql
SELECT COUNT(*) AS num_users 
FROM users;
```

```sql
SELECT *
FROM users
WHERE (age > 18 AND last_name = 'Barrows');
```
- If you want more filter, use AND or OR
- SQL treats '' as strings. "" as column names

```sql
SELECt *
FROM users
WHERE age > 18 AND country = 'Canada'
ORDER BY age DESC, last_name;
```
- ORDER BY will order 
- Opposite way ordering will be DESC
- to order more than one, add a comma

```sql
SELECT *
FROM users
WHERE country = 'Canada' AND payment_due_date > '2021-08-16';

-- this can improve: 

SELECT * NOW() as now
FROM users
WHERE country = 'Canada' AND payment_due_date < NOW();

-- hour specific: 
SELECT * CURRENT_DATE as current_date
FROM users
WHERE country = 'Canada' AND payment_due_date < CURRENT_DATE;
```
- this will be hour specific as well. SQL treats midnight if hour is not specified

To filter duplicates: 
```sql
SELECT DISTINCT country
FROM users
ORDER BY country;
```
- but we can't DISTINCT two things like: `SELECT DISTINCT country, last_name`

## Double table SQL
```sql
SELECT album_name, artist_name, song name
FROM albums
JOIN songs ON albums.id = album_id; 
```
- You have to somehow find a connection
- cannot be ambiguous where two tables share the same primary keys. Thus, you have to explicitly define `albums.id`

```sql
SELECT album_name, COUNT(songs.*) AS num_songs
FROM albums
JOIN songs ON albums.id = songs.album_id
GROUP BY album_name
HAVING COUNT(songs.*) > 10;
```
There's an order that has to be defined
1. FROM and JOIN 
2. WHERE
3. GROUP BY
4. HAVING: if aggregating, we have to use HAVING instead of WHERE 
5. SELECT
6. DISTINCT
7. ORDER BY 

```sql
-- Refer to the venn diagram 
-- If you want to join and show all the left column AND the inner join, say LEFT JOIN

SELECT album_name, artist_name, song_name
FROM albums
LEFT JOIN songs ON albums.id = songs.album_id;
WHERE songs.ablum_id IS NULL;
```
- Everything in the FROM is the LEFT table. Everthing after JOIN is the RIGHT

Visuaize join: sql-joins.leopard.in.us

```sql
SELECT album_name, AVG(songs.rating) AS avg_rating, MIN(songs.rating), MAX(songs.rating)
FROM albums
JOIN songs ON albums.id = songs.album_id;
GROUP BY album_name;
```
- Can have multiple AVG, MIN, MAX

```sql
-- to compare:
SELECT albums.album_name, 
  songs.song_name, 
  songs.rating
  (SELECT AVG(songs.rating) FROM songs WHERE songs.album_id = albums.id) AS avg_rating
FROM albums
JOIN songs ON albums.id = songs.album_id;
WHERE songs.rating > (SELECT AVG(songs.rating) FROM songs WHERE songs.album_id = albums.id); 
```
  - This will compare and only show the songs that have ratings more than the AVG ratings

## LIMITING in SQL
```sql
--LIMIT comes the last. Below sample will show the top 10 and start from 11 to 20
SELECT *
FROM users
LIMIT 10 OFFSET 10;
```
- `OFFSET (page_number - 1) * 10`
- ex) if you want to show only 31-40
- `OFFSET (3-1) * 10`