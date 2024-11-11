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
            leading: const Icon(Icons.mood),
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