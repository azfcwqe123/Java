## 상속 & 인터페이스

인터페이스
```java
package ex6;

public interface UnderWaterCharacter {
    void swim();
}

```

부모 클래스
```java
package ex6;

public class ZombieCharacter {

    String item;

    public ZombieCharacter(String item) {
        this.item = item;
    }

    public void showHp() {
        System.out.println("좀비의 체력은 20입니다.");
    }

    public void attack() {
        System.out.println("좀비가 공격합니다.");
    }

    public void dropItem() {
        System.out.println("몬스터가 죽었습니다 -> 썩은 고기 드랍");
    }

}


```

자식 클래스1
```java
package ex6;

public class Zombie extends ZombieCharacter { // 부모클래스에서 상속을 받는다.

    public Zombie(String item) {
        super(item); // 부모 생성자. 필수 호출
    }
}

```

자식 클래스2
```java
package ex6;

public class Husk extends ZombieCharacter { // 부모클래스에서 상속을 받는다.

    int hp; // 부모 클래스는 자식 클래스 사용 불가능.

    public Husk(String item, int hp) {
        super(item); // 부모 생성자. 필수 호출
        this.hp = hp;
    }

    @Override // 메서드 재정의(오버라이딩)
    public void showHp() {
        System.out.println("허스크의 체력은 " + hp + "입니다.");
    }

    @Override // 메서드 재정의(오버라이딩)
    public void attack() {
        System.out.println("허스크가 " + super.item + " 공격합니다."); // super.item -> 자식 클래스는 부모 클래스 사용 가능
    }

    public void attackEffect() { // 부모 클래스는 자식 클래스 사용 불가능.
        System.out.println("허기 상태 효과를 발동시킵니다.");
    }

    @Override // 메서드 재정의(오버라이딩)
    public void dropItem() {
        System.out.println("허스크가 죽었습니다 -> " + item + " 드랍");
    }
}


```

자식 클래스3
```java
package ex6;

public class Drowned extends ZombieCharacter implements UnderWaterCharacter { // 부모클래스와 인터페이스의 상속을 받는다.

    int hp; // 부모 클래스는 자식 클래스 사용 불가능.

    public Drowned(String item, int hp) {
        super(item); // 부모 생성자. 필수 호출
        this.hp = hp;
    }

    @Override
    public void showHp() { // 메서드 재정의(오버라이딩)
        System.out.println("익사자의 체력은 " + hp +"입니다.");
    }

    @Override
    public void attack() { // 메서드 재정의(오버라이딩)
        System.out.println("익사자가 " + super.item + " 공격합니다."  );
    }

    public void attackEffect() { // 부모 클래스는 자식 클래스 사용 불가능.
        System.out.println("삼지창을 던집니다.");
    }

    @Override
    public void dropItem() { // 메서드 재정의(오버라이딩)
        System.out.println("익사자가 죽었습니다 -> " + item + " 드랍");
    }

    public void swim() { // 인터페이스 기능을 구현.
        System.out.println("익사가 헤엄칩니다.");
    }
}

```

메인 클래스
```java
package ex6;

public class ZombieMain {
    public static void main(String[] args) {

        // 좀비 생성
        Zombie zombie = new Zombie("썩은 고기");
        Husk husk = new Husk("철 칼", 30);
        Drowned drowned = new Drowned("삼지창", 40);

        showZombie(zombie);
        showZombie(husk);
        showZombie(drowned);
    }

    static void showZombie(ZombieCharacter character) { // 부모 클래스는 자식을 담을 수 있다. 반대는 불가능

        character.showHp();
        character.attack();

        // instanceof는 객체가 특정 클래스나 인터페이스의 인스턴스인지 여부를 확인. // boolean 값 반환
        // 오른쪽이 왼쪽을 담을 수 있는지 확인하면 된다.
        if(character instanceof Husk husk) {
            husk.attackEffect();
        } else if(character instanceof Drowned drowned) {
            drowned.attackEffect();
            drowned.swim();
        }

        character.dropItem();

        System.out.println("--------");
    }
}


```

실행
```java
좀비의 체력은 20입니다.
좀비가 공격합니다.
몬스터가 죽었습니다 -> 썩은 고기 드랍
--------
허스크의 체력은 30입니다.
허스크가 철 칼 공격합니다.
허기 상태 효과를 발동시킵니다.
허스크가 죽었습니다 -> 철 칼 드랍
--------
익사자의 체력은 40입니다.
익사자가 삼지창 공격합니다.
삼지창을 던집니다.
익사가 헤엄칩니다.
익사자가 죽었습니다 -> 삼지창 드랍
--------
```

1. 부모 클래스에 생성자가 있을시, 자식 클래스에서 반드시 부모 클래스의 생성자(super)을 생성해줘야 한다.
2. 부모 클래스는 자식 클래스의 기능들을 사용하지 못한다.
3. 자식 클래스는 super 키워드를 사용해서 부모 클래스의 기능 사용 가능.
4. A instanceof B b 꼴은 타입 검사와 캐스팅된 객체 사용을 동시에 가능. // b라는 객체를 새로 생성하는 것이 아님. 
5. 인터페이스를 구현하는 클래스는, 오버라이딩 메서드와 다르게 인터페이스의 기능들을 반드시 구현해야한다.
6. 인터페이스는 public abstract가 묵시적으로 선언돼있다.
---


