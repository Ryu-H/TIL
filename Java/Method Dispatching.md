# Method Dispatching and Overloading

## Static Method Dispatching (Static Binding)

Static Method Dispatching 혹은 Static Binding은 compile time 때 일어난다 (class 정보를 사). 즉 compiler는 compile 타임에 어떤 메서드가 호출될지 알고 있다 or 알아야 한다. Overloading 같은 경우는 Static Dispatching에 해당한다.

## Receiver Parameter and Dynamic Method Dispatching

Dynamic Method Dispatching 혹은 Dynamic Binding은 runtime 때 일어난다 (object 정보를 사용). Overriding의 경우는 Dynamic Dispatching에 해당한다.

```java
Service svc = new ServiceImpl();
svc.run();
```
위에 예제문에 있는 Service가 interface 혹은 abstract class이고 ServiceImpl이 그 interface나 abstract class의 run()을 구현하는 concrete class라고 했을 때, 우리가 보기엔 compile time때 어떤 구현 메서드가 호출될지 결정될 것 같아 보이지만 실제로는 Dynamic Method Dispatching이 이루어지고 있다. 즉 compile time에서 compiler는 정확히 어떤 구현 클래스의 메서드가 호출될지 모른다. 코드를 작성하는 동안에는 눈에 보이진 않지만 실제로는 메서드가 invoke되는 object가 receiver parameter로 들어가고 그걸 이용해서 runtime 때 어떤 메서드가 실행될지 결정된다.

### Double Dispatching

Java의 경우 Single Receiver만 지원하는 언어이기 때문에 (이 부분에 관해 내가 아직 세밀하게 이해를 하고 있진 않지만) 아래와 같은 코드는 compile error가 발생한다.
```java
public class DispatchingFailExample {

    interface Post {
        void publishPost(Facebook sns);

        void publishPost(Instagram sns);
    }

    static class Text implements Post {
        @Override
        public void publishPost(Facebook sns) {
            System.out.println("Text - Facebook");
        }

        @Override
        public void publishPost(Instagram sns) {
            System.out.println("Text - Instagram");
        }
    }

    static class Picture implements Post {
        @Override
        public void publishPost(Facebook sns) {
            System.out.println("Picture - Facebook");
        }

        @Override
        public void publishPost(Instagram sns) {
            System.out.println("Picture - Instagram");
        }
    }

    interface SNS {}

    static class Facebook implements SNS {}

    static class Instagram implements SNS {}

    public static void main(String[] args) {
        List<Post> postFormats = Arrays.asList(new Text(), new Picture());

        List<SNS> snsPlatforms = Arrays.asList(new Facebook(), new Instagram());

        postFormats.forEach(p -> snsPlatforms.forEach(s -> p.publishPost(s)));
    }
}
```

Method Overloading을 위해서는 Static Dispatching이 일어나야 하기 때문에 compile 타임에 s가 어떤 타입인지 알 수 있어야 하는데 위에 코드에선 그것을 알 수 없다 - 물론 우리가 Facebook과 Instagram을 직접 만들어서 리스트에 넣긴 했지만 아랫단에서는 그저 SNS의 리스트라는 것 밖엔 모른다.

만약에 위와 비슷한 형태의 구조에서 다차원적인 다형성을 필요로 할 경우에 Double Dispatching을 사용한다.

```java
public class DoubleDispatchingExample {

    interface Post {
        void publishPost(SNS sns);
    }

    static class Text implements Post {
        @Override
        public void publishPost(SNS sns) {
            sns.publish(this);
        }
    }

    static class Picture implements Post {
        @Override
        public void publishPost(SNS sns) {
            sns.publish(this);
        }
    }

    interface SNS {
        void publish(Picture picture);
        void publish(Text text);
    }

    static class Facebook implements SNS {
        @Override
        public void publish(Picture picture) {
            System.out.println("Picture - Facebook");
        }

        @Override
        public void publish(Text text) {
            System.out.println("Text - Facebook");
        }
    }

    static class Instagram implements SNS {
        @Override
        public void publish(Picture picture) {
            System.out.println("Picture - Instagram");
        }

        @Override
        public void publish(Text text) {
            System.out.println("Text - Instagram");
        }
    }

    public static void main(String[] args) {
        List<Post> postFormats = Arrays.asList(new Text(), new Picture());

        List<SNS> snsPlatforms = Arrays.asList(new Facebook(), new Instagram());

        postFormats.forEach(p -> snsPlatforms.forEach(s -> p.publishPost(s)));
    }
}
```

## 몇가지 포인트
- Overloading은 method name과 parameter type만 가능하다. Return Type은 Method Signature에 포함되지 않고 따라서 같은 method name과 parameter type을 가졌지만 return type만을 바꿔서 overloading을 하는 건 불가능하다.

- 위와 같은 방식을 이용한 Visitor Pattern이 있다.

- Proxy Visitor Pattern - JPA 쿼리에서 Proxy들을 불러오거나 하는 경우 instanceof가 먹지 않기 때문에 Visitor Pattern을 사용할 수 밖에 없다.

- 자세한 Recap은 [토비의 봄TV 1회](https://youtu.be/s-tXAHub6vg) 참고
