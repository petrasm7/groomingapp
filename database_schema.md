# Database Schema for Dog Grooming Management Software

## Overview
This document outlines the database schema design for the dog grooming management software. The schema is designed to support all the required features including client management, dog information, appointment scheduling, service tracking, and messaging capabilities.

## Tables

### 1. Users
Stores information about system users (groomers/staff).

```sql
CREATE TABLE users (
  id INTEGER PRIMARY KEY,
  username TEXT NOT NULL UNIQUE,
  password_hash TEXT NOT NULL,
  full_name TEXT NOT NULL,
  email TEXT NOT NULL UNIQUE,
  phone TEXT,
  role TEXT NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### 2. Clients
Stores information about the clients (dog owners).

```sql
CREATE TABLE clients (
  id INTEGER PRIMARY KEY,
  first_name TEXT NOT NULL,
  last_name TEXT NOT NULL,
  email TEXT UNIQUE,
  phone TEXT NOT NULL,
  address TEXT,
  city TEXT,
  postal_code TEXT,
  notes TEXT,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### 3. Dogs
Stores information about the dogs linked to clients.

```sql
CREATE TABLE dogs (
  id INTEGER PRIMARY KEY,
  client_id INTEGER NOT NULL,
  name TEXT NOT NULL,
  breed TEXT,
  size TEXT,
  age INTEGER,
  weight REAL,
  temperament TEXT,
  medical_info TEXT,
  grooming_notes TEXT,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (client_id) REFERENCES clients (id) ON DELETE CASCADE
);
```

### 4. Services
Stores information about the different grooming services offered.

```sql
CREATE TABLE services (
  id INTEGER PRIMARY KEY,
  name TEXT NOT NULL,
  description TEXT,
  base_price REAL NOT NULL,
  duration_minutes INTEGER NOT NULL,
  is_active BOOLEAN DEFAULT TRUE,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### 5. Service_Price_Adjustments
Stores price adjustments for services based on dog size.

```sql
CREATE TABLE service_price_adjustments (
  id INTEGER PRIMARY KEY,
  service_id INTEGER NOT NULL,
  dog_size TEXT NOT NULL,
  adjustment_factor REAL NOT NULL DEFAULT 1.0,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (service_id) REFERENCES services (id) ON DELETE CASCADE,
  UNIQUE (service_id, dog_size)
);
```

### 6. Appointments
Stores information about scheduled appointments.

```sql
CREATE TABLE appointments (
  id INTEGER PRIMARY KEY,
  dog_id INTEGER NOT NULL,
  service_id INTEGER NOT NULL,
  groomer_id INTEGER,
  start_time TIMESTAMP NOT NULL,
  end_time TIMESTAMP NOT NULL,
  status TEXT NOT NULL DEFAULT 'scheduled',
  price REAL NOT NULL,
  vat_rate REAL NOT NULL DEFAULT 0.20,
  notes TEXT,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (dog_id) REFERENCES dogs (id) ON DELETE CASCADE,
  FOREIGN KEY (service_id) REFERENCES services (id) ON DELETE RESTRICT,
  FOREIGN KEY (groomer_id) REFERENCES users (id) ON DELETE SET NULL
);
```

### 7. Appointment_History
Stores historical information about completed appointments.

```sql
CREATE TABLE appointment_history (
  id INTEGER PRIMARY KEY,
  appointment_id INTEGER NOT NULL,
  service_provided TEXT NOT NULL,
  notes TEXT,
  before_photo_path TEXT,
  after_photo_path TEXT,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (appointment_id) REFERENCES appointments (id) ON DELETE CASCADE
);
```

### 8. Message_Templates
Stores customizable message templates for reminders.

```sql
CREATE TABLE message_templates (
  id INTEGER PRIMARY KEY,
  name TEXT NOT NULL,
  content TEXT NOT NULL,
  type TEXT NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### 9. Scheduled_Messages
Stores information about scheduled reminder messages.

```sql
CREATE TABLE scheduled_messages (
  id INTEGER PRIMARY KEY,
  appointment_id INTEGER NOT NULL,
  template_id INTEGER NOT NULL,
  scheduled_time TIMESTAMP NOT NULL,
  status TEXT NOT NULL DEFAULT 'pending',
  sent_time TIMESTAMP,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (appointment_id) REFERENCES appointments (id) ON DELETE CASCADE,
  FOREIGN KEY (template_id) REFERENCES message_templates (id) ON DELETE CASCADE
);
```

### 10. Settings
Stores system-wide settings including VAT rate and messaging configurations.

```sql
CREATE TABLE settings (
  id INTEGER PRIMARY KEY,
  key TEXT NOT NULL UNIQUE,
  value TEXT NOT NULL,
  description TEXT,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

## Indexes

```sql
-- Indexes for faster lookups
CREATE INDEX idx_dogs_client_id ON dogs (client_id);
CREATE INDEX idx_appointments_dog_id ON appointments (dog_id);
CREATE INDEX idx_appointments_service_id ON appointments (service_id);
CREATE INDEX idx_appointments_groomer_id ON appointments (groomer_id);
CREATE INDEX idx_appointments_start_time ON appointments (start_time);
CREATE INDEX idx_appointments_status ON appointments (status);
CREATE INDEX idx_scheduled_messages_appointment_id ON scheduled_messages (appointment_id);
CREATE INDEX idx_scheduled_messages_status ON scheduled_messages (status);
```

## Initial Data

```sql
-- Insert default services
INSERT INTO services (name, description, base_price, duration_minutes) VALUES
('Full Groom', 'Complete grooming service including bath, haircut, nail trim, ear cleaning', 50.00, 120),
('Wash and Tidy', 'Bath, blow dry, and light trimming', 30.00, 60),
('Nail Trim', 'Nail trimming service only', 15.00, 15),
('Ear Cleaning', 'Ear cleaning service only', 10.00, 15),
('Teeth Brushing', 'Teeth brushing service', 12.00, 15);

-- Insert default price adjustments
INSERT INTO service_price_adjustments (service_id, dog_size, adjustment_factor) VALUES
(1, 'Small', 1.0),
(1, 'Medium', 1.2),
(1, 'Large', 1.5),
(1, 'Extra Large', 1.8),
(2, 'Small', 1.0),
(2, 'Medium', 1.2),
(2, 'Large', 1.5),
(2, 'Extra Large', 1.8);

-- Insert default message templates
INSERT INTO message_templates (name, content, type) VALUES
('Appointment Reminder', 'Hello {client_name}, this is a reminder that {dog_name} has a grooming appointment scheduled for {appointment_time} tomorrow. Please reply to confirm. Thank you!', 'sms'),
('Appointment Confirmation', 'Thank you for booking with us! {dog_name}''s grooming appointment is confirmed for {appointment_time}. See you then!', 'sms'),
('Appointment Follow-up', 'Hello {client_name}, we hope {dog_name} enjoyed the grooming session today! Feel free to leave us feedback or book your next appointment.', 'sms');

-- Insert default settings
INSERT INTO settings (key, value, description) VALUES
('vat_rate', '0.20', 'Current VAT rate as a decimal'),
('business_name', 'Pawsome Grooming', 'Business name for receipts and messages'),
('business_phone', '+1234567890', 'Business phone number for WhatsApp and SMS'),
('reminder_hours_before', '24', 'Hours before appointment to send reminder');
```

## Relationships

1. **One-to-Many**: Client to Dogs (one client can have multiple dogs)
2. **One-to-Many**: Dog to Appointments (one dog can have multiple appointments)
3. **One-to-Many**: Service to Appointments (one service type can be used in multiple appointments)
4. **One-to-Many**: User (Groomer) to Appointments (one groomer can have multiple appointments)
5. **One-to-One**: Appointment to Appointment_History (each completed appointment has one history record)
6. **One-to-Many**: Appointment to Scheduled_Messages (one appointment can have multiple scheduled messages)
7. **One-to-Many**: Message_Template to Scheduled_Messages (one template can be used for multiple messages)

## Notes on Schema Design

1. **Flexibility**: The schema allows for adding new services and adjusting prices based on dog size.
2. **History Tracking**: Appointment history is stored separately to maintain a clean appointments table.
3. **Messaging**: Templates and scheduled messages support the automated reminder system.
4. **Settings**: System-wide settings are stored in a dedicated table for easy configuration.
5. **Status Tracking**: Appointment status field allows tracking of scheduled, completed, canceled appointments.
6. **VAT Handling**: VAT rate is stored both at the system level and per appointment for historical accuracy.
