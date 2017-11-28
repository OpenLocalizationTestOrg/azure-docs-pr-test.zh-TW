---
title: "Azure AD v2 iOS 快速入門 - 設定 | Microsoft Docs"
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
ms.openlocfilehash: 0ebca65585fc87bd4a85ba092cd423fce9540f58
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="1f13e-103">建立應用程式 (快速)</span><span class="sxs-lookup"><span data-stu-id="1f13e-103">Create an application (Express)</span></span>
<span data-ttu-id="1f13e-104">現在您需要在「Microsoft 應用程式註冊入口網站」註冊應用程式：</span><span class="sxs-lookup"><span data-stu-id="1f13e-104">Now you need to register your application in the *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="1f13e-105">透過 [Microsoft 應用程式註冊入口網站 (英文)](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure) 註冊您的應用程式</span><span class="sxs-lookup"><span data-stu-id="1f13e-105">Register your application via the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure)</span></span>
2.  <span data-ttu-id="1f13e-106">輸入應用程式的名稱和您的電子郵件</span><span class="sxs-lookup"><span data-stu-id="1f13e-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="1f13e-107">確定已選取 [Guided Setup (引導式設定)] 選項</span><span class="sxs-lookup"><span data-stu-id="1f13e-107">Make sure the option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="1f13e-108">依照指示取得應用程式識別碼並貼到您的程式碼中</span><span class="sxs-lookup"><span data-stu-id="1f13e-108">Follow the instructions to obtain the application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-to-your-solution-advanced"></a><span data-ttu-id="1f13e-109">將您的應用程式註冊資訊新增到方案 (進階)</span><span class="sxs-lookup"><span data-stu-id="1f13e-109">Add your application registration information to your solution (Advanced)</span></span>

1.  <span data-ttu-id="1f13e-110">移至 [Microsoft 應用程式註冊入口網站](https://apps.dev.microsoft.com/portal/register-app)</span><span class="sxs-lookup"><span data-stu-id="1f13e-110">Go to [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app)</span></span>
2.  <span data-ttu-id="1f13e-111">輸入應用程式的名稱和您的電子郵件</span><span class="sxs-lookup"><span data-stu-id="1f13e-111">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="1f13e-112">確定已取消選取 [Guided Setup (引導式設定)] 選項</span><span class="sxs-lookup"><span data-stu-id="1f13e-112">Make sure the option for Guided Setup is unchecked</span></span>
4.  <span data-ttu-id="1f13e-113">按一下 [`Add Platform`]，然後選取 [`Native Application`] 並按一下 [`Save`]</span><span class="sxs-lookup"><span data-stu-id="1f13e-113">Click `Add Platform`, then select `Native Application` and click `Save`</span></span>
5.  <span data-ttu-id="1f13e-114">返回至 Xcode。</span><span class="sxs-lookup"><span data-stu-id="1f13e-114">Go back to Xcode.</span></span> <span data-ttu-id="1f13e-115">在 `ViewController.swift` 中，以您剛剛註冊的應用程式識別碼取代開頭為 '`let kClientID`' 的行：</span><span class="sxs-lookup"><span data-stu-id="1f13e-115">In `ViewController.swift`, replace the line starting with '`let kClientID`' with the application ID you just registered:</span></span>

```swift
let kClientID = "Your_Application_Id_Here"
```

<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
<span data-ttu-id="1f13e-116">按住 Ctrl 鍵並按一下 <code>Info.plist</code> 以顯示內容功能表，然後按一下：<code>Open As</code> > <code>Source Code</code>
</span><span class="sxs-lookup"><span data-stu-id="1f13e-116">Control+click <code>Info.plist</code> to bring up the contextual menu, and then click: <code>Open As</code> > <code>Source Code</code>
</span></span></li>
<li>
<span data-ttu-id="1f13e-117">在 <code>dict</code> 根節點下，新增下列項目：</span><span class="sxs-lookup"><span data-stu-id="1f13e-117">Under the <code>dict</code> root node, add the following:</span></span>
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
<span data-ttu-id="1f13e-118">用您剛剛註冊的應用程式識別碼取代 <i><code>[Your_Application_Id_Here]</code></i></span><span class="sxs-lookup"><span data-stu-id="1f13e-118">Replace <i><code>[Your_Application_Id_Here]</code></i> with the Application Id you just registered</span></span>
</li>
</ol>
