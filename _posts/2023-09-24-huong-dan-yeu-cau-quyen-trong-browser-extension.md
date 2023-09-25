---
layout: post
title: Hướng dẫn yêu cầu quyền trong browser extension
date: 2023-09-25 01:00 +0700
description:
tag:
  - extension
image: /cara-memperbarui-fork-repository/repo.png
---

# Hướng Dẫn Yêu Cầu Quyền Truy Cập trong Chrome Extension

Khi phát triển extension, có những tình huống mà bạn cần yêu cầu quyền truy cập từ người dùng để thực hiện các tính năng cần thiết. Hôm nay mình sẽ hướng dẫn mọi người cách yêu cầu quyền truy cập một cách hợp lý và tránh annoy người dùng.

## 1. **Thêm permissions vào manifest.json**

Đầu tiên, bạn cần chỉ định quyền truy cập mà tiện ích của bạn cần trong tệp `manifest.json`.

```json
{
  "manifest_version": 2,
  "name": "My Chrome Extension",
  "version": "1.0",
  "permissions": ["storage", "activeTab"],
  "browser_action": {
    "default_popup": "popup.html",
    "default_icon": {
      "16": "images/icon16.png",
      "48": "images/icon48.png",
      "128": "images/icon128.png"
    }
  },
  "icons": {
    "16": "images/icon16.png",
    "48": "images/icon48.png",
    "128": "images/icon128.png"
  }
}
```

Trong ví dụ trên, tiện ích của bạn yêu cầu quyền truy cập `storage` và `activeTab`.
Bạn tham khảo tất cả permission tại [đây](https://developer.chrome.com/docs/extensions/mv3/declare_permissions/#permissions) :

## 2. **Yêu Cầu Quyền Truy Cập từ Người Dùng**

### a. Trong Popup

Nếu bạn muốn yêu cầu quyền truy cập trong popup của extension, bạn cần sử dụng JavaScript để tương tác với API `chrome.permissions.request`.

```javascript
document
  .getElementById("requestPermissionButton")
  .addEventListener("click", function () {
    chrome.permissions.request(
      {
        permissions: ["storage"],
        origins: ["https://example.com/"]
      },
      function (granted) {
        if (granted) {
          console.log("Quyền truy cập đã được cấp!");
        } else {
          console.log("Người dùng từ chối quyền truy cập.");
        }
      }
    );
  });
```

### b. Trong Background

Nếu bạn muốn yêu cầu quyền truy cập từ background script, bạn cũng sử dụng API `chrome.permissions.request`.

```javascript
chrome.runtime.onMessage.addListener(function (request, sender, sendResponse) {
  if (request.type == "requestPermission") {
    chrome.permissions.request(
      {
        permissions: ["storage"],
        origins: ["https://example.com/"]
      },
      function (granted) {
        if (granted) {
          console.log("Quyền truy cập đã được cấp!");
        } else {
          console.log("Người dùng từ chối quyền truy cập.");
        }
      }
    );
  }
});
```

## 3. **Xử Lý Khi Người Dùng Đồng Ý hoặc Từ Chối**

Sau khi người dùng đồng ý hoặc từ chối quyền truy cập, bạn nên xử lý tùy theo trường hợp để có một trải nghiệm người dùng tốt nhất. Mặt khác, bạn cần giải thích cho người dùng hiểu rõ để họ có thể chấp nhận request của bạn một cách tự tin nhất. Rõ ràng, nếu từ chối thì extension của bạn đã mất đi vài tính năng quan trọng.

## 4. **Chú Ý:**

- **Thận Trọng Khi Yêu Cầu Quyền Truy Cập:** Luôn cung cấp lý do cụ thể khi yêu cầu quyền truy cập và đảm bảo rằng tiện ích của bạn không vi phạm quyền riêng tư của người dùng.

- **Xử Lý Tốt Cả Trường Hợp Người Dùng Từ Chối:** Nếu người dùng từ chối quyền truy cập, hãy cung cấp thông báo hoặc hướng dẫn để giúp họ cấp quyền truy cập lại sau này.

Như vậy, với các bước trên, bạn có thể yêu cầu quyền truy cập một cách hợp lý trong browser extension của mình. Hãy nhớ luôn tôn trọng quyền riêng tư người dùng để mang lại một trải nghiệm tốt nhất có thể.

Happy Coding !!
