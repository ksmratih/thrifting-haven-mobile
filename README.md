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