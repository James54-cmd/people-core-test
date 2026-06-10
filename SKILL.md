# People Core HRIS - Frontend Development Standards

## Philosophy

The frontend follows a **Component-Based Architecture** built with **Blazor and MudBlazor**.

MudBlazor is the official design system of the application. All UI should be built using MudBlazor components whenever possible to ensure consistency, accessibility, responsiveness, and maintainability.

Pages orchestrate components and application state. Components encapsulate presentation and reusable UI behavior.

---

# Technology Stack

## Frontend Framework

- Blazor Server
- .NET 10

## UI Framework

- MudBlazor

## Styling

- MudBlazor Theme
- Utility classes only when necessary
- No inline styles unless dynamic values require them

## Icons

- MudBlazor Icons

## State

- Local component state by default
- Cascading parameters only when appropriate
- Shared state only for application-wide concerns

---

# Core Principles

## 1. Single Responsibility Principle

Every component should have one responsibility.

✅ Good

- EmployeeCard
- AttendanceSummaryCard
- LeaveBalanceCard
- EmployeeTable

❌ Bad

- EmployeeDashboardEverythingComponent

---

## 2. Reusability

If UI appears more than once, create a reusable component.

Examples:

- SearchBar
- PageHeader
- StatusChip
- ConfirmDialog
- EmptyState
- LoadingOverlay
- FilterPanel
- StatisticsCard

Never duplicate markup.

---

## 3. Composition over Complexity

Pages should compose feature components.

```text
EmployeePage

├── EmployeeHeader
├── EmployeeStatistics
├── EmployeeFilter
├── EmployeeTable
├── EmployeePagination
└── EmployeeDialogs
```

Avoid pages containing hundreds of lines of mixed markup and logic.

---

# MudBlazor Standards

## Always Prefer MudBlazor Components

Use:

- MudGrid
- MudStack
- MudPaper
- MudCard
- MudButton
- MudIconButton
- MudTable
- MudDataGrid
- MudTextField
- MudSelect
- MudAutocomplete
- MudDatePicker
- MudDialog
- MudSnackbar
- MudTabs
- MudChip
- MudAvatar
- MudMenu
- MudNavMenu

Avoid recreating components that already exist in MudBlazor.

---

## Layout

Use:

```text
MudLayout

    MudAppBar

    MudDrawer

    MudMainContent
```

Never build a custom layout using nested divs when MudLayout provides the same functionality.

---

## Spacing

Prefer:

```text
MudStack

MudGrid

Spacing Parameter
```

Avoid excessive manual margins and paddings.

Maintain consistent spacing throughout the application.

---

## Typography

Always use MudText.

Page Title → H4

Section Title → H5

Body → Body1

Caption → Caption

Avoid inconsistent typography.

---

## Forms

Always use MudBlazor inputs.

- MudTextField
- MudSelect
- MudAutocomplete
- MudNumericField
- MudDatePicker
- MudCheckBox
- MudSwitch

Do not mix native HTML inputs with MudBlazor controls.

---

## Dialogs

Use MudDialog for:

- Create
- Edit
- Delete Confirmation
- Details
- Approval Actions

Avoid navigating to separate pages for simple CRUD operations.

---

## Notifications

Always use MudSnackbar.

Never use browser alerts.

---

## Loading

Use:

- MudSkeleton
- MudProgressCircular
- MudProgressLinear

Every async operation should have visible feedback.

---

# Folder Structure

```text
Components/

    Layout/

        AppLayout
        Sidebar
        TopBar
        Footer

    Shared/

        Buttons/
        Cards/
        Dialogs/
        Tables/
        Inputs/
        Chips/

    Common/

        EmptyState
        LoadingState
        ErrorState
        SearchBar
        PageHeader

    Features/

        Dashboard/

        Employees/

            Components/

            Dialogs/

        Attendance/

        Leave/

        Payroll/

        Recruitment/

        Settings/

Pages/

Services/

Models/

DTOs/

Constants/

Enums/

Extensions/

Helpers/

wwwroot/
```

Feature-specific components belong inside their feature folder.

Only generic reusable components belong in Shared.

---

# Page Responsibilities

Pages should:

- Load data
- Coordinate components
- Manage page state
- Handle navigation
- Handle authorization
- Call services

Pages should NOT:

- Contain duplicated UI
- Build dialogs inline
- Build tables inline
- Mix multiple unrelated concerns
- Exceed reasonable complexity

---

# Component Responsibilities

Components should:

- Receive Parameters
- Expose EventCallbacks
- Display UI
- Be reusable
- Be presentation-focused

Components should NOT:

- Know about unrelated modules
- Handle application routing unnecessarily
- Access global state without need

---

# State Management

Prefer:

```text
Parent Page

↓

Child Component

↓

EventCallback

↓

Parent Updates State
```

Global state should be limited to:

- Current User
- Theme
- Sidebar State
- Notifications
- Authentication Context

---

# Naming Convention

Components

```text
EmployeeCard

AttendanceTable

LeaveBalanceCard

StatisticsCard

PageHeader
```

Methods

```text
LoadEmployees()

SearchEmployees()

OpenDialog()

DeleteEmployee()

RefreshAsync()
```

Booleans

```text
IsLoading

IsOpen

IsEditing

CanApprove

HasPermission
```

Collections

```text
Employees

Departments

AttendanceRecords

LeaveRequests
```

---

# CRUD Standards

Every management page should provide:

- Search
- Filters
- Sorting
- Pagination
- Create
- Edit
- Delete
- View Details

Large datasets should use server-side pagination.

---

# Responsive Design

Support:

- Mobile
- Tablet
- Desktop

Desktop:

- Permanent Drawer
- Multi-column layout

Tablet:

- Collapsible Drawer

Mobile:

- Overlay Drawer
- Single-column layout
- Full-width actions

Avoid fixed widths whenever possible.

---

# Authorization Awareness

## Admin

- User Management
- Payroll
- Company Settings
- Reports
- Audit Logs

## Manager

- Team Dashboard
- Team Attendance
- Team Leave Approval
- Department Reports

## Employee

- Personal Dashboard
- Attendance
- Leave Requests
- Payslips
- Profile

The UI should render only actions relevant to the current role.

---

# Code Quality Rules

Avoid:

- Duplicate code
- Inline styles
- Hardcoded colors
- Hardcoded spacing
- Long methods
- Large Razor files
- Copy-pasted dialogs
- Magic numbers

Prefer:

- Reusable components
- Theme configuration
- Constants
- Enums
- Helper methods
- Shared UI primitives

---

# Performance Guidelines

- Use server-side pagination
- Debounce search
- Lazy-load heavy content
- Minimize unnecessary re-rendering
- Keep components focused and lightweight

---

# Definition of Done

A frontend feature is complete only when it:

- Uses MudBlazor components consistently
- Is responsive
- Uses reusable components
- Handles loading, empty, and error states
- Follows naming conventions
- Respects role-based permissions
- Avoids duplicate code
- Uses the application theme instead of custom styling
- Is maintainable and extensible
- Keeps pages focused on orchestration while components handle presentation

The goal is to build an enterprise-grade HRIS frontend where every feature integrates seamlessly into a unified Blazor and MudBlazor design system.
