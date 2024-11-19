# :handbag::scarf: Thrifting Haven Mobile :boot::coat:

<details>
<Summary><b>Assignment 7</b></summary>


## [ASSIGNMENT 7](https://pbp-fasilkom-ui.github.io/ganjil-2025/en/assignments/individual/assignment-7)

## :memo: How to implement the checklist

### :ballot_box_with_check: Create a new Flutter application
+ Enter the following in the project directory to create a new flutter project in the terminal
```
flutter create thrifting_haven_mobile
cd thrifting_haven_mobile
```
+  Run the project in the terminal
```
flutter run
```
+ Make a new git repository and perform `git init` as well as
```
git add .
git commit -m "first commit"
git push -u origin main
```
+ Move class`MyHomePage` and `_MyHomePageState` from the `main.dart` to the `menu.dart` file

### :ballot_box_with_check: Create three simple buttons with icons and texts
+ Create a new class named `ItemHomepage` in the `menu.dart` file
```
 class ItemHomepage {
     final String name;
     final IconData icon;

     ItemHomepage(this.name, this.icon);
 }
 ```
+ Create a list of `ItemHomepage` containing the buttons for viewing the product list, adding a product and logout
```
 class MyHomePage extends StatelessWidget {  
     ...
     final List<ItemHomepage> items = [
         ItemHomepage("View Product List", Icons.list),
         ItemHomepage("Add Product", Icons.add),
         ItemHomepage("Logout", Icons.logout),
     ];
     ...
 }
```

### :ballot_box_with_check: Implement different colors for each button
In the `MyHomePage` class I add the following:
```

class MyHomePage extends StatelessWidget {
...
                    // Display ItemCard for each item in the items list.
                    children: items.asMap().entries.map((entry) {
                      int idx = entry.key;
                      ItemHomepage item = entry.value;
                      Color color;
                      switch (idx) {
                        case 0:
                          color = Colors.indigo.shade800;
                          break;
                        case 1:
                          color = Colors.indigo.shade400;
                          break;
                        case 2:
                          color = Colors.indigo.shade200;
                          break;
                        default:
                          color = Colors.indigo;
                      }
                      return ItemCard(item, color: color);
                    }).toList(),
...
}
```

### :ballot_box_with_check: Display a `Snackbar` with messages

+ After the buttons are added, create the `ItemCard` to display the button. The button pressed will display the following snackbar messages

 "You have pressed the View Product List button" when the View Product List button is pressed.
 "You have pressed the Add Product button" when the Add Product button is pressed.
 "You have pressed the Logout button" when the Logout button is pressed.

```
class ItemCard extends StatelessWidget {
  // Display the card with an icon and name.

  final ItemHomepage item;
  final Color color; 
  
  const ItemCard(this.item, {required this.color, super.key}); 

  @override
  Widget build(BuildContext context) {
    return Material(
      // Specify the background color of the application theme.
      color: color,
      // Round the card border.
      borderRadius: BorderRadius.circular(12),
      
      child: InkWell(
        // Action when the card is pressed.
        onTap: () {
          // Display the SnackBar message when the card is pressed.
          ScaffoldMessenger.of(context)
            ..hideCurrentSnackBar()
            ..showSnackBar(
              SnackBar(content: Text("You have pressed the ${item.name} button!"))
            );
        },
        // Container to store the Icon and Text
        child: Container(
          padding: const EdgeInsets.all(8),
          child: Center(
            child: Column(
              // Place the Icon and Text in the center of the card.
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                Icon(
                  item.icon,
                  color: Colors.white,
                  size: 30.0,
                ),
                const Padding(padding: EdgeInsets.all(3)),
                Text(
                  item.name,
                  textAlign: TextAlign.center,
                  style: const TextStyle(color: Colors.white),
                ),
              ],
            ),
          ),
        ),
      ),
    );
  } 
}
```

## :date: The difference between Stateless Widgets and Stateful Widgets

A stateless widget is an immutable widget whose properties remain unchanged after creation, making it ideal for static elements like text or icons that don’t need to respond to user interactions. A stateful widget is mutable and can rebuild itself to reflect changes in its state. The main difference is that stateless widgets are fixed, while stateful widgets can dynamically update in response to actions or events.

## :notebook_with_decorative_cover: Widgets used in this project and its uses
+ Scaffold: Provides page structure with an app bar and body.
+ AppBar: Displays the page title, "Thrifting Haven," with customizable color and text style.
+ Padding: Adds space around the body content for a cleaner layout.
+ Column & Row: Arranges widgets vertically (Column) and horizontally (Row).
+ InfoCard (custom widget): Uses Card to display user information with a shadowed box for emphasis.
+ SizedBox: Adds vertical spacing between elements.
+ GridView.count: Creates a grid layout with three columns for ItemCard widgets.
+ ItemCard (custom widget): Displays an icon and text for each menu option in a colored, tappable card.
+ Material & InkWell: Adds interactivity to ItemCard, showing a SnackBar message on tap.

## :film_projector: The use-case and variable that can be affected by `setState()`
`setState()` is used to update the UI of a stateful widget in response to changes. When `setState()` is called, it notifies Flutter that the widget's state has changed, prompting it to rebuild the UI with the new data. Variables affected by `setState()` are those in the widget's `State` class that directly impact the UI, such as text fields, toggle states, and visibility flags.

## :white_flag: The difference between `const` and `final` keyword
The `const` keyword is for compile-time constants, meaning the value must be known when the code is compiled. These values remain fixed throughout the app's lifecycle. The `final` keyword allows values to be assigned only once but at runtime, making it useful for variables that aren't known until the program runs. 


</details>


<details>
<Summary><b>Assignment 8</b></summary>

## [ASSIGNMENT 8](https://pbp-fasilkom-ui.github.io/ganjil-2025/en/assignments/individual/assignment-8)

## :memo: How to implement the checklist

### :ballot_box_with_check: Create a form page to add a new item

In the `lib` directory I made a `thriftentry_form.dart` file and added the following code
```
import 'package:flutter/material.dart';
import '../widgets/left_drawer.dart';

class ThriftEntryFormPage extends StatefulWidget {
  const ThriftEntryFormPage({super.key});

  @override
  State<ThriftEntryFormPage> createState() => _ThriftEntryFormPageState();
}

class _ThriftEntryFormPageState extends State<ThriftEntryFormPage> {
  final _formKey = GlobalKey<FormState>();
```

+ In the `thriftentry_form.dart` file include the data fields according to the model made in the previous project
```
class _ThriftEntryFormPageState extends State<ThriftEntryFormPage> {
  ...
  String _product = "";
  String _description = "";
  int _amount = 0;
  int _price = 0;
```
For every data field I added `Padding` as such based on its data type
```
                Padding(
                  padding: const EdgeInsets.all(8.0),
                  child: TextFormField(
                    decoration: InputDecoration(
                      hintText: "Product",
                      labelText: "Product",
                      border: OutlineInputBorder(
                        borderRadius: BorderRadius.circular(5.0),
                      ),
                    ),
                    onChanged: (String? value) {
                      setState(() {
                        _product = value!;
                      });
                    },
                    validator: (String? value) {
                      if (value == null || value.isEmpty) {
                        return "Product cannot be empty!";
                      }
                      return null;
                    },
                  ),
                ),
```

### :ballot_box_with_check: Redirect the user to the new item addition form when pressing the Add Item button on the main page

+ In the class `ItemCard` add the following line on the `OnTap` function to navigate to the `ThriftEntryFormPage` 
```
...
  if (item.name == "Add Product") {
    Navigator.push(
      context,
      MaterialPageRoute(
        builder: (context) => const ThriftEntryFormPage(),
      ),
    );
  }
...
```

+ To handle the navigation back to the Home Page we add a back button to the  `ThriftEntryFormPage` 
```
...
  leading: IconButton(
    icon: const Icon(Icons.arrow_back),
    onPressed: () {
      Navigator.of(context).pop();
    },
  ),
...
```

### :ballot_box_with_check: Display the data from the form in a pop-up after pressing the `Save` button on the new item addition form page

After pressing the `Save` button, it will display a pop-up message if the following code is implemented:
```
                Align(
                  alignment: Alignment.bottomCenter,
                  child: Padding(
                    padding: const EdgeInsets.all(8.0),
                    child: ElevatedButton(
                      style: ButtonStyle(
                        backgroundColor: MaterialStateProperty.all(
                            Theme.of(context).colorScheme.primary),
                      ),
                      onPressed: () {
                        if (_formKey.currentState!.validate()) {
                          showDialog(
                            context: context,
                            builder: (context) {
                              return AlertDialog(
                                title: const Text('Product successfully saved'),
                                content: SingleChildScrollView(
                                  child: Column(
                                    crossAxisAlignment: CrossAxisAlignment.start,
                                    children: [
                                      Text('Product: $_product'),
                                      Text('Description: $_description'),
                                      Text('Amount: $_amount'),
                                      Text('Price: $_price')
                                    ],
                                  ),
                                ),
                                actions: [
                                  TextButton(
                                    child: const Text('OK'),
                                    onPressed: () {
                                      Navigator.pop(context);
                                      _formKey.currentState!.reset();
                                    },
                                  ),
                                ],
                              );
                            },
                          );
                        }
                      },
                      child: const Text(
                        "Save",
                        style: TextStyle(color: Colors.white),
                      ),
                    ),
                  ),
                ),
```

### :card_file_box: Create a drawer in the application
Create a file named `left_drawer.dart` in the `lib` directory and add the following code:
```
import 'package:flutter/material.dart';
import 'package:thrifting_haven_mobile/screens/menu.dart';
import 'package:thrifting_haven_mobile/screens/thriftentry_form.dart';

class LeftDrawer extends StatelessWidget {
  const LeftDrawer({super.key});

  @override
  Widget build(BuildContext context) {
    return Drawer(
      child: ListView(
        children: [
          DrawerHeader(
            decoration: BoxDecoration(
              color: Theme.of(context).colorScheme.primary,
            ),
            child: const Column(
              children: [
                Text(
                  'Thrifting Haven',
                  textAlign: TextAlign.center,
                  style: TextStyle(
                    fontSize: 24,
                    fontWeight: FontWeight.bold,
                    color: Colors.white,
                  ),
                ),
                Padding(padding: EdgeInsets.all(8)),
                Text(
                  "Track your mental health every day here!",
                  textAlign: TextAlign.center,
                  style: TextStyle(
                    fontSize: 15,
                    color: Colors.white,
                  ),
                ),
              ],
            ),
          ),
          ListTile(
            leading: const Icon(Icons.home_outlined),
            title: const Text('Home Page'),
            // Redirection part to MyHomePage
            onTap: () {
              Navigator.pushReplacement(
                  context,
                  MaterialPageRoute(
                    builder: (context) => MyHomePage(),
                  ));
            },
          ),
          ListTile(
            leading: const Icon(Icons.inventory),
            title: const Text('Add Product'),
            // Redirection part to ThriftEntryFormPage
            onTap: () {
              Navigator.pushReplacement(
                context,
                MaterialPageRoute(builder: (context) => const ThriftEntryFormPage()),
              );
            },
          ),
        ],
      ),
    );
  }
}
```


## :card_index: The purpose and advantages of const in Flutter

`const` is used to mark widgets and variables as compile-time constants. `const` benefits performance since widgets marked as const are not rebuilt unnecessarily during widget rebuilds which optimizes memory and CPU usage.  The use of const is especially advantageous when dealing with static widgets, icons, or decorations that don't need to change, as it makes the application more efficient. Therefore, it shouldn't be used for variables that are expected to change.


## :bar_chart: Explain and compare the usage of Column and Row in Flutter

Column arranges widgets vertically, making it ideal for stacking items like form fields, while Row arranges widgets horizontally, suitable for side-by-side items like icons or buttons. 
+ Column Examples: the list of buttons in the home page. 
+ Row Examples: the widget that displays the name and class in the home page.


## :gear: Input Elements used on the form page 

Used Input Elements:

+ TextFormField: For capturing product name, description, amount, and price, with validation to ensure data correctness.
+ ElevatedButton: Used as a submit button to save product details.

Other Flutter Input Elements (not used in this form):

+ DropdownButtonFormField: For selecting from a predefined list of options.
+ Checkbox: For toggling options on or off.
+ Switch: Similar to a checkbox, used for binary (on/off) selections.
+ Slider: Allows users to choose a value within a specific range, useful for selecting quantities or levels.


## :framed_picture: How to set the theme within a Flutter application to ensure consistency

In the `main.dart` I set the theme by defining the `ThemeData` object passed into the `theme` parameter of all MaterialApp widgets
```
import 'package:flutter/material.dart';
import 'package:thrifting_haven_mobile/screens/menu.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Thrifting Haven',
      theme: ThemeData(
        colorScheme: ColorScheme.fromSwatch(
          primarySwatch: Colors.indigo,
        ).copyWith(secondary: Colors.indigo[400]),
      ),
      home: MyHomePage(),
    );
  }
}
```

## :link: How to manage navigation in a multi-page Flutter application

Navigation in a multi-page Flutter app is managed with the Navigator class, which provides functions to push and pop routes. Using `Navigator.push` to move to a new page, `Navigator.pop` to return to the previous page, and using `Navigator.pushNamed` to navigate between screens, which helps keep the code organized, especially in larger applications. 

</details>

<details>
<Summary><b>Assignment 9</b></summary>

## [ASSIGNMENT 9](https://pbp-fasilkom-ui.github.io/ganjil-2025/en/assignments/individual/assignment-9)

## :memo: How to implement the checklist

### :ballot_box_with_check: Implement the Django authentication system, registration feature, and login page in the Flutter project


After creating a django-app named `authentication` in the Django project, 
+ Create view methods for login, register and logout in `authentication/views.py`
```
from django.contrib.auth import authenticate, login as auth_login
from django.http import JsonResponse
from django.views.decorators.csrf import csrf_exempt
from django.contrib.auth.models import User
import json
from django.contrib.auth import logout as auth_logout

@csrf_exempt
def login(request):
    username = request.POST['username']
    password = request.POST['password']
    user = authenticate(username=username, password=password)
    if user is not None:
        if user.is_active:
            auth_login(request, user)
            # Successful login status.
            return JsonResponse({
                "username": user.username,
                "status": True,
                "message": "Login successful!"
                # Add other data if you want to send data to Flutter.
            }, status=200)
        else:
            return JsonResponse({
                "status": False,
                "message": "Login failed, account disabled."
            }, status=401)

    else:
        return JsonResponse({
            "status": False,
            "message": "Login failed, check email or password again."
        }, status=401)


@csrf_exempt
def register(request):
    if request.method == 'POST':
        data = json.loads(request.body)
        username = data['username']
        password1 = data['password1']
        password2 = data['password2']

        # Check if the passwords match
        if password1 != password2:
            return JsonResponse({
                "status": False,
                "message": "Passwords do not match."
            }, status=400)

        # Check if the username is already taken
        if User.objects.filter(username=username).exists():
            return JsonResponse({
                "status": False,
                "message": "Username already exists."
            }, status=400)

        # Create the new user
        user = User.objects.create_user(username=username, password=password1)
        user.save()

        return JsonResponse({
            "username": user.username,
            "status": 'success',
            "message": "User created successfully!"
        }, status=200)

    else:
        return JsonResponse({
            "status": False,
            "message": "Invalid request method."
        }, status=400)


@csrf_exempt
def logout(request):
    username = request.user.username

    try:
        auth_logout(request)
        return JsonResponse({
            "username": username,
            "status": True,
            "message": "Logged out successfully!"
        }, status=200)
    except:
        return JsonResponse({
        "status": False,
        "message": "Logout failed."
        }, status=401)
```
+ Add the URL routing functions in the `authentication/urls.py` 
```
from django.urls import path
from authentication.views import login, register, logout

app_name = 'authentication'

urlpatterns = [
    path('login/', login, name='login'),
    path('register/', register, name='register'),
    path('logout/', logout, name='logout'),
]
```
+ Create another URL routing inside `thrifting_haven/urls.py` by including `path('auth/', include('authentication.urls'))`

In order to integrate the authentication system in Fluttter we have to
+ Install the packages `flutter pub provider` and `flutter pub add pbp_django_auth`
+ Modify the root widget to create a new `Provider` object that will share an instance of `CookieRequest` with all components in the application
```
class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return Provider(
      create: (_) {
        CookieRequest request = CookieRequest();
        return request;
      },
      child: MaterialApp(
        title: 'Thrifting Haven',
        theme: ThemeData(
          useMaterial3: true,
          colorScheme: ColorScheme.fromSwatch(
            primarySwatch: Colors.deepPurple,
          ).copyWith(secondary: Colors.deepPurple[400]),
        ),
        home: MyHomePage(),
      ),
    );
  }
}
```
We can now make the login page
+ Create a new file named `login.dart` in the `screens` directory
+ Add the following code to `login.dart`
```
import 'package:thrifting_haven_mobile/screens/menu.dart';
import 'package:flutter/material.dart';
import 'package:pbp_django_auth/pbp_django_auth.dart';
import 'package:provider/provider.dart';
import 'package:thrifting_haven_mobile/screens/register.dart';

void main() {
  runApp(const LoginApp());
}

class LoginApp extends StatelessWidget {
  const LoginApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Login',
      theme: ThemeData(
        useMaterial3: true,
        colorScheme: ColorScheme.fromSwatch(
          primarySwatch: Colors.indigo,
        ).copyWith(secondary: Colors.indigo[400]),
      ),
      home: const LoginPage(),
    );
  }
}

class LoginPage extends StatefulWidget {
  const LoginPage({super.key});

  @override
  State<LoginPage> createState() => _LoginPageState();
}

class _LoginPageState extends State<LoginPage> {
  final TextEditingController _usernameController = TextEditingController();
  final TextEditingController _passwordController = TextEditingController();

  @override
  Widget build(BuildContext context) {
    final request = context.watch<CookieRequest>();

    return Scaffold(
      appBar: AppBar(
        title: const Text('Login'),
      ),
      body: Center(
        child: SingleChildScrollView(
          padding: const EdgeInsets.all(16.0),
          child: Card(
            elevation: 8,
            shape: RoundedRectangleBorder(
              borderRadius: BorderRadius.circular(12.0),
            ),
            child: Padding(
              padding: const EdgeInsets.all(20.0),
              child: Column(
                mainAxisSize: MainAxisSize.min,
                children: [
                  const Text(
                    'Login',
                    style: TextStyle(
                      fontSize: 24.0,
                      fontWeight: FontWeight.bold,
                    ),
                  ),
                  const SizedBox(height: 30.0),
                  TextField(
                    controller: _usernameController,
                    decoration: const InputDecoration(
                      labelText: 'Username',
                      hintText: 'Enter your username',
                      border: OutlineInputBorder(
                        borderRadius: BorderRadius.all(Radius.circular(12.0)),
                      ),
                      contentPadding:
                          EdgeInsets.symmetric(horizontal: 12.0, vertical: 8.0),
                    ),
                  ),
                  const SizedBox(height: 12.0),
                  TextField(
                    controller: _passwordController,
                    decoration: const InputDecoration(
                      labelText: 'Password',
                      hintText: 'Enter your password',
                      border: OutlineInputBorder(
                        borderRadius: BorderRadius.all(Radius.circular(12.0)),
                      ),
                      contentPadding:
                          EdgeInsets.symmetric(horizontal: 12.0, vertical: 8.0),
                    ),
                    obscureText: true,
                  ),
                  const SizedBox(height: 24.0),
                  ElevatedButton(
                    onPressed: () async {
                      String username = _usernameController.text;
                      String password = _passwordController.text;

		  // Check credentials
		  // TODO: Change the URL and don't forget to add a trailing slash (/) at the end of the URL!
		  // To connect the Android emulator to Django on localhost,
		  // use the URL http://10.0.2.2/
                      final response = await request
                          .login("http://localhost:8000/auth/login/", {
                        'username': username,
                        'password': password,
                      });

                      if (request.loggedIn) {
                        String message = response['message'];
                        String uname = response['username'];
                        if (context.mounted) {
                          Navigator.pushReplacement(
                            context,
                            MaterialPageRoute(
                                builder: (context) => MyHomePage()),
                          );
                          ScaffoldMessenger.of(context)
                            ..hideCurrentSnackBar()
                            ..showSnackBar(
                              SnackBar(
                                  content:
                                      Text("$message Welcome, $uname.")),
                            );
                        }
                      } else {
                        if (context.mounted) {
                          showDialog(
                            context: context,
                            builder: (context) => AlertDialog(
                              title: const Text('Login Failed'),
                              content: Text(response['message']),
                              actions: [
                                TextButton(
                                  child: const Text('OK'),
                                  onPressed: () {
                                    Navigator.pop(context);
                                  },
                                ),
                              ],
                            ),
                          );
                        }
                      }
                    },
                    style: ElevatedButton.styleFrom(
                      foregroundColor: Colors.white,
                      minimumSize: Size(double.infinity, 50),
                      backgroundColor: Theme.of(context).colorScheme.primary,
                      padding: const EdgeInsets.symmetric(vertical: 16.0),
                    ),
                    child: const Text('Login'),
                  ),
                  const SizedBox(height: 36.0),
                  GestureDetector(
                    onTap: () {
                      Navigator.push(
                        context,
                        MaterialPageRoute(
                            builder: (context) => const RegisterPage()),
                      );
                    },
                    child: Text(
                      'Don\'t have an account? Register',
                      style: TextStyle(
                        color: Theme.of(context).colorScheme.primary,
                        fontSize: 16.0,
                      ),
                    ),
                  ),
                ],
              ),
            ),
          ),
        ),
      ),
    );
  }
}
```
+ Change `home: MyHomePage()` to `home: LoginPage()` in the `main.dart`

Create a register function in the Flutter project
+ Add the `register.dart` into the `screens` folder and fill it with the following code
```
import 'dart:convert';
import 'package:flutter/material.dart';
import 'package:thrifting_haven_mobile/screens/login.dart';
import 'package:pbp_django_auth/pbp_django_auth.dart';
import 'package:provider/provider.dart';

class RegisterPage extends StatefulWidget {
  const RegisterPage({super.key});

  @override
  State<RegisterPage> createState() => _RegisterPageState();
}

class _RegisterPageState extends State<RegisterPage> {
  final _usernameController = TextEditingController();
  final _passwordController = TextEditingController();
  final _confirmPasswordController = TextEditingController();

  @override
  Widget build(BuildContext context) {
    final request = context.watch<CookieRequest>();
    return Scaffold(
      appBar: AppBar(
        title: const Text('Register'),
        leading: IconButton(
          icon: const Icon(Icons.arrow_back),
          onPressed: () {
            Navigator.pop(context);
          },
        ),
      ),
      body: Center(
        child: SingleChildScrollView(
          padding: const EdgeInsets.all(16.0),
          child: Card(
            elevation: 8,
            shape: RoundedRectangleBorder(
              borderRadius: BorderRadius.circular(12.0),
            ),
            child: Padding(
              padding: const EdgeInsets.all(20.0),
              child: Column(
                mainAxisSize: MainAxisSize.min,
                children: <Widget>[
                  const Text(
                    'Register',
                    style: TextStyle(
                      fontSize: 24.0,
                      fontWeight: FontWeight.bold,
                    ),
                  ),
                  const SizedBox(height: 30.0),
                  TextFormField(
                    controller: _usernameController,
                    decoration: const InputDecoration(
                      labelText: 'Username',
                      hintText: 'Enter your username',
                      border: OutlineInputBorder(
                        borderRadius: BorderRadius.all(Radius.circular(12.0)),
                      ),
                      contentPadding:
                          EdgeInsets.symmetric(horizontal: 12.0, vertical: 8.0),
                    ),
                    validator: (value) {
                      if (value == null || value.isEmpty) {
                        return 'Please enter your username';
                      }
                      return null;
                    },
                  ),
                  const SizedBox(height: 12.0),
                  TextFormField(
                    controller: _passwordController,
                    decoration: const InputDecoration(
                      labelText: 'Password',
                      hintText: 'Enter your password',
                      border: OutlineInputBorder(
                        borderRadius: BorderRadius.all(Radius.circular(12.0)),
                      ),
                      contentPadding:
                          EdgeInsets.symmetric(horizontal: 12.0, vertical: 8.0),
                    ),
                    obscureText: true,
                    validator: (value) {
                      if (value == null || value.isEmpty) {
                        return 'Please enter your password';
                      }
                      return null;
                    },
                  ),
                  const SizedBox(height: 12.0),
                  TextFormField(
                    controller: _confirmPasswordController,
                    decoration: const InputDecoration(
                      labelText: 'Confirm Password',
                      hintText: 'Confirm your password',
                      border: OutlineInputBorder(
                        borderRadius: BorderRadius.all(Radius.circular(12.0)),
                      ),
                      contentPadding:
                          EdgeInsets.symmetric(horizontal: 12.0, vertical: 8.0),
                    ),
                    obscureText: true,
                    validator: (value) {
                      if (value == null || value.isEmpty) {
                        return 'Please confirm your password';
                      }
                      return null;
                    },
                  ),
                  const SizedBox(height: 24.0),
                  ElevatedButton(
                    onPressed: () async {
                      String username = _usernameController.text;
                      String password1 = _passwordController.text;
                      String password2 = _confirmPasswordController.text;

                      // Check credentials
                      // TODO: Change the url, don't forget to add a slash (/) inthe end of the URL!
                      // To connect Android emulator with Django on localhost,
                      // use the URL http://10.0.2.2/
                      final response = await request.postJson(
                          "http://localhost:8000/auth/register/",
                          jsonEncode({
                            "username": username,
                            "password1": password1,
                            "password2": password2,
                          }));
                      if (context.mounted) {
                        if (response['status'] == 'success') {
                          ScaffoldMessenger.of(context).showSnackBar(
                            const SnackBar(
                              content: Text('Successfully registered!'),
                            ),
                          );
                          Navigator.pushReplacement(
                            context,
                            MaterialPageRoute(
                                builder: (context) => const LoginPage()),
                          );
                        } else {
                          ScaffoldMessenger.of(context).showSnackBar(
                            const SnackBar(
                              content: Text('Failed to register!'),
                            ),
                          );
                        }
                      }
                    },
                    style: ElevatedButton.styleFrom(
                      foregroundColor: Colors.white,
                      minimumSize: Size(double.infinity, 50),
                      backgroundColor: Theme.of(context).colorScheme.primary,
                      padding: const EdgeInsets.symmetric(vertical: 16.0),
                    ),
                    child: const Text('Register'),
                  ),
                ],
              ),
            ),
          ),
        ),
      ),
    );
  }
}
```


### :ballot_box_with_check: Create a custom model according to your Django application project

In the `models` subdirectory add the file `thrift_entry.dart` with the following code made from Quicktype
```
// To parse this JSON data, do
//
//     final product = productFromJson(jsonString);

import 'dart:convert';

List<Product> productFromJson(String str) => List<Product>.from(json.decode(str).map((x) => Product.fromJson(x)));

String productToJson(List<Product> data) => json.encode(List<dynamic>.from(data.map((x) => x.toJson())));

class Product {
    String model;
    String pk;
    Fields fields;

    Product({
        required this.model,
        required this.pk,
        required this.fields,
    });

    factory Product.fromJson(Map<String, dynamic> json) => Product(
        model: json["model"],
        pk: json["pk"],
        fields: Fields.fromJson(json["fields"]),
    );

    Map<String, dynamic> toJson() => {
        "model": model,
        "pk": pk,
        "fields": fields.toJson(),
    };
}

class Fields {
    int user;
    String name;
    int price;
    String description;
    String condition;

    Fields({
        required this.user,
        required this.name,
        required this.price,
        required this.description,
        required this.condition,
    });

    factory Fields.fromJson(Map<String, dynamic> json) => Fields(
        user: json["user"],
        name: json["name"],
        price: json["price"],
        description: json["description"],
        condition: json["condition"],
    );

    Map<String, dynamic> toJson() => {
        "user": user,
        "name": name,
        "price": price,
        "description": description,
        "condition": condition,
    };
}
```


### :ballot_box_with_check: Create a page containing a list of all items available at the JSON endpoint in Django that you have deployed

In the `screens` subdirectory add a file named `list_thriftentry.dart` 
+ Fill using the following code
```
import 'package:flutter/material.dart';
import 'package:pbp_django_auth/pbp_django_auth.dart';
import 'package:provider/provider.dart';
import 'package:thrifting_haven_mobile/models/thrift_entry.dart';
import 'package:thrifting_haven_mobile/widgets/left_drawer.dart';
import 'package:thrifting_haven_mobile/widgets/product_details.dart';

class ProductPage extends StatefulWidget {
  const ProductPage({super.key});

  @override
  State<ProductPage> createState() => _ProductPageState();
}

class _ProductPageState extends State<ProductPage> {
  Future<List<Product>> fetchProduct(CookieRequest request) async {
    // TODO: Don't forget to add the trailing slash (/) at the end of the URL!
    final response = await request.get('http://localhost:8000/json/');
    
    // Decoding the response into JSON
    var data = response;
    
    // Convert json data to a Product object
    List<Product> listProduct = [];
    for (var d in data) {
      if (d != null) {
        listProduct.add(Product.fromJson(d));
      }
    }
    return listProduct;
  }
  
  @override
  Widget build(BuildContext context) {
    final request = context.watch<CookieRequest>();
    return Scaffold(
      appBar: AppBar(
        title: const Text('Product List'),
        backgroundColor: Theme.of(context).colorScheme.primary,
        foregroundColor: Colors.white,
      ),
      drawer: const LeftDrawer(),
      body: FutureBuilder(
        future: fetchProduct(request),
        builder: (context, AsyncSnapshot snapshot) {
          if (snapshot.data == null) {
            return const Center(child: CircularProgressIndicator());
          } else {
            if (!snapshot.hasData) {
              return const Column(
                children: [
                  Text(
                    'There is no product data in Thrifting Haven',
                    style: TextStyle(fontSize: 20, color: Color(0xff59A5D8)),
                  ),
                  SizedBox(height: 8),
                ],
              );
            } else {
              return ListView.builder(
                itemCount: snapshot.data!.length,
                itemBuilder: (context, index) {
                  final product = snapshot.data![index];
                  return InkWell(
                    onTap: () {
                      Navigator.push(
                        context,
                        MaterialPageRoute(
                          builder: (context) => ProductDetailsPage(product: product),
                        ),
                      );
                    },
                    child: Card(
                      margin: const EdgeInsets.symmetric(horizontal: 16, vertical: 12),
                      child: Container(
                        decoration: BoxDecoration(
                          border: Border.all(
                            color: Colors.grey, // Color of the border
                            width: 1, // Width of the border
                          ),
                          borderRadius: BorderRadius.circular(12), // Border radius of the container
                        ),
                        padding: const EdgeInsets.all(20.0),
                        child: Column(
                          mainAxisAlignment: MainAxisAlignment.start,
                          crossAxisAlignment: CrossAxisAlignment.start,
                          children: [
                            Text(
                              "${snapshot.data![index].fields.name}",
                              style: const TextStyle(
                                fontSize: 18.0,
                                fontWeight: FontWeight.bold,
                              ),
                            ),
                            const SizedBox(height: 10),
                            Text("${snapshot.data![index].fields.description}"),
                            const SizedBox(height: 10),
                            Text("${snapshot.data![index].fields.price}"),
                            const SizedBox(height: 10),
                            Text("${snapshot.data![index].fields.condition}")
                          ],
                        ),
                      ),
                    ),
                  );
                },
              );
            }
          }
        },
      ),
    );
  }
}
```
+ Add the page to the `widgets/left.drawer` dart
```
ListTile(
    leading: const Icon(Icons.add_box),
    title: const Text('Product List'),
    onTap: () {
        // Route to the product page
        Navigator.push(
            context,
            MaterialPageRoute(builder: (context) => const ThriftEntryPage()),
        );
    },
),
```
+ Redirect the button in the `widgets/thrift_card.dart`
```
else if (item.name == "View Product") {
    Navigator.push(context,
        MaterialPageRoute(
            builder: (context) => const ProductEntryPage()
        ),
    );
}
```

### :ballot_box_with_check:  Create a detail page for each item listed on the Product list page and filter the item list page to display only items associated with the currently logged-in user

+ Create a new file named `product_detail.dart` under the `widgets` subdirectory and add the code
```
import 'package:flutter/material.dart'; 
import 'package:thrifting_haven_mobile/models/thrift_entry.dart'; 

class ProductDetailsPage extends StatelessWidget {
  final Product product;

  const ProductDetailsPage({super.key, required this.product});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(product.fields.name), 
        centerTitle: true,
        actions: <Widget>[
          IconButton(
            icon: const Icon(Icons.chevron_left),
            onPressed: () => Navigator.pop(context), 
          ),
        ], // Widget[]
      ), // AppBar
      body: SingleChildScrollView(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Text(
              product.fields.name,
              style: const TextStyle(fontSize: 24, fontWeight: FontWeight.bold),
            ), // Text
            const SizedBox(height: 10),
            Text("Description: ${product.fields.description}", style: const TextStyle(fontSize: 16)),
            const SizedBox(height: 10),
            Text("Price: ${product.fields.price}", style: const TextStyle(fontSize: 16)),
            const SizedBox(height: 10),
            Text("Description: ${product.fields.condition}", style: const TextStyle(fontSize: 16)),
          ],
        ),
      ),
    );
  }
}
```
+ To route towards the product details page after clicking on a product, in the `list_thriftentry.dart` file add the code
```
 onTap: () {
  Navigator.push(
    context,
    MaterialPageRoute(
      builder: (context) => ProductDetailsPage(product: product),
    ),
  );
},
```

## :mailbox_with_mail: Why we need to create a model to send or retrieve JSON Data

A model in Django defines the structure of data, ensuring consistency when sending or receiving JSON. It helps validate and store data correctly in the database. Without a model, errors like data mismatches can occur, as there's no defined structure to guide the process.

## :books: The function of the http library
The http library in Flutter is used to send network requests (like GET and POST) to the backend. It allows the app to communicate with the server, send data in the request body, and handle the server's response, such as JSON data.

## :cookie: The function of `CookieRequest`
CookieRequest manages HTTP requests with session handling, storing cookies like session cookies. It’s necessary to share it across the app to maintain a consistent session, allowing the app to recognize the user without requiring repeated logins.

## :incoming_envelope: The data transmission, from input to display in Flutter
In Flutter, user input is captured in form fields and stored in variables. When submitted, the data is sent to the backend via an HTTP request. The server processes it, and the response is used to update the UI, such as displaying confirmation or updating the view with new data.

## :gear: The authentication mechanism from login, register, to logout
In Flutter, the user enters credentials, which are sent to Django’s login endpoint. Django validates them, creates a session, and sends a response back. Flutter handles the response, showing the main menu if successful or an error if not. Upon logout, a request clears the session and redirects the user to the login screen.

</details>