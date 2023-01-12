*AController <- 응답을 받을 컨트롤러*

*BController <- 응답을 보낼 컨트롤러*



##### Delegate 패턴을 활용한 뷰 컨트롤러간 데이터 전송

> NotifyControllerHiDelegate <- 응답을 받고 싶은 컨트롤러가 채택하면 응답을 받을 수 있는 프로토콜 선언

    **BController 가 특정 상황에 AController 에게 응답을 주고 싶다고 하자**

1. NotifyControllerHiDelegate 라는 프로토콜을 선언한뒤 이름이 onReceive() 인 메소드 구현

2. BController 의 전역 변수로 delegate: NotifyControllerHiDelegate? 선언

3. AController 에서 NotifyControllerHiDelegate 프로토콜을 채택한 뒤, onReceive() 메소드의 몸체 구현 ex: print("B replied hello!")

4. AController 에서 BController 로 전환하기 전 BController의 delegate 변수에 self(AController 자기자신) 저장

5. BController 에서 AController 로 응답하고 싶을 때 delegate.onReceive() 호출

##### Closure 를 활용한 뷰 컨트롤러간 데이터 전송

1. BController 에 onReceiveClosure: (() -> ())? 변수 선언

2. AController 에서 BController 로 전환하기 전 BController의 onReceiveClosure 의 클로저 몸체 구현 ex: print("B replied hello!")

3. BController 에서 AController 로 응답하고 싶을 때 onReceiveClosure() 호출
