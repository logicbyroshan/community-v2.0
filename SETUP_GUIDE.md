# 🚀 Complete Setup Guide

This comprehensive guide will walk you through setting up Rise Together on your local machine, from installation to deployment.

---

## 📋 Table of Contents

1. [Prerequisites](#prerequisites)
2. [Local Development Setup](#local-development-setup)
3. [Environment Configuration](#environment-configuration)
4. [Database Setup](#database-setup)
5. [Static Files Configuration](#static-files-configuration)
6. [Running the Application](#running-the-application)
7. [Creating Admin User](#creating-admin-user)
8. [Testing](#testing)
9. [Troubleshooting](#troubleshooting)
10. [Production Deployment](#production-deployment)

---

## 📦 Prerequisites

### Required Software

#### 1. Python 3.8 or Higher

**Check if Python is installed:**
```bash
python --version
# or
python3 --version
```

**Install Python:**
- **Windows**: Download from [python.org](https://www.python.org/downloads/)
- **macOS**: 
  ```bash
  brew install python@3.11
  ```
- **Linux (Ubuntu/Debian)**:
  ```bash
  sudo apt update
  sudo apt install python3 python3-pip python3-venv
  ```

#### 2. Git

**Check if Git is installed:**
```bash
git --version
```

**Install Git:**
- **Windows**: Download from [git-scm.com](https://git-scm.com/download/win)
- **macOS**: 
  ```bash
  brew install git
  ```
- **Linux**:
  ```bash
  sudo apt install git
  ```

#### 3. pip (Python Package Manager)

Usually comes with Python. Verify:
```bash
pip --version
# or
pip3 --version
```

**Upgrade pip:**
```bash
python -m pip install --upgrade pip
```

---

## 💻 Local Development Setup

### Step 1: Clone the Repository

```bash
# Using HTTPS
git clone https://github.com/logicbyroshan/social-community-platform.git

# Or using SSH (if you have SSH keys set up)
git clone git@github.com:logicbyroshan/social-community-platform.git

# Navigate to project directory
cd social-community-platform
```

### Step 2: Create Virtual Environment

A virtual environment isolates project dependencies.

#### Windows (PowerShell)
```powershell
# Create virtual environment
python -m venv venv

# Activate virtual environment
venv\Scripts\activate

# You should see (venv) in your terminal prompt
```

#### Windows (Command Prompt)
```cmd
# Create virtual environment
python -m venv venv

# Activate virtual environment
venv\Scripts\activate.bat
```

#### macOS/Linux
```bash
# Create virtual environment
python3 -m venv venv

# Activate virtual environment
source venv/bin/activate

# You should see (venv) in your terminal prompt
```

**Note**: To deactivate the virtual environment later, simply run:
```bash
deactivate
```

### Step 3: Install Dependencies

With your virtual environment activated:

```bash
# Install all required packages
pip install -r requirements.txt

# If you encounter any errors, try upgrading pip first
pip install --upgrade pip
pip install -r requirements.txt
```

**Common Dependencies Installed:**
- Django 5.2.5
- Pillow (for image handling)
- Other project-specific packages

---

## ⚙️ Environment Configuration

### Step 1: Create Environment File

Create a `.env` file in the root directory:

```bash
# Create .env file
touch .env  # macOS/Linux
# or
New-Item .env  # Windows PowerShell
```

### Step 2: Configure Environment Variables

Add the following to your `.env` file:

```env
# Django Secret Key
SECRET_KEY=your-secret-key-here-change-this-in-production

# Debug Mode (set to False in production)
DEBUG=True

# Allowed Hosts (comma-separated)
ALLOWED_HOSTS=localhost,127.0.0.1

# Database Configuration (SQLite by default)
DATABASE_URL=sqlite:///db.sqlite3

# Email Configuration (for password reset functionality)
EMAIL_BACKEND=django.core.mail.backends.console.EmailBackend
EMAIL_HOST=smtp.gmail.com
EMAIL_PORT=587
EMAIL_USE_TLS=True
EMAIL_HOST_USER=your-email@gmail.com
EMAIL_HOST_PASSWORD=your-app-specific-password

# Static and Media Files
STATIC_URL=/static/
MEDIA_URL=/media/
```

### Step 3: Generate Secret Key

Generate a secure secret key for Django:

```python
# Run this in Python shell
python -c "from django.core.management.utils import get_random_secret_key; print(get_random_secret_key())"
```

Copy the output and replace `your-secret-key-here-change-this-in-production` in your `.env` file.

### Step 4: Email Configuration (Optional for Development)

For development, the console backend is fine. For production or testing email:

**Gmail Setup:**
1. Enable 2-Factor Authentication in your Google Account
2. Generate an App Password:
   - Go to Google Account Settings > Security
   - Select "App passwords"
   - Generate a new app password
   - Use this password in `EMAIL_HOST_PASSWORD`

**Alternative Email Providers:**
- **SendGrid**: Professional email service
- **Amazon SES**: AWS email service
- **Mailgun**: Developer-friendly email API

---

## 🗄️ Database Setup

### Step 1: Apply Migrations

Migrations create the database schema:

```bash
# Create migration files (if needed)
python manage.py makemigrations

# Apply migrations to database
python manage.py migrate
```

**Expected Output:**
```
Running migrations:
  Applying contenttypes.0001_initial... OK
  Applying auth.0001_initial... OK
  Applying accounts.0001_initial... OK
  Applying community.0001_initial... OK
  ...
```

### Step 2: Verify Database Creation

You should see a `db.sqlite3` file in your project root.

```bash
# Check if database exists
ls db.sqlite3  # macOS/Linux
dir db.sqlite3  # Windows
```

---

## 📁 Static Files Configuration

### Step 1: Collect Static Files

```bash
# Collect all static files into STATIC_ROOT
python manage.py collectstatic

# Type 'yes' when prompted
```

This gathers all static files (CSS, JS, images) into one location for serving.

### Step 2: Verify Static Files

Check that static files are in the `staticfiles` directory (or wherever your `STATIC_ROOT` points).

---

## 🏃 Running the Application

### Step 1: Start Development Server

```bash
python manage.py runserver
```

**Expected Output:**
```
Watching for file changes with StatReloader
Performing system checks...

System check identified no issues (0 silenced).
November 15, 2025 - 10:30:00
Django version 5.2.5, using settings 'config.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CTRL-BREAK.
```

### Step 2: Access the Application

Open your web browser and navigate to:
- **Homepage**: http://127.0.0.1:8000/
- **Admin Panel**: http://127.0.0.1:8000/admin/

### Step 3: Custom Port (Optional)

To run on a different port:
```bash
python manage.py runserver 8080
```

Access at: http://127.0.0.1:8080/

---

## 👤 Creating Admin User

### Create Superuser Account

```bash
python manage.py createsuperuser
```

**You'll be prompted for:**
- Username
- Email address
- Password (typed twice, won't be visible)

**Example:**
```
Username: admin
Email address: admin@risetogether.tech
Password: ********
Password (again): ********
Superuser created successfully.
```

### Access Admin Panel

1. Navigate to: http://127.0.0.1:8000/admin/
2. Log in with your superuser credentials
3. You can now manage:
   - Users
   - Blog posts
   - Projects
   - Activities
   - Resources
   - Newsletter subscriptions

---

## 🧪 Testing

### Run All Tests

```bash
python manage.py test
```

### Run Specific App Tests

```bash
# Test accounts app
python manage.py test accounts

# Test community app
python manage.py test community

# Test riseapp
python manage.py test riseapp
```

### Run with Coverage

```bash
# Install coverage (if not already installed)
pip install coverage

# Run tests with coverage
coverage run --source='.' manage.py test

# Generate coverage report
coverage report

# Generate HTML coverage report
coverage html
# Open htmlcov/index.html in browser
```

---

## 🐛 Troubleshooting

### Common Issues and Solutions

#### Issue 1: Module Not Found

**Error**: `ModuleNotFoundError: No module named 'django'`

**Solution**:
```bash
# Make sure virtual environment is activated
# You should see (venv) in prompt

# Reinstall dependencies
pip install -r requirements.txt
```

#### Issue 2: Port Already in Use

**Error**: `Error: That port is already in use.`

**Solution**:
```bash
# Use a different port
python manage.py runserver 8080

# Or kill the process using port 8000
# Windows:
netstat -ano | findstr :8000
taskkill /PID <PID> /F

# macOS/Linux:
lsof -ti:8000 | xargs kill -9
```

#### Issue 3: Database Migrations Error

**Error**: Migration conflicts or errors

**Solution**:
```bash
# Reset migrations (WARNING: This will delete data)
# Delete db.sqlite3
rm db.sqlite3  # macOS/Linux
del db.sqlite3  # Windows

# Delete migration files (keep __init__.py)
# Then recreate migrations
python manage.py makemigrations
python manage.py migrate
```

#### Issue 4: Static Files Not Loading

**Error**: CSS/JS files not loading

**Solution**:
```bash
# Collect static files again
python manage.py collectstatic --noinput

# Make sure DEBUG=True in development
# Check STATIC_URL in settings.py
```

#### Issue 5: Permission Denied (Media Files)

**Error**: Cannot upload images

**Solution**:
```bash
# Create media directory
mkdir media
mkdir media/profile_pics

# Set permissions (Linux/macOS)
chmod -R 755 media/
```

---

## 🌐 Production Deployment

### Pre-Deployment Checklist

- [ ] Set `DEBUG = False` in production
- [ ] Configure `ALLOWED_HOSTS` with your domain
- [ ] Use a production database (PostgreSQL recommended)
- [ ] Set up proper email backend
- [ ] Configure static file serving (WhiteNoise or CDN)
- [ ] Set up media file storage (AWS S3, Cloudinary)
- [ ] Enable HTTPS/SSL
- [ ] Configure environment variables securely
- [ ] Set up logging and monitoring
- [ ] Create database backups strategy

### Production Settings

Create a separate settings file or modify `config/settings.py`:

```python
# Production settings
DEBUG = False
ALLOWED_HOSTS = ['yourdomain.com', 'www.yourdomain.com']

# Security Settings
SECURE_SSL_REDIRECT = True
SESSION_COOKIE_SECURE = True
CSRF_COOKIE_SECURE = True
SECURE_BROWSER_XSS_FILTER = True
SECURE_CONTENT_TYPE_NOSNIFF = True
X_FRAME_OPTIONS = 'DENY'

# Database (PostgreSQL example)
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': os.getenv('DB_NAME'),
        'USER': os.getenv('DB_USER'),
        'PASSWORD': os.getenv('DB_PASSWORD'),
        'HOST': os.getenv('DB_HOST'),
        'PORT': os.getenv('DB_PORT', '5432'),
    }
}
```

### Deployment Platforms

#### Heroku

```bash
# Install Heroku CLI
# Login to Heroku
heroku login

# Create new app
heroku create your-app-name

# Set environment variables
heroku config:set SECRET_KEY=your-secret-key
heroku config:set DEBUG=False

# Add PostgreSQL
heroku addons:create heroku-postgresql:hobby-dev

# Deploy
git push heroku main

# Run migrations
heroku run python manage.py migrate

# Create superuser
heroku run python manage.py createsuperuser
```

#### DigitalOcean

- Use App Platform for easy deployment
- Or set up a Droplet with Nginx + Gunicorn
- Follow DigitalOcean's Django deployment guide

#### AWS, Google Cloud, Azure

- Use their respective app hosting services
- Configure environment variables in platform settings
- Set up database instances (RDS, Cloud SQL, Azure DB)
- Configure static file storage (S3, Cloud Storage, Azure Blob)

### Using Gunicorn (Production Server)

```bash
# Install Gunicorn
pip install gunicorn

# Run with Gunicorn
gunicorn config.wsgi:application --bind 0.0.0.0:8000
```

### Nginx Configuration (Example)

```nginx
server {
    listen 80;
    server_name yourdomain.com;

    location /static/ {
        alias /path/to/staticfiles/;
    }

    location /media/ {
        alias /path/to/media/;
    }

    location / {
        proxy_pass http://127.0.0.1:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

---

## 📚 Additional Resources

### Documentation
- [Django Official Documentation](https://docs.djangoproject.com/)
- [Django Deployment Checklist](https://docs.djangoproject.com/en/stable/howto/deployment/checklist/)

### Video Tutorials
- Search for "Django deployment" on YouTube
- Platform-specific deployment guides

### Community Support
- Django Forum
- Stack Overflow
- Rise Together Discord

---

## 🔄 Keeping Your Installation Updated

### Update Dependencies

```bash
# Activate virtual environment
source venv/bin/activate  # or venv\Scripts\activate on Windows

# Update pip
pip install --upgrade pip

# Update all packages
pip install --upgrade -r requirements.txt

# Update specific package
pip install --upgrade django
```

### Pull Latest Changes

```bash
# Fetch latest changes
git pull origin main

# Install any new dependencies
pip install -r requirements.txt

# Apply new migrations
python manage.py migrate

# Collect new static files
python manage.py collectstatic --noinput
```

---

## 🆘 Getting Help

If you encounter issues:

1. **Check Documentation**: Review this guide and Django docs
2. **Search Issues**: Look for similar issues on GitHub
3. **Ask Community**: Post in our Discord or discussions
4. **Create Issue**: Open a detailed issue on GitHub
5. **Contact Us**: Email contact@risetogether.tech

---

<div align="center">

**Happy Coding! 🚀**

[🏠 Back to README](README.md) | [📖 About](ABOUT.md) | [🛠️ Tech Stack](TECH_STACK.md)

</div>
