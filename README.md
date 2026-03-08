# Task Manager App

A Flutter-based task management application built progressively over 3 weeks as part of a Flutter learning journey.

## 📱 Features

- Login screen with form validation
- Add, delete, and complete tasks
- Filter tasks by All, Pending, and Completed
- Data persistence using SharedPreferences
- Clean and responsive UI

---

## 🗓️ Week 1: Basic Flutter Development and UI Building

### What I Learned
- Flutter project structure and basic widgets
- Building responsive UI with Column, Row, and Container
- Navigation between screens using Navigator.push()
- Form validation for email and password fields

### What I Built
- A login screen with two TextFormFields for email and password
- Email format validation using RegEx
- Password length validation (minimum 6 characters)
- "Forgot Password?" button
- Navigation from login screen to home screen
- Separated code into multiple files:
  - `main.dart` - App entry point
  - `pages/login.dart` - Login screen
  - `pages/home.dart` - Home screen

### Key Concepts
```dart
// Form validation example
validator: (value) {
  if (value == null || value.isEmpty) {
    return 'Please enter your email';
  }
  if (!RegExp(r'^[\w-\.]+@([\w-]+\.)+[\w-]{2,4}$').hasMatch(value)) {
    return 'Please enter a valid email';
  }
  return null;
},

// Navigation example
Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => const HomeScreen()),
);
```

---

## 🗓️ Week 2: State Management and Persistent Storage

### What I Learned
- Using setState to manage widget state
- Saving and retrieving data with SharedPreferences
- Building a dynamic list with ListView.builder
- JSON encoding and decoding for complex data

### What I Built
- Task list displayed in a ListView
- Add tasks via a dialog box
- Delete tasks from the list
- Mark tasks as complete with strikethrough text
- Summary cards showing Total, Done, and Pending counts
- Tasks persist after app restart using SharedPreferences

### Key Concepts
```dart
// Saving tasks with SharedPreferences
Future<void> _saveTasks() async {
  final prefs = await SharedPreferences.getInstance();
  await prefs.setString('tasks', jsonEncode(_tasks));
}

// Loading tasks on app start
Future<void> _loadTasks() async {
  final prefs = await SharedPreferences.getInstance();
  final String? tasksJson = prefs.getString('tasks');
  if (tasksJson != null) {
    setState(() {
      _tasks = List<Map<String, dynamic>>.from(jsonDecode(tasksJson));
    });
  }
}
```

---

## 🗓️ Week 3: Finishing Touches and Final Project

### What I Learned
- UI enhancements using elevation, shadows, and border radius
- Using Icons library for visual appeal
- Filtering lists dynamically with setState
- Confirming destructive actions with AlertDialog

### What I Built
- Filter tabs (All, Pending, Completed)
- Enhanced app bar with action buttons
- Clear all completed tasks with confirmation dialog
- Improved card design with rounded corners and shadows
- Extended FloatingActionButton with label
- Empty state messages for each filter

### Key Concepts
```dart
// Filtering tasks
List<Map<String, dynamic>> _getFilteredTasks() {
  List<Map<String, dynamic>> filtered = [];
  for (int i = 0; i < _tasks.length; i++) {
    if (_filter == 'All' ||
        (_filter == 'Pending' && !_tasks[i]['isCompleted']) ||
        (_filter == 'Completed' && _tasks[i]['isCompleted'])) {
      filtered.add({..._tasks[i], 'index': i});
    }
  }
  return filtered;
}
```

---

## 🛠️ Setup Instructions

### Prerequisites
- Flutter SDK installed
- Android Studio or VS Code with Flutter extension
- Android device or emulator

### Steps to Run
1. Clone the repository:
```bash
   git clone https://github.com/bilalkamran-devs/task-manager-app.git
```
2. Navigate to project folder:
```bash
   cd task-manager-app
```
3. Install dependencies:
```bash
   flutter pub get
```
4. Run the app:
```bash
   flutter run
```

---

## 📦 Dependencies

| Package | Version | Purpose |
|--------|---------|---------|
| shared_preferences | ^2.2.2 | Local data persistence |

---

## 📁 Project Structure
```
lib/
├── main.dart          # App entry point and theme
└── pages/
    ├── login.dart     # Login screen with form validation
    └── home.dart      # Home screen with task management
```

## 📹 Demo Video
https://github.com/user-attachments/assets/89d40eac-4e8f-4dc6-937d-46854063ccfa
---

## 👨‍💻 Author

**Bilal Kamran**
GitHub: [@bilalkamran-devs](https://github.com/bilalkamran-devs)
