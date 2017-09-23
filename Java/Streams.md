# Streams.md

Streams are uni-directional flow of data. On the abstract level, there are 2 types of stream:
1. Stream that work on byte level (InputStream and OutputStream)
2. Stream that work on char level (Reader and Writer)

## Complication in closing the Stream properly
Streams often work with resources that reside outside the JVM where the memory management is automatically handled, thus require some manual 'closing' once you are done working with the class. There are several complexities that entail this however.
