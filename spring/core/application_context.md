### ApplicationContext in Spring:

**Understanding ApplicationContext:**

In Spring, ApplicationContext serves as a pivotal component, acting as the backbone of the application. It functions as a repository for bean definitions and application components, facilitating the retrieval of assembled and configured beans.

**Key Functions of ApplicationContext:**

- **Initiating Beans:** ApplicationContext initializes beans defined within the application context, ensuring they are ready for use. For instance, consider the following Java configuration:

    ```java
    @Configuration
    public class AppConfig {
        @Bean
        public MyBean myBean() {
            return new MyBean();
        }
    }
    ```

- **Configuring Beans:** It configures beans according to the specifications provided, enabling flexible and tailored behavior. For example, utilizing annotations for configuration:

    ```java
    @Component
    public class MyComponent {
        @Autowired
        private Dependency dependency;
        // Other methods and fields
    }
    ```

- **Assembling Beans:** ApplicationContext brings together beans and their dependencies, orchestrating the application's architecture. Consider a scenario where beans are assembled through XML configuration:

    ```xml
    <beans>
        <bean id="dependency" class="com.example.Dependency"/>
        <bean id="myComponent" class="com.example.MyComponent"/>
    </beans>
    ```

- **Managing Beans Lifecycle:** From creation to destruction, ApplicationContext oversees the entire lifecycle of beans, ensuring proper management throughout. For instance, implementing lifecycle interfaces:

    ```java
    public class MyBean implements InitializingBean, DisposableBean {
        @Override
        public void afterPropertiesSet() {
            // Initialization logic
        }

        @Override
        public void destroy() {
            // Destruction logic
        }
    }
    ```

- **Serving as a Bean Factory:** Acting as a factory, it produces and provides beans as required, adhering to specified configurations. For instance, using factory methods:

    ```java
    @Configuration
    public class AppConfig {
        @Bean
        public MyBeanFactory myBeanFactory() {
            return new MyBeanFactory();
        }
    }
    ```

- **Acting as a Resource Loader:** ApplicationContext offers the capability to load resources from various sources, enhancing application flexibility. For example, loading properties from a file:

    ```java
    @PropertySource("classpath:application.properties")
    public class AppConfig {
        // Configuration methods
    }
    ```

- **Event Handling:** It possesses the ability to dispatch and receive application events, fostering inter-component communication and reactivity. For instance, defining an event listener:

    ```java
    @Component
    public class MyEventListener implements ApplicationListener<MyEvent> {
        @Override
        public void onApplicationEvent(MyEvent event) {
            // Event handling logic
        }
    }
    ```

- **Exposing Environment for Property Resolution:** ApplicationContext exposes an environment that allows resolving properties, contributing to application configuration and customization. For example, resolving properties in a configuration class:

    ```java
    @Value("${my.property}")
    private String myProperty;
    ```

**Common Types of ApplicationContext:**

- **AnnotationConfigApplicationContext:** Utilized for annotation-based configuration.

    ```java
    public static void main(String[] args) {
        AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext();
        context.register(AppConfig.class);
        context.refresh();
        // Access beans from the context
        MyComponent myComponent = context.getBean(MyComponent.class);
    }
    ```

- **AnnotationConfigWebApplicationContext:** Specifically designed for web applications utilizing annotation-based configuration.

    ```java
    public class MyWebAppInitializer implements WebApplicationInitializer {
        @Override
        public void onStartup(ServletContext servletContext) throws ServletException {
            AnnotationConfigWebApplicationContext context = new AnnotationConfigWebApplicationContext();
            context.register(WebConfig.class);
            context.setServletContext(servletContext);
            context.refresh();
        }
    }
    ```

- **ClassPathXmlApplicationContext:** Used for loading application context from XML configuration files located within the classpath.

    ```java
    ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
    ```

- **FileSystemXmlApplicationContext:** Similar to ClassPathXmlApplicationContext but loads XML configuration files from the filesystem.

    ```java
    ApplicationContext context = new FileSystemXmlApplicationContext("/path/to/applicationContext.xml");
    ```

- **XmlWebApplicationContext:** Tailored for web applications utilizing XML-based configuration.

    ```java
    public class MyWebAppInitializer implements WebApplicationInitializer {
        @Override
        public void onStartup(ServletContext servletContext) throws ServletException {
            XmlWebApplicationContext context = new XmlWebApplicationContext();
            context.setConfigLocation("/WEB-INF/applicationContext.xml");
            context.setServletContext(servletContext);
            context.refresh();
        }
    }
    ```

## Creating ApplicationContext Instances in Spring

There are several ways to create a new instance of an ApplicationContext, depending on the type of application and configuration method used.

### Non-Web Applications:

#### 1. AnnotationConfigApplicationContext:
   - Suitable for Java-based configuration using annotations.
   - **Example**:
     ```java
     AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
     ```

#### 2. ClassPathXmlApplicationContext:
   - Loads application context configuration from XML files in the classpath.
   - **Example**:
     ```java
     ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
     ```

#### 3. FileSystemXmlApplicationContext:
   - Loads application context configuration from XML files in the file system.
   - **Example**:
     ```java
     FileSystemXmlApplicationContext context = new FileSystemXmlApplicationContext("path/to/applicationContext.xml");
     ```

### Web Applications:

#### 1. Servlet 2 (web.xml):
   - Uses `ContextLoaderListener` or `DispatcherServlet` to initialize the Spring container.
   - **Example (ContextLoaderListener)**:
     ```xml
     <context-param>
         <param-name>contextConfigLocation</param-name>
         <param-value>/WEB-INF/applicationContext.xml</param-value>
     </context-param>
     <listener>
         <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
     </listener>
     ```

#### 2. Servlet 3 (XmlWebApplicationContext):
   - Uses `XmlWebApplicationContext` for XML-based configuration in Servlet 3.
   - **Example**:
     ```java
     XmlWebApplicationContext context = new XmlWebApplicationContext();
     context.setConfigLocation("/WEB-INF/applicationContext.xml");
     ```

#### 3. Servlet 3 (AnnotationConfigWebApplicationContext):
   - Uses `AnnotationConfigWebApplicationContext` for Java-based configuration in Servlet 3.
   - **Example**:
     ```java
     AnnotationConfigWebApplicationContext context = new AnnotationConfigWebApplicationContext();
     context.register(AppConfig.class);
     ```

### Spring Boot Applications:

#### 1. SpringBootConsoleApplication:
   - Utilizes `CommandLineRunner` for running tasks in a Spring Boot console application.
   - **Example**:
     ```java
     @SpringBootApplication
     public class SpringBootConsoleApplication implements CommandLineRunner {
         public static void main(String[] args) {
             SpringApplication.run(SpringBootConsoleApplication.class, args);
         }
         
         @Override
         public void run(String... args) throws Exception {
             // Spring Boot console application logic
         }
     }
     ```

#### 2. SpringBootWebApplication:
   - Embeds Tomcat server for running Spring Boot web applications.
   - **Example**:
     ```java
     @SpringBootApplication
     public class SpringBootWebApplication {
         public static void main(String[] args) {
             SpringApplication.run(SpringBootWebApplication.class, args);
         }
     }
     ```
