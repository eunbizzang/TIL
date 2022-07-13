https://www.baeldung.com/spring-jpa-like-queries


LIKE Query Methods

---
Set up
```
INSERT INTO movie(id, title, director, rating, duration) 
    VALUES(1, 'Godzilla: King of the Monsters', ' Michael Dougherty', 'PG-13', 132);
INSERT INTO movie(id, title, director, rating, duration) 
    VALUES(2, 'Avengers: Endgame', 'Anthony Russo', 'PG-13', 181);
INSERT INTO movie(id, title, director, rating, duration) 
    VALUES(3, 'Captain Marvel', 'Anna Boden', 'PG-13', 123);
INSERT INTO movie(id, title, director, rating, duration) 
    VALUES(4, 'Dumbo', 'Tim Burton', 'PG', 112);
INSERT INTO movie(id, title, director, rating, duration) 
    VALUES(5, 'Booksmart', 'Olivia Wilde', 'R', 102);
INSERT INTO movie(id, title, director, rating, duration) 
    VALUES(6, 'Aladdin', 'Guy Ritchie', 'PG', 128);
INSERT INTO movie(id, title, director, rating, duration) 
    VALUES(7, 'The Sun Is Also a Star', 'Ry Russo-Young', 'PG-13', 100);
```
---

1. Containing, Contains, IsContaining and Like

    Ex)
    SELECT * FROM movie WHERE title LIKE '%in%';


    ```
    List<Movie> findByTitleContaining(String title);
    List<Movie> findByTitleContains(String title);
    List<Movie> findByTitleIsContaining(String title);

    movieRepository.findByTitleContaining("in");
    movieRepository.findByTitleIsContaining("in");
    movieRepository.findByTitleContains("in");
    ```
    We can expect each of the three methods to return the same results.


    With a Like keyword, we're required to provide the wildcard character with our search parameter.

    ```
    List<Movie> findByTitleLike(String title);

    movieRepository.findByTitleLike("%in%");
    ```


2. StartsWith

    ```
    SELECT * FROM Movie WHERE Rating LIKE 'PG%';

    List<Movie> findByRatingStartsWith(String rating);

    movieRepository.findByRatingStartsWith("PG");
    ```


3. EndsWith
    ```
    SELECT * FROM Movie WHERE director LIKE '%Burton';

    List<Movie> findByDirectorEndsWith(String director);

    movieRepository.findByDirectorEndsWith("Burton");
    ```


4. Case Insensitivity
    ```
    List<Movie> findByTitleContainingIgnoreCase(String title);

    movieRepository.findByTitleContainingIgnoreCase("the");
    ```
    We might accomplish this by forcing the column to all capital or lowercase letters and providing the same with values we're querying.


5. Not

    NotContains, NotContaining and NotLike keywords
    ```
    List<Movie> findByRatingNotContaining(String rating);

    List<Movie> results = movieRepository.findByRatingNotContaining("PG");
    assertEquals(1, results.size());
    ```

    To achieve functionality that finds records where the director's name doesn't start with a particular string, we'll use the NotLike keyword to retain control over our wildcard placement:
    ```
    List<Movie> findByDirectorNotLike(String director);

    List<Movie> results = movieRepository.findByDirectorNotLike("An%");
    assertEquals(5, results.size());
    ```
    We can use NotLike in a similar way to accomplish a Not combined with the EndsWith kind of functionality.


Using @Query

: Sometimes we need to create queries that are too complicated for Query Methods or would result in absurdly long method names. In those cases, we can use the @Query annotation to query our database.

1. Named Parameters
    ```
    @Query("SELECT m FROM Movie m WHERE m.title LIKE %:title%")
    List<Movie> searchByTitleLike(@Param("title") String title);
    ```
    @Param annotation is important here because we're using a named parameter.

2. Ordered Parameters
    ```
    @Query("SELECT m FROM Movie m WHERE m.rating LIKE ?1%")
    List<Movie> searchByRatingStartsWith(String rating);
    ```



    





