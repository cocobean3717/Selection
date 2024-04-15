# Git Command

### 한글이 "\123" 형식으로 표현됨

원인 - 한글은 git 에서 **일반적이지 않은(unusual) 문자**로 인식

해결 - 아래 명령어 입력

```bash
git config --global core.quotepath false
```

### DS_Store
**하위 모든 디렉토리의 .DS_Store 파일 일괄 제거**
```base
find . -name .DS_Store -print0 | xargs -0 git rm -f --ignore-unmatch
```

### git update
> 원격지에 새로 생성된 브랜치가 있고, `git pull` 를 통해 로컬에 가져오려고 했지만 `git branch` 로 확인 해 봐도 브랜치가 보이지 않았다.
> 원격지의 변경사항을 확인하기전엔 **git remote** 명령을 통해 원격지의 변경사항을 먼저 가져와야한다.
```bash
git remote update
// 그리고
git pull
```
