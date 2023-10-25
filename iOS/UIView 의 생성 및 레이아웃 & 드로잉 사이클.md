
## 개요

> UIViewController 가 화면에 대한 상태를 가지듯, UIView 도 자신만의 상태를 가진다.
> 뷰의 생성 및 제약조건 설정, 실제로 화면에 그려지기까지의 메소드를 하나씩 살펴보고, 
> 궁극적인 목표인 layoutIfNeeded, setNeedsLayout 가 정확하게 무엇을 실행하는 함수인지 알아보자.

</br>
</br>

## Main Run Loop

> 함수를 알아보기전에 먼저 `Main Run Loop` 에 대한 개념부터 짚고 넘어갈 필요가 있다.
> `Main Run Loop` 는 iOS 애플리케이션이 실행될 때, 각종 이벤트(사용자 입력, 기기 상태 변화 등)를 
> 처리하며(위임된 핸들러가 실질적으로 이벤트를  처리한다.) 처리가 끝난 뒤 권한이 다시 `Main Run Loop` 로 돌아오면, 변경사항에 대한 UI를 업데이트하는 `Update Cycle` 이 호출된다.

</br>
</br>

## Update Cycle (= drawing cycle)

> 변경된 사항을 화면에 다시 그려주는 시점.
> 시스템은 실질적으로 변경된 사항이 있거나, 핸들러가 종료되어 `Main Run Loop` 로 반환될 때, Update Cycle 로 전환하여 화면을 갱신한다.

</br>
</br>

## init(frame: CGRect) & init(coder: NSCoder)
> UIView 가 초기화될 때 호출되는 함수.
> 커스텀 뷰를 구현하고 싶다면 UIView 를 상속 받고 위 두 이니셜라이저를 구현해주어야한다.
> 두 함수 모두 UIView 가 초기화 될 때 호출되는 함수지만, 구현 방식에 따른 차이가 있다.

**init(frame: CGRect)**
```swift
// CustomView 의 init(frame) 이 호출된다.
let view = CustomView(frame: .init(x: 0, y: 0, width: 200: height: 200))
```

**init(coder: NSCorder)**
```swift
// Xib 나 Storyboard 로 구성된 UI를 코드상에서 사용하기 위해서 사용된다.
let nib = Bundle.main.loadNibNamed("CustomView", owner: self, options: nil)!
let viewFromNib = nib.first as! CustomView
self.view.addSubview(viewFromNib)
```
> Xib 나 Storyboard 는 xml 형식의 파일로 저장되어있는데, 이를 실제로 사용하기 위해서는 클래스를 객체화 시키는 것 처럼 xml 을 실체화(메모리 적재) 시키는 작업이 필요하다. 이걸 NSCoder(실제론 NSUnarchiver) 가 수행하여 우리는 인터페이스 빌더로 작성된 UI를 소스코드상에서도 사용할 수 있다.

</br>
</br>

## layoutSubViews()

> UIView 의 위치나 크기(frame & bounds), 제약조건(contraints)들이 변경되어서 다시 그려야져야할 필요가 있을 때 시스템이 자동으로 호출하는 함수.
> _(1. 뷰의 사이즈가 재 조정되거나, 2. 하위뷰가 추가되거나, 3. 스크롤 뷰에서 스크롤 되거나, 4. 디바이스가 회전하거나, 5. 뷰의 제약조건이 갱신될 때 자동으로 layoutSubviews 가 호출된다.)_
> 해당 함수가 호출되면 현재 UIView 의 자식 뷰들의 layoutSubViews() 메소드가 호출됩니다.
> 호출 순서는 현재 뷰 -> 자식 뷰 순서대로 호출됩니다.

</br>
</br>

## setNeedsLayout()
>다음 `Update Cycle` 에 레이아웃을 갱신해야함을 시스템에게 알립니다.
>이 메소드를 호출한 UIView 는 다음 `Update Cycle` 에서 `layoutSubviews()` 가 호출된다. (= 갱신 예약)

## layoutIfNeeded()
> **즉시** 레이아웃을 갱신합니다.
> 이 메소드를 호출한 UIView 는 그 **즉시** 갱신됩니다. 일반적으로 뷰에 즉시 값이 반영되어야하는 애니메이션을 적용할 경우 사용됩니다.

## setNeedsDisplay()
> 다음 `Update Cycle` 에 다시 그려야한다는 것을 시스템에게 알립니다.
> `Update Cycle` 에서 `draw(_:CGRect)` 를 호출합니다.

### draw(\_: CGRect)
> 뷰의 콘텐츠가 실질적으로 그려질 때 호출됩니다.
> 코어 그래픽스 나 다른 드로잉 API 를 사용한 커스텀 뷰에서 그릴 때 사용하면 됩니다.

### willMove(toSuperview: UIView?)
> 상위 뷰에서 현재 뷰가 추가되거나 제거될 때 호출됩니다.

### didMoveToSuperview()
> 상위 뷰에서 현재 뷰가 추가되거나 제거될 때 호출됩니다.

### didMoveToWindow()
> 윈도우에서 뷰가 추가되거나 제거될 때 호출됩니다.

### removeFromSuperview()
> 상위뷰에서 제거될 때 호출됩니다.

### (보충) UIView 레이아웃 메소드 호출 순서
1. requiresConstraintBasedLayout (= translatesAutoresizingMaskIntoConstraints)
2. updateConstraints (= 오토레이아웃 설정)
3. intrinsicContentSize (= 고유 크기 지정)
4. layoutSubviews
5. drawRect (= draw(\_: CGRect))


## 참고
- https://sweetfood-dev.github.io/ios/viewlifecycle/ (UIView Drawing Cycle)
- https://ontheswift.tistory.com/20 (setNeedsLayout() vs layoutIfNeeded 차이점)
- https://baked-corn.tistory.com/105 (setNeedsLayout vs layoutIfNeeded)
- https://medium.com/@nirajpaul.ios/uiview-lifecycle-12435f8de492 (UIView lifecycle)
- https://medium.com/@b9d9/required-init-coder-nscoder-%EC%97%90-%EB%8C%80%ED%95%B4%EC%84%9C-b67ddfc628 (NSCoder)
- https://jeonyeohun.tistory.com/359 (NSCoder)
- https://velog.io/@haero_kim/Android-LayoutInflater-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0 (Android LayoutInflater)
- https://zeddios.tistory.com/359 (setNeedsDisplay)
