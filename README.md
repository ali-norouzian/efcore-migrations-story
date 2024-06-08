# efcore-migrations-story


Entity Framework Core (EF Core) migrations provide a way to incrementally update the database schema to keep it in sync with your EF Core model. Here’s a detailed explanation of the EF Core migrations system, including how to roll back to a previous migration, delete the last migration, and delete a specific migration.

### EF Core Migrations Overview

EF Core migrations allow you to:

1. **Create a new migration**: Capture the changes in your model and create a new migration script.
2. **Apply migrations**: Update the database schema to match the changes defined in the migration scripts.
3. **Remove migrations**: Remove a migration that you no longer need.

### Creating a New Migration

To create a new migration, you use the `Add-Migration` command in the Package Manager Console (PMC) or the `dotnet ef migrations add` command in the terminal.

**Example:**

- **Package Manager Console:**
  ```powershell
  Add-Migration InitialCreate
  ```
- **Command Line:**
  ```bash
  dotnet ef migrations add InitialCreate
  ```

This command generates a new migration script based on the current state of your EF Core model.

### Applying Migrations

To apply migrations and update the database schema, use the `Update-Database` command in the PMC or the `dotnet ef database update` command in the terminal.

**Example:**

- **Package Manager Console:**
  ```powershell
  Update-Database
  ```
- **Command Line:**
  ```bash
  dotnet ef database update
  ```

This command applies all pending migrations to the database.

### Rolling Back to a Previous Migration

To roll back to a previous migration, use the `Update-Database` command with the target migration name.

**Example:**

- **Package Manager Console:**
  ```powershell
  Update-Database InitialCreate
  ```
- **Command Line:**
  ```bash
  dotnet ef database update InitialCreate
  ```

This command reverts the database schema to the state defined by the specified migration.

### Deleting the Last Migration

To delete the last migration, you must first roll back the migration using the `Update-Database` command and then remove the migration script.

**Example:**

- **Step 1: Roll back the last migration**
  - **Package Manager Console:**
    ```powershell
    Update-Database PreviousMigrationName
    ```
  - **Command Line:**
    ```bash
    dotnet ef database update PreviousMigrationName
    ```

  Replace `PreviousMigrationName` with the name of the migration just before the last one.

- **Step 2: Remove the last migration**
  - **Package Manager Console:**
    ```powershell
    Remove-Migration
    ```
  - **Command Line:**
    ```bash
    dotnet ef migrations remove
    ```

### Deleting a Specific Migration

To delete a specific migration, you need to manually edit the Migrations folder and the database.

1. **Roll back to the migration before the one you want to delete**:
   - **Package Manager Console:**
     ```powershell
     Update-Database MigrationBeforeTarget
     ```
   - **Command Line:**
     ```bash
     dotnet ef database update MigrationBeforeTarget
     ```

   Replace `MigrationBeforeTarget` with the name of the migration just before the one you want to delete.

2. **Delete the migration files**: Delete the .cs file for the migration you want to remove from the Migrations folder.

3. **Update the Migration History Table**: If the migration was applied to the database, you might need to manually update the `__EFMigrationsHistory` table in the database to remove the entry for the deleted migration.

### Common Commands

- **Add Migration**:
  ```powershell
  Add-Migration MigrationName
  ```
  ```bash
  dotnet ef migrations add MigrationName
  ```

- **Update Database**:
  ```powershell
  Update-Database
  ```
  ```bash
  dotnet ef database update
  ```

- **Remove Last Migration**:
  ```powershell
  Remove-Migration
  ```
  ```bash
  dotnet ef migrations remove
  ```

### Summary

EF Core migrations provide a robust way to manage database schema changes over time. Understanding how to create, apply, roll back, and delete migrations is essential for maintaining a healthy and consistent database schema. By following the steps outlined above, you can effectively manage your database schema changes with EF Core migrations.
