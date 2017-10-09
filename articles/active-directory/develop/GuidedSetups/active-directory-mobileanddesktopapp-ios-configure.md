---
title: "aaaAzure AD v2 iOS 入門-設定 |Microsoft 文件"
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
ms.openlocfilehash: 537cc7f0de6cd947fe340566c9e93f8bb08d57a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a>建立應用程式 (快速)
現在您需要在應用程式中 hello tooregister *Microsoft 應用程式註冊入口網站*:
1. 註冊您的應用程式，透過 hello [Microsoft 應用程式註冊入口網站](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure)
2.  輸入應用程式的名稱和您的電子郵件
3.  請確定已選取 hello 引導式安裝選項
4.  遵循 hello 指示 tooobtain hello 應用程式識別碼，並將它貼到您的程式碼

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>新增應用程式註冊資訊 tooyour 方案 （進階）

1.  跳過[Microsoft 應用程式註冊入口網站](https://apps.dev.microsoft.com/portal/register-app)
2.  輸入應用程式的名稱和您的電子郵件
3.  請確定未引導式的安裝程式的 hello 選項
4.  按一下 [`Add Platform`]，然後選取 [`Native Application`] 並按一下 [`Save`]
5.  返回 tooXcode。 在`ViewController.swift`，取代 hello 一行開頭為 '`let kClientID`' hello 您剛登錄的應用程式識別碼：

```swift
let kClientID = "Your_Application_Id_Here"
```

<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
控制並按一下滑鼠左鍵<code>Info.plist</code>toobring 向上 hello 內容功能表，然後按一下: <code>Open As</code>> <code>Source Code</code>
</li>
<li>
在 hello<code>dict</code>根節點，加入下列 hello:
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
            <string>msal[Your_Application_Id_Here]</string>
            <string>auth</string>
        </array>
    </dict>
</array>
```
<ol start="8">
<li>
取代<i> <code>[Your_Application_Id_Here]</code> </i>以 hello 您剛登錄的應用程式識別碼
</li>
</ol>
