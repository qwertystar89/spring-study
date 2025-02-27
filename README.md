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

### Testing With a Mock Environment
- Spring Boot 2.x -> ```MockMvc```
- Spring Boot 3.2 -> ```MockMvcTester```

```java
@SpringBootTest
@AutoConfigureMockMvc
class MyMockMvcTests {

	@Test
	void testWithMockMvc(@Autowired MockMvc mvc) throws Exception {
		mvc.perform(get("/")).andExpect(status().isOk()).andExpect(content().string("Hello World"));
	}

	// If AssertJ is on the classpath, you can use MockMvcTester
	@Test
	void testWithMockMvcTester(@Autowired MockMvcTester mvc) {
		assertThat(mvc.get().uri("/")).hasStatusOk().hasBodyTextEqualTo("Hello World");
	}

	// If Spring WebFlux is on the classpath, you can drive MVC tests with a WebTestClient
	@Test
	void testWithWebTestClient(@Autowired WebTestClient webClient) {
		webClient
				.get().uri("/")
				.exchange()
				.expectStatus().isOk()
				.expectBody(String.class).isEqualTo("Hello World");
	}

}
```