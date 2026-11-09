# COBOL Account Management

## Purpose

This directory documents the COBOL account-management exercise in `src/cobol`. The program provides a menu to view, credit, or debit one account balance. Although this exercise may be used in a student-account context, the current implementation does not identify students or maintain separate accounts per student.

## Source Files

### `main.cob` - `MainProgram`

Entry point and user menu. `MAIN-LOGIC` repeats until the user selects Exit, accepts a menu choice, and dispatches the selected operation by calling `Operations` with one of these six-character operation codes:

- `TOTAL `: view the balance
- `CREDIT`: credit the account
- `DEBIT `: debit the account

Choices outside 1-4 display an invalid-choice message. Choice 4 ends the loop and the program.

### `operations.cob` - `Operations`

Implements account operations based on the operation code received through the `PASSED-OPERATION` linkage item.

- `TOTAL ` calls `DataProgram` with `READ` and displays the returned balance.
- `CREDIT` accepts an amount, reads the current balance, adds the amount, writes the new balance, and displays it.
- `DEBIT ` accepts an amount and reads the current balance. If the balance is at least the requested amount, it subtracts and saves the result. Otherwise, it displays an insufficient-funds message and leaves the stored balance unchanged.

The balance and amount fields use `PIC 9(6)V99`, which represents up to six integer digits and two implied decimal places.

### `data.cob` - `DataProgram`

Provides the balance storage interface. `PROCEDURE DIVISION USING PASSED-OPERATION BALANCE` accepts a `READ` or `WRITE` request: `READ` copies `STORAGE-BALANCE` to the caller's `BALANCE`, while `WRITE` copies the caller's balance into `STORAGE-BALANCE`.

`STORAGE-BALANCE` starts at `1000.00`. It is held in the program's working storage, so this implementation does not persist balances to a file or database across program runs.

## Business Rules and Current Limitations

- The program manages one balance, initialized to `1000.00` for each run.
- A credit adds the entered amount to the balance.
- A debit is allowed only when the current balance is greater than or equal to the entered amount; an insufficient-funds debit is rejected without changing the balance.
- There is no explicit validation for zero or non-positive transaction amounts, malformed input, or amounts beyond the numeric field's capacity.
- No student identifier, student-specific balance, account ownership check, or student eligibility rule is implemented. These rules should not be assumed from the current code.
- Balance data is held in memory only and is not shared across distinct student accounts.
