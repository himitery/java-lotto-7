<div align="center">
	<h1>우아한테크코스 웹 백엔드 7기 프리코스</h1>
	<p>
		<b>💸 자바로 구현하는 간단한 로또 발매기 💸</b>
	</p>
	<br>
</div>

## ⚙️ 프로젝트 개발 환경

> [!NOTE]
> 우아한테크코스에서 제공된 라이브러리 이외의 외부 라이브러리는 사용하지 않는다.

- Java Development Kit 21
- Gradle

<br />

## ⛳️ 요구 사항

### 🚀 기능 요구 사항

1. 로또 번호의 숫자 범위는 1~45까지이다.
2. 1개의 로또를 발행할 때 중복되지 않는 6개의 숫자를 뽑는다.
3. 당첨 번호 추첨 시 중복되지 않는 숫자 6개와 보너스 번호 1개를 뽑는다.
4. 당첨은 1등부터 5등까지 있다. 당첨 기준과 금액은 아래와 같다.

   | 등수 |     당첨금      | 일치하는 번호 수. | 보너스 번호 일치 |
   |:----:|:---------------:|:-----------------:|:----------------:|
   |  1   | 2,000,000,000원 |        6개        |        X         |
   |  2   |  30,000,000원   |        5개        |        O         |
   |  3   |   1,500,000원   |        5개        |        X         |
   |  4   |    50,000원     |        4개        |        X         |
   |  5   |     5,000원     |        3개        |        X         |

5. 로또 구입 금액을 입력하면 구입 금액에 해당하는 만큼 로또를 발행해야 한다.
6. 로또 1장의 가격은 1,000원이다.
7. 당첨 번호와 보너스 번호를 입력받는다.
8. 사용자가 구매한 로또 번호와 당첨 번호를 비교하여 당첨 내역 및 수익률을 출력하고 로또 게임을 종료한다.
9. 사용자가 잘못된 값을 입력할 경우 `IllegalArgumentException`을 발생시키고, "[ERROR]"로 시작하는 에러 메시지를 출력 후 그 부분부터 입력을 다시
   받는다.
	- `Exception`이 아닌 `IllegalArgumentException`, `IllegalStateException` 등과 같은 명확한 유형을 처리한다.

### 🖨️ 입출력 요구 사항

**입력**

- 로또 구입 금액을 입력받는다. 구입 금액은 1,000원 단위로 입력받으며 1,000원으로 나누어떨어지지 않는 경우 예외 처리한다.

  ```bash
  14000
  ```

- 당첨 번호를 입력받는다. 번호는 쉼표(,)를 기준으로 구분한다.

  ```bash
  1,2,3,4,5,6
  ```

- 보너스 번호를 입력받는다.

  ```bash
  7
  ```

**출력**

- 발행한 로또 수량 및 번호를 출력한다. 로또 번호는 오름차순으로 정렬하여 보여준다.

  ```bash
  8개를 구매했습니다.
  [8, 21, 23, 41, 42, 43]
  [3, 5, 11, 16, 32, 38]
  [7, 11, 16, 35, 36, 44]
  [1, 8, 11, 31, 41, 42]
  [13, 14, 16, 38, 42, 45]
  [7, 11, 30, 40, 42, 43]
  [2, 13, 22, 32, 38, 45]
  [1, 3, 5, 14, 22, 45]
  ```

- 당첨 내역을 출력한다.

  ```bash
  3개 일치 (5,000원) - 1개
  4개 일치 (50,000원) - 0개
  5개 일치 (1,500,000원) - 0개
  5개 일치, 보너스 볼 일치 (30,000,000원) - 0개
  6개 일치 (2,000,000,000원) - 0개
  ```

- 수익률은 소수점 둘째 자리에서 반올림한다. (ex. 100.0%, 51.5%, 1,000,000.0%)

  ```bash
  총 수익률은 62.5%입니다.
  ```

- 예외 상황 시 에러 문구를 출력해야 한다. 단, 에러 문구는 "[ERROR]"로 시작해야 한다.

  ```bash
  [ERROR] 로또 번호는 1부터 45 사이의 숫자여야 합니다.
  ```

**실행 결과 예시**

```bash
구입 금액을 입력해 주세요.
8000

8개를 구매했습니다.
[8, 21, 23, 41, 42, 43]
[3, 5, 11, 16, 32, 38]
[7, 11, 16, 35, 36, 44]
[1, 8, 11, 31, 41, 42]
[13, 14, 16, 38, 42, 45]
[7, 11, 30, 40, 42, 43]
[2, 13, 22, 32, 38, 45]
[1, 3, 5, 14, 22, 45]

당첨 번호를 입력해 주세요.
1,2,3,4,5,6

보너스 번호를 입력해 주세요.
7

당첨 통계
---
3개 일치 (5,000원) - 1개
4개 일치 (50,000원) - 0개
5개 일치 (1,500,000원) - 0개
5개 일치, 보너스 볼 일치 (30,000,000원) - 0개
6개 일치 (2,000,000,000원) - 0개
총 수익률은 62.5%입니다.
```

<br />

## 💎 프로젝트 설계 목표

### 1. TDD(Test Driven Development)

테스트를 먼저 작성하고 이를 기반으로 코드를 구현해 나가는 소프트웨어 개발 방법론이다.

### 2. DDD(Domain Driven Development)

도메인의 핵심 개념을 중심으로 설계를 진행하는 방법론이다.

**Hexagonal Architecture(Ports and Adapters Architecture) 적용**

- 애플리케이션의 도메인을 중심에 두고, 내부 로직과 외부 의존성을 **포트**와 **어댑터**로 연결하는 구조
- 도메인 로직이 외부 의존성에 직접 접근하지 않고 포트를 통해 접근하게 되어 결합도를 낮추고 테스트 가능성을 높임

### 3. 유연한 구조

프레임워크에서 제공하는 기능들의 일부를 직접 구현하여, 낮은 결합도와 높은 응집도의 구조를 지향한다.

**IoC(Inversion of Control), DI(Dependency Injection)**

- Spring Boot에서 제공하는 `ApplicationContext`와 유사한 기능 구현한다.
	- 클래스를 찾아 빈으로 생성한다.
	- 생성한 빈을 싱글톤으로 관리한다.
	- 생성자에 필요한 빈을 자동으로 주입한다.

**Validation**

- 프록시 패턴을 활용해 인터페이스 메서드 기반의 유효성 검사 지원한다.
- 도메인의 필드 기반 유효성 검사 지원한다.

<br />

## 📒 구현할 기능 목록

### 1. 테스트를 설계한다.

> [!IMPORTANT]
> TDD(Test Driven Development) 방법론에 따라 테스트를 먼저 설계하고 작성한다.

**✅ 입력 테스트**

- [x] 로또 구입 금액
	- [x] 구입 금액은 1,000의 배수이어야 한다.
	- [x] 구입 금액은 최소 1,000원 이상이어야 한다.
- [x] 당첨 번호
	- [x] 당첨 번호는 6개의 겹치지 않은 숫자로 이루어진다.
	- [x] 각 번호는 1~45 사이의 값을 가진다.
- [x] 보너스 번호
	- [x] 보너스 번호는 1개의 숫자로 이루어진다.
	- [x] 번호는 1~45 사이의 값을 가진다.

**✅ 도메인 테스트**

- [x] 로또 구매
	- [x] 로또 구매 개수는 `구입 금액 / 1000`이다.
- [x] 로또 번호 생성
	- [x] 로또 번호는 6개의 겹치지 않은 숫자로 이루어진다.
	- [x] 각 번호는 1~45 사이의 값을 가진다.
- [x] 로또 당첨 결과 확인
	- [x] 당첨 번호가 3개 미만으로 일치하면, 꽝이다.
	- [x] 당첨 번호가 3개 일치하면, 5등이다.
	- [x] 당첨 번호가 4개 일치하면, 4등이다.
	- [x] 당첨 번호가 5개 일치하고 보너스 번호가 일치하지 않으면, 3등이다.
	- [x] 당첨 번호가 5개 일치하고 보너스 번호가 일치하면, 2등이다.
	- [x] 당첨 번호가 6개 일치하면, 1등이다.

**✅ 출력 테스트**

- [x] 구입한 로또 번호 출력
	- [x] 구입 가격에 올바른 개수의 로또를 출력한다.
	- [x] 올바른 출력 형식을 따른다. (e.g. [1, 2, 3, 4, 5, 6])
- [x] 로또 결과 출력
	- [x] 5등부터 1등까지 차례대로 당첨 수를 출력한다.
- [x] 수익률 출력
	- [x] 결과에 따라 `총 수익 / 구입 금액`을 출력한다.
	- [x] 수익률은 소수점 둘째 자리에서 반올림한다.

**✅ 예외 테스트**

- [x] 예외 상황의 경우 `IllegalArgumentException`가 발생한다.
- [x] 예외 상황의 경우 `Exception Message`가 `[ERROR]`로 시작한다.

### 2. IoC(Inversion of Control), DI(Dependency Injection) 기능을 구현한다.

> [!NOTE]
> [자바로 구현하는 간단한 레이싱](https://github.com/himitery/java-racingcar-7)에서 구현한 코드를 기반으로 리팩터링을 진행한다.

- [x] 기존 클래스의 역할을 더욱 작게 쪼개는 것을 고려한다.
- [x] 일급 컬렉션을 적극적으로 활용한다.
- [x] 메서드의 이름을 더욱 명확히 할 수 있도록 노력한다.
- [x] 메서드의 기능을 최대한 작게 만든다.
  - 메서드의 길이는 최대한 15 이하가 되도록 한다.

### 3. 유효성 검증 기능을 구현한다.

> [!NOTE]
> [자바로 구현하는 간단한 레이싱](https://github.com/himitery/java-racingcar-7)에서 구현한 코드를 기반으로 기능 추가 및 리팩터링을
> 진행한다.

- [x] 더욱 다양한 유효성 검사를 지원한다.
  - `Max` 유효성 검사 기능 추가
  - `Divisible` 유효성 검사 기능 추가
  - `Unique` 유효성 검사 기능 추가
- [x] 메서드의 기능을 최대한 작게 만든다.
  - 메서드의 길이는 최대한 15 이하가 되도록 한다.

### 4. 도메인 로직을 구현한다.

**✅ 사용자로부터 입력을 받고 입력값을 검증한다.**

`amp.nextstep.edu.missionutils`에서 제공하는 `Console`을 활용한다.

- [x] 로또 구입 금액을 입력받고, 도메인 제약사항에 부합하는지 검증한다.
- [x] 로또 당첨 번호를 입력받고, 도메인 제약사항에 부합하는지 검증한다.
- [x] 로또 보너스 번호를 입력받고, 도메인 제약사항에 부합하는지 검증한다.

**✅ 로또를 생성한다.**

- [x] 구입 가격에 맞는 로또 개수를 생성한다.
	- Random 값 추출은 `camp.nextstep.edu.missionutils.Randoms`의 `pickUniqueNumbersInRange()`를 활용한다.
- [x] 생성된 로또 번호가 도메인 제약사항에 부합한 지 검증한다.
- [x] 생성된 로또 번호를 출력한다.

**✅ 로또 결과를 확인한다.**

- [x] 당첨 번호와 보너스 번호를 토대로, 로또의 등수를 반환한다.
- [x] 등수 별로 당첨된 개수를 출력한다.
- [x] 구입 금액 대비 수익률을 출력한다.
