# Mod2 Week3 Assessment

## Setup
1. Fork this repository.
1. You can either work on your clone in GitHub, or open your clone in visual studio.

## Questions (10 Points Possible)

<img alt="erd_for_assessment" src="https://github.com/modelmapper/modelmapper/assets/11747682/60bebb3c-9faa-4f3e-ae0a-7df7dde06784">

[Citation for ERD](https://circle.visual-paradigm.com/hospital/)
1. Use the Doctors Office ERD above to answer the following questions:
    1. How many patients can each doctor have? any number, one to many relationship between doctor to patients, so one doctor's dss can be linked to multiple patients
    1. How many doctors can each patient have? 1
    1. How would you describe the relationship between patients and tests? Be sure to use either one-to-one, one-to-many, or many-to-many in your answer. One-To-Many, There can be multiple tests linked to a single patient.
    1. What are the foreign keys in this diagram? test.DoctorDSS, test.PatientSS, Patient.DoctorDSS
    1. What is the primary key for the Tests table. ID
    1. What query would return the number of doctors who have a specialization in "pediatrics"? 
        \nSELECT COUNT(DSS) 
        FROM Doctor 
        Where Specialization = 'pediatrics';

<br>

2. What does a join table do? Why would we need one? A join table allows multiple tables information to be displayed based on relevant information between the two. You would need one when you need to combine two different tables into one single table.
3. What is a question that the following query helps answer?
Count the number of artists from each hometown.
Example return might be 
Loveland - 30
Fort Collins - 7
Denver - 142
```SQL
SELECT hometown, COUNT(name) FROM artists
GROUP BY hometown;
```

4. I'm trying to write a query to find the average age of all patients, but it's not working. How would you modify this query to get it to work as expected?
SELECT AVERAGE(age) AS "avg_patient_age"
FROM patients;
```SQL
SELECT age FROM AVERAGE(patients);
```
5. How would you describe the difference between a `LEFT JOIN` and an `INNER JOIN`
 An inner join will only show data where both tables have that common data. A left join will show all data of the table to the left of the join and show just the data from the right table where it has common data.
## Exercise (10 Points Possible)

Follow these steps to setup the assessment:
1. Create a new database named `flight_db` using pgAdmin.
2. Copy [this script](https://launch.turing.edu/module2/assessments/flight_db.txt) and paste it into the query tool to insert records into your database.
3. Run the following `SELECT` queries individually to get an understanding of the data:
> `SELECT * FROM airlines;`
> `SELECT * FROM flights;`

** If you need help setting up the database, reach out to an instructor! **

Please provide the QUERY (not the answer) that returns each of the following:
1. The flight numbers for all delayed flights (i.e. not on time).
SELECT flight_number
FROM flights
WHERE on_time = false;
3. The count of delayed flights.
SELECT COUNT(id) AS "Delayed_Flights"
FROM flights
WHERE on_time = false;
5. The sum of prices for all flights arriving to Raleigh-Durham (`RDU`).
SELECT SUM(price) AS "totalPrice_raleighFlights"
FROM flights
WHERE arrive_city = 'RDU';
7. The average price for all flights in the database.
SELECT ROUND(AVG(price),2) AS "avg_price"
FROM flights;
9. The average price for all flights arriving to Raleigh-Durham.
SELECT ROUND(AVG(price),2) AS "avg_price"
FROM flights
WHERE arrive_city = 'RDU';
11. The departure city and number of flights departing from each city.
SELECT depart_city, COUNT(id) AS "num_departures"
FROM flights
GROUP BY depart_city;
13. The count of airlines in the database.
SELECT COUNT(id) AS "num_airlines"
FROM airlines;
15. The count of flights in the database.
SELECT COUNT(id) AS "num_flights"
FROM flights;
17. The flight number, departure city, arrival city, price, and airline name of each flight. Do not return the airline ID number.
SELECT flight_number, depart_city, arrive_city, price, airlines.airline_name
FROM flights JOIN airlines
ON flights.airline_id = airlines.id;
19. The airline name, flight number, and price of each flight on the Delta airline. (Assume that you do not know the ID number of the Delta airline. In a larger database, you would be expected to memorize ID numbers).
SELECT airlines.airline_name, flights.flight_number, flights.price
FROM airlines JOIN flights
ON airlines.id = flights.airline_id
WHERE airlines.airline_name = 'Delta';
## Submission

Submit the Assessment Submission form linked in your cohort slack channel!

## Rubric

This assessment has a total of 20 Points. Earning 14 or more points is a pass and will indicate that you are progressing well with the material.

As a reminder, this assessment is for students and instructors to determine if there are any areas that need additional reinforcement!
