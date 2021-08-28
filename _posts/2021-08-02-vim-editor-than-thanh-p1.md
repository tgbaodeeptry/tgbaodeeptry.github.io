---
layout: post
title: Hướng dẫn cài đặt Vim - Editor thần thánh (P1)
thumbnail-img: /assets/posts/vim-editor-than-thanh-p1/2.png
tags: [vim, editor]
---

Xin chào các bạn. Trong bài viết hôm nay, mình sẽ chia sẽ cho các bạn một editor thần thánh cực kì nổi tiếng và phổ biến được ưa dùng với 25% lập trình viên trên toàn cầu, đó chính là Vim.

### VIM là gì? 

Vim (Vi IMproved) là một phần mềm mã nguồn mở được giới thiệu vào năm 1991 dựa trên  vi của Bill Joy với một số tính năng bổ sung. Vim ban đầu được phát triển cho Amiga, nhưng sau đó được phát triển thành ứng dụng đa nền tảng ( cho Windows, Linux, MacOS, ... ). Năm 2003, Vim được được bình chọn là trình soạn thảo phổ biến nhất.

### Ưu điểm và hạn chế của Vim

Ưu điểm

*   Gọn, nhẹ: G iao diện của Vim không dựa trên các menu hay icon mà dựa trên các lệnh được đưa ra từ text user interface. Nên bạn không cần phải lo về vấn đề nó có ngốn ram như VS Code không :)) 
*   Tốc độ làm việc nhanh: Vim chủ yếu tương tác với người dùng qua câu lệnh, nên chỉ cần bạn gõ phím ổn là bạn sẽ thấy tốc độ làm việc nhanh lên trông thấy 
*   Khả năng tùy chỉnh cao:  Một phần sức mạnh của Vim là nó có thể được tùy biến rộng rãi. Giao diện cơ bản có thể được thay đổi bởi nhiều tùy chọn có sẵn. Hay nói một cách khác là bạn có thể biến Vim như mong muốn của mình
*   Nhiều plugins: Vim có một lượng plugin đồ sộ cho phép người dùng nâng cao hiệu suất, cải thiện giao diện, ...
*   Cộng đồng cực kì lớn: Vì là một editor khá hay nên cồng động người dùng rất lớn ( > 25% lập trình viên đang sử dụng nó ).
*   Cảm giác ngầu lồi: Vim chủ yếu là dùng bàn phím, nên bạn có thể canh lúc có gái bên cạnh mà mở lên gõ tạch tạch cho ngầu :))

Nhược điểm:

*   Nhiều phím tắt: Vì mục đích của Vim là cải thiện tốc độ làm việc thông qua việc gõ phím, nên lượng phím tắt là vô số kể
*   Rất dễ nản: Với nhưng người lần mới sử dụng thì rất dễ bị nản vì nhiều lí do ( giao diện ban đầu khi chưa tùy chỉnh, phím tắt, câu lệnh, ... )

Vì vậy chúng ta có rất nhiều lý do để  NÊN sử dụng Vim

![Bảng xếp hạng các Editor được sử dụng nhiều nhất 2019](/assets/posts/vim-editor-than-thanh-p1/1.png)

### Cách cài đặt

Vim được tích hợp sẵn trong các phiên bản của Linux mới nhất nhưng bạn cũng có thể cài đặt riêng cho một số hệ điều hành khác.

Windows:

```
Các bạn cài theo đường dẫn sau: https://www.vim.org/download.php#pc`
```

Linux:

```bash
$ sudo apt-get update
```
```bash
$ sudo apt-get install vim
``` 

MacOS:

```bash
$ ruby -e ""$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"" < /dev/null 2> /dev/null
$ brew install vim`
```

### Khởi động

Bạn có thể khởi động vim sau đó chọn file, hoặc là mở vim với file cùng lúc. Trong những ví dụ dưới đây mình sẽ chỉ các bạn cách mở vim với file cùng lúc. Các bạn có thể xóa phần file đi thì có thể mở vim trống nhé

Windows:

*   Các bạn mở PowerShell hoặc Command Prompt và gõ câu lệnh sau. Các bạn nhớ thay đường dẫn tới vim.exe và file.txt thành đường dẫn tới file của bạn nhé

```
"C:\program Files\gvim\vim9.9\vim.exe" file.txt
```

Linux / MacOS:

```bash
$ vim file.txt
```  

*   Hoặc các bạn có thể thay vim thành vi cho gọn :D

```bash
$ vi file.txt
```

![Giao diện mặc định của Vim](/assets/posts/vim-editor-than-thanh-p1/2.png)

### Các thao tác cơ bản

Trong vim có ba chế độ:

*   NORMAL: Trong chế độ này bản có thể dùng các phím tắt các câu lệnh mà không làm ảnh hưởng tới phần văn bản đang gõ.
*   INSERT: Bạn có thể gõ code, văn bản này trong chế độ này. Đồng thời trong chế độ này bạn không thể dùng phím tắt hoặc lệnh.
*   VISUAL: Chế độ chọn. Bạn có thể dùng chế độ này để chọn nhanh phần văn bản để xử lý.

![Các mode trong Vim](/assets/posts/vim-editor-than-thanh-p1/vim-demonstration.gif)

Di chuyển:

*   `h`: di chuyển con trỏ chuột  sang trái
*   `j`: di chuyển con trỏ chuột  xuống dưới
*   `k`: di chuyển con trỏ chuột  lên trên
*   `l`: di chuyển con trỏ chuột  sang phải
*   `$`: di chuyển con trỏ chuột xuống  cuối dòng
*   `0`: di chuyển con trỏ chuột về  đầu dòng
*   `gg`: di chuyển con trỏ chuột về  đầu văn bản
*   `G`: di chuyển con trỏ chuột xuống  cuối văn bản
*   `Ctrl-y`:  cuộn lên văn bản  một dòng
*   `Ctrl-e`:  cuộn xuống văn bản  một dòng
*   `Ctrl-u`:  cuộn lên văn bản  nửa màn hình
*   `Ctrl-d`:  cuộn xuống văn bản  nửa màn hình

Thay đổi chế độ:

*   `i`: Chuyển sang chế độ  INSERT
*   `v`: Chuyển sang chế độ  VISUAL
*   `V`: Chuyển sang chế độ  VISUAL LINE (chọn hàng thay vì chọn từ như VISUAL)
*   `Esc`: Chuyển sang chế độ  NORMAL

Thao tác với văn bản:

*   `x`:  Xóa kí tự tại con trỏ
*   `y`:  Copy phần văn văn bản đã chọn trong chế độ VISUAL
*   `p`:  Paste phần văn bản đã lưu
*   `d`:  Delete văn bản
    *   `d2w`: Xóa 2 từ đăng sau con trỏ (delete ... word)
    *   `d$`: Xóa đến cuối dòng
    *   `d3b`: Xóa 2 từ đằng trước con trỏ (delete ... backwards)
    *   `dt)`: Xóa đến kí tự ")" (delete till ...)
    *   `d2j`: Xóa 2 dòng bên dưới (delete ... j là xuống)
    *   `d2h`: Xóa 2 chữ bên trải (delete ... h là qua trái)
    *   `dd`: Xóa dòng hiện tại của con trỏ
*   `u`:  Undo 
*   `Ctrl-r`:  Redo

Câu lệnh thường gặp:

*   `:w`:  Lưu văn bản
*   `:wq`:  Lưu và thoát văn bản ( hoặc sử dụng ZZ )
*   `:q!`:  Thoát không lưu

Để làm quen Vim tốt hơn bạn có thể sử dụng lệnh  `:Tutor`  để mở tutorial được cài mặc định trong Vim

![Làm việc với Vim](/assets/posts/vim-editor-than-thanh-p1/4.gif)
---------------------------------------------------------------------------------------------------------

### Tạm kết

Trên đây là một cách cài Vim cũng như một số thao tác khi làm viêc với Vim để nâng cao tốc độ và năng suất công việc. Trong bài viết tiếp theo, mình sẽ hướng dẫn cho các bạn cách tùy chỉnh Vim theo ý muốn và giới thiệu mốt số plugin hay cần thiết nhé.

Don't forget to rate and share :D
