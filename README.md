# 💪 Fitness Platform - Comprehensive Fitness & Nutrition Management System

[![.NET](https://img.shields.io/badge/.NET-8.0-512BD4?style=flat&logo=dotnet)](https://dotnet.microsoft.com/)
[![SQL Server](https://img.shields.io/badge/SQL%20Server-2022-CC2927?style=flat&logo=microsoft-sql-server)](https://www.microsoft.com/sql-server)
[![SignalR](https://img.shields.io/badge/SignalR-Real--time-00ADD8?style=flat)](https://dotnet.microsoft.com/apps/aspnet/signalr)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

A comprehensive fitness management platform connecting trainers, nutritionists, and trainees. Built with **Clean Architecture** principles, featuring real-time messaging, workout video management, nutrition planning, and role-based access control.

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Tech Stack](#-tech-stack)
- [Architecture](#-architecture)
- [Features](#-features)
- [Project Structure](#-project-structure)
- [Getting Started](#-getting-started)
- [API Endpoints](#-api-endpoints)
- [Future Improvements](#-future-improvements)
- [Screenshots](#-screenshots)
- [Contributing](#-contributing)
- [Contact](#-contact)

---

## 🎯 Overview

The Fitness Platform is a full-stack solution designed to bridge the gap between fitness professionals and trainees. It provides a centralized ecosystem where trainers can share workout videos, nutritionists can create meal plans, and trainees can track their fitness journey with personalized guidance.

**Key Highlights:**
- Multi-role authentication system (Admin, Trainer, Nutritionist, Trainee)
- Real-time messaging using SignalR
- Comprehensive video management with reviews and ratings
- Nutrition plan creation and assignment
- User profile management with fitness metrics
- Custom role-based authorization attributes

---

## 🛠 Tech Stack

### Backend
- **Framework:** ASP.NET Core 8.0 Web API
- **ORM:** Entity Framework Core 9.0
- **Database:** SQL Server
- **Authentication:** ASP.NET Core Identity + JWT
- **Real-time Communication:** SignalR
- **API Documentation:** Swagger/OpenAPI

### Architecture Patterns
- Clean Architecture (3-Layer)
- Repository Pattern
- Unit of Work Pattern
- Dependency Injection
- Custom Authorization Attributes

---

## 🏗 Architecture

The solution follows **Clean Architecture** with clear separation of concerns across three main layers:

```
Fitness-Platform/
│
├── FitCore/                    # Domain Layer
│   ├── Models/                 # Domain entities
│   ├── Dto/                    # Data transfer objects
│   └── IRepositories/          # Repository interfaces
│
├── FitData/                    # Data Access Layer
│   ├── Data/                   # DbContext
│   ├── Repositories/           # Repository implementations
│   └── Migrations/             # EF Core migrations
│
└── Fit/                        # Presentation Layer
    ├── Controllers/            # API endpoints
    └── Authorization/          # Custom authorization attributes
```

### Key Design Patterns

**Custom Role-Based Authorization**
- Attribute-based authorization for each role
- `[AdminAuthorize]`, `[TrainerAuthorize]`, `[TraineeAuthorize]`, `[NutritionistAuthorize]`
- Automatic role validation with meaningful error messages

**Unit of Work Pattern**
- Centralized transaction management
- Single point of database commit
- Cleaner service orchestration

**Repository Pattern**
- Abstraction over data access
- Easier testing and maintainability
- Separation of concerns

---

## ✨ Features

### 🔐 Authentication & Authorization
- ✅ JWT-based authentication
- ✅ Role-based registration (Admin, Trainer, Nutritionist, Trainee)
- ✅ Custom authorization attributes for each role
- ✅ Secure password management
- ✅ User profile with fitness metrics

### 👥 User Management
- ✅ Multi-role user system
- ✅ Profile management (height, weight, age, gender, fitness level)
- ✅ Password change functionality
- ✅ User search by name or ID
- ✅ Role-specific data filtering

### 🎥 Video Management (Trainers)
- ✅ CRUD operations for workout videos
- ✅ Video categorization by:
  - **Exercise Type** (Shoulder, Back, Chest, Legs, Arms, Core, Cardio, Abs)
  - **Difficulty Level** (Beginner, Intermediate, Advanced)
- ✅ Video ownership validation
- ✅ Trainer-specific video library

### ⭐ Video Reviews (Trainees)
- ✅ Rate and review workout videos
- ✅ One review per trainee per video
- ✅ Edit and delete own reviews
- ✅ View reviews with full user context
- ✅ Public and authenticated review endpoints

### 🥗 Nutrition Planning (Nutritionists)
- ✅ Create personalized meal plans
- ✅ Assign plans to specific trainees
- ✅ Plan categorization by meal type (Breakfast, Lunch, Dinner, Snack)
- ✅ Edit and soft-delete plans
- ✅ Nutritionist-specific plan management
- ✅ Admin oversight of all plans

### 💬 Real-Time Messaging
- ✅ SignalR-powered chat system
- ✅ One-on-one messaging between users
- ✅ Message history retrieval
- ✅ Timestamp tracking
- ✅ Database-persisted messages

### 🔍 Search & Discovery
- ✅ Search users by name or ID
- ✅ Get all trainees, trainers, or nutritionists
- ✅ Role-filtered user listings
- ✅ Comprehensive user profiles in search results

---

## 📂 Project Structure

<details>
<summary>Click to expand detailed structure</summary>

```
Fitness-Platform-master/
│
├── Fit/ (Presentation Layer)
│   ├── Controllers/
│   │   ├── AuthController.cs
│   │   ├── ProfileController.cs
│   │   ├── VideoController.cs
│   │   ├── VideoReviewController.cs
│   │   ├── NutritionistController.cs
│   │   ├── SearchController.cs
│   │   └── MessagesController.cs
│   ├── Authorization/
│   │   ├── RoleAuthorizeAttribute.cs
│   │   ├── AdminAuthorizeAttribute.cs
│   │   ├── TrainerAuthorizeAttribute.cs
│   │   ├── TraineeAuthorizeAttribute.cs
│   │   └── NutritionistAuthorizeAttribute.cs
│   ├── Program.cs
│   └── appsettings.json
│
├── FitCore/ (Domain Layer)
│   ├── Models/
│   │   ├── ApplicationUser.cs
│   │   ├── Video.cs
│   │   ├── VideoReview.cs
│   │   ├── NutritionPlans.cs
│   │   ├── TraineerReview.cs
│   │   ├── ChatMessage.cs
│   │   ├── Level.cs
│   │   ├── ExerciseType.cs
│   │   └── MealType.cs
│   ├── Dto/
│   │   ├── Authentication/
│   │   ├── Profile/
│   │   ├── Admin/
│   │   ├── NutritionistAndPlan/
│   │   ├── VideoReview/
│   │   └── Search/
│   └── IRepositories/
│       ├── IAuthServices.cs
│       ├── IVideoService.cs
│       ├── IVideoReviewServices.cs
│       ├── INutritionistServices.cs
│       ├── ISearch.cs
│       ├── IMessageStore.cs
│       └── IUnitOfWork.cs
│
└── FitData/ (Data Access Layer)
    ├── Data/
    │   └── ApplicationDbContext.cs
    ├── Repositories/
    │   ├── AuthServices.cs
    │   ├── VideoService.cs
    │   ├── VideoReviewServices.cs
    │   ├── NutritionistServices.cs
    │   ├── Search.cs
    │   ├── ChatHub.cs
    │   ├── EFMessageStore.cs
    │   └── UnitOfWork.cs
    └── Migrations/
```

</details>

---

## 🚀 Getting Started

### Prerequisites

- [.NET 8.0 SDK](https://dotnet.microsoft.com/download/dotnet/8.0)
- [SQL Server 2022](https://www.microsoft.com/sql-server/sql-server-downloads) or SQL Server Express
- [Visual Studio 2022](https://visualstudio.microsoft.com/) or [VS Code](https://code.visualstudio.com/)
- [Git](https://git-scm.com/)

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/Ahmed-M-Sabry/Fitness-Platform.git
cd Fitness-Platform
```

2. **Configure the database**

Update the connection string in `appsettings.json`:
```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=.;Database=FitnessDB;Trusted_Connection=True;MultipleActiveResultSets=true;TrustServerCertificate=True"
  }
}
```

3. **Configure JWT settings**

Update JWT configuration in `appsettings.json`:
```json
{
  "JWT": {
    "Key": "YourSuperSecretKeyHereMustBe32CharsMin",
    "Issuer": "FitnessAPI",
    "Audience": "FitnessClient",
    "DurationInDays": 30
  }
}
```

4. **Apply database migrations**
```bash
cd FitData
dotnet ef database update --startup-project ../Fit
```

5. **Run the application**
```bash
cd ../Fit
dotnet run
```

The API will be available at `https://localhost:7XXX` and Swagger UI at `https://localhost:7XXX/swagger`

### Database Seeding

The database includes lookup tables that should be seeded:
- **Levels:** Beginner (1), Intermediate (2), Advanced (3)
- **ExerciseTypes:** Shoulder, Back, Chest, Legs, Arms, Core, Cardio, Abs, Cardio
- **MealTypes:** Breakfast (1), Dinner (2), Lunch (3), Snack (4)

---

## 📡 API Endpoints

### Authentication
| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| POST | `/Register-Admin` | Register admin user | No |
| POST | `/Register-Trainee` | Register as trainee | No |
| POST | `/Register-Trainer` | Register as trainer | No |
| POST | `/Register-Nutritionist` | Register as nutritionist | No |
| POST | `/Login` | User login | No |

### Profile Management
| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/api/Profile/User-Profile` | Get current user profile | Yes |
| PUT | `/api/Profile/UpdateProfile` | Update user profile | Yes |
| PUT | `/api/Profile/ChangePassword` | Change password | Yes |

### Videos (Trainers Only)
| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/api/Video/Get-My-Videos` | Get trainer's videos | Trainer |
| GET | `/api/Video/Get-Video-By-Id` | Get video by ID | Trainer |
| POST | `/api/Video/Add-Video` | Create new video | Trainer |
| PUT | `/api/Video/Edit-Video/{id}` | Update video | Trainer |
| DELETE | `/api/Video/Delete-Video/{id}` | Delete video | Trainer |

### Video Reviews (Trainees Only)
| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/api/VideoReview/Get-My-Videos-Reviews` | Get trainee's reviews | Trainee |
| GET | `/api/VideoReview/Get-Video-Reviews-By-Id-Login` | Get review by ID | Trainee |
| GET | `/api/VideoReview/Get-Video-Reviews-By-Id-Wihout-Login` | Get review (public) | No |
| POST | `/api/VideoReview/Add-Video-Review` | Create review | Trainee |
| PUT | `/api/VideoReview/Edit-Video-Review` | Update review | Trainee |
| DELETE | `/api/VideoReview/Delete-Video-Review` | Delete review | Trainee |

### Nutrition Plans (Nutritionists)
| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/api/Nutritionist/Get-My-Plans` | Get nutritionist's plans | Nutritionist |
| GET | `/api/Nutritionist/Get-By-Id` | Get plan by ID | Nutritionist |
| GET | `/api/Nutritionist/Get-All-Plans-Admin` | Get all plans | Admin |
| POST | `/api/Nutritionist/Create-Plan` | Create nutrition plan | Nutritionist |
| PUT | `/api/Nutritionist/Edit-Plan` | Update plan | Nutritionist |
| PUT | `/api/Nutritionist/Delete-Plan` | Soft delete plan | Nutritionist |

### Search
| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/Get-All-Trainees` | List all trainees | No |
| GET | `/Get-All-Trainers` | List all trainers | No |
| GET | `/Get-All-Nutritionist` | List all nutritionists | No |
| GET | `/Get-By-Name` | Search user by name | No |
| GET | `/Get-By-Id` | Get user by ID | No |

### Real-Time Messaging
| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| POST | `/api/messages/send` | Send message | Yes |
| POST | `/api/messages` | Get message history | Yes |
| **SignalR Hub** | `/chatHub` | Real-time chat connection | Yes |

---

## 🔮 Future Improvements

### Short-term (Next Sprint)
- [ ] Implement workout program builder
- [ ] Add progress tracking for trainees
- [ ] Implement appointment booking system
- [ ] Add video streaming support
- [ ] Implement payment integration for premium features

### Medium-term
- [ ] Build mobile app (Flutter/React Native)
- [ ] Add unit and integration tests
- [ ] Implement CI/CD pipeline
- [ ] Add Docker support
- [ ] Implement notification system (email/push)
- [ ] Add social features (follow trainers/nutritionists)

### Long-term
- [ ] AI-powered workout recommendations
- [ ] Nutrition analysis with calorie tracking
- [ ] Integration with fitness wearables
- [ ] Video analytics (watch time, completion rate)
- [ ] Advanced reporting dashboard
- [ ] Multi-language support

---

## 📸 Screenshots

*Coming soon! Frontend development in progress.*

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 📞 Contact

**Ahmed Mohamed Sabry**

- GitHub: [@Ahmed-M-Sabry](https://github.com/Ahmed-M-Sabry)
- LinkedIn: [a7medsabrii](https://www.linkedin.com/in/a7medsabrii)
- Email: a7med.mohamed.sabri@gmail.com

---

## 🙏 Acknowledgments

- Clean Architecture by Robert C. Martin
- ASP.NET Core Documentation
- SignalR Documentation
- Entity Framework Core Team

---

<div align="center">

**⭐ Star this repository if you find it helpful!**

Made with ❤️ by [Ahmed M. Sabry](https://github.com/Ahmed-M-Sabry)

</div>
