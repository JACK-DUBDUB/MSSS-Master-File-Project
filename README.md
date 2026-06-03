# MSSS Master File Project

> **Staff Master File Management System** for Malin Space Science Systems (MSSS)  
> Windows Forms application comparing `Dictionary<int, string>` vs `SortedDictionary<int, string>`

![.NET](https://img.shields.io/badge/.NET-8.0%2B-blueviolet) ![Windows Forms](https://img.shields.io/badge/Windows%20Forms-Desktop-blue) ![C%23](https://img.shields.io/badge/C%23-12.0%2B-green)

---

## Overview

The project delivers a keyboard-driven, multi-window Windows Forms application that manages the staff master file for **Malin Space Science Systems (MSSS)**. Staff members are identified by their UK mobile number (stored as 9-digit integers starting with `77`).

Two functionally identical solutions were developed so performance and usability could be directly compared:

| Solution | Data Structure              | Folder Name                              | Admin Form Name   |
|----------|-----------------------------|------------------------------------------|-------------------|
| 1        | `Dictionary<int, string>`   | `MSSS Master File Project - Dictionary`  | `Form2_Admin`     |
| 2        | `SortedDictionary<int, string>` | `MSSS Master File Project - Sorted Dictionary` | `Form2`       |

Both solutions implement:
- CSV loading into a static master collection
- Real-time filtering by partial name or ID prefix
- Read-only master list + selectable filtered results
- Modal Admin interface for full CRUD operations
- Full keyboard navigation and shortcuts
- Status strip feedback on every major action
- Automatic save back to CSV when Admin closes

---

## Features Implemented

### General Interface (Form1)
- Loads `MalinStaffNamesV3.csv` via `OpenFileDialog`
- Populates a non-selectable read-only `ListBox` with all records
- Real-time filtering into a selectable `ListBox` as you type (name contains / ID starts with)
- Selecting a record populates the detail textboxes
- `Alt + A` opens the Admin form (modal)
- Special Create mode triggered when ID = `77` and name is empty
- Keyboard shortcuts: `F4` / `F5` to clear filters, `Alt + A` to open Admin
- Status strip provides constant feedback

### Admin Interface (Form2 / Form2_Admin)
- Modeless control box removed
- Staff ID field is read-only
- **Create** – validates unique 9-digit ID starting with `77`
- **Update** – modifies name for existing ID
- **Delete** – removes record with confirmation via status strip
- Changes saved to CSV on close (`Alt + L` or Save & Close button)
- Overloaded constructors support both Add and Edit modes
- Comprehensive validation and user feedback

### Technical Quality
- Static `MasterFile` collection (public for controlled access)
- All methods private where appropriate
- Extensive keyboard handling (`Form_KeyDown`)
- Proper modal dialog pattern with data passing
- Error handling + status strip throughout
- Code comments mapping to assessment criteria (Q4–Q7)
- Clean separation into two distinct solutions with different namespaces

---

## Repository Structure

```
MSSS-Master-File-Project/
├── MSSS Master File Project - Dictionary/          # Solution 1
│   ├── Form1.cs              # General GUI (load, filter, display)
│   ├── Form1.Designer.cs
│   ├── Form2_Admin.cs        # Admin GUI (CRUD)
│   ├── Form2_Admin.Designer.cs
│   ├── Program.cs
│   └── MSSS Master File Project - Dictionary.sln
│
├── MSSS Master File Project - Sorted Dictionary/   # Solution 2
│   ├── Form1.cs              # General GUI
│   ├── Form1.Designer.cs
│   ├── Form2.cs              # Admin GUI
│   ├── Form2.Designer.cs
│   ├── Program.cs
│   └── MSSS Master File Project - Sorted Dictionary.sln
│
├── MalinStaffNamesV3.csv     # Staff data file (ID, Name)
├── README.md
└── .git/
```

> **Note:** The two solutions are intentionally kept completely separate (different folders + different `.sln` files) as required by the assessment. They share only the CSV data file at the root.

---

## Getting Started

### Requirements
- Windows 10/11
- Visual Studio 2022 or later (.NET desktop development workload)
- .NET 8.0 SDK or newer

### How to Run

1. Clone the repository:
   ```bash
   git clone https://github.com/JACK-DUBDUB/MSSS-Master-File-Project.git
   cd MSSS-Master-File-Project
   ```

2. Open either solution in Visual Studio:
   - `MSSS Master File Project - Dictionary.sln`
   - or `MSSS Master File Project - Sorted Dictionary.sln`

3. Set **Form1** as the startup form (it already should be).

4. Press `F5` to run.

5. On first run, use the menu or the load functionality to select `MalinStaffNamesV3.csv`.

You can run both solutions side-by-side to compare behaviour and performance.

---

## Keyboard Shortcuts

| Keys          | Location       | Action                                      |
|---------------|----------------|---------------------------------------------|
| `Alt + A`     | General GUI    | Open Admin form (modal)                     |
| `Alt + L`     | Admin GUI      | Save changes & close Admin                  |
| `F4`          | General GUI    | Clear Name filter textbox                   |
| `F5`          | General GUI    | Clear ID filter textbox + refresh           |
| `Tab` / `Shift+Tab` | Both GUIs | Navigate between controls                |
| `Enter`       | Selectable list| Populate detail textboxes                   |

The entire application is designed to be fully operable via keyboard, meeting the "keyboard driven application" requirement.

---

## Performance Testing (Question 8)

Both File I/O methods and the two data structures have been benchmarked using `Stopwatch` and Visual Studio Performance Profiler.

**Key observations from development:**
- Native `StreamReader` + `string.Split` was faster and lighter than `CsvHelper` for this simple two-column dataset.
- `SortedDictionary` generally performed better on initial display and memory usage.
- `Dictionary` had a slight edge on value-based (name) searches.
- Full test results, tables, and profiler screenshots should be added to the assessment document.

---

*This repository contains original student work submitted for assessment purposes.*
