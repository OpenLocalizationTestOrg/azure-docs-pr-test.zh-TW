---
title: "如何為您的應用程式服務應用程式設定 Google 驗證"
description: "了解如何為您的應用程式服務應用程式設定 Google 驗證。"
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: 2b2f9abf-9120-4aac-ac5b-4a268d9b6e2b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: d6c1707f67d986487e5a45e76ffc9a02ddf16eb1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-your-app-service-application-to-use-google-login"></a><span data-ttu-id="cc3c8-103">如何設定 App Service 應用程式以使用 Google 登入</span><span class="sxs-lookup"><span data-stu-id="cc3c8-103">How to configure your App Service application to use Google login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="cc3c8-104">本主題說明如何設定 Azure App Service，以使用 Google 做為驗證提供者。</span><span class="sxs-lookup"><span data-stu-id="cc3c8-104">This topic shows you how to configure Azure App Service to use Google as an authentication provider.</span></span>

<span data-ttu-id="cc3c8-105">若要完成本主題的程序，您必須具有已通過電子郵件地址驗證的 Google 帳戶。</span><span class="sxs-lookup"><span data-stu-id="cc3c8-105">To complete the procedure in this topic, you must have a Google account that has a verified email address.</span></span> <span data-ttu-id="cc3c8-106">若要建立新的 Google 帳戶，請前往 [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302)。</span><span class="sxs-lookup"><span data-stu-id="cc3c8-106">To create a new Google account, go to [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span></span>

## <span data-ttu-id="cc3c8-107"><a name="register"> </a>向 Google 註冊您的應用程式</span><span class="sxs-lookup"><span data-stu-id="cc3c8-107"><a name="register"> </a>Register your application with Google</span></span>
1. <span data-ttu-id="cc3c8-108">登入 [Azure 入口網站]，然後瀏覽到您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="cc3c8-108">Log on to the [Azure portal], and navigate to your application.</span></span> <span data-ttu-id="cc3c8-109">複製 **URL**，以供稍後用來設定 Google 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cc3c8-109">Copy your **URL**, which you use later to configure your Google app.</span></span>
2. <span data-ttu-id="cc3c8-110">瀏覽至 [Google APIs](http://go.microsoft.com/fwlink/p/?LinkId=268303) 網站，以您的 Google 帳戶認證登入，按一下 [建立專案]，提供 [專案名稱]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="cc3c8-110">Navigate to the [Google apis](http://go.microsoft.com/fwlink/p/?LinkId=268303) website, sign in with your Google account credentials, click **Create Project**, provide a **Project name**, then click **Create**.</span></span>
3. <span data-ttu-id="cc3c8-111">在 [社交平台類 API] 下，按一下 [Google + API]，然後按一下 [啟用]。</span><span class="sxs-lookup"><span data-stu-id="cc3c8-111">Under **Social APIs** click **Google+ API** and then **Enable**.</span></span>
4. <span data-ttu-id="cc3c8-112">在左側導覽中，按一下 [憑證] > [OAuth 同意畫面]，然後選取您的 [電子郵件地址]，輸入 [產品名稱]，再按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="cc3c8-112">In the left navigation, **Credentials** > **OAuth consent screen**, then select your **Email address**,  enter a **Product Name**, and click **Save**.</span></span>
5. <span data-ttu-id="cc3c8-113">在 [憑證] 索引標籤中，按一下 [建立認證] > [OAuth 用戶端 ID]，然後選取 [網路應用程式]。</span><span class="sxs-lookup"><span data-stu-id="cc3c8-113">In the **Credentials** tab, click **Create credentials** > **OAuth client ID**, then select **Web application**.</span></span>
6. <span data-ttu-id="cc3c8-114">將您稍早複製的 App Service **URL** 貼到 [已授權的 JAVASCRIPT 來源]，然後將重新導向 URI 貼到 [授權的重新導向 URI]。</span><span class="sxs-lookup"><span data-stu-id="cc3c8-114">Paste the App Service **URL** you copied earlier into **Authorized JavaScript Origins**, then paste your redirect URI into **Authorized Redirect URI**.</span></span> <span data-ttu-id="cc3c8-115">重新導向 URI 是您的應用程式 URL 加上路徑 /.auth/login/google/callback。</span><span class="sxs-lookup"><span data-stu-id="cc3c8-115">The redirect URI is the URL of your application appended with the path, */.auth/login/google/callback*.</span></span> <span data-ttu-id="cc3c8-116">例如： `https://contoso.azurewebsites.net/.auth/login/google/callback`。</span><span class="sxs-lookup"><span data-stu-id="cc3c8-116">For example, `https://contoso.azurewebsites.net/.auth/login/google/callback`.</span></span> <span data-ttu-id="cc3c8-117">請確實使用 HTTPS 配置。</span><span class="sxs-lookup"><span data-stu-id="cc3c8-117">Make sure that you are using the HTTPS scheme.</span></span> <span data-ttu-id="cc3c8-118">然後按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="cc3c8-118">Then click **Create**.</span></span>
7. <span data-ttu-id="cc3c8-119">在下一個畫面上，記下用戶端識別碼和用戶端密碼的值。</span><span class="sxs-lookup"><span data-stu-id="cc3c8-119">On the next screen, make a note of the values of the client ID and client secret.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="cc3c8-120">用戶端密碼是重要的安全性認證。</span><span class="sxs-lookup"><span data-stu-id="cc3c8-120">The client secret is an important security credential.</span></span> <span data-ttu-id="cc3c8-121">請勿與任何人共用此密碼，或在用戶端應用程式中加以散發。</span><span class="sxs-lookup"><span data-stu-id="cc3c8-121">Do not share this secret with anyone or distribute it within a client application.</span></span>


## <span data-ttu-id="cc3c8-122"><a name="secrets"> </a>將 Google 資訊新增至應用程式</span><span class="sxs-lookup"><span data-stu-id="cc3c8-122"><a name="secrets"> </a>Add Google information to your application</span></span>
1. <span data-ttu-id="cc3c8-123">回到 [Azure 入口網站]，並瀏覽到您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="cc3c8-123">Back in the [Azure portal], navigate to your application.</span></span> <span data-ttu-id="cc3c8-124">依序按一下 [設定] 及 [驗證/授權]。</span><span class="sxs-lookup"><span data-stu-id="cc3c8-124">Click **Settings**, and then **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="cc3c8-125">如果 [驗證/授權] 功能未啟用，請切換到 [開] 。</span><span class="sxs-lookup"><span data-stu-id="cc3c8-125">If the Authentication / Authorization feature is not enabled, turn the switch to **On**.</span></span>
3. <span data-ttu-id="cc3c8-126">按一下 [Google] 。</span><span class="sxs-lookup"><span data-stu-id="cc3c8-126">Click **Google**.</span></span> <span data-ttu-id="cc3c8-127">貼上先前取得的應用程式識別碼與應用程式密碼值，然後選擇性啟用應用程式需要的任何範圍。</span><span class="sxs-lookup"><span data-stu-id="cc3c8-127">Paste in the App ID and App Secret values which you obtained previously, and optionally enable any scopes your application requires.</span></span> <span data-ttu-id="cc3c8-128">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="cc3c8-128">Then click **OK**.</span></span>
   
   ![][1]
   
   <span data-ttu-id="cc3c8-129">App Service 預設會提供驗證，但不會限制對您網站內容和 API 的已授權存取。</span><span class="sxs-lookup"><span data-stu-id="cc3c8-129">By default, App Service provides authentication but does not restrict authorized access to your site content and APIs.</span></span> <span data-ttu-id="cc3c8-130">您必須在應用程式程式碼中授權使用者。</span><span class="sxs-lookup"><span data-stu-id="cc3c8-130">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="cc3c8-131">(選擇性) 若要限制只有透過 Google 授權的使用者可以存取您的網站，請將 [要求未經驗證時所採取的動作] 設為 [Google]。</span><span class="sxs-lookup"><span data-stu-id="cc3c8-131">(Optional) To restrict access to your site to only users authenticated by Google, set **Action to take when request is not authenticated** to **Google**.</span></span> <span data-ttu-id="cc3c8-132">這會要求所有要求都需經過驗證，且所有未經驗證的要求都會重新導向至 Google 以進行驗證。</span><span class="sxs-lookup"><span data-stu-id="cc3c8-132">This requires that all requests be authenticated, and all unauthenticated requests are redirected to Google for authentication.</span></span>
5. <span data-ttu-id="cc3c8-133">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="cc3c8-133">Click **Save**.</span></span>

<span data-ttu-id="cc3c8-134">現在，您已可在應用程式中使用 Google 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="cc3c8-134">You are now ready to use Google for authentication in your app.</span></span>

## <span data-ttu-id="cc3c8-135"><a name="related-content"> </a>相關內容</span><span class="sxs-lookup"><span data-stu-id="cc3c8-135"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Anchors. -->

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-settings.png

<!-- URLs. -->

[Google apis]: http://go.microsoft.com/fwlink/p/?LinkId=268303

[Azure 入口網站]: https://portal.azure.com/

