## 터미널 Solarized Theme 적용

```sh
$mkdir -p ~/.mysetting/Solarized
$cd ~/.mysetting/Solarized
$git clone https://github.com/sigurdga/gnome-terminal-colors-solarized.git
$cd gnome-terminal-colors-solarized
$./install.sh
```
그럼 다음과 같은 순서 대로 물어 물어 옵니다.  
색상 선택: 1번을 선택  
Please select a color scheme:  
1) dark  
2) dark_alternative  
3) light  
#? 1

프로파일 선택: 1번을 선택  
Please select a Gnome Terminal profile:  
1) 이름 없음  
#? 1

You have selected:

  Scheme:  dark  
  Profile: 이름 없음 (b1dcc9dd-5262-4d8d-a863-c897e6d979b9)

프로파일을 덮어쓰겠냐고 물으면 yes를 입력  
Are you sure you want to overwrite the selected profile?  
(YES to continue) yes  
Confirmation received -- applying settings  

A dircolors adapted to solarized can be automatically downloaded.

1) Download seebi' dircolors-solarized: https://github.com/seebi/dircolors-solarized

2) [DEFAULT] I don't need any dircolors.

디렉토리및파일 색상 변경을 설치하겠냐고 물으면 2번을 눌러 설치 안함을 선택.  
Enter your choice : [2] 2

---

터미널을 종료했다 다시 실행하면 됩니다.

# 디렉토리및 파일 색상 설정

```sh
cd ~/.mysetting/solarized
$git clone https://github.com/seebi/dircolors-solarized

$vi ~/.bash_profile
```

맨밑에 아래 줄을 붙여 넣으세요.

```vim
eval `dircolors ~/.mysetting/solarized/dircolors-solarized/dircolors.ansi`

:wq
```
터미널을 종료 하고 재실행하면 반영됩니다.  
또는 

```sh
$suource ~/.bash_profile
```
