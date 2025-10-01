# PROJECT TITLE: OLA RIDE INSIGHTS

# AIM: “To analyze OLA’s ride-sharing data using SQL, Power BI, and Streamlit in order to extract actionable insights that enhance operational efficiency, improve customer satisfaction, and optimize business strategies through interactive dashboards and applications.”

# ANALYSIS BY POWER BI:
<img width="1052" height="592" alt="OLA" src="https://github.com/user-attachments/assets/55712ce0-2280-45eb-b62f-a45b129e3c83" />

# ANALYSIS BY SQL QUERY:
-- QUERY SOLVING

-- 1: Retrieve all successful bookings:
SELECT * FROM ola 
WHERE Booking_Status='Success';

-- 2: Find the average ride distance for each vehicle type:
SELECT Vehicle_Type,ROUND(AVG(Ride_Distance),2) AS Average_Ride_Distance 
FROM ola
GROUP BY Vehicle_Type
ORDER BY avg(Ride_Distance) DESC;

-- 3: Total number of cancelled rides by customers
SELECT Booking_Status,COUNT(Booking_Status) AS Total_Ride_Cancel
FROM ola
GROUP BY Booking_Status
HAVING Booking_Status='Canceled by Customer';

-- 4: The top 5 customers who booked the highest number of rides
SELECT Customer_ID,COUNT('Booking_Status') as Highest_Number_Of_Ride
FROM ola
WHERE Booking_Status='Success'
GROUP BY Customer_ID
ORDER BY COUNT('Booking_Status') DESC
LIMIT 5;

-- 5:The number of rides cancelled by drivers due to personal and car-related issues:
SELECT Canceled_Rides_by_Driver AS Reason,count(*) as Number_Of_Ride_Driver_Cancel
FROM ola
GROUP BY Canceled_Rides_by_Driver
HAVING Canceled_Rides_by_Driver ='Personal & Car related issue';

-- 6: Maximum and minimum driver ratings for Prime Sedan bookings:
SELECT Vehicle_Type,MAX(Driver_Ratings) AS Max_Rating,MIN(Driver_Ratings) AS Min_Rating
FROM ola
GROUP BY Vehicle_Type
HAVING Vehicle_Type='Prime Sedan';

-- 7: Retrieve all rides where payment was made using UPI:
SELECT * FROM ola
WHERE Payment_Method='UPI';

-- 8: Find the average customer rating per vehicle type:
SELECT Vehicle_Type,ROUND(AVG(Customer_Rating),2) AS Average_Customer_Rating
FROM ola
GROUP BY Vehicle_Type;

-- 9: Calculate the total booking value of rides completed successfully:
SELECT Booking_Status,SUM(Booking_Value) AS Total_Booking
FROM ola
WHERE Booking_Status='Success'
GROUP BY Booking_Status;

-- 10: List all incomplete rides along with the reason
SELECT Incomplete_Rides,Incomplete_Rides_Reason
FROM ola
WHERE Incomplete_Rides='Yes';
