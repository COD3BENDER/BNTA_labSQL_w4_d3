# Football Matches - Tasks

Each of the questions/tasks below can be answered using a `SELECT` query. When you find a solution copy it into the code block under the question before pushing your solution to GitHub.

1) Find all the matches from 2017.

```sql

SELECT * FROM matches WHERE season = 2017 


```

2) Find all the matches featuring Barcelona.

```sql

SELECT * FROM matches Where hometeam LIKE 'Barcelona' OR awayteam LIKE 'Barcelona'; 


```

3) What are the names of the Scottish divisions included?

```sql

SELECT name FROM divisions WHERE country LIKE 'Scotland'


```

4) Find the value of the `code` for the `Bundesliga` division. Use that code to find out how many matches Freiburg have played in that division. HINT: You will need to query both tables

```sql

SELECT COUNT(*) FROM(SELECT * FROM matches WHERE division_code LIKE (SELECT code FROM divisions WHERE name LIKE 'Bundesliga') INTERSECT (SELECT * FROM matches WHERE hometeam LIKE 'Freiburg' Or awayteam LIKE 'Freiburg')) I 

<!-- Saw online that you need the I to indicate the derived table otherwise SQL will show Syntax Error -->


```

5) Find the teams which include the word "City" in their name. 

```sql

SELECT DISTINCT hometeam from matches WHERE hometeam LIKE ('%City%') INTERSECT SELECT DISTINCT awayteam from matches WHERE awayteam LIKE ('%City%') 


```

6) How many different teams have played in matches recorded in a French division?

```sql

SELECT COUNT(*) FROM (SELECT DISTINCT matches.hometeam FROM divisions JOIN matches ON divisions.code=matches.division_code AND divisions.country = 'France') I


```

7) Have Huddersfield played Swansea in any of the recorded matches?

```sql
SELECT
    CASE WHEN EXISTS 
    (
        SELECT id from matches WHERE hometeam LIKE 'Huddersfield' AND awayteam LIKE 'Swansea' OR awayteam LIKE 'Huddersfield' AND hometeam LIKE 'Swansea'
    )
    THEN 'TRUE'
    ELSE 'FALSE'
END



```

8) How many draws were there in the `Eredivisie` between 2010 and 2015?

```sql
<!-- Copy solution here -->
SELECT COUNT(id) FROM matches WHERE division_code = 'N1' AND season BETWEEN 2010 AND 2015 AND ftr = 'D'

```

9) Select the matches played in the Premier League in order of total goals scored from highest to lowest. When two matches have the same total the match with more home goals should come first.

```sql
<!-- Copy solution here -->
SELECT * FROM matches WHERE division_code = 'E0' ORDER BY (fthg + ftag) DESC, fthg DESC

```

10) In which division and which season were the most goals scored?

```sql
<!-- Copy solution here -->


```

### Useful Resources

- [Filtering results](https://www.w3schools.com/sql/sql_where.asp)
- [Ordering results](https://www.w3schools.com/sql/sql_orderby.asp)
- [Grouping results](https://www.w3schools.com/sql/sql_groupby.asp)