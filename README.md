# 📖 BookLibraryApp

The starting point of a book library web application built with **ASP.NET Core MVC** and **Entity Framework Core**. It defines the data model (books and authors) and the database configuration that a full library app is built on.

![.NET](https://img.shields.io/badge/.NET-8.0-512BD4?logo=dotnet&logoColor=white)
![ASP.NET Core MVC](https://img.shields.io/badge/ASP.NET%20Core-MVC-5C2D91)
![EF Core](https://img.shields.io/badge/EF%20Core-9.0-6DB33F)
![Status](https://img.shields.io/badge/status-work%20in%20progress-orange)

---

## 📖 Overview

BookLibraryApp sets up the foundations of a library management system:

- an **ASP.NET Core MVC** project with the default layout and home page,
- two domain models, **Book** and **Author**, linked by a one-to-many relationship,
- an **EF Core `DbContext`** that maps those models to a SQL Server database and configures the relationship with the Fluent API,
- the connection string and dependency-injection setup in `Program.cs`.

> ℹ️ This project is a **work in progress**: the model and database layer are in place, but the CRUD pages for books and authors have not been added yet. The finished version of the idea is in the [WebBookLibrary](https://github.com/FarahOUERTANI/WebBookLibrary) repository.

## ✨ What's Implemented

- ✅ MVC project structure (Controllers / Models / Views)
- ✅ `Book` and `Author` entities
- ✅ One-to-many relationship configured in `OnModelCreating`:
  ```csharp
  modelBuilder.Entity<Book>()
      .HasOne(b => b.Author)
      .WithMany(a => a.Books)
      .HasForeignKey(b => b.AuthorId);
  ```
- ✅ `AppDbContext` registered with SQL Server in `Program.cs`
- ⏳ Controllers and views for managing books and authors (to do)
- ⏳ EF Core migrations (to do)

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Framework | ASP.NET Core 8 (MVC) |
| ORM | Entity Framework Core 9 |
| Database | SQL Server LocalDB |
| UI | Razor views, Bootstrap |

## 🗂️ Project Structure

```
BookLibraryApp/
├── Controllers/
│   └── HomeController.cs      # Home, privacy and error pages
├── Data/
│   └── AppDbContext.cs        # DbSets + Book→Author relationship
├── Models/
│   ├── Author.cs              # Id, Name, Biography, DateOfBirth, Books
│   └── Book.cs                # Id, Title, Description, PublishedDate, AuthorId
├── Views/                     # Default Home and Shared views
├── wwwroot/                   # Static files
├── appsettings.json           # Connection string (BookLibraryDb)
└── Program.cs                 # DI registration & pipeline
```

## 🧩 Data Model

| Author | | Book | |
|---|---|---|---|
| `Id` | int (PK) | `Id` | int (PK) |
| `Name` | string | `Title` | string |
| `Biography` | string | `Description` | string |
| `DateOfBirth` | DateTime | `PublishedDate` | DateTime |
| `Books` | collection | `AuthorId` | int (FK → Author) |

## 🚀 Getting Started

### Prerequisites
- [.NET 8 SDK](https://dotnet.microsoft.com/download/dotnet/8.0)
- SQL Server LocalDB (or another SQL Server instance)

### Setup
1. Clone the repository:
   ```bash
   git clone https://github.com/FarahOUERTANI/BookLibraryApp.git
   cd BookLibraryApp/BookLibraryApp
   ```
2. Add the SQL Server provider and the EF Core tools. `Program.cs` calls `UseSqlServer`, which lives in this package:
   ```bash
   dotnet add package Microsoft.EntityFrameworkCore.SqlServer
   ```
   ```bash
   dotnet add package Microsoft.EntityFrameworkCore.Tools
   ```
3. Create the first migration and the database:
   ```bash
   dotnet ef migrations add InitialCreate
   ```
   ```bash
   dotnet ef database update
   ```
4. Run the app:
   ```bash
   dotnet run
   ```
   Then open **https://localhost:7041**.

## 🔮 Next Steps
- Scaffold `BooksController` and `AuthorsController` with their views
- Add validation attributes to the models
- Add navigation links for books and authors

## 👩‍💻 Author

**Farah Ouertani** – [github.com/FarahOUERTANI](https://github.com/FarahOUERTANI)
