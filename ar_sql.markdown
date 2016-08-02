## AUTHORS : CHRIS, ADRIAN

Translate SQL to ActiveRecord
======

SELECT *
FROM
  users;

```  
Users.all
```

SELECT *
FROM
  users
WHERE
  user.id = 1;

  ```
Users.first
  ```

SELECT *
FROM
  posts
ORDER BY
  created_at DESC
LIMIT 1;

```
Users.last
```


SELECT *
FROM
  users
JOIN
  posts
ON
  posts.author_id = users.id
WHERE
  posts.created_at >= '2014-08-31 00:00:00';

```
Users.joins("users on post.author_id = user.id").where(:created_at >= "2014-08-31 00:00:00")
```


SELECT
  count(*)
FROM
  users
GROUP BY
  favorite_color
HAVING
  count(*) > 1;

```
Users.select("COUNT(*) AS my_count").group(:favorite_color).having("my_count > 1")
```


The most recently updated user
```
Users.order(:updated_at => :desc).find(1)
```


* The oldest user (by age)

```
Users.order(:age => desc).find(1)
```

* all the users

```
Users.all
```

* all posts sorted in descending order by date created

```
Posts.order(:created_at => :desc)
```


Translate Active Record to SQL
======


Post.all

``` sql
SELECT *
FROM posts
```


Post.first

```sql
SELECT *
FROM posts
LIMIT 1
```

Post.last
SELECT *
FROM posts
ORDER BY created_at DESC
LIMIT 1

```sql
Post.where(:id => 4)
SELECT *
FROM posts
WHERE id = 4
```


Post.find(4)

```sql
SELECT
FROM posts
WHERE id = 4
```

User.count

```sql
SELECT COUNT(*)
FROM users
```

Post.select(:name).where(:created_at > 3.days.ago).order(:created\_at)

```sql
SELECT name
FROM post
WHERE created_at > CURRENT_DATE - 3
ORDER BY created_at
```

Post.select("COUNT(*)").group(:category_id)

```sql
SELECT COUNT(*)
FROM post
GROUP BY category_id
```

All posts created before 2014

```sql
SELECT *
FROM posts
WHERE created_at < '2014-1-1'
```

A list of all (unique) first names for authors who have written at least 3 posts

```sql
SELECT DISTINCT name, COUNT(post.authorid) AS count
FROM posts
HAVING count >= 3
```

The posts with titles that start with the word "The"

```sql
SELECT *
FROM posts
WHERE title LIKE 'The %'
```

Posts with IDs of 3,5,7, and 9

```sql
SELECT *
FROM posts
WHERE id IN (3,5,7,9)
```


Custom Translation: 3 Queries
======

1.youngest user by age 

```sql
 SELECT *
 FROM user
 ORDER BY age ASC
```
2.count the posts for users who's name starts with c

```sql
SELECT count(author_id)
FROM post
WHERE name ILIKE 'c%'
```
3. find the highest number of posts from users on a given category

```sql
SELECT category ,COUNT(post_id)
FROM posts
GROUP BY category
```
