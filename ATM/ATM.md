## Introduction

An automated teller machine (ATM) is an electronic telecommunications instrument that provides the clients of a financial institution with access to financial transactions in a public space without the need for a cashier or bank teller.
ATMs are necessary as not all the bank branches are open every day of the week, and some customers may not be in a position to visit a bank each time they want to withdraw or deposit money.


## System Requirements

The main components of the ATM that will affect interactions between the ATM and its users are:
1. **Card reader:** to read the users’ ATM cards.
2. **Keypad:** to enter information into the ATM e.g. PIN. cards.
3. **Screen:** to display messages to the users.
4. **Cash dispenser:** for dispensing cash.
5. **Deposit slot:** For users to deposit cash or checks.
6. **Printer:** for printing receipts.
7. **Communication/Network Infrastructure:** it is assumed that the ATM has a communication infrastructure to communicate with the bank upon any transaction or activity.

The user can have two types of accounts: 1) Checking, and 2) Savings, and should be able to perform the following five transactions on the ATM:
1. **Balance inquiry:** To see the amount of funds in each account.
2. **Deposit cash:** To deposit cash.
3. **Deposit check:** To deposit checks. 
4. **Withdraw cash:** To withdraw money from their checking account.
5. **Transfer funds:** To transfer funds to another account.


## How ATM Works ?

The ATM will be managed by an operator, who operates the ATM and refills it with cash and receipts. 
The ATM will serve one customer at a time and should not shut down while serving. 
To begin a transaction in the ATM, the user should insert their ATM card, which will contain their account information. 
Then, the user should enter their Personal Identification Number (PIN) for authentication. 
The ATM will send the user’s information to the bank for authentication; without authentication, the user cannot perform any transaction/service.
The user’s ATM card will be kept in the ATM until the user ends a session. For example, the user can end a session at any time by pressing the cancel button, and the ATM Card will be ejected. The ATM will maintain an internal log of transactions that contains information about hardware failures; this log will be used by the ATM operator to resolve any issues.
1. Identify the system user through their PIN.
2. In the case of depositing checks, the amount of the check will not be added instantly to the user account; it is subject to manual verification and bank approval.
3. It is assumed that the bank manager will have access to the ATM’s system information stored in the bank database.
4. It is assumed that user deposits will not be added to their account immediately because it will be subject to verification by the bank.
5. It is assumed the ATM card is the main player when it comes to security; users will authenticate themselves with their debit card and security pin.


## Use Case

Here are the actors of the ATM system and their use cases:

Operator: The operator will be responsible for the following operations:
1. Turning the ATM ON/OFF using the designated Key-Switch. 
2. Refilling the ATM with cash.
3. Refilling the ATM’s printer with receipts.
4. Refilling the ATM’s printer with INK.
5. Take out deposited cash and checks.

Customer: The ATM customer can perform the following operations:

1. Balance inquiry: the user can view his/her account balance.
2. Cash withdrawal: the user can withdraw a certain amount of cash.
3. Deposit funds: the user can deposit cash or checks.
4. Transfer funds: the user can transfer funds to other accounts.

Bank Manager: The Bank Manager can perform the following operations:

1. Generate a report to check total deposits.
2. Generate a report to check total withdrawals.
3. Print total deposits/withdrawal reports. 
4. Checks the remaining cash in the ATM.


## Class Diagram

Here are the main classes of the ATM System:

1. **ATM:** The main part of the system for which this software has been designed. It has attributes like ‘atmID’ to distinguish it from other available ATMs, and ‘location’ which defines the physical address of the ATM.
2. **CardReader:** To encapsulate the ATM’s card reader used for user authentication.
3. **CashDispenser:** To encapsulate the ATM component which will dispense cash.
4. **Keypad:** The user will use the ATM’s keypad to enter their PIN or amounts.
5. **Screen:** Users will be shown all messages on the screen and they will select different transactions by touching the screen.
6. **Printer:** To print receipts.
7. **DepositSlot:** User can deposit checks or cash through the deposit slot.
8. **Bank:** To encapsulate the bank which ownns the ATM. The bank will hold all the account information and the ATM will communicate with the bank to perform customer transactions.
9. **Account:** We’ll have two types of accounts in the system: 1)Checking and 2)Saving.
10. **Customer:** This class will encapsulate the ATM’s customer. It will have the customer’s basic information like name,email, etc.
11. **Card:** Encapsulating the ATM card that the customer will use to authenticate themselves. Each customer can have one card.
12. **Transaction:** Encapsulating all transactions that the customer can perform on the ATM, like BalanceInquiry, Deposit, Withdraw, etc.


## Code

**Enums and Constants:**

```
public enum TransactionType {
  BALANCE_INQUIRY, DEPOSIT_CASH, DEPOSIT_CHECK, WITHDRAW, TRANSFER
}
public enum TransactionStatus {
  SUCCESS, FAILURE, BLOCKED, FULL, PARTIAL, NONE
}
public enum CustomerStatus {
  ACTIVE, BLOCKED, BANNED, COMPROMISED, ARCHIVED, CLOSED, UNKNOWN
}
public class Address {
  private String streetAddress;
  private String city;
  private String state;
  private String zipCode;
  private String country;
}
```

**Customer, Card, and Account:**


```
public class Customer {
  private String name;
  private String email;
  private String phone;
  private Address address;
  private CustomerStatus status;
  private Card card;
  private Account account;
  public boolean makeTransaction(Transaction transaction);
  public Address getBillingAddress();
}
public class Card {
  private String cardNumber;
  private String customerName;
  private Date cardExpiry;
  private int pin;
  public Address getBillingAddress();
}
public class Account {
  private int accountNumber;
  private double totalBalance;
  private double availableBalance;
  public double getAvailableBalance();
}
public class SavingAccount extends Account {
  private double withdrawLimit;
}
public class CheckingAccount extends Account {
  private String debitCardNumber;
}
```

**Bank, ATM, CashDispenser, Keypad, Screen, Printer and DepositSlot:**

```
public class Bank {
  private String name;
  private String bankCode;
  public String getBankCode();
  public boolean addATM();
}
public class ATM {
  private int atmID;
  private Address location;
  private CashDispenser cashDispenser;
  private Keypad keypad;
  private Screen screen;
  private Printer printer;
  private CheckDeposit checkDeposit;
  private CashDeposit cashDeposit;
  public boolean authenticateUser();
  public boolean makeTransaction(Customer customer, Transaction transaction);
}
public class CashDispenser {
  private int totalFiveDollarBills;
  private int totalTwentyDollarBills;
  public boolean dispenseCash(double amount);
  public boolean canDispenseCash();
}
public class Keypad {
  public String getInput();
}
public class Screen {
  public boolean showMessage(String message);
  public TransactionType getInput();
}
public class Printer {
  public boolean printReceipt(Transaction transaction);
}
public abstract class DepositSlot {
  private double totalAmount;
  public double getTotalAmount();
}
public class CheckDepositSlot extends DepositSlot {
  public double getCheckAmount();
}
public class CashDepositSlot extends DepositSlot {
  public double receiveDollarBill();
}

```

**Transaction and its subclasses:**

```

public abstract class Transaction {
  private int transactionId;
  private TransactionStatus status;
  public boolean makeTransation();
}
public class BalanceInquiry extends Transaction {
  private int accountId;
  public double getAccountId();
}
public abstract class Deposit extends Transaction {
  private double amount;
  public double getAmount();
}
public class CheckDeposit extends Deposit {
  private String checkNumber;
  private String bankCode;
  public String getCheckNumber();
}
public class CashDeposit extends Deposit {
  private double cashDepositLimit;
}
public class Withdraw extends Transaction {
  private double amount;
  public double getAmount();
}
public class Transfer extends Transaction {
  private int destinationAccountNumber;
  public int getDestinationAccount();
}

````


