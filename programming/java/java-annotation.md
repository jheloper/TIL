# 자바 어노테이션

**어노테이션(Annotation)**은 **메타데이터(metadata)**라고 할 수 있음.

메타데이터란 애플리케이션이 처리할 데이터가 아닌, 코드를 어떻게 컴파일하고 처리할 것인지 알려주는 정보.



## 어노테이션의 용도

- 컴파일러에게 코드 문법 에러를 체크하도록 정보를 제공
- 개발 툴이 빌드나 배치 시 코드를 자동으로 생성할 수 있도록 정보를 제공
- 런타임 시 특정 기능을 실행하도록 정보를 제공





## 어노테이션 타입 정의와 적용

어노테이션 타입을 정의하는 방법은 인터페이스를 정의하는 것과 유사함. `@interface`를 사용해서 어노테이션을 정의함.

```java
public @interface AnnotationName {}
```

위처럼 정의한 어노테이션은 코드에서 다음과 같이 사용함.

```java
@AnnotationName
```

어노테이션은 엘리먼트를 멤버로 가질 수 있음. 엘리먼트는 타입과 이름으로 구성되며, 디폴트 값을 가질 수 있음.

엘리먼트 타입으로는 기본 타입과 참조 타입 모두 사용할 수 있음.

디폴트 값이 없다면 반드시 값을 기술해야 하며, 디폴트 값이 있으면 생략 가능함.

어노테이션은 기본 엘리먼트인 value를 가짐.

```java
public @interface AnnotationName {
  	// 타입 elementName() [defalut 값];
  	int elementName() default 10;
  	String value(); // 기본 엘리먼트 value
}

@AnnotationName("값"); // 이렇게 값만 기술할 경우 기본 엘리먼트인 value 값으로 설정됨

@AnnotationName(value = "값", elementName = 5); // 기본 엘리먼트와 다른 엘리먼트의 값을 동시에 주고 싶다면 정상적으로 엘리먼트 이름을 지정해야 함.
```

### 어노테이션 적용 대상

어노테이션 적용 가능 대상은 `java.lang.annotation.ElementType` 열거 상수로 정의되어 있음.

어노테이션 적용 대상을 지정할 때에는 `@Target` 어노테이션을 사용함. `@Target`의 기본 엘리먼트는 어노테이션 적용 대상을 복수 개로 지정하기 위해서 ElementType 배열을 값으로 가짐.

```java
@Target({ElementType.TYPE, ElementType.FIELD, ...})
public @interface AnnotationName {}
```

### 어노테이션 유지 정책

어노테이션 정의 시 사용 용도에 따라 어느 범위까지 유지할 것인지 지정해야 함. 소스 상에만 유지할 것인지, 컴파일된 클래스까지 유지할 것인지, 런타임 시에도 유지할 것인지 지정해야 함. `@Retention` 어노테이션을 사용해서 어노테이션 유지 정책을 지정하며 기본 엘리먼트는 RetentionPolicy 타입이므로 3가지 상수 중 하나를 지정하면 됨.

어노테이션 유지 정책은 `java.lang.annotation.RetentionPolicy` 열거 상수로 정의되어 있음.

| RetentionPolicy 열거 상수 | 설명                                       |
| --------------------- | ---------------------------------------- |
| SOURCE                | 소스 상에서만 어노테이션 정보를 유지함. 소스 코드를 분석할 때만 의미가 있으며, 바이트 코드 파일에는 정보가 남지 않음. |
| CLASS                 | 바이트 코드 파일까지 어노테이션 정보를 유지함. 하지만 리플렉션을 이용해서 어노테이션 정보를 얻을 수는 없음. |
| RUNTIME               | 바이트 코드 파일까지 어노테이션 정보를 유지하면서 리플렉션을 이용해서 런타임 시에 어노테이션 정보를 얻을 수 있음. |

```java
@Target({ElementType.TYPE, ElementType.FIELD, ...})
@Retention(RetentionPolicy.RUNTIME) // 런타임 유지 정책을 지정함.
public @interface AnnotationName {}
```

### 런타임 시 어노테이션 정보 사용하기

어노테이션 자체는 아무런 동작을 가지지 않는 표식일 뿐이지만 리플렉션을 이용해서 어노테이션의 적용 여부와 엘리먼트 값을 읽고 적절히 처리할 수 있음. 클래스에 적용된 어노테이션 정보를 얻으려면 `java.lang.Class` 를 이용하면 되지만 필드, 생성자, 메서드에 적용된 어노테이션 정보를 얻으려면 Class의 `getFields()`, `getConstructors()`, `getDeclaredMethods()` 메서드를 통해서 `java.lang.reflect` 패키지의 Field, Constructor, Method 타입의 배열을 얻어야 함.

그 다음 Class, Field, Constructor, Method가 가지고 있는 메서드를 호출해서 적용된 어노테이션 정보를 얻을 수 있음.

| 리턴 타입        | 메서드명(매개변수)                               | 설명                                       |
| ------------ | ---------------------------------------- | ---------------------------------------- |
| boolean      | isAnnotationPresent(Class\<T extends Annotation\> annotationClass) | 지정한 어노테이션이 적용되었는지 여부. Class의 상위 클래스에 적용된 경우에도 true 리턴. |
| Annotation   | getAnnotation(Class\<T\> annotationClass) | 지정한 어노테이션이 적용되어 있으면 어노테이션 리턴, 그렇지 않으면 null 리턴. Class의 상위 클래스에 적용된 경우에도 어노테이션 리턴. |
| Annotation[] | getAnnotations()                         | 적용된 모든 어노테이션을 배열로 리턴. Class의 상위 클래스에 적용된 어노테이션도 전부 포함됨. |
| Annotation[] | getDeclaredAnnotations()                 | 직접 적용된 모든 어노테이션을 배열로 리턴. Class의 상위 클래스에 적용된 어노테이션은 포함하지 않음. |