---
title: "aaaAzure AD v2 Windows 桌面快速入門-測試 |Microsoft 文件"
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
ms.openlocfilehash: 0ae9612e1585c54a3fe35ba9d18f92554099b2c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a><span data-ttu-id="687b4-103">測試您的程式碼</span><span class="sxs-lookup"><span data-stu-id="687b4-103">Test your code</span></span>

<span data-ttu-id="687b4-104">若要 tootest 您的應用程式，請按`F5`toorun Visual Studio 中的專案。</span><span class="sxs-lookup"><span data-stu-id="687b4-104">In order tootest your application, press `F5` toorun your project in Visual Studio.</span></span> <span data-ttu-id="687b4-105">您的主視窗應會出現：</span><span class="sxs-lookup"><span data-stu-id="687b4-105">Your Main Window should appear:</span></span>

![範例螢幕擷取畫面](media/active-directory-mobileanddesktopapp-windowsdesktop-test/samplescreenshot.png)

<span data-ttu-id="687b4-107">當你準備好 tootest 時，請按一下*呼叫 Microsoft Graph API*並使用 Microsoft Azure Active Directory （組織帳戶） 或 Microsoft 帳戶 （live.com、 outlook.com） 帳戶 toosign 中的。</span><span class="sxs-lookup"><span data-stu-id="687b4-107">When you're ready tootest, click *Call Microsoft Graph API* and use a Microsoft Azure Active Directory (organizational account) or a Microsoft Account (live.com, outlook.com) account toosign in.</span></span> <span data-ttu-id="687b4-108">它是 hello 第一次，您會看到一個視窗詢問使用者 toosign 中：</span><span class="sxs-lookup"><span data-stu-id="687b4-108">It it is hello first time, you will see a window asking user toosign in:</span></span>

![登入](media/active-directory-mobileanddesktopapp-windowsdesktop-test/signinscreenshot.png)

### <a name="consent"></a><span data-ttu-id="687b4-110">同意</span><span class="sxs-lookup"><span data-stu-id="687b4-110">Consent</span></span>
<span data-ttu-id="687b4-111">hello 第一次您登入 tooyour 應用程式，您會看到類似 toohello 下列同意畫面，您需要在 tooexplicitly 接受：</span><span class="sxs-lookup"><span data-stu-id="687b4-111">hello first time you sign in tooyour application, you will be presented with a consent screen similar toohello below, where you need tooexplicitly accept:</span></span>

![同意畫面](media/active-directory-mobileanddesktopapp-windowsdesktop-test/consentscreen.png)

### <a name="expected-results"></a><span data-ttu-id="687b4-113">預期的結果</span><span class="sxs-lookup"><span data-stu-id="687b4-113">Expected results</span></span>
<span data-ttu-id="687b4-114">您應該會看到 hello API 呼叫的結果 畫面 hello Microsoft Graph API 呼叫所傳回的使用者設定檔資訊。</span><span class="sxs-lookup"><span data-stu-id="687b4-114">You should see user profile information returned by hello Microsoft Graph API call on hello API Call Results screen.</span></span>

<span data-ttu-id="687b4-115">您也應該會看到透過 hello 權杖的基本資訊`AcquireTokenAsync`或`AcquireTokenSilentAsync`hello 語彙基元資訊 方塊中：</span><span class="sxs-lookup"><span data-stu-id="687b4-115">You  should also see basic information about hello token acquired via `AcquireTokenAsync` or `AcquireTokenSilentAsync` in hello Token Info box:</span></span>

|<span data-ttu-id="687b4-116">屬性</span><span class="sxs-lookup"><span data-stu-id="687b4-116">Property</span></span>  |<span data-ttu-id="687b4-117">格式</span><span class="sxs-lookup"><span data-stu-id="687b4-117">Format</span></span>  |<span data-ttu-id="687b4-118">描述</span><span class="sxs-lookup"><span data-stu-id="687b4-118">Description</span></span> |
|---------|---------|---------|
|<span data-ttu-id="687b4-119">名稱</span><span class="sxs-lookup"><span data-stu-id="687b4-119">Name</span></span> | <span data-ttu-id="687b4-120">{使用者完整名稱}</span><span class="sxs-lookup"><span data-stu-id="687b4-120">{User Full name}</span></span> |<span data-ttu-id="687b4-121">hello 使用者的名字和姓氏</span><span class="sxs-lookup"><span data-stu-id="687b4-121">hello user’s first and last name</span></span>|
|<span data-ttu-id="687b4-122">使用者名稱</span><span class="sxs-lookup"><span data-stu-id="687b4-122">Username</span></span> |<span>user@domain.com</span> |<span data-ttu-id="687b4-123">用 tooidentify hello 使用者 hello 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="687b4-123">hello username used tooidentify hello user</span></span>|
|<span data-ttu-id="687b4-124">權杖到期</span><span class="sxs-lookup"><span data-stu-id="687b4-124">Token Expires</span></span> |<span data-ttu-id="687b4-125">{DateTime}</span><span class="sxs-lookup"><span data-stu-id="687b4-125">{DateTime}</span></span>         |<span data-ttu-id="687b4-126">hello 的 hello 權杖到期的時間。</span><span class="sxs-lookup"><span data-stu-id="687b4-126">hello time on which hello token expires.</span></span> <span data-ttu-id="687b4-127">MSAL 會延長為您 hello 到期日 hello 語彙基元時所需的更新</span><span class="sxs-lookup"><span data-stu-id="687b4-127">MSAL will extend hello expiration date for you by renewing hello token when necessary</span></span>|
|<span data-ttu-id="687b4-128">存取權杖</span><span class="sxs-lookup"><span data-stu-id="687b4-128">Access token</span></span> |<span data-ttu-id="687b4-129">{字串}</span><span class="sxs-lookup"><span data-stu-id="687b4-129">{String}</span></span>         |<span data-ttu-id="687b4-130">hello 語彙基元字串傳送，會將要求傳送給 tooHTTP 需要授權標頭</span><span class="sxs-lookup"><span data-stu-id="687b4-130">hello token string sent that will be sent tooHTTP requests that require an authorization header</span></span>|

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="687b4-131">與範圍和委派的權限有關的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="687b4-131">More information about scopes and delegated permissions</span></span>
<span data-ttu-id="687b4-132">Graph API 需要 hello`user.read`範圍 tooread 使用者設定檔。</span><span class="sxs-lookup"><span data-stu-id="687b4-132">Graph API requires hello `user.read` scope tooread user profile.</span></span> <span data-ttu-id="687b4-133">根據預設值，在我們註冊入口網站上註冊的每個應用程式中都會自動新增此範圍。</span><span class="sxs-lookup"><span data-stu-id="687b4-133">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="687b4-134">您後端伺服器的部分其他圖形 API 和自訂 API 也會需要其他範圍。</span><span class="sxs-lookup"><span data-stu-id="687b4-134">Some other Graph APIs as well as custom APIs for your backend server require additional scopes.</span></span> <span data-ttu-id="687b4-135">例如，對於圖形中，`Calendars.Read`是必要的 toolist 使用者的行事曆。</span><span class="sxs-lookup"><span data-stu-id="687b4-135">For example, for Graph, `Calendars.Read` is required toolist user’s calendars.</span></span> <span data-ttu-id="687b4-136">順序 tooaccess hello 使用者的行事曆應用程式的內容中，您需要 tooadd`Calendars.Read`委派應用程式註冊資訊，然後再加入`Calendars.Read`toohello`AcquireTokenAsync`呼叫。</span><span class="sxs-lookup"><span data-stu-id="687b4-136">In order tooaccess hello user’s calendar in a context of an application, you need tooadd `Calendars.Read` delegated application registration’s information and then add `Calendars.Read` toohello `AcquireTokenAsync` call.</span></span> <span data-ttu-id="687b4-137">當您增加 hello 範圍數目，可能會提示使用者輸入其他的同意授權。</span><span class="sxs-lookup"><span data-stu-id="687b4-137">User may be prompted for additional consents as you increase hello number of scopes.</span></span>

<!--end-collapse-->



