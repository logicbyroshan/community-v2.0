# 📁 Project Structure

This document provides a detailed overview of the Rise Together project structure, explaining the purpose of each directory and file.

---

## 🌲 Directory Tree

```
Rise-Together/
│
├── 📁 accounts/                    # User authentication & profile management
├── 📁 community/                   # Community features (blogs, projects, activities)
├── 📁 feed/                        # Social feed functionality
├── 📁 riseapp/                     # Core application features
├── 📁 config/                      # Project configuration
├── 📁 static/                      # Static files (CSS, JS, Images)
├── 📁 templates/                   # HTML templates
├── 📁 media/                       # User-uploaded files
├── 📁 screenshots/                 # Project screenshots
├── 📁 docs/                        # Documentation files
├── 📄 manage.py                    # Django management script
├── 📄 requirements.txt             # Python dependencies
├── 📄 db.sqlite3                   # SQLite database (development)
├── 📄 README.md                    # Main documentation
├── 📄 ABOUT.md                     # Detailed project information
├── 📄 TECH_STACK.md                # Technology stack details
├── 📄 SETUP_GUIDE.md               # Installation guide
├── 📄 PROJECT_STRUCTURE.md         # This file
├── 📄 CONTRIBUTING.md              # Contribution guidelines
├── 📄 LICENSE                      # MIT License
└── 📄 .gitignore                   # Git ignore rules
```

---

## 📂 Core Django Apps

### 1. `accounts/` - User Authentication & Profiles

Handles user registration, authentication, and profile management.

```
accounts/
├── migrations/              # Database migrations
│   ├── __init__.py
│   ├── 0001_initial.py
│   └── ...
├── management/              # Custom management commands
│   └── commands/
├── __init__.py
├── admin.py                # Admin interface configuration
├── apps.py                 # App configuration
├── forms.py                # User forms (login, register, profile)
├── models.py               # User profile model
├── signals.py              # Django signals (auto-create profiles)
├── urls.py                 # URL routing
├── views.py                # View functions
└── tests.py                # Unit tests
```

**Key Models:**
- `Profile`: Extended user profile with bio, skills, social links, profile picture

**Key Views:**
- User registration (`join`)
- Login/logout
- Profile view and edit
- Password reset functionality

**Key Features:**
- Custom user profile with additional fields
- Profile picture upload
- Social media links
- Activity score tracking
- Email verification ready

---

### 2. `community/` - Community Features

Manages blogs, projects, and activities.

```
community/
├── migrations/              # Database migrations
├── __init__.py
├── admin.py                # Admin configuration
├── apps.py                 # App configuration
├── models.py               # Blog, Project, Activity models
├── urls.py                 # URL routing
├── views.py                # View functions
└── tests.py                # Unit tests
```

**Key Models:**
- `Blog`: Blog posts with title, content, author, tags
- `Project`: Community projects with tech stack, links
- `Activity`: Community events and challenges

**Key Views:**
- Blog listing and detail pages
- Project showcase
- Activity calendar
- Category filtering

**Key Features:**
- Rich text content (TinyMCE integration)
- Tag system for categorization
- Reading time estimation
- Featured content
- Technology tags for projects

---

### 3. `feed/` - Social Feed

Social networking features including posts, comments, and likes.

```
feed/
├── migrations/              # Database migrations
├── __init__.py
├── admin.py                # Admin configuration
├── apps.py                 # App configuration
├── forms.py                # Post and comment forms
├── models.py               # Feed post, comment, like models
├── urls.py                 # URL routing
├── views.py                # View functions
└── tests.py                # Unit tests
```

**Key Models:**
- `FeedPost`: User posts with different types (normal, blog, project)
- `PostComment`: Comments on posts
- `PostLikeNew`: Post likes/reactions
- `CommentLikeNew`: Comment likes
- `Hashtag`: Hashtag system

**Key Features:**
- Multiple post types
- Comment system
- Like/unlike functionality
- Hashtag support
- User feed timeline

---

### 4. `riseapp/` - Core Application

Main application handling homepage, resources, and general features.

```
riseapp/
├── migrations/              # Database migrations
├── __init__.py
├── admin.py                # Admin configuration
├── apps.py                 # App configuration
├── models.py               # Contact, Newsletter, Resource models
├── urls.py                 # URL routing
├── views.py                # View functions
└── tests.py                # Unit tests
```

**Key Models:**
- `Contact`: Contact form submissions
- `Newsletter`: Newsletter subscriptions
- `Testimonial`: User testimonials
- `FAQ`: Frequently asked questions
- `Resource`: Learning resources

**Key Views:**
- Homepage
- Resources library
- Contact form
- Newsletter subscription
- About page

**Key Features:**
- Contact form with email notifications
- Newsletter management
- Resource categorization
- FAQ system
- Testimonial showcase

---

## ⚙️ Configuration

### `config/` - Project Settings

```
config/
├── __init__.py
├── settings.py             # Main Django settings
├── urls.py                 # Root URL configuration
├── asgi.py                 # ASGI configuration (async)
└── wsgi.py                 # WSGI configuration (production)
```

**settings.py includes:**
- Installed apps configuration
- Middleware settings
- Database configuration
- Static files settings
- Media files settings
- Email configuration
- Security settings
- Template configuration

**urls.py includes:**
- Root URL patterns
- App URL includes
- Admin URL
- Media files serving (development)

---

## 🎨 Frontend Files

### `static/` - Static Assets

```
static/
├── css/
│   ├── base.css            # Global styles, animations
│   ├── home.css            # Homepage styles
│   ├── profile.css         # Profile page styles
│   ├── auth.css            # Authentication styles
│   └── edit_profile.css    # Profile editing styles
├── js/
│   └── auth.js             # Authentication interactions
└── images/
    └── logo.png            # Community logo
```

**CSS Organization:**
- **base.css**: Global styles, utilities, animations, navbar, footer
- **home.css**: Homepage-specific styles and sections
- **profile.css**: User profile layout and components
- **auth.css**: Login/register page styles
- **edit_profile.css**: Profile editing form styles

**JavaScript:**
- Vanilla JS for interactivity
- Form validation
- Dynamic content loading
- Smooth scrolling
- Modal interactions

---

### `templates/` - HTML Templates

```
templates/
├── base.html                   # Base template (navbar, footer, scripts)
├── Home.html                   # Homepage template
├── accounts/
│   ├── join.html               # Registration page
│   ├── login.html              # Login page
│   ├── profile.html            # User profile display
│   ├── profile_sidebar.html    # Profile sidebar component
│   ├── edit_profile.html       # Profile editing
│   ├── settings.html           # User settings
│   ├── password_reset.html     # Password reset request
│   ├── password_reset_done.html
│   ├── password_reset_confirm.html
│   └── password_reset_complete.html
├── feed/
│   ├── feed_list.html          # Social feed listing
│   ├── feed_list_new.html      # Updated feed design
│   ├── post_detail.html        # Single post view
│   ├── post_detail_new.html    # Updated post detail
│   ├── create_post.html        # Create post form
│   ├── create_normal_post.html
│   ├── create_blog_post.html
│   └── create_project_post.html
└── Pages/
    ├── blogs.html              # Blog listing
    ├── blog-detail.html        # Individual blog post
    ├── projects.html           # Projects showcase
    ├── projects_old.html
    ├── activities.html         # Community activities
    ├── activities_old.html
    └── resources.html          # Learning resources
```

**Template Structure:**
- **base.html**: Master template with common elements
- **App-specific templates**: Organized by Django app
- **Component templates**: Reusable template parts
- **Old templates**: Kept for reference (can be removed)

---

## 📦 Media Files

### `media/` - User Uploads

```
media/
├── profile_pics/           # User profile pictures
└── feed/
    └── media/              # Feed post images/media
```

**Configuration:**
- Handled by Django's media file system
- Pillow for image processing
- Automatic thumbnail generation
- File size limits enforced

---

## 📸 Documentation Assets

### `screenshots/` - Project Screenshots

```
screenshots/
├── RiseThumb.png           # Main thumbnail
├── Home.png                # Homepage screenshot
├── about.png
├── mission.png
├── projects.png
├── activity.png
├── article.png
├── team.png
├── leaderboard.png
├── achievements.png
├── resources.png
├── faq.png
└── feedback.png
```

Used in README and documentation.

---

### `docs/` - Additional Documentation

```
docs/
├── INDEX.md                # Documentation index
└── screenshots/
    └── README.md
```

Extended documentation and guides.

---

## 🔧 Configuration Files

### `manage.py`
Django's command-line utility for administrative tasks.

**Common commands:**
```bash
python manage.py runserver      # Start development server
python manage.py migrate        # Apply database migrations
python manage.py makemigrations # Create new migrations
python manage.py createsuperuser # Create admin user
python manage.py test           # Run tests
python manage.py collectstatic  # Collect static files
```

---

### `requirements.txt`
Lists all Python package dependencies.

**Key packages:**
- Django==5.2.5
- Pillow (image processing)
- django-tinymce (rich text editor)
- Additional utility packages

**Usage:**
```bash
pip install -r requirements.txt
```

---

### `db.sqlite3`
SQLite database file (development).

**Contains:**
- User accounts and profiles
- Blog posts and projects
- Comments and likes
- Activities and resources
- All application data

**Note**: Excluded from version control via `.gitignore`

---

### `.gitignore`
Specifies files to ignore in version control.

**Ignores:**
- `venv/` - Virtual environment
- `db.sqlite3` - Database file
- `*.pyc` - Python bytecode
- `__pycache__/` - Python cache
- `.env` - Environment variables
- `staticfiles/` - Collected static files
- `media/` - User uploads

---

## 🗂️ Database Schema

### User & Authentication
- `auth_user` - Django default user model
- `accounts_profile` - Extended profile information

### Community Content
- `community_blog` - Blog posts
- `community_project` - Project showcases
- `community_activity` - Community events

### Social Feed
- `feed_feedpost` - User posts
- `feed_postcomment` - Comments
- `feed_postlikenew` - Post likes
- `feed_commentlikenew` - Comment likes
- `feed_hashtag` - Hashtags

### Core App
- `riseapp_contact` - Contact submissions
- `riseapp_newsletter` - Newsletter subscribers
- `riseapp_resource` - Learning resources
- `riseapp_faq` - FAQ entries
- `riseapp_testimonial` - User testimonials

---

## 🔄 Application Flow

### User Journey
1. **Visit Homepage** → `riseapp/views.py`
2. **Register Account** → `accounts/views.py` → Create User & Profile
3. **Browse Content** → `community/views.py` → Display blogs/projects
4. **Engage** → `feed/views.py` → Create posts, comment, like
5. **Access Resources** → `riseapp/views.py` → View resources

### Data Flow
```
User Request → URLs → Views → Models → Database
                              ↓
                          Templates → Response
```

---

## 📊 App Dependencies

```
config (root project)
├── accounts (user authentication)
├── community (content management)
├── feed (social features)
└── riseapp (core features)
```

All apps are loosely coupled and can function independently.

---

## 🔐 Security Considerations

### Protected Directories
- `media/` - User uploads (validate file types)
- `static/` - Served separately in production
- `venv/` - Never commit to version control

### Sensitive Files
- `.env` - Environment variables
- `db.sqlite3` - Database (use PostgreSQL in production)
- Secret keys and API credentials

### Security Features
- CSRF protection enabled
- Password hashing (PBKDF2)
- SQL injection protection (ORM)
- XSS protection
- Clickjacking protection

---

## 🧪 Testing Structure

### Test Files
Each app has a `tests.py` file:
- `accounts/tests.py` - User and profile tests
- `community/tests.py` - Blog, project tests
- `feed/tests.py` - Feed functionality tests
- `riseapp/tests.py` - Core feature tests

### Test Coverage
Run tests with:
```bash
python manage.py test
coverage run --source='.' manage.py test
coverage report
```

---

## 📝 Code Organization Principles

### Django Best Practices
- ✅ One app, one purpose
- ✅ Models in `models.py`
- ✅ Business logic in `views.py` or separate services
- ✅ Forms in `forms.py`
- ✅ URLs in `urls.py`
- ✅ Templates organized by app

### File Naming
- Snake_case for Python files
- PascalCase for class names
- lowercase for templates
- kebab-case for URLs

### Code Style
- PEP 8 compliance
- Meaningful variable names
- Docstrings for functions/classes
- Comments for complex logic

---

## 🚀 Scalability Considerations

### Current Structure
- Modular app design
- Separated concerns
- Template inheritance
- Static file management

### Future Enhancements
- API layer (Django REST Framework)
- Caching (Redis)
- Task queue (Celery)
- Microservices architecture
- Containerization (Docker)

---

## 📚 Additional Resources

### Django Documentation
- [Django Project Structure](https://docs.djangoproject.com/en/stable/intro/tutorial01/)
- [Django Apps](https://docs.djangoproject.com/en/stable/ref/applications/)
- [Django Templates](https://docs.djangoproject.com/en/stable/topics/templates/)

### Best Practices
- [Two Scoops of Django](https://www.feldroy.com/books/two-scoops-of-django-3-x)
- [Django Design Patterns](https://django-design-patterns.readthedocs.io/)

---

<div align="center">

**Well-organized code is the foundation of maintainable software**

[🏠 Back to README](README.md) | [📖 About](ABOUT.md) | [🚀 Setup Guide](SETUP_GUIDE.md)

</div>
