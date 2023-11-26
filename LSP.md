# LSP (Liskov Substitution Principle)

- Liskov : 리스코프
- Substitution : 치환
- Principle : 원칙

> 이 원칙은 하위 클래스는 언제나 상위 클래스를 대체할 수 있어야 한다고 주장합니다. 즉, 상위 클래스의 인스턴스를 하위 클래스의 인스턴스로 대체해도 프로그램의 기능이 올바르게 작동해야 합니다.

이 원칙을 위반하는 경우, 하위 클래스가 상위 클래스의 기능을 제대로 수행하지 못하거나, 상위 클래스가 가진 규약을 변경하는 경우가 발생할 수 있습니다.

## LSP를 적용하기 전

```java
public class Rectangle {
    protected int width;
    protected int height;

    public void setWidth(int width) {
        this.width = width;
    }

    public void setHeight(int height) {
        this.height = height;
    }

    public int getArea() {
        return width * height;
    }
}

public class Square extends Rectangle {
    @Override
    public void setWidth(int width) {
        super.setWidth(width);
        super.setHeight(width); // 사각형의 너비와 높이가 같도록 설정
    }

    @Override
    public void setHeight(int height) {
        super.setWidth(height); // 사각형의 너비와 높이가 같도록 설정
        super.setHeight(height);
    }
}
```

위의 코드에서 Square 클래스는 Rectangle의 하위 클래스입니다. 하지만 setWidth나 setHeight 메서드를 호출할 때 사각형의 너비와 높이를 같게 설정합니다. 이는 Rectangle의 정의와 맞지 않으므로 LSP를 위반하는 것입니다.

## LSP를 적용한 후

```java
public interface Shape {
    int getArea();
}

public class Rectangle implements Shape {
    protected int width;
    protected int height;

    public Rectangle(int width, int height) {
        this.width = width;
        this.height = height;
    }

    @Override
    public int getArea() {
        return width * height;
    }
}

public class Square implements Shape {
    private int side;

    public Square(int side) {
        this.side = side;
    }

    @Override
    public int getArea() {
        return side * side;
    }
}
```

이 코드에서는 Shape 인터페이스를 정의하고, Rectangle과 Square는 각각 이 인터페이스를 구현합니다. 이제 Square와 Rectangle은 서로 다른 클래스이지만, 같은 인터페이스를 구현합니다. 이 방법으로 Square는 Rectangle의 대체품으로 쓰이지 않으므로 LSP를 준수하게 됩니다.