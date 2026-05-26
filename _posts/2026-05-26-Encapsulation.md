---
layout: single
title:  "[Java] 객체의 상태는 숨기고 행동만 노출하라 - 캡슐화(Encapsulation)"
categories: coding
tag: [Java]
---

객체지향 프로그래밍을 공부하다 보면 캡슐화(Encapsulation)라는 말을 정말 많이 듣게 된다.  
하지만 많은 사람들이 캡슐화를 단순히:

- private 사용하기
- getter/setter 만들기

정도로만 이해하는 경우가 많다.

하지만 캡슐화의 핵심은 단순히 데이터를 숨기는 것이 아니다.

캡슐화는 객체 내부의 구현을 숨기고, 외부에서는 정해진 인터페이스를 통해서만 객체를 조작하도록 만드는 것이다. (MangKyu's Diary)

즉, 객체가 자신의 상태를 스스로 관리하게 만드는 것이 핵심이다.

---

# 1. 캡슐화가 필요한 이유

은행 계좌를 예시로 생각해보자.

계좌(Account)는 다음과 같은 상태를 가진다.

- 잔액(balance)

그리고 다음과 같은 행동을 가진다.

- 입금(deposit)
- 출금(withdraw)
- 잔액 조회(getBalance)

그런데 만약 외부에서 balance에 직접 접근할 수 있다면 어떨까?

## 잘못된 설계 예시
``` java
public class BankAccount { 
	public long balance;  
} 
```

이 경우 외부에서 다음과 같은 코드가 가능해진다.
``` java
BankAccount account = new BankAccount();
	account.balance = -1000000; 
```

즉, 객체의 상태가 언제든지 잘못된 값으로 변경될 수 있다.

이러한 구조는:

- 데이터 무결성을 깨뜨리고
- 비즈니스 규칙을 강제할 수 없으며
- 유지보수를 어렵게 만든다.

---

# 2. 캡슐화를 적용한 객체

캡슐화의 핵심은 상태를 숨기고, 정해진 행동만 외부에 공개하는 것이다.

따라서 balance를 private으로 숨기고,  
입금/출금 메서드를 통해서만 상태를 변경하도록 만든다.

## 캡슐화된 계좌 객체 구조
``` java
public class BankAccount {

    private long balance;

    public BankAccount(long balance) {
        this.balance = balance;
    }

    public void deposit(long amount) {

        if (amount <= 0) {
            throw new IllegalArgumentException("입금 금액은 0보다 커야 합니다.");
        }

        balance += amount;
    }

    public void withdraw(long amount) {

        if (amount > balance) {
            throw new IllegalArgumentException("잔액이 부족합니다.");
        }

        balance -= amount;
    }

    public long getBalance() {
        return balance;
    }
}
```


이제 객체는 스스로 자신의 상태를 관리하게 된다.

외부에서는:

- deposit()
- withdraw()

같은 공개된 메서드만 사용할 수 있고,  
잔액(balance)을 직접 변경할 수는 없다.

---

# 3. getter/setter를 많이 만드는 것이 좋은 설계일까?

많은 사람들이 캡슐화를 다음처럼 이해한다.
``` java
@Getter
@Setter
public class User {

    private String name;
    private int age;

}
```

하지만 무분별한 setter는 객체의 상태를 외부에서 마음대로 변경할 수 있게 만든다.

즉, 객체가 자신의 상태를 스스로 제어하지 못하게 된다.

실제로 객체지향에서는:

> 객체의 상태보다 객체의 행동이 더 중요하다.

라는 이야기를 많이 한다. (MangKyu's Diary)

따라서 객체는 단순한 데이터 저장소가 아니라:

- 자신의 상태를 관리하고
- 비즈니스 규칙을 검증하며
- 스스로 책임을 수행해야 한다.

---

# 4. 캡슐화의 장점

## 1) 데이터 보호

객체 내부 상태를 외부에서 직접 변경할 수 없다.

즉, 잘못된 값이 들어오는 것을 막을 수 있다.

---

## 2) 비즈니스 규칙 강제

출금 금액이 잔액보다 큰 경우를 생각해보자.

캡슐화가 되어 있다면 withdraw() 내부에서 이를 검증할 수 있다.

즉, 객체가 스스로 자신의 규칙을 지키게 된다.

---

## 3) 유지보수 용이

내부 구현이 변경되더라도 외부 코드에는 영향을 최소화할 수 있다.

즉:

- 구현(Implementation)
- 인터페이스(Interface)

를 분리할 수 있게 된다. (MangKyu's Diary)

---

# 5. 캡슐화의 핵심은 "정보 은닉"이다

캡슐화는 단순히 private을 사용하는 기술이 아니다.

진짜 핵심은:

- 변경될 수 있는 구현을 숨기고
- 외부에는 안정적인 인터페이스만 공개하는 것이다. (MangKyu's Diary)

즉:

- 객체의 상태는 숨기고
- 객체의 행동만 외부에 공개해야 한다.

---

# 마무리

캡슐화는 객체지향 설계의 가장 중요한 원칙 중 하나이다.

좋은 객체는:

- 자신의 상태를 스스로 관리하고
- 외부의 잘못된 접근을 막으며
- 정해진 방식으로만 동작하도록 설계되어야 한다.

그리고 이러한 설계를 가능하게 만드는 핵심이 바로 캡슐화이다.

결국 객체지향 프로그래밍은:

> "데이터를 외부에 노출하는 것"이 아니라  
> "객체가 스스로 책임지게 만드는 것"

이라고 볼 수 있다.