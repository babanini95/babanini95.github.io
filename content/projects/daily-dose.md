+++
title = 'Daily Dose'
date = 2025-08-10T17:40:33+08:00
draft = false
author = "Abdullah Robbani"
tags = ["python", "flask", "hackathon"]
categories = ["team project"]
+++

[**DailyDose**](https://github.com/freeCodeCamp-2025-Summer-Hackathon/indigo-class) is a full stack web application designed to help users cultivate positivity and mindfulness through daily affirmations. Built with Python (Flask), PostgreSQL, and jinja templating, the platform enables users to discover, save, and manage affirmations, as well as create custom categories and receive daily motivational emails.

This team project was developed during one month of [freeCodeCamp Summer Hackathon 2025](https://github.com/freeCodeCamp-2025-Summer-Hackathon).
<!--more-->
![homepage screenshot](https://raw.githubusercontent.com/babanini95/babanini95.github.io/refs/heads/main/content/projects/images/daily-dose-homepage.png)
___

## Key Features

- **User Authentication:** Secure registration, login, and password management.
- **Affirmation Management:** Add, edit, pin, and favorite affirmations. Browse, filter, and search affirmations by category.
- **Custom Categories:** Users can create and manage their own affirmation categories.
- **Daily Affirmation Email:** Optional daily email delivery of a motivational quote.
- **Admin Dashboard:** Admins can manage users, affirmations, categories, and monitor email delivery.
- **Responsive UI:** Clean, accessible design with mobile-first CSS and interactive JavaScript.
- **Dockerized Deployment:** Easily reproducible environment using Docker and Docker Compose.
- **Database Seeding:** Sample data for quick setup and testing.

___

## Technical Stack

- **Backend:** Python, Flask, SQLAlchemy
- **Frontend:** Jinja, HTML, CSS, JavaScript
- **Database:** PostgreSQL
- **DevOps:** Docker, Git
- **Environment:** uv

___

## Team and Contributions

The team was consists of 9 members (including me) from around the world. We distributed the development as follows:

- Frontend: 5 members
- Backend: 4 members (including me)

Aside from frontend and backend, some members are also contributed to DevOps, design product, documentation, and project management.

___

## Repository Structure

```markdown
indigo-class/
├── app/
│   ├── __init__.py          # Flask app factory
│   ├── controllers/
│   │   ├── root.py          # Root blueprint and routes
│   │   ├── auth.py          # Authentication blueprint and routes
│   │   ├── affirmations.py  # Affirmation blueprint and routes
│   │   ├── categories.py    # Affirmation categories blueprint and routes
│   │   ├── user.py          # User blueprint and routes
│   │   └── admin/
│   │       ├── dashboard.py    # Admin dashboard blueprint and routes
│   │       └── user.html       # User management blueprint and routes
│   ├── static/              # Static files (CSS, JS, images)
│   └── templates/           # HTML templates
│       ├── base.html a      # Base template
│       ├── _header.html     # Base template's header partial
│       ├── _footer.html     # Base template's footer partial
│       ├── home/
│       │   ├── index.html       # Home page template
│       │   └── dashboard.html   # User dashboard template
│       ├── auth/
│       │   ├── register.html                 # Account registration template
│       │   ├── login.html                    # Login template
│       │   ├── reset_password_request.html   # Password reset request template
│       │   ├── new_password.html             # New password input template
│       │   └── user_settings.html            # User settings template
│       ├── affirmations/
│       │   ├── index.html   # Affirmation list template
│       │   ├── add.html     # Affirmation submission template
│       │   └── edit.html    # Affirmation edit template
│       ├── categories/
│       │   ├── list.html    # Affirmation categories list template
│       │   ├── add.html     # Affirmation category submission template
│       │   └── edit.html    # Affirmation category edit template
│       └── admin/
│           ├── dashboard.html      # Admin dashboard template
│           ├── users.html          # Users management template
│           ├── affirmations.html   # Affirmation management template
│           ├── categories.html     # Categories management template
│           ├── analytics.html      # Analytics template
│           └── settings.html       # Admin settings template
├── main.py                  # Application entry point
├── pyproject.toml           # Project configuration
├── Dockerfile               # Instructions for building the Docker image
├── docker-compose.yml       # Requirements for building the Docker image
└── README.md
```

___

## Future Plans

After the hackathon, we decided to continue the project and add more features. But we have not yet decided on the next steps.

___

You can check the repo here: *[github.com/freeCodeCamp-2025-Summer-Hackathon/indigo-class](https://github.com/freeCodeCamp-2025-Summer-Hackathon/indigo-class)*
