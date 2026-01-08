# Load Balancer Algorithms 

Main Resource: https://www.youtube.com/watch?v=dBmxNsS3BGE

# Static Load Balancing Algorithms 
These algorithms expect a fixed number of servers. 

<br>


## Round Robin 
[Alternative resource link](https://www.youtube.com/watch?v=VaqHjAcHXZQ)
- Simple Algorithm: For each request, store requests in a queue and distribute them amoung X servers sequentially. 

Pseudo code example: 
```
servers = ["A", "B", "C"] 
count   = 0 

while queue:  
    servers[idx] = queue.pop()  

    if count == len(server) - 1: 
        count = 0 
    else 
        count += 1 

# Ex) 5 Msgs would send to: 'A', 'B', 'C', 'A', 'B' 
```
### Pros
- Simple

### Cons
- Can't account for an overloaded server, or can overload if servers are not monitored

### Alternative Round Robins
- **Stick Round Robin**:    Put related data on the same server 
- **Weighted Round Robin**: Assign a weight (priority) to different servers. Good if servers have variable capabilities. 

<br>

## IP/URL Hash
Take hash or IP or URL to determine request endpoint. Adds randomness. 

<br> 

---

# Dynamic Algorithms 
Take active performance metrics and use them to make decisions.


<br>

## Least Connections 
- Monitor the least number of connections and send requests there

### Pros: 
- Dynamic :D 

### Cons: 
- Easy to reroute requests all to one server 

<br>

## Least Time 
Check the server with the smallest latency and use that server 

### Pros: 
- Very accurate 

### Cons: 
- Lots of over head 