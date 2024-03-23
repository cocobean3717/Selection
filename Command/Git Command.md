# 깃 명령어

#### 한글이 "\123" 형식으로 표현됨

원인 - 한글은 git 에서 **일반적이지 않은(unusual) 문자**로 인식

해결 - 아래 명령어 입력

```bash
git config --global core.quotepath false
```

**하위 모든 디렉토리의 .DS_Store 파일 일괄 제거**
```base
find . -name .DS_Store -print0 | xargs -0 git rm -f --ignore-unmatch
```