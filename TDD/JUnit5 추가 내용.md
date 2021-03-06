<h1>JUnit 5 추가 내용</h1>

<h2>조건에 따른 테스트</h2>

* JUnit 5는 조건에 따라 테스트를 실행할지 여부를 결정하는 기능을 제공하는데, 이 어노테이션들에 대해 살펴보자.
  * `@EnabledOnOs`, `@DisabledOnOs`
  * `@EnabledOnJre`, `@DisabledOnJre`
  * `@EnabledIfSystemProperty`, `@DisabledIfSystemProperty`
  * `@EnabledIfEnvironmentVariable`, `@DisabledIfEnvironmentVariable`

* 테스트 메소드가 특정 운영체제에서만 동작해야 한다면 `@EnabledOnOs` 어노테이션을 사용한다.   
  반대의 경우는 `@DisabledOnOs` 어노테이션을 사용한다. 아래는 예시이다.
```java
public class OsTmpPathTest{

    @Test
    @EnabledOnOs(OS.WINDOWS)
    void windowTmpPath() {
        Path tmpPath = Paths.get("C:\\temp");
        assertTrue(File.isDirectory(tmpPath));
    }

    @Test
    @EnabledOnOs(OS.LINUX)
    void linuxTmpPath() {
        Path tmpPath = Paths.get("/tmp");
        assertTrue(File.isDirectory(tmpPath));
    }
}
```

* `OS` 타입은 열거 타입으로 `WINDOWS`, `MAC`, `OS`와 같은 운영체제 이름을 값으로 정의하고 있다.   
  `@EnabledOnOs` 어노테이션과 `@DisabledOnOs` 어노테이션은 `OS` 열거 타입을 인자로 사용해서 테스트를 실행하거나   
  실행하지 않을 운영체제 조건을 지정한다.

* Java 버전에 따라 테스트를 실행하고 싶다면 `@EnabledOnJre` 어노테이션을 사용한다.   
  반대로는 `@DisabledOnJre` 어노테이션을 사용한다.
```java
@Test
@EnabledOnJre({JRE.JAVA_8, JRE.JAVA_9. JRE.JAVA_10, JRE.JAVA_11})
void testOnJre() {
    assertEquals(LocalDate.of(1919, 3, 1), LocalDate.of(2019, 3, 1).minusYears(100));
}
```

* `JRE` 열거 타입은 Java의 버전을 정의하고 있다. JUnit 5.4.0 기준으로 `JRE` 열거 타입은 `JAVA_8`부터 `JAVA_13`까지의 값을   
  정의하고 있으며 추자로 `OTHER` 값을 정의할 수 있다. Java 7이나 Java 6을 사용할 때 `JRE.OTHER`를 사용할 수 있지만,   
  Java 8부터 JUnit 5 를 사용할 수 있기 때문에 실질적으로 `JRE.OTHER`를 사용할 일은 없다.

* `@EnabledIfSystemProperty` 어노테이션과 `@DisabledIfSystemProperty` 어노테이션은 시스템 프로퍼티 값을 비교하여   
  테스트 실행 여부를 결정한다. 아래 코드는 예시인데, `java.vm.name` 시스템 프로퍼티 값이 OpenJDK를 포함하고 있으면   
  해당 테스트를 실행한다.
```java
@Test
@EnabledIfSystemProperty(named = "java.vm.name", matches = ".*OpenJDK.*")
void openJdk() {
    assertEquals(2, 1 + 1);
}
```

* `@EnabledIfSystemProperty` 어노테이션의 named 속성은 시스템 프로퍼티의 이름을 지정하고,   
  matches 속성에는 값의 일치 여부를 검사할 때 사용할 정규 표현식을 지정한다.

* `@EnabledIfEnvironmentVariable`도 named 속성과 matches 속성을 사용한다.   
  차이점은 named 속성에 환경 변수 이름을 사용한다는 것이다.
<hr/>

<h2>태깅과 필터링</h2>

* `@Tag` 어노테이션은 테스트에 태그를 달 때 사용한다. `@Tag` 어노테이션은 클래스와 테스트 메소드에 적용할 수 있다.
```java
import org.junit.jupiter.api.Tag;

@Tag("integration")
public class TagTest {

    @Tag("very-slow")
    @Test
    void verySlow() {
        int result = someVerySlowOperation();
        assertEquals(result, 0);
    }
}
```

* 위 코드는 `verySlow()` 테스트 메소드에 이름이 "very-slow"인 태그를 붙였다.   
  여러 태그를 붙이고 싶다면 각 이름마다 `@Tag` 어노테이션을 사용하면 된다.

* 태그의 이름은 아래 규칙을 따라야 한다.
  * null이거나 공백이면 안된다.
  * 좌우 공백을 제거한 뒤에 공백을 포함하면 안된다.
  * ISO 제어 문자를 포함하면 안된다.
  * 다음 글자를 포기하면 안된다. --> `,` , `()`, `&`, `|`, `!`

* `@Tag` 어노테이션을 이용하면 maven이나 gradle에서 실행할 테스트를 선택할 수 있다.   
  다음은 태그명을 사용해서 실행할 테스트를 선택하는 maven 설정 예시이다.
```xml
<plugin>
    <artifactId>maven-surefire-plugin</artifactId>
    <version>2.22.1</version>
    <configuration>
        <groups>integration</groups>
        <excludedGroups>slow | very-slow</excludedGroups>
    </configuration>
</plugin>
```

* `<groups>` 요소는 실행에 포함할 태그를 지정하고, `<excludedGroups>` 태그는 실행에서 제외할 태그를 지정한다.   
  위 코드는 integration 태그를 테스트 대상에 포함하고, slow 태그나 very-slow 태그는 테스트 대상에서 제외한다.   
  제외 대상이 우선한다.

* 아래는 위 코드와 동일한 태그를 테스트 대상으로 선택하는 gradle 예시이다.
```gradle
test {
    useJUnitPlatform {
        includeTags 'integration'
        excludeTags 'slow | very-slow'
    }
}
```

* 테스트 포함 대상이나 제외 대상을 지정할 때 태그식을 사용하는데, 태그 식에서는 다음 연산을 이용해서 식을 조합할 수 있다.
  * `!` : NOT 연산
  * `&` : AND 연산
  * `|` : OR 연산
* 이 연산을 사용하면 다양한 태그 조합을 사용해서 테스트 대상을 구분할 수 있다.
<hr/>

<h2>중첩 구성</h2>

* `@Nested` 어노테이션을 사용하면 중첩 클래스에 테스트 메소드를 추가할 수 있다.   
  아래는 `@Nested`를 사용한 코드의 전형적인 구조이다.
```java
import org.junit.jupiter.api.Nested;

public class Outer {

    @BeforeEach void outerBefore() {}

    @Test void outer() {}

    @AfterEach void outerAfter() {}

    @Nested
    class NestedA {

        @BeforeEach void nestedBefore() {}

        @Test void nested1() {}

        @AfterEach void nestedAfter() {}
    }
}
```

* 위 코드를 기준으로 중첩 클래스의 테스트 메소드인 `nested1()`을 실행하는 순서는 다음과 같다.
  1. `Outer` 객체 생성
  2. `NestedA` 객체 생성
  3. `outerBefore()` 수행
  4. `nestedBefore()` 수행
  5. `nested1()` 수행
  6. `nestedAfter()` 수행
  7. `outerAfter()` 수행

* 중첩된 클래스는 내부 클래스이므로 외부 클래스의 멤버에 접근할 수 있다.   
  이 특징을 활용하면 상황별로 중첩 테스트 클래스를 분리해서 테스트 코드를 구성할 수 있다.
```java
public class UserServiceTest {

    private MemoryUserRepository repository;
    private UserService service;

    @BeforeEach
    void setUp() {
        repository = new MemoryUserRepository();
        service = new UserService(repository);
    }

    @Nested
    class GivenUser {

        @BeforeEach
        void givenUser() {
            repository.save(new User("id", "pw", "email"));
        }

        @Test
        void dupId() {
            //..
        }

        @Nested
        class GivenNoDupId {
            //..
        }
    }
}
```
<hr/>

<h2>테스트 메시지</h2>

* 아래 코드를 보자.
```java
List<Integer> ret = getResults();
List<Integer> expected = Arrays.asList(1, 2, 3);
for(int i = 0; i < expected.size(); i++) {
    assertEquals(expected.get(i), ret.get(i));
}
```

* 위 테스트 코드는 for 구문을 이용해서 `List`에 대한 검증을 수행하고 있다.   
  루프를 도는 과정에서 값 검증에 실패하면 아래와 같이 메시지가 출력된다.
```
org.opentest4j.AssertionFailedError:
Expected :2
Actual :6
```

* 위 에러 메시지만으로는 `List`의 몇 번째 요소를 검증하다가 실패했는지 알 수 없다.   
  expected에서 기대값이 2인 요소가 몇 번째인지 코드를 뒤져야 한다. 또한 만약 2인 요소가 두 개 이상이면   
  찾기는 더욱 힘들어진다.

* 설명 문자열을 사용하면 이런 문제를 쉽게 해결할 수 있다. 아래는 위의 코드에 설명 문자열을 추가한 것이다.
```java
List<Integer> ret = getResults();
List<Integer> expected = Arrays.asList(1, 2, 3);
for(int i = 0; i < expected.size(); i++) {
    assertEquals(expected.get(i), ret.get(i)), "ret[" + i + "]");
}
```

* 이제 오류가 발생하면 메시지가 아래와 같이 출력된다.
```
org.opentest4j.AssertionFailedError: ret[1] ==>
Expected :2
Actual :6
```

* 실패 문구를 보면 ret의 1번 인덱스 값을 검증하다 실패했다는 것을 쉽게 알 수 있다.   
  이렇게 한 테스트 메소드에 구분이 쉽지 않은 단언을 여러 번 하는 경우, 메시지를 사용해서 각 단언을 쉽게 구분할 수 있다.
<hr/>

<h2>@TempDir 어노테이션을 이용한 임시 폴더 생성</h2>

* 파일과 관련된 테스트 코드를 만들다 보면 임시로 사용할 폴더가 필요할 때가 있다.   
  테스트를 시작하기 전에 임시 폴더를 만들고, 테스트가 끝나면 삭제하는 코드를 직접 작성할 수도 있지만, 꽤나 번거로운 작업이다.

* JUnit 5.4에 추가된 `@TempDir` 어노테이션을 사용하면 임시 폴더 관련 작업을 테스트 코드에서 쉽게 처리할 수 있다.   
  `@TempDir`을 필드 또는 생명주기 관련 메소드나 테스트 메소드의 파라미터로 사용하면, JUnit은 임시 폴더를 생성하고,   
  `@TempDir` 어노테이션을 붙인 필드나 파라미터에 임시 폴더 경로를 전달한다.

* `@TempDir` 어노테이션은 `File` 타입이나 `Path` 타입에 적용할 수 있다.
```java
public class TempDirTest {

    @TempDir
    File tempFolder;

    @Test
    void fileTest() {
        // tempFolder에 파일 생성 등의 작업
    }
}
```

* 위 코드는 `File` 타입의 tempFolder 필드에 `@TempDir` 어노테이션을 적용했다.   
  이 경우 테스트 메소드를 실행하기 전에 임시 폴더를 생성하고, 그 폴더 정보를 tempFolder 필드에 할당한다.

* 필드에 적용하면 각 테스트 메소드를 실행할 때마다 임시 폴더를 생성한다. 만약 특정 메소드에서만 임시 폴더를 생성해서   
  사용하고 싶다면 테스트 메소드의 파라미터에 `@TempDir`를 적용하면 된다.
```java
@Test
void fileTest(@TempDir Path tempFolder) {
    //..
}
```

* 테스트를 실행한 뒤에는 생성된 임시 폴더가 삭제된다. 물론 이 과정에서 임시 폴더 내에 작성한 파일도 함께 삭제된다.

* 특정 테스트 클래스 단위로 임시 폴더를 생성하고 싶다면 정적 필드에 `@TempDir` 어노테이션을 붙인다. 정적 필드에 `@TempDir`을   
  적용하면 각 테스트 메소드마다 임시 폴더를 생성하지 않는다. 대신 테스트 클래스의 모든 테스트 메소드를 실행하기 전에 임시 폴더를   
  한번 생성하고 모든 테스트 메소드의 실행이 끝난 뒤에 임시 폴더를 삭제한다.
```java
public class TempDirTest {

    @TempDir
    static File tempFolderPerClass;

    //..
}
```

* 정적 필드 대신에 `@BeforeAll` 메소드의 파라미터에 `@TempDir`를 적용해도 된다.
```java
public class TempDirTest {

    @BeforeAll
    static void setUp(@TempDir File tempFolder) {
        //..
    }

    //..
}
```

<hr/>

<h2>@Timeout 어노테이션을 이용한 테스트 실행 시간 검증</h2>

* `@Timeout` 어노테이션은 JUnit 5.5 버전부터 지원하는 어노테이션으로, `@Timeout` 어노테이션을 사용하면 테스트가 일정 시간 내에   
  실행되는지 검증할 수 있다. 아래는 `@Timeout` 어노테이션을 이용해서 테스트 메소드가 1초 내에 실행되는지를 검증하는 예시이다.
```java
public class TimeoutTest{ 

    @Test
    @Timeout(1)
    void sleep2Seconds() throws InterruptedException {
        Thread.sleep(2000);
    }
}
```

* 테스트 메소드 내에서 2초 동안 실행을 멈추므로 이 테스트의 실행 시간은 1초를 초과해서 실패하게 된다.   
  테스트 실패 메시지는 다음과 같다.
```
java.util.concurrent.TimeoutException : sleep2Seconds() timed out after 1 second.
```

* 초가 아닌 다른 시간 단위를 사용하고 싶다면 unit 속성에 `TimeUnit` 값을 지정하면 된다.   
  아래는 밀리초 단위로 설정하는 예시이다.
```java
@Test
@Timeout(value = 500, unit = TimeUnit.MILLISECONDS)
void sleep40mills() throws InterruptedException {
    Thread.sleep(40);
}
```
<hr/>