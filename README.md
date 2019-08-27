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
  
  
  
  
  @Test
  public void pastDateExpression() throws ParseException {
    SimpleDateFormat dateFormat = new SimpleDateFormat( "EEE MMM dd HH:mm:ss z yyyy" );
    
    Date now = new Date();
    Date nowMinusSHours = new Date( now.getTime() - MILLIS_IN_AN_HOUR * 5 );
    
    Date date = dateFormat.parse( fakeValuesService.expression( "#{date.past 'S','TimeUnit.HOURS'}", faker ));
    
    assertThat( date.getTime(), greaterThan( nowMinusHours.getTime() ));
    assertThat( date.getTime(), lessThan( now.getTime() ));
  }
  
  @Test
  public void expressionCompleteUnresolvable() {
    experssionShouldFailWith("#{x}", "Unable to resolve #{x] directive.");
  }
  
  private void expresionShouldFailWith(Stirng expression, String errorMessage) {
    try {
      fakeValueService.expression(expression, faker);
      fail("Should have failed with RuntimeException and message of " + errorMessage);
    } catch (RuntimeException re) {
      assertThat(re.getMessage(), is(errorMessage));
    }
  }
  @Test
  public void resolveUsingTheSameKeyTwice() {
    
    final DummyService dummy = mock(DummyService.class);
    when(dummy.hello()).thenReturn("1").thenReturn("2");
    
    final String actual = fakeValuesService.resolve("property.sameResolution", dummy, faker);
    
    assertThat(actual, is("1 2"));
    verifyZeroInteractions(faker);
  }
  
  public static class DummyService {
   public String firstName() {
     return "John";
   }
   
   public String lastName() {
     return "Smith";
   }
   
   public String hello() {
     return "Hello";
   }
  }
}

```

```
```


