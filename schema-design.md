##MySQL database design section
1. Patients Table
Purpose: Stores personal details of patients.

Columns:

patient_id: Primary Key, auto-incremented integer.

full_name: String (max 100 characters), not null.

email: String (max 100 characters), unique and not null.

phone: String (max 15 characters), optional.

date_of_birth: Date, optional.

gender: Enum ('Male', 'Female', 'Other'), not null.

created_at: Timestamp, defaults to current time.

2. Doctors Table
Purpose: Stores doctor profiles and availability.

Columns:

doctor_id: Primary Key, auto-incremented integer.

full_name: String (max 100 characters), not null.

email: String (max 100 characters), unique and not null.

phone: String (max 15 characters), optional.

specialization: String (max 100 characters), not null.

available: Boolean, defaults to true.

created_at: Timestamp, defaults to current time.

3. Appointments Table
Purpose: Links patients and doctors for scheduled consultations.

Columns:

appointment_id: Primary Key, auto-incremented integer.

patient_id: Foreign Key referencing patients.patient_id, not null.

doctor_id: Foreign Key referencing doctors.doctor_id, not null.

appointment_time: Datetime, not null.

status: Enum ('Scheduled', 'Completed', 'Cancelled'), defaults to 'Scheduled'.

notes: Text, optional.

created_at: Timestamp, defaults to current time.

4. Admin Table
Purpose: Stores admin user credentials for managing the system.

Columns:

admin_id: Primary Key, auto-incremented integer.

username: String (max 50 characters), unique and not null.

password_hash: String (hashed), not null.

email: String (max 100 characters), unique, optional.

last_login: Timestamp, optional.

##MongoDB Collection Design

Collection Name: prescriptions
Purpose:
To store flexible, detailed prescription records associated with appointments. Each prescription can contain multiple medicines with varying instructions. This structure benefits from MongoDB’s ability to handle nested and dynamic data.

MongoDB Collection Design
📦 Collection Name: prescriptions
Purpose:
To store flexible, detailed prescription records associated with appointments. Each prescription can contain multiple medicines with varying instructions. This structure benefits from MongoDB’s ability to handle nested and dynamic data.

Example Document (with nested fields & arrays):
{
  "_id": "presc_1001",
  "appointment_id": 45,
  "doctor_id": 7,
  "patient_id": 12,
  "issued_at": "2025-06-29T10:00:00Z",
  "notes": "Patient has mild infection. Monitor symptoms.",
  "medications": [
    {
      "name": "Amoxicillin",
      "dosage": "500mg",
      "frequency": "3 times a day",
      "duration": "7 days"
    },
    {
      "name": "Paracetamol",
      "dosage": "650mg",
      "frequency": "2 times a day",
      "duration": "5 days"
    }
  ]
}

Nested medications array:

Supports multiple medicine entries per prescription.

Each entry includes structured dosage and usage details.

Reference fields:

appointment_id, doctor_id, patient_id allow linkage to relational database records (MySQL).

Flexible schema:

Easily allows adding fields like follow_up_required, allergy_notes, or refill_info in future versions.

##MySQL Database Design

Table: patients
id: INT, Primary Key, Auto Increment

full_name: VARCHAR(100), Not Null

email: VARCHAR(100), Not Null, Unique

phone: VARCHAR(15), Optional

date_of_birth: DATE, Optional

gender: ENUM('Male', 'Female', 'Other'), Not Null

created_at: TIMESTAMP, Default Current Time

📌 If a patient is deleted, consider deleting related appointments using ON DELETE CASCADE.

✅ Table: doctors
id: INT, Primary Key, Auto Increment

full_name: VARCHAR(100), Not Null

email: VARCHAR(100), Not Null, Unique

phone: VARCHAR(15), Optional

specialization: VARCHAR(100), Not Null

available: BOOLEAN, Default TRUE

created_at: TIMESTAMP, Default Current Time

📌 Doctors should not have overlapping appointments; system logic must validate this before booking.

✅ Table: appointments
id: INT, Primary Key, Auto Increment

doctor_id: INT, Foreign Key → doctors(id), Not Null

patient_id: INT, Foreign Key → patients(id), Not Null

appointment_time: DATETIME, Not Null

duration_minutes: INT, Default 60

status: ENUM('Scheduled', 'Completed', 'Cancelled'), Default 'Scheduled'

notes: TEXT, Optional

created_at: TIMESTAMP, Default Current Time

📌 You can enforce time gap logic for doctors in application code to avoid double booking.

✅ Table: admin
id: INT, Primary Key, Auto Increment

username: VARCHAR(50), Not Null, Unique

password_hash: VARCHAR(255), Not Null

email: VARCHAR(100), Optional, Unique

last_login: TIMESTAMP, Optional

🔒 Admins manage users and system settings. Keep passwords encrypted.

🏥 Optional Table: clinic_locations
id: INT, Primary Key, Auto Increment

name: VARCHAR(100), Not Null

address: TEXT, Not Null

phone: VARCHAR(15), Optional

🌍 If supporting multiple branches, this table links doctors or appointments to a location.

💳 Optional Table: payments
id: INT, Primary Key, Auto Increment

appointment_id: INT, Foreign Key → appointments(id), Not Null

amount: DECIMAL(10,2), Not Null

payment_method: ENUM('Cash', 'Card', 'UPI'), Not Null

status: ENUM('Pending', 'Completed', 'Failed'), Default 'Pending'

paid_at: DATETIME, Optional

This helps track financial records and can be extended with invoice or refund details.

## MongoDB Collection Design
Collection: prescriptions
This collection stores unstructured, flexible prescription data issued by doctors during appointments. It complements the structured appointments and patients tables in MySQL by holding complex or optional metadata.

{
  "_id": "ObjectId('665fd12c8a1b2e4c9c111234')",
  "appointmentId": 51,
  "patientId": 12,
  "doctorId": 7,
  "issuedAt": "2025-06-29T10:30:00Z",
  "medications": [
    {
      "name": "Amoxicillin",
      "dosage": "500mg",
      "frequency": "3 times a day",
      "duration": "7 days",
      "notes": "Take after food"
    },
    {
      "name": "Ibuprofen",
      "dosage": "400mg",
      "frequency": "2 times a day",
      "duration": "5 days",
      "notes": "Avoid if stomach upset"
    }
  ],
  "doctorNotes": "Patient showing symptoms of infection. Monitor for 5 days.",
  "refillInfo": {
    "allowed": true,
    "refillCount": 1,
    "lastRefilled": null
  },
  "pharmacy": {
    "name": "City Care Pharmacy",
    "location": "Downtown Plaza"
  },
  "tags": ["infection", "follow-up", "antibiotic"],
  "attachments": [
    {
      "filename": "lab_results.pdf",
      "uploadedAt": "2025-06-28T18:00:00Z",
      "url": "https://clinic-files.com/docs/lab_results_12.pdf"
    }
  ]
}



