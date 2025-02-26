create database Ola_booking;
use ola_booking;

# Q.1 What is the total number of rides?
SELECT 
    COUNT(*) Total_rides
FROM
    ola;

| Metric      | Value  |
|------------|--------|
| Total Rides | 40,539 |

# Q.2 What is the total revenue generated?

SELECT 
    SUM(booking_value) AS Total_Revenue
FROM
    ola;
    
# Q.3 Which payment method is most preferred?

select Payment_Method,count(*) User_count from ola # Cash payment method is most preferred
where Payment_Method is not null 
group by 1  
order by 2 desc;
 
# Q.4 What is the number of cancellations by customers vs. drivers?
SELECT 
    COUNT(Canceled_Rides_by_Customer) Customers_cancellention,
    COUNT(Canceled_Rides_by_Driver) Drivers_cancellention
FROM
    ola; 

# Q.5 What is the average ride distance and fare per vehicle type?
Select Vehicle_Type, 
round(avg(Ride_Distance),2) as Avg_Distance,
round(avg(booking_value),2) as Avg_Fare from ola
group by 1
order by 3 desc;

# Q.6 Which are the top 5 pickup locations with the highest ride counts?
select Pickup_Location, count(*) Ride_Count from ola
where Booking_Status = "Success" 
group by 1 
order by 2 desc 
limit 5 ;

#Q.7 What are the peak booking hours?
SELECT 
    HOUR(time) Peak_Hours, COUNT(*) Ride_count
FROM
    ola
    group by 1
    order by 2 desc
    ;
# Q.8 What is the percentage of completed vs. incomplete rides? 
SELECT 
    ROUND((SUM(CASE
                WHEN Incomplete_Rides = 'no' THEN 1
                ELSE 0
            END) / COUNT(*)) * 100,
            1) AS Completed_Rides,
    ROUND((SUM(CASE
                WHEN incomplete_rides = 'yes' THEN 1
                ELSE 0
            END) / COUNT(*)) * 100,
            1) AS Incomplete_Rides
FROM
    ola; 
# Q.9 What are the average ratings given by customers vs. drivers?
SELECT 
    Vehicle_Type,
    ROUND(AVG(Driver_Ratings), 2) Avg_Driver_Rating,
    ROUND(AVG(Customer_Rating), 2) Avg_Customer_Rating
FROM
    ola
GROUP BY 1
;

# Q.10 What is the breakdown of cancellation reasons? 
SELECT 
    Incomplete_Rides_Reason, COUNT(*) Occurances_count
FROM
    ola
WHERE
    Incomplete_Rides_Reason IS NOT NULL
GROUP BY 1
ORDER BY 2 DESC; 

# Q.12 Who are the top 5 customers with the most bookings (customer loyalty)?
SELECT 
    Customer_ID, COUNT(*) Customer_loyalty
FROM
    ola
GROUP BY 1
ORDER BY 2 DESC
LIMIT 5;

# Q.13 Which drivers have the lowest ratings? 
select Booking_ID as Driver_ID, Driver_Ratings 
from ola
where Driver_Ratings is not null
order by Driver_Ratings asc
;

# Q.13 What is the average TAT (turnaround time) by vehicle type? 
select Vehicle_Type, 
round(avg(V_TAT) ,2)Avg_Vechicle_TAT,
round(avg(C_TAT), 2) Avg_Customer_TAT
 from ola
 group by 1 ; 
# Q.14 Which are the most profitable pickup-drop location pairs? 
SELECT 
    Pickup_Location, Drop_Location, SUM(Booking_Value) Total_Revenue
FROM
    ola
    group by 1,2 
    order by 3 desc
    limit 5; 
# Q 15 Who are the customers who frequently cancel rides? 
select Customer_ID, count(Canceled_Rides_by_Customer) from ola
where Canceled_Rides_by_Customer is not null
group by Customer_ID
order by 2 desc 
limit 5 ; 

# Q.16 What are the peak demand days of the week? 
SELECT 
    DAYNAME(date) Peak_day_demand, COUNT(*)
FROM
    ola
GROUP BY 1
ORDER BY 2 DESC;

# Q.17 What is the revenue contribution by payment method?
SELECT 
    Payment_Method,
    SUM(Booking_Value) Revenue,
    ROUND((SUM(booking_value) / (SELECT 
                    SUM(booking_value)
                FROM
                    ola) * 100),
            2) AS Revenue_Percentage
FROM
    ola
WHERE
    Booking_Status = 'success'
GROUP BY 1
; 
# Q.18 What are the longest and shortest rides by distance?

(select 'Longest_ride' as Type, Booking_Id, Ride_Distance from ola
order by Ride_Distance desc limit 1) 
union all 
(select 'Shortest_ride' as Type, Booking_Id, Ride_Distance from ola
where Ride_Distance >0
order by Ride_Distance asc limit 1) ;

#Q 19 In which cities do customers give the best and worst ratings?
(SELECT 
    Pickup_Location City, Customer_Rating Best_Rating
FROM
    ola
GROUP BY 1 , 2
ORDER BY 2 DESC
LIMIT 1) UNION (SELECT 
    Pickup_Location City, Customer_Rating Best_Rating
FROM
    ola
WHERE
    Customer_Rating IS NOT NULL
GROUP BY 1 , 2
ORDER BY 2 ASC
LIMIT 1)


 
