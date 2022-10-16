# 문자열 사칙 연산 계산기
<details>
<summary>접기/펼치기</summary>

## 기능 요구사항

* 사용자가 입력한 문자열 값에 따라 사칙연산을 수행할 수 있는 계산기를 구현해야 한다.
* 입력 문자열의 숫자와 사칙 연산 사이에는 반드시 빈 공백 문자열이 있다고 가정한다.
* 나눗셈의 경우 결과 값을 정수로 떨어지는 값으로 한정한다.
* 문자열 계산기는 사칙연산의 계산 우선순위가 아닌 입력 값에 따라 계산 순서가 결정된다. 즉, 수학에서는 곱셈, 나눗셈이 덧셈, 뺄셈 보다 먼저 계산해야 하지만 이를 무시한다.
* 예를 들어 2 + 3 * 4 / 2와 같은 문자열을 입력할 경우 2 + 3 * 4 / 2 실행 결과인 10을 출력해야 한다.

### STEP1 문자열계산기 기능 요구사항 정리 
* 문자열을 입력받는 View 생성
  * [x] 공백 문자열로 구분
  * [x] 숫자와 연산자로 분리해서 반환
  * [x] 나눗셈의 경우 분모로 0을 받을 수 없음
* 계산 수행 객체
  * [x] 숫자 2개와 연산자하나를 통해 계산
  * [x] 연산자별로 다른 계산방식을 가짐
* [x] 계산 결과 출력

### 문자열 계산기 리팩터링 요구사항
* [x] try-catch 대신 예외 발생 전에 오류 잡기
* [x] BinaryOperator<> 사용해보기
* [x] 문자열계산기를 무상태 객체로 리팩터링 해보기
* [x] ConverUtil 대신 SRP를 지킬 수 있는 객체로 만들어보기
</details>

# STEP 2 : 로또(자동)
<details>
<summary>접기/펼치기</summary>

## 기능 요구사항 정리

* 로또 구입 금액을 입력하면 구입 금액에 해당하는 로또를 발급한다.

* 로또 입력 (LottoInputView.java)
  * [x] 금액을 입력받는다.
  * [x] 당첨번호를 입력받는다. 

* 로또 (Lotto.java)
    * [x] 로또 도메인 객체를 만든다.
    * [x] 로또는 6개의 숫자를 가진다.
    * [x] 현재 가진 숫자들과 당첨번호를 비교해 맞춘 갯수를 반환

* 여러 로또를 가지고 있는 객체를 생성 (LottoManger.java)
  * 로또 일급컬렉션
  * 로또 1장의 가격은 1000원
  * 로또의 가격을 관리
  * [x] 숫자는 shuffle() 메서드로 자동 생성한다.
  * [x] 여러 로또를 가짐
  * [x] 당첨번호로 여러 로또의 맞춘 갯수를 얻음
  * [x] 번 금액을 이용해 수익률을 반환하는 메서드

* 당첨통계를 계산
  * 맞춘 갯수를 입력받아 (맞춘갯수, 당첨금액)을 객체를 만듬
  * (맞춘갯수, 당첨금액, 갯수) 형태로 만들어 반환
  * 번 금액 반환하는 메서드

* 출력
  * 당첨통계 출력
  * 수익률 출력

## 프로그래밍 요구사항
* 모든 기능을 TDD로 구현
* indent depth 2 넘지 않기
* 모든 로직에 단위 테스트 (UI 제외)
* else 사용 X

## 피드백 리팩터링
* [x] 가능한 부분에 일급 컬렉션 사용
* [x] 상수/변수/생성자/메서드(public) 메서드(private) 정렬 유지
* [x] NPE 생기지 않도록 변경
* [x] 최대한 오류가 생기기전에 예외 던지기
* [x] depth 2 변경
* [x] 반복되는 System.out.println() 보다 StringBuilder 사용
</details>

# STEP 3 로또(2등)
<details>
<summary>접기/펼치기</summary>
## 로또(자동) 피드백 적용
* [x] 오타 주의
* [x] 방어적 복사 사용
* [x] 매직넘버 변경, 매직 리터럴 변경
* [x] 올바른 접근 제어자 체크
* [x] 객체의 불변성 혹은 실질적 불변성 확보해보기
* [x] 유틸리티 클래스 사용 시 생성자 제한
* [x] 생성자에 로직 넣지 않기 (테스트하기 좋은 구조로 만들기)
* [x] shuffle 후 초기 상태 유지
* [x] 굳이 객체를 다시 생성하지 않기

## 보너스 2등 요구사항 추가
* [x] 보너스 볼 입력받기
* [x] 입력받은 보너스 볼을 비교하는 로직 추가
* [x] 보너스 볼 등수 추가
</details>

# 로또(수동)
<details>
<summary>접기/펼치기</summary>

## 로또(2등) 피드백 적용
* [x] stream의 anyMatch() 활용, groupingBy() 활용
* [x] 자료구조를 항상 초기화
* [x] 객체명을 명확하게 수정
* [x] 인터페이스가 하위 구현체에 의존하지 않도록 의존성 분리
* [x] 가능한 일급 컬렉션, 원시값 포장 추가
* [x] keySet() 대신 entrySet() 비교 후 사용해보기
* [x] 상수명은 컨벤션에 맞게 작성
* [x] 가독성을 위해 String.format() 활용

## 로또(수동) 기능 요구사항
* [] 자동 이외의 수동 로또 기능 추가
  * [] 구매할 로또 번호를 입력받아서 로또 생성
* [] 자동과 수동으로 생성된 모든 로또를 관리하는 객체
  * [] 각 로또에 대한 정보를 상태로 가짐
  * [] 당첨번호와, 보너스볼 정보를 통해 맞춘 갯수를 알아냄
* [] 맞춘 갯수로 등수를 생성하는 객체
* [] 주어진 등수 정보를 출력하는 객체
</details>

  