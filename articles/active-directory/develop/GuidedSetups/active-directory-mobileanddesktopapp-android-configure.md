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
## <a name="create-an-application-express"></a><span data-ttu-id="5843a-103">建立應用程式 (快速)</span><span class="sxs-lookup"><span data-stu-id="5843a-103">Create an application (Express)</span></span>
<span data-ttu-id="5843a-104">現在您需要在應用程式中 hello tooregister *Microsoft 應用程式註冊入口網站*:</span><span class="sxs-lookup"><span data-stu-id="5843a-104">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="5843a-105">註冊您的應用程式，透過 hello [Microsoft 應用程式註冊入口網站](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure)</span><span class="sxs-lookup"><span data-stu-id="5843a-105">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure)</span></span>
2.  <span data-ttu-id="5843a-106">輸入應用程式的名稱和您的電子郵件</span><span class="sxs-lookup"><span data-stu-id="5843a-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="5843a-107">請確定已選取 hello 引導式安裝選項</span><span class="sxs-lookup"><span data-stu-id="5843a-107">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="5843a-108">遵循 hello 指示 tooobtain hello 應用程式識別碼，並將它貼到您的程式碼</span><span class="sxs-lookup"><span data-stu-id="5843a-108">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="5843a-109">新增應用程式註冊資訊 tooyour 方案 （進階）</span><span class="sxs-lookup"><span data-stu-id="5843a-109">Add your application registration information tooyour solution (Advanced)</span></span>
<span data-ttu-id="5843a-110">現在您需要在應用程式中 hello tooregister *Microsoft 應用程式註冊入口網站*:</span><span class="sxs-lookup"><span data-stu-id="5843a-110">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="5843a-111">移 toohello [Microsoft 應用程式註冊入口網站](https://apps.dev.microsoft.com/portal/register-app)tooregister 應用程式</span><span class="sxs-lookup"><span data-stu-id="5843a-111">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="5843a-112">輸入應用程式的名稱和您的電子郵件</span><span class="sxs-lookup"><span data-stu-id="5843a-112">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="5843a-113">請確定未引導式的安裝程式的 hello 選項</span><span class="sxs-lookup"><span data-stu-id="5843a-113">Make sure hello option for Guided Setup is unchecked</span></span>
4. <span data-ttu-id="5843a-114">按一下 `Add Platform`，然後選取 `Native Application` 並按下 [儲存]</span><span class="sxs-lookup"><span data-stu-id="5843a-114">Click `Add Platform`, then select `Native Application` and hit Save</span></span>
5.  <span data-ttu-id="5843a-115">開啟 `MainActivity` (在 `app` > `java` > *`{host}.{namespace}`* 底下)</span><span class="sxs-lookup"><span data-stu-id="5843a-115">Open `MainActivity` (under `app` > `java` > *`{host}.{namespace}`*)</span></span>
6.  <span data-ttu-id="5843a-116">取代 hello *[輸入 hello 應用程式的程式識別碼]* hello 一行開頭`final static String CLIENT_ID`hello 您剛登錄的應用程式識別碼：</span><span class="sxs-lookup"><span data-stu-id="5843a-116">Replace hello *[Enter hello application Id here]* in hello line starting with `final static String CLIENT_ID` with hello application ID you just registered:</span></span>

```java
final static String CLIENT_ID = "[Enter hello application Id here]";
```
<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
<span data-ttu-id="5843a-117">開啟`AndroidManifest.xml`(下`app`  >  `manifests`) 新增 hello 太下列活動`manifest\application`節點。</span><span class="sxs-lookup"><span data-stu-id="5843a-117">Open `AndroidManifest.xml` (under `app` > `manifests`) Add hello following activity too`manifest\application` node.</span></span> <span data-ttu-id="5843a-118">如此會註冊`BrowserTabActivity`tooallow hello OS tooresume 完成 hello 驗證之後，應用程式：</span><span class="sxs-lookup"><span data-stu-id="5843a-118">This registers a `BrowserTabActivity` tooallow hello OS tooresume your application after completing hello authentication:</span></span>
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
<span data-ttu-id="5843a-119">在 hello `BrowserTabActivity`，取代`[Enter hello application Id here]`hello 應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="5843a-119">In hello `BrowserTabActivity`, replace `[Enter hello application Id here]` with hello application ID.</span></span>
</li>
</ol>
