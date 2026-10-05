# Employee Management System

A small Java system for Organization X that registers employees, processes their
payments (including overtime, a department bonus, and bracketed tax rules), and
produces a payroll report. Built as part of a Software Testing course assignment,
with a full black-box and white-box test suite.

## Case study

> The organization needs to manage its employees, process their payments, and
> generate reports.

## Functional requirements

| ID | Requirement |
|----|-------------|
| FR1 | The system shall allow adding a new employee record with an ID, name, department, and base salary. |
| FR2 | The system shall reject employee registration when the ID or name is missing/empty, the base salary is negative, or the ID is already in use. |
| FR3 | The system shall allow an existing employee record to be removed by ID, and shall report when the ID does not exist. |
| FR4 | The system shall compute an employee's net payment from base salary, overtime hours (at 1.5x the hourly rate), a 10% bonus for the Management department, and a tax rate that depends on the resulting gross pay (25% at or above 5000, otherwise 15%). |
| FR5 | The system shall reject payment processing when the employee ID is not registered or when hours/overtime hours are negative. |
| FR6 | The system shall generate a payroll report listing each employee's net pay, the total payroll, the average net pay, and the top earner; and shall state clearly when there are no employees to report. |
| FR7 | The system shall be able to report the current number of registered employees. |

## Business rules

- Overtime is paid at **1.5x** the employee's derived hourly rate (`base salary / 160` standard hours).
- Employees in the **Management** department receive a **10% bonus** on gross pay.
- Gross pay **at or above 5000** is taxed at **25%**; below 5000 it is taxed at **15%**.
- Employee ID, name, and salary are validated on registration; duplicate IDs are rejected.

## Project structure

```
src/ems/
├── Employee.java                     # Employee data model
├── EmployeeManagementSystem.java     # Business logic + interactive console menu
└── EmployeeManagementSystemTest.java # Black-box and white-box test suite (no dependencies)
```

## Requirements

- Java Development Kit (JDK) 8 or later. Check with:
```
  java -version
```

## How to run

Clone the repository, then from its root folder:

```bash
# 1. Compile
javac -d build src/ems/*.java

# 2. Run the interactive console app (add employees, process payments, see reports)
java -cp build ems.EmployeeManagementSystem

# 3. Run the automated test suite
java -cp build ems.EmployeeManagementSystemTest
```

### Example: using the console app

```
==== Employee Management System ====
1. Add employee
2. Remove employee
3. Process payment
4. Generate payroll report
5. Show employee count
6. Exit
Choose an option (1-6): 1
Employee ID: E001
Name: Alice Uwase
Department: Engineering
Base salary: 3000
Employee added successfully.
```

## Testing

No external test framework is required — `EmployeeManagementSystemTest` is a
small, self-contained harness that prints `[OK]` or `[FAIL]` per test case and
a final summary.

- **Black-box tests (BB-01 – BB-12)**: derived from the functional requirements
  above using equivalence partitioning and boundary value analysis, without
  reference to the source code.
- **White-box tests (WB-01 – WB-06)**: derived from the source code itself,
  each one forcing a specific branch (e.g. the exact tax-bracket boundary, the
  Management bonus combined with overtime) that the black-box tests do not
  reach.

Current result: **18 / 18 test cases pass.**

Full results, with inputs, expected results, and the real observed output,
are documented in [`docs/Test-Case-Report.docx`](docs/Test-Case-Report.docx).

## Author

Agape Gift ([@AgapegifT](https://github.com/AgapegifT))
