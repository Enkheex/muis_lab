CREATE DATABASE DreamHome;
USE DreamHome;

CREATE TABLE Branch (
    branchNo CHAR(4) PRIMARY KEY,
    street VARCHAR(25),
    city VARCHAR(15),
    postcode VARCHAR(10)
);

INSERT INTO Branch VALUES
('B001', '10 London St',   'London',      'SW1 4EH'),
('B002', '11 Moscow St',   'Moscow',      'AB2 3SU'),
('B003', '12 NYC St',      'NYC',         'G11 9QX'),
('B004', '13 Shanghai St', 'Shanghai',    'BS99 1NZ'),
('B005', '14 Damdin St',   'Ulaanbaatar', 'NW10 6EU');

CREATE TABLE Staff (
    staffNo VARCHAR(5) PRIMARY KEY,
    fName VARCHAR(30),
    lName VARCHAR(30),
    position VARCHAR(20),
    sex CHAR(1) CHECK(sex IN ('M','F')),
    DOB DATE,
    salary DECIMAL(10, 2),
    branchNo CHAR(4),
    FOREIGN KEY (branchNo) REFERENCES Branch(branchNo)
);

INSERT INTO Staff VALUES
('S001', 'John',  'White', 'Assistant',  'M', '2001-01-01', 10000, 'B001'),
('S002', 'Ann',   'Beech', 'Assistant',  'F', '2002-02-02', 20000, 'B002'),
('S003', 'David', 'Ford',  'Manager',    'M', '2003-03-03', 30000, 'B003'),
('S004', 'Mary',  'Howe',  'Manager',    'F', '2004-04-04', 40000,  'B004'),
('S005', 'Susan', 'Brand', 'Supervisor', 'F', '2005-05-05', 50000, 'B005');

CREATE TABLE PrivateOwner (
    ownerNo VARCHAR(5) PRIMARY KEY,
    fName VARCHAR(30),
    lName VARCHAR(30),
    address VARCHAR(100),
    telNo VARCHAR(20)
);

INSERT INTO PrivateOwner VALUES
('O001', 'Joe',   'Keogh',  '1 Park Ln, London',       '01224-861212'),
('O002', 'Ivan',  'Petrov', '2 Red Sq, Moscow',        '0141-357-7419'),
('O003', 'Tina',  'Murphy', '3 5th Ave, NYC',          '0141-943-1728'),
('O004', 'Li',    'Wang',   '4 Bund, Shanghai',        '0141-225-7025'),
('O005', 'Bat',   'Erdene', '5 Peace Ave, Ulaanbaatar','9911-2233');

CREATE TABLE PropertyForRent (
    propertyNo VARCHAR(5) PRIMARY KEY,
    street VARCHAR(25),
    city VARCHAR(15),
    postcode VARCHAR(10),
    type VARCHAR(10),  
    rooms INT,
    rent DECIMAL(10,2),  
    ownerNo VARCHAR(5),  
    staffNo VARCHAR(5), 
    branchNo CHAR(4),   
    FOREIGN KEY (ownerNo) REFERENCES PrivateOwner(ownerNo),
    FOREIGN KEY (staffNo) REFERENCES Staff(staffNo),
    FOREIGN KEY (branchNo) REFERENCES Branch(branchNo)
);

INSERT INTO PropertyForRent VALUES
('P001', '15 West St',      'London',      'SW1 4EH',  'Flat',  1, 500,  'O001', 'S001', 'B001'),
('P002', '16 East St',      'Moscow',      'AB2 3SU',  'House', 2, 600,  'O002', 'S002', 'B002'),
('P003', '17 North St',     'NYC',         'G11 9QX',  'Flat',  3, 700, 'O003', 'S003', 'B003'),
('P004', '18 South St',     'Shanghai',    'BS99 1NZ', 'Flat',  4, 800,  'O004', 'S004', 'B004'),
('P005', '19 Sukhbaatar Sq','Ulaanbaatar', 'NW10 6EU', 'House', 5, 900,  'O005', 'S005', 'B005');

CREATE TABLE Client (
    clientNo VARCHAR(5) PRIMARY KEY,
    fName VARCHAR(30),
    lName VARCHAR(30),  
    telNo VARCHAR(20),
    prefType VARCHAR(10),
    maxRent DECIMAL(10,2)
);

INSERT INTO Client VALUES
('C001', 'Mike',   'Ritchie', '01475-392178', 'Flat',  500),
('C002', 'Mary',   'Tregear', '01224-196720', 'House', 600),
('C003', 'John',   'Kay',     '0207-774-5632', 'Flat',  700),
('C004', 'Aline',  'Stewart', '0141-848-1825', 'Flat',  800),
('C005', 'Sarnai', 'Bold',    '8899-1122',     'House', 900);

CREATE TABLE Viewing (
    clientNo VARCHAR(5),
    propertyNo VARCHAR(5),
    viewDate DATE,      
    comment VARCHAR(50),
    PRIMARY KEY (clientNo, propertyNo, viewDate), 
    FOREIGN KEY (clientNo) REFERENCES Client(clientNo),
    FOREIGN KEY (propertyNo) REFERENCES PropertyForRent(propertyNo)
);

INSERT INTO Viewing VALUES
('C001', 'P001', '2024-05-24', 'too small'),
('C002', 'P002', '2024-04-20', 'too remote'),
('C003', 'P003', '2024-05-26', 'excellent'),
('C004', 'P004', '2024-05-14', NULL),
('C005', 'P005', '2024-04-28', 'perfect');

CREATE TABLE Registration (
    clientNo VARCHAR(5),
    branchNo CHAR(4),
    staffNo VARCHAR(5), 
    dateJoined DATE,   
    FOREIGN KEY (clientNo) REFERENCES Client(clientNo),
    FOREIGN KEY (branchNo) REFERENCES Branch(branchNo),
    FOREIGN KEY (staffNo) REFERENCES Staff(staffNo)
);

INSERT INTO Registration VALUES
('C001', 'B001', 'S001', '2025-01-01'),
('C002', 'B002', 'S002', '2025-02-02'),
('C003', 'B003', 'S003', '2025-03-03'),
('C004', 'B004', 'S004', '2025-04-04'),
('C005', 'B005', 'S005', '2025-05-05');

SELECT * FROM Branch;
SELECT * FROM Staff;
SELECT * FROM PrivateOwner;
SELECT * FROM Client;
SELECT * FROM PropertyForRent;
SELECT * FROM Viewing;
SELECT * FROM Registration;
