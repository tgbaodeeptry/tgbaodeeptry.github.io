---
layout: post
title: Hướng dẫn cài đặt Vim - Editor thần thánh (P2)
thumbnail-img: /assets/posts/vim-editor-than-thanh-p2/12.png
tags: [vim, editor]
---

Xin chào các bạn, trong  [bài viết trước](htps://codelearn.io/sharing/cai-dat-vim-editor-than-thanh-phan-1)  mình đã giới thiệu cho các bạn về Vim, cách cài đặt Vim và một số thao tác cơ bản. Trong bài viết hôm nay, mình sẽ hướng dẫn cho các bạn cách tinh chỉnh Vim và cài một số plugin phố biến.

Trong bài viết này mình sẽ thao tác toàn bộ với Linux, với một số bạn dùng MacOS, Windows bạn cũng có thể làm tương tự

### Tùy chỉnh Vim cơ bản

Mặc định, file config của vim sẽ nằm ở  `~/.vimrc` trong một số trường hợp nó có thể ở  `/etc/vim/vimrc` hoặc  `/etc/vimrc`. Hoặc nếu file không tồn tại, bạn hãy tạo file mới bằng lệnh 

```bash
$ touch ~/.vimrc`
```

sau đó bạn mở file lên theo 

```bash
$ vim ~/.vimrc`
```

![Giao diện sau khi mở file config Vim lên](/assets/posts/vim-editor-than-thanh-p2/1.png)

Bạn chuyển sang  INSERT MODE và thêm các config như sau:

```vim
" Bật highlight cú pháp cho một loại file (như .py, .cpp, .xml)
syntax enable
syntax on

" Hiện số thứ tự của dòng
set number

" Không hiện số thứ tự của dòng
set nonumber

" Hiện số thứ tự theo cách relative
" Dòng hiện tại đánh số 0, dòng trên và dòng dưới là 1, 
" và cứ thế đối với các dòng khác
set relativenumber

" Hiện số thứ tự theo cách hybrid
" Dòng hiện tại đánh số là số dòng thực tế, 
" dòng trên và dòng dưới là 1, và cứ thế đối với các dòng khác
set number relativenumber

" Chỉnh 4 space mỗi tab
set tabstop=4

" Chỉnh 4 space mỗi indent
set shiftwidth=4

" Sử dụng space character thay tab character khi nhấn Tab
set expandtab

" Tự động indent khi xuống hàng
set autoindent

" Sử dụng clipboard hệ thống thay buffer của vim
set clipboard=unnamedplus

" Chỉnh độ delay (ms) giữa lần chuyển chế độ
set ttimeoutlen=50

" Highlight dòng hiện tại
set cursorline`
```

Lưu lại và thoát bằng lệnh  `:wq` sau khi mở lại ta sẽ có giao diện như này đây

![Giao diện sau khi config một số thứ cơ bản của Vim](/assets/posts/vim-editor-than-thanh-p2/2.png)

### Cài đặt Plugin cho Vim

Chúng ta có 2 cách cài đặt Plugin cho Vim:

*   Cài đặt Vim thuần bằng tay
*   Cài đặt Vim bằng các gói quản lý Plugin

#### \# Cài đặt Vim thuần bằng tay

Mặc định, thư mục  `~/.vim` sẽ không có cấu trúc để cài Plugin, chúng ta sẽ tạo các thư mục bằng cách

```bash
$ mkdir -p ~/.vim/pack/vendor/start`
```

Sau đó thêm các plugin muốn cài vào thư mục đó, nó sẽ load tự động khi mở vim lên.

Ví dụ khi cài NERDTree ( Sidebar chọn file cho Vim ), ta thực hiện:

```bash
$ git clone --depth 1 \
  https://github.com/preservim/nerdtree.git \
  ~/.vim/pack/vendor/start/nerdtree`
```

Nó có nghĩa là: clone plugin vào thư mục  `~/.vim/pack/vendor/start/` với tên  `nerdtree`

#### \# Cài đặt Vim bằng các gói quản lý Plugin

Có nhiều gói quản lý Plugin như: Bundle, Vim-Plug, Pathogen,... vân vân và mây mây. Trong bài viết này mình sẽ dùng  `Vim-Plug`, vì mình thấy nó có khá nhiều đặc điểm hay

*   Cú pháp gọn, dễ nhớ
*   Khá nhanh
*   Cài đặt cũng dễ

Cách cài đặt:

*   Unix (Linux / MacOS)

```bash
$ curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim`
``` 

*   Windows (dùng PowerShell)

```
$ iwr -useb https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim |`
    ni "$(@($env:XDG_DATA_HOME, $env:LOCALAPPDATA)[$null -eq $env:XDG_DATA_HOME])/nvim-data/site/autoload/plug.vim" -Force
```

Sử dụng:

1.  Chúng ta mở  `~/.vimrc lên
2.  Kiếm đoạn nào trống trống ấy :))
3.  Rồi thêm phần mở đầu  call  `plug#begin()`
4.  Bên dưới ta ghi các Plugin muốn cái theo cú pháp  `Plug "xxxx"` (Với xxxx là đuôi của đường dẫn github tới plugin cần cài)
5.  Sau khi thêm, ta kết thúc phần cài đặt plugin bằng cách thêm  `call  plug#end()`  vào cuối

Ví dụ:

```vim
" Gọi đầu tiên
call plug#begin('~/.vim/plugged')

" Cài plugin Shorthand notation;  https://github.com/junegunn/vim-easy-align
Plug 'junegunn/vim-easy-align'

" Hoặc sử dụng đường dẫn trực tiếp luôn
Plug 'https://github.com/junegunn/vim-github-dashboard.git'

" Cài đặt nhiều Plugin bằng cách sử |
Plug 'SirVer/ultisnips' | Plug 'honza/vim-snippets'

" Loading sau khi cài Plugin. 
Plug 'scrooloose/nerdtree', { 'on':  'NERDTreeToggle' }
Plug 'tpope/vim-fireplace', { 'for': 'clojure' }

" Cài plugin với branch tùy chọn
Plug 'rdnetto/YCM-Generator', { 'branch': 'stable' }

" Cài plugin bằng tag released
Plug 'fatih/vim-go', { 'tag': '*' }

" Tùy chọn khi cài plugin
Plug 'nsf/gocode', { 'tag': 'v.20150303', 'rtp': 'vim' }

" Cài plugin từ bên ngoài ~/.vim/plugged với post-update
Plug 'junegunn/fzf', { 'dir': '~/.fzf', 'do': './install --all' }

" Kết thúc việc cài plugin
call plug#end()
```

Sau đó save và reload bằng lệnh  `:source %` hoặc ta thoát mở lại. Sau đó gõ câu lệnh  `:PlugInstall` để cài đặc các plugin nhé :D

![Install Plugin với Vim](/assets/posts/vim-editor-than-thanh-p2/3.png)

Ngoài ra còn một số lệnh như:

*   `PlugUpdate`: cập nhật các Plugin đến phiên bản mới nhất
*   `PlugClean`: Xóa các Plugin đã cài nhưng không có trong config
*   `PlugUpgrade`: Tự update chính Vim-Plug
*   `PlugStatus`: Xem trạng thái của các Plugin
*   `PlugSnapshot`: Tạo bản backup phòng trường hợp bị mất

### Một số plugin phổ biến cho Vim

#  [vim-airline](https://github.com/vim-airline/vim-airline)

Plugin thay đổi giao diện cho status bar của Vim

```vim
" Cài đặt với Vim-Plug
Plug 'vim-airline/vim-airline'
Plug 'vim-airline/vim-airline-themes'
```

Các bạn có thể truy cập  [vim-airline-themes](https://github.com/vim-airline/vim-airline-themes#vim-airline-themes--) để chọn theme bạn thích nhé

![vim-airline plugin cho vim](/assets/posts/vim-editor-than-thanh-p2/4.gif)

#  [nerdtree](https://github.com/preservim/nerdtree)

Plugin hiện các thư mục, file theo dạng tree

```vim
" Cài đặt với Vim-Plug
Plug 'preservim/nerdtree'

" Thêm đoạn này vào .vimrc sau đó reload và :PlugInstall
syntax on
filetype plugin indent on
```

![Plugin NERDTree cho Vim](/assets/posts/vim-editor-than-thanh-p2/5.png)

#  [nerd commenter](https://github.com/preservim/nerdcommenter)

Plugin comment đa dạng cho Vim

```vim
" Cài đặt với Vim-Plug
Plug 'preservim/nerdcommenter'
```

![Plugin Nerd Commenter cho Vim](/assets/posts/vim-editor-than-thanh-p2/6.gif)

#  [fzf](https://github.com/junegunn/fzf.vim)

Plugin tìm kiếm file nhanh chóng

```vim
" Cài đặt với Vim-Plug
Plug 'junegunn/fzf', { 'do': { -> fzf#install() } }
Plug 'junegunn/fzf.vim'
```

![plugin fzf cho Vim ](/assets/posts/vim-editor-than-thanh-p2/7.gif)

#  [vim-surround](https://github.com/tpope/vim-surround)

Plugin thao tác nhanh với ngoặc, xml tags, ngoặc kép, dấu nháy ...

```vim
" Cài đặt với Vim-Plug
Plug 'tpope/vim-surround'
```

![Plugin Vim-Surround cho Vim](/assets/posts/vim-editor-than-thanh-p2/8.gif)

### Cài đặt giao diện cho Vim

#### #  [Dracula Theme](https://github.com/dracula/vim)

*   Cài đặt

```vim
" Cài đặt với Vim-Plug
Plug 'dracula/vim', { 'name': 'dracula' }

" Thêm đoạn này vào .vimrc
syntax enable
colorscheme dracula

" Sau đó reload .vimrc và dùng lệnh
:PlugInstall
```

*   Hình ảnh

![Giao diện dracula của Vim](/assets/posts/vim-editor-than-thanh-p2/9.png)

#### #  [Monokai Theme](https://github.com/sickill/vim-monokai)

*   Cài đặt

```vim
" Cài đặt với Vim-Plug
Plug 'sickill/vim-monokai'

" Thêm đoạn này vào .vimrc
syntax enable
colorscheme monokai

" Sau đó reload .vimrc và dùng lệnh
:PlugInstall
```

*   Hình ảnh

### ![Monokai Theme của Vim](/assets/posts/vim-editor-than-thanh-p2/10.png)

#### #  [Solarized Theme](https://github.com/altercation/vim-colors-solarized)

*   Cài đặt

```vim
" Cài đặt với Vim-Plug
Plug 'altercation/vim-colors-solarized'

" Thêm đoạn này vào .vimrc, thay dark thành light 
" nếu bạn muốn giao diện sáng
syntax enable
set background=dark
colorscheme solarized

" Sau đó reload .vimrc và dùng lệnh
:PlugInstall
```

*   Hình ảnh

![Giao diện solarized của Vim](/assets/posts/vim-editor-than-thanh-p2/11.png)

### Thành quả

Đây là Vim của mình sau khi tùy chỉnh, đẹp đúng không nhỉ?

![](/assets/posts/vim-editor-than-thanh-p2/12.png)

Các bạn có thể sử dụng config của mình  [tại đây](https://gist.github.com/tgbaodeeptry/491347d1ae0c7fdd0440f61e92ee9802)

### Phần Kết

Qua hai bài viết, mình đã giới thiệu gần như mọi thứ cơ bản của Vim. Vim rất hay, rất tốt và cũng rất cần thiết cho mọi lập trình viên để nâng cao năng suất làm việc. Series này chỉ giới thiệu những thứ cơ bản thôi, bạn có thể tự tìm tòi để nâng cao tốc độ và tay nghề nhé. Hẹn gặp lại các bạn trong những bài viết khác nhé. Đừng quên rate và share cho mình nhé :D Và nếu các bạn không hiểu phần nào có thể comment bên dưới nha
