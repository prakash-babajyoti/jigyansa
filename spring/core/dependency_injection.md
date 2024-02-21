**Dependency Injection (DI)** is a software development technique wherein objects do not create their dependencies internally. Instead, objects declare the dependencies they require, and it is the responsibility of an external object or framework to provide concrete dependencies to them.

***Types of Dependency Injection:***
1. **Constructor Injection**: Dependencies are provided through a class constructor. For example:
    ```java
    public class UserService {
        private final UserRepository userRepository;

        public UserService(UserRepository userRepository) {
            this.userRepository = userRepository;
        }

        // Other methods using userRepository...
    }
    ```

2. **Setter Injection**: Dependencies are set through setter methods. For example:
    ```java
    public class ProductService {
        private ProductRepository productRepository;

        public void setProductRepository(ProductRepository productRepository) {
            this.productRepository = productRepository;
        }

        // Other methods using productRepository...
    }
    ```

3. **Interface Injection**: Dependencies are injected through implementing an interface. For example:
    ```java
    public interface PaymentGateway {
        void processPayment(Order order);
    }

    public class PayPalGateway implements PaymentGateway {
        @Override
        public void processPayment(Order order) {
            // PayPal payment processing logic
        }
    }

    public class OrderService implements PaymentGateway {
        private final PaymentGateway paymentGateway;

        public OrderService(PaymentGateway paymentGateway) {
            this.paymentGateway = paymentGateway;
        }

        @Override
        public void processPayment(Order order) {
            paymentGateway.processPayment(order);
        }
    }
    ```

***Advantages of Using Dependency Injection:***
- Increased Code Reusability: Components can be easily reused across different parts of the application.
- Improved Code Readability: Clear separation of concerns leads to more understandable code.
- Enhanced Code Maintainability: Changes to dependencies are centralized, making maintenance easier.
- Enhanced Code Testability: Dependencies can be easily mocked or replaced during testing.
- Reduced Coupling: Loose coupling between components leads to a more flexible and adaptable codebase.
- Increased Cohesion: Each component is focused on a single task, enhancing the overall design coherence.
