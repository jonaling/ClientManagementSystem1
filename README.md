# ClientManagementSystem1 C#/Docker Project
This is a Client Management system created for learning purposes to direct clinics and such.

This project is created to run on c# with a system dedicated to helping a doctor manage patients visitation data as well as help secretaries with reservations and patient profiles.

Currently run using a sql database on Azure.

These are the quries used to create tables in the database:

CREATE TABLE Users {
  user_id int NOT NULL,
  user_username varchar(255),
  user_password varchar(255)
  PRIMARY KEY(user_id)
} ;

CREATE TABLE Accounts (
	account_id int NOT NULL,
	account_user_id int NOT NULL,
	account_name varchar(100) NOT NULL,
	account_dob date,
	account_creation_date datetime,
	account_type int,
	account_notes varchar(255),
	account_phone_code varchar(10),
	account_phone varchar(20),
	PRIMARY KEY(account_id),
	FOREIGN KEY(account_user_id) REFERENCES Users(user_id)
);

CREATE TABLE Reservations (
	reservation_id int NOT NULL,
	reservation_patient_id int NOT NULL,
	reservation_secretary_id int NOT NULL,
	reservation_visit_date date,
	reservation_visit_slot int,
	reservation_date datetime,
	PRIMARY KEY(reservation_id),
	FOREIGN KEY(reservation_patient_id) REFERENCES Accounts(account_id),
	FOREIGN KEY(reservation_secretary_id) REFERENCES Accounts(account_id),
);

CREATE TABLE Visits (
	visit_id int NOT NULL,
	visit_reservation_id int NOT NULL,
	visit_doctor_id int NOT NULL,
	visit_date date,
	visit_reasons varchar(200),
	visit_diagnosis varchar(200),
	visit_notes varchar(200),
	PRIMARY KEY(visit_id),
	FOREIGN KEY(visit_reservation_id) REFERENCES Reservations(reservation_id),
	FOREIGN KEY(visit_doctor_id) REFERENCES Accounts(account_id),
);

