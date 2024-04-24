# Railway_Reservation_System


mysql> CREATE DATABASE railway_system;
Query OK, 1 row affected (0.04 sec)

mysql> USE railway_system;
Database changed
mysql> CREATE TABLE user (
    -> user_id INT PRIMARY KEY,
    -> user_name VARCHAR(50),
    -> age INT,
    -> gender VARCHAR(50),
    -> phone VARCHAR(15),
    -> gmail VARCHAR(100),
    -> password VARCHAR(100)
    -> );
Query OK, 0 rows affected (0.06 sec)

mysql> CREATE TABLE passenger (
    -> passenger_id INT PRIMARY KEY,
    -> user_id INT,
    -> FOREIGN KEY(user_id) REFERENCES user(user_id),
    -> ticket_number VARCHAR(20),
    -> seat_number VARCHAR(20)
    -> );
Query OK, 0 rows affected (0.04 sec)

mysql> CREATE TABLE train (
    -> train_id INT PRIMARY KEY,
    -> train_name VARCHAR(100),
    -> departure_time TIME,
    -> arrival_time TIME,
    -> origin VARCHAR(100),
    -> destination VARCHAR(100),
    -> capacity INT
    -> );
Query OK, 0 rows affected (0.05 sec)

mysql> CREATE TABLE station (
    -> station_id INT PRIMARY KEY,
    -> station_name VARCHAR(100),
    -> location VARCHAR(100)
    -> );
Query OK, 0 rows affected (0.04 sec)

mysql> CREATE TABLE ticket (
    -> ticket_id INT PRIMARY KEY,
    -> user_id INT,
    -> train_id INT,
    -> seat_number VARCHAR(20),
    -> FOREIGN KEY(user_id) REFERENCES user(user_id),
    -> FOREIGN KEY(train_id) REFERENCES train(train_id)
    -> );
Query OK, 0 rows affected (0.05 sec)

mysql> CREATE TABLE books (
    -> user_id INT,
    -> ticket_id INT,
    -> PRIMARY KEY (user_id, ticket_id),
    -> FOREIGN KEY (user_id) REFERENCES user(user_id),
    -> FOREIGN KEY (ticket_id) REFERENCES ticket(ticket_id)
    -> );
Query OK, 0 rows affected (0.04 sec)

mysql> CREATE TABLE cancel (
    -> user_id INT,
    -> ticket_id INT,
    -> passenger_id INT,
    -> PRIMARY KEY (user_id, ticket_id, passenger_id),
    -> FOREIGN KEY (user_id) REFERENCES user(user_id),
    -> FOREIGN KEY (ticket_id) REFERENCES ticket(ticket_id),
    -> FOREIGN KEY (passenger_id) REFERENCES passenger(passenger_id)
    -> );
Query OK, 0 rows affected (0.05 sec)

mysql> CREATE TABLE starts (
    -> train_id INT,
    -> station_id INT,
    -> PRIMARY KEY (train_id, station_id),
    -> FOREIGN KEY (train_id) REFERENCES train(train_id),
    -> FOREIGN KEY (station_id) REFERENCES station(station_id)
    -> );
Query OK, 0 rows affected (0.04 sec)

mysql> CREATE TABLE stops (
    -> train_id INT,
    -> station_id INT,
    -> PRIMARY KEY (train_id, station_id),
    -> FOREIGN KEY (train_id) REFERENCES train(train_id),
    -> FOREIGN KEY (station_id) REFERENCES station(station_id)
    -> );
Query OK, 0 rows affected (0.05 sec)

mysql> CREATE TABLE reaches (
    -> train_id INT,
    -> station_id INT,
    -> time TIME,
    -> PRIMARY KEY (train_id, station_id),
    -> FOREIGN KEY (train_id) REFERENCES train(train_id),
    -> FOREIGN KEY (station_id) REFERENCES station(station_id)
    -> );
Query OK, 0 rows affected (0.04 sec)

ALTER COMMAND:

mysql> ALTER TABLE train
    -> CHANGE COLUMN capacity seats_available INT;
Query OK, 0 rows affected (0.06 sec)
Records: 0  Duplicates: 0  Warnings: 0

DROP COMMAND:

mysql> CREATE TABLE train_schedule (
    -> schedule_id INT PRIMARY KEY,
    -> departure_time TIME,
    -> arrival_time TIME
    -> );
Query OK, 0 rows affected (0.04 sec)

mysql> DROP TABLE train_schedule;
Query OK, 0 rows affected (0.03 sec)

TRUNCATE COMMAND:

mysql> TRUNCATE TABLE train_schedule;
Query OK, 0 rows affected (0.04 sec)

INSERT COMMAND:

mysql> INSERT INTO user (user_id, user_name, age, gender, phone, gmail, password)
    -> VALUES
    -> (1, 'Rajesh Sharma', 35, 'Male', '+91-9876543210', 'rajesh.sharma@example.com', 'rajesh@123'),
    -> (2, 'Priya Patel', 28, 'Female', '+91-8765432109', 'priya.patel@example.com', 'priya@456'),
    -> (3, 'Amit Kumar', 40, 'Male', '+91-7654321098', 'amit.kumar@example.com', 'amit@789');
Query OK, 3 rows affected (0.05 sec)
Records: 3  Duplicates: 0  Warnings: 0

mysql> INSERT INTO passenger (passenger_id, user_id, ticket_number, seat_number)
    -> VALUES
    -> (1, 1, 'IND123', 'B12'),
    ->  (2, 2, 'IND124', 'C13'),
    -> (3, 3, 'IND125', 'A14');
Query OK, 3 rows affected (0.02 sec)
Records: 3  Duplicates: 0  Warnings: 0

mysql> INSERT INTO train (train_id, train_name, departure_time, arrival_time, origin, destination, seats_available)
    -> VALUES
    -> (1, 'Rajdhani Express', '09:00:00', '14:00:00', 'New Delhi', 'Mumbai', 200),
    -> (2, 'Shatabdi Express', '10:00:00', '13:00:00', 'Kolkata', 'New Delhi', 150),
    -> (3, 'Duronto Express', '08:30:00', '16:30:00', 'Chennai', 'Bangalore', 180);
Query OK, 3 rows affected (0.03 sec)
Records: 3  Duplicates: 0  Warnings: 0

mysql> INSERT INTO station (station_id, station_name, location)
    -> VALUES
    -> (1, 'New Delhi Railway Station', 'New Delhi'),
    -> (2, 'Mumbai Central', 'Mumbai'),
    -> (3, 'Howrah Junction', 'Kolkata');
Query OK, 3 rows affected (0.02 sec)
Records: 3  Duplicates: 0  Warnings: 0

mysql> INSERT INTO ticket (ticket_id, user_id, train_id, seat_number)
    -> VALUES
    -> (1, 1, 1, 'A1'),
    -> (2, 2, 2, 'B2'),
    -> (3, 3, 3, 'C3');
Query OK, 3 rows affected (0.02 sec)
Records: 3  Duplicates: 0  Warnings: 0

mysql> INSERT INTO books (user_id, ticket_id) VALUES
    -> (1, 1),
    -> (2, 2),
    -> (3, 3);
Query OK, 3 rows affected (0.02 sec)
Records: 3  Duplicates: 0  Warnings: 0

mysql> INSERT INTO cancel (user_id, ticket_id, passenger_id) VALUES
    -> (1, 1, 1),
    -> (2, 2, 2),
    -> (3, 3, 3);
Query OK, 3 rows affected (0.02 sec)
Records: 3  Duplicates: 0  Warnings: 0

mysql> INSERT INTO starts (train_id, station_id) VALUES
    -> (1, 1),
    -> (2, 2),
    -> (3, 3);
Query OK, 3 rows affected (0.02 sec)
Records: 3  Duplicates: 0  Warnings: 0

mysql> INSERT INTO stops (train_id, station_id) VALUES
    -> (1, 1),
    -> (2, 2),
    -> (3, 3);
Query OK, 3 rows affected (0.02 sec)
Records: 3  Duplicates: 0  Warnings: 0

mysql> INSERT INTO reaches (train_id, station_id, time) VALUES
    -> (1, 1, '09:00:00'),
    -> (2, 2, '10:30:00'),
    -> (3, 3, '11:45:00');
Query OK, 3 rows affected (0.02 sec)
Records: 3  Duplicates: 0  Warnings: 0

SELECT COMMAND:

mysql> SELECT * FROM user;
+---------+---------------+------+--------+----------------+---------------------------+------------+
| user_id | user_name     | age  | gender | phone          | gmail                     | password   |
+---------+---------------+------+--------+----------------+---------------------------+------------+
|       1 | Rajesh Sharma |   35 | Male   | +91-9876543210 | rajesh.sharma@example.com | rajesh@123 |
|       2 | Priya Patel   |   28 | Female | +91-8765432109 | priya.patel@example.com   | priya@456  |
|       3 | Amit Kumar    |   40 | Male   | +91-7654321098 | amit.kumar@example.com    | amit@789   |
+---------+---------------+------+--------+----------------+---------------------------+------------+
3 rows in set (0.00 sec)

mysql> SELECT * FROM passenger;
+--------------+---------+---------------+-------------+
| passenger_id | user_id | ticket_number | seat_number |
+--------------+---------+---------------+-------------+
|            1 |       1 | IND123        | B12         |
|            2 |       2 | IND124        | C13         |
|            3 |       3 | IND125        | A14         |
+--------------+---------+---------------+-------------+
3 rows in set (0.01 sec)


DELETE COMMAND :

mysql> DELETE FROM cancel;
Query OK, 3 rows affected (0.00 sec)

UPDATE COMMAND :

mysql> UPDATE passenger
    -> SET seat_number = 'D15'
    -> WHERE passenger_id = 1;
Query OK, 1 row affected (0.02 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> SELECT * FROM passenger;
+--------------+---------+---------------+-------------+
| passenger_id | user_id | ticket_number | seat_number |
+--------------+---------+---------------+-------------+
|            1 |       1 | IND123        | D15         |
|            2 |       2 | IND124        | C13         |
|            3 |       3 | IND125        | A14         |
+--------------+---------+---------------+-------------+
3 rows in set (0.00 sec)
