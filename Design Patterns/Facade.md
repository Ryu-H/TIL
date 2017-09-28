# Facade
Design Pattern으로 굳이 분류하거나 정의하기에 애매할 정도로 넘나 자주 보이고 흔히 쓰이는 패턴.. 복잡한 내부적 Sub-system들을 Facade로 추상화 시켜서 복잡도를 낮추는 기법이라고 하면 될 듯 하다.

## 사용하면 좋은 점
- 사용하는 모듈은 Facade를 통해서 필요한 동작들을 수행함으로서 복잡할 수 있는 내부적인 Sub-system에 관해 신경쓰지 않아도 된다 - 존재조차 모르면 물론 더 좋음
- 사용되는 모듈은 외부에서 Sub-system에 직접적으로 들어오는 Dependency가 줄어들면서 시스템에 기능을 더하거나 코드를 유지보수하기가 쉬워진다
- 새로 짜는 코드에서 오래된 Legacy code나 디자인이 별로인 API를 사용해야 할 경우 직접적으로 연동하려고 하면 지저분해질 수 있다. 이럴 때도 그 위에 Facade를 입혀서 새로 짜는 코드의 시점에서 적절한 추상화를 시키면 깔끔하게 사용할 수 있다

## Example Code
```java
public class TV {
  private Screen screen;
  private Speaker speaker;
  private PowerSupply powerSupply;

  public TV() {
    this.screen = new Screen();
    this.speaker = new Speaker();
    this.powerSupply = new PowerSupply();
  }

  public void powerOn() {
    this.powerSupply.supplyPower();
    this.screen.displayStuff();
    this.speaker.emitSound();
  }
}

public class Screen {
  public void displayStuff() {
  }
}

public class Speaker {
  public void emitSound() {
  }
}

public class PowerSupply {
  public void supplyPower() {
  }
}

class Me {
    public static void main(String[] args) {
      TV tv = new TV();
      tv.powerOn();
    }
}

```
