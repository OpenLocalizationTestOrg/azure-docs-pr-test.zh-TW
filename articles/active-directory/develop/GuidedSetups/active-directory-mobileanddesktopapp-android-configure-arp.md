---
title: "aaaAzure AD v2 Android 入門-設定 |Microsoft 文件"
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
ms.openlocfilehash: eaa41805c92212154ee8d51d3eb3aee1202eef1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
## <a name="add-hello-applications-registration-information-tooyour-app"></a><span data-ttu-id="27539-103">新增 hello 應用程式的註冊資訊 tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="27539-103">Add hello application’s registration information tooyour app</span></span>

<span data-ttu-id="27539-104">在此步驟中，您需要 tooadd hello 用戶端識別碼 tooyour 專案。</span><span class="sxs-lookup"><span data-stu-id="27539-104">In this step, you need tooadd hello Client ID tooyour project.</span></span>

1.  <span data-ttu-id="27539-105">開啟 `MainActivity` (在 `app` > `java` > *`{host}.{namespace}`* 底下)</span><span class="sxs-lookup"><span data-stu-id="27539-105">Open `MainActivity` (under `app` > `java` > *`{host}.{namespace}`*)</span></span>
2.  <span data-ttu-id="27539-106">取代 hello 一行開頭`final static String CLIENT_ID`使用：</span><span class="sxs-lookup"><span data-stu-id="27539-106">Replace hello line starting with `final static String CLIENT_ID` with:</span></span>
```java
final static String CLIENT_ID = "[Enter hello application Id here]";
```
3. <span data-ttu-id="27539-107">開啟：`app` > `manifests` > `AndroidManifest.xml`</span><span class="sxs-lookup"><span data-stu-id="27539-107">Open: `app` > `manifests` > `AndroidManifest.xml`</span></span>
4. <span data-ttu-id="27539-108">新增下列活動太 hello`manifest\application`節點。</span><span class="sxs-lookup"><span data-stu-id="27539-108">Add hello following activity too`manifest\application` node.</span></span> <span data-ttu-id="27539-109">此暫存器`BrowserTabActivity`tooallow hello OS tooresume 完成 hello 驗證之後，應用程式：</span><span class="sxs-lookup"><span data-stu-id="27539-109">This register a `BrowserTabActivity` tooallow hello OS tooresume your application after completing hello authentication:</span></span>

```xml
<!--Intent filter toocapture System Browser calling back tooour app after Sign In-->
<activity
    android:name="com.microsoft.identity.client.BrowserTabActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />

        <!--Add in your scheme/host from registered redirect URI-->
        <!--By default, hello scheme should be similar too'msal[appId]' -->
        <data android:scheme="msal[Enter hello application Id here]"
            android:host="auth" />
    </intent-filter>
</activity>
```

### <a name="what-is-next"></a><span data-ttu-id="27539-110">下一步</span><span class="sxs-lookup"><span data-stu-id="27539-110">What is Next</span></span>

[<span data-ttu-id="27539-111">測試和驗證</span><span class="sxs-lookup"><span data-stu-id="27539-111">Test and Validate</span></span>](active-directory-mobileanddesktopapp-android-test.md)
