# iOS의 화면 전환 및 데이터 전송 장단점

### performSegue() 전환

1. 세그웨이 스토리 보드 생성 및 식별자 지정
2. 전송받는 뷰 컨트롤러에 받을 변수 지정
3. 보낼 객체 생성
4. performSegue() 호출

```swift
performSegue(withIdentifier: "식별자", sender: sender)
```



**문제점**

- 데이터 전송 전 많은 작업(식별자 스트링, 전송 객체) 필요

- 식별자 간 명칭을 표준화 시키지 않으면 나중에 알기 힘듦

- 스토리보드와 소스코드간 스위칭하며 수정 필요

- 스토리보드 사이즈가 커질수록 난잡해짐 (알아보기 힘듦)



### present() 전환

1. 뷰 컨트롤러 식별자 지정 (뷰 컨트롤러 명과 동일하게 지정)
2. 전송받는 뷰 컨트롤러에 받을 변수 지정
3. 뷰 컨트롤러 인스턴스 화 및 데이터 지정
4. present() 호출



**문제점**

- 스토리 보드를 찾는 과정이 번거로움 (extension 으로 해결가능)



### 인스턴스 생성 후 전환

> Interface Builder 를 사용하지 않고 뷰 컨트롤러를 인스턴스화 후 present()

```swift
let viewController = MainViewController()
present(viewController, animated: true)
```



**문제점**

- Interface Builder 를 쓰지 못하므로, UI를 소스 코드로 손수 그려줘야함...

- (위 이유로) 복잡한 UI를 구현하기 힘듦



