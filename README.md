# 💰 Income & Expense Tracker in C

> 📒 **Track your income, record your expenses, and see where your money goes.**

[![Maruf Billah — Visit My Portfolio](portfolio-banner.svg)](https://syntaxmaruf-portfolio.curlyriver4.chatgpt.site/)

## 👋 About Me
🎓 I am **Maruf Billah**, a CSE student at **Daffodil International University**. I created this project during my **1st year, 3rd semester**.

## 🤖 My Idea: Learn the Logic, Build with AI
💡 My main goal is to turn a real problem into clear program logic and explain how the solution works. I use AI as a tool to help build the project, explore ideas, and improve the result.

🧠 This project was developed with AI assistance. My focus is on the problem, the choices behind the code, and checking the output. I am still learning C. Understanding every detail takes time, but understanding the main flow and taking responsibility for the result remain important.

## 🎯 What Problem Does It Solve?
💸 Small daily expenses are easy to forget. This program keeps income and expense entries in one place. You can see all entries, check your balance, and view totals for one month.

## ✨ Features
| | Feature | What it does |
| :-: | :--- | :--- |
| ➕ | Add income | Save money you receive, such as salary or pocket money. |
| ➖ | Add expense | Save money you spend, such as food or travel costs. |
| 📋 | View all records | Show each entry with its ID, date, type, amount, category, and note. |
| 💰 | View balance | Show total income minus total expenses. |
| 📅 | Monthly summary | Show income, expenses, and net change for one month. |
| 🗑️ | Delete a record | Find an entry by ID and ask before removing it. |
| 💾 | File storage | Save entries automatically after an add or delete. Load them when the program starts. |
| 🛡️ | Input checks | Check menu numbers, real dates, money amounts, and text length. |

## 🖥️ Main Menu
```text
=== PERSONAL EXPENSE TRACKER ===
1. Add income
2. Add expense
3. View all records
4. View balance
5. Monthly summary
6. Delete a record
0. Exit
```

## 🔄 How the Program Works
🚀 At startup, the program reads saved entries from `expenses.txt`. If there is no data file or backup, it starts with an empty list.

➕ To add income or an expense, choose the matching menu option. Enter a date, amount, category, and note. The program checks the input, gives the entry a new ID, and saves it.

📋 To view records, the program goes through the array and prints each entry. Entries stay in the order they were added.

🧮 To calculate totals, the program adds all income amounts and all expense amounts separately. It subtracts expenses from income.

📅 For a monthly summary, enter any real date in the month you want. For example, `2026-11-01` selects November 2026. The program compares the year and month of each entry.

🗑️ To delete an entry, enter its ID and confirm with `1`. Enter `0` to keep it. The program shifts the later array entries left and saves the change.

## 🧮 Calculation Example
| | Item | Amount |
| :-: | :--- | ---: |
| 💵 | Income | BDT 1000.00 |
| 🍔 | Food expense | BDT 80.50 |
| 🚌 | Travel expense | BDT 50.00 |
| ➖ | Total expenses | BDT 130.50 |
| 💰 | Balance | **BDT 869.50** |

💡 **Balance = total income − total expenses.** A negative balance is allowed. It means recorded expenses are higher than recorded income.

📅 **Monthly net change = income in that month − expenses in that month.** This is the change for that month, not a balance carried forward from earlier months.

## 🧱 How One Record Is Stored
| | Field | Meaning | Example |
| :-: | :--- | :--- | :--- |
| 🔢 | `id` | Unique entry number | `1` |
| 📅 | `date` | Date in Year-Month-Day format | `2026-11-13` |
| 🏷️ | `type` | `I` for income, `E` for expense | `E` |
| 💵 | `amount` | Money stored as whole poisha | `8050` means BDT 80.50 |
| 📂 | `category` | A short group name | `Food` |
| 📝 | `note` | A short explanation | `Lunch` |

🪙 Money uses `long long` integers in poisha. This avoids floating-point rounding in money calculations. The display converts poisha back to Taka with two decimal places.

## 🛠️ Functions Explained
| | Function | Job |
| :-: | :--- | :--- |
| ⌨️ | `readLine()` | Read one line and reject input that is too long. |
| 🔢 | `readNumber()` | Accept a whole number inside the allowed range. |
| 📆 | `validDate()` | Check the format, month length, and leap year. |
| 📅 | `readDate()` | Ask again until a valid date is entered. |
| 🔤 | `readText()` | Accept nonblank printable English text without the pipe symbol. |
| 💵 | `readMoney()` | Read a positive amount with up to two decimal places. |
| 🪙 | `printMoney()` | Display poisha as Taka and poisha. |
| 💾 | `saveData()` | Write entries to a temporary file, then replace the main data file. |
| 📂 | `loadData()` | Load saved entries and check their structure. |
| ➕ | `addRecord()` | Collect an entry, assign an ID, and save it. |
| 📋 | `showRecords()` | Print all entries. |
| 🧮 | `showSummary()` | Calculate all-time or monthly totals. |
| 🗑️ | `deleteRecord()` | Remove an entry after confirmation. |
| 🚀 | `main()` | Load data, show the menu, and call the selected function. |

## 💾 Files and Saving
| | File | Purpose |
| :-: | :--- | :--- |
| 💻 | `expense_tracker.c` | The complete C source code. |
| 📖 | `README.md` | This project guide. |
| 📒 | `expenses.txt` | Your saved entries, created when data is saved. |
| 📝 | `expenses.tmp` | Temporary file used during saving. |
| 🛟 | `expenses.bak` | Previous data file kept during replacement. |

🔍 The data file begins with a format marker and the next ID. Each later line stores one record, with fields separated by `|`.

🛡️ If a save fails, the add or delete is rolled back in memory. If the main file is missing but a backup exists, the program stops and asks you to restore it. If saved data fails the checks, the program stops rather than overwriting it.

⚠️ The backup is a basic safeguard. It is not a full recovery system. Existing backup files can cause later saves to fail on Windows because of how file renaming works. Keep a separate copy of important data and check error messages.

## ✅ Input Rules
| | Input | Rule |
| :-: | :--- | :--- |
| 🔢 | Menu | Whole numbers from 0 to 6. |
| 📅 | Date | A real date from 1900 to 9999, written as `YYYY-MM-DD`. |
| 💵 | Amount | BDT 0.01 to 1,000,000,000.00, with at most two decimal places. |
| 📂 | Category | Up to 30 characters; nonblank printable English text. |
| 📝 | Note | Up to 80 characters; type `None` if no note is needed. |
| 🚫 | Separator | Do not use the pipe symbol in category or note. |

## 🚀 Run the Project
🧰 Install a C compiler such as GCC first. VS Code needs a compiler installed separately.

📥 **1. Clone the repository**
```bash
git clone https://github.com/SyntaxMaruf/Personal-Expense-Tracker.git
cd Personal-Expense-Tracker
```

🔨 **2. Compile**
```bash
gcc -std=c11 -Wall -Wextra expense_tracker.c -o expense_tracker
```

▶️ **3. Run on Windows PowerShell**
```powershell
.\expense_tracker.exe
```

▶️ **3. Run on Linux or macOS**
```bash
./expense_tracker
```

📂 Run the program from the same folder each time. It reads and writes data in the current working folder.

## 🧪 Validation
✅ The supplied source compiled with GCC using `-std=c11 -Wall -Wextra -Werror`.

🔍 See the source and the rules above for what the program checks. Passing a compile check does not prove every possible situation is covered.

## 📚 C Concepts Used
🧱 **Structures and arrays:** keep related entry fields together and hold records in memory.

🔁 **Loops and conditions:** repeat the menu, inspect entries, and choose actions.

🧩 **Functions:** split input, calculations, display, and saving into smaller jobs.

🔤 **Strings and parsing:** read text, compare dates, and convert input into numbers.

📁 **File handling:** use `fopen`, `fprintf`, `fgets`, `fclose`, and `rename` to save and load records.

## 🔎 Limits and Future Ideas
📦 This version allows **1000 successful additions in total**. Deleted IDs are not reused, so deleting entries does not restore the addition allowance.

💻 This is a local terminal program for one user. It has no login, encryption, database, or cloud sync. Avoid running two copies against the same data file.

🛠️ Editing entries, category totals, search, CSV export, and stronger backup recovery are future ideas. They are not included in this version.

## 🙌 Support
⭐ If this project helps you learn, feel free to give it a star.

👨‍💻 **Maruf Billah · CSE · Daffodil International University**

