### java-facker
---
https://github.com/DiUS/java-faker

```java
Faker faker = new Faker();
String name = faker.name().fullName();
String firstName = faker.name().firstName();
String lastName = faker.name().lastName();
String streetAddress = faker.address().streetAddress();

Faker faker = new Faker(new Loclae("YOUR_LOCALE"));
```

```java
// src/test/java/com/github/javafaker/service/FakeValuesServiceTest.java

public class FakeValuesServiceTest extends AbstractFakerTest {
  
  private static final Long MILLIS_IN_AN_HOUR = 1000 * 60 * 60L;
  private static final Long MILLIS_IN_A_DAY = MILLIS_IN_AN_HOUR * 24;
  
  @Mock
  private RandomService randomService;
  
  private FakeValueService fakeValuesService;
  
  @Before
  public void before() {
    super.before();
    MockitoAnnotations.initMocks(this);
    
    when(randomService.nextInt(anyInt())).thenReturn(0);
    
    fakeValuesService = spy(new FakeValuesService(new Locale("test"), randomService));
  }
  
  
  
  
  
  
  
  
  
}

```

```
```


