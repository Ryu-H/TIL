# String Format

String이 아닌 타입들과 String을 섞어서 이어 붙이려고 하다보면 따옴표 열고 닫기가 넘나 귀찮기도 하고 띄어 쓰기도 헷갈림. 이럴 때 System.out.printf() 같은 걸 씁시다.

## Format Specifier

- %d - Decimal (Integer)
- %o - Octal
- %x - Hexadecimal
- %f - Decimal (Float)
- %s - 들어가는 Parameter가 Formattable을 구현하면 format()을 쓰고 아니면 toString()을 쓴다
