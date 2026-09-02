# How the Code Works
- Database Setup: Creates a users table in SQLite with id, username, and password_hash.
- Password Strength Check: Validates that passwords are at least 12 characters and include uppercase, lowercase, numbers, and special characters.
- Registration: If the password is strong, it is hashed with bcrypt and stored securely in the database. Weak passwords are rejected.
- Login: When a user logs in, the entered password is hashed and compared with the stored hash. If they match → login successful.
- Interactive Menu: Provides options for registering, logging in, showing users, changing passwords, and deleting accounts.
## What Happens If Password Rules Are Ignored
- If a user tries to register with a weak password (e.g., less than 12 characters, missing uppercase, missing number, etc.), the system rejects registration and shows clear error messages.
- This ensures that only strong passwords are stored, reducing the risk of brute‑force or dictionary attacks.
- During login, if the wrong password is entered, bcrypt verification fails and the system shows “Invalid username or password.”
<img width="1200" height="1600" alt="output review" src="https://github.com/user-attachments/assets/03bdeadd-c068-4d46-b7e0-ce019636fc33" />




