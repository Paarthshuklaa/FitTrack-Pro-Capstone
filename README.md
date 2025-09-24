# FitTrack Pro: A Boutique Fitness Studio Management System 🏋️‍♀️

## 🚀 The Challenge

This project is designed for the **TCS Last Mile Program - Phase 2 Capstone**. It aims to solve the operational challenges faced by a growing boutique fitness studio named "Synergy Fitness," which specializes in group classes and personal training.

> As Synergy Fitness's client base expands, their reliance on manual and disconnected systems (spreadsheets, paper forms, text messages) has become a major bottleneck, leading to inefficiencies and a poor customer experience.

Their key pain points are:

- **Inefficient Client Management:** Client data, membership status, and purchased session packages are tracked in a complex, error-prone spreadsheet.
- **Chaotic Class Scheduling:** Bookings are managed via phone calls and a shared calendar, frequently causing overbooked classes and scheduling conflicts.
- **Lack of Performance Tracking:** Management has no easy way to analyze class popularity, trainer performance, or client attendance trends.
- **Disconnected Trainer Workflow:** Trainers lack a central system to view their daily schedules or log important notes on client progress.
- **Manual Billing and Renewals:** Tracking used sessions and prompting clients for package renewals is a manual process, resulting in lost revenue opportunities.

## ✨ The Solution

**FitTrack Pro** is a custom Salesforce application built to be the central nervous system for Synergy Fitness. The platform will automate and connect all core operations, from client onboarding and class scheduling to progress tracking and package renewals. It will serve as the single source of truth for all studio data, providing a seamless experience for staff and delivering actionable insights to management.

## 🛠️ Core Features & Technical Implementation

### 📊 Data Model

The application is built on a foundation of standard and custom objects to create a robust, relational data model.

| Object Name | Object Type | Purpose | Key Relationships |
| :--- | :--- | :--- | :--- |
| **Contact** | Standard | Stores all information about a client. | Primary object for clients. |
| **Task** | Standard | Used to create automated follow-up tasks for trainers. | Related to `Contact`. |
| **Fitness Class** | Custom | Defines the classes offered (e.g., "HIIT Burn," time, trainer). | - |
| **Session Package**| Custom | Defines purchasable packages (e.g., "10 Class Pass," price). | - |
| **Client Package**| Custom | Links a Client to a purchased Session Package. Tracks `Sessions Remaining`. | Master-Detail to `Contact` and Lookup to `Session Package`. |
| **Class Attendance**| Custom | A junction object logging a Client's attendance in a specific class. | Master-Detail to `Contact` and Master-Detail to `Fitness Class`. |

### ⚙️ Automation

Declarative and programmatic automation will be used to streamline key business processes.

- **Screen Flow:** A guided flow for front-desk staff to easily register a new client and sell them their first `Session Package`, creating both a `Contact` and `Client Package` record in one seamless process.
- **Record-Triggered Flow:** When a `Class Attendance` record is created, a flow will automatically trigger to find the client's active `Client Package` and decrement the `Sessions Remaining` field by one.
- **Validation Rule:** A validation rule on the `Class Attendance` object will prevent a new attendance record from being saved if the client's `Sessions Remaining` on their active package is `0`.
- **Apex Trigger:** An `after update` trigger on the `Client Package` object. When the `Sessions Remaining` field is updated to `0`, the trigger will automatically create a `Task` for the client's primary trainer with the subject "Follow up with [Client Name] to renew their package."

### 🔒 Security Model

A role-based security model will ensure that users can only access the data relevant to their job function.

- **Studio Manager Profile/Role:** Has full "View All" and "Modify All" access to all custom objects, including financial reports and dashboards.
- **Trainer Profile/Role:** Can only see and manage the `Contacts` (clients) and `Fitness Classes` assigned to them. Access will be controlled via Sharing Rules. They will not be able to see financial data.
- **Front Desk Profile:** Can create and manage `Contacts`, `Client Packages`, and `Class Attendance` but cannot see sensitive financial reports or dashboards.

### 📈 Reports & Dashboards

Custom analytics will provide management with 360-degree visibility into the studio's performance.

- **Reports:**
    - "Most Popular Classes by Attendance"
    - "Monthly Revenue from Package Sales"
    - "Clients with Low Remaining Sessions" (for proactive renewal outreach)
- **Dashboard:**
    - A "Studio Performance" dashboard with components visualizing class capacity rates, revenue trends, and client retention metrics.

### 🖥️ Custom User Interface (LWC)

A custom Lightning Web Component will provide a superior user experience for trainers.

- **Component Name:** "My Day at a Glance"
- **Purpose:** This LWC will be placed on the Trainer's Homepage and will display a clean, calendar-like list of the trainer's scheduled classes and personal training sessions for the current day. Each entry will be clickable to show a list of registered clients.

## 💻 Technology Stack

- Salesforce Platform (Lightning Experience)
- Apex
- Lightning Web Components (LWC)
- SOQL & SOSL
- Salesforce Declarative Automation Tools (Flow, Approval Processes)

## 🚧 Project Status

- [x] Phase 1: Problem Understanding & Industry Analysis
- [ ] Phase 2: Organizational Setup & Salesforce Edition
- [ ] Phase 3: Data Modeling & Relationships
- [ ] Phase 4: Process Automation (Declarative)
- [ ] Phase 5: Process Automation (Programmatic)
- [ ] Phase 6: Lightning App Building
- [ ] Phase 7: Integration & External Access
- [ ] Phase 8: Data Management & Deployment
- [ ] Phase 9: Reports & Dashboards
- [ ] Phase 10: Final Presentation & Handoff
![Uploading image.png…]()
