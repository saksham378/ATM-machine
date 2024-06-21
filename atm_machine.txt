class ATM:
    def __init__(self, users):
        self.users = users

    def display_menu(self):
        print("\n==== ATM Menu ====")
        print("1. Check Balance")
        print("2. Deposit")
        print("3. Withdraw")
        print("4. Exit")

    def authenticate_user(self, username, pin):
        for user in self.users:
            if user['username'] == username and user['pin'] == pin:
                return True, user
        return False, None

    def check_balance(self, user):
        print(f"Your balance is {user['balance']}")

    def deposit(self, user, amount):
        user['balance'] += amount
        print(f"{amount} deposited successfully.")
        self.check_balance(user)

    def withdraw(self, user, amount):
        if amount > user['balance']:
            print("Insufficient funds.")
        else:
            user['balance'] -= amount
            print(f"{amount} withdrawn successfully.")
            self.check_balance(user)

    def run(self):
        while True:
            print("\n==== Welcome to the ATM ====")
            username = input("Enter your username: ")
            pin = input("Enter your PIN: ")

            authenticated, user = self.authenticate_user(username, pin)

            if authenticated:
                while True:
                    self.display_menu()
                    choice = input("Enter your choice (1-4): ")

                    if choice == '1':
                        self.check_balance(user)
                    elif choice == '2':
                        amount = float(input("Enter the amount to deposit: "))
                        self.deposit(user, amount)
                    elif choice == '3':
                        amount = float(input("Enter the amount to withdraw: "))
                        self.withdraw(user, amount)
                    elif choice == '4':
                        print("Thank you for using the ATM. Goodbye!")
                        exit()
                    else:
                        print("Invalid choice. Please try again.")

            else:
                print("Invalid username or PIN. Please try again.")


# Sample user data
users = [
    {'username': 'user1', 'pin': '1234', 'balance': 1000.0},
    {'username': 'user2', 'pin': '5678', 'balance': 1500.0},
    {'username': 'user3', 'pin': '9876', 'balance': 2000.0},
    {'username': 'user4', 'pin': '5432', 'balance': 500.0},
    {'username': 'user5', 'pin': '6789', 'balance': 2500.0},
]

# Create an ATM instance and run the program
atm = ATM(users)
atm.run()
