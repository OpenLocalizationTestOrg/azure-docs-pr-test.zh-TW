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
ms.openlocfilehash: e14796c37ab0c30d948b6f783dac80059375afa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a>建立應用程式 (快速)
現在您需要在應用程式中 hello tooregister *Microsoft 應用程式註冊入口網站*:
1. 註冊您的應用程式，透過 hello [Microsoft 應用程式註冊入口網站](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure)
2.  輸入應用程式的名稱和您的電子郵件
3.  請確定已選取 hello 引導式安裝選項
4.  遵循 hello 指示 tooobtain hello 應用程式識別碼，並將它貼到您的程式碼

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>新增應用程式註冊資訊 tooyour 方案 （進階）
現在您需要在應用程式中 hello tooregister *Microsoft 應用程式註冊入口網站*:
1. 移 toohello [Microsoft 應用程式註冊入口網站](https://apps.dev.microsoft.com/portal/register-app)tooregister 應用程式
2. 輸入應用程式的名稱和您的電子郵件 
3. 請確定未引導式的安裝程式的 hello 選項
4. 按一下 `Add Platform`，然後選取 `Native Application` 並按下 [儲存]
5.  開啟 `MainActivity` (在 `app` > `java` > *`{host}.{namespace}`* 底下)
6.  取代 hello *[輸入 hello 應用程式的程式識別碼]* hello 一行開頭`final static String CLIENT_ID`hello 您剛登錄的應用程式識別碼：

```java
final static String CLIENT_ID = "[Enter hello application Id here]";
```
<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
開啟`AndroidManifest.xml`(下`app`  >  `manifests`) 新增 hello 太下列活動`manifest\application`節點。 如此會註冊`BrowserTabActivity`tooallow hello OS tooresume 完成 hello 驗證之後，應用程式：
</li>
</ol>

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
<!-- Workaround for Docs conversion bug -->
<ol start="8">
<li>
在 hello `BrowserTabActivity`，取代`[Enter hello application Id here]`hello 應用程式識別碼。
</li>
</ol>
