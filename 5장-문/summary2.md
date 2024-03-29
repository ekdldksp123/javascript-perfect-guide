# 5장 문 part.2

## 5.5 점프문

- 점프 문은 이름에서 짐작할 수 있듯 자바스크립트 인터프리터가 소스코드의 다른 위치로 이동하게 한다.
    - `break, continue, return, yield, throw`

### 5.5.1 라벨 붙은 문

- 어떤 문이든 그 앞에 다음과 같이 식별자와 콜론을 붙여 라벨을 만들 수 있다.
    
    ```tsx
    identifier: statement
    ```
    
    - 자바스크립트에서 문 라벨을 이용하는 문은 `break` 와 `continue` 뿐이다
    
    예시 (continue
    
    ```tsx
    mainloop: while(token !== null){
    		//코드 생략
    		continue mainloop;
    		//코드 생략
    }
    ```
    

### 5.5.2 break

- `break` 문은 단독으로 사용하면 자신을 포함하고 있는 가장 가까운 루프 또는 switch 문을 즉시 빠져나간다.
    
    ```tsx
    break;
    ```
    
    - 이런 형태의 `break` 문은 루프나 switch 문을 빠져나가므로 빠져나갈 문 안에 있어야만 유효하다

- 주 목적
    - 일반적으로 어떤 이유로든 루프를 더 진행할 필요가 없을 때 일찍 끝내는 용도로 사용
    
    ```tsx
    for(let i = 0; i < a.length; i++) {
    		if (a[i] === target) break;		
    }
    ```
    
- `break` 키워드 다음에 문 라벨을 붙일수 있다.
    
    ```tsx
    break labelname;
    ```
    
    - `break` 문에 라벨을 사용하면 해당 라벨이 붙은 문을 종료한다.
        - `break` 문에 라벨을 사용하는 경우는 탈출하려는 문이 가장 가까운 루프나 switch문이 아닐때다.
        
        ```tsx
        let matrix = getData(); // 숫자로 구성된 2차원 배열 생성
        
        let sum = 0, success = false;
        // 에러가 발생 했을때 빠져나갈 수 있도록 라벨 붙은 문으로 시작
        computeSum: if (matrix) {
        	for(let x = 0; x < matrix.length; x++) { 
        		let row= matrix[x];
        		if (!row) break computeSum;
        		for(let y = 0; y < row.length; y++) {
        			let cell = row[y];
        			if (isNaN(cell)) break computeSum; 
        			sum += cell;
        } }
        success = true;
        }
        ```
        
        > if (!row) break computeSum; 부분에서 자신을 감싼 for문이 아닌, 그 외부의 라벨 붙은 문을 종료 시켜 코드를 빠져나갔다.
        > 
    
- `break` 문에 붙은 라벨이 꼭 루프나 switch 문이 아니어도 된다.
    - `break` 문은 자신을 둘러싼 문이면 어떤 형태든 **빠져나갈 수 있다**
    

### 5.5.3 continue

- `continue` 문은 break와 비슷하게 루프 안에서 continue를 사용하면 루프의 다음 반복으로 넘어간다.
    
    ```tsx
    continue
    
    continue labelname;
    ```
    
    - `continue` 문은 라벨이 있든 없든 루프 바디 안에서만 사용할 수 있다.

- 인터프리터는 `continue` 문을 만나면 루프의 현재 반복을 멈추고 다음 반복으로 넘어간다. → 따라서 루프 타입에 따라 결과가 다를 수 있다.
    - while 루프
        - expression을 루프 맨 위에서 다시 평가하고, true면 루프 바디를 맨 위에서부터 실행
    - do/while 루프
        - 루프 맨 아래까지 건너 뛴 다음, 루프 조건을 다시 평가한 후 맨 위부터 재시작
    - for 루프
        - increment(증가) 표현식을 평가하고 다시 test 표현식을 평가해서 반복을 재개할 지 결정
    - for/in , for/of
        - 다음 값 또는 프로퍼티 이름이 변수에 할당된다.
        

### 5.5.4 return

- 함수호출은 표현식이고, 표현식은 모두 값이 있다.
    - `return` 문은 그 함수 호출의 반환 값을 지정한다
        
        ```tsx
        return expression;
        ```
        
    - `return` 문이 없는 함수 호출은 undefined로 평가된다.
    - `return` 문은 함수 바디 안에만 쓸 수 있다.
    

### 5.5.5 yield

- `yield`문은 return 문과 비슷하지만 **제너레이터 함수 안에서만 사용**되며 실제로 제어권을 넘기지 않고 다음값만 넘길떄 사용된다.
    
    ```tsx
    function* range(from, to){
    		for(let i = from; i<= to; i++} {
    			yield i;
    		}
    }
    ```
    

### 5.5.6 throw

- 예외 (exception)는 예외적인 조건이나 에러가 일어났다는 신호
    - `throw` 는 그런 에러나 예외적 조건이 일어났다는 신호를 보내는 것
        - 자바스크립트에서 예외는 런타임 에러가 일어났을때, 그리고 프로그램에서 직접 `throw` 문을 통해 일으켰을때 발생한다.
    
    ```tsx
    throw expression;
    ```
    
    - expression은 어떤 타입의 값으로든 평가될 수 있다.
        
        > 어떤 타입의 객체든 보낼 수 있다는 뜻
        > 

- 예외가 일어나면 자바스크립트 인터프리터는 즉시 프로그램 실행을 멈추고 가장 가까운 예외 핸들러로 점프한다.(catch)
    - 코드 블록에 연결된 catch 절이 없다면 인터프리터는 가장 가까운 코드블록의 catch를 찾는다.
        - 이를 계속 반복해서 수행하다 콜스택의 끝까지 예외 핸들러를 찾지 못한다면 예외를 에러로 간주하고 사용자에게 보고한다.

### 5.5.7 try/catch/filnally

- `try/catch/filnally` 문은 자바스크립트의 예외처리 메커니즘이다.
    - try
        - 처리하려 하는 예외가 담긴 코드블록
    - catch
        - try 블록에서 예외가 발생하면 catch 절이 호출
    - finally
        - try 블록에서 무슨일이 일어났든 관계없이 실행되는 일종의 정리 코드
    - 각 블록은 모두 중괄호에 둘러싸여 있어야한다.
    
    ```tsx
    try {
    // 문제가 없을 경우 일반적으로 이 코드는 블록 위쪽에서
    // 아래쪽으로 실행됩니다. 하지만 이 코드는 때때로 예외를 일으킬 수 있는데, 
    //throw 문을 통해 예외를 직접 일으키거나 예외를 일으키는
    // 메서드를 호출해서 간접적으로 일으킵니다.
    catch(e) {
    // 이 블록의 문은 try 블록에서 예외를 일으켰을 때만 실행될니다. 
    // 이 문은 로컬 변수 e를 사용할 수 있으며 이 변수는
    // Error 객체 또는 전달받은 값을 참조합니다
    // 이 블록은 예외를 처리할 수도 있고,
    // 아무 일도 하지 않고 무시할 수도 있으며,
    // throw를 통해 다시 예외를 일으킬 수도 있습니다.
    }
    finally {
    //이 블록은 try 블록에서 무슨 일이 있었든 항상 실행될니다. 
    //경우의 수는 다음과 같습니다
    //1) 정상적으로 try 블록의 끝에 도달한 경우
    //2) break, continue, return 문을 통해 try 블록을 빠져나가는 경우 
    //3) 위 catch 절에서 처리한 예외 때문에 try 블록이 종료된 경우 
    //4)예외가캐치되지않고계속전파되는경우
    }
    ```
    
    > 동작 순서 경우의 수
    try → finally
    try → catch → finally
    > 

---

## 5.6 기타 문

### 5.6.1 with

- with 문은 지정된 객체의 프로퍼티가 해당 블록의 스코프 안에 있는 변수인 것처럼 코드 블록을 실행한다

```jsx
with(document.forms[0) {
	// 폼 요소에 직접 접근합니다
	name.value = "";
	address.value = "";
	email.value = "";
}
```

- with 문을 사용하지 말아야 하는 이유
    - 자바스크립트 코드를 최적화 하기 어렵다
    - with 문을 사용하지 않는 동등한 코드에 비해 상당히 느리게 동작한다

### 5.6.2 debugger

- 실행 환경에 따라서 디버깅 동작을 실행할 수 있다
- 이 문은 일종의 중단점 기능을 해서 자바스크립트 코드 실행을 멈춘다
- 그러면 디버거에서 변수 값을 출력하거나 콜 스택을 살펴볼 수 있다

```jsx
function f(o) {
	if(o === undefined) debugger;
	...
}
```

### 5.6.3 “use strict”

- ES5에 도입한 지시자(directive) 이다
- 이후의 코드가 스트릭트 코드 , 즉 스트릭트 모드를 따르는 코드라는 선언이다
- “use strict” 지시자와 일반적인 문의 차이점
    - 이 지시자에는 아무런 키워드도 없다
    - 이 지시자는 스크립트나 함수 바디의 맨 처음에만 존재할 수 있고 이 앞에 실제문이 있어서는 안된다
- 명시적으로 지시자를 사용하지 않더라도 class 바디나 ES6 모듈 안에 있는 코드는 자동으로 스트릭트 코드가 된다
    - 즉 모듈로 작성한 자바스크립트 코드는 자동으로 스트릭트 모드를 따르며, 그 안에 “use strict” 지시자를 사용할 필요가 없어진다
- 스트릭트 모드는 자바스크립트의 중요한 결함을 수정하고 더 강력히 에러를 체크하며 보안을 강화한 것이다
- 스트릭트 모드와 일반 모드의 차이
    - 스트릭트 모드에서는 with 문을 허옹하지 않는다
    - 스트릭트 모드에서는 반드시 모든 변수를 선언해야 한다
        - 일반 모드에서는 전역 객체에 새 프로퍼티를 추가하는 방식으로 묵시적으로 전역 변수를 선언한다
    - 스트릭트 모드에서는 메서드가 아니라 함수로 호출된 함수의 this 값은 undefined 이다
        - 일반 모드에서 함수로서 호출된 함수의 this 는 항상 전역 객체이다
        - 또한 스트릭트 모드에서 함수를 call() 이나 apply()로 호출하면 해당 함수의 this 값은 call() 이나 apply()에 전달된 첫번째 인자이다
        - 일반 모드에서는 null 이나 undefined 값이 전역 객체로 대페되며 객체가 아닌 값은 객체로 변환된다
    - 스트릭트 모드에서는 eval()에 전달된 코드는 호출자의 스코프에 변수를 선언하거나 함수를 정의할 수 없다.
        - 대신 eval()을 위해 새로 생성된 스코프에 변수나 함수가 생성된다.
        - 이 스코프는 eval()이 종료될 때 함께 종료된다
    - 스트릭트 모드에서 함수의 arguments 객체는 함수에 전달된 값을 정적으로 복사해 유지한다
        - 일반모드에서 arguments 객체는 배열 요소와 이름 붙은 함수 매개변수가 같은 값을 참조하는 마술 같은 동작 방식을 가진다
    - 스트릭트 모드에서는 delete 연산자 뒤에 변수, 함수, 함수 매개변수 등 유효하지 않는 식별자를 사용할 때 SyntaxError가 일어난다
        - 일반 모드에서 delete 표현식을 이런식으로 사용하면 아무 일도 일어나지 않고 false로 평가된다
    - 스트릭트 모드에서는 8진수 정수 리터럴(0으로 시작하되 그 뒤에 x가 없는 리터럴)이 허용되지 않는다
        - 일반 모드에서는 일부 실행 환경에서 8진수 리터럴을 허용한다
    - 스트릭트 모드에서는 콜 스택을 살펴보는 기능이 제한된다
        - arguments.caller 와 arguments.callee는 모두 스트릭트 모드 함수에서 TypeError를 일으킨다

---

## 5.7 선언

- 자바스크립트의 선언은 상수, 변수, 함수, 클래스를 정의하고 모듈에서 값을 가져오고, 내보낼 때 사용한다

### 5.7.2 함수

```jsx
function area(radius) {
	return Math.PI * radius * radius
}
```

- 함수 선언은 함수 객체를 생성하고 이를 지정된 이름에 할당한다
- 함수 선언은 어떤 블록에 있든 해당 블록의 코드보다 먼저 처리되고, 함수 이름은 그 블록을 통틀어 함수 객체에 묶인다
    
    → 호이스팅 된다
    
    ⇒ 결과적으로 함수를 선언하는 코드보다 앞에 있는 코드에서 그 함수를 호출할 수 있다
    

### 5.7.3 클래스

```jsx
class Circle {
	constructor(radius) {
		this.r = radius
	}

	area() {
		return Math.PI * this.r * this.r
	}

	circumference() {
		return 2 * Math.PI * this.r
	}
}
```

- 함수와 달리 클래스 선언은 끌어올려지지 않으며, 선언한 클래스는 선언하기 전에는 사용할 수 없다

### 5.7.4 가져오기와 내보내기

- 한 모듈에서 정의한 값을 다른 모듈에서 사용하려면 정의한 모듈에서 export로 값을 내보내고, 사용할 모듈에서 import 해야 한다
- import 지시자는 다른 모듈에서 하나 이상의 값을 가져오고, 현재 모듈에서 사용할 이름을 부여한다
    
    ```jsx
    import Circle from './Circle.js'
    import {PI, TAU} from './contstants.js'
    import {magnitude as hypotenuse} from './utils.js'
    ```
    
- export 지시자는 때때로 다른 선언을 변경하여 상수, 변수, 함수, 클래스를 정의하는 동시에 내보내는 일종의 복합 선언을 만들수 있다
- 모듈에서 내보내는 값이 단 하나뿐일 때는 일반적으로 export default 를 사용한다
    
    ```jsx
    export const TAU = 2 * Math.PI
    export function manitude(x,y){
    	return Math.sqrt(x*x + y*y)
    }
    
    export default class Circle{...}
    ```
    

