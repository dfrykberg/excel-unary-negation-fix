# excel-unary-negation-fix
A Python script to audit and patch high-risk unary negation precedence bugs in Excel formulas.
# Excel Unary Negation Audit & Patch Tool

A Python-based safety utility designed for structural engineers, financial modelers, and data analysts to scan directories of `.xlsx` spreadsheets and flag hidden mathematical order-of-operations risks caused by Microsoft Excel's legacy operator precedence hierarchy.

## The Mathematical Risk
In standard algebraic notation (BEDMAS/PEMDAS), exponentiation binds tighter than a leading negative sign. Therefore, the expression `-4^2` or `=-(2+2)^2` must evaluate to `-16`. 

Microsoft Excel uniquely violates this rule by evaluating **unary negation first**, incorrectly yielding a positive `16`. 

While harmless in isolation (e.g., `=-A1`), this quirk can introduce severe, silent sign-inversion calculations in complex engineering or financial sheets where the formula designer assumed standard mathematical laws would apply. This tool isolates and reports only the instances where a leading negative sign is directly paired with a trailing power operation (`^` or `POWER()`), completely ignoring harmless negation.

---

## 📚 Non-Programmer's Guide to Running the Tool

You do not need to know how to code to use this script. Follow these simple steps:

### Step 1: Install Python
1. Download **Python 3.x** from the official site: https://python.org
2. Run the installer.
3. **CRITICAL STEP (Windows):** On the very first installation screen, check the box at the bottom that reads **"Add python.exe to PATH"**. Complete the installation wizard.

### Step 2: Open Your Command Interface
* **Windows:** Press the Windows Key, type `cmd`, and press Enter.
* **Mac:** Press Cmd + Space, type `Terminal`, and press Enter.

### Step 3: Install the Excel Plugin
In your Command Prompt or Terminal window, type the following command and press Enter:
```bash
pip install openpyxl
```

### Step 4: Run the Script
1. Download `excel_math_audit.py` from this repository and save it to your desktop.
2. In your Terminal or Command Prompt, point your system to your desktop folder by typing:
```bash
cd Desktop
```
3. Launch the tool by typing:
```bash
python excel_math_audit.py
```
4. Paste the full folder path containing your Excel files when prompted.

---

## Technical Features
* **Safe Mode First:** The script initially executes a 100% read-only scan, mapping exactly which file, worksheet, and cell coordinate holds a high-risk formula string.
* **Optional Automatic Patching:** If risks are detected, the user can optionally authorize the script to restructure the cell formulas securely, rewriting the misleading sequence from `=-` to `=0-` (forcing standard subtraction behavior).
* **Whitespace Insensitive:** The internal parser dynamically catches and resolves human spacing anomalies (e.g., catching `=-`, `= -`, and `=  -  `).

## License
Distributed under the MIT License. See `LICENSE` for more information.
