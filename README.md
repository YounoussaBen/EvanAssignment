# EvanAssignment


## A Comprehensive Banking System

### Scenario

You are tasked with developing a comprehensive banking system for a fictional bank, "FutureBank." This system will allow for the creation and management of various types of bank accounts, perform complex financial transactions, and generate reports. This assignment will require you to apply concepts from object-oriented programming, including classes, inheritance, polymorphism, encapsulation, and abstract classes, along with the use of iterators, generators, and decorators.

### Requirements

1. **Account Management**
   - Create an abstract class `Account` with attributes like `account_number`, `owner`, and `balance`. Include abstract methods `deposit` and `withdraw`.
   - Implement concrete subclasses for different types of accounts:
     - `CheckingAccount` with an additional attribute for overdraft limit.
     - `SavingsAccount` with an interest rate.
     - `BusinessAccount` with a credit limit.

2. **Transaction Management**
   - Create a class `Transaction` to represent individual transactions. This class should include details like the transaction amount, type (deposit or withdrawal), and timestamp.
   - Implement a method in each account class to keep track of transactions.

3. **Customer Management**
   - Create a class `Customer` with attributes like `name`, `customer_id`, and a list of accounts.
   - Implement methods to add and remove accounts.

4. **Bank System**
   - Create a class `Bank` to manage customers and accounts. This class should be able to generate reports like total assets, customer lists, and transaction histories.

5. **Iterators and Generators**
   - Implement an iterator for the `Bank` class to iterate over customers.
   - Implement a generator to iterate over transactions in a specified time range.

6. **Decorators**
   - Implement a decorator to log every transaction performed.

### Detailed Requirements

1. **Account Management**
   - Define the abstract class `Account` with private attributes and use property decorators for accessing these attributes. Implement methods to get account details and check the balance.
   - In `CheckingAccount`, override the `withdraw` method to allow overdrafts up to the overdraft limit.
   - In `SavingsAccount`, implement a method to apply interest to the balance.
   - In `BusinessAccount`, override the `withdraw` method to allow withdrawals up to the credit limit.

2. **Transaction Management**
   - Define the `Transaction` class with attributes for the transaction amount, type, and timestamp. Use the `datetime` module to generate timestamps.
   - In each account class, implement a method to log transactions and maintain a list of transactions.

3. **Customer Management**
   - Define the `Customer` class with methods to add and remove accounts. Ensure that a customer cannot have duplicate accounts of the same type.

4. **Bank System**
   - Define the `Bank` class with methods to add and remove customers, generate reports, and find customers by various criteria.
   - Implement a method to calculate the bank's total assets by summing the balances of all accounts.

5. **Iterators and Generators**
   - Implement an iterator in the `Bank` class to iterate over customers, returning each customer object.
   - Implement a generator in the `Account` class to yield transactions within a specified date range.

6. **Decorators**
   - Implement a decorator to log each transaction performed, including the account number, transaction type, amount, and timestamp. Apply this decorator to the deposit and withdraw methods of the account classes.

### Example Usage

Below is a high-level example of how the system could be used:

```python
from datetime import datetime, timedelta
from services import Customer, CheckingAccount, SavingsAccount, BusinessAccount, Bank


# Create customers
customer1 = Customer(name="Alice", customer_id="C001")
customer2 = Customer(name="Bob", customer_id="C002")

# Create accounts
checking_account = CheckingAccount(account_number="A1001", owner=customer1, balance=1000, overdraft_limit=500)
savings_account = SavingsAccount(account_number="A1002", owner=customer1, balance=2000, interest_rate=0.02)
business_account = BusinessAccount(account_number="A2001", owner=customer2, balance=5000, credit_limit=2000)

# Add accounts to customers
customer1.add_account(checking_account)
customer1.add_account(savings_account)
customer2.add_account(business_account)

# Create bank and add customers
bank = Bank()
bank.add_customer(customer1)
bank.add_customer(customer2)

# Perform transactions
checking_account.deposit(200)
checking_account.withdraw(1500)
savings_account.deposit(300)
business_account.withdraw(6000)

# Generate reports
print(bank.generate_total_assets_report())
print(bank.generate_customer_list())
print(checking_account.get_transaction_history())

# Iterate over customers
for customer in bank:
    print(customer.name)

# Use the transaction generator
start_date = datetime.now() - timedelta(days=30)
end_date = datetime.now()
for transaction in checking_account.transaction_generator(start_date, end_date):
    print(transaction)
```

