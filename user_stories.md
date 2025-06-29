
Admin User Stories:
Admins interact with the system through the AdminDashboard, which connects via Thymeleaf Controllers to the Service Layer. Admins need functionality to manage system users, including doctors and patients, through the underlying MySQL repositories. Their actions involve tasks like registering new doctors, editing admin profiles, or managing appointment types, all of which access JPA Entities (Admin, Doctor) stored in the MySQL Database. Admins expect a smooth interface to oversee platform usage and make backend configuration changes efficiently.

Patient User Stories:
Patients access the application via RESTModules such as PatientDashboard, Appointments, and PatientRecord, using JSON APIs managed by REST Controllers. These controllers delegate business logic to the Service Layer, which interacts with both MySQL and MongoDB Repositories. Patients can register, view available doctor slots, book appointments, and access their prescriptions—stored as MongoDB Documents. Their interaction primarily involves fetching and storing structured and unstructured data across two databases, ensuring convenience and access to real-time medical services.

Doctor User Stories:
Doctors use the DoctorDashboard, routed through Thymeleaf Controllers, which call the Service Layer for backend logic. Doctors manage their availability, view scheduled appointments, and access patient records. Their appointment schedules are stored in MySQL Entities (Appointment), while patient prescriptions are accessed through the MongoDB Repository. Doctors rely on a unified dashboard that integrates with both relational and NoSQL databases to manage patient interactions efficiently, ensuring seamless diagnosis and consultation workflows.
