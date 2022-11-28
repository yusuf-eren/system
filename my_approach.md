# Real World Metrics
First of all, I assume that we have 12 hours availability and %30 of the users are parking from 8.45 am to 5 pm
because they are parking their cars while working. So we should handle the first 3 hours of starting of our application.
The %70 of the users are parking for visiting, hanging or any other reason.
This is not a usable data for 20 parking lots because system is not complex and scalable. But in many case, The usage data is important.

# Database - Cache
We can use SQL database for these operations. Because our application is not going to scale much and it will be mostly write-update only. We should use NOSQL if we are going to scale
our app to multiple parking companies and if it will continue to extend. Because SQL databases are vertically scaled. That means our application will spend more money
on systems. We can scale our application horizontally for reducing costs.

-Our application will be mostly write-update only for our database. We are not going to read data frequently.
Because all active operations are happening in a single day. Every single day is a new operation of writing data. So, cache daily data on redis and remove at the end of the process.

So the solution is;
-The most important point is we are not going to fetch all data from database. Because we don't need older records any time.
We are just writing data into db for security, reporting, analyzing, etc. We just need empty and filled parking lots.
So when we get a new operation we can write it into the db and at the same time we cache it on redis.
At the exit, We should follow these processess

1. Get data from cache
2. find data in the db and update the status of the data
3. remove from cache

-One more problem is increasing data in db each day. We can shard our databases to little chunks for managing data.

# Fee Calculation
The cars are paying the fee at exit. We should report (current time) - (enter time).

# Planning
My thoughts are finished here. Now I'm going to create a Database Schema with System Design. Finally, I will create API Schema.

# My questions before starting
My questions before starting(Answered)
1) Will this application scale at any point? Will it include just 20 parking lots?
2) Can cars stay in a lot after 7pm? So is there any limits to stay in a lot?
3) as I understand, users can not reserve any parking lot without entering the parking gate. Is that right?