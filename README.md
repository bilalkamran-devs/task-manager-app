# Task Manager App

A Flutter-based task management application built progressively over 6 weeks as part of a Flutter Development Internship at DevelopersHub Corporation.

## 📱 Features

- Login and Signup with Firebase Authentication
- Add, delete, and complete tasks
- Filter tasks by All, Pending, and Completed
- Data persistence using SharedPreferences
- Fetch and display users from a REST API
- User profile screen with posts
- State management using Provider
- Smooth UI animations
- Cloud Firestore for user data storage

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

---

## 🗓️ Week 4: API Integration and Networking

### What I Learned
- Using the http package to make REST API calls
- Parsing JSON responses into Dart objects
- Handling network errors gracefully
- Showing loading indicators while fetching data

### What I Built
- API service class for all network requests
- Users list screen fetching data from JSONPlaceholder API
- User profile screen showing name, email, phone, company and posts
- Loading spinner while data is being fetched
- Error screen with retry button for failed requests
- Pull to refresh functionality

### Key Concepts
```dart
// Fetching data from API
static Future<List<dynamic>> fetchUsers() async {
  try {
    final response = await http
        .get(Uri.parse('$baseUrl/users'), headers: _headers)
        .timeout(const Duration(seconds: 10));
    if (response.statusCode == 200) {
      return jsonDecode(response.body);
    } else {
      throw Exception('Failed to load users: ${response.statusCode}');
    }
  } catch (e) {
    throw Exception('Network error: $e');
  }
}
```

---

## 🗓️ Week 5: Firebase Authentication and Database

### What I Learned
- Setting up Firebase in a Flutter project
- Implementing Email/Password Authentication
- Storing and retrieving data from Cloud Firestore
- Managing user sessions

### What I Built
- Firebase Authentication for login and signup
- Signup screen with name, email, and password
- User data stored in Cloud Firestore
- Profile dialog showing name and email from Firestore
- Logout functionality
- Auto navigation based on auth state

### Key Concepts
```dart
// Sign up and save to Firestore
static Future<UserCredential> signUp({
  required String name,
  required String email,
  required String password,
}) async {
  final UserCredential userCredential =
      await _auth.createUserWithEmailAndPassword(
    email: email,
    password: password,
  );
  await _firestore.collection('users').doc(userCredential.user!.uid).set({
    'name': name,
    'email': email,
    'createdAt': DateTime.now().toIso8601String(),
  });
  return userCredential;
}
```

---

## 🗓️ Week 6: State Management with Provider and Final Enhancements

### What I Learned
- Refactoring setState to Provider for cleaner state management
- Using ChangeNotifier and Consumer widgets
- Implementing explicit animations with AnimationController
- Performance optimization with proper widget separation

### What I Built
- TaskProvider class using ChangeNotifier
- Refactored HomeScreen to use Consumer<TaskProvider>
- Header slides down from top on app open
- FAB bounces in with elastic animation
- Task cards slide in from right one by one
- Smooth filter tab transitions with AnimatedContainer
- Task completion animates with AnimatedDefaultTextStyle

### Key Concepts
```dart
// Provider setup
class TaskProvider extends ChangeNotifier {
  List<Task> _tasks = [];

  void addTask(String title) {
    _tasks.add(Task(...));
    notifyListeners();
  }
}

// Consuming Provider in UI
Consumer<TaskProvider>(
  builder: (context, taskProvider, child) {
    return ListView.builder(
      itemCount: taskProvider.filteredTasks.length,
      ...
    );
  },
)
```

---

## 🛠️ Setup Instructions

### Prerequisites
- Flutter SDK installed
- Android Studio or VS Code with Flutter extension
- Android device or emulator
- Firebase account

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
4. Add your `google-services.json` file to `android/app/`
5. Run the app:
```bash
   flutter run
```

---

## 📦 Dependencies

| Package | Version | Purpose |
|--------|---------|---------|
| shared_preferences | ^2.2.2 | Local data persistence |
| http | ^1.2.0 | REST API calls |
| firebase_core | ^3.3.0 | Firebase initialization |
| firebase_auth | ^5.1.0 | User authentication |
| cloud_firestore | ^5.2.0 | Cloud database |
| provider | ^6.1.2 | State management |

---

## 📁 Project Structure
```
lib/
├── main.dart                  # App entry point and Provider setup
├── pages/
│   ├── login.dart             # Firebase login screen
│   ├── signup.dart            # Firebase signup screen
│   ├── home.dart              # Home screen with Provider
│   ├── users_list.dart        # API users list screen
│   └── user_profile.dart      # API user profile screen
├── providers/
│   └── task_provider.dart     # Provider state management
└── services/
    ├── api_service.dart       # REST API service
    └── auth_service.dart      # Firebase auth service
```

---

## 🎬 Video

https://github.com/user-attachments/assets/3d522d1a-f028-47bf-8d8a-c38a42008f94


## 👨‍💻 Author

**Bilal Kamran**
GitHub: [@bilalkamran-devs](https://github.com/bilalkamran-devs)
