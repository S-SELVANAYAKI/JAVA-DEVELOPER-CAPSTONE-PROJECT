##admin user story

Title:
As an admin, I want to log into the portal with my username and password, so that I can securely manage the platform.

Acceptance Criteria:

The login page must accept valid username and password.

Incorrect credentials should display an error message.

Successful login should redirect the admin to the dashboard.

Priority: High
Story Points: 3
Notes:

Ensure password encryption and secure authentication practices are in place.

Implement login attempt throttling or CAPTCHA after multiple failed attempts.

User Story 2
Title:
As an admin, I want to log out of the portal, so that I can protect access to the system after use.

Acceptance Criteria:

Logout option must be available on every page after login.

Clicking logout should terminate the session and redirect to login page.

Any further access attempt without logging in must be redirected to login page.

Priority: Medium
Story Points: 2
Notes:

Invalidate session/token upon logout.

Consider adding an auto-logout feature for inactivity.

User Story 3
Title:
As an admin, I want to add doctors to the portal, so that they can be registered and visible to patients.

Acceptance Criteria:

Admin can access a form to enter doctor's details.

Doctor information must be validated and saved to the database.

A success message should confirm doctor addition.

Priority: High
Story Points: 5
Notes:

Fields may include name, specialty, availability, contact info.

Duplicate checks for email or license number.

User Story 4
Title:
As an admin, I want to delete a doctor's profile from the portal, so that I can manage outdated or incorrect entries.

Acceptance Criteria:

Admin should see a list of registered doctors.

Each profile should have a delete button with confirmation.

Deleted profiles should no longer appear in user or admin view.

Priority: High
Story Points: 3
Notes:

Consider soft delete (marking inactive) instead of hard delete.

Provide an audit trail for admin actions.

User Story 5
Title:
As an admin, I want to run a stored procedure in MySQL CLI to get the number of appointments per month, so that I can track usage statistics.

Acceptance Criteria:

Stored procedure exists and returns monthly appointment counts.

Admin can execute it from the CLI and view results.

The output should be sorted by month.

Priority: Medium
Story Points: 2
Notes:

Include error handling if stored procedure fails.

Optional: expose this data in a dashboard for easier access.


##PATIENT STORIES

Title:
As a patient, I want to view a list of doctors without logging in, so that I can explore available options before registering.

Acceptance Criteria:

A public doctor directory should be accessible without login.

Each doctor profile must display key details like name, specialty, and availability.

There should be a call-to-action to sign up or log in for appointment booking.

Priority: High
Story Points: 3
Notes:

Consider search and filter functionality (e.g., by specialty or location).

Profiles should limit sensitive info until after login.

User Story 2
Title:
As a patient, I want to sign up using my email and password, so that I can book appointments.

Acceptance Criteria:

A sign-up form should collect email and password.

The system must validate the input and store encrypted credentials.

Successful sign-up should redirect to the patient dashboard.

Priority: High
Story Points: 2
Notes:

Include email uniqueness check and confirmation message.

Use secure password practices (e.g., min length, symbols).

User Story 3
Title:
As a patient, I want to log into the portal, so that I can manage my bookings.

Acceptance Criteria:

Patients can log in using their registered email and password.

On success, the patient should be redirected to their personalized dashboard.

Incorrect credentials should prompt an appropriate error.

Priority: High
Story Points: 2
Notes:

Implement session/token-based authentication.

Provide "forgot password" functionality.

User Story 4
Title:
As a patient, I want to log out of the portal, so that I can secure my account.

Acceptance Criteria:

Logout option should be available after login.

Clicking logout should terminate the session and return to homepage/login page.

No protected routes should be accessible after logout.

Priority: Medium
Story Points: 1
Notes:

Consider auto-logout for inactivity.

Show confirmation message upon successful logout.

User Story 5
Title:
As a patient, I want to log in and book an hour-long appointment, so that I can consult with a doctor.

Acceptance Criteria:

Logged-in patients should see available time slots for each doctor.

Patient must be able to select a slot and confirm the booking.

System should prevent double-booking and confirm the appointment.

Priority: High
Story Points: 5
Notes:

Send appointment confirmation via email.

Optional: Add calendar integration or reminders.

User Story 6
Title:
As a patient, I want to view my upcoming appointments, so that I can prepare accordingly.

Acceptance Criteria:

Patients should see a list of upcoming appointments on their dashboard.

Each entry should show date, time, doctor’s name, and meeting details.

The list must be updated dynamically when appointments are added/cancelled.

Priority: Medium
Story Points: 3


Notes:

Provide sorting by date.

Optional: allow cancellation or rescheduling.

##DOCTOR STORIES

Title:
As a doctor, I want to log into the portal, so that I can manage my appointments.

Acceptance Criteria:

Doctors can log in using their registered credentials.

Successful login should redirect to the doctor dashboard.

Incorrect login should display a clear error message.

Priority: High
Story Points: 2
Notes:

Use secure authentication and session management.

Include account lockout or CAPTCHA on multiple failed attempts.

User Story 2
Title:
As a doctor, I want to log out of the portal, so that I can protect my data.

Acceptance Criteria:

Logout option should be available on all pages after login.

Logging out should end the session and redirect to login or home.

Protected routes should no longer be accessible after logout.

Priority: Medium
Story Points: 1
Notes:

Consider session timeout for added security.

Confirmation message after logout improves UX.

User Story 3
Title:
As a doctor, I want to view my appointment calendar, so that I can stay organized.

Acceptance Criteria:

Doctors can access a calendar view of upcoming appointments.

Appointments should display patient name, date, and time.

Calendar should allow navigation by week and month.

Priority: High
Story Points: 4
Notes:

Consider integration with Google Calendar or exporting to .ics.

Use visual cues (colors, icons) for appointment status.

User Story 4
Title:
As a doctor, I want to mark my unavailability, so that patients can only see available slots.

Acceptance Criteria:

Doctors can select date ranges/times to mark as unavailable.

Marked time slots should not be shown as available to patients.

System should automatically block new bookings during unavailable times.

Priority: High
Story Points: 3
Notes:

Allow both one-time and recurring unavailability settings.

Display a summary of blocked time slots for confirmation.

User Story 5
Title:
As a doctor, I want to update my profile with specialization and contact information, so that patients have up-to-date information.

Acceptance Criteria:

Editable profile fields include name, specialization, contact info, and bio.

Changes should be saved to the database and reflected in patient view.

Input validation must ensure only valid formats are accepted.

Priority: Medium
Story Points: 2
Notes:

Provide option to upload profile picture.

Log edits for admin visibility and accountability.

User Story 6
Title:
As a doctor, I want to view the patient details for upcoming appointments, so that I can be prepared.

Acceptance Criteria:

Appointment entries should display patient name, age, gender, and contact info.

Notes or past history (if available) should be visible to the doctor.

Information should be viewable in both list and calendar views.

Priority: High
Story Points: 3
Notes:

Secure sensitive patient information with role-based access.

Optional: allow doctors to add consultation notes post-appointment.
