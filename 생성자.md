### 생성자

```java
package ex5;

class Player { // 생성자의 이름은 클래스와 같다.

    String name;
    int hp;

    public Player(String name, int hp) { // 생성자 생성
        this.name = name;
        this.hp = hp;
    }

    public Player(String name) { // 이름만 설정
        this(name, 100); // 오버로딩 사용
    }

    public Player() { // 기본값
        this("Steve", 100); // 오버로딩 사용
    }

    public void showStatus() {
        System.out.println("이름: " + name + " 체력: " + hp);
    }

}

public class PlayerMain {
    public static void main(String[] args) {

        Player player1 = new Player("Zombie", 50);
        Player player2 = new Player("Skeleton");
        Player player3 = new Player();

        player1.showStatus();
        player2.showStatus();
        player3.showStatus();
    }
}

```

```
이름: Zombie 체력: 50
이름: Skeleton 체력: 100
이름: Steve 체력: 100
```

---

1. <ins>오버로딩</ins>을 사용해서 생성자를 여러개 만들 수 있다. 
2. 클래스에서 생성자를 생성하지 않으면 컴파일러가 <ins>자동으로 기본 생성자</ins>(매개변수X)를 추가한다.
3. 메서드 내에서는 매개변수가 우선순위에 있다!
---
### 생성자 호출 막기

```java
package ex5;

class MathTool {

    private MathTool() { // 생성자 생성 X

    }

    public static int add(int a, int b) {
        return a + b;
    }

    public static int minus(int a, int b) {
        return a - b;
    }

    public static double divide(int a, int b) {
        return (double) a / b;
    }

}

public class MathMain {
    public static void main(String[] args) {

        // MathTool mathTool = new MathTool(); 객체 생성 불가능
        int addResult = MathTool.add(5,5);
        int minusResult = MathTool.minus(5, 10);
        double divideResult = MathTool.divide(15,2);

        System.out.println(addResult);
        System.out.println(minusResult);
        System.out.println(divideResult);
    }
}
```

1. 객체 생성이 불가능 하므로, 객체와 독립적인 메서드 영역에서 MathTool 클래스의 메서드를 호출해야한다. 
