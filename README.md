# python-project
import random 
import getpass
accounts = {}
print("             Welcome to online banking       ")

def create_account():
    username = input("Enter new username: ")
    if username in accounts:
        print("Account already exists.")
        return
    password = getpass.getpass("Enter new password: ")
    accounts[username] = {"password": password, "balance": 0}
    print("Account created successfully.")
    accno=random.randint(1000000000,9999999999)
    print("Your account number is:",accno)  
    pan=input("enter your pan number:")               

def login():
    username = input("Enter username: ")
    password = getpass.getpass("Enter password: ")
    if username in accounts and accounts[username]["password"] == password:
        print("Login successful.")
        return username
    else:
        print("Invalid username or password.")
        return None

def deposit(username):
    amount = float(input("Enter amount to deposit: "))
    if amount<=0:
        print(" Sorry! Deposit amount must be greater than 0")
        return
    accounts[username]["balance"] += amount
    print(f"Deposited ₹{amount}. New balance: ₹{accounts[username]['balance']}")

def withdraw(username):
    amount = float(input("Enter amount to withdraw: "))
    if amount<=0:
        print("Sorry...! withdrawal amount must be greater than zero")
        return
    if accounts[username]["balance"] >= amount:
        accounts[username]["balance"] -= amount
        print(f"Withdrew ₹{amount}. New balance: ₹{accounts[username]['balance']}")
    else:
        print("Insufficient balance.")

def check_balance(username):
    print(f"Current balance: ₹{accounts[username]['balance']}")

def close_account(username):
    confirm = input("Are you sure you want to close your account? (yes/no): ")
    if confirm.lower() == 'yes':
        del accounts[username]
        print("Account closed.")
    else:
        print("Account not closed.")
def main():
    while True:
        print("\n-----HAPPY BANKING------")
        print("1. Create Account")
        print("2. Login")
        print("3. Exit")
        choice = input("Enter your choice: ")

        if choice == '1':
            create_account()
        elif choice == '2':
            user = login()
            if user:
                while True:
                    print("\n--- Menu ---")
                    print("1. Deposit")
                    print("2. Withdraw")
                    print("3. Check Balance")
                    print("4. Close Account")
                    print("5. Logout")
                    action = input("Enter your choice: ")

                    if action == '1':
                        deposit(user)
                    elif action == '2':
                        withdraw(user)
                    elif action == '3':
                        check_balance(user)
                    elif action == '4':
                        close_account(user)
                        break
                    elif action == '5':
                        print("Logged out.")
                        break
                    else:
                        print("Invalid choice.")
        elif choice == '3':
            print("Exiting...")
            print("Have a nice day")
            break
        else:
            print("Invalid choice.")
if __name__=="__main__":
  main()
