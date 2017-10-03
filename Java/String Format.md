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
