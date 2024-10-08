# Hospital-Management-Database-using-SQL
CREATE DATABASE HospitalManagement;

USE HospitalManagement;

CREATE TABLE Patients (
  PatientID INT PRIMARY KEY,
  FirstName VARCHAR(50) NOT NULL,
  LastName VARCHAR(50) NOT NULL,
  DateOfBirth DATE NOT NULL,
  Email VARCHAR(100) UNIQUE NOT NULL,
  Phone VARCHAR(20) NOT NULL,
  Address VARCHAR(255) NOT NULL
);

CREATE TABLE Doctors (
  DoctorID INT PRIMARY KEY,
  FirstName VARCHAR(50) NOT NULL,
  LastName VARCHAR(50) NOT NULL,
  Specialty VARCHAR(100) NOT NULL,
  Email VARCHAR(100) UNIQUE NOT NULL,
  Phone VARCHAR(20) NOT NULL
);

CREATE TABLE Departments (
  DepartmentID INT PRIMARY KEY,
  DepartmentName VARCHAR(100) NOT NULL
);

CREATE TABLE Rooms (
  RoomID INT PRIMARY KEY,
  RoomType VARCHAR(50) NOT NULL,
  DepartmentID INT NOT NULL,
  FOREIGN KEY (DepartmentID) REFERENCES Departments(DepartmentID)
);

CREATE TABLE Appointments (
  AppointmentID INT PRIMARY KEY,
  PatientID INT NOT NULL,
  DoctorID INT NOT NULL,
  AppointmentDate DATE NOT NULL,
  AppointmentTime TIME NOT NULL,
  FOREIGN KEY (PatientID) REFERENCES Patients(PatientID),
  FOREIGN KEY (DoctorID) REFERENCES Doctors(DoctorID)
);

CREATE TABLE Medications (
  MedicationID INT PRIMARY KEY,
  MedicationName VARCHAR(100) NOT NULL,
  Price DECIMAL(10, 2) NOT NULL
);

CREATE TABLE Prescriptions (
  PrescriptionID INT PRIMARY KEY,
  AppointmentID INT NOT NULL,
  MedicationID INT NOT NULL,
  Dosage VARCHAR(50) NOT NULL,
  FOREIGN KEY (AppointmentID) REFERENCES Appointments(AppointmentID),
  FOREIGN KEY (MedicationID) REFERENCES Medications(MedicationID)
);

CREATE TABLE Bills (
  BillID INT PRIMARY KEY,
  AppointmentID INT NOT NULL,
  BillDate DATE NOT NULL,
  Total DECIMAL(10, 2) NOT NULL,
  FOREIGN KEY (AppointmentID) REFERENCES Appointments(AppointmentID)
);

CREATE TABLE Payments (
  PaymentID INT PRIMARY KEY,
  BillID INT NOT NULL,
  PaymentDate DATE NOT NULL,
  Amount DECIMAL(10, 2) NOT NULL,
  FOREIGN KEY (BillID) REFERENCES Bills(BillID)
);

//insert data
INSERT INTO Patients (PatientID, FirstName, LastName, DateOfBirth, Email, Phone, Address)
VALUES
  (1, 'John', 'Doe', '1990-01-01', 'john.doe@example.com', '123-456-7890', '123 Main St');

INSERT INTO Doctors (DoctorID, FirstName, LastName, Specialty, Email, Phone)
VALUES
  (1, 'Jane', 'Doe', 'Cardiology', 'jane.doe@example.com', '987-654-3210');

INSERT INTO Departments (DepartmentID, DepartmentName)
VALUES
  (1, 'Cardiology');

INSERT INTO Rooms (RoomID, RoomType, DepartmentID)
VALUES
  (1, 'Exam Room', 1);

INSERT INTO Appointments (AppointmentID, PatientID, DoctorID, AppointmentDate, AppointmentTime)
VALUES
  (1, 1, 1, '2022-01-01', '10:00:00');

INSERT INTO Medications (MedicationID, MedicationName, Price)
VALUES
  (1, 'Aspirin', 5.99);

INSERT INTO Prescriptions (PrescriptionID, AppointmentID, MedicationID, Dosage)
VALUES
  (1, 1, 1, 'Take 2 tablets daily');

INSERT INTO Bills (BillID, AppointmentID, BillDate, Total)
VALUES
  (1, 1, '2022-01-01', 100.00);

INSERT INTO Payments (PaymentID, BillID, PaymentDate, Amount)
VALUES
  (1, 1, '2022-01-01', 100.00);

retrieve data
