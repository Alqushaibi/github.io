---
layout: post
title: Cấu trúc cơ bản của một Chrome Extension
date: 2023-09-25 01:00 +0700
description:
tag:
  - extension
image: /images/extension-architecture.png
---

![](https://wd.imgix.net/image/BrQidfK9jaQyIHwdw91aVpkPiib2/CNDAVsTnJeSskIXVnSQV.png?auto=format)

Để xây dựng một browser extension, bạn cần hiểu về cấu trúc cơ bản của nó.

**1. manifest.json:**
manifest.json là một tệp cấu hình chính của tiện ích. Nó chứa các thông tin cơ bản như tên, phiên bản, quyền truy cập và các tài nguyên khác. Đây cũng là nơi bạn định nghĩa các UI component (như icon, popup, options page) và các sự kiện

**2. popup.html**
popup.html là UI component nhỏ xuất hiện khi người dùng nhấp vào biểu tượng tiện ích trên thanh công cụ. Đây thường là giao diện tương tác ngắn gọn, thường dùng để hiển thị thông tin hoặc tùy chọn nhanh.

**3. background.js:**
background.js là một tệp JavaScript chạy trong background và xử lý các sự kiện không thể thực hiện trực tiếp từ popup.html. hay UI. Đây là nơi bạn thực hiện các function phức tạp như quản lý dữ liệu và tương tác với các API của trình duyệt.

**4. content_scripts:**
content_scripts chứa các mã nguồn JavaScript và CSS sẽ chạy trực tiếp trên trang web mà tiện ích của bạn được kích hoạt. Điều này cho phép tiện ích tương tác trực tiếp với nội dung của trang. Mặt khác, khi website của user load thì browser sẽ inject content script của bạn vào website của end user với độ ưu tiên cao nhất để bạn có thể override nội dung theo ý muốn.

**5. icons:**
Thư mục icons chứa các icon đại diện cho tiện ích của bạn. Chrome sẽ sử dụng các biểu tượng này để hiển thị trên thanh công cụ và trong quản lý tiện ích.

**6. options.html: Trang Cài Đặt**
Nếu tiện ích của bạn có các tùy chọn cài đặt, bạn có thể tạo options.html. Đây là nơi người dùng có thể điều chỉnh cài đặt theo ý muốn.

**7. permissions:**
Trong manifest.json, bạn sẽ define rõ các quyền truy cập mà tiện ích của bạn cần. Điều này bảo đảm rằng tiện ích chỉ có thể truy cập vào thông tin cần thiết mà không vi phạm quyền riêng tư của người dùng.
Chúc các bạn sớm làm được một extension hữu ích : D
