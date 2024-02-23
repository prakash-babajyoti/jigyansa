## Spring Bean Lifecycle Overview

```java
package org.example;

import org.springframework.beans.factory.DisposableBean;
import org.springframework.beans.factory.InitializingBean;

import javax.annotation.PostConstruct;
import javax.annotation.PreDestroy;

public class ExampleBean implements InitializingBean, DisposableBean {
    
    public ExampleBean() {
        System.out.println("Constructor called.");
    }

    @PostConstruct
    public void postConstruct() {
        System.out.println("@PostConstruct method called.");
    }

    @Override
    public void afterPropertiesSet() throws Exception {
        System.out.println("InitializingBean::afterPropertiesSet method called.");
    }

    public void init() {
        System.out.println("@Bean(initMethod) method called.");
    }

    public void display() {
        System.out.println("Bean is ready to use.");
    }

    @PreDestroy
    public void preDestroy() {
        System.out.println("@PreDestroy method called.");
    }

    @Override
    public void destroy() throws Exception {
        System.out.println("DisposableBean::destroy method called.");
    }

    public void customDestroy() {
        System.out.println("@Bean(destroyMethod) method called.");
    }
}
```

```java
package org.example;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;

@Configuration
@ComponentScan(basePackages = "org.example")
public class AppConfig {

    @Bean(initMethod = "init", destroyMethod = "customDestroy")
    public ExampleBean exampleBean() {
        return new ExampleBean();
    }
}
```

```java
package org.example;

import org.springframework.context.annotation.AnnotationConfigApplicationContext;

public class Main {
    public static void main(String[] args) {
        // Initialize Spring context
        try (AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class)) {
            // Get bean from context
            ExampleBean bean = context.getBean(ExampleBean.class);
            // Use bean
            bean.display();
        }
    }
}
```

In Spring Framework, the lifecycle of a bean consists of several stages, including instantiation, initialization, usage, and destruction. This note provides a detailed overview of the bean lifecycle using an example (`ExampleBean`) and Spring configuration (`AppConfig`).

### 1. Bean Instantiation:

- **Constructor**: The bean class `ExampleBean` is instantiated when the Spring container initializes.

### 2. Bean Initialization:

- **Post-Construct Method**: The `@PostConstruct` annotated method `postConstruct()` is called after the bean is constructed, but before it is returned to the caller. This method is used for post-initialization logic.

- **InitializingBean Interface**: The `afterPropertiesSet()` method from the `InitializingBean` interface is invoked after the properties of the bean have been set. This method allows for custom initialization logic.

- **Init Method**: The custom initialization method `init()` specified by the `initMethod` attribute in the `@Bean` annotation of `AppConfig` is called. This method can contain additional initialization logic specific to the bean.

### 3. Bean Usage:

- **Bean Ready for Use**: After initialization, the bean is ready to be used by other components in the application.

### 4. Bean Destruction:

- **Pre-Destroy Method**: The `@PreDestroy` annotated method `preDestroy()` is called before the bean is destroyed. This method is used for pre-destruction cleanup tasks.

- **DisposableBean Interface**: The `destroy()` method from the `DisposableBean` interface is invoked during bean destruction. This method allows for custom cleanup logic.

- **Custom Destroy Method**: The custom destroy method `customDestroy()` specified by the `destroyMethod` attribute in the `@Bean` annotation of `AppConfig` is called. This method can contain additional cleanup logic specific to the bean.

### Example Usage:

The `Main` class demonstrates the usage of the Spring bean by obtaining an instance of `ExampleBean` from the Spring container and invoking its `display()` method.


