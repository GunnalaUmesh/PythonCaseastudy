# PythonCaseastudy


class Account:

    def __init__(self, acc_no, name, balance=0):

        self.acc_no = acc_no

        self.name = name

        self.balance = balance

        self.transactions = []




    def deposit(self, amount):

        self.balance += amount

        self.transactions.append(f"Deposited: {amount}")

        print(f"Deposited {amount}. New balance: {self.balance}")




    def withdraw(self, amount):

        if amount > self.balance:

            print("Insufficient funds!")

        else:

            self.balance -= amount

            self.transactions.append(f"Withdrew: {amount}")

            print(f"Withdrew {amount}. New balance: {self.balance}")




    def transfer(self, amount, target_account):

        if amount > self.balance:

            print("Insufficient funds!")

        else:

            self.balance -= amount

            target_account.balance += amount

            self.transactions.append(f"Transferred: {amount} to {target_account.acc_no}")

            target_account.transactions.append(f"Received: {amount} from {self.acc_no}")

            print(f"Transferred {amount} to account {target_account.acc_no}. New balance: {self.balance}")




    def print_transactions(self):

        print(f"Transactions for account {self.acc_no}:")

        for transaction in self.transactions:

            print(transaction)




def main():

    accounts = {}




    while True:

        print("\n1. Create Account")

        print("2. View Account details by AccNo.")

        print("3. Withdraw")

        print("4. Deposit")

        print("5. Fund Transfer")

        print("6. Print Transactions")

        print("7. Exit")




        choice = int(input("Enter your choice: "))




        if choice == 1:

            acc_no = input("Enter account number: ")

            name = input("Enter account holder name: ")

            accounts[acc_no] = Account(acc_no, name)

            print(f"Account created for {name} with account number {acc_no}.")




        elif choice == 2:

            acc_no = input("Enter account number: ")

            if acc_no in accounts:

                account = accounts[acc_no]

                print(f"Account Number: {account.acc_no}, Name: {account.name}, Balance: {account.balance}")

            else:

                print("Account not found!")




        elif choice == 3:

            acc_no = input("Enter account number: ")

            if acc_no in accounts:

                amount = float(input("Enter amount to withdraw: "))

                accounts[acc_no].withdraw(amount)

            else:

                print("Account not found!")




        elif choice == 4:

            acc_no = input("Enter account number: ")

            if acc_no in accounts:

                amount = float(input("Enter amount to deposit: "))

                accounts[acc_no].deposit(amount)

            else:

                print("Account not found!")




        elif choice == 5:

            from_acc = input("Enter your account number: ")

            to_acc = input("Enter target account number: ")

            if from_acc in accounts and to_acc in accounts:

                amount = float(input("Enter amount to transfer: "))

                accounts[from_acc].transfer(amount, accounts[to_acc])

            else:

                print("One or both accounts not found!")




        elif choice == 6:

            acc_no = input("Enter account number: ")

            if acc_no in accounts:

                accounts[acc_no].print_transactions()

            else:

                print("Account not found!")




        elif choice == 7:

            print("Exiting...")

            break




        else:

            print("Invalid choice! Please try again.")




if __name__ == "__main__":

    main()
