create database AIRLINE;
Query OK, 1 row affected (0.007 sec)

MariaDB [(none)]> use AIRLINE;
Database changed
MariaDB [AIRLINE]> show tables;
Empty set (0.001 sec)

MariaDB [AIRLINE]> create table customer(Cust_Id int primary key auto_increment,Name varchar(200),Mobile_No int unique,Gender varchar(10),Address varchar(200));
Query OK, 0 rows affected (0.023 sec)

MariaDB [AIRLINE]> desc customer;
+-----------+--------------+------+-----+---------+----------------+
| Field     | Type         | Null | Key | Default | Extra          |
+-----------+--------------+------+-----+---------+----------------+
| Cust_Id   | int(11)      | NO   | PRI | NULL    | auto_increment |
| Name      | varchar(200) | YES  |     | NULL    |                |
| Mobile_No | int(11)      | YES  | UNI | NULL    |                |
| Gender    | varchar(10)  | YES  |     | NULL    |                |
| Address   | varchar(200) | YES  |     | NULL    |                |
+-----------+--------------+------+-----+---------+----------------+
5 rows in set (0.042 sec)

MariaDB [AIRLINE]> drop table customer;
Query OK, 0 rows affected (0.010 sec)

MariaDB [AIRLINE]> create table customer(Cust_Id int primary key auto_increment,Name varchar(200) not null,Mobile_No int unique not null,Gender varchar(10) not null,Address varchar(200) not null);
Query OK, 0 rows affected (0.013 sec)

MariaDB [AIRLINE]> desc customer;
+-----------+--------------+------+-----+---------+----------------+
| Field     | Type         | Null | Key | Default | Extra          |
+-----------+--------------+------+-----+---------+----------------+
| Cust_Id   | int(11)      | NO   | PRI | NULL    | auto_increment |
| Name      | varchar(200) | NO   |     | NULL    |                |
| Mobile_No | int(11)      | NO   | UNI | NULL    |                |
| Gender    | varchar(10)  | NO   |     | NULL    |                |
| Address   | varchar(200) | NO   |     | NULL    |                |
+-----------+--------------+------+-----+---------+----------------+
5 rows in set (0.040 sec)

MariaDB [AIRLINE]> create table airport(Airport_Code int primary key,Airport_Name varchar(100)not null,City varchar(200)not null,State varchar(200)not null);
Query OK, 0 rows affected (0.014 sec)

MariaDB [AIRLINE]> desc airport;
+--------------+--------------+------+-----+---------+-------+
| Field        | Type         | Null | Key | Default | Extra |
+--------------+--------------+------+-----+---------+-------+
| Airport_Code | int(11)      | NO   | PRI | NULL    |       |
| Airport_Name | varchar(100) | NO   |     | NULL    |       |
| City         | varchar(200) | NO   |     | NULL    |       |
| State        | varchar(200) | NO   |     | NULL    |       |
+--------------+--------------+------+-----+---------+-------+
4 rows in set (0.041 sec)

MariaDB [AIRLINE]> create table Flight(Flight_No int auto_increment,AirLine_Name varchar(200),Arrival_Time datetime not null,Departure_Time datetime not null,Total_Seat int,price int not null);
ERROR 1075 (42000): Incorrect table definition; there can be only one auto column and it must be defined as a key
MariaDB [AIRLINE]> create table Flight(Flight_No int primary key auto_increment,AirLine_Name varchar(200),Arrival_Time datetime not null,Departure_Time datetime not null,Total_Seat int,price int not null);
Query OK, 0 rows affected (0.024 sec)

MariaDB [AIRLINE]> desc Flight;
+----------------+--------------+------+-----+---------+----------------+
| Field          | Type         | Null | Key | Default | Extra          |
+----------------+--------------+------+-----+---------+----------------+
| Flight_No      | int(11)      | NO   | PRI | NULL    | auto_increment |
| AirLine_Name   | varchar(200) | YES  |     | NULL    |                |
| Arrival_Time   | datetime     | NO   |     | NULL    |                |
| Departure_Time | datetime     | NO   |     | NULL    |                |
| Total_Seat     | int(11)      | YES  |     | NULL    |                |
| price          | int(11)      | NO   |     | NULL    |                |
+----------------+--------------+------+-----+---------+----------------+
6 rows in set (0.039 sec)

MariaDB [AIRLINE]> create table ticket(Ticket_No int primary key auto_increment,status varchar(100),Cust_Id int,Foreign Key(Cust_Id) references Customer(Cust_Id),Ariport_code int,Flight_No int,Foreign_Key(Airport_Code) references airport(Airport_Code),Foreign Key(Flight_No) references Flight(Flight_No));
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near '(Airport_Code) references airport(Airport_Code),Foreign Key(Flight_No) refere...' at line 1
MariaDB [AIRLINE]> create table ticket(Ticket_No int primary key auto_increment,status varchar(100),Cust_Id int,Foreign Key(Cust_Id) references Customer(Cust_Id),          Ariport_code int,Flight_No int,Foreign_Key(Airport_Code) references airport(Airport_Code),Foreign Key(Flight_No) references Flight(Flight_No));
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near '(Airport_Code) references airport(Airport_Code),Foreign Key(Flight_No) refere...' at line 1
MariaDB [AIRLINE]> create table ticket(Ticket_No int primary key auto_increment,status varchar(100),Cust_Id int,Foreign Key(Cust_Id) references Customer(Cust_Id),          Ariport_code int,Flight_No int));
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near ')' at line 1
MariaDB [AIRLINE]> create table ticket(Ticket_No int primary key auto_increment,status varchar(100),Cust_Id int,Foreign Key(Cust_Id) references Customer(Cust_Id),          Ariport_code int,Flight_No int));
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near ')' at line 1
MariaDB [AIRLINE]> create table ticket(Ticket_No int primary key auto_increment,status varchar(100),Cust_Id int,Foreign Key(Cust_Id) references Customer(Cust_Id),          Ariport_code int,Flight_No int);
Query OK, 0 rows affected (0.025 sec)

MariaDB [AIRLINE]> desc Ticket;
+--------------+--------------+------+-----+---------+----------------+
| Field        | Type         | Null | Key | Default | Extra          |
+--------------+--------------+------+-----+---------+----------------+
| Ticket_No    | int(11)      | NO   | PRI | NULL    | auto_increment |
| status       | varchar(100) | YES  |     | NULL    |                |
| Cust_Id      | int(11)      | YES  | MUL | NULL    |                |
| Ariport_code | int(11)      | YES  |     | NULL    |                |
| Flight_No    | int(11)      | YES  |     | NULL    |                |
+--------------+--------------+------+-----+---------+----------------+
5 rows in set (0.040 sec)

MariaDB [AIRLINE]> alter table Ticket add Foreign Key Airport_code references airport(Airport_Code));
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near 'references airport(Airport_Code))' at line 1
MariaDB [AIRLINE]> alter table Ticket add Foreign Key Ariport_code references airport(Airport_Code));
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near 'references airport(Airport_Code))' at line 1
MariaDB [AIRLINE]> drop table Ticket;
Query OK, 0 rows affected (0.030 sec)

MariaDB [AIRLINE]> create table ticket(Ticket_No int primary key auto_increment,status varchar(100),Cust_Id int,Foreign Key(Cust_Id) references Customer(Cust_Id),          Airport_Code int,Flight_No int);
Query OK, 0 rows affected (0.014 sec)

MariaDB [AIRLINE]> desc Ticket;
+--------------+--------------+------+-----+---------+----------------+
| Field        | Type         | Null | Key | Default | Extra          |
+--------------+--------------+------+-----+---------+----------------+
| Ticket_No    | int(11)      | NO   | PRI | NULL    | auto_increment |
| status       | varchar(100) | YES  |     | NULL    |                |
| Cust_Id      | int(11)      | YES  | MUL | NULL    |                |
| Airport_Code | int(11)      | YES  |     | NULL    |                |
| Flight_No    | int(11)      | YES  |     | NULL    |                |
+--------------+--------------+------+-----+---------+----------------+
5 rows in set (0.027 sec)

MariaDB [AIRLINE]> alter table Ticket add Foreign Key Airport_code references airport(Airport_Code));
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near 'references airport(Airport_Code))' at line 1
MariaDB [AIRLINE]> alter table Ticket add Foreign Key(Airport_code) references airport(Airport_Code));
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near ')' at line 1
MariaDB [AIRLINE]> alter table Ticket add Foreign Key(Airport_code) references airport(Airport_Code));
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near ')' at line 1
MariaDB [AIRLINE]> desc airport;
+--------------+--------------+------+-----+---------+-------+
| Field        | Type         | Null | Key | Default | Extra |
+--------------+--------------+------+-----+---------+-------+
| Airport_Code | int(11)      | NO   | PRI | NULL    |       |
| Airport_Name | varchar(100) | NO   |     | NULL    |       |
| City         | varchar(200) | NO   |     | NULL    |       |
| State        | varchar(200) | NO   |     | NULL    |       |
+--------------+--------------+------+-----+---------+-------+
4 rows in set (0.026 sec)

MariaDB [AIRLINE]> desc ticket;
+--------------+--------------+------+-----+---------+----------------+
| Field        | Type         | Null | Key | Default | Extra          |
+--------------+--------------+------+-----+---------+----------------+
| Ticket_No    | int(11)      | NO   | PRI | NULL    | auto_increment |
| status       | varchar(100) | YES  |     | NULL    |                |
| Cust_Id      | int(11)      | YES  | MUL | NULL    |                |
| Airport_Code | int(11)      | YES  |     | NULL    |                |
| Flight_No    | int(11)      | YES  |     | NULL    |                |
+--------------+--------------+------+-----+---------+----------------+
5 rows in set (0.026 sec)

MariaDB [AIRLINE]> Alter table Ticket add Foreign Key(Airport_code) references airport(Airport_Code));
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near ')' at line 1
MariaDB [AIRLINE]> Alter table Ticket add Foreign Key(Airport_code) references airport(Airport_Code);
Query OK, 0 rows affected (0.071 sec)
Records: 0  Duplicates: 0  Warnings: 0

MariaDB [AIRLINE]> desc Ticket;
+--------------+--------------+------+-----+---------+----------------+
| Field        | Type         | Null | Key | Default | Extra          |
+--------------+--------------+------+-----+---------+----------------+
| Ticket_No    | int(11)      | NO   | PRI | NULL    | auto_increment |
| status       | varchar(100) | YES  |     | NULL    |                |
| Cust_Id      | int(11)      | YES  | MUL | NULL    |                |
| Airport_Code | int(11)      | YES  | MUL | NULL    |                |
| Flight_No    | int(11)      | YES  |     | NULL    |                |
+--------------+--------------+------+-----+---------+----------------+
5 rows in set (0.034 sec)

MariaDB [AIRLINE]> Alter table Ticket add Foreign Key(Flight_No) references Flight(Flight_No);
Query OK, 0 rows affected (0.049 sec)
Records: 0  Duplicates: 0  Warnings: 0

MariaDB [AIRLINE]> desc ticket;
+--------------+--------------+------+-----+---------+----------------+
| Field        | Type         | Null | Key | Default | Extra          |
+--------------+--------------+------+-----+---------+----------------+
| Ticket_No    | int(11)      | NO   | PRI | NULL    | auto_increment |
| status       | varchar(100) | YES  |     | NULL    |                |
| Cust_Id      | int(11)      | YES  | MUL | NULL    |                |
| Airport_Code | int(11)      | YES  | MUL | NULL    |                |
| Flight_No    | int(11)      | YES  | MUL | NULL    |                |
+--------------+--------------+------+-----+---------+----------------+
5 rows in set (0.040 sec)

MariaDB [AIRLINE]> show tables;
+-------------------+
| Tables_in_airline |
+-------------------+
| airport           |
| customer          |
| flight            |
| ticket            |
+-------------------+
4 rows in set (0.002 sec)

MariaDB [AIRLINE]> desc airport;
+--------------+--------------+------+-----+---------+-------+
| Field        | Type         | Null | Key | Default | Extra |
+--------------+--------------+------+-----+---------+-------+
| Airport_Code | int(11)      | NO   | PRI | NULL    |       |
| Airport_Name | varchar(100) | NO   |     | NULL    |       |
| City         | varchar(200) | NO   |     | NULL    |       |
| State        | varchar(200) | NO   |     | NULL    |       |
+--------------+--------------+------+-----+---------+-------+
4 rows in set (0.031 sec)

MariaDB [AIRLINE]> insert into airport values(101,"Kempegawada","Banglore","Karnataka");
Query OK, 1 row affected (0.002 sec)

MariaDB [AIRLINE]> insert into airport values(102,"Indira Gandhi","Delhi","Delhi");
Query OK, 1 row affected (0.002 sec)

MariaDB [AIRLINE]> insert into airport values(103,"Shivaji","Pune","Maharastra");
Query OK, 1 row affected (0.001 sec)

MariaDB [AIRLINE]> select * from airport;
+--------------+---------------+----------+------------+
| Airport_Code | Airport_Name  | City     | State      |
+--------------+---------------+----------+------------+
|          101 | Kempegawada   | Banglore | Karnataka  |
|          102 | Indira Gandhi | Delhi    | Delhi      |
|          103 | Shivaji       | Pune     | Maharastra |
+--------------+---------------+----------+------------+
3 rows in set (0.001 sec)

MariaDB [AIRLINE]> show tables;
+-------------------+
| Tables_in_airline |
+-------------------+
| airport           |
| customer          |
| flight            |
| ticket            |
+-------------------+
4 rows in set (0.001 sec)

MariaDB [AIRLINE]> desc customer;
+-----------+--------------+------+-----+---------+----------------+
| Field     | Type         | Null | Key | Default | Extra          |
+-----------+--------------+------+-----+---------+----------------+
| Cust_Id   | int(11)      | NO   | PRI | NULL    | auto_increment |
| Name      | varchar(200) | NO   |     | NULL    |                |
| Mobile_No | int(11)      | NO   | UNI | NULL    |                |
| Gender    | varchar(10)  | NO   |     | NULL    |                |
| Address   | varchar(200) | NO   |     | NULL    |                |
+-----------+--------------+------+-----+---------+----------------+
5 rows in set (0.026 sec)

MariaDB [AIRLINE]> insert into customer values(null,"Siddharth",70707070,"Male","Banglore");
Query OK, 1 row affected (0.012 sec)

MariaDB [AIRLINE]> insert into customer values(null,"Rahul",232324,"Male","Pune");
Query OK, 1 row affected (0.001 sec)

MariaDB [AIRLINE]> insert into customer values(null,"Deepak",233324,"Delhi","Delhi");
Query OK, 1 row affected (0.002 sec)

MariaDB [AIRLINE]> insert into customer values(null,"Sakshi",233324,"Male","Arrah");
ERROR 1062 (23000): Duplicate entry '233324' for key 'Mobile_No'
MariaDB [AIRLINE]> insert into customer values(null,"Sakshi",991224,"Male","Arrah");
Query OK, 1 row affected (0.011 sec)

MariaDB [AIRLINE]> select * from customer;
+---------+-----------+-----------+--------+----------+
| Cust_Id | Name      | Mobile_No | Gender | Address  |
+---------+-----------+-----------+--------+----------+
|       1 | Siddharth |  70707070 | Male   | Banglore |
|       2 | Rahul     |    232324 | Male   | Pune     |
|       3 | Deepak    |    233324 | Delhi  | Delhi    |
|       5 | Sakshi    |    991224 | Male   | Arrah    |
+---------+-----------+-----------+--------+----------+
4 rows in set (0.001 sec)

MariaDB [AIRLINE]> show tables;
+-------------------+
| Tables_in_airline |
+-------------------+
| airport           |
| customer          |
| flight            |
| ticket            |
+-------------------+
4 rows in set (0.001 sec)

MariaDB [AIRLINE]> desc flight;
+----------------+--------------+------+-----+---------+----------------+
| Field          | Type         | Null | Key | Default | Extra          |
+----------------+--------------+------+-----+---------+----------------+
| Flight_No      | int(11)      | NO   | PRI | NULL    | auto_increment |
| AirLine_Name   | varchar(200) | YES  |     | NULL    |                |
| Arrival_Time   | datetime     | NO   |     | NULL    |                |
| Departure_Time | datetime     | NO   |     | NULL    |                |
| Total_Seat     | int(11)      | YES  |     | NULL    |                |
| price          | int(11)      | NO   |     | NULL    |                |
+----------------+--------------+------+-----+---------+----------------+
6 rows in set (0.034 sec)

MariaDB [AIRLINE]> insert into flight values(500,"Indigo",'2021-11-19 10:15:24','2021-11-19 12:15:24');
ERROR 1136 (21S01): Column count doesn't match value count at row 1
MariaDB [AIRLINE]> insert into flight values(500,"Indigo",'2021-11-19 10:15:24','2021-11-19 12:15:24',100,2000);
Query OK, 1 row affected (0.002 sec)

MariaDB [AIRLINE]> select * from flight;
+-----------+--------------+---------------------+---------------------+------------+-------+
| Flight_No | AirLine_Name | Arrival_Time        | Departure_Time      | Total_Seat | price |
+-----------+--------------+---------------------+---------------------+------------+-------+
|       500 | Indigo       | 2021-11-19 10:15:24 | 2021-11-19 12:15:24 |        100 |  2000 |
+-----------+--------------+---------------------+---------------------+------------+-------+
1 row in set (0.001 sec)

MariaDB [AIRLINE]> insert into flight values(null,"Spice_Jet",'2020-10-10 10:15:24','2020-10-10 12:15:24',120,3000);
Query OK, 1 row affected (0.001 sec)

MariaDB [AIRLINE]> insert into flight values(500,"Indigo",'2021-11-19 10:15:24','2021-11-19 12:15:24',100,2000);
ERROR 1062 (23000): Duplicate entry '500' for key 'PRIMARY'
MariaDB [AIRLINE]> insert into flight values(null,"Indigo",'2021-11-19 10:15:24','2021-11-19 12:15:24',100,2000);
Query OK, 1 row affected (0.011 sec)

MariaDB [AIRLINE]> select * from flight;
+-----------+--------------+---------------------+---------------------+------------+-------+
| Flight_No | AirLine_Name | Arrival_Time        | Departure_Time      | Total_Seat | price |
+-----------+--------------+---------------------+---------------------+------------+-------+
|       500 | Indigo       | 2021-11-19 10:15:24 | 2021-11-19 12:15:24 |        100 |  2000 |
|       501 | Spice_Jet    | 2020-10-10 10:15:24 | 2020-10-10 12:15:24 |        120 |  3000 |
|       502 | Indigo       | 2021-11-19 10:15:24 | 2021-11-19 12:15:24 |        100 |  2000 |
+-----------+--------------+---------------------+---------------------+------------+-------+
3 rows in set (0.001 sec)

MariaDB [AIRLINE]> insert into flight values(null,"Spice_Jet",'2020-10-10 10:15:24','2020-10-10 12:15:24',120,3000);
Query OK, 1 row affected (0.001 sec)

MariaDB [AIRLINE]> select * from flight;
+-----------+--------------+---------------------+---------------------+------------+-------+
| Flight_No | AirLine_Name | Arrival_Time        | Departure_Time      | Total_Seat | price |
+-----------+--------------+---------------------+---------------------+------------+-------+
|       500 | Indigo       | 2021-11-19 10:15:24 | 2021-11-19 12:15:24 |        100 |  2000 |
|       501 | Spice_Jet    | 2020-10-10 10:15:24 | 2020-10-10 12:15:24 |        120 |  3000 |
|       502 | Indigo       | 2021-11-19 10:15:24 | 2021-11-19 12:15:24 |        100 |  2000 |
|       503 | Spice_Jet    | 2020-10-10 10:15:24 | 2020-10-10 12:15:24 |        120 |  3000 |
+-----------+--------------+---------------------+---------------------+------------+-------+
4 rows in set (0.001 sec)

MariaDB [AIRLINE]> insert into flight values(null,"Spice_Jet",'2020-10-10 10:15:24','2020-10-10 12:15:24',120,3000);
Query OK, 1 row affected (0.012 sec)

MariaDB [AIRLINE]> select * from flight;
+-----------+--------------+---------------------+---------------------+------------+-------+
| Flight_No | AirLine_Name | Arrival_Time        | Departure_Time      | Total_Seat | price |
+-----------+--------------+---------------------+---------------------+------------+-------+
|       500 | Indigo       | 2021-11-19 10:15:24 | 2021-11-19 12:15:24 |        100 |  2000 |
|       501 | Spice_Jet    | 2020-10-10 10:15:24 | 2020-10-10 12:15:24 |        120 |  3000 |
|       502 | Indigo       | 2021-11-19 10:15:24 | 2021-11-19 12:15:24 |        100 |  2000 |
|       503 | Spice_Jet    | 2020-10-10 10:15:24 | 2020-10-10 12:15:24 |        120 |  3000 |
|       504 | Spice_Jet    | 2020-10-10 10:15:24 | 2020-10-10 12:15:24 |        120 |  3000 |
+-----------+--------------+---------------------+---------------------+------------+-------+
5 rows in set (0.001 sec)

MariaDB [AIRLINE]> show tables;
+-------------------+
| Tables_in_airline |
+-------------------+
| airport           |
| customer          |
| flight            |
| ticket            |
+-------------------+
4 rows in set (0.001 sec)

MariaDB [AIRLINE]> select * from airport;
+--------------+---------------+----------+------------+
| Airport_Code | Airport_Name  | City     | State      |
+--------------+---------------+----------+------------+
|          101 | Kempegawada   | Banglore | Karnataka  |
|          102 | Indira Gandhi | Delhi    | Delhi      |
|          103 | Shivaji       | Pune     | Maharastra |
+--------------+---------------+----------+------------+
3 rows in set (0.001 sec)

MariaDB [AIRLINE]> select * from customer;
+---------+-----------+-----------+--------+----------+
| Cust_Id | Name      | Mobile_No | Gender | Address  |
+---------+-----------+-----------+--------+----------+
|       1 | Siddharth |  70707070 | Male   | Banglore |
|       2 | Rahul     |    232324 | Male   | Pune     |
|       3 | Deepak    |    233324 | Delhi  | Delhi    |
|       5 | Sakshi    |    991224 | Male   | Arrah    |
+---------+-----------+-----------+--------+----------+
4 rows in set (0.000 sec)

MariaDB [AIRLINE]> select * from flight;
+-----------+--------------+---------------------+---------------------+------------+-------+
| Flight_No | AirLine_Name | Arrival_Time        | Departure_Time      | Total_Seat | price |
+-----------+--------------+---------------------+---------------------+------------+-------+
|       500 | Indigo       | 2021-11-19 10:15:24 | 2021-11-19 12:15:24 |        100 |  2000 |
|       501 | Spice_Jet    | 2020-10-10 10:15:24 | 2020-10-10 12:15:24 |        120 |  3000 |
|       502 | Indigo       | 2021-11-19 10:15:24 | 2021-11-19 12:15:24 |        100 |  2000 |
|       503 | Spice_Jet    | 2020-10-10 10:15:24 | 2020-10-10 12:15:24 |        120 |  3000 |
|       504 | Spice_Jet    | 2020-10-10 10:15:24 | 2020-10-10 12:15:24 |        120 |  3000 |
+-----------+--------------+---------------------+---------------------+------------+-------+
5 rows in set (0.001 sec)

MariaDB [AIRLINE]> desc ticket;
+--------------+--------------+------+-----+---------+----------------+
| Field        | Type         | Null | Key | Default | Extra          |
+--------------+--------------+------+-----+---------+----------------+
| Ticket_No    | int(11)      | NO   | PRI | NULL    | auto_increment |
| status       | varchar(100) | YES  |     | NULL    |                |
| Cust_Id      | int(11)      | YES  | MUL | NULL    |                |
| Airport_Code | int(11)      | YES  | MUL | NULL    |                |
| Flight_No    | int(11)      | YES  | MUL | NULL    |                |
+--------------+--------------+------+-----+---------+----------------+
5 rows in set (0.032 sec)

MariaDB [AIRLINE]> insert into ticket values(1000,"Confirmed",1,101,500);
Query OK, 1 row affected (0.001 sec)

MariaDB [AIRLINE]> insert into ticket values(null,"Confirmed",2,101,500);
Query OK, 1 row affected (0.002 sec)

MariaDB [AIRLINE]> insert into ticket values(null,"Confirmed",3,101,500);
Query OK, 1 row affected (0.012 sec)

MariaDB [AIRLINE]> select * from ticket;
+-----------+-----------+---------+--------------+-----------+
| Ticket_No | status    | Cust_Id | Airport_Code | Flight_No |
+-----------+-----------+---------+--------------+-----------+
|      1000 | Confirmed |       1 |          101 |       500 |
|      1001 | Confirmed |       2 |          101 |       500 |
|      1002 | Confirmed |       3 |          101 |       500 |
+-----------+-----------+---------+--------------+-----------+
3 rows in set (0.001 sec)

MariaDB [AIRLINE]> select * from customer;
+---------+-----------+-----------+--------+----------+
| Cust_Id | Name      | Mobile_No | Gender | Address  |
+---------+-----------+-----------+--------+----------+
|       1 | Siddharth |  70707070 | Male   | Banglore |
|       2 | Rahul     |    232324 | Male   | Pune     |
|       3 | Deepak    |    233324 | Delhi  | Delhi    |
|       5 | Sakshi    |    991224 | Male   | Arrah    |
+---------+-----------+-----------+--------+----------+
4 rows in set (0.001 sec)

MariaDB [AIRLINE]> select * from flight;
+-----------+--------------+---------------------+---------------------+------------+-------+
| Flight_No | AirLine_Name | Arrival_Time        | Departure_Time      | Total_Seat | price |
+-----------+--------------+---------------------+---------------------+------------+-------+
|       500 | Indigo       | 2021-11-19 10:15:24 | 2021-11-19 12:15:24 |        100 |  2000 |
|       501 | Spice_Jet    | 2020-10-10 10:15:24 | 2020-10-10 12:15:24 |        120 |  3000 |
|       502 | Indigo       | 2021-11-19 10:15:24 | 2021-11-19 12:15:24 |        100 |  2000 |
|       503 | Spice_Jet    | 2020-10-10 10:15:24 | 2020-10-10 12:15:24 |        120 |  3000 |
|       504 | Spice_Jet    | 2020-10-10 10:15:24 | 2020-10-10 12:15:24 |        120 |  3000 |
+-----------+--------------+---------------------+---------------------+------------+-------+
5 rows in set (0.001 sec)

MariaDB [AIRLINE]> select * from ticket;
+-----------+-----------+---------+--------------+-----------+
| Ticket_No | status    | Cust_Id | Airport_Code | Flight_No |
+-----------+-----------+---------+--------------+-----------+
|      1000 | Confirmed |       1 |          101 |       500 |
|      1001 | Confirmed |       2 |          101 |       500 |
|      1002 | Confirmed |       3 |          101 |       500 |
+-----------+-----------+---------+--------------+-----------+
3 rows in set (0.001 sec)

MariaDB [AIRLINE]> select c.Cust_Id,c.Name,c.Gender,f.AirLine_Name, f.Flight_No,f.Arrival_Time,f.Departure_Time t.Ticket_No,t.status from customer c,flight f,ticket t where t.Cust_Id = c.Cust_Id and t.Flight_No = f.Flight_No;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near '.Ticket_No,t.status from customer c,flight f,ticket t where t.Cust_Id = c.Cus...' at line 1
MariaDB [AIRLINE]> select c.Cust_Id,c.Name,c.Gender,f.AirLine_Name, f.Flight_No,f.Arrival_Time,f.Departure_Time t.Ticket_No,t.status from customer c,flight f,ticket t where t.Cust_Id = c.Cust_Id and t.Flight_No = f.Flight_No;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near '.Ticket_No,t.status from customer c,flight f,ticket t where t.Cust_Id = c.Cus...' at line 1
MariaDB [AIRLINE]> select c.Cust_Id,c.Name,c.Gender,f.AirLine_Name, f.Flight_No,f.Arrival_Time,f.Departure_Time,t.Ticket_No,t.status from customer c,flight f,ticket t where t.Cust_Id = c.Cust_Id and t.Flight_No = f.Flight_No;
+---------+-----------+--------+--------------+-----------+---------------------+---------------------+-----------+-----------+
| Cust_Id | Name      | Gender | AirLine_Name | Flight_No | Arrival_Time        | Departure_Time      | Ticket_No | status    |
+---------+-----------+--------+--------------+-----------+---------------------+---------------------+-----------+-----------+
|       1 | Siddharth | Male   | Indigo       |       500 | 2021-11-19 10:15:24 | 2021-11-19 12:15:24 |      1000 | Confirmed |
|       2 | Rahul     | Male   | Indigo       |       500 | 2021-11-19 10:15:24 | 2021-11-19 12:15:24 |      1001 | Confirmed |
|       3 | Deepak    | Delhi  | Indigo       |       500 | 2021-11-19 10:15:24 | 2021-11-19 12:15:24 |      1002 | Confirmed |
+---------+-----------+--------+--------------+-----------+---------------------+---------------------+-----------+-----------+
3 rows in set (0.001 sec)

MariaDB [AIRLINE]> select c.Cust_Id,c.Name,c.Gender,f.AirLine_Name, f.Flight_No,f.Arrival_Time,f.Departure_Time,t.Ticket_No,t.status from customer c,flight f,ticket t where t.Cust_Id = c.Cust_Id an