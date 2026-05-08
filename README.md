# Clinic Appointment and Diagnostic Platform – ER Diagram

## Overview

This project represents the database design for a clinic management system.
The system focuses on handling appointments, consultations, diagnostic tests, reports, and payments in a structured and scalable way.

The goal of this design is to model a real-world clinic workflow where patients book appointments, visit doctors, undergo consultations, get prescribed tests, receive reports, and make payments.

---

## System Workflow

The overall flow of the system is:

Patient → Appointment → Consultation → Tests → Reports → Payment

* A patient books an appointment with a doctor
* The appointment may result in a consultation
* During consultation, doctors can prescribe diagnostic tests
* Tests generate reports later
* Payments are linked to the consultation

---

## Entities and Description

### Patients

Stores basic information about patients.

* id (PK)
* first_name, last_name
* email, phone_number
* created_at, updated_at

---

### Doctors

Stores doctor details.

* id (PK)
* first_name, last_name
* email, phone_number
* experience, fees
* created_at, updated_at

---

### Specialty

Represents different medical specialties (e.g., Cardiology, Neurology).

* id (PK)
* name

---

### Doctor_Specialty

Junction table to support multiple specialties per doctor.

* id (PK)
* doctor_id (FK)
* speciality_id (FK)

---

### Appointments

Represents booking made by a patient with a doctor.

* id (PK)
* patient_id (FK)
* doctor_id (FK)
* reason_for_visit
* appointment_date
* booked_at, updated_at
* status (PENDING, CONFIRMED, CANCELLED)

---

### Consultation

Represents the actual visit after an appointment.

* id (PK)
* appointment_id (FK, UNIQUE)
* doctor_id (FK)
* notes

Note: Not every appointment results in a consultation.

---

### Tests

Stores master list of diagnostic tests.

* id (PK)
* name (UNIQUE)
* price

---

### Prescribed_Tests

Junction table representing tests prescribed during a consultation.

* id (PK)
* consultation_id (FK)
* test_id (FK)

---

### Reports

Stores results of prescribed tests.

* id (PK)
* prescribed_test_id (FK)
* result
* generated_at

---

### Payments

Stores payment details for consultations.

* id (PK)
* consultation_id (FK)
* transaction_id (UNIQUE)
* amount
* payment_method (CREDIT_CARD, DEBIT_CARD, UPI)
* status (SUCCESSFUL, FAILED, CANCELLED, PENDING)
* payment_date

---

## Relationships

* One patient can have many appointments
* One doctor can handle many appointments
* One appointment results in at most one consultation
* One consultation can have multiple prescribed tests
* Each prescribed test generates a report
* Each consultation is associated with payment(s)
* One doctor can have multiple specialties

---

## Design Decisions

* Appointment and Consultation are separated to handle no-shows or cancellations
* Many-to-many relationships are handled using junction tables
* Reports are linked to prescribed tests instead of directly to consultation
* Payments are associated with consultations for better billing control
* Unique constraints are used to maintain data integrity

---

## How to Use

* The ER diagram image is included in this repository
* The schema definition is provided using structured notation
* This design can be implemented in relational databases like PostgreSQL or MySQL

---

## Author

Md Kashif Khan
