## Spring Profiles

Spring Profiles provide a way to customize application behavior across different environments. By activating specific profiles, developers can configure beans, properties, and other components to adapt to different deployment scenarios such as development, testing, staging, or production. This note covers all aspects of Spring Profiles along with examples.

### 1. Definition and Usage:

Spring Profiles allow developers to segregate application configurations, making it easier to manage and maintain multiple deployment environments. Profiles can be activated based on various conditions, such as environment variables, system properties, or explicit configuration.

### 2. Declaring Profiles:

Profiles can be declared in several ways:

- **Using @Profile Annotation**: Apply the `@Profile` annotation to beans to specify which profiles they belong to.
  ```java
  @Component
  @Profile("dev")
  public class DevelopmentDataSource implements DataSource { ... }
  ```

- **Using application.properties or application.yml**: Define profiles in the `application.properties` or `application.yml` file.
  ```yaml
  spring.profiles.active=dev
  ```

### 3. Profile-Specific Configuration:

Profiles can have their own configuration settings, allowing for environment-specific customization.

- **Separate Configuration Files**: Use separate configuration files for each profile, such as `application-dev.properties` and `application-prod.properties`.

- **Profile-Specific Beans**: Define beans specific to a profile using `@Profile` annotation.
  ```java
  @Component
  @Profile("dev")
  public class DevelopmentDataSource implements DataSource { ... }
  ```

### 4. Activating Profiles:

Profiles can be activated using various mechanisms:

- **Using Command-Line Arguments**: Pass profile names as command-line arguments.
  ```
  java -jar myapp.jar --spring.profiles.active=dev
  ```

- **Using Environment Variables**: Set the `SPRING_PROFILES_ACTIVE` environment variable.
  ```bash
  export SPRING_PROFILES_ACTIVE=dev
  ```

- **Using application.properties or application.yml**: Set `spring.profiles.active` property in the configuration file.
  ```yaml
  spring.profiles.active=dev
  ```

### 5. Default Profiles:

Spring allows defining default profiles that get activated if no other profiles are specified.

- **application.properties or application.yml**: Set `spring.profiles.default` property.
  ```yaml
  spring.profiles.default=dev
  ```

### 6. Example:

Consider a Spring Boot application with two profiles: `dev` and `prod`. We can configure different database connections for each profile.

- **Development Configuration**:
  ```java
  @Component
  @Profile("dev")
  public class DevelopmentDataSource implements DataSource { ... }
  ```

- **Production Configuration**:
  ```java
  @Component
  @Profile("prod")
  public class ProductionDataSource implements DataSource { ... }
  ```

- **Activate Profiles**:
  ```
  java -jar myapp.jar --spring.profiles.active=prod
  ```

