# AndroidX ViewModel Internals

This project explores how **ViewModels** retain complex state across configuration changes and how they work under the hood by re-implementing a simplified version of `androidx.lifecycle.ViewModel`.

## Key Concepts Covered

### 1. **Custom ViewModel (MyViewModel)**
- **Abstract Base Class**: The custom `MyViewModel` class extends `ViewModel` to manage and retain UI-related data.
- **CoroutineScope**: A `CoroutineScope` is included, using `Dispatchers.Main` + `SupervisorJob` to perform asynchronous work safely.
- **onCleared() Method**: The `onCleared()` method is used to clean up resources when the `ViewModel` is no longer needed.

### 2. **ViewModel Store (MyViewModelStore)**
The `MyViewModelStore` class is a simplified version of the **ViewModel store**:
- Stores instances of `ViewModel` in a `HashMap<String, MyViewModel>`.
- Functions:
  - `put()`: Adds a ViewModel.
  - `get()`: Retrieves a ViewModel.
  - `clear()`: Clears all stored ViewModels.

### 3. **Factory Interface (MyViewModelFactory)**
- The **Factory Interface** is used to generate `ViewModel` instances.
- The default factory uses reflection to instantiate `ViewModel` objects without arguments.

### 4. **Provider (MyViewModelProvider)**
- The provider checks if a `ViewModel` already exists. If it does, it returns the existing instance. If not, it creates a new instance via the factory, stores it, and returns it.

### 5. **ViewModel Restoration in Activities**
- **lastCustomNonConfigurationInstance (deprecated)**: This method is used to survive configuration changes in Activities.
- **onDestroy()**: Clears the `ViewModel` store only if the Activity is finishing.

---

## Features

- **CounterViewModel**: This is a simple ViewModel that manages a counter state. It demonstrates state survival after a screen rotation and constructor-based factory usage.

---

## Key Libraries Used

- `androidx.lifecycle.ViewModel`: This is the core class for managing UI-related data.
- **Coroutines**: Used for asynchronous tasks in `ViewModels`.

---

## Getting Started

1. Clone the repository:
   ```bash
   git clone https://github.com/tashafdev/AndroidX-ViewModel-Internals.git
