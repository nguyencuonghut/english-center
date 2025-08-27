Software Requirements Specification

Language Center Management System
1. Introduction
1.1 Purpose

This document defines the functional and non-functional requirements for the Language Center Management System (LCMS). It is intended to guide stakeholders and the development team in building a professional, scalable solution to manage multiple branches, staff, courses, classes, students, attendance, payroll, and communications.
1.2 Document Conventions

    Requirements are labeled with unique identifiers: FR- for functional and NFR- for non-functional.

    Roles are emphasized in bold (e.g., Admin).

1.3 Intended Audience and Reading Suggestions

    Owners/Managers: focus on sections 2 and 3 for operational overview.

    Developers/Testers: review all sections, particularly 3 and 5.

    Future Integrators: consult sections 4 and 5 for interfaces and constraints.

1.4 Product Scope

LCMS streamlines operations of language center chains:

    Centralized management of branches, staff, rooms, courses, classes.

    Student enrollment, tuition handling, attendance tracking, payroll.

    Notifications via email/Zalo and financial reporting.

    Modular design prepared for mobile apps, payment gateways, and accounting integration.

1.5 References

    Laravel Framework Documentation.

    OWASP Security Guidelines.

    ISO/IEC 9126 Software Quality Standard.

2. Overall Description
2.1 Product Perspective

LCMS is a web-based, multi-branch system built on Laravel MVC architecture. It integrates RESTful APIs (GraphQL optional) for future mobile or third-party interaction and leverages queues for asynchronous tasks.
2.2 Product Functions

    Branch creation and manager assignment.

    Teacher profiles, class schedules, and payroll.

    Course catalog and class management with room scheduling.

    Student enrollment, tuition tracking, and class transfers.

    Attendance and reporting dashboards.

    Role-based access control and notifications.

2.3 User Classes and Characteristics
Role	Characteristics	Privileges
Admin	System owners or HQ staff	Full access to all modules, system configuration
Manager	Oversees a branch	Manage local classes, teachers, students, finances
Teacher	Conducts classes	View assigned classes, record attendance, student remarks
Parent/Student (future)	Read-only interface	Access attendance, tuition status, comments
2.4 Operating Environment

    Server: PHP 8.x, Laravel 10+, MySQL/PostgreSQL, Redis for cache/queue.

    Client: Modern browsers (Chrome, Firefox, Edge, Safari).

    Deployment: Linux servers or cloud platforms with CI/CD pipelines.

2.5 Design and Implementation Constraints

    Passwords hashed using bcrypt/argon2.

    Use of Laravel Eloquent ORM and middleware.

    No overlapping class schedules for a room or teacher.

2.6 Assumptions and Dependencies

    Stable internet connection for email/Zalo services.

    External services (email, Zalo, payment gateways) provide required APIs.

    Future mobile app or CRM integration via REST/GraphQL endpoints.

3. System Features
3.1 Branch Management

Description: Create, modify, lock, and delete branches, each assigned a manager.

    FR-1: System shall allow Admin to create branches with name and address.

    FR-2: System shall enable assigning a manager (user) to a branch.

    FR-3: Branch list view shall display branch name, address, and status.

3.2 Manager Management

Description: CRUD operations for branch managers.

    FR-4: System shall store manager details: full name, phone, email, address.

    FR-5: Admin can create, update, lock, or delete manager accounts.

    FR-6: Managers can manage only their assigned branch.

3.3 Teacher Management

Description: Maintain teacher profiles and assignments.

    FR-7: System shall store teacher details (code, personal info, qualifications).

    FR-8: Teachers can be assigned to multiple classes.

    FR-9: Attendance per class session shall record pay rate for payroll.

3.4 Course Management

Description: Catalog of language courses categorized by age group and language.

    FR-10: System shall support CRUD for courses with fields: name, age group, language, description.

    FR-11: Courses can be opened or closed.

3.5 Class Management

Description: Define classes under courses and branches.

    FR-12: Each class shall have a unique code, name, schedule, tuition fee, start date, duration, and status.

    FR-13: Each class shall link to a course, branch, teacher, and room.

    FR-14: System shall allow class sessions to be postponed or canceled; attendance and payroll must reflect changes.

    FR-15: Students may join late or transfer; tuition calculations shall consider remaining sessions and fees.

3.6 Room Management

Description: Manage classroom inventory and scheduling.

    FR-16: Rooms shall have code, name, and capacity.

    FR-17: System shall prevent assigning multiple classes to the same room and time slot.

3.7 Student Enrollment & Tuition

Description: Register students, track payments, and handle transfers.

    FR-18: System shall record student personal and contact information.

    FR-19: Students can enroll in classes at any point; system calculates prorated tuition.

    FR-20: Transfers shall reconcile paid tuition between old and new classes (refund or additional payment).

    FR-21: Payment history and outstanding balance per student shall be tracked.

3.8 Attendance & Payroll

Description: Track teaching sessions and compute teacher wages.

    FR-22: Attendance records shall capture class, teacher, date, status, and pay amount per session.

    FR-23: Manager can submit attendance; Admin approves payroll.

    FR-24: System shall import payroll data from Excel and email payslips to teachers.

3.9 Notifications & Communication

Description: Notify students/teachers via email and Zalo.

    FR-25: System shall send tuition reminders and class end notifications to students.

    FR-26: Teachers can send end-of-course remarks and video links to students.

    FR-27: Notifications can be scheduled or queued for bulk dispatch.

3.10 Dashboard & Reporting

Description: Provide analytics and financial reporting.

    FR-28: Admin dashboard shall display counts of branches, managers, teachers, students, classes, total tuition, near-expiry enrollments, and outstanding debts.

    FR-29: Branch-level dashboards available to managers.

    FR-30: Export reports to PDF/Excel by date range.

3.11 Role & Access Control

    FR-31: Users shall be assigned roles (Admin, Manager, Teacher).

    FR-32: Role-based middleware shall restrict access to resources.

3.12 Authentication

    FR-33: System shall provide login via email and password.

    FR-34: Password reset via email link.

3.13 Accounting Module (Optional Initial Scope)

    FR-35: Maintain ledger accounts and transactions (revenue/expense) per branch.

    FR-36: Record payment and expense entries linked to tuition and payroll.

3.14 Future Extensions

    Parent/student portal.

    Online classes with virtual meeting links and materials.

    Integration with payment gateways and CRM.

4. External Interface Requirements
4.1 User Interfaces

    Responsive web UI with localized (vi/en) support.

    Dashboard with charts (using charting libraries) for admins/managers.

4.2 API Interfaces

    RESTful APIs returning JSON.

    OAuth2/JWT or token-based authentication for API clients.

    Webhooks for Zalo and email services.

4.3 Hardware Interfaces

    None specific beyond standard web servers.

4.4 Software Interfaces

    Email SMTP or transactional email services.

    Zalo Official Account API.

    Optional: Payment gateway APIs, Excel import/export libraries.

4.5 Communications Interfaces

    HTTPS for all web/API traffic.

    Queue system for background jobs (Redis).

5. Non-Functional Requirements
5.1 Performance Requirements

    NFR-1: Page responses shall complete within 2 seconds under normal load.

    NFR-2: System shall handle concurrent operations from multiple branches without conflict.

5.2 Security Requirements

    NFR-3: Passwords must be hashed; sensitive data encrypted at rest.

    NFR-4: Implement audit logs for critical operations.

    NFR-5: Role-based access and CSRF protection enforced.

5.3 Reliability & Availability

    NFR-6: Daily automated backups with restore procedures.

    NFR-7: System availability target of 99% uptime.

5.4 Maintainability

    NFR-8: Code follows PSR-12 standards and is covered by unit/feature tests.

    NFR-9: CI/CD pipeline automatically runs tests and deployments.

5.5 Usability

    NFR-10: Interfaces shall be intuitive and provide validation errors in Vietnamese and English.

    NFR-11: Documentation and user manuals provided for each role.

5.6 Internationalization

    NFR-12: System prepared for multiple languages and currencies.

5.7 Scalability

    NFR-13: Architecture supports addition of new branches without code changes.

    NFR-14: Modular structure for future microservice separation.

6. Other Requirements

    NFR-15: Logging and monitoring to centralize error and performance metrics with alerting.

    NFR-16: Compliance with local tax/accounting regulations for financial reports.

    NFR-17: Data privacy compliance (e.g., GDPR or local equivalents).

7. Appendices
7.1 Glossary

    Branch: Physical location of the language center.

    Class: Specific scheduled group of students for a course.

    Manager: Person responsible for operations of a branch.

    Tuition: Fee charged to a student for attending a class.

7.2 Open Issues

    Integration details for payment gateways.

    Final choice of notification providers (email, Zalo).

    Parent/student portal scope.
