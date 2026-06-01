# FactScope 🔍

**FactScope** is a professional Android application developed in Kotlin and Jetpack Compose, designed to provide fast and reliable access to verified humanitarian data and official international reports.

## Project Vision
Our goal is to counter misinformation by bridging the gap between users and official institutional archives. Instead of relying on generic search engines, FactScope directly queries high-profile sources:
- **ReliefWeb (UN OCHA):** For humanitarian reports, global crises, and official UN updates.
- **World Bank:** For economic indicators and global development statistics.

---

## 🏗 Technical Architecture

The project follows **Clean Architecture** principles and a **Modular Repository Pattern** to ensure scalability, testability, and robustness.

### 1. Domain Layer - Modular Repositories
We use a common interface (`FactRepository`) to standardize data fetching across different sources. This allows us to add new institutional sources (WHO, World Bank, etc.) by simply plugging in new modules without affecting the core logic.

### 2. Parallel UseCase Execution
The search logic is handled by a specialized UseCase that launches queries across all registered repositories in **parallel** using Kotlin Coroutines (`async/await`). This ensures maximum performance even as the number of data sources grows.

### 3. Resilience & Error Handling
Each module is isolated. If one API source fails or returns an error (e.g., 403 Forbidden due to pending approval), the UseCase gracefully handles the exception, allowing the user to still view results from other functional sources.

### 4. Development & Production Strategy
To ensure a smooth development workflow while respecting API provider policies:
- **Development Mode:** Uses certified local mock data extracted from official reports to allow UI/UX refinement without straining API servers.
- **Production Mode:** Ready to switch to live API v2 endpoints upon `appname` approval.

---

## 🛠 Tech Stack
- **Language:** Kotlin 2.0 (Stable)
- **UI Framework:** Jetpack Compose (Material 3)
- **Networking:** Retrofit 2.11 + OkHttp 4.12
- **Serialization:** Kotlinx Serialization
- **Architecture:** MVVM + Clean Architecture UseCases

---

