# Partition vs Sharding 

Let's take an example where a database is created that contains many global users. 
For our use case, let's say we need to query by country for the fastest results, how should we design out db? 

## Partition
Idea that, within a database, we seaparate out our data segments by *field*, in this case by country. There are a few different ways to do this. 

### Horizontal Partitioning
Parition across different tables or databases within a database server. 

---
**Table 1 or DB 1**

| User    | Country |
| ----    | ------- |  
| Robert  | USA     | 
| Ethan   | USA     | 

---
**Table 2 or DB 2**

| User    | Country |
| ----    | ------- |  
| Akash   | India   | 
| Adi     | India   | 
---

### Verticial Partitioning 
Makes no sense to me, but this is just partitioning under the same table. 

| User    | Country |
| ----    | ------- |  
| Robert  | USA     | 
| Akash   | India   | 
| Ethan   | USA     | 
| Adi     | India   | 

## Sharding 
Same thing as horizontal partitioning, but with different database servers (instead of different databases or tables on the same server).
- Use this to reduce database connection limits



