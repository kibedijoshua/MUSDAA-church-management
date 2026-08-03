MUSDAA Fellowship Management System
Overview

The MUSDAA Fellowship Management System is a comprehensive web application designed to manage the operations of the Makerere University Seventh-day Adventist Association (MUSDAA). This system streamlines member management, attendance tracking, event coordination, prayer requests, sermon libraries, and contributions.
Features
Member Management

    User registration and authentication (JWT)

    Member profiles with church-specific information

    Role-based access (Admin, Pastor, Member, Visitor)

    Member directory and search

Attendance Tracking

    Service types (Kikoni, Afrostone, Nkrukote, Lumbox, Uh Mitchelex, Sabbath, etc.)

    Check-in system for services

    Attendance history per member

    Dashboard statistics (monthly attendance, growth percentage)

Events Management

    Create/Edit/Delete events (admin only)

    Events calendar view

    Members can RSVP to events

    RSVP tracking with guest count

    Event attendance reports

Prayer Wall

    Members can submit prayer requests

    Public/Private options

    "I prayed" button to show support

    Prayer count tracking

    Admin can mark prayers as answered with testimony

Sermons Library

    Sermon series organization

    Upload audio sermons (MP3)

    Sermon metadata (speaker, date, Bible verses, description)

    Audio player with play counter

    Filter by series

    Download count tracking

Contributions Management

    Contribution types (Tithe, Offering, Building Fund, etc.)

    Record contributions with payment methods

    PDF receipts generation

    Contribution statements

    Annual giving summary

Admin Dashboard

    Overview statistics

    Quick action buttons

    Recent prayer requests

    Upcoming events

    All management via Django Admin

Tech Stack
Backend
Technology	Purpose
Django 5.0	Web framework
Django REST Framework	API development
JWT Authentication	Secure authentication
SQLite	Database (development)
PostgreSQL	Database (production-ready)
Frontend
Technology	Purpose
React 18	UI framework
Vite	Build tool
Lucide React	Icon library
Axios	HTTP client
React Router	Navigation
Project Structure
text

musdaa-backend/
├── accounts/                 # User authentication
│   ├── models.py             # Custom User model
│   ├── serializers.py        # User serializers
│   ├── views.py              # Auth views (register, login, profile)
│   └── urls.py               # Auth URLs
├── members/                  # Member management
│   ├── models.py             # MemberProfile model
│   ├── serializers.py        # Member serializers
│   ├── views.py              # Member views
│   └── urls.py               # Member URLs
├── attendance/               # Attendance tracking
│   ├── models.py             # ServiceType, Service, Attendance
│   ├── serializers.py        # Attendance serializers
│   ├── views.py              # Check-in, stats, reports
│   └── urls.py               # Attendance URLs
├── events/                   # Event management
│   ├── models.py             # Event, EventRSVP
│   ├── serializers.py        # Event serializers
│   ├── views.py              # Event CRUD, RSVP
│   └── urls.py               # Event URLs
├── prayers/                  # Prayer wall
│   ├── models.py             # PrayerRequest, PrayerRecord
│   ├── serializers.py        # Prayer serializers
│   ├── views.py              # Submit, pray, list prayers
│   └── urls.py               # Prayer URLs
├── sermons/                  # Sermon library
│   ├── models.py             # SermonSeries, Sermon
│   ├── serializers.py        # Sermon serializers
│   ├── views.py              # Upload, list, listen
│   └── urls.py               # Sermon URLs
├── contributions/            # Contributions management
│   ├── models.py             # ContributionType, Contribution
│   ├── serializers.py        # Contribution serializers
│   ├── views.py              # Record, list, receipts
│   └── urls.py               # Contribution URLs
├── utils/                    # Utilities
│   ├── whatsapp.py           # WhatsApp API integration
│   ├── pdf_generator.py      # PDF receipt generator
│   └── permissions.py        # Custom permissions
└── church/                   # Project settings
    ├── settings.py           # Django settings
    └── urls.py               # Main URLs

church-frontend/
├── src/
│   ├── api/
│   │   └── client.js         # Axios configuration
│   ├── components/
│   │   ├── Layout/
│   │   │   ├── Sidebar.jsx
│   │   │   └── Header.jsx
│   │   └── UI/
│   │       ├── Card.jsx
│   │       ├── Badge.jsx
│   │       ├── Btn.jsx
│   │       ├── Input.jsx
│   │       ├── Modal.jsx
│   │       └── SummaryCard.jsx
│   ├── pages/
│   │   ├── LoginPage.jsx
│   │   ├── RegisterPage.jsx
│   │   ├── Dashboard.jsx
│   │   ├── ServicesPage.jsx
│   │   ├── EventsPage.jsx
│   │   ├── PrayerWallPage.jsx
│   │   ├── SermonsPage.jsx
│   │   ├── ProfilePage.jsx
│   │   └── AdminDashboardPage.jsx
│   ├── styles/
│   │   └── theme.js          # Color theme
│   ├── App.jsx               # Main app with routing
│   └── main.jsx              # Entry point
└── package.json              # Dependencies

Installation Guide
Prerequisites

    Python 3.12 or higher

    Node.js 18 or higher

    pip

    npm or yarn

Backend Setup
Step 1: Clone the Repository
bash

git clone https://github.com/yourusername/musdaa-management.git
cd musdaa-management/backend

Step 2: Create Virtual Environment

Windows:
bash

python -m venv venv
venv\Scripts\activate

Mac/Linux:
bash

python3 -m venv venv
source venv/bin/activate

Step 3: Install Dependencies
bash

pip install -r requirements.txt

Step 4: Configure Environment Variables

Create a .env file in the backend root:
env

SECRET_KEY=your-secret-key-here
DEBUG=True
DATABASE_URL=sqlite:///db.sqlite3

Step 5: Run Migrations
bash

python manage.py makemigrations
python manage.py migrate

Step 6: Create Superuser
bash

python manage.py createsuperuser

Step 7: Run the Server
bash

python manage.py runserver

Backend will be available at: http://127.0.0.1:8000/
Frontend Setup
Step 1: Navigate to Frontend Directory
bash

cd ../frontend

Step 2: Install Dependencies
bash

npm install

Step 3: Configure API URL

Create a .env file in the frontend root:
env

VITE_API_URL=http://127.0.0.1:8000/api/

Step 4: Run Development Server
bash

npm run dev

Frontend will be available at: http://localhost:5173/
API Endpoints
Authentication
Method	Endpoint	Description
POST	/api/auth/register/	Register new user
POST	/api/auth/login/	Login (returns JWT)
POST	/api/auth/token/refresh/	Refresh JWT token
GET	/api/auth/profile/	Get user profile
PUT	/api/auth/profile/	Update user profile
Members
Method	Endpoint	Description
GET	/api/members/profile/	Get member profile
PUT	/api/members/profile/	Update member profile
Attendance
Method	Endpoint	Description
GET	/api/attendance/service-types/	List service types
GET	/api/attendance/services/	List services
POST	/api/attendance/checkin/	Check in to service
GET	/api/attendance/my-attendance/	My attendance history
GET	/api/attendance/stats/	Dashboard statistics
Events
Method	Endpoint	Description
GET	/api/events/	List events
POST	/api/events/	Create event (admin)
POST	/api/events/rsvp/	RSVP to event
Prayers
Method	Endpoint	Description
GET	/api/prayers/	List prayer requests
POST	/api/prayers/	Submit prayer request
POST	/api/prayers/pray/	Pray for a request
Sermons
Method	Endpoint	Description
GET	/api/sermons/	List sermons
GET	/api/sermons/series/	List sermon series
POST	/api/sermons/{id}/listen/	Record listen
Contributions
Method	Endpoint	Description
GET	/api/contributions/	List contributions
POST	/api/contributions/	Record contribution (admin)
GET	/api/contributions/receipt/{id}/	Download PDF receipt
Testing Credentials
Role	Username	Password
Admin	admin	admin123
Member	testmember	Test@123
User Roles
Role	Permissions
Admin	Full access to everything
Pastor	Can manage events, prayers, sermons
Member	Can check in, RSVP, submit prayers
Visitor	Limited access (public view only)
Mobile Responsive

The frontend is fully responsive and works on:

    Desktop

    Tablet

    Mobile

Security Features

    JWT authentication with refresh tokens

    Role-based access control

    Password validation

    CORS configuration

    SQL injection protection (Django ORM)

    XSS protection

Contributing

    Fork the repository

    Create a feature branch: git checkout -b feature/amazing-feature

    Commit your changes: git commit -m 'Add some amazing feature'

    Push to the branch: git push origin feature/amazing-feature

    Open a Pull Request

License

This project is licensed under the MIT License. See the LICENSE file for details.
Support

For support, email: menhyajoshua@gmail.com
Acknowledgments

    MUSDAA (Makerere University Seventh-day Adventist Association)

    All contributors and testers

Quick Start

Clone and setup everything:
bash

git clone https://github.com/yourusername/musdaa-management.git
cd musdaa-management
./setup.sh    # Or setup.bat for Windows

Made with love for MUSDAA
