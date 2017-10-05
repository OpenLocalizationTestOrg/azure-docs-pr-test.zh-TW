---
title: "Azure AD v2 Android 快速入門 - 測試 | Microsoft Docs"
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
ms.openlocfilehash: 6df64f4820f8409bd8897d5ac24f81bffeeef102
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
## <a name="test-your-code"></a><span data-ttu-id="cd381-103">測試您的程式碼</span><span class="sxs-lookup"><span data-stu-id="cd381-103">Test your code</span></span>

1. <span data-ttu-id="cd381-104">將您的程式碼部署到裝置/模擬器。</span><span class="sxs-lookup"><span data-stu-id="cd381-104">Deploy your code to your device/emulator.</span></span>
2. <span data-ttu-id="cd381-105">當您準備好進行測試時，請使用 Microsoft Azure Active Directory (組織帳戶) 或 Microsoft 帳戶 (live.com、outlook.com) 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="cd381-105">When you're ready to test, use a Microsoft Azure Active Directory (organizational account) or a Microsoft Account (live.com, outlook.com) account to sign in.</span></span> 

<span data-ttu-id="cd381-106">![範例螢幕擷取畫面](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
</span><span class="sxs-lookup"><span data-stu-id="cd381-106">![Sample screen shot](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
</span></span><br/><br/><span data-ttu-id="cd381-107">
![登入](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)</span><span class="sxs-lookup"><span data-stu-id="cd381-107">
![Sign-in](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)</span></span>

### <a name="consent"></a><span data-ttu-id="cd381-108">同意</span><span class="sxs-lookup"><span data-stu-id="cd381-108">Consent</span></span>
<span data-ttu-id="cd381-109">使用者第一次登入您的應用程式時，系統會向他們顯示如下所示的類似同意畫面，其中包含他們必須明確接受的事項：</span><span class="sxs-lookup"><span data-stu-id="cd381-109">The first time a user signs in to your application, they will be presented with a consent screen similar to the below, where they need to explicitly accept:</span></span> 

![同意](media/active-directory-mobileanddesktopapp-android-test/androidconsent.png)


### <a name="expected-results"></a><span data-ttu-id="cd381-111">預期的結果</span><span class="sxs-lookup"><span data-stu-id="cd381-111">Expected results</span></span>
<span data-ttu-id="cd381-112">您應該會看到呼叫 Microsoft 圖形 API ‘me’ 端點的結果，該呼叫可用來取得使用者設定檔 - https://graph.microsoft.com/v1.0/me。</span><span class="sxs-lookup"><span data-stu-id="cd381-112">You should see the results of a call to Microsoft Graph API ‘me’ endpoint used to to obtain the user profile - https://graph.microsoft.com/v1.0/me.</span></span> <span data-ttu-id="cd381-113">如需一般 Microsoft Graph 端點的清單，請參閱這篇[文章 (英文)](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries)。</span><span class="sxs-lookup"><span data-stu-id="cd381-113">For a list of common Microsoft Graph endpoints, please see this [article](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="cd381-114">與範圍和委派的權限有關的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="cd381-114">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="cd381-115">Microsoft Graph API 需要 `user.read` 範圍以讀取使用者的設定檔。</span><span class="sxs-lookup"><span data-stu-id="cd381-115">The Microsoft Graph API requires the `user.read` scope to read the user's profile.</span></span> <span data-ttu-id="cd381-116">根據預設值，在我們註冊入口網站上註冊的每個應用程式中都會自動新增此範圍。</span><span class="sxs-lookup"><span data-stu-id="cd381-116">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="cd381-117">Microsoft Graph 的某些其他 API 與您後端伺服器的自訂 API 一樣，需要其他範圍。</span><span class="sxs-lookup"><span data-stu-id="cd381-117">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="cd381-118">例如，針對 Microsoft Graph，需要範圍 `Calendars.Read` 才能列出使用者的行事曆。</span><span class="sxs-lookup"><span data-stu-id="cd381-118">For example, for Microsoft Graph, the scope `Calendars.Read` is required to list the user’s calendars.</span></span> <span data-ttu-id="cd381-119">為了在應用程式內容中存取使用者的行事曆，您需要將 `Calendars.Read` 委派權限新增至應用程式註冊的資訊，然後將 `Calendars.Read` 範圍新增至 `acquireTokenSilentAsync` 呼叫。</span><span class="sxs-lookup"><span data-stu-id="cd381-119">In order to access the user’s calendar in a context of an application, you need to add the `Calendars.Read` delegated permission to the application registration’s information and then add the `Calendars.Read` scope to the `acquireTokenSilentAsync` call.</span></span> <span data-ttu-id="cd381-120">系統可能會在您增加範圍數目時，提示使用者同意其他事項。</span><span class="sxs-lookup"><span data-stu-id="cd381-120">The user may be prompted for additional consents as you increase the number of scopes.</span></span>

<!--end-collapse-->
