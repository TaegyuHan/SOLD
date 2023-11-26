# DIP (Dependency Inversion Principle)

- Dependency : 의존성
- Inversion : 역전
- Principle : 원칙

> 고수준 모듈이 저수준 모듈에 직접 의존하지 않도록 하여, 시스템의 유연성과 재사용성을 증가시키는 원칙입니다. 이 원칙에 따르면, 모듈 간의 의존성은 추상화에 기반해야 합니다. 즉, 추상화된 인터페이스를 통해 서로 의존하도록 하는 것이 핵심입니다.

DIP를 적용하지 않은 경우, 고수준 모듈(비즈니스 로직을 수행하는 모듈)이 저수준 모듈(데이터 접근 또는 기타 기술적 세부사항을 처리하는 모듈)에 직접 의존하게 됩니다. 이는 유연성과 재사용성을 저하시킵니다.

## DIP를 적용하기 전

```java
public class CustomerService {
    private OracleDatabase database;

    public CustomerService() {
        this.database = new OracleDatabase(); // OracleDatabase에 직접 의존
    }

    public void addCustomer(Customer customer) {
        database.add(customer);
    }
}

public class OracleDatabase {
    public void add(Customer customer) {
        // Oracle 데이터베이스에 고객 정보 저장
    }
}
```

위 코드에서 `CustomerService` 클래스는 `OracleDatabase` 클래스에 직접 의존하고 있습니다. 이렇게 되면, 데이터베이스를 변경하려 할 때 `CustomerService` 클래스도 수정해야 합니다.

## DIP를 적용한 후

```java
public interface CustomerRepository {
    void add(Customer customer);
}

public class CustomerService {
    private CustomerRepository repository;

    public CustomerService(CustomerRepository repository) {
        this.repository = repository; // 의존성 주입
    }

    public void addCustomer(Customer customer) {
        repository.add(customer);
    }
}

public class OracleDatabase implements CustomerRepository {
    @Override
    public void add(Customer customer) {
        // Oracle 데이터베이스에 고객 정보 저장
    }
}
```

DIP를 적용한 이 코드에서 `CustomerService`는 `CustomerRepository` 인터페이스에 의존합니다. 이 인터페이스는 `OracleDatabase` 클래스에 의해 구현됩니다. 이제 CustomerService 클래스는 특정 데이터베이스 구현에 직접적으로 의존하지 않게 되므로, 다른 데이터베이스로 쉽게 전환할 수 있습니다. 새로운 데이터베이스 구현이 필요한 경우, `CustomerRepository` 인터페이스를 구현하는 새 클래스를 만들면 됩니다.