# Emergency-Responses-Website-Helpmate-
Helpmate is an emergency assistance platform with SOS alerts, nearby help, emergency contacts, and helpline services built using Node.js, Express, and PostgreSQL.
##  Project Setup & Installation Guide

```bash
mkdir helpmate
cd helpmate
npx create-react-app client
Inside helpmate folder create backend:
mkdir server
cd server
npm init -y
**Backend Dependencies**
npm install express cors dotenv pg nodemailer multer axios country-state-city
npm install nodemon --save-dev
Run backend:
npx nodemon index.js
**Frontend Dependencies**
cd client
npm install axios
npm install lottie-react react-useanimations lottie-web
npm install react-hot-toast react-toastify
npm install framer-motion
npm install lucide-react
npm install react-leaflet leaflet
**Database Configuration (PostgreSQL)**
**Users Table**
CREATE TABLE users(
  id SERIAL PRIMARY KEY,
  full_name TEXT,
  email TEXT UNIQUE,
  phone TEXT,
  password TEXT,
  is_verified BOOLEAN DEFAULT false,
  profile_image TEXT,
  city VARCHAR(100),
  state VARCHAR(100),
  pincode VARCHAR(20),
  country VARCHAR(100),
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
**Email OTP Table**
CREATE TABLE email_otps(
  id SERIAL PRIMARY KEY,
  email TEXT,
  otp TEXT,
  expires_at TIMESTAMP,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
**Emergency Contacts Table**
CREATE TABLE emergency_contacts (
  id SERIAL PRIMARY KEY,
  user_id INTEGER NOT NULL,
  name VARCHAR(100) NOT NULL,
  phone VARCHAR(20) NOT NULL,
  email VARCHAR(100) DEFAULT '',
  relation VARCHAR(50),
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT fk_user
    FOREIGN KEY (user_id)
    REFERENCES users(id)
    ON DELETE CASCADE
);
**Emergency Alerts Table**
CREATE TABLE emergency_alerts (
  id SERIAL PRIMARY KEY,
  user_email VARCHAR(255) NOT NULL,
  alert_type VARCHAR(50) NOT NULL,
  status VARCHAR(50) NOT NULL DEFAULT 'alert_sent',
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
**SOS Responses Table**
CREATE TABLE sos_responses (
    id SERIAL PRIMARY KEY,
    user_email VARCHAR(255) NOT NULL,
    helper_name VARCHAR(255) NOT NULL,
    helper_email VARCHAR(255) NOT NULL,
    response VARCHAR(10) NOT NULL,
    created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP
);
**Active SOS Status Table**
CREATE TABLE sos_active (
    user_email VARCHAR(255) PRIMARY KEY,
    active BOOLEAN NOT NULL DEFAULT FALSE,
    updated_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
    status VARCHAR(50) DEFAULT 'SAFE',
    helper_name VARCHAR(255)
);
**Database Alter Commands Used During Development**
ALTER TABLE users ADD COLUMN otp VARCHAR(6);
ALTER TABLE users ADD COLUMN is_verified BOOLEAN DEFAULT FALSE;
ALTER TABLE users ADD COLUMN profile_image TEXT;
ALTER TABLE users ADD COLUMN city VARCHAR(100);
ALTER TABLE users ADD COLUMN state VARCHAR(100);
ALTER TABLE users ADD COLUMN pincode VARCHAR(20);
ALTER TABLE users ADD COLUMN country VARCHAR(100);
**🚀 Run Project**
**Backend:**
cd server
node index.js
**Frontend:**
cd client
npm start
