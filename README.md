# **🔥Node 공부🔥**

----------

아래 내용은 Node에 대해 핵심적으로 알아야 할 내용들을 찾아 공부하며, 이해한 내용을 최대한 자세하고 정확하게 가공하여 기록하였다. 

주로 Node.js 교과서의 저자인 조현영(ZeroCho)님의 유튜브 교육 방송 중 노드 교과서 개정판에 대한 것을 뼈대로 하여 내용에 조금씩 살을 붙여 작성되었다.

첨부한 이미지들 또한 대부분 노드 교과서 책을 캡처한 것이다. 

---------

## #1 노드에 대한 이해

**Node?**

> 1. 공식 홈페이지에서는 노드를 **크롬 V8 자바스크립트 엔진으로 빌드된 JS 런타임**이라고 정의하고 있다. 간단하게 말하면 노드는 **JS** **실행기**이다. 그럼 노드가 없었을 때는 JS를 실행하지 못했을까? 원래 JS는 HTML 파일 안에서 스크립트 태그로 포함되고 브라우저에서 실행되어 왔다. 즉, **초기의 JS는 브라우저와 HTML에 종속되어 능동적으로 무언가를 하는 데 많은 제약**이 있었다. 그런데 Node가 개발되고 JS는 그러한 종속성으로부터 완전히 해방된다. 이것과 더불어 크롬이 나오고 JS 코드를 빠르게 실행시킬 수 있게 되면서 특히 웹 개발을 하는 실무에서 많은 지지를 받는다. 
>
> 2. 개발자 비중에서 웹 개발자가 가장 많은데, 웹 개발자는 프론트엔드에 쓰이는 언어가 JS뿐이라서 JS를 당연히 다룰 수밖에 없다. 이 말은 곧 JS 개발자가 가장 많다는 말과 같다. 사람은 기본적으로 귀찮음을 느끼기 때문에 ‘한 언어로 모든 것을 할 수 없을까?’라는 생각을 한다. 이러한 생각을 현실로 만들어주는 것이 바로 Node이다. 
>
> 3. Node를 잘 모르는 사람들은 Node를 서버라고 생각한다. 그것은 틀린 말이고 단지 서버를 생성하고 실행하고 처리를 하도록 코딩되어 있는 JS코드를 실행시켜주는 일을 하는 것일 뿐이다. 
>
> 4. 노드는 C++로 구현된 V8과 libuv를 내부적으로 포함하고 있다. V8은 오픈 소스 JS 엔진이며 JS의 속도 문제를 개선해준다. 또한 libuv는 노드의 특성인 이벤트 기반, 논 블로킹 I/O 모델을 구현한 라이브러리인데, 이 libuv로 인해 비동기 I/O 처리가 가능하게 됐다. JS는 싱글 스레드와 비동기 I/O 모델을 택하였고 프로그래밍 난이도도 Java처럼 멀티 스레드를 구현하는 것만큼 어렵지 않고 쉽고 처리 속도도 엄청나게 빠르다. 그래서 Node가 초보자가 입문하기에도 비교적 편한 장점이 있다. 

**Node의 특성?**

> 1. **이벤트 기반**: 이벤트가 발생할 때 미리 지정해둔 작업을 수행하는 방식.
>
>    어떤 이벤트에 연관된 이벤트 리스너에 콜백함수를 등록해두고 그 이벤트가 발생하면 이벤트 리스너가 감지하여 해당 이벤트 처리를 위해 콜백 함수를 호출하게 된다.
>
>    그냥 너무 당연한 이야기를 하는 것이기 때문에 어렵게 받아드리지 않아도 되는 것이다. Node만 그런 것이 아니라 대부분 갖는 특성이다. 기본적인 특성이라고 보면 된다.
>
> 2. **논 블로킹**: 오래 걸리는 작업(I/O작업(파일 시스템 접근, 네트워크 요청), 압축, 암호화 등)을 백그라운드로 보내서 다음 코드가 먼저 실행되게 하고, 나중에 오래 걸리는 작업을 실행. 반면 그런 작업이 아닌 경우에는 블로킹 방식으로 실행된다. 논 블로킹과 함께 다니는 용어는 비동기이다. 
>
> 3. **싱글 스레드**: 노드 프로세스는 멀티 스레드로 이루어져 있지만 사람이 컨트롤 할 수 있는 스레드는 하나이기 때문에 싱글 스레드라고 표현. 주로 멀티 스레드 대신 멀티 프로세스 활용(I/O 작업이 많을 때). 14버전부터 멀티 스레드 사용이 가능해졌다.
>
>    싱글 스레드이기 때문에 동시성이 없다. 프로그램 기능 및 효율면에서 멀티 스레드로 되어 있는 것이 동시성을 갖기에 사용자에게 있어 무조건 좋지만 개발하는 사람의 입장에서 멀티 스레드를 개발하는 일은 매우 힘든 일(빡쌘 코딩)이다. 그래서 Node에서는 그냥 싱글 스레드를 택하여 프로그램이 한 번에 한 가지 일에 집중하도록 하며 개발자의 부담을 줄여줬다. 그래도 안 하는 것과 못하는 것은 다른데, Node는 멀티 스레딩을 못했지만 14버전 부터는 멀티 스레드를 다룰 수 있게 기능을 확장시켰다. 그냥 없어서 아쉬우니 추가된 기능일 뿐 배워서 써먹을 일은 없다. 

**Node의 역할?**

>  **서버의 역할을 할 수 있는 Node의 장단점**
>
>  ![K-001](https://user-images.githubusercontent.com/52457180/90981680-6aa44c80-e59d-11ea-819f-08dcdbc757aa.jpg)
>
>  - CPU 작업을 위해 AWS Lambda나 Google Cloud Functions 같은 별도 서비스를 사용한다. Node는 JS 런타임이기 때문에 용도가 서버에만 한정되지 않고 웹, 모바일, 데스크탑 애플리케이션에 모두 사용될 수 있다. 

- [x] 중간메모
  - 동기를 이해하려면 실행 컨텍스트(호출 스택, this, scope)를 알아야 하고, 비동기를 이해하기 위해서는 이벤트 루프를 알아야 한다.
  - 자바스크립트에서 가장 중요한 이론적인 개념은 실행 컨텍스트, 이벤트 루프, 프로토타입이다.

**호출 스택? 백그라운드? 태스크 큐? 이벤트 루프**

> ![K-002](https://user-images.githubusercontent.com/52457180/90985100-90891b80-e5b4-11ea-8244-2eebce233344.jpg)
>
> 1. 자바스크립트로 만들어진 프로그램이 실행되면서 **V8 엔진의 호출 스택**에는 가장 아래에 기본적으로 anonymous라는 가상의 전역 컨텍스트가 쌓인다. 그 위에 **동기적**(위에서 아래로 순서대로)으로 호출된 순서대로 함수가 쌓이고 함수가 끝나면서 빠지게 된다. 만약 함수가 끝나기 전에 그 안에서 또 다른 함수를 호출한다면 호출 스택에 처음 호출한 함수 위에 새로 부른 함수가 쌓이며 늦게 호출한 함수가 끝나야 일찍 호출한 함수가 스택에서 빠져나올 수 있다.
>
> 2. 자바스크립트에서 비동기적으로 일을 처리할 수 있도록 만들어 놓은 함수(대표적으로 setTimeout())들이 있는데, 그러한 함수들은 브라우저나 NodeJS(**JS 구동 환경**)에게 web apis의 이벤트(타이머)를 요청한 후 바로 스택에서 제거된다.(이 과정에서 소스코드 끝이면서 스택 가장 아래에 anonymous만 있다면 anonymous도 빠져나와 빈 상태가 됨.) 그러한 구동 환경에 의해 백그라운드에서 요청했었던 특정 비동기 api(타이머)의 작업이 완료되면 등록시켰던 콜백 함수를 **태스크 큐**(콜백 함수들이 대기하는 큐(FIFO) 형태의 배열)에 추가시켜 대기시킨다.
>
> 3. 대기하고 있던 콜백 함수들은 호출 스택이 완전히 빈 상태가 될 때 까지 대기를 한다. 빈 상태가 되면 그제서야 **이벤트 루프**에 의해 호출 스택으로 옮겨져(태스크 큐에서 대기 중이던 우선 순위가 높은 것이 먼저 빠져 나간다. 예를 들면 promise) 동기적으로 일이 처리된다. 
>
> 4. 이런 식으로 이벤트 루프는 '**현재 실행중인 태스크가 없는지**'와 '**태스크 큐에 태스크가 있는지**'를 반복적으로 확인한다.
> 5. 예제
>
>    ```javascript
>    function oneMore() {
>     console.log("one more");
>    }
>    function run(){
>     console.log("run run");
>     setTimeout(() => {
>         console.log("wow");
>     }, 0);
>     new Promise((resolve) => {
>         resolve("hi");
>     }).then(console.log);
>     oneMore();
>    }
>    setTimeout(run, 5000);
>    ```
>
>    ```console
>    실행결과:
>    run run
>    one more
>    hi
>    wow
>    ```

- [x] 중간메모**(중요)**
  - Promise에서 then 전은 호출 스택에서 동기적으로 처리되고 then 이후는 백그라운드로 넘어가 비동기적으로 작업을 처리한다.
  - 백그라운드에서 동시에 실행된다고 했는데, 어? 자바스크립트는 싱글 스레드인데 무슨 말이지? 하고 의문이 생길 수 있다. 실제로 V8과 같은 자바스크립트 엔진은 단일 호출 스택(Call Stack)을 사용하며, 요청이 들어올 때마다 해당 요청을 순차적으로 호출 스택에 담아 처리할 뿐이다. 그렇다면 비동기 요청은 어떻게 이루어지며, 동시성에 대한 처리는 누가 하는 걸까? 바로 이 자바스크립트 엔진을 구동하는 환경, 즉 브라우저나 Node.js가 담당한다.
  - 백그라운드(Web APIs)와 태스크 큐는 다른 언어(C++)로 구현되어 있다. 노드의 구성 요소인 libuv가 백그라운드나 태스크 큐에서의 일처리를 할 수 있도록 지원한다. 따라서, 싱글 스레드의 특성을 갖는 Node의 특성을 어기는 것이 아니라 다른 언어로 만들어진 것들에 의해 마치 멀티 스레드인 것처럼 동작한다. 그래서 동시성을 갖는 것처럼 보이고 JS 자체에는 동시성이 없다. 이런 동시성과 밀접한 개념이며 용어인 이벤트 루프를 이해해야 한다. 자바스크립트는 이 이벤트 루프를 이용해 비동기 방식으로 동시성을 지원한다. 
  - libuv가 바로 이벤트 루프를 제공한다고 보면 된다. 정리하면, V8은 비동기 작업을 위해 Node.js의 API를 호출하며, 이 때 넘겨진 콜백은 libuv의 이벤트 루프를 통해 스케쥴되고 실행된다.
  - 자바스크립트가 '단일 스레드' 기반의 언어라는 말은 '자바스크립트 엔진이 단일 호출 스택을 사용한다'는 관점에서만 사실이다. 실제 자바스크립트가 구동되는 환경(브라우저, Node.js등)에서는 주로 여러 개의 스레드가 사용되며, 이러한 구동 환경이 단일 호출 스택을 사용하는 자바 스크립트 엔진과 상호 연동하기 위해 사용하는 장치가 바로 '이벤트 루프'인 것이다.
  - 전역 환경에서 실행되는 코드는 한 단위의 코드블록으로써 가상의 익명함수로 감싸져 있다고 생각하는 것이 좋다. 따라서 위의 코드의 첫 줄이 실행될 때에 호출 스택의 맨 아래에 익명 함수가 하나 추가되며, 마지막 라인까지 실행되고 나서야 스택에서 제거된다.
  - `setTimeout` 뿐만 아니라 브라우저의 다른 비동기 함수들(`addEventListener`, `XMLHttpRequest`… )이나 Node.js의 IO 관련 함수들 등 모든 비동기 방식의 API들은 이벤트 루프를 통해 콜백 함수를 실행한다.
  - Node.js의 비동기 API들은 **중첩된 콜백 호출에 대한 에러 처리**를 위해 '**첫 번째 인수는 에러 콜백 함수**' 라는 컨벤션을 따르고 있다
  - 아까 Promise의 then은 우선 순위가 높아 먼저 실행된다고 했는데, 좀 더 자세하게 말해보면 promise에 의한 콜백 함수는 일반 태스크 큐에 추가되지 않고 별도의 **마이크로 태스크 큐**에 추가된다. 그리고 이벤트 루프는 코드의 실행이 끝나면 가장 먼저 마이크로 태스크 큐가 비어있는지 확인 후 있다면 호출 스택으로 옮겨 먼저 실행시키고 나중에 다 빈 것을 확인 한 후에 일반 태스크 큐에 있는 것을 호출 스택으로 옮겨 실행시킨다. 

-----

## **#2 JavaScript 문법**

**var, const, let ?**

 > 1. ES2015 이전에는 var로 변수를 선언했었다. 이후부터는 const와 let으로 대체되는데, 가장 큰 차이는 함수 스코프에서 블록 스코프로 바뀌었다는 것이다.
 > 2. const와 let의 공통점은 var와 다르게 **변수 재선언 불가능**이다. 차이점은 변수의 재할당 가능(immutable) 여부이다. let은 변수 재할당이 가능하지만 const는 재할당 또한 불가능하다. 또한, let은 선언 후 나중에 값을 할당해도 되지만 const는 더 엄격하게 변수 선언 동시에 값을 할당해줘야 한다. 어긴다면 에러가 발생한다.
 > 3. 그런데 만약 const에 객체를 할당했다면, 객체의 어떤 속성의 값을 바꾸는 것은 가능하다. 
 > 4. 기본적으로 변수 선언할 때 const로 하는 것이 안전하고 좋다고 한다. 판단은 순간순간 개발자 자신이 판단하자. 

**템플릿 문자열, 객체 리터럴**

> 1. 문자열을 ' 이 아닌 `(일명 빽틱) 로 감싸고 그 사이에 변수를 ${ } 로 감싸 포함시키는 것을 **템플릿 문자열**이라고 부른다. 
> 2. 객체 리터럴 문법이 좀 더 간결해졌다. 
>    - 객체의 메서드에 function을 붙이지 않아도 된다.
>    - 속성명과 값의 이름이 동일하다면 : 로 굳이 표현하지 않고 단어 하나만 적는다.
>    - [변수 + 값]으로 객체의 속성명을 동적으로 지정할 수 있다.

**화살표 함수**

> 1. 만약 중괄호 다음에 바로 return해주는 코드가 있는 화살표 함수라면, 중괄호를 써지지 않고 리턴 값만 표시해줘도 된다.
>    - 여기서 주의할 것이 있다. 바로 {}로 감싸진 객체를 리턴할 때 인데, 중괄호를 생략해도 된다고 했다고 그냥 생략하고 끝을 내면 안 된다. 왜냐면 해석을 못한다. 함수의 중괄호인지 객체를 표현하는 중괄호인지 모른다. 
>
> ```javascript
> const obj = (x, y) => {
> return {x, y};
> }
> // 변경 후
>
> const obj = (x, y) => ({x, y});// 객체는 마찬가지로 함수의 중괄호를 생략해도 되지만 소괄호로 한번 감싸줘야 한다. 
>```
>
> 2. 화살표 함수가 생겼는데 function 함수를 여전히 사용해야 하는 이유는 this라는 것 때문이다. function 함수는 this를 따로 갖지만, 화살표 함수는 부모의 this를 물려받는다. 이런 차이점을 이용해 자기만의 this를 가질 필요가 있는 경우에 function을 이용한다. 그러한 경우는 아래 예를 작성했다.
>
> ```javascript
> button.addEventListener("click", function() => {
>	console.log(this.textContent); // 버튼에 적혀있는 텍스트를 콘솔에 찍으려고 할 때 화살표 함수가 아닌 function 함수를 사용한다. 
>});
>
> // 하지만 화살표 함수로 가능하긴 하다. e를 매개변수로 보내는 방법이다. 
> button.addEventListener("click", function(e) => {
>	console.log(e.target.textContent); 
> });
> ```
>
> 3. 따라서, this를 쓸 일이 있다면 function을, 그게 아니라면 다 화살표 함수를 사용하면 된다.
>

**비구조화 할당(구조 분해 할당)?**

> 1. ```javascript
>     // 객체
>     // 구조 분해 할당 전
>     const ex = { a: 123, b : { c: 135, d: 146}};
>     console.log(ex.a);
>     console.log(ex.b.d);
>
>     // 구조 분해 할당 후
>     const {a, b: { d }} = ex;
>     console.log(a);
>     console.log(d);
>
>     // 배열
>     // 구조 분해 할당 전
>     const arr = [1, 2, 3, 4, 5];
>     const x = arr[0];
>     const y = arr[1];
>     const z = arr[4];
>
>     // 구조 분해 할당 후
>     const [x, y, , , z] = arr;
>
>    ```
> 
> 2. 주의할 것으로 객체 내에 this를 사용되고 있는 함수를 속성으로 갖고 있다면 구조 분해 할당을 하지 않는 것이 좋다. 문제를 일으킨다. 

**클래스와 상속?**

> 1. 사실 클래스는 프로토타입인데, 그 프로토타입 문법을 좀 더 깔금하게 작성할 수 있도록 클래스 문법을 도입하였다. Constructor와 extends 등을 깔끔하게 처리할 수 있게 됐고 코드가 그룹화되어 가독성이 향상됐다. 
> 2. 원래는 클래스를 코딩할 때, 이해하기 어려운 표현 방식으로 생성자 메서드, static 메서드, 인스턴스 메서드 등이 연관성이 없는 것처럼 따로 작성되어 왔다. 상속할 때도 엄청 알아보기 힘든 구조로 작성해야 했다. 
>

**Promise와 async/await?**

> 1. promise에 대해 간단하게 설명하자면, 내용이 실행은 되었지만 결과는 아직 반환되지 않은 객체라고 할 수있다. 결과 값을 promise가 가지고 있다가 원하는 타이밍에 then()이나 catch()를 만나 결과를 반환하여 다른 일을 진행하게 할 수 있다. 
>
> 2. 콜백 헬이라고 부르는 지저분한 자바스크립트 코드의 해결책이다.
>
> 3. resolve(성공리턴값) -> then으로 연결
>
>    reject(실패리턴값) -> catch로 연결
>
>    finally 부분은 무조건 실행됨.
>
> 4. promise.all(배열): 여러 개의 프로미스를 동시에 실행
>
>    - 하나라도 실패하면 catch로 감.
>    - promise.allSettled로 실패한 것만 추려낼 수 있다. 요즘엔 all 안 쓰고 이걸 쓴다.
>
> 5. 콜백 헬의 문제점을 보완한 것이 promise인데, 이것 또한 프로미스 헬이 생길 수 있다. 그래서 async/await을 사용하여 한 번 더 축약하여 코딩이 더욱 편해졌다.
>
> 6. 비동기 처리하는 메서드를 호출할 함수 선언 앞에 async를 붙여주고, 그 비동기 처리를 하는 메서드 호출 앞에 await을 붙여 주어 그 함수의 결과 값을 받아와 사용할 수 있다.
>
> 7. 조금 안 좋은 것은 await으로 resolve의 결과만 받아올 수 있기 때문에 reject의 결과는 모른다. 따라서 무조건 try/catch 구문으로 감싸주어 reject에 대한 것은 catch에서 처리해준다. 
>
> 8. 프로미스 배열에 대해 await과 for으로 각각 프로미스의 then 결과를 출력할 수 있다. 
>
>    (이 프로미스 반복문은 나중에 좀 더 자세히 알아보고 이정도만...)
>

**프론트엔드 자바스크립트(주로 브라우저에서 서버로 요청)**

> 1. 예전에 서버로 요청을 보내는 코드를 작성할 때, 라이브러리 없이 브라우저가 지원하는 XMLHttpRequest 객체를 이용했었다.
>
> 2. 하지만 요즘에는 **AJAX 요청을 위해 Axios 라이브러리를 사용**하고 있다. Axios는 IE에서도 문제없이 잘 돌아가고 JSON을 처리를 하는 코드도 짧기 때문에 다른 것(ex. fetch) 보다 더 좋다. 
>
>    ```html
>    // 브라우저에서의 axios 사용법 (node에서의 사용법은 조금 다름.)
>    // html 파일 내에 다음과 같이 작성하고 사용.
>    <script src="http://unpkg.com/axios/dist/axios.min.js"></script>
>    <script>
>    	// 처리할 내용(GET, POST 요청 등)
>    </script>
>    ```
>
> 3. GET 요청 보내기
>
>    - axios.get 함수의 인수로 요청을 보낼 URI 주소를 입력한다. 
>    - 서버 요청은 비동기적으로 일어난다. 즉, 프로미스 기반이라 async/await을 사용하여 표현할 수 있다.
>
> 4. POST 요청 보내기
>
>    - axios.post 함수의 인수로 요청을 보낼 URI 주소와 서버로 보낼 데이터를 입력한다.
>
> 5. FormData 객체
>
>    - 보통 이미지 또는 파일, 동영상 업로드 할 때 많이 사용된다.
>    - axios로 서버에 위와 같은 데이터를 전송할 때, FormData 객체를 생성하여 내용물을 채워 주고 그 FormData 객체를 axios.post에 인수로 입력시킨다.
>
> 6. encodeURIComponent와 decodeURIComponent
>
>    - 서버로 요청을 보내는 브라우저 쪽에서 axios로 URI 주소를 넣어줄 때, 그 주소에 만약 한글이 포함되어야 한다면 한글로 인한 문제를 없애주기 위해 사용하는 것들이다. `(빽틱)으로 URI 전체를 감싸주고 중간에 한글이 들어가야 하는 위치에 ${encodeURIComponent('한글')}을 삽입시킨다. 
>    - 반대로 요청을 받는 서버 쪽에서는 decodeURIComponent를 사용하여 이상한 아스키 코드로 변환된 한글을 다시 어떤 한글인지 해석해낼 수 있다. 
>
> 7. html 태그 안에 데이터를 저장하는 방법 = data attribute와 dataset의 이용
>
>    - 서버의 데이터를 프런트엔드로 내려줄 때 사용한다. 쉽게 말하면, html과 js 간의 데이터 교환을 하고 싶을 때 사용한다.
>    - 어떤 태그의 속성명으로 data-id로 정하고 값을 할당해놓았다면, 자바스크립트에서 태그.dataset.id으로 접근 가능하다. data-user-job -> dataset.userJob
>    - html 태그에 데이터가 저장되는 것이므로 공개되어도 상관이 없는 것들을 위해 사용하자.

- [x] 중간메모
  - 요즘에는 URL보다 URI를 많이 말한다. URL은 서버에 있는 파일 위치를 말하고, URI는 서버에 있는 자원의 위치를 말한다. 파일보다는 자원의 중요성이 커서 그렇다.

**REPL 환경에서 JS 실행하기**

> 1. 자바스크립트는 스크립트 언어라서 즉석에서 코드를 실행할 수 있다.
> 2. REPL = R(read) + E(evaluate) + P(print) + L(loop)
> 3. 명령 프롬포트에 JS 코드를 한 줄 씩 입력하여 실행할 수 있는 환경이다.
> 4. 간단한 작업을 할 때 쓴다.

**JS 파일을 모듈로 만들기**

> 1. 노드는 자바스크립트 코드를 모듈로 만들 수 있다.
>    - 모듈: 특정한 기능을 하는 함수나 변수들의 집합
>    - 모듈로 만들면 여러 프로그램에서 재사용 가능.
> 2. 다른 파일에서 사용할 수 있도록 **module.exports =** 로 변수, 함수 또는 객체를 전달할 수 있다. 
> 3. 반대로 다른 파일에 있는 변수를 사용하고자 할 때는 **require()**로 import하여 값을 받아 구조 분해 할당을 통해 변수를 사용한다. 
> 4. 이제는 좀 더 간단해져서 **require 대신 import**을, **module.exports 대신** **export default**를 쓰는 것으로 바뀐다.
> 5. 자세히 들여다보면 각각 당장은 1:1 대응되는 것은 아니니 조심은 해야 한다. 
> 6. 노드에서의 지원은 **module.exports =** 와 **require()**이다. 이러한 것들은 노드 내부에 탑재되어 있기 때문에 그냥 불러서 사용하면 된다. 그래서 JS 파일을 실행할 때 오류없이 실행되는 것이다. 

------

## **#3 노드 내장 객체**

**global**과 **console, 타이머?**

> 1. 이것들은 모두 **노드 내장 객체**이다. 
> 2. **global**
>    - 노드의 전역 객체(브라우저에서는 비슷한 것으로 window 객체가 있다. -> 이제는 **globalThis**로 통합됨.)
> 3. **console**
>    - 콘솔에 특정 결과를 print한다.
>    - console.log(): 평범한 로깅
>    - console.dir(): 객체를 로깅할 때 유용하다.
>    - console.time('아무거나') ~ console.timeEnd('같은내용'): 사이의 실행 시간을 측정한다. 
>    - console.error(): 에러 로깅
>    - console.trace(): 호출스택 로깅
> 4. **Timer method**
>    - setTimeout(콜백, 밀리초): 주어진 밀리초 동안 백그라운드에 머무르다 시간이 되면 태스크 큐로 콜백을 옮김.
>    - setInterval(콜백, 밀리초): 주어진 밀리초 마다 콜백 함수를 태스크 큐로 옮김.
>    - setImmediate(콜백): 콜백 함수를 즉시 태스크 큐로 옮김.
>    - 각자의 clear 메서드로 중간에 취소 가능. (변수명을 입력으로 받음.)

______**filename**, ______**dirname** **??**

> 노드는 브라우저와 다르게 우리의 컴퓨터에 접근을 할 수가 있다.
>
> - __filename: 현재 파일 경로
>
> - __dirname: 현재 폴더 경로

**module.exports? exports?**

> ```javascript
> // 하나만을 모듈로 만들고 싶다.
> module.exports = 함수 또는 변수;
> 
> // 여러 개를 모듈로 만들고 싶다.
> exports.a = a;
> exports.b = b;
> 
> // 또는
> module.exports = {
>     a,
>     b,
> }
> ```
>
> - 만약 exports로 먼저 썼다면 계속 exports로 해주어야 한다. 어기고 module.exports를 사용하는 순간 앞서 exports했던 것들이 무시된다.
>
> - 최초의 상태는 module.exports === exports === {} (빈 객체)라고 한다.

**this**

> 1. 노드에서 this를 사용할 때 주의점
>    - 최상위 스코프의 this는 module.exports를 가리킴
>    - 그 외에는 브라우저의 자바스크립트와 동일
>    - 함수 선언문 내부의 this는 global 객체를 가리킴. 
>    - 반면 함수 밖의 this, 즉 전역 스코프의 this는 빈 객체를 반환.

**require()**

> - require가 제일 위에 올 필요는 없음. but import 는 제일 위에 와야 함.
> - require.cache에 한 번 require한 모듈에 대한 캐싱 정보가 들어 있음.
> - require.main은 노드 실행 시 첫 모듈을 가리킴.
> - require.main === module
> - 순환 참조가 발생할 수 있는데, 노드에서 그러한 상황을 막아 준다.

**process**

> 1. 노드는 운영체제에도 접근이 가능하다. 노드를 실행하면 프로세스 하나가 실행되는데, node process 로 확인이 가능하다. 현재 실행중인 노드 프로세스의 정보를 담고 있는 것을 볼 수 있다.
>
> 2. process.env?
>    - 시스템 환경 변수들이 들어 있는 객체
>      1. 비밀키(데이터베이스 비밀번호, 서드파티 앱 키 등)를 보관하는 용도로 쓰임.
>      2. 자바스크립트 코드 상에서 process.env를 통해 접근이 가능하다. 
>      3. 일부 환경 변수는 노드 실행 시 영향을 미침.
> 3. process.nextTick()?
>    - 이벤트 루프가 다른 콜백 함수들 보다 nextTick의 콜백 함수를 우선적으로 처리함.
>    - 비슷한 경우로 promise가 있다. 
>    - setImmediate, setTimeout 보다 promise와 nextTick이 먼저 실행된다.

-------

## **#4 노드 내장 모듈**

**os**

> 1. 따로 모듈을 만들어주지 않아도 require()로 그냥 불러와서 사용할 수 있다.
> 2. 메서드 
>    - os.cpus(): 컴퓨터의 코어 정보를 보여준다.
>    - os.freemem(): 사용 가능한 메모리(RAM)를 보여준다.
>    - os.totalmem(): 전체 메모리 용량을 보여준다.

**path**

>1. 경로 처리할 때 사용됨. (윈도우는 \, POSIX는 /로 구분)
>
>2. ```javascript
>    const path = require("path");
>    ```
>
>  // 둘다 마지막에 절대 경로가 포함되어 있다. 각각 차이가 있다.
>  console.log(path.join(__dirname, "..", "/var.js"));
>  console.log(path.resolve(__dirname, "..", "/var.js"))
>  ```
>
>  ```
>  C:\~~~\var.js -> 절대 경로를 무시하고 앞의 주소와 붙여 준다.
>  C:\var.js -> 앞의 주소는 무시하고 절대 경로만을 표시해준다.
>  ```
>  
>  - join과 resolve의 차이: resolve는 /를 절대경로로 처리, join은 상대경로로 처리
>  - \\\와 \\의 차이: \\는 윈도 경로 구분자, \\\는 자바스크립트 문자열 안에서 사용(\\가 특수문자라 \\\로 이스케이프 해준 것)
>  - 윈도에서 POSIX path를 쓰고 싶다면: path.posix
>  ```

**URL (searchParam, queryString)**

> 1. 인터넷 주소를 쉽게 조작하도록 도와주는 모듈
>
> 2. url 처리에 크게 두 가지 방식이 있음 - 둘 다 잘 쓰임
>
>    - 노드 방식(기존) - url.parse(주소)를 이용
>    - WHATWG 방식(요즘) - new URL(주소)를 이용
>
>    ![K-002](https://user-images.githubusercontent.com/52457180/91333393-81021080-e808-11ea-86c5-32d363b3f9c5.jpg)
>
>    
>
> 3. ex)
>
>    ![K-003](https://user-images.githubusercontent.com/52457180/91334020-58c6e180-e809-11ea-8b88-1ab2357ead1e.jpg)
>
>    ![K-004](https://user-images.githubusercontent.com/52457180/91334535-194cc500-e80a-11ea-9f5e-2cf568111179.jpg)
>
>    - WHATWG에만 username, password, origin, **searchParams** 속성이 있다.
>
>    - 반면, 노드 방식은 username과 password 대신 auth 속성이 있고, searchParams 대신 **query**가 있다. 
>
> 4. **searchParams**
>
>    - WHATWG 방식에서 쿼리스트링(search) 부분 처리를 도와주는 객체
>    - 쿼리스트링 부분이 문자열이기 때문에 객체로 바꿔줌.
>    - new URL(주소).searchParams.toString():  조작한 searchParams 객체를 다시 문자열로 만든다.
>    - 그 외, 여러가지 유용한 메서드를 갖는다.
>
> 5. **querystring**
>
>    - 기존 노드 방식에서는 쿼리스트링을 querystring 모듈로 처리
>    - querystring.parse(쿼리): url의 uqery 부분을 자바스크립트 객체로 분해한다.
>    - querystring.stringify(객체): 분해된 query 객체를 문자열로 다시 조립한다.

**crypto** (단방향 암호화)

> 암호화하는 것은 워낙 CPU를 잡아 먹기 때문에 멀티스레드로 돌아간다.
>
> 1. 암호화는 가능하지만 복호화는 불가능
>
> 2. 단방향 암호화의 대표 주자는 해시 기법
>
>    - 문자열을 고정된 길이의 다른 문자열로 바꾸는 방식
>
> 3. Hash 사용하기 (sha512)
>
>    - createHash(알고리즘): 사용할 해시 알고리즘을 넣어준다.
>
>      - md5, sha1, sha256, sha512 등이 가능하지만, md5,, sha1은 취약점이 있다.
>
>      - 현재는 sha512로 충분하다.
>
>    - update(문자열): 변환할 문자열을 넣어준다.
>
>    - digest(인코딩): 인코딩할 알고리즘을 넣어준다.
>
>      - base64, hex, latin1이 주로 사용되는데, 그중 base64가 결과 문자열이 가장 짧아 애용된다. 
>      - 결과물로 변환된 문자열을 반환한다.
>
>    ![K-005](https://user-images.githubusercontent.com/52457180/91337075-d1c83800-e80d-11ea-90fc-8ac47999c1ae.jpg)
>
>    - createHash에 들어가는 알고리즘 = pbkdf2
>
>      - 현재는 pbkdf2나 bcrypt, scrypt 알고리즘이 쓰인다.
>      - Node에서는 pbkdf2와 scrypt를 지원한다.
>
>      ![K-006](https://user-images.githubusercontent.com/52457180/91339042-dc380100-e810-11ea-89d0-d4978d825148.jpg)
>
>      - crypto.randomByes로 64바이트 문자열 생성 -> salt 역할
>      - pbkdf2 인수에 순서대로 비밀번호, salt, 반복 횟수, 출력 바이트, 알고리즘(sha512) 를 넣어준다.
>      - 반복 횟수를 조정해 암호화하는 데 1초 정도 걸리게 맞추는 것이 권장된다.
>
>      ![K-007](https://user-images.githubusercontent.com/52457180/91339394-5e282a00-e811-11ea-905a-63832e38a945.jpg)
>
>      - 콘솔에서 salt와 password에 해당하는 것은 DB에 둘 다 저장시켜 관리해주어야 한다.

**양방향 암호화** (복호화가 가능) 

> 대칭형 암호화
>
> - key라는 것이 사용됨 
> - 암호화할 때와 복호화할 때 같은 key를 사용해야 함.
> - Node 자체에 내장된 것이 있지만 사용하기 어렵다.(cipher, decipher)
> - 다른 사람이 만든 crypto-js 라는 것은 install해서 사용하는 것을 권장
>
> 비대칭형 암호화
>
> - HTTPs가 비대칭형 암호화를 사용한다고 한다.
>
> 
>
> 아직 쓸 일이 없을 거 같아서 필요하면 더 자세히 조사

**util**

> 노드에서 각종 편의 기능을 모아둔 모듈
>
> - deprecated와 promisify가 자주 쓰임
> - deprecated (프로그래밍 용어, 중요도가 떨어진 함수가 곧 사라지게 되는 것을 의미)
>   - util.deprecate: 함수가 deprecated 처리되었음을 알려주는 용도
>   - 첫 번째 인자로 넣은 함 수를 사용했을 때 경고 메시지가 출력된다.
>   - 두 번째 인자로 경고 메시지 내용을 넣는다. 
>   - 함수가 조만간 사라지거나 변경될 때 알려줄 수 있어 유용하다.
> - promisify
>   - util.promisify: 콜백 패턴을 프로미스 패턴으로 바꿔줄 수 있다.
>   - 바꿀 함수를 인자로 제공한다. 바꾸면 async/await 패턴까지 사용할 수 있어 좋다. 단, 콜백이 (error, data) => {} 형식이어야 한다.

**worker_threads**

> 원래 싱글 스레드인 노드에서 멀티 스레드 방식으로 작업할 수 있도록 지원해주는 모듈이다. 멀티 스레드를 사용하는 경우는 극히 드문 경우이다. 하지만 알아 놓자.
>
> 1. CPU를 많이 사용하는 암호화나 압축 등의 작업을 직접 구현할 때 사용한다.
>
> 2. 굉장히 복잡한 과정을 거쳐야 한다. 
>
> 3. isMainThread와 if-else 구문을 활용하여 메인 스레드와 워커 스레드를 분기 처리하여 작업을 하게 한다.
>
> 4. 기본 예제
>
>    ```javascript
>    const {
>      Worker, isMainThread, parentPort,
>    } = require('worker_threads');
>    
>    if (isMainThread) { // 부모일 때
>      const worker = new Worker(__filename);
>      worker.on('message', message => console.log('from worker', message));
>      worker.on('exit', () => console.log('worker exit'));
>      worker.postMessage('ping');
>    } else { // 워커일 때
>      parentPort.on('message', (value) => {
>        console.log('from parent', value);
>        parentPort.postMessage('pong');
>        parentPort.close();
>      });
>    }
>    ```
>
> 5. 재밌는 예제
>
>    ```javascript
>    // prime.js
>    // 소수를 찾아주는 알고리즘인 에라토스테네스의 체를 구현한 것
>    // 워커 스레드를 사용하기 전
>    const min = 2;
>    const max = 10000000;
>    const primes = [];
>    
>    function findPrimes(start, range) {
>      let isPrime = true;
>      const end = start + range;
>      for (let i = start; i < end; i++) {
>        for (let j = min; j < Math.sqrt(end); j++) {
>          if (i !== j && i % j === 0) {
>            isPrime = false;
>            break;
>          }
>        }
>        if (isPrime) {
>          primes.push(i);
>        }
>        isPrime = true;
>      }
>    }
>    
>    console.time('prime');
>    findPrimes(min, max);
>    console.timeEnd('prime');
>    console.log(primes.length);
>    ```
>
>    ```javascript
>    // prime-worker.js
>    // 워커 스레드를 적용
>    const { Worker, isMainThread, parentPort, workerData } = require('worker_threads');
>    
>    const min = 2;
>    let primes = [];
>    
>    function findPrimes(start, range) {
>      let isPrime = true;
>      const end = start + range;
>      for (let i = start; i < end; i++) {
>        for (let j = min; j < Math.sqrt(end); j++) {
>          if (i !== j && i % j === 0) {
>            isPrime = false;
>            break;
>          }
>        }
>        if (isPrime) {
>          primes.push(i);
>        }
>        isPrime = true;
>      }
>    }
>    
>    if (isMainThread) {
>      const max = 10000000;
>      const threadCount = 8; // 바꿔가면서 자신의 컴퓨터 성능에 맞게 맞춘다.
>      const threads = new Set();
>      const range = Math.ceil((max - min) / threadCount);
>      let start = min;
>      console.time('prime');
>      for (let i = 0; i < threadCount - 1; i++) {
>        const wStart = start;
>        threads.add(new Worker(__filename, { workerData: { start: wStart, range } }));
>        start += range;
>      }
>      threads.add(new Worker(__filename, { workerData: { start, range: range + ((max - min + 1) % threadCount) } }));
>      for (let worker of threads) {
>        worker.on('error', (err) => {
>          throw err;
>        });
>        worker.on('exit', () => {
>          threads.delete(worker);
>          if (threads.size === 0) {
>            console.timeEnd('prime');
>            console.log(primes.length);
>          }
>        });
>        worker.on('message', (msg) => {
>          primes = primes.concat(msg);
>        });
>      }
>    } else {
>      findPrimes(workerData.start, workerData.range);
>      parentPort.postMessage(primes);
>    }
>    ```
>
>    - 소스 길이는 엄청 많아졌지만 결과를 보면 훨씬 빠르게 결과를 도출해내는 것을 볼 수 있다. 
>    - 하지만 일반적으로 노드로 멀티 스레싱을 하기 보다 효율이 더 좋은 다른 언어(C++, Java, Pyrhon 등)로 작성된 멀티 스레드 응용 프로그램을 노드의 **child_process** 모듈을 통해 실행하고 그 결과를 받아오는 쪽을 선택한다.

**child_process**

> 예제
>
> ```javascript
> // exec.js
> const exec = require('child_process').exec;
> 
> var process = exec('dir');
> 
> process.stdout.on('data', function(data) {
>   console.log(data.toString());
> }); // 실행 결과
> 
> process.stderr.on('data', function(data) {
>   console.error(data.toString());
> }); // 실행 에러
> ```
>
> ```javascript
> // spawn.js
> const spawn = require('child_process').spawn;
> 
> var process = spawn('python', ['test.py']);
> 
> process.stdout.on('data', function(data) {
>   console.log(data.toString());
> }); // 실행 결과
> 
> process.stderr.on('data', function(data) {
>   console.error(data.toString());
> }); // 실행 에러
> ```
>
> ```python
> // test.py
> print('hello python')
> ```

---------

## #5 파일 시스템 접근하기 

**fs**

> - 브라우저에서는 파일 시스템에 접근이 불가능하지만 노드에서는 가능하다.
>
> - 파일을 읽고 쓰는 행위는 **비동기적**이다.
>
> - 기본 예제
>
>   ```javascript
>   // readFile.js : 콜백 함수에 의한 비동기 처리
>   const fs = require('fs');
>
>   fs.readFile('./readme.txt', (err, data) => {
>     if (err) {
>       throw err;
>     }
>     console.log(data);
>     console.log(data.toString());
>   });
>   ```
>
>   ```javascript
>   // readFilePromise.js : promise에 의한 비동기 처리
>   const fs = require('fs').promises;
>
>   fs.readFile('./readme.txt')
>     .then((data) => {
>       console.log(data);
>       console.log(data.toString());
>     })
>     .catch((err) => {
>       console.error(err);
>     });
>   ```
>
>   ```javascript
>   // writeFile.js 
>   const fs = require('fs');
>
>   fs.writeFile('./writeme.txt', '글이 입력됩니다', (err) => {
>     if (err) {
>       throw err;
>     }
>     fs.readFile('./writeme.txt', (err, data) => {
>       if (err) {
>        throw err;
>       }
>       console.log(data.toString());
>     });
>   });
>   ```
>
> - 비동기 처리에 대한 이해
>
>   ```javascript
>   // async.js
>   const fs = require('fs');
>   
>   console.log('시작');
>   fs.readFile('./readme2.txt', (err, data) => {
>     if (err) {
>       throw err;
>     }
>     console.log('1번', data.toString());
>   });
>   fs.readFile('./readme2.txt', (err, data) => {
>     if (err) {
>       throw err;
>     }
>     console.log('2번', data.toString());
>   });
>   fs.readFile('./readme2.txt', (err, data) => {
>     if (err) {
>       throw err;
>     }
>     console.log('3번', data.toString());
>   });
>   console.log('끝');
>   ```
>
>   ➡ 위 코드는 어떤 작업이 먼저 끝날 것인지 예측이 불가능한 코드.
>
>   ![K-001](https://user-images.githubusercontent.com/52457180/91439829-9f1f4d80-e8a8-11ea-9633-313bc67c9990.jpg)
>
> - 동기적으로 순서를 맞춰주는 방법으로는 fs.readFileSync를 사용하는 것이 있다.
>
> - 비동기적으로 백그라운드에서 동시에 여러개의 파일 처리를 하고 각각의 결과를 예측할 수 있도록 순서를 지켜주는 방법이 있다.
>
>   1) 콜백
>
>   ```javascript
>   const fs = require('fs');
>   
>   console.log('시작');
>   fs.readFile('./readme2.txt', (err, data) => {
>     if (err) {
>       throw err;
>     }
>     console.log('1번', data.toString());
>     fs.readFile('./readme2.txt', (err, data) => {
>       if (err) {
>         throw err;
>       }
>       console.log('2번', data.toString());
>       fs.readFile('./readme2.txt', (err, data) => {
>         if (err) {
>           throw err;
>         }
>         console.log('3번', data.toString());
>         console.log('끝');
>       });
>     });
>   });
>   ```
>
>   2) promise
>
>   ```javascript
>   const fs = require('fs').promises;
>   
>   console.log('시작');
>   fs.readFile('./readme2.txt')
>     .then((data) => {
>       console.log('1번', data.toString());
>       return fs.readFile('./readme2.txt');
>     })
>     .then((data) => {
>       console.log('2번', data.toString());
>       return fs.readFile('./readme2.txt');
>     })
>     .then((data) => {
>       console.log('3번', data.toString());
>       console.log('끝');
>     })
>     .catch((err) => {
>       console.error(err);
>     });
>   ```
>
>   3) async/await 을 이용한 방법
>
>   ```javascript
>   const fs= = require('fs').promises;
>   
>   async function main() {
>       let data = await fs.readFile("./readme.txt");
>       console.log("1번", data.toString());
>       data = await fs.readFile("./readme.txt");
>       console.log("2번", data.toString());
>       data = await fs.readFile("./readme.txt");
>       console.log("3번", data.toString());
>       data = await fs.readFile("./readme.txt");
>       console.log("4번", data.toString());
>   }
>   main();
>   ```

**버퍼와 스트림 이해하기**

> - 버퍼 : 일정한 크기로 모아두는 데이터
>
>   1) 일정한 크기가 되면 한 번에 처리
>
>   2) 버퍼링: 버퍼에 데이터가 찰 때까지 모으는 작업
>
> - 스트림 : 데이터의 흐름
>
>   1) 일정한 크기로 나눠서 여러 번에 걸쳐서 처리
>
>   2) 버퍼(또는 청크)의 크기를 작게 만들어서 주기적으로 데이터를 전달
>
>   3) 스트리밍 : 일정한 크기의 데이터를 지속적으로 전달하는 작업
>
>   ![K-002](https://user-images.githubusercontent.com/52457180/91443763-c37e2880-e8ae-11ea-9e47-fffd86ea6ed6.jpg)
>
>   ![K-003](https://user-images.githubusercontent.com/52457180/91443832-d7298f00-e8ae-11ea-9bd4-c686b7e561cf.jpg)

버퍼 사용하기

> 



