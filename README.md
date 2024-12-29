# BookMyShow
Database - Use Case Problem

## Entity-Relationship Diagram
![image](https://github.com/user-attachments/assets/77b38328-be6b-4c04-93f3-228e02318b79)

---
## Create Table Queries:

```
CREATE TABLE City (
    City_id INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR (100) NOT NULL UNIQUE
);
```

```
CREATE TABLE Theatre (
    Theatre_id INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR (100) NOT NULL,
    City_id INT NOT NULL,
    Address VARCHAR (255),
    Phone_No VARCHAR (10),
    FOREIGN KEY (City_id) REFERENCES City (City_id)
);
````

```
CREATE TABLE Movie (
    Movie_id INT AUTO_INCREMENT PRIMARY KEY,
    Title VARCHAR (200) NOT NULL,
    Genre VARCHAR (50),
    Duration INT NOT NULL,
    Language VARCHAR (50) NOT NULL
);
```

```
CREATE TABLE ShowDetails (
    Show_id INT AUTO_INCREMENT PRIMARY KEY,
    Theatre_id INT NOT NULL,
    Movie_id INT NOT NULL,
    ShowDate DATE NOT NULL,
    ShowTime TIME NOT NULL,
    FOREIGN KEY (Theatre_id) REFERENCES Theatre (Theatre_id),
    FOREIGN KEY (Movie_id) REFERENCES Movie (Movie_id),
    UNIQUE (Theatre_id, Movie_id, ShowDate, ShowTime)
);
```
## Sample Entries Queries:

***CITY TABLE*** :

```
INSERT INTO City (Name) VALUES
('Chennai'),
('Coimbatore'),
('Delhi');
```

![image](https://github.com/user-attachments/assets/ab15669e-6af1-46aa-b769-b43a8b510a7a)

---
***THEATRE TABLE*** :
```
INSERT INTO Theatre (Name, City_id, Address, Phone_No) VALUES
('PVR', 1, '123, Velachery, Chennai', '9876543210'),
('Cosmos Cinemas', 2, '123, Narasimhanaickenpalayam', '9876543201'),
('Akshara Theatre', 3, '123, Rohini Nagar, Delhi', '9876543021');
```

![image](https://github.com/user-attachments/assets/c9b5d60d-f7b2-4d1e-8762-fba553e42dd3)

---
***MOVIE TABLE*** :
```
INSERT INTO Movie (Title, Genre, Duration, Language) VALUES
('Avatar: The Way of Water', 'Sci-Fi', 192, 'English'),
('RRR', 'Action', 187, 'Telugu'),
('Inception', 'Thriller', 148, 'English');
```

![image](https://github.com/user-attachments/assets/a7afd3aa-4bd6-43a5-aaa1-18fd9297a137)

---
***SHOW DETAILS TABLE*** :
```
INSERT INTO ShowDetails (Theatre_id, Movie_id, ShowDate, ShowTime) VALUES
(1, 1, '2025-1-2', '18:00:00'),
(1, 2, '2025-1-2', '21:00:00'),
(2, 1, '2025-1-3', '20:30:00'),
(2, 3, '2025-1-3', '23:30:00'),
(3, 2, '2025-1-4', '18:30:00'),
(3, 3, '2025-1-4', '21:00:00');
```

![image](https://github.com/user-attachments/assets/be7c5d4a-6ff4-4bc9-9750-bfa5dcb8d971)

---
## Query to List Shows on a Given Date at a Given Theatre 

```
SELECT 
    s.Show_id,
    t.Name AS TheatreName,
    c.Name AS City,
    m.Title AS MovieTitle,
    s.ShowDate,
    s.ShowTime
FROM 
    ShowDetails s
JOIN 
    Theatre t ON s.Theatre_id = t.Theatre_id
JOIN 
    Movie m ON s.Movie_id = m.Movie_id
JOIN 
    City c ON t.City_id = c.City_id
WHERE 
    s.ShowDate = '2025-1-3'
    AND t.Name = 'Cosmos Cinemas';
```

![image](https://github.com/user-attachments/assets/c26ab95f-0579-41f3-b984-a33485c24998)
