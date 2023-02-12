#### UIView(+UIViewController) 의 Layout(크기 지정 및 배치) 3단계

1. Update (업데이트)
   Constraints(제약)를 갱신하는단계
   
   subViews에서 superView 단계로 호출(갱신)됨

2. Layout (레이아웃)
   
   Constraints(제약)를 바탕으로 레이아웃 실행
   
   이 단계에서 UIView의 Center와 bounds가 결정됨 (크기 및 위치가 지정되는 듯)
   
   superView에서 subView 순서로 호출됨

3. Draw (그리기)
   
   UIView의 drawRect(rect: CGRect) 가 호출되어 화면에 그려짐 

#### UIViewController에서 레이아웃이 결정되는 과정

1. viewWillLayoutSubviews() 호출

        뷰의 레이아웃이 **변경되기 직전 하고싶은 작업** 해당 메소드 override 해서 기술

        예를 들면 UIView의 프로퍼티(배경색, 폰트사이즈 등등) 변경 

2. UIViewController의 contentView가 layoutSubviews() 호출 (여기서 contentView는 self.view 를 말하는듯...?)

3. UIViewController의 변경사항을 모든 View에 반영

4. viewDidLayoutSubviews() 호출

        모든 레이아웃이 **변경된 후 하고싶은 작업** 해당 메소드 override 해서 기술

        예를 들면 height 변경, frame 변경 후 layoutIfNeeded() 호출
