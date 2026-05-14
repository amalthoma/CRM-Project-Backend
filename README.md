# CRM Workflow Management System - Backend

FastAPI backend for managing digital marketing and software project workflows.

## Week 1 & Week 2 Implementation (Completed)

### Features Implemented
- **Day 1**: FastAPI project setup & MySQL database connection
- **Day 2**: JWT authentication system (login/register)
- **Day 3**: User CRUD APIs with role-based access
- **Day 4**: Roles & Departments management APIs
- **Day 5**: Customer management APIs
- **Day 6**: Enquiry management APIs
- **Day 7**: Enquiry assignment & status update logic
- **Day 8**: Quotation APIs with status workflow
- **Day 9**: Quotation approve/reject/confirm logic
- **Day 10**: Project APIs with quotation linkage
- **Day 11**: Task APIs with department & staff assignment
- **Day 12**: Task assignment & status update endpoints
- **Day 13**: Task logs for hour tracking
- **Day 14**: Daily reports & Feedback APIs

### Project Structure
```
CRM/
├── app/
│   ├── __init__.py
│   └── main.py              # FastAPI application entry point
├── api/
│   └── v1/
│       ├── api.py           # API router
│       └── endpoints/
│           ├── auth.py      # Authentication endpoints
│           ├── users.py     # User CRUD
│           ├── roles.py     # Role management
│           ├── departments.py
│           ├── customers.py
│           ├── enquiries.py
│           ├── quotations.py
│           ├── projects.py
│           ├── tasks.py
│           ├── reports.py
│           └── feedback.py
├── core/
│   ├── config.py            # Configuration settings
│   └── security.py          # JWT & password hashing
├── db/
│   └── session.py           # Database session
├── models/
│   ├── __init__.py
│   ├── base.py              # Base model
│   ├── user.py              # User, Role, Department models
│   ├── customer.py          # Customer model
│   ├── enquiry.py           # Enquiry model
│   ├── quotation.py         # Quotation model
│   ├── project.py           # Project model
│   ├── task.py              # Task & TaskLog models
│   ├── report.py            # DailyReport model
│   └── feedback.py          # Feedback model
├── schemas/
│   ├── __init__.py
│   ├── user.py              # User schemas
│   ├── customer.py          # Customer schemas
│   ├── enquiry.py           # Enquiry schemas
│   ├── quotation.py         # Quotation schemas
│   ├── project.py           # Project schemas
│   ├── task.py              # Task schemas
│   ├── report.py            # Report schemas
│   └── feedback.py          # Feedback schemas
├── init_db.py               # Database initialization script
├── requirements.txt         # Python dependencies
├── .env.example             # Environment variables template
└── README.md
```

## Installation

### Prerequisites
- Python 3.8+
- MySQL 8.0+

### Setup Steps

1. **Clone the repository**
   ```bash
   cd c:/Users/Amal\ Thomas/CRM
   ```

2. **Create virtual environment**
   ```bash
   python -m venv venv
   venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Configure environment variables**
   ```bash
   cp .env.example .env
   ```
   Edit `.env` with your database credentials:
   ```
   DATABASE_URL=mysql+pymysql://root:your_password@localhost:3306/crm_db
   SECRET_KEY=your-secret-key-here
   ALGORITHM=HS256
   ACCESS_TOKEN_EXPIRE_MINUTES=30
   ```

5. **Create MySQL database**
   ```sql
   CREATE DATABASE crm_db;
   ```

6. **Initialize database**
   ```bash
   python init_db.py
   ```
   This creates:
   - Default roles (Admin, Manager, Staff)
   - Default departments (Marketing, Development, Design)
   - Default admin user (admin@crm.com / admin123)

7. **Run the server**
   ```bash
   uvicorn app.main:app --reload
   ```

   Server will run at: `http://localhost:8000`

## API Documentation

Once the server is running, access:
- Swagger UI: `http://localhost:8000/docs`
- ReDoc: `http://localhost:8000/redoc`

## API Endpoints

### Authentication
- `POST /api/v1/auth/login` - User login
- `POST /api/v1/auth/register` - User registration

### Users
- `POST /api/v1/users/` - Create user
- `GET /api/v1/users/` - List users
- `GET /api/v1/users/{id}` - Get user by ID
- `PUT /api/v1/users/{id}` - Update user
- `DELETE /api/v1/users/{id}` - Delete user

### Roles
- `POST /api/v1/roles/` - Create role
- `GET /api/v1/roles/` - List roles
- `GET /api/v1/roles/{id}` - Get role by ID
- `PUT /api/v1/roles/{id}` - Update role
- `DELETE /api/v1/roles/{id}` - Delete role

### Departments
- `POST /api/v1/departments/` - Create department
- `GET /api/v1/departments/` - List departments
- `GET /api/v1/departments/{id}` - Get department by ID
- `PUT /api/v1/departments/{id}` - Update department
- `DELETE /api/v1/departments/{id}` - Delete department

### Customers
- `POST /api/v1/customers/` - Create customer
- `GET /api/v1/customers/` - List customers
- `GET /api/v1/customers/{id}` - Get customer by ID
- `PUT /api/v1/customers/{id}` - Update customer
- `DELETE /api/v1/customers/{id}` - Delete customer

### Enquiries
- `POST /api/v1/enquiries/` - Create enquiry
- `GET /api/v1/enquiries/` - List enquiries
- `GET /api/v1/enquiries/{id}` - Get enquiry by ID
- `PUT /api/v1/enquiries/{id}` - Update enquiry
- `PUT /api/v1/enquiries/{id}/assign` - Assign enquiry to staff
- `PUT /api/v1/enquiries/{id}/status` - Update enquiry status
- `DELETE /api/v1/enquiries/{id}` - Delete enquiry

### Quotations
- `POST /api/v1/quotations/` - Create quotation
- `GET /api/v1/quotations/` - List quotations
- `GET /api/v1/quotations/{id}` - Get quotation by ID
- `PUT /api/v1/quotations/{id}` - Update quotation
- `PUT /api/v1/quotations/{id}/approve` - Approve quotation
- `PUT /api/v1/quotations/{id}/reject` - Reject quotation
- `PUT /api/v1/quotations/{id}/confirm` - Confirm quotation
- `DELETE /api/v1/quotations/{id}` - Delete quotation

### Projects
- `POST /api/v1/projects/` - Create project (requires confirmed quotation)
- `GET /api/v1/projects/` - List projects
- `GET /api/v1/projects/{id}` - Get project by ID
- `PUT /api/v1/projects/{id}` - Update project
- `PUT /api/v1/projects/{id}/status` - Update project status
- `DELETE /api/v1/projects/{id}` - Delete project

### Tasks
- `POST /api/v1/tasks/` - Create task
- `GET /api/v1/tasks/` - List tasks
- `GET /api/v1/tasks/project/{project_id}` - Get tasks by project
- `GET /api/v1/tasks/{id}` - Get task by ID
- `PUT /api/v1/tasks/{id}` - Update task
- `PUT /api/v1/tasks/{id}/assign` - Assign task to staff
- `PUT /api/v1/tasks/{id}/status` - Update task status
- `POST /api/v1/tasks/{id}/log-hours` - Log hours for task
- `GET /api/v1/tasks/{id}/logs` - Get task logs
- `DELETE /api/v1/tasks/{id}` - Delete task

### Daily Reports
- `POST /api/v1/reports/` - Create daily report
- `GET /api/v1/reports/` - List reports
- `GET /api/v1/reports/user/{user_id}` - Get reports by user
- `GET /api/v1/reports/{id}` - Get report by ID
- `PUT /api/v1/reports/{id}` - Update report
- `DELETE /api/v1/reports/{id}` - Delete report

### Feedback
- `POST /api/v1/feedback/` - Create feedback
- `GET /api/v1/feedback/` - List feedback
- `GET /api/v1/feedback/project/{project_id}` - Get feedback by project
- `GET /api/v1/feedback/{id}` - Get feedback by ID
- `PUT /api/v1/feedback/{id}` - Update feedback
- `DELETE /api/v1/feedback/{id}` - Delete feedback

### Status Logs
- `POST /api/v1/status-logs/` - Create status log
- `GET /api/v1/status-logs/` - List status logs
- `GET /api/v1/status-logs/module/{module_name}` - Get logs by module
- `GET /api/v1/status-logs/record/{module_name}/{record_id}` - Get logs by record
- `GET /api/v1/status-logs/{id}` - Get status log by ID
- `DELETE /api/v1/status-logs/{id}` - Delete status log

### Notifications
- `POST /api/v1/notifications/` - Create notification
- `GET /api/v1/notifications/` - List notifications
- `GET /api/v1/notifications/user/{user_id}` - Get notifications by user
- `GET /api/v1/notifications/user/{user_id}/unread` - Get unread notifications
- `GET /api/v1/notifications/{id}` - Get notification by ID
- `PUT /api/v1/notifications/{id}` - Update notification
- `PUT /api/v1/notifications/{id}/mark-read` - Mark notification as read
- `DELETE /api/v1/notifications/{id}` - Delete notification

## Database Schema

### Tables Created
- `users` - Staff/user accounts
- `roles` - User roles (Admin, Manager, Staff)
- `departments` - Company departments
- `customers` - Customer information
- `enquiries` - Lead enquiries with status tracking
- `quotations` - Quotations with approval workflow
- `projects` - Projects linked to quotations
- `tasks` - Hour-based task allocation
- `task_logs` - Hour tracking per task
- `daily_reports` - Staff daily work reports
- `feedback` - Customer feedback (1-5 rating)
- `status_logs` - Audit trail for status changes
- `notifications` - User notifications (read/unread)

## Workflow

1. **Customer → Enquiry**: Create customer, then enquiry
2. **Enquiry → Quotation**: Create quotation from enquiry
3. **Quotation → Project**: Approve quotation, then confirm to create project
4. **Project → Tasks**: Split project into hour-based tasks
5. **Tasks → Task Logs**: Staff log hours against tasks
6. **Project → Feedback**: Customer provides feedback
7. **Status Changes**: All status changes tracked in status_logs
8. **Notifications**: Users receive notifications for relevant updates

## Technologies Used

- **FastAPI** - Modern Python web framework
- **SQLAlchemy** - ORM for database operations
- **PyMySQL** - MySQL database driver
- **Pydantic** - Data validation
- **JWT** - Authentication
- **Passlib** - Password hashing with bcrypt

## Development Notes

- All endpoints return JSON responses
- CORS enabled for all origins (configure for production)
- Database auto-creates tables on startup
- JWT tokens expire after 30 minutes (configurable)
- Date format for reports/logs: YYYYMMDD (integer)
- Rating scale for feedback: 1-5
