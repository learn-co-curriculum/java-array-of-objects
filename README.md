# Arrays of Objects

## Learning Goals

- Initialize an array with object references
- Iterate over an array of objects

## Arrays of objects

An array can store primitive types (`int`, `boolean`, etc.) or it can
store reference types. For example, an array of `String` objects can be declared
and initialized as shown: 

```java
String[] names = {"Leslie", "Ann", "Ron", "Ben"};
```

Recall that an array is a reference type itself, and that a variable
declared with an array type such as `names` is a pointer
to the array object in the heap.

![string_array](https://curriculum-content.s3.amazonaws.com/6676/java-multipleclasses/stringarray.png)

Let's define a new class named `Product`.

```java
public class Product {
    private String name;
    private double price;
    private int quantity;

    public Product(String name, double price, int quantity) {
        this.name = name;
        this.price = price;
        this.quantity = quantity;
    }

    public String getName() {return name;}

    public double getPrice() {return price;}

    public int getQuantity() {return quantity;}

    public void setName(String name) {this.name = name;}

    public void setPrice(double price) {this.price = price;}

    public void setQuantity(int quantity) {this.quantity = quantity;}

    @Override
    public String toString() {
        return "name='" + name + '\'' +
                ", price=" + price +
                ", quantity=" + quantity;
    }
}
```

We can create an array and assign new `Product` instances
using indexing as shown:

```java
//Declare array and allocate space to store 3 Product references
Product[] products = new Product[3];

// Create 3 Product instances and store each reference in the array
products[0] = new Product("wireless keyboard", 199.99, 100);
products[1] = new Product("wireless mouse", 14.99, 150);
products[2] = new Product("webcam", 49.99, 20);
```

We can also declare and initialize the array in one step:

```java
Product[] products = new Product[] {
        new Product("wireless keyboard", 199.99, 100),
        new Product("wireless mouse", 14.99, 150),
        new Product("webcam", 49.99, 20)
 };
```

Both approaches result in the same object structure in the heap (the strings
are displayed as primitive values but are in fact separate objects):

![product_array](https://curriculum-content.s3.amazonaws.com/6676/java-multipleclasses/productarray.png)

## Driver Class

Let's look at an example driver class `ProductDriver`
for instantiating an array of `Product`
and iterating over the array to look for a product with a specific name.
We'll prompt the user to enter the product name, then use a separate
helper method `lookupProduct` to search the array.

```java
import java.util.Scanner;

public class ProductDriver {

    public static void main(String[] args) {
        Product[] products = new Product[] {
                new Product("wireless keyboard", 199.99, 100),
                new Product("wireless mouse", 14.99, 150),
                new Product("webcam", 49.99, 20)
        };

        Scanner scanner = new Scanner(System.in);

        // Ask user for product productName
        System.out.println("Enter product name:");
        String searchName = scanner.nextLine();

        // Lookup product in the array
        Product product = lookupProduct(products, searchName);

        // Display result of product lookup
        if (product == null) {
            System.out.printf("Product '%s' not found%n", searchName);
        }
        else {
            System.out.println(product);
        }
    }

    //helper method to search array for Product with matching name
    public static Product lookupProduct(Product[] products, String searchName) {
        // Loop through array
        for (Product product : products) {
            // Compare next array element's name with the parameter
            if (product.getName().equals(searchName)) {
                return product;
            }
        }
        // No product with matching name in the array, return null.
        return null;
    }
}
```

If we run the program and enter the name of an existing product,
we see the product information displayed:

```text
Enter product name:
wireless mouse
name='wireless mouse', price=14.99, quantity=150
```

Entering a non-existing product name results in an error message:

```text
Enter product name:
dual monitor stand
Product 'dual monitor stand' not found
```


## Conclusion

An array is an object that holds a fixed number of values of a single type,
which could be a primitive type or a reference type.
