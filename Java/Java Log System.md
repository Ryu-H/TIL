# Java Log System

## Summary

- `Logger.getLogger(String name)`을 부르면 이미 생성된 Logger를 리턴하거나, 없다면 새 Logger를 생성한다. LogManager로 접근 - `LogManager.getLogger(String loggerName)` - 은 이미 생성된 후에야 가능.
- Logger는 다수의 Handler를 가질 수 있고 Handler는 하나의 Formatter를 가질 수 있다.
- Logger의 이름은 계층적인 구조를 가진다. 하위 계층에 있는 Logger에 기록을 하면 상위 계층에 있는 Logger에도 함께 기록이 된다. 상위 로거의 로깅 레벨을 높게 설정해서 핵심적인 내용들만 기록하게 해두고 실제 로깅은 하위 로거에 기록을 하는 게 일반적인 사용법
- 이름 상으로 상위 로거가 있을 경우 하위 로거를 생성하면 상위 로거의 로깅 레벨등을 기본값으로 상속받는다



Example using Global Logger:
```java
LogManager logManager = LogManager.getLogManager();

Logger logger = logManager.getLogger(Logger.GLOBAL_LOGGER_NAME);

logger.log(Level.FINE, "This log entry so fine.");
```

or for simpler use
```java
static Logger logger = LogManager.getLogManager().getLogger(Logger.GLOBAL_LOGGER_NAME);
```

## LogManager
- Managed as a Singleton object per app
- Manages objects that do the actual logging

## Logger
- Does the actual logging
- Global logger available - access using the `Logger.GLOBAL_LOGGER_NAME`

## Logging Levels
- 7 Levels
  - Severe
  - Warning
  - Config
  - Info
  - Fine
  - Finer
  - Finest
- Call `setLevel(Level logLevel);` on a Logger instance to set the logging level - all loggings below the setLevel will not be registered
  - `Level.ALL` and `Level.OFF` available for setting logLevel


## Types of Log Methods
- Level Convenience methods:
```java
logger.severe("This will be logged as severe.");
logger.warning("This will be logged at the warning level.");
// and so on..
```
- Precise Log - Standard log gets the calling info wrong sometimes.. therefore:
```java
logger.logp(Level level, String className, String methodName, String message);
```

- Entering and Exiting
Logged at **Level.FINER** level. The messages will be **ENTRY** and **RETURN** respectively.
```java
logger.entering(String className, String methodName);
logger.exiting(String className, String methodName);
```

- Parameterised Logging: In the case of log, logp and entering and exiting, you can add additional parameters to the log message. To add multiple parameters, an object array will need to be passed in.
  -  For log() and logp(), the message can have positional substitution with zero-based index: {0}
  ```java
logger.log(Level.INFO, "This is a parameterised message: {0}", "parameter");
  ```
  - for entering and exiting convenience methods, the message can't be changed but the parameters will simply be space separated
  ```java
  logger.entering("classname", "methodName", new Object[]{ "first", "second"});)
  ```

## Handler
TODO

## Formatter
TODO

## Log Configuration File
TODO
