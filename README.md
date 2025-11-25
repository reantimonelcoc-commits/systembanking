accounts_data = {
    "admin": {"password": "admin123"},
    "users": {}
}

# Admin Menu
def admin_menu():
    while True:
        print("\n--- ADMIN MENU ---")
        print("[1] Create User Account")
        print("[2] View All Users")
        print("[3] Logout")
        choice = input("Choose: ")

        if choice == "1":
            username = input("Enter new username: ")
            if username in accounts_data["users"]:
                print("User already exists.")
                continue
            password = input("Enter password: ")
            accounts_data["users"][username] = {"password": password, "balance": 0}
            print(f"✅ Account for '{username}' created successfully.")
        elif choice == "2":
            print("\n--- USER ACCOUNTS ---")
            for user, info in accounts_data["users"].items():
                print(f"User: {user}, Balance: ₱{info['balance']}")
        elif choice == "3":
            break
        else:
            print("Invalid choice!")

# User Menu
def user_menu(username):
    while True:
        print(f"\n--- USER MENU ({username}) ---")
        print("[1] Check Balance")
        print("[2] Deposit")
        print("[3] Withdraw")
        print("[4] Logout")
        choice = input("Choose: ")

        if choice == "1":
            print(f"Your balance: ₱{accounts_data['users'][username]['balance']}")
        elif choice == "2":
            amt = float(input("Enter amount to deposit: ₱"))
            accounts_data["users"][username]["balance"] += amt
            print("✅ Deposit successful!")
        elif choice == "3":
            amt = float(input("Enter amount to withdraw: ₱"))
            if amt <= accounts_data["users"][username]["balance"]:
                accounts_data["users"][username]["balance"] -= amt
                print("✅ Withdrawal successful!")
            else:
                print("❌ Insufficient balance!")
        elif choice == "4":
            break
        else:
            print("Invalid choice!")

# Main Program
def main():
    while True:
        print("\n==== SIMPLE BANKING SYSTEM ====")
        print("[1] Admin Login")
        print("[2] User Login")
        print("[3] Exit")
        choice = input("Choose: ")

        if choice == "1":
            password = input("Enter admin password: ")
            if password == accounts_data["admin"]["password"]:
                admin_menu()
            else:
                print("❌ Wrong password!")
        elif choice == "2":
            username = input("Username: ")
            password = input("Password: ")
            if username in accounts_data["users"] and accounts_data["users"][username]["password"] == password:
                user_menu(username)
            else:
                print("❌ Invalid login!")
        elif choice == "3":
            print("👋 Goodbye!")
            break
        else:
            print("Invalid choice!")

if __name__ == "__main__":
    main()
