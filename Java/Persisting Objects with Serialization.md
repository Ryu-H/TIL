# Persisting Objects with Serialization

클래스가 `Serializable` 인터페이스를 구현하게 함으로써 그 객체들이 Serializable하다는 것을 표기할 수 있다. 인터페이스 자체는 아무런 메써드 디피니션이 없음.

## ObjectOutputStream and ObjectInputStream

각각 Serialization과 Deserialization을 수행한다.

```java
SerializableThing st = new BankAccount();

try (ObjectOutputStream objectStream = new ObjectOutputStream(Files.newOutputSteam(Paths.get(filename)))) {
  objectStream.writeObject(st);
} catch (IOException e) {
  // ...
}
```
```java
SerializableThing st = null;

try (ObjectInputStream objectStream = new ObjectInputStream(Files.newInputStream(Paths.get(filename)))) {
  st = (SerializableThing) objectStream.readObject();
} catch (IOException e) {
  // ...
} catch (ClassNotFoundException e) {
  // If type cannot be found int the classpath
}
```

## Class Version Compatibility

When trying to deserialize an object, the runtime will throw `InvalidClassException` if the Serial Version UID for the serialized object is different than that of the current type that we are trying to deserilize to. The Serial Version UID is affected by contents of the class including interfaces it implements and its methods, changes that should not necessarily warrant such "version incompatibility".

We can add `serialVersionUID` to the type as a private static final long to manually manage the compatibility during serialization/deserialization.

You can use *serialver* utility to generate the Serial Version UID in the same way that the Java runtime would create - however some argue that this should be avoided and rather prefer starting from 1 and incrementing.

```java
private static final long serialVersionUID = 1L;
```

// TODO: Add info on writeObject and readObject for custom serialization/deserialization
