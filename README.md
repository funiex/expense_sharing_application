# Daily Expenses Sharing Application

## Overview

expanse sharing application project is an example Flask web application designed to manage expenses among users. This README provides an overview of the project structure and how to run the application.

## Directory Structure

```lua
expense_sharing_application/
├── manage.py
├── expense_sharing_application/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── expense/
│   ├── migrations/
│   │   └── __init__.py
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── serializers.py
│   ├── tests.py
│   └── views.py
├── templates/
│   └── index.html
└──Back end Intern Assignment.pdf
```


## Project Structure

- The `expense_sharing_application/` directory serves as the root directory of the Django project.

    - **`manage.py`**: A command-line utility for managing the project.

    - **`expense_sharing_application/`**: The main Django app for the expense_sharing_application project.

        - **`__init__.py`**: Marks the directory as a Python package.
        
        - **`settings.py`**: Contains project settings and configurations.
        
        - **`urls.py`**: Defines URL patterns for routing requests to views.
        
        - **`wsgi.py`**: Entry point for WSGI-compatible web servers.

    - **`expense/`**: A secondary app within the project, possibly handling expense-related functionalities.

        - **`migrations/`**: Contains database migration files.
        
        - **`__init__.py`**, **`admin.py`**, **`apps.py`**, **`models.py`**, **`serializers.py`**, **`tests.py`**, **`views.py`**: Standard Django files for defining models, views, serializers, tests, etc.

    - **`templates/`**: Directory containing HTML templates for rendering views.

This structure organizes the project's files and directories according to Django conventions, facilitating easy management and navigation.


## Getting Started

To set up and run the Django project with Django REST Framework:

1. Install Django and Django REST Framework:

    ```bash
    pip install django djangorestframework mysqlclient
    ```

2. Navigate to the project directory:

    ```bash
    cd expense_sharing_application/
    ```



3. Configure Database (MySQL)
         `Install MySQL and create a new database:`
   

    ```bash
    CREATE DATABASE expense_db;
    ```
4. Update settings.py to use MySQL:` In expense_app/settings.py, find the DATABASES section and update it like so:`
    ```bash
       DATABASES = {
                'default': {
                'ENGINE': 'django.db.backends.mysql',
                'NAME': 'expense_db',
                'USER': 'your_databse_username',
                'PASSWORD': 'your_mysql_password',
                'HOST': 'localhost',
                'PORT': '3306',
                  }
              }
    ```
5. Apply database migrations:
   ```bash
      python manage.py migrate
    ```

4. Start the development server:

    ```bash
    python manage.py runserver
    ```

5. Access the application at [http://localhost:8000/](http://localhost:8000/).

6. (Optional) Create a superuser to access the Django admin panel:

    ```bash
    python manage.py createsuperuser
    ```

    Follow the prompts to create a username, email, and password.

Now you're ready to use the expense_sharing_application Django application with Django REST Framework!




## Class Diagram

```bash
+------------------+       +-------------------+       +---------------------+       +---------------------+
|       User       |       |      Expense      |       |   ExpensePaidBy     |       |   ExpenseOwedBy     |
+------------------+       +-------------------+       +---------------------+       +---------------------+
| - userId (PK)    |       | - expenseId (PK)  |       | - userId (FK)       |       | - userId (FK)       |
| - name           |       | - desc            |       | - expenseId (FK)    |       | - expenseId (FK)    |
| - email          |       | - amount          |       | - amountPaid        |       | - amountOwed        |
| - mobileNumber   |       | - createdById (FK)|       +---------------------+       +---------------------+
+------------------+       | - createdAt       |       
                           +-------------------+
```


### User Class

- **userId**
- name
- email
- mobileNumber

### Expense Class

- **expenseId**
- desc
- amount
- createdById
- createdAt

### ExpensePaidBy Class

- **userId**
- **expenseId**
- amount

### ExpenseOwedBy Class

- **userId**
- **expenseId**
- amount

## Database Model

### User

- **userId**: Integer (Primary Key)
- **name**: String (255), Not Null
- **email**: String (255), Unique, Not Null
- **mobileNumber**: String (20), Not Null

### Expense

- **expenseId**: Integer (Primary Key)
- **desc**: String (255), Not Null
- **amount**: Decimal (15, 2), Not Null
- **createdById**: Integer, Not Null
- **createdAt**: Timestamp, Default: Current Timestamp

### ExpensePaidBy

- **userId**: Integer (Foreign Key to User.userId, Primary Key)
- **expenseId**: Integer (Foreign Key to Expense.expenseId, Primary Key)
- **amount**: Decimal (15, 2), Not Null

### ExpenseOwedBy

- **userId**: Integer (Foreign Key to User.userId, Primary Key)
- **expenseId**: Integer (Foreign Key to Expense.expenseId, Primary Key)
- **amount**: Decimal (15, 2), Not Null


## Entity Descriptions

### User

- **userId**: Unique identifier for each user.
- **name**: Name of the user.
- **email**: Email address of the user.
- **mobileNumber**: Mobile number of the user.

### Expense

- **expenseId**: Unique identifier for each expense.
- **desc**: Description of the expense.
- **amount**: Total amount of the expense.
- **createdById**: User ID of the creator of the expense. Default: userId = 1
- **createdAt**: Timestamp indicating when the expense was created.

### ExpensePaidBy

- **user**: User who paid for the expense.
- **expense**: Expense for which the user made a payment.
- **amountPaid**: Amount paid by the user for the expense.

### ExpenseOwedBy

- **user**: User who owes money for the expense.
- **expense**: Expense for which the user owes money.
- **amountOwed**: Amount owed by the user for the expense.

## Relationships

- The `User` entity is associated with the `UserExpensePaid` and `UserExpenseOwed` entities.
- The `Expense` entity is associated with the `UserExpensePaid` and `UserExpenseOwed` entities.


# Splitwise API Documentation

### 1. Get Users

- **Endpoint:** `/users`  
- **Method:** GET  
- **Description:** Retrieves a list of all users.  
- **Response Format:**
    ```json
    {
    "users": [
        {
        "userId": 1,
        "name": "John Doe",
        "email": "john.doe@example.com",
        "mobileNumber": "123-456-7890"
        },
        // Additional user objects...
    ]
    }
    ```

### 2. Add User

- **Endpoint:** `/add_user`  
- **Method:** POST  
- **Description:** Adds a new user to the system.  
- **Request Format:**
    ```json
    {
    "name": "John Doe",
    "email": "john.doe@example.com",
    "mobileNumber": "123-456-7890"
    }
    ```
- **Response Format:**
    ```json
    {
    "message": "User added successfully"
    }
    ```

### 3. Add Expense

**Equal Split**
- **Endpoint:** `/add_expense`
- **Method:** POST
- **Description:** Adds a new expense along with expense-related details.
- **Request Format:**
    ```json
    {
    "expense_type": "EQUAL",
    "desc": "electricity bill",
    "total_amount": 500,
    "paidBy": {
        "2": 200,
        "3": 300
    }
    }
    ```
- **Response Format:**
    ```json
    {
    "message": "Expense split equally added successfully"  // or details of any errors
    }
    ```

**Exact Split**
- **Endpoint:** `/add_expense`
- **Method:** POST
- **Description:** Adds a new expense along with expense-related details.
- **Request Format:**
    ```json
    {
    "expense_type": "EXACT",
    "desc": "paytm",
    "total_amount": 600,
    "paidBy": {
        "1": 300,
        "3": 300
    },
    "owedBy": {
        "1": 100,
        "3": 200,
        "4": 300
    }
    }
    ```
- **Response Format:**
    ```json
    {
    "message": "Expense split exactly added successfully"  // or details of any errors
    }
    ```

**Percent Split**
- **Endpoint:** `/add_expense`
- **Method:** POST
- **Description:** Adds a new expense along with expense-related details.
- **Request Format:**
    ```json
    {
    "expense_type": "PERCENT",
    "desc": "paytm",
    "total_amount": 700,
    "paidBy": {
        "1": 700
    },
    "owedBy": {
        "1": 20,
        "2": 33,
        "3": 47
    }
    }
    ```

- **Response Format:**
    ```json
    {
    "message": "Expense split by percentage added successfully"  // or details of any errors
    }
    ```









