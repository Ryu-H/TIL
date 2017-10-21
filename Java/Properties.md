# Properties
Hashtable로 구현됨. Application의 실행 사이에 Key/Value Pair를 저장하고 싶을 때 쓰는 듯

## 기본적인 사용법
- `setPropeties()`
- `getProperties(String key)` & `getProperties(String key, String default)`
- `new Properties(Properties default)` - 컨스트럭터에 다른 Properties를 집어넣으면 기본값으로 쓸 수 있음 (상기한 getProperties with default보다 우선권을 가짐)

## 파일로 저장하기
- 이미 뭔가 들어가 있는 Properties에 load를 할 경우, 중복된 키 값은 Override되는 듯
- store할 때 커멘트에 ""을 넣으면 위에 #만 생기고 null을 집어넣으면 커멘트 줄 자체가 없어진다


### Simple Text
```
#Comment
#Sat Oct 21 16:19:54 NZDT 2017
Key1=Value1
Key2=Value2
spa\ ces=yeah spaces
```
InputStream, OutputStream, Reader 그리고 Writer로 사용 가능. 커멘트는 솔직히 왜 필요한지 모르겠..

- `.load(InputStream inputStream)`
- `.load(Reader reader)`
- `.store(OutputStream outputStream, String comment)`
- `.store(Writer writer, String comment)`

### XML
```xml
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<!DOCTYPE properties SYSTEM "http://java.sun.com/dtd/properties.dtd">
<properties>
  <comment>comment</comment>
  <entry key="Key1">Value1</entry>
  <entry key="Key2">Value2</entry>
  <entry key="spa ces">yeah spaces</entry>
</properties>
```

InputStream과 OutputStream으로만 사용 가능.

- `.loadFromXML(InputStream inputStream)`
- `.storeToXML(OutputStream outputStream)`
