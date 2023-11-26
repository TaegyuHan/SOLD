# SRP (Single Responsibility Principle)

- Single : 단일
- Responsibility : 책임
- Principle : 원칙

> 이 원칙에 따르면, 클래스는 하나의 책임만 가져야 합니다. 즉, 클래스는 변경의 이유가 오직 하나여야 합니다. 이 원칙은 코드의 복잡성을 줄이고 유지보수를 용이하게 합니다.

## SRP를 적용하기 전의 클래스

```java
public class User {
    private String name;
    private String email;

    public User(String name, String email) {
        this.name = name;
        this.email = email;
    }

    // 사용자 정보를 데이터베이스에 저장
    public void saveToDatabase() {
        // 데이터베이스 저장 로직
        System.out.println("Saving user to database");
    }

    // 기타 사용자 관련 메서드들
}
```

위의 User 클래스는 사용자 정보를 관리하고 데이터베이스에 저장하는 두 가지 책임을 갖고 있습니다. 이는 SRP를 위반하는 것입니다.

## SRP를 적용한 후의 클래스들

```java
public class User {
    private String name;
    private String email;

    public User(String name, String email) {
        this.name = name;
        this.email = email;
    }

    // 기타 사용자 관련 메서드들
}

public class UserRepository {
    public void save(User user) {
        // 데이터베이스 저장 로직
        System.out.println("Saving user to database");
    }
}
```

위와 같이 변경하면 User 클래스는 오직 사용자 정보를 관리하는 책임만을 갖게 되며, UserRepository 클래스는 사용자 정보를 데이터베이스에 저장하는 책임을 갖게 됩니다. 이렇게 책임을 분리함으로써, 각 클래스는 변경에 대한 이유가 단 한 가지만을 갖게 되며, 이는 유지보수와 확장성을 향상시키는 데 도움이 됩니다.