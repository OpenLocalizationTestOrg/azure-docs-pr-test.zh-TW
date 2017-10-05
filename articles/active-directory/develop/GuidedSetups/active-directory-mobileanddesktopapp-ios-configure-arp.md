---
title: "Azure AD v2 iOS 快速入門 - 設定 (ARP) | Microsoft Docs"
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
ms.openlocfilehash: 50cb4a2803b6aebe8b39ec9fb02da2293c1065fa
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
## <a name="add-the-applications-registration-information-to-your-app"></a><span data-ttu-id="f3a8e-103">將應用程式的註冊資訊新增到您的應用程式</span><span class="sxs-lookup"><span data-stu-id="f3a8e-103">Add the application’s registration information to your app</span></span>

<span data-ttu-id="f3a8e-104">在這個步驟中，您需要將應用程式識別碼新增到您的專案：</span><span class="sxs-lookup"><span data-stu-id="f3a8e-104">In this step, you need to add the Application Id to your project:</span></span>

1.  <span data-ttu-id="f3a8e-105">在 `ViewController.swift` 中，將開頭為 '`let kClientID`' 的那一行取代為：</span><span class="sxs-lookup"><span data-stu-id="f3a8e-105">In `ViewController.swift`, replace the line starting with '`let kClientID`' with:</span></span>
```swift
let kClientID = "[Enter the application Id here]"
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="f3a8e-106">按住 Ctrl 鍵並按一下 <code>Info.plist</code> 以顯示內容功能表，然後按一下：<code>Open As</code> > <code>Source Code</code>
</span><span class="sxs-lookup"><span data-stu-id="f3a8e-106">Control+click <code>Info.plist</code> to bring up the contextual menu, and then click: <code>Open As</code> > <code>Source Code</code>
</span></span></li>
<li>
<span data-ttu-id="f3a8e-107">在 <code>dict</code> 根節點下，新增下列項目：</span><span class="sxs-lookup"><span data-stu-id="f3a8e-107">Under the <code>dict</code> root node, add the following:</span></span>
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
            <string>msal[Enter the application Id here]</string>
            <string>auth</string>
        </array>
    </dict>
</array>
```
