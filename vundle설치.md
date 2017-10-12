# 프로그래밍을 위한 vim 세팅
## 복사/붙여넣기
- vi가 익숙하지 않을 경우 gedit을 이용해도 됩니다.
- 맥용 virtualbox 5.1.28에서 macos용이 게스트 확장이 안되고 있습니다. 클립보드 공유와 화면크기 자동조정, 마우스 통합등. 맥사용자는 불편하더라도 당분간 아래 방법을 써야 합니다. 아님 paralls, vmware를 이용하는 것도 무방합니다.
- centOS에서 브라우저 내용을 복사해서 터미널로 붙여 넣을 때는 ``Shift+Ctrl+v``
- 또는 Alt + 마우스 왼쪽클릭 하면 팝업메뉴가 나옵니다. 붙여넣기 선택
- 또는 터미널 메뉴의 편집 > 붙여넣기를 선택합니다.
## git 설치

```sh
$sudo yum install git
```
- sudo 가붙은 명령은 관리자 비밀번호 입력해야 합니다.

## gvim설치
```sh
$sudo yum install gvim
```

- gvim을 설치하는 이유는 클립보드로 복사, 붙여넣기를 해야 하기 때문입니다.
- vim에서 클립보드 내용을 붙여 넣으려면 "+P
- vim의 내용을 클립보드로 복사 하려면 "+Y
- 이 동작은 .vimrc 에 set clipboard=unnamed 를 추가해야 동작 됩니다. 이 후 한꺼번에 추가하도록 하겠습니다.

터미널에서 vi를 실행하면 gvim이 실행되도록 .bash_profile을 수정합니다.

## .bash_profile 수정
```sh
$cd ~
$vi .bash_profile
```
```vim
" 마지막에 줄에 아래문장을 붙여 넣습니다.
alias vi="gvim -v"

:wq
```
```sh
$source .bash_profile
```

## .vim 디렉토리 생성 및 vundle clone

```sh

$mkdir -p .vim/bundle
$git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
```
## .vimrc 생성

``.vimrc`` 파일을 오픈합니다.

```vim

$gvim
:e ~/.vimrc
```
``.vimrc`` 파일이 열리면 아래 내용을 복사해서 붙여 넣습니다.  
vim에서 붙여넣기 할 때는 편집 메뉴에 있는 붙이기를 선택합니다. 

```vim

"=================================================
" Vundle
" https://github.com/gmarik/vundle
"=================================================
set nocompatible
filetype off
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()

Plugin 'VundleVim/Vundle.vim'
Plugin 'tpope/vim-fugitive'

" All of your Plugins must be added before the following line
Plugin 'altercation/vim-colors-solarized'  " solarized 테마
Plugin 'scrooloose/nerdtree' " 파일/폴더관리
Plugin 'terryma/vim-multiple-cursors'  " 멀티커서 
Plugin 'kien/ctrlp.vim'
"==============    SnipMate  =====================  # 코드단축
Plugin 'MarcWeber/vim-addon-mw-utils'
Plugin 'tomtom/tlib_vim'
Plugin 'garbas/vim-snipmate'
Plugin 'honza/vim-snippets'
"=================================================

Plugin 'davidhalter/jedi-vim'	"파이썬 ide
Plugin 'vim-airline/vim-airline'	"vim 꾸미기
Plugin 'vim-airline/vim-airline-themes'	"vim 꾸미기 테마
Plugin 'tpope/vim-surround'		"문자 감싸기
Plugin 'suan/vim-instant-markdown'  " 마크다운 미리보기
Plugin 'VisIncr'  " 자동증감01234
Plugin 'klen/python-mode' " ide
"==============  마크다운   ======================
Plugin 'godlygeek/tabular' 
Plugin 'plasticboy/vim-markdown'
Plugin 'mzlogin/vim-markdown-toc'
"=================================================
"Plugin 'joshdick/onedark.vim'
"Plugin 'vim-pandoc/vim-pandoc'
"Plugin 'vim-pandoc/vim-pandoc-syntax' 
"Plugin 'junegunn/goyo.vim'
"=====================================
"Plugin 'dbext.vim' " dbms관리
"=====================================
"
call vundle#end()
filetype plugin indent on
" To ignore plugin indent changes, instead use:
" filetype plugin on
"

" Brief help
" :PluginList       - 설치된 플러그인 목록 보기
" :PluginInstall    - 플러그인설치; append `!` to update or just
" :PluginUpdate		- 플러그인 업데이트
" :PluginSearch foo - 플러그인 검색; append `!` to refresh local cache
" :PluginClean      - 사용하지 않은 플러그인 삭제; append `!` to auto-approve removal
" .vimrc에 플러그인을 추가했으면
":w 저장 
":source %  ".vimrc 다시 로드
":PluginInstall				"플러그인 설치
" http://vimawesome.com		"플러그인 조회 사이트
" http://vimcast.org		"강좌
" see :h vundle				"for more details or wiki for FAQ
" Put your non-Plugin stuff after this line

" Use Vim settings, rather than Vi settings (much better!).
" This must be first, because it changes other options as a side effect.
"============================================================="
" An example for a vimrc file.
"
" Maintainer:	Bram Moolenaar <Bram@vim.org>
" Last change:	2011 Apr 15
"
" To use it, copy it to
"     for Unix and OS/2:  ~/.vimrc
"	      for Amiga:  s:.vimrc
"  for MS-DOS and Win32:  $VIM\_vimrc
"	    for OpenVMS:  sys$login:.vimrc

" When started as "evim", evim.vim will already have done these settings.
if v:progname =~? "evim"
  finish
endif

" Use Vim settings, rather than Vi settings (much better!).
" This must be first, because it changes other options as a side effect.
set nocompatible

" allow backspacing over everything in insert mode
set backspace=indent,eol,start

if has("vms")
  set nobackup		" do not keep a backup file, use versions instead
else
  set backup		" keep a backup file
endif
set history=50		" keep 50 lines of command line history
set ruler		" show the cursor position all the time
set showcmd		" display incomplete commands
set incsearch		" do incremental searching

" For Win32 GUI: remove 't' flag from 'guioptions': no tearoff menu entries
" let &guioptions = substitute(&guioptions, "t", "", "g")

" Don't use Ex mode, use Q for formatting
map Q gq

" CTRL-U in insert mode deletes a lot.  Use CTRL-G u to first break undo,
" so that you can undo CTRL-U after inserting a line break.
inoremap <C-U> <C-G>u<C-U>

" In many terminal emulators the mouse works just fine, thus enable it.
if has('mouse')
  set mouse=a
endif

" Switch syntax highlighting on, when the terminal has colors
" Also switch on highlighting the last used search pattern.
if &t_Co > 2 || has("gui_running")
  syntax on
  set hlsearch
endif

" Only do this part when compiled with support for autocommands.
if has("autocmd")

  " Enable file type detection.
  " Use the default filetype settings, so that mail gets 'tw' set to 72,
  " 'cindent' is on in C files, etc.
  " Also load indent files, to automatically do language-dependent indenting.
  filetype plugin indent on

  " Put these in an autocmd group, so that we can delete them easily.
  augroup vimrcEx
  au!

  " For all text files set 'textwidth' to 78 characters.
  autocmd FileType text setlocal textwidth=78

  " When editing a file, always jump to the last known cursor position.
  " Don't do it when the position is invalid or when inside an event handler
  " (happens when dropping a file on gvim).
  " Also don't do it when the mark is in the first line, that is the default
  " position when opening a file.
  autocmd BufReadPost *
    \ if line("'\"") > 1 && line("'\"") <= line("$") |
    \   exe "normal! g`\"" |
    \ endif

  augroup END

else

  set autoindent		" always set autoindenting on

endif " has("autocmd")

" Convenient command to see the difference between the current buffer and the
" file it was loaded from, thus the changes you made.
" Only define it when not defined already.
if !exists(":DiffOrig")
  command DiffOrig vert new | set bt=nofile | r ++edit # | 0d_ | diffthis
		  \ | wincmd p | diffthis
endif

set nu		" 줄번호를 보여줌

" 탭설정 하기
set ts=4	" 탭의 4의 공백 폭을 
"set sts=4	 "탭을 눌렀을 때 스페이스(ascii-0x20) 4개가 삽입되도록 합니다.
"set sw=4	 "'<'나 '>'키로 줄 전체를 밀거나 당길 때 참조되는 폭입니다.
"set et		 "set expandtab 탭을 공백으로 바꿈
"retab		 "et를 다시 적용
set bs+=indent,eol,start	"들여쓰기된 스페이스를 지울 때 백스페이스를 여러번 누르지 않도록 하기 위해 sts 설정값만큼 백스페이스가 적용됩니다.

"==========    instant_markdown     ======================
"마크다운 문서를 작성시 브라우저로 미리 보기
"let g:instant_markdown_slow = 1
let g:instant_markdown_autostart = 1 "자동실행 방지 0

"========     vim_markdown    ============================
" 마크다운 편집을 도와줌
let g:vim_markdown_folding_disabled = 1
let g:vim_markdown_toc_autofit = 1
let g:vim_markdown_math = 1
let g:vim_markdown_frontmatter = 1
let g:vim_markdown_toml_frontmatter = 1
let g:vim_markdown_json_frontmatter = 1

"===================================================================
" 컴파일 , 키맵
" c언어,pytyon
" compile and Run
" java는 eclipse에서 컴파일
au FileType c map <F5> :w<Enter>:!gcc % -o %<.o<Enter>:!./%<.o<Enter>
au FileType python map <F5> :w<Enter>:!python %<Enter>
au FileType rube map <F5> :w<Enter>:!rube %<Enter>


"외부에서 파일변경시 자동으로 읽어들임
"이클립스, xcode 사용시 
set autoread< 

"클립보드사용
set clipboard=unnamed

"===============   airline    ===============
" 화이트 스페이스 체크 안함. 
let g:airline#extensions#whitespace#enabled = 0		
let g:airline#extensions#tabline#enabled = 1 
" vim-airline 버퍼 목록 켜기
" let g:airline#extensions#tabline#fnamemod = ':t' 
" vim-airline 버퍼 목록 파일명만 출력
" let g:airline#extensions#tabline#buffer_nr_show = 1 
" buffer number를 보여준다
let g:airline#extensions#tabline#buffer_nr_format = '%s:' 
" buffer number format
"let g:airline_powerline_fonts = 1
let g:airline_theme='solarized'
let g:airline_solarized_bg='dark'
set laststatus=2
colorscheme solarized
let g:solarized_termcolors=256
"===============   airline    =================

let mapleader=","  " 리더키를 , 로 변경 주석처리하면 원상태
nnoremap <Leader>ex !!$SHELL<CR> ",ex로 외부명령을 실행
"nnoremap <Leader>rc :tabnew $MYVIMRC<CR> "새탭으로 오픈
"nnoremap <Leader>rc :rightbelow vnew $MYVIMRC<CR>" 오른쪽에 오픈
nnoremap <Leader>rc :e $MYVIMRC<CR> ",rc로 .vimrc파일 오픈
"nnoremap <Leader>n :NERDTreeToggle<CR>
"nnoremap <C-F> :NERDTreeFind<CR>

"================  약어  (abbreviations)  ======================
" snippet은 tab을 눌러야하고 약어는 자동으보 바뀜
" snippet은 자동완성, 
"ab la Los Angeles(L.A) 이렇게 사용해야함.
"한글 약어는 안되는 단어도 있음, 한글 약어가 안될땐 snippet에 추가.
ab 컨브 Ctrl+v
ab 컨씨 Ctrl+c
ab 컨엠 Ctrl+m
ab 이시 Ctrl+[ or \<Esc\>
ab 노모 Normal mode
ab 커모 Command mode
ab 비모 Visual mode
ab 인모 Insert mode
ab 로렘 정당은 법률이 정하는 바에 의하여 국가의 보호를 받으며, 국가는 법률이 정하는 바에 의하여 정당운영에 필요한 자금을 보조할 수 있다. 대통령의 임기연장 또는 중임변경을 위한 헌법개정은 그 헌법개정 제안 당시의 대통령에 대하여는 효력이 없다. 위원은 탄핵 또는 금고 이상의 형의 선고에 의하지 아니하고는 파면되지 아니한다. 제3항의 승인을 얻지 못한 때에는 그 처분 또는 명령은 그때부터 효력을 상실한다. 이 경우 그 명령에 의하여 개정 또는 폐지되었던 법률은 그 명령이 승인을 얻지 못한 때부터 당연히 효력을 회복한다.
ab 배요일 "월", "화", "수", "목", "금", "토", "일"
ab 배코이름 "유재석", "박명수", "강호동", "신동엽", "박미선"
ab 배색깔 "빨강", "주황", "노랑", "초록", "파랑", "남", "보라"
ab 브이아이 VI
ab 빔 VIM


```

저장하고 .vimrc를 다시 읽어들입니다.

```vim
:w
:so %
```
오류가 많이 나는데 무시 해도 됩니다. 아직 플러그인 설치가 되지 않아서 발생하는 오류 입니다.  
플러그인을 설치합니다.

```vim
:PluginInstall
```
vim을 종료했다 다시 시작합니다.
설치가 완료 되었습니다.
