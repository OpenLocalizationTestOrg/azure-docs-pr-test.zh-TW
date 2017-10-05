---
title: "Azure AD v2 Windows Desktop 快速入門 - 測試 | Microsoft Docs"
description: "Windows Desktop .NET (XAML) 應用程式如何呼叫需要來自 Azure Active Directory v2 端點之存取權杖的 API"
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
ms.openlocfilehash: 972cc48057c13271d725b0c973c3ccf651ad27c4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
## <a name="test-your-code"></a><span data-ttu-id="bbaa8-103">測試您的程式碼</span><span class="sxs-lookup"><span data-stu-id="bbaa8-103">Test your code</span></span>

<span data-ttu-id="bbaa8-104">為測試您的應用程式，請按 `F5` 以在 Visual Studio 中執行專案。</span><span class="sxs-lookup"><span data-stu-id="bbaa8-104">In order to test your application, press `F5` to run your project in Visual Studio.</span></span> <span data-ttu-id="bbaa8-105">您的主視窗應會出現：</span><span class="sxs-lookup"><span data-stu-id="bbaa8-105">Your Main Window should appear:</span></span>

![範例螢幕擷取畫面](media/active-directory-mobileanddesktopapp-windowsdesktop-test/samplescreenshot.png)

<span data-ttu-id="bbaa8-107">當您準備好進行測試時，請按一下 [呼叫 Microsoft 圖形 API]，然後使用 Microsoft Azure Active Directory (組織帳戶) 或 Microsoft 帳戶 (live.com、outlook.com) 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="bbaa8-107">When you're ready to test, click *Call Microsoft Graph API* and use a Microsoft Azure Active Directory (organizational account) or a Microsoft Account (live.com, outlook.com) account to sign in.</span></span> <span data-ttu-id="bbaa8-108">如果這是第一次進行此操作，系統會顯示視窗要求使用者登入：</span><span class="sxs-lookup"><span data-stu-id="bbaa8-108">It it is the first time, you will see a window asking user to sign in:</span></span>

![登入](media/active-directory-mobileanddesktopapp-windowsdesktop-test/signinscreenshot.png)

### <a name="consent"></a><span data-ttu-id="bbaa8-110">同意</span><span class="sxs-lookup"><span data-stu-id="bbaa8-110">Consent</span></span>
<span data-ttu-id="bbaa8-111">第一次登入應用程式時，系統會向您顯示如下所示的類似同意畫面，其中包含您必須明確接受的事項：</span><span class="sxs-lookup"><span data-stu-id="bbaa8-111">The first time you sign in to your application, you will be presented with a consent screen similar to the below, where you need to explicitly accept:</span></span>

![同意畫面](media/active-directory-mobileanddesktopapp-windowsdesktop-test/consentscreen.png)

### <a name="expected-results"></a><span data-ttu-id="bbaa8-113">預期的結果</span><span class="sxs-lookup"><span data-stu-id="bbaa8-113">Expected results</span></span>
<span data-ttu-id="bbaa8-114">您應該會在 [API 呼叫結果] 畫面上看到由 Microsoft 圖形 API 傳回的使用者設定檔資訊。</span><span class="sxs-lookup"><span data-stu-id="bbaa8-114">You should see user profile information returned by the Microsoft Graph API call on the API Call Results screen.</span></span>

<span data-ttu-id="bbaa8-115">您應該也會在 [權杖資訊] 方塊中，看到透過 `AcquireTokenAsync` 或 `AcquireTokenSilentAsync` 取得之權杖的相關基本資訊：</span><span class="sxs-lookup"><span data-stu-id="bbaa8-115">You  should also see basic information about the token acquired via `AcquireTokenAsync` or `AcquireTokenSilentAsync` in the Token Info box:</span></span>

|<span data-ttu-id="bbaa8-116">屬性</span><span class="sxs-lookup"><span data-stu-id="bbaa8-116">Property</span></span>  |<span data-ttu-id="bbaa8-117">格式</span><span class="sxs-lookup"><span data-stu-id="bbaa8-117">Format</span></span>  |<span data-ttu-id="bbaa8-118">描述</span><span class="sxs-lookup"><span data-stu-id="bbaa8-118">Description</span></span> |
|---------|---------|---------|
|<span data-ttu-id="bbaa8-119">名稱</span><span class="sxs-lookup"><span data-stu-id="bbaa8-119">Name</span></span> | <span data-ttu-id="bbaa8-120">{使用者完整名稱}</span><span class="sxs-lookup"><span data-stu-id="bbaa8-120">{User Full name}</span></span> |<span data-ttu-id="bbaa8-121">使用者的名字和姓氏</span><span class="sxs-lookup"><span data-stu-id="bbaa8-121">The user’s first and last name</span></span>|
|<span data-ttu-id="bbaa8-122">使用者名稱</span><span class="sxs-lookup"><span data-stu-id="bbaa8-122">Username</span></span> |<span>user@domain.com</span> |<span data-ttu-id="bbaa8-123">用來識別使用者的使用者名稱</span><span class="sxs-lookup"><span data-stu-id="bbaa8-123">The username used to identify the user</span></span>|
|<span data-ttu-id="bbaa8-124">權杖到期</span><span class="sxs-lookup"><span data-stu-id="bbaa8-124">Token Expires</span></span> |<span data-ttu-id="bbaa8-125">{DateTime}</span><span class="sxs-lookup"><span data-stu-id="bbaa8-125">{DateTime}</span></span>         |<span data-ttu-id="bbaa8-126">權杖的到期時間。</span><span class="sxs-lookup"><span data-stu-id="bbaa8-126">The time on which the token expires.</span></span> <span data-ttu-id="bbaa8-127">MSAL 將會在必要時更新權杖來為您延長到期日期</span><span class="sxs-lookup"><span data-stu-id="bbaa8-127">MSAL will extend the expiration date for you by renewing the token when necessary</span></span>|
|<span data-ttu-id="bbaa8-128">存取權杖</span><span class="sxs-lookup"><span data-stu-id="bbaa8-128">Access token</span></span> |<span data-ttu-id="bbaa8-129">{字串}</span><span class="sxs-lookup"><span data-stu-id="bbaa8-129">{String}</span></span>         |<span data-ttu-id="bbaa8-130">傳送的權杖字串將傳送至需要授權標頭的 HTTP 要求</span><span class="sxs-lookup"><span data-stu-id="bbaa8-130">The token string sent that will be sent to HTTP requests that require an authorization header</span></span>|

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="bbaa8-131">與範圍和委派的權限有關的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="bbaa8-131">More information about scopes and delegated permissions</span></span>
<span data-ttu-id="bbaa8-132">圖形 API 需要 `user.read` 範圍才能讀取使用者設定檔。</span><span class="sxs-lookup"><span data-stu-id="bbaa8-132">Graph API requires the `user.read` scope to read user profile.</span></span> <span data-ttu-id="bbaa8-133">根據預設值，在我們註冊入口網站上註冊的每個應用程式中都會自動新增此範圍。</span><span class="sxs-lookup"><span data-stu-id="bbaa8-133">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="bbaa8-134">您後端伺服器的部分其他圖形 API 和自訂 API 也會需要其他範圍。</span><span class="sxs-lookup"><span data-stu-id="bbaa8-134">Some other Graph APIs as well as custom APIs for your backend server require additional scopes.</span></span> <span data-ttu-id="bbaa8-135">例如，對於圖形 API 而言，就需要 `Calendars.Read` 來列出使用者的行事曆。</span><span class="sxs-lookup"><span data-stu-id="bbaa8-135">For example, for Graph, `Calendars.Read` is required to list user’s calendars.</span></span> <span data-ttu-id="bbaa8-136">為了在應用程式內容中存取使用者的行事曆，您需要新增 `Calendars.Read` 委派應用程式註冊的資訊，然後將 `Calendars.Read` 新增至 `AcquireTokenAsync` 呼叫。</span><span class="sxs-lookup"><span data-stu-id="bbaa8-136">In order to access the user’s calendar in a context of an application, you need to add `Calendars.Read` delegated application registration’s information and then add `Calendars.Read` to the `AcquireTokenAsync` call.</span></span> <span data-ttu-id="bbaa8-137">系統可能會在您增加範圍數目時，提示使用者同意其他事項。</span><span class="sxs-lookup"><span data-stu-id="bbaa8-137">User may be prompted for additional consents as you increase the number of scopes.</span></span>

<!--end-collapse-->



