# How the Code Works
- Database Setup: Creates a users table in SQLite with id, username, and password_hash.
- Password Strength Check: Validates that passwords are at least 12 characters and include uppercase, lowercase, numbers, and special characters.
- Registration: If the password is strong, it is hashed with bcrypt and stored securely in the database. Weak passwords are rejected.
- Login: When a user logs in, the entered password is hashed and compared with the stored hash. If they match → login successful.
- Interactive Menu: Provides options for registering, logging in, showing users, changing passwords, and deleting accounts.
