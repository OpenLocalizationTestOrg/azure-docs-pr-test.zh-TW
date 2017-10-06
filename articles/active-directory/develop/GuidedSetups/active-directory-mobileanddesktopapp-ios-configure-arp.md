---
title: "aaaAzure AD v2 iOS 入門-設定 (ARP) |Microsoft 文件"
description: "iOS (Swift) 應用程式如何呼叫需要來自 Azure Active Directory v2 端點之存取權杖的 API"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: e5087e13160243d808b1d02771fa66fb332cfad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
## <a name="add-hello-applications-registration-information-tooyour-app"></a>新增 hello 應用程式的註冊資訊 tooyour 應用程式

在此步驟中，您需要 tooadd hello 應用程式識別碼 tooyour 專案：

1.  在`ViewController.swift`，取代 hello 一行開頭為 '`let kClientID`' 具有：
```swift
let kClientID = "[Enter hello application Id here]"
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
控制並按一下滑鼠左鍵<code>Info.plist</code>toobring 向上 hello] 內容功能表，然後按一下 [: <code>Open As</code>> <code>Source Code</code>
</li>
<li>
在 [hello<code>dict</code>根節點，加入下列 hello:
</li>
</ol>

```xml
<key>CFBundleURLTypes</key>
<array>
    <dict>
        <key>CFBundleTypeRole</key>
        <string>Editor</string>
        <key>CFBundleURLName</key>
        <string>$(PRODUCT_BUNDLE_IDENTIFIER)</string>
        <key>CFBundleURLSchemes</key>
        <array>
            <string>msal[Enter hello application Id here]</string>
            <string>auth</string>
        </array>
    </dict>
</array>
```
