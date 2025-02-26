<div align="center">

  # **End-to-End Data Analyst Project: Ola Ride Booking Analysis**


</div>

## Table of Contents
1. [Situation](#situation)
2. [Task](#task)
3. [Action](#action)
   - [Data Preparation](#data-preparation)
   - [Database Creation and Querying](#database-creation-and-querying)
   - [Data Visualization](#data-visualization)
4. [Result](#result)
5. [Key Metrics and Visuals](#key-metrics-and-visuals)
6. [Recommendations](#recommendations)
7. [Conclusion](#conclusion)

## Situation
Ola, as a leading ride-hailing service, handles a vast amount of ride booking data daily. The challenge was to analyze this data to uncover trends, identify inefficiencies, and provide actionable recommendations.

## Task
As the data analyst on this project, my task was to:
1. Clean and prepare the data for analysis.
2. Perform in-depth analysis using SQL queries to extract meaningful insights.
3. Create interactive dashboards in Power BI to visualize the findings.
4. Provide actionable recommendations based on the data.

## Action
### Data Preparation
- Cleaned raw data in **MS Excel**, removed duplicates, handled missing values, and ensured consistency in formatting (e.g., dates, times, and currency).
- Ensured the accuracy and reliability of the analysis.

### Database Creation and Querying
- Created a MySQL database named `Ola_booking` and imported the cleaned dataset.
- Used SQL to answer key business questions, such as:
  - **Total Rides and Revenue**: Identified that Ola completed **40.54K rides**, generating **22M in revenue**.
  - **Payment Methods**: Discovered that **cash** is the most preferred payment method among customers.
  - **Cancellations**: Found that **10.06% of rides were canceled by drivers**, while **17.79% were canceled by customers**.
  - **Top Vehicle Types**: Sedan and Bike emerged as the top vehicle types by ride distance.
  - **Customer Ratings**: The average customer rating across all rides was **2.48**.
  - **Peak Booking Hours**: Identified the busiest hours of the day for ride bookings.
  - **Top Customers**: Highlighted the top 5 loyal customers based on booking frequency.

### Data Visualization
- Created an interactive **Power BI dashboard** to visualize the insights. The dashboard includes:
  - **Ride Volume Over Time**: A line chart showing trends in ride bookings.
  - **Booking Status Breakdown**: A pie chart displaying the distribution of successful and canceled rides.
  - **Top 5 Vehicle Types by Ride Distance**: A bar chart highlighting the most used vehicle types.
  - **Cancellation Reasons**: A bar chart showing the primary reasons for ride cancellations.
  - **Revenue by Payment Method**: A pie chart illustrating revenue distribution across payment methods.
  - **Customer vs. Driver Ratings**: A scatter plot comparing customer and driver ratings.

## Result
The analysis provided several actionable insights:
1. **Operational Efficiency**:
   - Identified peak booking hours and days, allowing Ola to optimize driver availability to meet demand.
   - Found cancellation reasons (e.g., driver unavailability, change of plans) to help reduce cancellations and improve customer satisfaction.

2. **Revenue Growth**:
   - Identified the most profitable pickup-drop location pairs, allowing Ola to focus on high-revenue routes.
   - Insights into payment methods can help Ola promote less popular methods (e.g., UPI, credit cards) to diversify revenue streams.

3. **Customer Experience**:
   - Analyzed customer ratings and feedback to address issues like driver behavior, vehicle conditions, and ride comfort.
   - Suggested loyalty programs for top customers to enhance retention.

4. **Driver Performance**:
   - Identified drivers with low ratings, enabling targeted training programs to improve service quality.
   - Calculated average turnaround times by vehicle type, helping optimize fleet management.

## Key Metrics and Visuals
- **Total Rides**: 40.54K
- **Total Revenue**: 22M
- **Top Vehicle Types**: Sedan and Bike
- **Average Customer Rating**: 2.48
- **Cancellation Rates**: 10.06% (drivers), 17.79% (customers)

<div align="center">

## Recommendations
Based on the analysis, I recommend the following actions:

- **Optimize Driver Allocation**: Focus on peak hours and high-demand areas to reduce wait times and cancellations.
- **Improve Customer Ratings**: Address common complaints (e.g., AC issues, driver behavior) to enhance customer satisfaction.
- **Promote Digital Payments**: Encourage the use of UPI and credit cards to reduce reliance on cash payments.
- **Reward Loyal Customers**: Implement loyalty programs for top customers to increase retention and repeat bookings.
- **Enhance Driver Training**: Provide targeted training for low-rated drivers to improve service quality.

## Conclusion
This project has provided a comprehensive understanding of Ola's ride booking operations. The insights and recommendations derived from the data will help Ola optimize its services, improve customer satisfaction, and drive revenue growth.

Thank you for your time and attention.

</div>
