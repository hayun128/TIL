# Facade Pattern

<aside>
✨ Facade Pattern이란

서브시스템을 쉽게 사용할수 있도록 하이레벨 인터페이스를 정의하고 제공하는 것

</aside>

예를 들어 영화를 보려고 한다면 

TV켜기 → 영화 검색 → 영화 결제 → 영화 재생 

이라는 단계를 거처야 함 

큰 동작인 영화보기를 위해 작은 서브동작인 검색이나 결제가 필요한 것

### 예제

---

```java
public class Facade {
    private String beverageName;
    private String MovieName;

		public Facade(String beverage, String MovieName) {
        this.beverageName = beverageName;
        this.MovieName = MovieName;
    }

    public void ViewMovie() {
        Beverage beverage = new Beverage(beverageName);
        RemoteControl remote = new RemoteControl();
        Movie movie = new Movie(MovieName);

        remote.TurnOn();
        movie.SearchMovie();
        movie.ChargeMovie();
        movie.PlayMovie();
    }

}
```

만든 서브동작들을 Facade에서 하나로 묶고

```java
public void view() {
            Facade facade = new Facade("포도주스", "범죄도시3");
            facade.ViewMovie();
    }
```

실행한다
