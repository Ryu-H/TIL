# Streams.md

Streams are uni-directional flow of data. On the abstract level, there are 2 types of stream:
1. Stream that work on byte level (InputStream and OutputStream)
2. Stream that work on char level (Reader and Writer)

## Complication in closing the Stream properly
Streams often work with resources that reside outside the JVM where the memory management is automatically handled, thus require some manual 'closing' once you are done working with the class.  The firsthand approach to this would be to enclose the code working with the stream class with a **try** block and call the close() method inside the **finally** block. There are several complexities that could be overlooked however.
- If an error occurs before the stream object is initialised, the reference to the stream may be null and the close() method call may result in a NullPointerException. This means you'd need to do a null check first before you call close().
- Since the close() call is happening outside the **try** block, any exception that occurs while attempting to close the stream will not be handled, which means you need to enclose the code to close the stream to be also inside its own try-catch block.

Inevitably, the code becomes quite bloated and unclean just to achieve something that *should* be fairly straight forward.

Refer to [try-with-resources Statement](./try-with-resources%20Statement.md) for a cleaner way of working with classes that implement AutoClosable interface.

## Deprecated classes in java.io package
Following classes have apparently been Deprecated:
- FileInputStream
- FileOutputStream
- FileReader
- FileWriter

Note that it is just those classes in the java.io package that are deprecated, not the entire package.

## java.io.file package

There is a new java.nio.file package with the following classes/interfaces that provide cleaner and better functionality for the deprecated classes.
- Files (Supports some static methods that return instance of stream classes - newBufferReader(), newBuffferedWriter() etc)
- Path
- Paths (Support static methods to return instance of Path)
- FileSystem
- FileSystems (Support static methods to return instance of FileSystem)
