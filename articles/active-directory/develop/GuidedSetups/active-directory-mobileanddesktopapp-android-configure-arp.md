---
title: "Azure AD v2 Android 快速入門 - 設定 | Microsoft Docs"
description: "Android 應用程式如何取得存取權杖，以及如何呼叫 Microsoft 圖形 API，或呼叫需要來自 Azure Active Directory v2 端點之存取權杖的 API"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: c09937582118ebcc5b8cbc1f43a0a2019f2f7a89
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
## <a name="add-the-applications-registration-information-to-your-app"></a><span data-ttu-id="a5105-103">將應用程式的註冊資訊新增到您的應用程式</span><span class="sxs-lookup"><span data-stu-id="a5105-103">Add the application’s registration information to your app</span></span>

<span data-ttu-id="a5105-104">在這個步驟中，您需要將用戶端識別碼新增到您的專案。</span><span class="sxs-lookup"><span data-stu-id="a5105-104">In this step, you need to add the Client ID to your project.</span></span>

1.  <span data-ttu-id="a5105-105">開啟 `MainActivity` (在 `app` > `java` > *`{host}.{namespace}`* 底下)</span><span class="sxs-lookup"><span data-stu-id="a5105-105">Open `MainActivity` (under `app` > `java` > *`{host}.{namespace}`*)</span></span>
2.  <span data-ttu-id="a5105-106">將開頭為 `final static String CLIENT_ID` 的那一行取代為：</span><span class="sxs-lookup"><span data-stu-id="a5105-106">Replace the line starting with `final static String CLIENT_ID` with:</span></span>
```java
final static String CLIENT_ID = "[Enter the application Id here]";
```
3. <span data-ttu-id="a5105-107">開啟：`app` > `manifests` > `AndroidManifest.xml`</span><span class="sxs-lookup"><span data-stu-id="a5105-107">Open: `app` > `manifests` > `AndroidManifest.xml`</span></span>
4. <span data-ttu-id="a5105-108">將下列活動新增至 `manifest\application` 節點。</span><span class="sxs-lookup"><span data-stu-id="a5105-108">Add the following activity to `manifest\application` node.</span></span> <span data-ttu-id="a5105-109">這會註冊 `BrowserTabActivity`，以允許 OS 在完成驗證之後繼續執行您的應用程式：</span><span class="sxs-lookup"><span data-stu-id="a5105-109">This register a `BrowserTabActivity` to allow the OS to resume your application after completing the authentication:</span></span>

```xml
<!--Intent filter to capture System Browser calling back to our app after Sign In-->
<activity
    android:name="com.microsoft.identity.client.BrowserTabActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />

        <!--Add in your scheme/host from registered redirect URI-->
        <!--By default, the scheme should be similar to 'msal[appId]' -->
        <data android:scheme="msal[Enter the application Id here]"
            android:host="auth" />
    </intent-filter>
</activity>
```

### <a name="what-is-next"></a><span data-ttu-id="a5105-110">下一步</span><span class="sxs-lookup"><span data-stu-id="a5105-110">What is Next</span></span>

[<span data-ttu-id="a5105-111">測試和驗證</span><span class="sxs-lookup"><span data-stu-id="a5105-111">Test and Validate</span></span>](active-directory-mobileanddesktopapp-android-test.md)
