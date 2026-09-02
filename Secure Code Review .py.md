import sqlite3
import bcrypt
import re

# --- Step 1: Initialize Database ---
def init_db():
    conn = sqlite3.connect("users.db")
    cursor = conn.cursor()
    cursor.execute("""
    CREATE TABLE IF NOT EXISTS users (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        username TEXT UNIQUE NOT NULL,
        password_hash BLOB NOT NULL
    )
    """)
    conn.commit()
    conn.close()

# --- Step 2: Password Strength Check ---
def check_password_strength(password):
    messages = []

    if len(password) < 12:
        messages.append("Password length less than 12 characters")
    if not re.search(r"[A-Z]", password):
        messages.append("No uppercase letter used")
    if not re.search(r"[a-z]", password):
        messages.append("No lowercase letter used")
    if not re.search(r"[0-9]", password):
        messages.append("No number used")
    if not re.search(r"[@$!%*?&]", password):
        messages.append("No special character used")

    if not messages:
        return "Strong password"
    else:
        return "\n".join(messages)

# --- Step 3: Register User ---
def register_user(username, password):
    strength = check_password_strength(password)
    print(strength)

    if "No" in strength or "Password length" in strength:
        print("Registration failed: Weak password")
        return

    conn = sqlite3.connect("users.db")
    cursor = conn.cursor()
    try:
        hashed = bcrypt.hashpw(password.encode(), bcrypt.gensalt())
        # Store as BLOB
        cursor.execute("INSERT INTO users (username, password_hash) VALUES (?, ?)",
                       (username, sqlite3.Binary(hashed)))
        conn.commit()
        print("User registered successfully")
    except sqlite3.IntegrityError:
        print("Username already exists")
    finally:
        conn.close()

# --- Step 4: Login User ---
def login_user(username, password):
    conn = sqlite3.connect("users.db")
    cursor = conn.cursor()
    # SELECT instead of INSERT
    cursor.execute("SELECT password_hash FROM users WHERE username = ?", (username,))
    result = cursor.fetchone()
    conn.close()

    if result:
        stored_hash = result[0]

        # Ensure stored_hash is bytes
        if isinstance(stored_hash, str):
            stored_hash = stored_hash.encode('utf-8')

        if bcrypt.checkpw(password.encode(), stored_hash):
            print("Login successful")
        else:
            print("Invalid username or password")
    else:
        print("Invalid username or password")

# --- Step 5: Interactive Menu ---
if __name__ == "__main__":
    init_db()
    while True:
        print("\n--- Secure Login System ---")
        print("1. Register")
        print("2. Login")
        print("3. Exit")
        choice = input("Enter choice (1/2/3): ")

        if choice == "1":
            uname = input("Enter username: ")
            pwd = input("Enter password: ")
            register_user(uname, pwd)

        elif choice == "2":
            uname = input("Enter username: ")
            pwd = input("Enter password: ")
            login_user(uname, pwd)

        elif choice == "3":
            print("Exiting From Login Account""...")
            break
        else:
            print("Invalid choice, try again.")
