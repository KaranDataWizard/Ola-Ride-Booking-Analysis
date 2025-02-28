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
    | Metric        | Value      |
|--------------|-----------|
| Total Revenue | 22,182,680 |

    
# Q.3 Which payment method is most preferred?

select 
Payment_Method,count(*) User_count from ola 
where Payment_Method is not null 
group by 1  
order by 2 desc;
 | Payment Method | User Count |
|---------------|------------|
| Cash          | 13,708     |
| UPI           | 10,289     |
| Credit Card   | 951        |
| Debit Card    | 259        |

# Q.4 What is the number of cancellations by customers vs. drivers?
SELECT 
    COUNT(Canceled_Rides_by_Customer) Customers_cancellention,
    COUNT(Canceled_Rides_by_Driver) Drivers_cancellention
FROM
    ola; 
    | Customer Cancellations | Driver Cancellations |
|------------------------|----------------------|
| 4,079                  | 7,212                |


# Q.5 What is the average ride distance and fare per vehicle type?
Select Vehicle_Type, 
round(avg(Ride_Distance),2) as Avg_Distance,
round(avg(booking_value),2) as Avg_Fare from ola
group by 1
order by 3 desc;
| Vehicle Type  | Avg Distance (km) | Avg Fare (₹) |
|--------------|------------------|-------------|
| Prime Sedan  | 15.66            | 564.78      |
| Prime Plus   | 15.22            | 547.28      |
| Mini         | 15.50            | 546.54      |
| eBike        | 15.74            | 546.11      |
| Bike         | 15.88            | 544.54      |
| Auto         | 6.21             | 540.94      |
| Prime SUV    | 15.30            | 540.25      |


# Q.6 Which are the top 5 pickup locations with the highest ride counts?
select Pickup_Location, count(*) Ride_Count from ola
where Booking_Status = "Success" 
group by 1 
order by 2 desc 
limit 5 ;
| Pickup Location    | Ride Count |
|--------------------|-----------|
| Indiranagar       | 549       |
| Banashankari      | 542       |
| Ramamurthy Nagar  | 542       |
| Kammanahalli      | 533       |
| KR Puram         | 532       |


#Q.7 What are the peak booking hours?
SELECT 
    HOUR(time) Peak_Hours, COUNT(*) Ride_count
FROM
    ola
    group by 1
    order by 2 desc
    | Peak Hours | Ride Count |
|------------|-----------|
| 8         | 1789      |
| 9         | 1762      |
| 21        | 1744      |
| 10        | 1734      |
| 0         | 1726      |
| 7         | 1717      |
| 11        | 1707      |
| 13        | 1703      |

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
    | Completed Rides (%) | Incomplete Rides (%) |
|---------------------|----------------------|
| 58.4               | 3.8                  |

# Q.9 What are the average ratings given by customers vs. drivers?
SELECT 
    Vehicle_Type,
    ROUND(AVG(Driver_Ratings), 2) Avg_Driver_Rating,
    ROUND(AVG(Customer_Rating), 2) Avg_Customer_Rating
FROM
    ola
GROUP BY 1
;
| Vehicle Type  | Avg Driver Rating | Avg Customer Rating |
|--------------|------------------|------------------|
| Prime Sedan  | 4.00             | 3.99             |
| Bike        | 3.98             | 3.98             |
| Prime SUV   | 4.01             | 3.99             |
| eBike       | 4.02             | 3.99             |
| Mini        | 3.99             | 4.01             |
| Prime Plus  | 4.01             | 4.00             |
| Auto        | 3.99             | 4.00             |

# Q.10 What is the breakdown of cancellation reasons? 
SELECT 
    Incomplete_Rides_Reason, COUNT(*) Occurances_count
FROM
    ola
WHERE
    Incomplete_Rides_Reason IS NOT NULL
GROUP BY 1
ORDER BY 2 DESC; 
| Incomplete Rides Reason | Occurrences Count |
|-------------------------|-------------------|
| Customer Demand        | 618               |
| Vehicle Breakdown      | 617               |
| Other Issue           | 307               |


# Q.11 Who are the top 5 customers with the most bookings (customer loyalty)?
SELECT 
    Customer_ID, COUNT(*) Customer_loyalty
FROM
    ola
GROUP BY 1
ORDER BY 2 DESC
LIMIT 5;
| Customer ID  | Customer Loyalty |
|-------------|-----------------|
| CID706246   | 3               |
| CID688426   | 3               |
| CID887797   | 3               |
| CID219102   | 3               |
| CID954071   | 3               |


# Q.12 Which drivers have the lowest ratings? 
select Booking_ID as Driver_ID, Driver_Ratings 
from ola
where Driver_Ratings is not null
order by Driver_Ratings asc
;
| Driver ID        | Driver Ratings |
|------------------|---------------|
| CNR5030034044   | 3             |
| CNR3926354992   | 3             |
| CNR8005774170   | 3             |
| CNR3748772929   | 3             |
| CNR4008689887   | 3             |
| CNR1949532700   | 3             |     

# Q.13 What is the average TAT (turnaround time) by vehicle type? 
select Vehicle_Type, 
round(avg(V_TAT) ,2)Avg_Vechicle_TAT,
round(avg(C_TAT), 2) Avg_Customer_TAT
 from ola
 group by 1 ; 
 | Vehicle Type  | Avg Vehicle TAT | Avg Customer TAT |
|--------------|----------------|------------------|
| Prime Sedan  | 170.99         | 84.91           |
| Bike         | 171.35         | 84.68           |
| Prime SUV    | 169.89         | 84.39           |
| eBike        | 169.24         | 85.90           |
| Mini         | 170.89         | 84.52           |
| Prime Plus   | 170.56         | 85.52           |
| Auto         | 173.02         | 85.59           |


# Q.14 Which are the most profitable pickup-drop location pairs? 
SELECT 
    Pickup_Location, Drop_Location, SUM(Booking_Value) Total_Revenue
FROM
    ola
    group by 1,2 
    order by 3 desc
    limit 5; 
    | Pickup Location  | Drop Location             | Total Revenue |
|-----------------|--------------------------|--------------|
| Hulimavu       | Majestic                  | 21150        |
| Hennur         | Padmanabhanagar           | 20359        |
| BTM Layout     | Marathahalli              | 19951        |
| Banashankari   | Rajarajeshwari Nagar      | 19883        |
| Peenya         | Majestic                  | 19714        |

# Q 15 Who are the customers who frequently cancel rides? 
select Customer_ID, count(Canceled_Rides_by_Customer) from ola
where Canceled_Rides_by_Customer is not null
group by Customer_ID
order by 2 desc 
limit 5 ; 
| Customer ID  | Canceled Rides by Customer |
|-------------|--------------------------|
| CID497942   | 2                        |
| CID718782   | 2                        |
| CID548434   | 2                        |
| CID934862   | 2                        |
| CID208386   | 2                        |


# Q.16 What are the peak demand days of the week? 
SELECT 
    DAYNAME(date) Peak_day_demand, COUNT(*)
FROM
    ola
GROUP BY 1
ORDER BY 2 DESC;
| Peak Day   | Ride Count |
|------------|-----------|
| Wednesday  | 6894      |
| Tuesday    | 6742      |
| Thursday   | 5478      |
| Sunday     | 5450      |
| Friday     | 5389      |
| Monday     | 5317      |
| Saturday   | 5269      |


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

| Payment Method | Revenue  | Revenue Percentage |
|---------------|---------|--------------------|
| Cash         | 7,540,582  | 33.99%             |
| UPI          | 5,583,785  | 25.17%             |
| Credit Card  | 496,718    | 2.24%              |
| Debit Card   | 141,392    | 0.64%              |

# Q.18 What are the longest and shortest rides by distance?

(select 'Longest_ride' as Type, Booking_Id, Ride_Distance from ola
order by Ride_Distance desc limit 1) 
union all 
(select 'Shortest_ride' as Type, Booking_Id, Ride_Distance from ola
where Ride_Distance >0
order by Ride_Distance asc limit 1) ;
| Type            | Booking ID      | Ride Distance (km) |
|----------------|----------------|--------------------|
| Longest Ride   | CNR3612067560   | 49                 |
| Shortest Ride  | CNR3800597072   | 1                  |


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
| City              | Best Rating |
|------------------|------------|
| Sahakar Nagar    | 5          |
| Ramamurthy Nagar | 3          |



 
