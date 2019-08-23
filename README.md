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
