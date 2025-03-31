# Dog Grooming Management Software - User Guide

## Introduction

Welcome to the Dog Grooming Management Software! This comprehensive system is designed to streamline your dog grooming business operations, from appointment scheduling to client management and automated reminders.

## Table of Contents

1. [Getting Started](#getting-started)
2. [Dashboard Overview](#dashboard-overview)
3. [Client Management](#client-management)
4. [Dog Management](#dog-management)
5. [Appointment Scheduling](#appointment-scheduling)
6. [Service and Pricing Management](#service-and-pricing-management)
7. [Messaging and Reminders](#messaging-and-reminders)
8. [Data Import/Export](#data-importexport)
9. [Dog Breed Management](#dog-breed-management)
10. [Troubleshooting](#troubleshooting)

## Getting Started

### First-time Setup

1. Access the application through your web browser
2. Create an admin account on the first login
3. Configure your business settings:
   - Set your business hours
   - Configure VAT rate
   - Set up default services and pricing

### System Requirements

- Modern web browser (Chrome, Firefox, Safari, Edge)
- Internet connection
- Mobile or desktop device

## Dashboard Overview

The dashboard provides a quick overview of your business:

- Today's appointments
- Upcoming appointments
- Recent clients
- Quick access to key features

### Navigation

The main navigation menu includes:
- Calendar
- Clients
- Dogs
- Services
- Messages
- Import/Export
- Dog Breeds
- Settings

## Client Management

### Adding a New Client

1. Navigate to the Clients page
2. Click "Add Client"
3. Fill in the required information:
   - First name
   - Last name
   - Phone number
4. Optional information:
   - Email
   - Address
   - City
   - Postal code
   - Notes
5. Click "Save"

### Searching for Clients

1. Use the search bar at the top of the Clients page
2. Enter client name, email, or phone number
3. Results will update as you type

### Editing Client Information

1. Find the client in the list
2. Click the "Edit" button
3. Update the information
4. Click "Save"

### Viewing Client Details

1. Find the client in the list
2. Click the "View" button
3. View client details, dogs, and appointment history

### Adding a Dog to a Client

1. Find the client in the list
2. Click the "Add Dog" button
3. Fill in the dog details
4. Click "Save"

## Dog Management

### Adding a New Dog

1. Navigate to the Dogs page
2. Click "Add Dog"
3. Select the owner (client)
4. Fill in the required information:
   - Name
   - Breed (select from list or add new)
   - Size
5. Optional information:
   - Date of birth
   - Notes
   - Medical conditions
6. Click "Save"

### Searching for Dogs

1. Use the search bar at the top of the Dogs page
2. Enter dog name or breed
3. Filter by owner using the dropdown
4. Results will update as you type

### Editing Dog Information

1. Find the dog in the list
2. Click the "Edit" button
3. Update the information
4. Click "Save"

### Viewing Dog Details

1. Find the dog in the list
2. Click the "View" button
3. View dog details, appointment history, and statistics

### Booking an Appointment for a Dog

1. Find the dog in the list
2. Click the "Book" button
3. Follow the appointment scheduling process

## Appointment Scheduling

### Calendar Views

The calendar offers three views:
- Day view: Detailed view of a single day
- Week view: Overview of the entire week
- Month view: Monthly overview

Switch between views using the buttons at the top of the calendar.

### Creating a New Appointment

1. Navigate to the Calendar page
2. Click on the desired time slot
3. Select the dog for the appointment
4. Choose the service
5. Set the appointment duration
6. Add any notes
7. Click "Save"

### Editing an Appointment

1. Click on the appointment in the calendar
2. Update the information
3. Click "Save"

### Canceling an Appointment

1. Click on the appointment in the calendar
2. Click "Cancel Appointment"
3. Confirm the cancellation

### Appointment Status

Appointments can have the following statuses:
- Scheduled: Initial status
- Confirmed: Appointment has been confirmed
- Completed: Service has been provided
- Canceled: Appointment was canceled
- No-show: Client didn't show up

Update the status by clicking on the appointment and selecting the new status.

## Service and Pricing Management

### Adding a New Service

1. Navigate to the Services page
2. Click "Add Service"
3. Fill in the required information:
   - Name
   - Description
   - Base price
   - Duration (minutes)
4. Click "Save"

### Setting Price Adjustments

1. Find the service in the list
2. Click the "Pricing" button
3. Set adjustment factors for different dog sizes:
   - Small
   - Medium
   - Large
   - Extra Large
4. Click "Save Price Adjustments"

### VAT Settings

1. Navigate to the Services page
2. Click "VAT Settings"
3. Set the VAT rate (e.g., 0.20 for 20%)
4. Click "Save VAT Rate"

### Viewing Price Calculations

When setting price adjustments, a preview table shows:
- Size
- Adjustment factor
- Price (excluding VAT)
- Price (including VAT)

## Messaging and Reminders

### Creating Message Templates

1. Navigate to the Messages page
2. Click "Add Template"
3. Fill in the required information:
   - Name
   - Type (SMS or WhatsApp)
   - Content
4. Use placeholders for dynamic content:
   - {client_name} - Client's full name
   - {dog_name} - Dog's name
   - {appointment_time} - Formatted appointment date and time
   - {service_name} - Name of the service
   - {price} - Price of the service
5. Click "Save"

### Scheduling Messages

Messages are automatically scheduled when appointments are created. You can also:

1. Navigate to the Appointments page
2. Click on an appointment
3. Click "Schedule Reminder"
4. Select the template
5. Set the scheduled time
6. Click "Save"

### Viewing Scheduled Messages

1. Navigate to the Messages page
2. Click the "Scheduled Messages" tab
3. View all scheduled messages with their status

### Canceling Scheduled Messages

1. Navigate to the Messages page
2. Click the "Scheduled Messages" tab
3. Find the message in the list
4. Click "Cancel" (only available for pending messages)

### Processing Messages

1. Navigate to the Messages page
2. Click "Process Pending Messages"
3. The system will send all pending messages that are due

## Data Import/Export

### Exporting Data

1. Navigate to the Import/Export page
2. Click "Export to Excel"
3. Save the Excel file to your computer

The export includes two sheets:
- Clients: All client information
- Dogs: All dog information with client references

### Importing Clients

1. Navigate to the Import/Export page
2. Select "Clients" from the Import Type dropdown
3. Click "Choose File" and select your Excel file
4. Click "Import Data"
5. Review the import results

### Importing Dogs

1. Navigate to the Import/Export page
2. Select "Dogs" from the Import Type dropdown
3. Click "Choose File" and select your Excel file
4. Click "Import Data"
5. Review the import results

### Download Import Template

1. Navigate to the Import/Export page
2. Click "Download template"
3. Use this template as a guide for formatting your import data

## Dog Breed Management

### Viewing Dog Breeds

1. Navigate to the Dog Breeds page
2. View the list of all breeds with their sizes

### Adding a New Breed

1. Navigate to the Dog Breeds page
2. Click "Add New"
3. Enter the breed name
4. Select the typical size
5. Click "Save"

### Editing a Breed

1. Find the breed in the list
2. Click the "Edit" button
3. Update the information
4. Click "Save"

### Seeding the Database

To quickly populate the database with common dog breeds:

1. Navigate to the Dog Breeds page
2. Click "Seed Database"
3. Confirm the action

### Using Breeds in Dog Management

When adding or editing a dog:
1. Select a breed from the dropdown
2. If the breed doesn't exist, click "Add New Breed"
3. Enter the new breed details
4. Continue with the dog information

## Troubleshooting

### Common Issues

#### Application Not Loading
- Check your internet connection
- Clear your browser cache
- Try a different browser

#### Cannot Save Changes
- Ensure all required fields are filled
- Check for error messages
- Try refreshing the page

#### Calendar Not Showing Appointments
- Check if you're viewing the correct date
- Verify that appointments have been created
- Try switching between calendar views

### Getting Help

If you encounter any issues not covered in this guide, please contact support at support@doggroomingsoftware.com.

## Conclusion

This Dog Grooming Management Software is designed to make your business operations more efficient. By utilizing all the features described in this guide, you can streamline appointment scheduling, client management, and communications, allowing you to focus on providing excellent grooming services to your canine clients.
