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


