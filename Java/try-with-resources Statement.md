# try-with-resources Statement

To be used with classes that implement AutoClosable interface.

## AutoClosable and Closable interfaces

Closable interface extends from AutoClosable, which the relation may seem a bit reversed. Closable interface throws IOException whereas AutoClosable throws an Exception.

## try-with-resources

The try-with-resources will handle not just the exception that may be thrown while working with the resources, but also the ones that could be thrown while attempting to close them.

Instead of
```java
Reader reader;
try {
  reader = new BufferedReader(...);
  // do stuff
} finally {
  try {
    if (reader != null)
      reader.close()  
  } catch (IOException e) {
    // handle e
  }
}
```
use
```java
try (Reader reader = new BufferedReader(...)) {
  // do stuff
} catch (IOException e) {
  // handle e
}
```

### Multiple resources

Multiple resources can be used inside a single try-with-resources statement - simply separate the resource declarations by a semi-colon.
