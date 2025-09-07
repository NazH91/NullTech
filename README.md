# NullTech
CodeNection - Industry Collaboration

# Insurance Verification App

## Overview
This Django-based web application helps verify **car insurance details** during online applications.  

The system checks whether the entered **IC number, owner name, and vehicle plate** match the official records in the database. This prevents users from mistyping details that could cause insurance errors.  

---

## Problem it Solves
When buying or renewing car insurance online, users often:  
- Mistype or enter **incorrect IC numbers**  
- Enter a **wrong owner name**  
- Provide a **plate number that doesn’t belong to them**  

These mistakes can:  
- Delay approval  
- Cause incorrect pricing  
- Lead to invalid or fraudulent insurance coverage  

---

## Solution
The app provides **real-time verification** of:  
- **IC Number** → checked in database  
- **Owner Name** → must match IC owner  
- **Plate Number** → must belong to the IC owner  
- **Car Model & Year** → stored and displayed for confirmation  

If the IC, Name, and Plate don’t match, the system **blocks the submission** (hard stop).  

---

## Features
- **Hard stop rule** → IC ↔ Name ↔ Plate must match, or form submission fails.  
- **Validation feedback** → errors shown inline next to inputs.  
- **Success confirmation** → if valid, owner & car details are displayed.  
- Uses **SQLite database** (easy to test & deploy).  

---

## Database Schema
- **Owner**: `ic_number`, `name`  
- **CarModel**: `name`  
- **Vehicle**: `plate_number`, `car_model_id`, `manufacture_year`, `owner_id`  

---

## How to Run
```bash
# Clone project
git clone [<repo-url>](https://github.com/NazH91/NullTech.git)
cd insurance_verification

# Install dependencies
pip install django

# Run migrations
python manage.py makemigrations
python manage.py migrate

# Load sample data
sqlite3 db.sqlite3 < seed.sql

# Start server
python manage.py runserver
```

Open: [http://127.0.0.1:8000](http://127.0.0.1:8000)

---

## Example Behavior
### Correct Input
- IC: `900101-14-1111`  
- Name: `KAMAL`  
- Plate: `ABC123`  

→ **Pass**: Shows verified owner and vehicle info.  

### Wrong Name
- IC: `900101-14-1111`  
- Name: `JAMAL`  
- Plate: `ABC123`  

→ **Fail**: *“IC belongs to KAMAL, but you entered JAMAL.”*  

### Wrong Plate
- IC: `900101-14-1111`  
- Name: `KAMAL`  
- Plate: `XYZ789`  

→ **Fail**: *“Plate XYZ789 does not belong to KAMAL.”*  

### Invalid IC
- IC: `999999-99-9999`  

→ **Fail**: *“IC number not found in database.”*  

