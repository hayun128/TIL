# 의존성

## 의존성이란?

<aside>
✨ 파라미터나 리턴값, 지역변수 등으로 다른 겍체를 참조하는 것

</aside>

- **A가 B에 의존한다 ⇒ B가 변하면 A에 영향을 미친다**
  A 클래스가 B 클래스를 사용할때 **A가 B에 의존한다**고 말한다
  ⇒ 이럴때 A는 B가 없다면 작동할수 없다
  ⇒ **B가 변하면 A에 영향을 미친다**

예를 들어 피자 가게 요리사는 피자 레시피가 바뀌면 바뀐 레시피를 따라 피자 만드는 방법을 바꿔야 한다

→ **레시피의 변화가 요리사의 행동에 영향을 미쳤기 때문에**
**요리사는 레피시에 의존한다** 라고 볼수 있다

- 코드
  ```java
  class BurgerChef {
      private HamBurgerRecipe hamBurgerRecipe;

      public BurgerChef() {
          hamBurgerRecipe = new HamBurgerRecipe();
      }
  }
  ```
  더 많은 버거레시피를 의존하게 하려면 인터페이스로 추상화해야 한다
  ```java
  class BurgerChef {
      private BurgerRecipe burgerRecipe;
  		/*버거셰프의 맴버변수인 버거레시피를 선언
  			버거레시피 인터테이스의 객체를 참조한다
  			버거셰프클래스의 객체가 만들어질때 햄버거 레시피로 초기화 된다

  			=> 버거셰프 객체가 버거레시피 변수를 통해서 햄버거레시피 클래스의
  				  newBurger() 메도스를 호출할 수 있다*/

      public BurgerChef() {
          burgerRecipe = new HamBurgerRecipe();
  					//생성자에서 버거 레시피를 햄버거레시피로 초기화
          //burgerRecipe = new CheeseBurgerRecipe();
          //burgerRecipe = new ChickenBurgerRecipe();
      }
  }

  interface BugerRecipe {  //인터페이스
      newBurger();
      // 이외의 다양한 메소드
  }

  class HamBurgerRecipe implements BurgerRecipe { //인터페이스로 객체 구현하기
      //newBurger() 메소드를 오버라이드해서 햄버거 객체를 만들고 반환한다
  		public Burger newBurger() {
          return new HamBerger();
      }
      // ...
  }
  ```

# DI

Dependency Injection 의존성 주입이란

위에 코드처럼 버거셰프 안에서 의존관계인 버거레시피가 어떤건지 직접 정했다면

예를 들어서 **메뉴 결정을 사장님이 하는거야** 음 햄버거는 맛이 없어 빼 치즈버거를 넣자 이러는데 사장님은 의존관계가 있는 레시피와 셰프와는 다른 사람이잖아 제 3자그러니까 외부에서 의존관계를 정해주고 주입(제공)한다 이렇게 됨

의존관계를 의존관계 외부에서 결정하고 주입하는 것이 DI 의존성 주입이다

직접적인 의존관계가 아니게 만들어주는 것

## 장점

1. 의존성이 줄어든다

   DI로 구현하면 **주입받는대상이 변해도 구현한걸 수정할 일이 없거나 줄어든다**

2. 버거셰프 안에서만 사용되던 레시피를 셰프와 나눠서 구현하게 되면 새로 만들지 않고 **재사용**할수 있다

3. 레시피를 셰프와 **분리해서 테스트**할수 있다

4. 기능들을 분리하면 **가독성**이 높아진다

## 구현하는 방법

의존관계를 외부에서 결정하는 것 ⇒ **클래스 변수를 결정하는 방법**이 DI를 구현하는 방법이다

의존하는 객체를 그대로 가져오는 것이 아니라 클래스 변수로 받는 것

```java
class BurgerChef {
    private BurgerRecipe burgerRecipe;

    public BurgerChef(BurgerRecipe burgerRecipe) {
        this.burgerRecipe = burgerRecipe;
    }
}

class BurgerRestaurantOwner {
    private BurgerChef burgerChef = new BurgerChef(new HamburgerRecipe());

    public void changeMenu() {
        burgerChef = new BurgerChef(new CheeseBurgerRecipe());
    }
}
```

```java
class BurgerChef {
    private BurgerRecipe burgerRecipe = new HamburgerRecipe();

    public void setBurgerRecipe(BurgerRecipe burgerRecipe) {
        this.burgerRecipe = burgerRecipe;
    }
}

class BurgerRestaurantOwner {
    private BurgerChef burgerChef = new BurgerChef();

    public void changeMenu() {
        burgerChef.setBurgerRecipe(new CheeseBurgerRecipe());
    }
```

<aside>
✨ 다시 정리해보자

의존성이란 의존하는 관계에서 의존 받는 대상이 바뀔때 의존하는 대상도 영향을 받는 것 이다

DI는 의존성을 외부에서 주입해주는 것이다
의존성이 줄어들고 코드의 재사용성도 높아지고 의존받는 대상을 의존하는 대상과 분리해서 테스트를 할수 있는 등의 장점이 있다

구현하는 방법은 클래스 변수를 결정하는 방법과 같다
생성자를 이용하거나 메소드를 이용하는 등의 방법이 있다

</aside>
