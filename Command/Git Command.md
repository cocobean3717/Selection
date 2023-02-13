# 깃 허브 명령어

#### 한글이 "\123" 형식으로 표현됨

원인 - 한글은 git 에서 **일반적이지 않은(unusual) 문자**로 인식

해결 - 아래 명령어 입력

```bash
git config --global core.quotepath false
```
