# String Format

String이 아닌 타입들과 String을 섞어서 이어 붙이려고 하다보면 따옴표 열고 닫기가 넘나 귀찮기도 하고 띄어 쓰기도 헷갈림. 이럴 때 System.out.printf() 같은 걸 씁시다.

## Format Specifier의 형식

${argument index}{flags}{width}{precision}conversion

### conversion

- %d - Decimal (Integer)
- %o - Octal
- %x or %X - Hexadecimal
- %f - Decimal (Float)
- %s - 들어가는 Parameter가 Formattable을 구현하면 format()을 쓰고 아니면 toString()을 쓴다

### flags
- **#** - radix
- **0** - zero-padding (used with width)
- **-** - left-justify (used with width)
- **,** - include group separator
- **_space_** - leave space for positive number

### Argument Index
- 아무 것도 안함 - 그냥 argument로 들어간 순서대로. 대부분은 이렇게 쓰는 걸로 충분하죠
- **$_index_** - Index of argument to use
- **<** - 좀 전에 들어간 format specifier와 같은 걸로. 똑같은 값을 여러번 다르게 format할 때 유용

## Formatter class

**Appendable** interface를 구현하는 객체들 (Writer라거나) 에게 컨텐츠를 포맷해서 보낼 수 있다. AutoClosable을 구현하기 때문에 try-with-resources로 쓸 수 있고, 안에 들어간 Writer object도 알아서 닫아줌 
