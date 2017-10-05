---
title: "如何為您的應用程式服務應用程式設定 Facebook 驗證"
description: "了解如何為您的應用程式服務應用程式設定 Facebook 驗證。"
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: b6b4f062-fcb4-47b3-b75a-ec4cb51a62fd
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: c1b4c91d384c56c4f55bf8d31ced250f51c0d837
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-your-app-service-application-to-use-facebook-login"></a><span data-ttu-id="27196-103">如何設定 App Service 應用程式以使用 Facebook 登入</span><span class="sxs-lookup"><span data-stu-id="27196-103">How to configure your App Service application to use Facebook login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="27196-104">本主題說明如何設定 Azure App Service，以使用 Facebook 做為驗證提供者。</span><span class="sxs-lookup"><span data-stu-id="27196-104">This topic shows you how to configure Azure App Service to use Facebook as an authentication provider.</span></span>

<span data-ttu-id="27196-105">若要完成本主題的程序，您必須具有已通過電子郵件地址與手機號碼驗證的 Facebook 帳戶。</span><span class="sxs-lookup"><span data-stu-id="27196-105">To complete the procedure in this topic, you must have a Facebook account that has a verified email address and a mobile phone number.</span></span> <span data-ttu-id="27196-106">若要建立新的 Facebook 帳戶，請前往 [facebook.com]。</span><span class="sxs-lookup"><span data-stu-id="27196-106">To create a new Facebook account, go to [facebook.com].</span></span>

## <span data-ttu-id="27196-107"><a name="register"> </a>向 Facebook 註冊您的應用程式</span><span class="sxs-lookup"><span data-stu-id="27196-107"><a name="register"> </a>Register your application with Facebook</span></span>
1. <span data-ttu-id="27196-108">登入 [Azure 入口網站]，然後瀏覽到您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="27196-108">Log on to the [Azure portal], and navigate to your application.</span></span> <span data-ttu-id="27196-109">複製您的 **URL**。</span><span class="sxs-lookup"><span data-stu-id="27196-109">Copy your **URL**.</span></span> <span data-ttu-id="27196-110">您將使用此 URL 設定您的 Facebook 應用程式。</span><span class="sxs-lookup"><span data-stu-id="27196-110">You will use this to configure your Facebook app.</span></span>
2. <span data-ttu-id="27196-111">在其他瀏覽器視窗中，瀏覽至 [Facebook 開發人員] 網站，並以您的 Facebook 帳戶認證登入。</span><span class="sxs-lookup"><span data-stu-id="27196-111">In another browser window, navigate to the [Facebook Developers] website and sign-in with your Facebook account credentials.</span></span>
3. <span data-ttu-id="27196-112">(選擇性) 按一下 [應用程式] > [以開發人員身分註冊]，接受政策並遵循註冊步驟 (若您尚未註冊)。</span><span class="sxs-lookup"><span data-stu-id="27196-112">(Optional) If you have not already registered, click **Apps** > **Register as a Developer**, then accept the policy and follow the registration steps.</span></span>
4. <span data-ttu-id="27196-113">按一下 [我的應用程式] > [新增應用程式] > [網站] > [略過並建立應用程式識別碼]。</span><span class="sxs-lookup"><span data-stu-id="27196-113">Click **My Apps** > **Add a New App** > **Website** > **Skip and Create App ID**.</span></span> 
5. <span data-ttu-id="27196-114">在 [顯示名稱] 中輸入應用程式的唯一名稱，輸入 [連絡人電子郵件]，選擇應用程式的 [類別]，然後按一下 [建立應用程式識別碼] 並完成安全性檢查。</span><span class="sxs-lookup"><span data-stu-id="27196-114">In **Display Name**, type a unique name for your app, type your **Contact Email**, choose a **Category** for your app, then click **Create App ID** and complete the security check.</span></span> <span data-ttu-id="27196-115">這會將您帶到開發人員儀表板來設定新的 Facebook 應用程式。</span><span class="sxs-lookup"><span data-stu-id="27196-115">This takes you to the developer dashboard for your new Facebook app.</span></span>
6. <span data-ttu-id="27196-116">在 [Facebook 登入] 下，按一下 [開始使用]。</span><span class="sxs-lookup"><span data-stu-id="27196-116">Under "Facebook Login," click **Get Started**.</span></span> <span data-ttu-id="27196-117">將應用程式的**重新導向 URI**新增至 [有效的 OAuth 重新導向 URI]，然後按一下 [儲存變更]。</span><span class="sxs-lookup"><span data-stu-id="27196-117">Add your application's **Redirect URI** to **Valid OAuth redirect URIs**, then click **Save Changes**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="27196-118">您的重新導向 URI 是應用程式 URL 加上路徑 */.auth/login/facebook/callback*。</span><span class="sxs-lookup"><span data-stu-id="27196-118">Your redirect URI is the URL of your application appended with the path, */.auth/login/facebook/callback*.</span></span> <span data-ttu-id="27196-119">例如， `https://contoso.azurewebsites.net/.auth/login/facebook/callback`。</span><span class="sxs-lookup"><span data-stu-id="27196-119">For example, `https://contoso.azurewebsites.net/.auth/login/facebook/callback`.</span></span> <span data-ttu-id="27196-120">請確實使用 HTTPS 配置。</span><span class="sxs-lookup"><span data-stu-id="27196-120">Make sure that you are using the HTTPS scheme.</span></span>
   > 
   > 
7. <span data-ttu-id="27196-121">在左側導覽中按一下 [設定]。</span><span class="sxs-lookup"><span data-stu-id="27196-121">In the left-hand navigation, click **Settings**.</span></span> <span data-ttu-id="27196-122">在 [應用程式密碼] 欄位中，按一下 [顯示]，在系統要求時提供您的密碼，然後記下 [應用程式識別碼] 和 [應用程式密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="27196-122">On the **App Secret** field, click **Show**, provide your password if requested, then make a note of the values of **App ID** and **App Secret**.</span></span> <span data-ttu-id="27196-123">稍後您會在 Azure 中使用這些資訊來設定您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="27196-123">You use these later to configure your application in Azure.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="27196-124">應用程式密鑰是重要的安全性認證。</span><span class="sxs-lookup"><span data-stu-id="27196-124">The app secret is an important security credential.</span></span> <span data-ttu-id="27196-125">請勿與任何人共用此密碼，或在用戶端應用程式中加以散發。</span><span class="sxs-lookup"><span data-stu-id="27196-125">Do not share this secret with anyone or distribute it within a client application.</span></span>
   > 
   > 
8. <span data-ttu-id="27196-126">用來註冊應用程式的 Facebook 帳戶是應用程式的系統管理員。</span><span class="sxs-lookup"><span data-stu-id="27196-126">The Facebook account which was used to register the application is an administrator of the app.</span></span> <span data-ttu-id="27196-127">此時，只有系統管理員可以登入此應用程式。</span><span class="sxs-lookup"><span data-stu-id="27196-127">At this point, only administrators can sign into this application.</span></span> <span data-ttu-id="27196-128">若要驗證其他 Facebook 帳戶，請按一下 [應用程式檢閱] 並啟用 [公開 <您的應用程式名稱>]，以允許使用 Facebook 驗證來公開存取。</span><span class="sxs-lookup"><span data-stu-id="27196-128">To authenticate other Facebook accounts, click **App Review** and enable **Make <your-app-name> public** to enable general public access using Facebook authentication.</span></span>

## <span data-ttu-id="27196-129"><a name="secrets"> </a>將 Facebook 資訊加入應用程式</span><span class="sxs-lookup"><span data-stu-id="27196-129"><a name="secrets"> </a>Add Facebook information to your application</span></span>
1. <span data-ttu-id="27196-130">回到 [Azure 入口網站]，並瀏覽到您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="27196-130">Back in the [Azure portal], navigate to your application.</span></span> <span data-ttu-id="27196-131">按一下 [設定] > [驗證/授權]，並確定 [App Service 驗證] 為 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="27196-131">Click **Settings** > **Authentication / Authorization**, and make sure that **App Service Authentication** is **On**.</span></span>
2. <span data-ttu-id="27196-132">按一下 [Facebook]，貼上先前取得的應用程式識別碼與應用程式密碼值，選擇性啟用應用程式需要的任何範圍，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="27196-132">Click **Facebook**, paste in the App ID and App Secret values which you obtained previously, optionally enable any scopes needed by your application, then click **OK**.</span></span>
   
    ![][0]
   
    <span data-ttu-id="27196-133">App Service 預設會提供驗證，但不會限制對您網站內容和 API 的已授權存取。</span><span class="sxs-lookup"><span data-stu-id="27196-133">By default, App Service provides authentication but does not restrict authorized access to your site content and APIs.</span></span> <span data-ttu-id="27196-134">您必須在應用程式程式碼中授權使用者。</span><span class="sxs-lookup"><span data-stu-id="27196-134">You must authorize users in your app code.</span></span>
3. <span data-ttu-id="27196-135">(選擇性) 若要限制只有透過 Facebook 授權的使用者可以存取您的網站，請將 [要求未經驗證時所採取的動作] 設為 [Facebook]。</span><span class="sxs-lookup"><span data-stu-id="27196-135">(Optional) To restrict access to your site to only users authenticated by Facebook, set **Action to take when request is not authenticated** to **Facebook**.</span></span> <span data-ttu-id="27196-136">這會要求所有的要求都經過驗證，且所有未經驗證的要求會重新導向至 Facebook 以進行驗證。</span><span class="sxs-lookup"><span data-stu-id="27196-136">This requires that all requests be authenticated, and all unauthenticated requests are redirected to Facebook for authentication.</span></span>
4. <span data-ttu-id="27196-137">設定驗證完成時，按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="27196-137">When done configuring authentication, click **Save**.</span></span>

<span data-ttu-id="27196-138">現在，您已可在應用程式中使用 Facebook 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="27196-138">You are now ready to use Facebook for authentication in your app.</span></span>

## <span data-ttu-id="27196-139"><a name="related-content"> </a>相關內容</span><span class="sxs-lookup"><span data-stu-id="27196-139"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->
[0]: ./media/app-service-mobile-how-to-configure-facebook-authentication/mobile-app-facebook-settings.png

<!-- URLs. -->
<span data-ttu-id="27196-140">[Facebook 開發人員]: http://go.microsoft.com/fwlink/p/?LinkId=268286</span><span class="sxs-lookup"><span data-stu-id="27196-140">[Facebook Developers]: http://go.microsoft.com/fwlink/p/?LinkId=268286</span></span>
<span data-ttu-id="27196-141">[facebook.com]: http://go.microsoft.com/fwlink/p/?LinkId=268285</span><span class="sxs-lookup"><span data-stu-id="27196-141">[facebook.com]: http://go.microsoft.com/fwlink/p/?LinkId=268285</span></span>
[Get started with authentication]: /en-us/develop/mobile/tutorials/get-started-with-users-dotnet/
<span data-ttu-id="27196-142">[Azure 入口網站]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="27196-142">[Azure portal]: https://portal.azure.com/</span></span>
