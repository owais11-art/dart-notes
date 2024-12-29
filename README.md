# dart-notes

```dart
void main() {
  // variables
  var name = "Owais"; // infers the type of variable
  
  // Explicitly define the type
  String email = "owais21@gmail.com";
  int age = 18;
  double cgpa = 7.95;
  bool isGraduated = true;
  List<String>fruits = ["Mango", "Orange", "Apple"];
  Set<int> points = {5, 2, 6};
  Map<String, String> student = {
    "name": "Owais",
    "address": "SGR"
  };

  String Function(int) myFun = (int m) {
    return "$m";
}

  String? hobby = null; // nullabe variable
  
  final int data = 91; // run time constant
  const double pi = 3.14; // compile time constant
  
  // List methods & properties
  fruits.add("Pear"); // adds new element at the end
  fruits.removeLast(); // removes the last element
  fruits.remove("Apple"); // removes the first occurance of the element
  print(fruits.length); // print length of list
  print(fruits[0]); //access element at the given index
  fruits[1] = "Banana"; // change the value at given index

  // Functions
  var greeting = greet(name: "Aqib", age: 26);
  print(greeting);
  
  // loops
  
  for (String fruit in fruits) {
    print(fruit);
  }
  
  //conditions
  
  if(age > 18) {
    print("Can Vote");
  } else if(age == 18) {
    print("Can vote from this year!");
  } else {
    print("Cannot vote and you are young");
  }
  // Objects
  
  MenuItem noodles = MenuItem("veg noodles", 250);
  print(noodles.price);

  //Generics -> passing types to classes and functions to make them generic...

  Collection planets = Collection<String>(
      "My Planets",
      [
        "Mercury",
        "Venus",
        "Earth",
        "Mars",
        "Jupiter",
        "Saturn",
        "Uranus",
        "Neptune"
      ]
    );

  // Futures --> represents the result of asynchronous process

  fetchPost().then((post) {
      print(post.id);
      print(post.title);
    });

// Or using async await --> make sure the function have async keyword before using await like `void main() async {...}`

  var post = await fetchPost();
  print(post.id);
  print(post.title);
}

class MenuItem {
  String title;
  double price;
  
  MenuItem(this.title, this.price);
  String format() {
    return "$title --> $price";
  }

  @override
  String toString() {
    return format();
  }
}

// Inheritance

class Pizza extends MenuItem {
  List<String> toppings;
  
  // (super.title, super.price) or super(title, price) passes these values to constructor of super class
  
  Pizza(this.toppings, super.title, super.price);
  
  // OR
  
//   Pizza(this.toppings, String title, double price) : super(title, price);

 // method overriding
  @override
  String format() {
    return "overriden: ${super.format()}, $toppings";
  }
}

//Generics
class Collection<T> {
  String name;
  List<T> data;
  Collection(this.name, this.data);
  
  T randomItem() {
    data.shuffle();
    return data[0];
  }
}

// Futures

Future<Post> fetchPost() {
  const Duration delay = Duration(seconds: 3);
  return Future.delayed(delay, () {
    return Post(123, "What is Dart?");
  });
}

// Fetch from API. 
Future<Post> fetchNetworkPost() async {
  var uri = Uri.https('jsonplaceholder.typicode.com', '/posts/2');
  final response = await http.get(uri);
  print(response.body);
  Map<String, dynamic> data = convert.jsonDecode(response.body);
  return Post(data["id"], data["title"]);
}

class Post {
  int id;
  String title;
  
  Post(this.id, this.title);
}

String greet({required String name, required int age}) {
  return "My name is $name, and I am $age years old.";
}

```
