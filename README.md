# 📱 Concetto 

> **Official Android application for Concetto — the Techno-Management Fest of IIT (ISM) Dhanbad**

Concetto is a full-stack mobile platform built to provide participants with a centralized experience for discovering events, registering for competitions, managing teams, receiving announcements, exploring schedules, accessing fest information, and participating in the Campus Ambassador program.

The project consists of a native Android application backed by a RESTful Node.js/Express API and MongoDB database.

---

## ✨ Features

### 🏠 Home & Fest Information

* Fest homepage with featured content
* Event highlights and promotional banners
* Latest announcements
* Fest information and navigation
* Quick access to important sections

### 🎯 Events

Browse and explore different categories of Concetto events:

* Main-stage events
* Departmental events
* Club events
* Guest lectures
* Event schedules
* Event descriptions and guidelines
* Prize pool and organizer information
* External registration links
* Event posters and other media

### 👥 Team Management

Participants can manage their event teams directly through the application.

* Create a team
* Invite participants using email/user details
* View incoming invitations
* Accept or decline invitations
* View team information
* Track team members
* Enforce minimum and maximum team-size constraints
* Register a completed team for an event
* Prevent duplicate event registrations

### 🔐 Authentication & Account Management

The application provides a complete authentication workflow:

* User registration
* User login
* Email verification
* OTP generation and verification
* OTP resend functionality
* Password hashing
* JWT-based authentication
* Access and refresh tokens
* Protected API routes
* Logout
* User profile management

### 📢 Announcements & Notifications

Participants can stay updated with real-time fest information through:

* Dynamic announcements
* New-event announcements
* Firebase Cloud Messaging notifications
* Notification service integrated into the Android application

Administrators can also publish announcements through protected backend routes.

### 🏆 Campus Ambassador Program

Concetto includes a dedicated Campus Ambassador system:

* Campus Ambassador registration
* Unique referral codes
* Referral tracking
* Referral-based statistics
* Revenue tracking
* Ambassador leaderboard
* Mobile-optimized leaderboard API

### 🏫 Accommodation

The Android application includes an accommodation workflow for collecting participant stay information, including:

* Name
* Email
* Admission number
* Hostel
* Room number
* Contact number
* T-shirt/size information
* Supporting image

The accommodation form is integrated with Google Forms.

### 👨‍💼 Admin Functionality

Authorized administrators can:

* Add new events
* Publish announcements
* Automatically generate an announcement when a new event is added
* Manage fest-related backend content

---

# 🏗️ System Architecture

Concetto follows a client-server architecture:

```text
                    ┌──────────────────────┐
                    │    Android Client    │
                    │       Kotlin         │
                    └──────────┬───────────┘
                               │
                         Retrofit / HTTP
                               │
                               ▼
                    ┌──────────────────────┐
                    │    REST API Server    │
                    │   Node.js + Express   │
                    └──────────┬───────────┘
                               │
                    ┌──────────┴──────────┐
                    │                     │
                    ▼                     ▼
             ┌─────────────┐      ┌──────────────┐
             │  MongoDB    │      │ External     │
             │  Database   │      │ Services     │
             └─────────────┘      └──────────────┘
                                      │
                              ┌───────┼────────┐
                              ▼       ▼        ▼
                           Gmail   Firebase  Google
                            OTP       FCM      Forms
```

---

# 📱 Android Application

The Android client is developed natively using **Kotlin** and follows a structured architecture using Activities, Fragments, ViewModels, adapters, data models and service layers.

### Major Android Components


app/src/main/java/com/iitism/concetto_24/

├── auth/
│   ├── LoginFragment.kt
│   ├── SignupFragment.kt
│   ├── OtpFragment.kt
│   ├── LoginSignup.kt
│   └── OnBoardingFragment.kt
│
├── ui/
│   ├── HomeFragment.kt
│   ├── EventsFragment.kt
│   ├── ScheduleFragment.kt
│   ├── AnnouncementsFragment.kt
│   ├── CampusAmbassadorFragment.kt
│   ├── ProfileFragment.kt
│   ├── GalleryFragment.kt
│   ├── SponsorsFragment.kt
│   ├── CoreTeamFragment.kt
│   ├── GuestTalkFragment.kt
│   ├── MerchandiseFragment.kt
│   └── MainActivity.kt
│
├── ViewModel/
│   ├── CoreTeamViewModel.kt
│   ├── ScheduleViewModel.kt
│   └── SponsorViewModel.kt
│
├── retrofit/
│   ├── AnnouncementApi.kt
│   └── AnnouncementRetrofitInstance.kt
│
├── services/
│   ├── AuthClient.kt
│   ├── AuthService.kt
│   ├── GoogleFormApi.kt
│   └── MyFirebaseMessagingService.kt
│
├── models/
│   ├── User.kt
│   ├── EventsData.kt
│   ├── Announcement.kt
│   ├── LoginRequest.kt
│   ├── LoginResponse.kt
│   ├── RegisterRequest.kt
│   ├── RegisterResponse.kt
│   ├── LeaderboardEntry.kt
│   └── ...
│
└── adapter/
    ├── EventsAdapter.kt
    ├── ScheduleAdapter.kt
    ├── AnnouncementsRVAdapter.kt
    ├── GalleryAdapter.kt
    ├── SponsorRVAdapter.kt
    └── ...


# ⚙️ Backend

The backend is implemented using:

* **Node.js**
* **Express.js**
* **MongoDB**
* **Mongoose**
* **JWT**
* **bcrypt**
* **Nodemailer**
* **OTP Generator**
* **CORS**

The backend follows a modular structure separating routes, controllers, models, middleware and utility functions.


concetto-backend-24/

├── controllers/
│   ├── admin.js
│   ├── announcements.js
│   ├── auth.js
│   ├── campusAmbassador.js
│   ├── events.js
│   └── register.js
│
├── models/
│   ├── users.js
│   ├── events.js
│   ├── teams.js
│   ├── invites.js
│   ├── announcements.js
│   ├── notification.js
│   ├── otp.js
│   └── referralCode.js
│
├── routes/
│   ├── auth.js
│   ├── admin.js
│   ├── announcements.js
│   ├── campusAmbassador.js
│   └── register.js
│
├── middlewares/
│   ├── checkAdmin.js
│   └── deserializeUser.js
│
├── utils/
│   ├── jwtUtils.js
│   ├── otpSender.js
│   ├── refCode.js
│   ├── schema.js
│   └── CustomError.js
│
├── app.js
├── package.json
└── .env
```

---

# 🔌 REST API

## Authentication

| Method | Endpoint                | Description                |
| ------ | ----------------------- | -------------------------- |
| `POST` | `/api/register`         | Register a new user        |
| `POST` | `/api/login`            | Login                      |
| `POST` | `/api/logout`           | Logout                     |
| `POST` | `/api/verifyotp`        | Verify email OTP           |
| `POST` | `/api/verifyotp-mobile` | Verify OTP from mobile     |
| `POST` | `/api/resendotp`        | Resend OTP                 |
| `GET`  | `/api/protected`        | Access protected user data |

---

## Team & Event Registration

| Method | Endpoint                     | Description              |
| ------ | ---------------------------- | ------------------------ |
| `POST` | `/register/createTeam`       | Create a team            |
| `POST` | `/register/sendInvite`       | Invite a participant     |
| `POST` | `/register/acceptInvite`     | Accept team invitation   |
| `POST` | `/register/declineInvite`    | Decline invitation       |
| `GET`  | `/register/myInvites`        | Get received invitations |
| `GET`  | `/register/sentInvites`      | Get sent invitations     |
| `GET`  | `/register/teamInfo/:teamId` | Get team information     |
| `POST` | `/register/registerForEvent` | Register team for event  |

Protected team endpoints require user authentication.

---

## 📢 Announcements

| Method | Endpoint                          | Description                |
| ------ | --------------------------------- | -------------------------- |
| `GET`  | `/announcements/getAnnouncements` | Fetch latest announcements |

Administrators can publish announcements through the protected admin endpoint.

---

## 🏆 Campus Ambassador

| Method | Endpoint                               | Description                   |
| ------ | -------------------------------------- | ----------------------------- |
| `POST` | `/campusAmbassador/campus`             | Register as Campus Ambassador |
| `GET`  | `/campusAmbassador/leaderboard`        | Get ambassador leaderboard    |
| `GET`  | `/campusAmbassador/leaderboard-mobile` | Get mobile leaderboard        |

---

## 👨‍💼 Admin

| Method | Endpoint                 | Description             |
| ------ | ------------------------ | ----------------------- |
| `POST` | `/admin/addEvent`        | Add a new event         |
| `POST` | `/admin/addAnnouncement` | Publish an announcement |

Admin endpoints use authentication and administrator authorization middleware.

---

# 🔐 Authentication Flow

Concetto implements token-based authentication using JWT.

```text
User
 │
 ├── Register / Login
 │
 ▼
Node.js API
 │
 ├── Validate credentials
 ├── bcrypt password verification
 │
 ▼
Generate JWT
 │
 ├── Access Token
 └── Refresh Token
 │
 ▼
Android Application
 │
 └── Uses token for protected requests
```

Passwords are hashed using **bcrypt** before being stored in MongoDB.

Email verification uses an OTP workflow:

```text
Registration
     │
     ▼
Generate OTP
     │
     ▼
Store OTP + Expiration
     │
     ▼
Send OTP through Email
     │
     ▼
User enters OTP
     │
     ▼
Verify OTP
     │
     ▼
Account Verified
```

OTP expiration is enforced by the backend.

---

# 👥 Team Registration Flow

```text
User
 │
 ├── Select Event
 │
 ▼
Create Team
 │
 ▼
Team Leader
 │
 ├── Invite Participants
 │
 ▼
Participants
 │
 ├── Accept
 └── Decline
 │
 ▼
Team Reaches Valid Size
 │
 ▼
Team Leader Registers
 │
 ▼
Event Registration Confirmed
```

The backend validates:

* Team existence
* Team leader permissions
* Minimum team size
* Maximum team size
* Duplicate event registrations
* Duplicate invitations
* Already registered teams
* Invitation ownership

---

# 🗄️ Database Design

Concetto uses **MongoDB with Mongoose**.

### User

Stores participant information including:

* Username
* Email
* Password hash
* Phone number
* College
* IIT (ISM) status
* Verification status
* Campus Ambassador status
* Registered events
* Teams
* Referral information

### Event

Stores:

* Event name
* Type
* Description
* Rounds
* Guidelines
* Contact information
* Minimum team size
* Maximum team size
* Registered participants/teams

### Team

Stores:

* Team name
* Event
* Team leader
* Team members
* Registration status

### Invitation

Stores:

* Sender
* Recipient
* Team
* Invitation status

Supported states:

```text
pending
accepted
declined
```

### OTP

Stores:

* Email
* OTP
* Expiration time

### Referral Code

Stores:

* Referral code
* Ambassador
* Number of referrals
* Revenue

### Announcement

Stores:

* Title
* Body
* Timestamp

---

# 📡 Android ↔ Backend Communication

The Android application communicates with the backend using **Retrofit** and JSON-based REST APIs.

```text
Android Fragment
       │
       ▼
Service / Retrofit
       │
       ▼
HTTP Request
       │
       ▼
Express Router
       │
       ▼
Controller
       │
       ▼
Mongoose Model
       │
       ▼
MongoDB
       │
       ▼
JSON Response
       │
       ▼
Android UI
```

---

# 🔔 Push Notifications

The application integrates **Firebase Cloud Messaging (FCM)** for notifications.

The Android application includes a dedicated:

```text
MyFirebaseMessagingService
```

to receive and process Firebase messages.

Notifications can be used to keep participants informed about important fest updates.

---

# 🖼️ Static & Dynamic Content

The Android application also contains structured local JSON resources for fest content such as:

```text
assets/
├── club_events.json
├── concetto_events.json
├── departmental_events.json
├── guest_lectures.json
├── coreTeam.json
└── sponsorData.json
```

This allows structured event, sponsor, guest lecture and team information to be consumed by the application.

---

# 🛠️ Tech Stack

## Android

* **Kotlin**
* Android SDK
* XML Layouts
* AndroidX
* Material Components
* Navigation Component
* ViewBinding
* RecyclerView
* ViewModel
* Retrofit
* Gson
* OkHttp
* Glide
* Picasso
* Android Security Crypto

## Backend

* **Node.js**
* **Express.js**
* **MongoDB**
* **Mongoose**
* JWT
* bcrypt
* Nodemailer
* OTP Generator
* Joi
* CORS
* Cookie Parser
* dotenv

## Services & Integrations

* Firebase Cloud Messaging
* Google Forms
* Email OTP
* Cloudinary
* MongoDB Atlas

## Development Tools

* Android Studio
* VS Code
* Git
* GitHub
* Thunder Client

---

# 🚀 Getting Started

## Android Application

### Requirements

* Android Studio
* JDK
* Android SDK
* Android device or emulator

### Setup

```bash
git clone <repository-url>
```

Open the Android project in Android Studio and allow Gradle to synchronize the project.

Configure the required Firebase and backend settings before running the application.

---

# ⚙️ Backend Setup

### Requirements

* Node.js
* MongoDB / MongoDB Atlas
* npm

Navigate to the backend directory:

```bash
cd concetto-backend-24
```

Install dependencies:

```bash
npm install
```

Create a `.env` file containing the required environment variables:

```env
ATLAS_URL=<mongodb-connection-string>

ATS=<access-token-secret>
RTS=<refresh-token-secret>

MAIL_USER=<email>
MAIL_PASS=<email-app-password>

PORT=8000
```

Start the server:

```bash
npm start
```

The backend will start on the configured port.

---

# 🔒 Security Notes

Do **not** commit sensitive configuration files or credentials to GitHub.

In particular, keep the following private:

```text
.env
API keys
JWT secrets
Database credentials
Email credentials
Firebase private credentials
```

Use environment variables for secrets when deploying the backend.

---

# 📂 Repository Structure

If keeping Android and backend together:

```text
Concetto/
│
├── android/
│   └── Concetto-24/
│
├── backend/
│   └── concetto-backend-24/
│
└── README.md
```

Alternatively, Android and backend can be maintained as separate repositories.

---

# 📈 Key Engineering Highlights

* Built a **native Android application** using Kotlin.
* Implemented a **RESTful backend** using Node.js and Express.
* Designed MongoDB schemas using Mongoose.
* Implemented **JWT-based authentication** with protected routes.
* Added **OTP-based email verification**.
* Implemented complete **team creation, invitation and event registration workflows**.
* Developed a **Campus Ambassador referral and leaderboard system**.
* Integrated **Firebase Cloud Messaging** for notifications.
* Connected Android client APIs using **Retrofit, Gson and OkHttp**.
* Implemented role-based access for administrative operations.
* Integrated external services including **Google Forms, Cloudinary and email services**.

---

# 🎯 Project Impact

Concetto was designed as a centralized digital platform for fest participants, reducing the need to rely on multiple disconnected channels for event discovery, registration, team management, announcements and participant communication.

The platform combines a native Android client with a dedicated backend and database layer to support dynamic, authenticated and participant-specific functionality.

---

# 🔮 Future Improvements

Potential improvements include:

* Automated CI/CD pipeline
* Dockerized backend deployment
* Improved API documentation with Swagger/OpenAPI
* Automated unit and integration testing
* Database indexing and query optimization
* Advanced admin dashboard
* Real-time event updates using WebSockets
* Enhanced analytics for event participation
* Improved notification targeting
* Production monitoring and logging

---

## 👩‍💻 Contributors

Developed as part of the **Concetto — IIT (ISM) Dhanbad** technical team.

---

## 📄 License

This project is intended for educational, organizational and fest-related purposes.

© Concetto, IIT (ISM) Dhanbad
