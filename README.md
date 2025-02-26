# spring-study

## Testing Spring Boot Applications
- [Testing Spring Boot Applications](https://docs.spring.io/spring-boot/reference/testing/spring-boot-applications.html)

```@SpringBootTest``` will not start a server. You can use ```webEnvironment``` attribute of ```@SpringBootTest``` to further refine how your tests run:
  - MOCK(default)
  - RANDOM_PORT
  - DEFINE_PORT
  - NONE

### Detecting Test Configuration
- If you want to customize the primary configuration, you can use a nested ```@TestConfiguration``` class. Unlike a nested ```@Configuration``` class, which would be used instead of your application’s primary configuration, a nested ```@TestConfiguration``` class is used in addition to your application’s primary configuration.
- ```@SpringBootTest``` will not call your ```main``` method, and instead the class itself is used directly to create the ```ApplicationContext```