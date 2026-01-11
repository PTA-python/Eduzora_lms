"# Eduzora LMS - Learning Management System

A complete online learning management system built with PHP, featuring course management, student enrollment, instructor dashboard, payment processing, and more.

## Table of Contents

- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Configuration](#configuration)
- [Database Setup](#database-setup)
- [Usage Guide](#usage-guide)
- [Project Structure](#project-structure)

## Features

- **Admin Dashboard** - Complete admin panel for managing users, courses, categories, FAQs, and languages
- **Instructor Module** - Instructors can create, edit, and manage courses with curriculum and lessons
- **Student Dashboard** - Students can enroll in courses, track progress, and leave reviews
- **Course Management** - Create courses with videos, lessons, and structured curriculum
- **Payment Integration** - Stripe and PayPal integration for course purchases
- **Messaging System** - Communication between students and instructors
- **Wishlist & Cart** - Students can add courses to wishlist and cart
- **Coupon System** - Instructors can create discount coupons
- **Order Management** - Complete order tracking with invoices
- **Email Notifications** - Automated email notifications for registration, password reset, etc.
- **User Roles** - Admin, Instructor, and Student roles with specific permissions
- **Responsive Design** - Mobile-friendly interface

## Requirements

- **PHP** - 7.4 or higher
- **MySQL** - 5.7 or higher
- **Web Server** - Apache with mod_rewrite enabled
- **Composer** - For PHP dependency management
- **Extensions** - PDO, OpenSSL, cURL, GD Library

## Installation

### 1. Clone or Download the Project

```bash
cd your-project-directory
```

### 2. Install Dependencies

```bash
composer install
```

This will install required packages:
- Stripe PHP SDK
- Omnipay (PayPal)
- PHPMailer for email functionality

### 3. Configure Web Server

For Apache, ensure `.htaccess` support is enabled:
- Enable `mod_rewrite` module
- Allow `.htaccess` files in your document root

### 4. Create Database

Create a new MySQL database:

```sql
CREATE DATABASE eduzora_lms;
```

Import the database schema:

```bash
mysql -u root -p eduzora_lms < database.sql
```

## Configuration

### Critical: Update Configuration Files

You **MUST** update the following configuration files with your actual credentials before running the application:

#### 1. Database Configuration (`config/config.php`)

Open `config/config.php` and update with your database details:

```php
<?php
$dbhost = 'localhost';      // Your database host
$dbname = 'eduzora_lms';    // Your database name
$dbuser = 'root';           // Your database username
$dbpass = '';               // Your database password
```

#### 2. Payment Gateway Configuration (`config/config_payment.php`)

**IMPORTANT**: Add your actual payment credentials. These are required for payment processing.

##### PayPal Configuration

1. Go to [PayPal Developer Dashboard](https://developer.paypal.com/)
2. Create a REST API app and copy your Client ID and Secret
3. Update `config/config_payment.php`:

```php
define('CLIENT_ID', 'YOUR_PAYPAL_CLIENT_ID');        // Get from PayPal Dashboard
define('CLIENT_SECRET', 'YOUR_PAYPAL_CLIENT_SECRET'); // Get from PayPal Dashboard
```

##### Stripe Configuration

1. Go to [Stripe Dashboard](https://dashboard.stripe.com/)
2. Navigate to Developers > API Keys
3. Copy your test keys (for development)
4. Update `config/config_payment.php`:

```php
define('STRIPE_TEST_PK', 'pk_test_YOUR_STRIPE_PUBLISHABLE_KEY');  // Publishable Key
define('STRIPE_TEST_SK', 'sk_test_YOUR_STRIPE_SECRET_KEY');       // Secret Key
```

**For Production**: Replace test keys with live keys and set `testMode` to false.

#### 3. Email Configuration (`config/config.php`)

Configure SMTP settings for email notifications:

```php
define("SMTP_HOST", "sandbox.smtp.mailtrap.io");      // Your SMTP host
define("SMTP_PORT", "587");                            // SMTP port
define("SMTP_USERNAME", "YOUR_MAILTRAP_USERNAME");    // Your SMTP username
define("SMTP_PASSWORD", "YOUR_MAILTRAP_PASSWORD");    // Your SMTP password
define("SMTP_ENCRYPTION", "tls");
define("SMTP_FROM", "contact@yourwebsite.com");        // Email from address
```

**Recommended**: Use [Mailtrap.io](https://mailtrap.io/) for testing emails in development.

## Database Setup

### Import Database Schema

Run the provided SQL file to set up all tables:

```bash
mysql -u root -p eduzora_lms < database.sql
```

### Database Tables

The system creates the following main tables:
- **users** - Student accounts
- **admins** - Admin accounts
- **instructors** - Instructor accounts
- **courses** - Course information
- **categories** - Course categories
- **languages** - Course languages
- **lessons** - Course lessons/curriculum
- **enrollments** - Student course enrollments
- **orders** - Course purchase orders
- **payments** - Payment records
- **messages** - Student-Instructor messaging
- **wishlists** - Saved courses
- **reviews** - Course reviews
- **coupons** - Discount codes
- **faqs** - Frequently asked questions
- And more...

## Usage Guide

### Access the Application

```
http://localhost/eduzora_lms/
```

### User Roles & Login

#### Admin Login
- URL: `http://localhost/eduzora_lms/admin/`
- Manage all aspects of the platform

#### Instructor Login
- URL: `http://localhost/eduzora_lms/instructor.php`
- Create and manage courses
- View revenue and withdrawals
- Communicate with students

#### Student Login
- URL: `http://localhost/eduzora_lms/login.php`
- Enroll in courses
- Track progress
- Leave reviews
- Purchase courses

### Key Features Usage

#### Creating a Course (Instructor)

1. Login as instructor
2. Go to Dashboard
3. Click "Create Course"
4. Fill in course details (title, description, category, etc.)
5. Add course content (lessons, videos, materials)
6. Set pricing and publish

#### Enrolling in Courses (Student)

1. Browse available courses
2. View course details and reviews
3. Click "Enroll" or "Add to Cart"
4. Proceed to checkout
5. Select payment method (Stripe or PayPal)
6. Complete payment
7. Access course content

#### Creating Coupons (Instructor)

1. Login as instructor
2. Go to Dashboard > Coupons
3. Create new coupon
4. Set discount percentage/amount and validity
5. Share coupon code with students

## Project Structure

```
eduzora_lms/
├── admin/                          # Admin dashboard pages
│   ├── dashboard.php
│   ├── category-*.php
│   ├── course-*.php
│   ├── instructor-*.php
│   └── ...
├── config/                         # Configuration files
│   ├── config.php                 # Database & SMTP config
│   ├── config_payment.php         # Payment gateway config
│   └── functions.php              # Helper functions
├── uploads/                        # User uploaded files
│   └── (course videos, images, etc.)
├── vendor/                         # Composer dependencies
│   ├── stripe/stripe-php
│   ├── omnipay/paypal
│   ├── phpmailer/phpmailer
│   └── ...
├── dist-admin/                     # Admin frontend assets
│   ├── js/
│   ├── css/
│   └── ...
├── dist-front/                     # Frontend assets
│   ├── js/
│   ├── css/
│   └── ...
├── index.php                       # Home page
├── login.php                       # Student login
├── registration.php                # Student registration
├── instructor.php                  # Instructor login
├── instructor-*.php                # Instructor pages
├── student-*.php                   # Student pages
├── checkout.php                    # Payment checkout
├── cart.php                        # Shopping cart
├── courses.php                     # Course listing
├── course.php                      # Course detail page
├── paypal-success.php              # PayPal return
├── stripe-success.php              # Stripe return
└── database.sql                    # Database schema
```

## Important Security Notes

⚠️ **Before deploying to production:**

1. **Update all credentials** - Replace placeholder values with actual credentials
2. **Use environment variables** - Consider using .env files for sensitive data
3. **Enable HTTPS** - Required for payment processing
4. **Change admin credentials** - Update default admin account
5. **Set proper file permissions** - Restrict access to config files
6. **Update base URLs** - Change `BASE_URL` in config to your domain
7. **Review security settings** - Enable proper authentication and validation

## Configuration Checklist

- [ ] Database configured in `config/config.php`
- [ ] PayPal credentials added to `config/config_payment.php`
- [ ] Stripe test/live keys added to `config/config_payment.php`
- [ ] SMTP configuration complete
- [ ] Database imported successfully
- [ ] `BASE_URL` and `ADMIN_URL` updated
- [ ] Web server configured with `.htaccess` support
- [ ] Upload directory has write permissions
- [ ] HTTPS enabled (for production)

## Troubleshooting

### Payment not working
- Verify payment gateway credentials in `config/config_payment.php`
- Check if payment returns are pointing to correct URLs
- Review payment gateway logs in vendor code

### Emails not sending
- Verify SMTP credentials in `config/config.php`
- Check SMTP port is correct (usually 587 or 465)
- Try using Mailtrap for testing

### Database connection errors
- Verify database host, name, username, and password
- Ensure MySQL service is running
- Check user has proper permissions

### Course uploads not working
- Verify `uploads/` directory exists and is writable
- Check file size limits in PHP configuration

## Support

For issues or questions, refer to the help files:
- `_help_general.txt` - General functionality
- `_help_payment.txt` - Payment setup
- `_help_course_concept.txt` - Course structure
- `_help_jquery.txt` - Frontend interactions

## License

Proprietary - All rights reserved" 
