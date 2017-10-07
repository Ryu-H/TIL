# Regular Expressions

## String에 쓸 수 있는 정규표현식 함수들

- replaceFirst() and replaceAll()
- split() - Array를 돌려줌 - "Apple, Apple" 을 **\\\b**로 쪼개면 왜 ", " 으로도 쪼개지는지 잘 모르겠?
- matches() - String에 match되는지 boolean 돌려줌

## Dedicated Regular Expression classes

정규표현식의 Compilation은 꽤 무거운 작업이 될 수 있다. 그러므로 String에 직접적으로 쓸 수 있는 정규표현식 함수들을 여러번 쓰게 되면 비효율적. 이럴땐 정규표현식을 위해서 만들어진 Class들을 사용하자

## Pattern class와 Matcher class
Pattern은 정규표현식을 Compile하고 Matcher의 팩토리 역할을 한다. Matcher는 정규표현식을 String에 매칭한다.

```java
Pattern pattern = Pattern.compile("\\w+");

Matcher matcher = pattern.matcher("apple, apple and orange please");

while (matcher.find()) {
  System.out.println(matcher.group());
}
```
```
apple
apple
and
orange
please
```
