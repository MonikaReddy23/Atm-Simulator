import time

print("Please insert your card")
time.sleep(2)

password = 2623
max_attempts = 3
balance = 10000

# Loop for retrying the PIN input if it's wrong
for attempt in range(max_attempts):
    pin = int(input("Enter your ATM pin number: "))
    if pin == password:
        print("Pin accepted!")
        break
    else:
        print(f"Invalid pin entered. You have {max_attempts - (attempt + 1)} attempts remaining.")
        if attempt == max_attempts - 1:
            print("Too many invalid attempts. Exiting.")
            exit()

# Main ATM operations loop
while True:
    print("""
    1 = Check balance
    2 = Withdraw balance
    3 = Deposit amount
    4 = Exit
    """)
    
    try:
        option = int(input("Enter your choice: "))
    except ValueError:
        print("Please enter a valid option:")
        continue

    if option == 1:
        print(f"Your current balance is {balance}")
    
    elif option == 2:
        try:
            withdraw_amount = int(input("Enter the amount to withdraw: "))
            if withdraw_amount <= 0:
                print("Please enter a positive amount to withdraw.")
            elif withdraw_amount > balance:
                print("Insufficient funds.")
            else:
                balance -= withdraw_amount
                print(f"{withdraw_amount} is debited from your account.")
                print(f"Your current balance is {balance}")
        except ValueError:
            print("Please enter a valid amount to withdraw.")
    
    elif option == 3:
        try:
            deposit_amount = int(input("Enter the amount to deposit: "))
            if deposit_amount <= 0:
                print("Please enter a positive amount to deposit.")
            else:
                balance += deposit_amount
                print(f"{deposit_amount} is credited into your bank account.")
                print(f"Your current balance is {balance}")
        except ValueError:
            print("Please enter a valid amount to deposit.")
    
    elif option == 4:
        print("Exiting the ATM system.")
        break
    
    else:
        print("Invalid option entered. Please try again.")
