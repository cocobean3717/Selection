# 깃 명령어

### 한글이 "\123" 형식으로 표현됨
한글은 git 에서 **일반적이지 않은(unusual) 문자**로 인식


```bash
git config --global core.quotepath false
```

</br>

### .DS_Store 파일이 깃에 포함되는 문제
1. 하위 모든 디렉토리의 .DS_Store 파일 일괄 제거
```bash
find . -name .DS_Store -print0 | xargs -0 git rm -f --ignore-unmatch
```

2. 이미 원격지에 커밋되었다면 제거 후 다시 커밋
```bash
git rm -r --cached .    // 기존에 작성된 내역을 제거 (실제 파일은 제거되지 않으니 안심)
git add .
git commit -m "applying .gitignore"
```

3. .gitignore 파일 생성 후 아래 내용 추가
```vim
.DS_Store
._.DS_Store
**/.DS_Store
**/._.DS_Store
```