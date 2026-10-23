# NutriNest 🥗📱

[![Kotlin](https://img.shields.io/badge/Kotlin-1.9.0-7F52FF.svg?logo=kotlin&logoColor=white)](https://kotlinlang.org/)
[![Android](https://img.shields.io/badge/Platform-Android-3DDC84.svg?logo=android&logoColor=white)](https://developer.android.com)
[![Compile SDK](https://img.shields.io/badge/Compile%20SDK-36-blue.svg)](https://developer.android.com)
[![Target SDK](https://img.shields.io/badge/Target%20SDK-34-brightgreen.svg)](https://developer.android.com)
[![Min SDK](https://img.shields.io/badge/Min%20SDK-24%20(Nougat)-orange.svg)](https://developer.android.com)
[![Architecture](https://img.shields.io/badge/Architecture-MVP-purple.svg)](#architecture)
[![UI](https://img.shields.io/badge/UI-Material%203%20%7C%20ViewBinding-blueviolet.svg)](#tech-stack)

> **NutriNest** is an intuitive Android mobile application designed to simplify healthy living through personalized nutrition tracking, automated meal planning, intelligent grocery list management, and customizable dietary restriction controls.

---

## 📖 Table of Contents

- [Overview](#-overview)
- [Key Features](#-key-features)
  - [1. Authentication & Onboarding Flow](#1-authentication--onboarding-flow)
  - [2. Dashboard & Daily Tracking](#2-dashboard--daily-tracking)
  - [3. Meal Planner & Generator](#3-meal-planner--generator)
  - [4. Smart Grocery List](#4-smart-grocery-list)
  - [5. Profile & Dietary Restrictions](#5-profile--dietary-restrictions)
  - [6. Application Settings](#6-application-settings)
- [Architecture](#-architecture)
- [Tech Stack & Libraries](#-tech-stack--libraries)
- [Project Directory Structure](#-project-directory-structure)
- [Quick Start & Demo Account](#-quick-start--demo-account)
- [Setup & Installation](#-setup--installation)
- [Future Enhancements](#-future-enhancements)
- [License](#-license)

---

## 🌟 Overview

Maintaining a balanced diet and managing meal prep can be overwhelming. **NutriNest** streamlines this entire journey into a cohesive mobile experience. Built with clean **Model-View-Presenter (MVP)** architecture in **Kotlin**, the app enables users to establish their personal health profiles, set calorie and macro targets, dynamically generate meal plans, check off grocery shopping items with responsive micro-interactions, and customize diet restrictions.

---

## 🚀 Key Features

### 1. Authentication & Onboarding Flow
- **Sign In (`LoginActivity`)**: Quick login with form validation and feedback.
- **3-Step Guided Registration**:
  - **Account Setup (`RegisterActivity`)**: Name, email, and password verification.
  - **Health Assessment (`HealthInfoActivity`)**: Capture age, weight, height, existing allergies, and dietary categories (Vegan, Vegetarian, Gluten-Free, Diabetic, etc.).
  - **Goal Selection (`GoalsActivity`)**: Choose lifestyle goals (Weight Loss, Maintenance, Muscle Gain) and activity levels to dynamically initialize the user profile.

### 2. Dashboard & Daily Tracking (`DashboardFragment`)
- **Daily Overview**: View greeting, daily target vs. consumed calories (`1,650 / 2,000 cal`).
- **Interactive Daily Meals**:
  - View scheduled meals for the day (Breakfast, Lunch, Dinner, Snacks).
  - **Tap to Toggle**: Mark meals as completed.
  - **Long-Press to Remove**: Remove a meal directly from the dashboard view with instant feedback.

### 3. Meal Planner & Generator (`MealPlanFragment`)
- **Automated Meal Plan Generation**: Instant one-tap generation of balanced daily meal suggestions with full nutritional breakdowns.
- **Macronutrient Calculations**: Live aggregation of total calories, protein, carbohydrates, and fats.
- **Interactive Calorie Goal Slider**: Real-time `SeekBar` synced with numerical input to fine-tune personal daily caloric targets.
- **Item Management**: Long-click to delete unwanted meal plans.

### 4. Smart Grocery List (`GroceryFragment`)
- **Real-Time Item Filtering**: Instant search as you type using `TextWatcher`.
- **Dynamic Item Creation**: Dialog prompt to add custom grocery items and quantities (e.g., *"Chicken Breast - 2 lbs"*).
- **Completion Micro-Animations**: Tapping an item triggers a smooth fade-out animation before clearing it from the list.
- **Long-Press Removal**: Quick deletion of grocery entries.

### 5. Profile & Dietary Restrictions (`ProfileFragment`)
- **Personal Information**: View and update full name and email address.
- **Dietary Restriction Management**: Check or uncheck standard restrictions (Vegan, Gluten-free, etc.) and add custom dietary rules (e.g., *"Low Carb"*).
- **Persistent Profile Changes**: Save modified profile data and restrictions directly to the repository.

### 6. Application Settings (`SettingsFragment`)
- **Notification Toggles**: Individual toggles for Meal Alerts, Hydration Reminders, Weekly Reports, and Marketing Notifications.
- **Data & Safety Options**: Data export prompt and account deletion safeguard.
- **Session Logout**: Securely resets the current user session and redirects back to the login screen.

---

## 🏗 Architecture

NutriNest adheres to the **Model-View-Presenter (MVP)** architectural pattern to ensure loose coupling, clear separation of concerns, and testability.

```
┌────────────────────────────────┐         ┌────────────────────────────────┐
│             VIEW               │         │           PRESENTER            │
│  (Activity / Fragment / XML)   │ ◄─────► │     (*Contract.Presenter)      │
│     - Renders UI elements      │  Calls  │  - Handles user interactions   │
│     - Dispatches user events   │ Updates │  - Executes business logic     │
│     - Implements *Contract.View│         │  - Formats data for presentation│
└────────────────────────────────┘         └───────────────┬────────────────┘
                                                           │
                                                           │ Queries / Mutates
                                                           ▼
                                           ┌────────────────────────────────┐
                                           │             MODEL              │
                                           │   (Data Classes & Repository)  │
                                           │  - User, MealPlan, GroceryItem │
                                           │  - UserRepository              │
                                           │  - MealRepository              │
                                           │  - GroceryRepository           │
                                           └────────────────────────────────┘
```

- **Contracts (`*Contract.kt`)**: Define interfaces for both the `View` and `Presenter`, establishing a strict contract of interactions.
- **Views**: Activities and Fragments handle only UI rendering and user inputs, delegating all logic to the presenter.
- **Presenters**: Manage state, compute macronutrient totals, filter lists, and communicate with repositories.
- **Repositories**: Centralized data management simulating persistent and in-memory state across screens.

---

## 🛠 Tech Stack & Libraries

| Component | Technology / Library | Description |
| :--- | :--- | :--- |
| **Language** | Kotlin 1.9.0 | Primary application programming language |
| **Minimum SDK** | API 24 (Android 7.0 Nougat) | Maximum compatibility across modern devices |
| **Target SDK** | API 34 (Android 14) / Compile SDK 36 | Optimized for modern Android platforms |
| **Build System** | Gradle 8.3.2 (Kotlin DSL `.kts`) | Modern build automation and dependency resolution |
| **UI Components** | Google Material Components 3 | Buttons, TextInputs, Cards, and Bottom Navigation |
| **View Binding** | Android ViewBinding | Type-safe and null-safe view references |
| **Navigation** | Android Support Fragments & BottomNavigationView | Single-hub multi-fragment navigation |
| **Testing** | JUnit 4 & Espresso | Unit and instrumented UI test frameworks |

---

## 📂 Project Directory Structure

```text
NutriNest/
├── app/
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com/example/nutrinest/
│   │   │   │   ├── app/
│   │   │   │   │   └── NutriNest.kt                # Application class & DI setup
│   │   │   │   ├── data/
│   │   │   │   │   ├── models/                    # Domain data entities
│   │   │   │   │   │   ├── GroceryItem.kt
│   │   │   │   │   │   ├── Meal.kt
│   │   │   │   │   │   ├── MealPlan.kt
│   │   │   │   │   │   ├── Restriction.kt
│   │   │   │   │   │   ├── SettingOption.kt
│   │   │   │   │   │   └── User.kt
│   │   │   │   │   └── repositories/              # State & data repositories
│   │   │   │   │       ├── GroceryRepository.kt
│   │   │   │   │       ├── MealRepository.kt
│   │   │   │   │       └── UserRepository.kt
│   │   │   │   └── screens/                       # MVP feature slices
│   │   │   │       ├── dashboard/                 # Dashboard feature & adapter
│   │   │   │       ├── grocery/                   # Grocery list & adapter
│   │   │   │       ├── login/                     # Authentication
│   │   │   │       ├── main/                      # MainActivity (Navigation hub)
│   │   │   │       ├── mealplan/                  # Meal planning & generator
│   │   │   │       ├── profile/                   # Profile & dietary preferences
│   │   │   │       ├── registration/              # Multi-step onboarding
│   │   │   │       │   ├── health/                # Health info input
│   │   │   │       │   └── goals/                 # Nutrition goal selection
│   │   │   │       └── settings/                  # App settings & preferences
│   │   │   ├── res/                               # Layouts, drawables, menus & themes
│   │   │   └── AndroidManifest.xml                # Manifest declaration
│   │   └── test/                                  # Unit tests
│   └── build.gradle.kts                           # Module-level Gradle configuration
├── gradle/
│   ├── wrapper/                                   # Gradle wrapper binaries
│   └── libs.versions.toml                         # Version catalog
├── build.gradle.kts                               # Project-level Gradle configuration
└── settings.gradle.kts                            # Settings Gradle
```

---

## 🔑 Quick Start & Demo Account

For rapid testing and evaluation without completing registration, use the pre-configured credentials:

| Field | Value |
| :--- | :--- |
| **Email** | `test@test.com` |
| **Password** | `password123` |

*Alternatively, click **"Sign Up"** to walk through the custom profile creation flow.*

---

## ⚙️ Setup & Installation

### Prerequisites
1. **Android Studio**: Iguana (2023.2.1) or newer recommended.
2. **JDK**: Java Development Kit 17 or higher.
3. **Android SDK**: Android API level 34 or higher installed via SDK Manager.

### Steps
1. **Clone the repository**:
   ```bash
   git clone https://github.com/your-username/NutriNest.git
   cd NutriNest
   ```
2. **Open the project in Android Studio**:
   - Open Android Studio, select **File > Open**, and browse to the cloned `NutriNest` directory.
3. **Sync Gradle**:
   - Let Android Studio download and sync project dependencies automatically (or click **Sync Project with Gradle Files**).
4. **Run the App**:
   - Select an Android Virtual Device (AVD with API 24+) or connect a physical Android device via USB debugging.
   - Click the **Run** button (`Shift + F10`) or use Gradle:
     ```bash
     ./gradlew assembleDebug
     ```

---

## 🔮 Future Enhancements

- [ ] **Room Database & Cloud Sync**: Transition from in-memory repositories to local Room persistence and Google Firebase Firestore cloud syncing.
- [ ] **Barcode Food Scanner**: Camera-based scanning of packaged foods via ML Kit to automatically pull calorie and macro info.
- [ ] **Push Reminders & WorkManager**: Scheduled meal and hydration notifications using Android `WorkManager`.
- [ ] **Dark Mode Theme Support**: Full system-wide day/night theme toggle in settings.
- [ ] **Export to PDF / CSV**: Download weekly meal plans and grocery lists to external storage or cloud drive.

---

## 📄 License

This project was developed as part of a **Mobile Application Development** course curriculum. Feel free to use, modify, and reference this code for learning and educational purposes.

