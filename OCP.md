# OCP(Open-Closed Principle)

- Open : 개방
- Closed : 폐쇠
- Principle : 원칙

> 클래스는 확장에는 열려 있어야 하지만 수정에는 닫혀 있어야 한다는 원칙입니다. 즉, 기존 코드를 변경하지 않고도 클래스의 기능을 확장할 수 있어야 합니다.

이 원칙을 Java 코드로 설명하기 위해, 간단한 예를 들겠습니다. 가정해보겠습니다: 우리는 여러 종류의 직원에 대한 급여 계산 시스템을 개발하고 있습니다.

## OCP를 적용하기 전

```java
public class Employee {
    private String type;

    public Employee(String type) {
        this.type = type;
    }

    public String getType() {
        return type;
    }
}

public class PayrollSystem {
    public double calculatePay(Employee employee) {
        if (employee.getType().equals("Permanent")) {
            // 영구 직원에 대한 급여 계산
            return calculatePermanentPay();
        } else if (employee.getType().equals("Temporary")) {
            // 임시 직원에 대한 급여 계산
            return calculateTemporaryPay();
        }
        return 0.0;
    }

    private double calculatePermanentPay() {
        // 영구 직원 급여 계산 로직
        return 4000.0;
    }

    private double calculateTemporaryPay() {
        // 임시 직원 급여 계산 로직
        return 2000.0;
    }
}
```

위의 코드에서 PayrollSystem 클래스는 직원의 유형에 따라 다른 급여 계산 로직을 적용합니다. 새로운 직원 유형이 추가될 때마다 PayrollSystem 클래스를 수정해야 합니다. 이는 OCP를 위반하는 것입니다.

## OCP를 적용한 후

```java
public abstract class Employee {
    public abstract double calculatePay();
}

public class PermanentEmployee extends Employee {
    @Override
    public double calculatePay() {
        // 영구 직원 급여 계산 로직
        return 4000.0;
    }
}

public class TemporaryEmployee extends Employee {
    @Override
    public double calculatePay() {
        // 임시 직원 급여 계산 로직
        return 2000.0;
    }
}

public class PayrollSystem {
    public double calculatePay(Employee employee) {
        return employee.calculatePay();
    }
}
```

이렇게 변경하면, PayrollSystem 클래스는 수정할 필요 없이 새로운 직원 유형을 추가할 수 있습니다. 각 직원 유형의 급여 계산 로직은 해당 직원 유형의 클래스 내에서 정의됩니다. 새로운 직원 유형을 추가하고 싶다면, 단순히 Employee를 상속받는 새로운 클래스를 만들고 calculatePay 메서드를 구현하면 됩니다. 이는 OCP 원칙을 잘 따른 예입니다.