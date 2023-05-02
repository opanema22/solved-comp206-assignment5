Download Link: https://assignmentchef.com/product/solved-comp206-assignment5
<br>
<strong>Ex. 1 —                      A Banking System Application</strong>

In this exercise, you will create a C program, bankapp.c to implement a simple banking application.

Your application provides three capabilities: (i) Add an account number, (ii) Make a deposit, (iii) Make a withdrawal. All of your banking data is stored in a CSV file bankdata.csv which has the following format. You can use vi to create a sample data file of your own for testing purposes.

AC,2023,Jane Smith

TX,2023,2020-02-10,1023.34

AC,5023,Sally Long

TX,2023,2020-02-10,-103.34

TX,5023,2020-01-15,78.00

As can be seen above, there are two kinds of records in this CSV file. (i) Account records, indicated by AC in the first field, followed by a 4 digit account number, followed by the name of the account holder (max 30 characters long). (ii) Then there are transaction records that are indicated by TX in the first field, followed by the account number, transaction date in YYYY-MM-DD format, followed by the amount of money deposited or withdrawn (negative values for the latter).

1.Use vi to create a C program source file bankapp.c

2.<strong> </strong>The program should include a comment section at the beginning that describes its purpose (couple of lines), the author (your name), your department, a small “history” section indicating what changes you did on what date. The code should be properly indented for readability as well as contain any additional comments required to understand the program logic.

3.The source code should be compilable by (exactly) using the command gcc -o bankapp bankapp.c

4.<strong> </strong>The compilation step should not issue any warnings.

5.<strong> </strong>All the error messages must be printed to stderr and not stdout.

6.<strong> </strong>Your program’s usage is as follows. To add a new account

$ ./bankapp -a ACCTNUM NAME

To make a deposit

$ ./bankapp -d ACCTNUM DATE AMOUNT

To make a withdrawl

$ ./bankapp -w ACCTNUM DATE AMOUNT

Any other attempt must throw a usage error. <strong>You may however, chose to ignore the extra arguments passed to any of the above valid options at your discretion and continue processing. </strong>The exit code for invalid usage of your program should be 1.

$ ./bankapp

Error, incorrect usage!

-a ACCTNUM NAME

-d ACCTNUM DATE AMOUNT

-w ACCTNUM DATE AMOUNT

$ echo $?

1

In case the user passed a valid option but did not pass sufficient arguments to process it, provide a more customized error message.

$ ./bankapp -a 1024

Error, incorrect usage!

-a ACCTNUM NAME

$ echo $?

1

$ ./bankapp -d 1024 2010-02-12

Error, incorrect usage!

-d ACCTNUM DATE AMOUNT

$ echo $?

1

$ ./bankapp -w 1024

Error, incorrect usage!

-w ACCTNUM DATE AMOUNT

$ echo $?

1

7Your program should read the data contents from a CSV file, bankdata.csv. It must be present in the current directory. If the program cannot find it, it must thrown an error and terminate with code 100.

$ ./bankapp -a 1024 “John Smith”

Error, unable to locate the data file bankdata.csv

$ echo $?

100

8.<strong>(2 Points) </strong>Your program must allow new accounts to be added. These accounts will be appended to the data file bankdata.csv.

$ ./bankapp -a 1024 “John Doe”

$ tail -1 bankdata.csv

AC,1024,John Doe

If the account number already exists (as indicated by the AC records), then the program should not add it, instead throw an error message to indicate this and terminate with error code 50.

$ ./bankapp -a 1024 “John Doe”

Error, account number 1024 already exists

$ echo $?

50

9.<strong> </strong>Your program should facilitate deposits to an existing account. A transaction record indicating the amount of money to be deposited is then appended to the data file.

$ ./bankapp -d 1024 2020-02-12 334.52

$ tail -1 bankdata.csv

TX,1024,2020-02-12,334.52

If the account does not exist, it should throw an error message and terminate with code 50.

$ ./bankapp -d 1025 2020-02-12 334.52

Error, account number 1025 does not exists

$ echo $?

50

10.<strong> </strong>Your program should facilitate withdrawals from an existing account. A transaction record indicating the amount of money that is withdrawn is then appended to the data file.

$ ./bankapp -w 1024 2020-02-14 20.00

$ tail -1 bankdata.csv

TX,1024,2020-02-14,-20.00

If the account does not exist, it should throw an error message and terminate with code 50.

$ ./bankapp -w 1025 2020-02-14 20.00

Error, account number 1025 does not exists

$ echo $?

50

If the account does not have enough balance, it should display an error message, and also indicate the current balance in the account. Terminate with code 60. You should be able to compute the existing balance on the account by adding up all the deposits and withdrawals on the account. Make sure that the amounts you print on the screen has only 2 decimal places.

$ ./bankapp -w 1024 2020-02-15 2020.00

Error, account number 1024 has only 314.52

11.<strong> </strong>Remember to terminate the successful execution of your program with code 0.

12.Your program must not crash because the data file is empty (or at any other situation). Instead it should do the proper processing according to the scenarios already described earlier. (i.e, add a new account, let the user know the account does not exist for a transaction, etc.).

13.<strong> </strong>Your program should include some function definitions of your own. At a minimum, you should have one function per operator. You are free to have additional functions in your program.

<strong>** Important ** </strong>If your program “hangs” / is stuck while executing it through the tester script and requires TAs to interrupt it, you will loose  If your program causes corruption of the data file for any of the test cases, you will loose <strong>4 points</strong>.