**Anti-Pattern Examples**

1. **Spaghetti Code**

   *Explanation*: Spaghetti code refers to complex methods with deeply nested conditional statements and intertwined logic, making code difficult to understand and maintain.

   *Example*:
   ```java
   public class SpaghettiCodeExample {
       public void processOrder(Order order) {
           if (order.getStatus().equals("pending")) {
               // Process pending order
               if (order.getPaymentMethod().equals("credit_card")) {
                   // Process credit card payment
               } else {
                   // Process other payment methods
               }
               // More nested logic...
           } else if (order.getStatus().equals("shipped")) {
               // Process shipped order
               if (order.getShippingMethod().equals("express")) {
                   // Process express shipping
               } else {
                   // Process standard shipping
               }
               // More nested logic...
           }
           // More nested logic...
       }
   }
   ```

2. **Magic Numbers and Strings**

   *Explanation*: Magic numbers and strings are hard-coded values without explanation or meaningful identifiers, reducing code readability and maintainability.

   *Example*:
   ```java
   public class MagicNumbersExample {
       public double calculateTotalPrice(double price, int quantity) {
           double taxRate = 0.08;
           double shippingCost = 5.0;
           double totalPrice = price * quantity;
           totalPrice += totalPrice * taxRate;
           totalPrice += shippingCost;
           return totalPrice;
       }
   }
   ```

3. **Copy-Paste Programming**

   *Explanation*: Copy-paste programming involves duplicating code blocks instead of abstracting common functionality into reusable components, leading to redundancy and potential inconsistency.

   *Example*:
   ```java
   public class CopyPasteProgrammingExample {
       public double calculateAreaOfSquare(double sideLength) {
           return sideLength * sideLength;
       }

       public double calculateAreaOfRectangle(double length, double width) {
           return length * width;
       }

       public double calculateAreaOfTriangle(double base, double height) {
           return (base * height) / 2;
       }
   }
   ```

4. **God Object**

   *Explanation*: The "God Object" anti-pattern occurs when a single class or module becomes overly complex and takes on too many responsibilities, leading to a tangled mess that is hard to understand and maintain.

   *Example*:
   ```java
   public class GodObjectExample {
       private List<Book> books;
       private List<Customer> customers;
       private List<Order> orders;

       // Methods for managing books, customers, orders, generating reports, etc.

       public void addBook(Book book) {
           // Add book to the list of books
       }

       public void placeOrder(Order order) {
           // Place an order
       }

       // More methods...
   }
   ```
   
5. **Primitive Obsession**

   *Explanation*: Primitive obsession occurs when primitive data types (such as integers, strings, or booleans) are excessively used instead of creating custom domain objects. This can lead to code duplication, reduced readability, and limited expressiveness.

   *Example*:
   ```java
   public class PrimitiveObsessionExample {
       public boolean validateUsername(String username) {
           // Check if username is between 6 and 20 characters
           return username.length() >= 6 && username.length() <= 20;
       }

       public double calculateTotalPrice(double price, int quantity) {
           // Calculate total price
           return price * quantity;
       }

       // More methods using primitive types directly...
   }
   ```

   In this example, primitive types (`String`, `double`, `int`) are used directly for representing concepts like usernames and prices. Instead, it would be better to create domain-specific classes (e.g., `Username`, `Price`) with appropriate validation and behavior, improving code clarity and maintainability.

6. **Lazy Class**

   *Explanation*: The lazy class anti-pattern occurs when a class does not have enough responsibility or functionality to justify its existence. This can result in unnecessary complexity and maintenance overhead.

   *Example*:
   ```java
   public class LazyClassExample {
       // This class has minimal functionality and does not justify its existence
   }
   ```

   In this example, the `LazyClassExample` class lacks meaningful functionality and serves little purpose in the codebase. It may have been created with good intentions but does not contribute significantly to the system's functionality. Identifying and refactoring lazy classes can help improve code clarity and maintainability by reducing unnecessary complexity and clutter in the codebase.
---

These examples illustrate common anti-patterns in Java code, emphasizing the importance of writing clean, maintainable code by avoiding these practices.
