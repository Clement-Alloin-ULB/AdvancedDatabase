# Advanced Databases 

Authors : Alloin Clément 573143 ,Fernandes do Rosario Tiago 502627 , Laravine Noah  ,Diximier François

## PostgreSQL 

## Cassandra 

### Run Cassandra

Cassandra **3.11.16** (latest version working on Windows) (https://cassandra.apache.org/_/download.html)  
with Python **2.7** (https://www.python.org/downloads/release/python-2718/)  
and JDK **8**  (https://www.oracle.com/java/technologies/downloads/#java8)  

```bash
#Launch Cassandra
cassandra

#To query Cassandra in terminal
cqlsh
```

### Execute the queries

#### Insert
In a new terminal ($PATH to update)

```bash
#For 1k insert
cassandra-stress user profile=$PATH n=1000 ops(insert=1) no-warmup -rate threads=512
#For 10k insert
cassandra-stress user profile=$PATH n=10000 ops(insert=1) no-warmup -rate threads=512
#For 100k insert
cassandra-stress user profile=$PATH n=100000 ops(insert=1) no-warmup -rate threads=512
```

This will create a new Keyspace called stress_test with one column family and populate it with X rows.

#### Delete

With Cqlsh or RazorSQL
```bash
#cqlsh , enable tracing to view time elapse
tracing on ;
Truncate stress_test.ratings ;
#RazorSql
Truncate ratings ;
```

#### Select

To populate the database with real data to do the select we need the data.csv.  
We used a csv containing 25M rows to populate the cassandra database but it is too big to upload it on gitHub.  
We only included one with 250k rows .  

```bash
#In cqlsh
#25K Rows
copy stress_test.ratings (rating_id,user_id,movie_id,rating,timestamp,title,genre_id,genre_name) from './data.csv' WITH HEADER = TRUE AND MAXROWS=25000; 
#250K Rows
copy stress_test.ratings (rating_id,user_id,movie_id,rating,timestamp,title,genre_id,genre_name) from './data.csv' WITH HEADER = TRUE AND MAXROWS=250000; 
#25M Rows
#File for this one not on github
copy stress_test.ratings (rating_id,user_id,movie_id,rating,timestamp,title,genre_id,genre_name) from './data.csv' WITH HEADER = TRUE; 
```

With RazorSQL
```sql
Select title from ratings where genre_name = 'Thriller' AND rating >= 4 ALLOW FILTERING;
```

#### Means Calculations

With RazorSQL
```sql
SELECT avg(rating) from ratings where genre_name = 'Comedy' ALLOW FILTERING;
```

#### Update

 / (Explained in the repport)


## HBase