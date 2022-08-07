# Lesson 1 Exercise 1: Creating a Table with PostgreSQL
# 

<img src="https://www.ovhcloud.com/sites/default/files/styles/text_media_horizontal/public/2021-09/ECX-1909_Hero_PostgreSQL_600x400%402x.png" width="730">

### Walk through the basics of PostgreSQL. You will need to complete the following tasks: 
<br>
<li>Create a table in PostgreSQL, <li> Insert rows of data <li> Run a simple SQL query to validate the information. <br>

#### Import the library 


```python
import psycopg2
```

#### Create a connection to the database


```python
try: 
    conn = psycopg2.connect("**params")
except psycopg2.Error as e: 
    print("Error: Could not make connection to the Postgres database")
    print(e)
```

#### Use the connection to get a cursor that can be used to execute queries.


```python
try: 
    cur = conn.cursor()
except psycopg2.Error as e: 
    print("Error: Could not get curser to the Database")
    print(e)
```

#### TO-DO: Set automatic commit to be true so that each action is committed without having to call conn.commit() after each command. 


```python
conn.set_session(autocommit=True)
```

#### TO-DO: Create a database to do the work in. 


```python
try: 
    cur.execute("create database dbmusic")
except psycopg2.Error as e:
    print(e)
```

#### TO-DO: Add the database name in the connect statement. Let's close our connection to the default database, reconnect to the new database, and get a new cursor.


```python
try: 
    conn.close()
except psycopg2.Error as e:
    print(e)
    
try: 
    conn = psycopg2.connect("**params")
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

#### TO-DO Create a Song Library that contains a list of songs, including the song name, artist name, year, album it was from, and if it was a single. 

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

#### TO-DO: Insert the following row in the table
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

#### ISSUE: I miss the requirements, so was necessesary rename the table, add a new column and add the miss information


```python
try: 
    cur.execute("ALTER TABLE song_title RENAME TO song_library;")
except psycopg2.Error as e: 
    print("Error: Issue rename the table")
    print (e)
```

#### ISSUE: Create a new column to Song Library named song_title


```python
try: 
    cur.execute("ALTER TABLE song_library ADD song_title varchar;")
except psycopg2.Error as e: 
    print("Error: Issue rename the table")
    print (e)
```

    Error: Issue rename the table
    column "song_title" of relation "song_library" already exists
    


#### ISSUE: Add the information  a new column to Song Library named song_title


```python
try: 
    cur.execute("UPDATE song_library SET single = False, song_title = 'Let it be' WHERE id = 1")
except psycopg2.Error as e: 
    print("Error: Issue updating the table")
    print (e)
```

#### TO-DO: Insert the following row in the table

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

#### TO-DO: Validate your data was inserted into the table. 


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

