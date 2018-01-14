# Annotations

```java
@Target(Element.TYPE)
@Retention(RetentionPolicy.RUNTIME)
public @interface WorkHandler {
    boolean useThreadPool() default true;
}
```

- Specifying the default is optional
- Having just one element with its name as 'value' allow usage without specifying the element name

```java
@Target(Element.METHOD)
@Retention(RetentionPolicy.CLASS)
public @interface ThreadSafe {
    boolean value() default false;
}
```
