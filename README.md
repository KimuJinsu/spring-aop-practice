
# Spring AOP (Aspect-Oriented Programming) 개요

**Spring AOP**는 관점 지향 프로그래밍(AOP)을 지원하는 강력한 프레임워크로, 비즈니스 로직과 **공통 기능**(예: 로깅, 트랜잭션 관리)을 **분리**하여 코드의 **재사용성**과 **유지보수성**을 높이는 데 사용됩니다.  
이는 런타임 시 동적으로 적용되어 코드에 부가적인 기능을 삽입할 수 있습니다.

---

## 🌟 AOP의 주요 개념

Spring AOP를 구성하는 핵심 개념은 다음과 같습니다.

### 1. **Aspect (애스펙트)**
- **정의**: 여러 클래스에 걸쳐 공통적으로 사용되는 기능을 모듈화한 것입니다.  
  예: 로깅, 트랜잭션 관리, 보안 등.
- **역할**: 비즈니스 로직에 영향을 주지 않으면서 공통 기능을 추가합니다.

---

### 2. **Join Point (조인 포인트)**
- **정의**: Aspect가 적용될 수 있는 지점입니다.  
  예: 메서드 호출, 예외 처리 등.
- **특징**: Spring AOP에서 Join Point는 **메서드 실행**만을 의미합니다.

---

### 3. **Advice (어드바이스)**
- **정의**: 특정 Join Point에서 수행할 작업(로직)입니다.
- **종류**:
  - **Before Advice**: 메서드 실행 전에 동작.
  - **After Returning Advice**: 메서드가 정상적으로 실행된 후 동작.
  - **After Throwing Advice**: 메서드에서 예외가 발생한 후 동작.
  - **After (Finally) Advice**: 메서드 실행 후, 예외 발생 여부와 상관없이 동작.
  - **Around Advice**: 메서드 실행 전후에 동작하며, 실행 자체를 제어 가능.

---

### 4. **Pointcut (포인트컷)**
- **정의**: Join Point를 선별하는 기준. 특정 클래스나 메서드에만 AOP를 적용할 때 사용합니다.
- **구현**: AspectJ 포인트컷 표현식을 사용하여 정의합니다.

---

### 5. **Advisor (어드바이저)**
- **정의**: Pointcut과 Advice를 결합한 객체로, 어떤 Join Point에 어떤 Advice를 적용할지 결정합니다.

---

### 6. **Proxy (프록시)**
- **정의**: AOP에서 생성된 객체로, 타겟 객체를 대신하여 동작합니다.
- **Spring AOP의 구현**:
  - JDK 동적 프록시: 인터페이스 기반.
  - CGLIB 프록시: 클래스 기반.

---

### 7. **Weaving (위빙)**
- **정의**: Aspect를 실제 코드에 적용하는 과정입니다.
- **Spring AOP의 특징**: 런타임에 위빙이 수행됩니다.

---

## 🧩 PCD(Pointcut Designator) 설명

Pointcut Designator는 Join Point를 정확히 선택하기 위한 표현식입니다.

### 1. `execution`
- **설명**: 특정 메서드 실행에 대해 Pointcut을 적용.
- **예시**:  
  ```java
  execution(public * com.example.service.*.*(..))
  ```
  com.example.service 패키지 내의 모든 메서드에 Pointcut 적용.

---

### 2. `within`
- **설명**: 특정 클래스 내부의 메서드에 대해 Pointcut을 적용.
- **예시**:  
  ```java
  within(com.example.service.*)
  ```
  com.example.service 패키지의 클래스에 포함된 메서드에 Pointcut 적용.

---

### 3. `this`
- **설명**: 프록시 객체의 타입에 따라 Pointcut을 적용.
- **예시**:  
  ```java
  this(com.example.MyService)
  ```
  프록시 객체가 MyService 타입일 때 적용.

---

### 4. `target`
- **설명**: 실제 타겟 객체의 타입에 따라 Pointcut을 적용.
- **예시**:  
  ```java
  target(com.example.MyService)
  ```
  실제 객체가 MyService일 때 적용.

---

### 5. `args`
- **설명**: 메서드의 인자 타입에 따라 Pointcut을 적용.
- **예시**:  
  ```java
  args(String, ..)
  ```
  첫 번째 인자가 String 타입인 메서드에 적용.

---

### 6. `@within`
- **설명**: 특정 애노테이션이 있는 클래스 내부의 메서드에 적용.
- **예시**:  
  ```java
  @within(org.springframework.stereotype.Service)
  ```
  @Service 애노테이션이 있는 클래스의 모든 메서드에 적용.

---

### 7. `@target`
- **설명**: 특정 애노테이션이 붙은 클래스 객체에 적용.
- **예시**:  
  ```java
  @target(org.springframework.stereotype.Service)
  ```
  @Service 애노테이션이 붙은 클래스의 객체가 타겟일 때 적용.

---

### 8. `@annotation`
- **설명**: 특정 애노테이션이 있는 메서드에 적용.
- **예시**:  
  ```java
  @annotation(org.springframework.transaction.annotation.Transactional)
  ```
  @Transactional 애노테이션이 있는 메서드에 적용.

---

### 9. `@args`
- **설명**: 메서드 인자가 특정 애노테이션을 포함하는 경우 적용.
- **예시**:  
  ```java
  @args(org.springframework.validation.annotation.Validated)
  ```
  메서드 인자가 @Validated 애노테이션이 붙은 객체일 때 적용.

---

### 10. `bean`
- **설명**: 특정 이름의 스프링 빈에 대해 Pointcut을 적용.
- **예시**:  
  ```java
  bean(myBean)
  ```
  이름이 myBean인 빈의 메서드에 적용.

---

## 🔧 실습을 통해 배우는 AOP 활용법

1. **Aspect 정의**:  
   ```java
   @Aspect
   @Component
   public class LoggingAspect {
       @Before("execution(* com.example.service.*.*(..))")
       public void logBefore(JoinPoint joinPoint) {
           System.out.println("Method executed: " + joinPoint.getSignature());
       }
   }
   ```

2. **Pointcut 표현식 설정**:  
   - 특정 패키지의 모든 메서드에 로깅 추가.

3. **Advisor 활용**:  
   - Pointcut과 Advice를 결합해 관리.

4. **Proxy 객체 생성**:  
   - 비즈니스 로직과 공통 기능의 분리를 통해 가독성과 유지보수성 향상.

---

## ✨ AOP의 장점
- **공통 기능 분리**: 비즈니스 로직과 공통 기능의 명확한 분리.
- **코드 중복 감소**: 공통 로직을 재사용 가능.
- **유지보수성 향상**: 코드 수정이 간단하며 가독성이 높아짐.


---

## 📌 주의 사항
- **성능 고려**: AOP는 런타임에 동작하므로 과도한 사용은 성능 저하를 유발할 수 있습니다.
- **적용 범위 제한**: 비즈니스 로직과 직접 관련되지 않은 공통 기능에만 적용.
