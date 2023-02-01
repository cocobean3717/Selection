## UIScrollView

- FrameLayout: 스크롤 뷰에서 현재 보여지고 있는 영역 정의

- ContentLayout: 스크롤 뷰 내용의 전체 영역 정의

<br />

### 코드로 스크롤 뷰 만드는 방법

```
// 스크롤 뷰 생성

let scrollView: UIScrollView! = UIScrollView()

// 스크롤 내부에 들어갈 콘텐츠 뷰 생성

let contentView: UIView! = UIView()



// 제약조건 변경을 위해 시스템 오토레이아웃 해제

scrollView.translatesAutoresizingMaskIntoConstraints = false

contentView.translatesAutoresizingMaskIntoConstraints = false



// 뷰 얹기

view.addSubview(scrollView)

scrollView.addSubview(contentView)



// 스크롤 뷰와 부모 뷰의 레이아웃 맞춤

NSLayoutConstraint.activate([

scrollView.leadingAnchor.constraint(equalTo: view.safeAreaLayoutGuide.leadingAnchor),

scrollView.trailingAnchor.constraint(equalTo: view.safeAreaLayoutGuide.trailingAnchor),

scrollView.topAnchor.constraint(equalTo: view.safeAreaLayoutGuide.topAnchor),

scrollView.bottomAnchor.constraint(equalTo: view.safeAreaLayoutGuide.bottomAnchor)

])



// 콘텐츠 뷰의 레이아웃은 스크롤 뷰의 contentLayoutGuide와 동일(!)하게 맞춰줌

NSLayoutConstraint.activate([

contentView.leadingAnchor.constraint(equalTo: scrollView.contentLayoutGuide.leadingAnchor),

contentView.trailingAnchor.constraint(equalTo: scrollView.contentLayoutGuide.trailingAnchor),

contentView.topAnchor.constraint(equalTo: scrollView.contentLayoutGuide.topAnchor),

contentView.bottomAnchor.constraint(equalTo: scrollView.contentLayoutGuide.bottomAnchor)

])



// 수직(!)으로 스크롤 하기위해 콘텐츠 뷰의 너비와 스크롤 뷰의 너비를 동일하게 맞춰줌

contentView.widthAnchor.constraint(equalTo: scrollView.widthAnchor).isActive = true



// 콘텐츠 뷰의 높이와 스크롤 뷰의 높이를 동일하게 맞춰주되, priority 를 조정하여 스크롤이 가능하도록 변경

let contentViewHeight = contentView.heightAnchor.constraint(greaterThanOrEqualTo: view.heightAnchor)

contentViewHeight.priority = .defaultLow

contentViewHeight.isActive = true



// 콘텐츠 뷰의 내부에 뷰를 채운뒤 레이아웃을 지정해주면 수직 스크롤이 적용됨!

contentView.addSubview(movieTitle)

contentView.addSubview(movieImage)

contentView.addSubview(movieDescription)

NSLayoutConstraint.activate([

movieTitle.centerXAnchor.constraint(equalTo: contentView.centerXAnchor),

movieTitle.topAnchor.constraint(equalTo: contentView.topAnchor, constant: 150),

movieImage.centerXAnchor.constraint(equalTo: contentView.centerXAnchor),

  movieImage.widthAnchor.constraint(equalToConstant: 300),

  movieImage.heightAnchor.constraint(equalToConstant: 300),

    movieImage.topAnchor.constraint(equalTo: movieTitle.bottomAnchor, constant: 40),

movieDescription.topAnchor.constraint(equalTo: movieImage.bottomAnchor, constant: 40),

movieDescription.leadingAnchor.constraint(equalTo: contentView.leadingAnchor, constant: 20),

movieDescription.trailingAnchor.constraint(equalTo: contentView.trailingAnchor, constant: -20)

])
```

#### 참고

https://velog.io/@nnnyeong/iOS-UIScrollView-%EB%8B%A4%EB%A3%A8%EA%B8%B0-autolayout-programatically
