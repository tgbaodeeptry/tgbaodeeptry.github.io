---
layout: post
title: Hạn chế tấn công web với Cloudflare
thumbnail-img: /assets/posts/han-che-tan-cong-web/thumb.jpg
tags: [cloudflare]
---

Một website được gọi là hoàn thiện chỉ khi nó thỏa mãn được những tiêu chí về tốc độ, sự linh hoạt, giao diện, ... Và một phần quan trọng đó là khả năng ngăn chặn các cuộc tấn công từ chối dịch vụ có quy mô từ bên ngoài (DOS). 

Cùng với sự phát triển Internet, số lượng website ngày càng gia tăng một cách nhanh chóng, tuy nhiên vấn đề bảo vệ website khỏi cuộc tấn công vẫn chưa được quan tâm. Những vấn đề này chỉ khi xảy ra, mọi người mới bắt đầu chú trọng tới, nhưng khi đó, nó đã gây tổn hại rất lớn đến hệ thống rồi !

Trong bài viết này, mình sẽ giới thiệu cho các bạn hiểu về một cuộc tấn công DDOS là như thế nào, và cách hạn chế nó nhé :D

### Tấn công từ chối dịch vụ là gì?

Tấn công từ chối dịch vụ (DOS - Denial of Service) hay Tấn công từ chối dịch vụ phân tán (DDOS - Distributed Denial of Service). L à một nỗ lực làm cho những người dùng không thể sử dụng tài nguyên của một máy tính. Mặc dù phương tiện để tiến hành, động cơ, mục tiêu của tấn công từ chối dịch vụ có thể khác nhau, nhưng nói chung nó gồm có sự phối hợp, sự cố gắng ác ý của một người hay nhiều người để một trang, hay hệ thống mạng không thể sử dụng, làm gián đoạn, hoặc làm cho hệ thống đó chậm đi một cách đáng kể với người dùng bình thường, bằng cách làm quá tải tài nguyên của hệ thống.

![](https://codelearn.io/Media/Default/Users/CoderToDev/cloudflare/v%C3%AD-d%E1%BB%A5-v%E1%BB%81-t%E1%BA%A5n-c%C3%B4ng-ddos%20(1).png)

Chúng ta có thể hiểu nôm na rằng: Tấn công từ chối dịch vụ là việc sử dụng các botnet ( máy tính khác ) trên toàn thế giới, cùng lúc gửi request tới một website, một địa chỉ ip nào đó. Làm cho máy chủ không thể phản hồi kịp các request đó, làm cho máy chủ bị tắc nghẽn về băng thông, tài nguyên của máy. Từ đó khiến cho website không thế đáp ứng yêu cầu người dùng, gây ảnh hưởng tới trải nghiệm người dùng, gây ảnh hưởng tới kinh tế, lợi nhuận của các doanh nghiệp.

### Cách phòng chống, hạn chế

Chúng ta có nhiều cách để hạn chế ảnh hưởng của các cuộc tấn công từ chối dịch vụ:

*   Giới hạn số lượng request mỗi ip trong một khoảng thời gian nào đó
*   Thiết lập Firewall, để chặn sử dụng từ các backlist ip, từ các country
*   Sử dụng hệ thống proxy để ẩn ip của máy chủ
*   Hạn chế các yêu cầu trong trong giai đoạn cao điểm
*   Phân tích traffic để có những biện pháp phù hợp
*   Và còn nhiều hơn thế nữa ...

Bên cạnh đó, chúng ta còn có thể sử dụng  `Cloudflare`, một dịch vụ bảo vệ website được sử dụng phố biến, với 2 phiên bản: miễn phí và bản trả phí. Dù là bản miễn phí, nhưng nó cũng tỏa ra hiệu quả trong việc hạn chế các cuộc tấn công từ chối dịch vụ ở mức vừa và trung bình. Chúng ta hãy cùng tìm hiểu nó nhé

### Đăng ký tài khoản Cloudflare

Đó là điều hiển nhiên rồi. có làm mới có ... thế sử dụng nhé :)

1, Truy cập trang địa chỉ chính của  [Cloudflare](https://www.cloudflare.com/). Sau đó nhấn  Sign Up để đăng ký

![](https://codelearn.io/Media/Default/Users/CoderToDev/cloudflare/Screenshot%202020-06-20%2022.03.01.jpg)

2\. Nhập địa chỉ email, mật khẩu bạn muốn đăng ký

![](https://codelearn.io/Media/Default/Users/CoderToDev/cloudflare/Screenshot%202020-06-20%2022.04.46.jpg)

3\. Nhập tên miền mà bạn muốn đăng ký với dịch vụ Cloudflare

![](https://codelearn.io/Media/Default/Users/CoderToDev/cloudflare/Screenshot%202020-06-20%2022.08.21.jpg)

4\. Chọn gói cloudflare (ở đây mình chọn miễn phí, vì mình .. không có tiền :v)

![](https://codelearn.io/Media/Default/Users/CoderToDev/cloudflare/Screenshot%202020-06-20%2022.11.24.jpg)

5\. Sau đó nhấn nút Continue để tiếp tục, vì mấy cái đó mình config sau cũng được

![](https://codelearn.io/Media/Default/Users/CoderToDev/cloudflare/Screenshot%202020-06-20%2022.13.45.jpg)

6\. Thay đổi nameserver của trang bạn đăng ký tên miền, thành nameserver của cloudflare

![](https://codelearn.io/Media/Default/Users/CoderToDev/cloudflare/Screenshot%202020-06-20%2022.21.20.jpg)

Sau đó ta nhấn Done để hoàn thành nhé :D

### Tùy chỉnh Cloudflare để hạn chế DDOS

Sau khi các bạn đăng ký tài khoản thành công, thì chúng ta đã được 80% rồi ấy, phần còn lại chỉ cần config một tý là sẽ OK ngay thôi

![](https://codelearn.io/Media/Default/Users/CoderToDev/cloudflare/Screenshot%202020-06-21%2012.27.52.jpg)

Trong Cloudflare có khá nhiều tính năng khá là hay như phân tích traffic, ssl miễn phí, firewall, cache để optimize tốc độ, ... ngoài ra chúng ta còn có thể cài thêm Apps cho web, giống như việc cài plugin với wordpress vậy  

![](https://codelearn.io/Media/Default/Users/CoderToDev/cloudflare/Screenshot%20from%202020-06-21%2012-33-48.png)

Các bạn có thể tự tìm hiểu nhé, trong phạm vi bài này mình sẽ chỉ cho bạn một cách chặn tấn công DOS một cách hiệu quả với Security Level.

1\. Đầu tiên, các bạn truy cập vào mục Overview và click chọn Under Attack Mode

![](https://codelearn.io/Media/Default/Users/CoderToDev/cloudflare/Screenshot%202020-06-21%2012.41.41.jpg)

2\. Sau khi bật xong, mọi thứ sẽ như thế này

![](https://codelearn.io/Media/Default/Users/CoderToDev/cloudflare/Screenshot%202020-06-21%2012.42.55.jpg)

3\. Vậy là đã thành công rồi ấy, bây giờ mọi người dùng khi truy cập vào web sẽ phải chờ 5s để bên Cloudflare kiểm tra có phải người dùng ảo không. Từ đó có thể giảm gánh nặng về băng thông, bộ nhớ cho website của bạn 

![](https://codelearn.io/Media/Default/Users/CoderToDev/cloudflare/under-attack-mode_enabled.gif)

Mặc dù nhìn nó khá phiền khi phải chờ 5s, nhưng các bạn có thể so sánh trước khi bật và khi bật xong, mọi thứ sẽ rất khác. Nếu các bạn thấy vẫn không chặn được, các bạn có thể thử thêm config Firewall hoặc là mua phiên bản có phí để được mở thêm nhiều chức năng hơn nhé. 

### Tổng kết

Qua bài viết này mình đã giới thiệu sơ cho các bạn về Cloudflare, một dịch vụ phổ biến dùng trong bảo vệ website khỏi các cuộc tấn công quy mô lớn. Theo như mình được biết thì  codelearn.io cũng đang sử dụng dịch vụ Cloudflare ấy, như vậy bạn có thể hiểu được sự cần thiết và sức mạnh của Cloudflare rồi nhỉ ~. Nếu các bạn gặp khó khăn trong việc setup Cloudflare, các bạn có thêm comment bên dưới hoặc tham gia  [cộng đồng Cloudflare](https://community.cloudflare.com/) để được hỗ trợ nhé <3

Nếu các bạn thấy bài viết này hay thì đừng ngại rate 5\* cho mình nhé :D
