# Secure Login System – Code Overview
A Python‑based secure login system that demonstrates best practices in authentication.
It uses SQLite for local storage and bcrypt for password hashing, ensuring passwords are never stored in plain text.
The system enforces strong password rules, prevents SQL injection with parameterized queries, and provides an interactive menu for user registration, login, and account management.
## Features
- User Registration with strong password validation
- Secure Login using bcrypt hash verification
- SQLite database storage (no plain-text passwords)
- Interactive menu for Register, Login, Exit
## Security Highlights
- Passwords stored as bcrypt hashes (never plain text)
- Parameterized SQL queries prevent SQL injection
- Password strength rules enforced

