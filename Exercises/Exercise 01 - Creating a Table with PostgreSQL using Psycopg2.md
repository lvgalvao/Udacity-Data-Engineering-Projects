# Lesson 1 Exercise 1: Creating a Table with PostgreSQL
# 

<img src="https://www.ovhcloud.com/sites/default/files/styles/text_media_horizontal/public/2021-09/ECX-1909_Hero_PostgreSQL_600x400%402x.png" width="730">


```python
import psycopg2
```


```python
try: 
    conn = psycopg2.connect("host=127.0.0.1 dbname=lucianogalvao user=lucianogalvao password=u65hfgo9")
except psycopg2.Error as e: 
    print("Error: Could not make connection to the Postgres database")
    print(e)
```


```python
try: 
    cur = conn.cursor()
except psycopg2.Error as e: 
    print("Error: Could not get curser to the Database")
    print(e)
```


```python
conn.set_session(autocommit=True)
```


```python
try: 
    cur.execute("create database dbgalderma")
except psycopg2.Error as e:
    print(e)
```


```python
try: 
    conn.close()
except psycopg2.Error as e:
    print(e)
    
try: 
    conn = psycopg2.connect("host=127.0.0.1 dbname=dbgalderma user=lucianogalvao password=u65hfgo9")
except psycopg2.Error as e: 
    print("Error: Could not make connection to the Postgres database")
    print(e)
    
try: 
    cur = conn.cursor()
except psycopg2.Error as e: 
    print("Error: Could not get curser to the Database")
    print(e)

conn.set_session(autocommit=True)
```

### Create a Song Library that contains a list of songs, including the song name, artist name, year, album it was from, and if it was a single. 

`song_title
artist_name
year
album_name
single`


```python
try: 
    cur.execute("CREATE TABLE song_title (id serial PRIMARY KEY, artist_name varchar, year integer, album_name varchar, single varchar);")
except psycopg2.Error as e: 
    print("Error: Issue creating table")
    print (e)
```

### TO-DO: Insert the following row in the table
`First Row:  "Across The Universe", "The Beatles", "1970", "False", "Let It Be"`


```python
try: 
    cur.execute("INSERT INTO song_title (artist_name, year, album_name, single) \
    VALUES (%s, %s, %s, %s) RETURNING id", \
                ("The Beatles", "1970", "Across The Universe", "Let It Be"))
except psycopg2.Error as e: 
    print("Error: Issue creating rows")
    print (e)
```

### TO-DO: Change the Table name to Song Library


```python
try: 
    cur.execute("ALTER TABLE song_title RENAME TO song_library;")
except psycopg2.Error as e: 
    print("Error: Issue rename the table")
    print (e)
```

### TO-DO: Create a new column to Song Library named song_title


```python
try: 
    cur.execute("ALTER TABLE song_library ADD song_title varchar;")
except psycopg2.Error as e: 
    print("Error: Issue rename the table")
    print (e)
```

    Error: Issue rename the table
    column "song_title" of relation "song_library" already exists
    


### TO-DO: Add the information  a new column to Song Library named song_title


```python
try: 
    cur.execute("UPDATE song_library SET single = False, song_title = 'Let it be' WHERE id = 1")
except psycopg2.Error as e: 
    print("Error: Issue updating the table")
    print (e)
```

### TO-DO: Insert the following row in the table

`Second Row: "The Beatles", "Think For Yourself", "False", "1965", "Rubber Soul"`


```python
try: 
    cur.execute("INSERT INTO song_library (song_title, artist_name, year, album_name, single) \
    VALUES (%s, %s, %s, %s, %s) RETURNING id", \
                ("Think For Yourself", "The Beatles", "1970", "Rubber Soul", "False"))
except psycopg2.Error as e: 
    print("Error: Issue creating rows")
    print (e)
```

### TO-DO: Validate your data was inserted into the table. 


```python
## TO-DO: Finish the SELECT * Statement 
try: 
    cur.execute("SELECT * FROM song_library;")
except psycopg2.Error as e: 
    print("Error: select *")
    print (e)

row = cur.fetchone()
while row:
   print(row)
   row = cur.fetchone()
```

    (1, 'The Beatles', 1970, 'Across The Universe', 'false', 'Let it be')
    (2, 'The Beatles', 1970, 'Rubber Soul', 'False', 'Think For Yourself')



```python

```
