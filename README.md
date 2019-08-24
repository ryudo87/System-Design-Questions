# Design the Twitter timeline and search
### Use cases
* **User** posts a tweet
    * **Service** pushes tweets to followers, sending push notifications and emails
* **User** views the user timeline (activity from the user)
* **User** views the home timeline (activity from people the user is following)
* **User** searches keywords
* **Service** has high availability

### Constraints and assumptions
#### State assumptions

* 100 million active users
* 500 million tweets per day or 15 billion tweets per month
    * Each tweet averages a fanout of 10 deliveries
    * 5 billion total tweets delivered on fanout per day
    * 150 billion tweets delivered on fanout per month
* 250 billion read requests per month
* 10 billion searches per month

Timeline
* Viewing the timeline should be fast
* Twitter is **more read heavy than write heavy **

Search
* Search is read-heavy


## Step 2: Create a high level design
> Outline a high level design with all important components.
![Imgur](http://i.imgur.com/48tEA2j.png)

## Step 3: Design core components
### Use case: User posts a tweet

We could store the user's own tweets to populate the user timeline  in a [relational database](https://github.com/donnemartin/system-design-primer#relational-database-management-system-rdbms).  

We should discuss the [use cases and tradeoffs between choosing SQL or NoSQL](https://github.com/donnemartin/system-design-primer#sql-or-nosql).

Fanning out tweets to all followers (60 thousand tweets delivered on fanout per second) will **overload a traditional [relational database]**(https://github.com/donnemartin/system-design-primer#relational-database-management-system-rdbms).  

We'll probably want to choose a data store with **fast writes** such as a **NoSQL database** or **Memory Cache**.  
Reading 1 MB sequentially from memory takes about 250 microseconds, 
while reading from SSD takes 4x and from disk takes 80x longer.<sup><a href=https://github.com/donnemartin/system-design-primer#latency-numbers-every-programmer-should-know>1</a></sup>

