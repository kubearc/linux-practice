
# Shell Scripting Practice Tasks

---

## 🟢 Task 1: Check User Details

**Objective:**  
Write a script that:
- Accepts a username as input (use `read`)
- Checks whether the user exists on the system (use `id` command)
- If the user exists, print:
  - Their home directory
  - Their login shell

---

## 🟢 Task 2: Count File Content Stats

**Objective:**  
Write a script that:
- Asks the user to enter a file path (e.g., `/etc/passwd`)
- Prints the number of lines, words, and characters in the file  
- Use the `wc` command

---

## 🟢 Task 3: Simple Arithmetic Calculator

**Objective:**  
Write a script that:
- Prompts the user to enter:
  - First number
  - Second number
  - Operator (`+`, `-`, `*`, or `/`)
- Performs the calculation and prints the result

---

## 🟡 Task 4: Backup /var/log with Timestamp

**Objective:**  
Write a script that:
- Creates a compressed tar backup of `/var/log`
- The backup filename must include the current date and time  
  Example output: `var-log-26th-May-03.13.tar.gz`

---

## 🟢 Task 5: Check File or Directory Existence

**Objective:**  
Write a script that:
- Asks the user to input a path
- Checks if the path exists
- Prints whether it is:
  - A regular file
  - A directory
  - Or does not exist

---

## 🟢 Task 6: Check Internet Connectivity

**Objective:**  
Write a script that:
- Pings `google.com`
- Prints "Internet is working" if successful, otherwise "Internet is not reachable"

---

## 🟢 Task 7: Login User Check

**Objective:**  
Write a script that:
- Accepts a username
- Checks if that user is currently logged in using the `who` command

---

## 🟢 Task 8: Number Comparison Script

**Objective:**  
Write a script that:
- Accepts two numbers
- Compares them using `if`, `elif`, and `else`
- Prints which one is greater or if they are equal

---

## 🟢 Task 9: Basic Password Length Checker

**Objective:**  
Write a script that:
- Asks the user to enter a password
- Checks if it is at least 8 characters long
- If yes, print "Password is strong", else print "Password is too short"

**Hint:**  
Use `${#password}` to get the length of the input string. For example - if [ ${#password} -ge 8 ]; then

---
