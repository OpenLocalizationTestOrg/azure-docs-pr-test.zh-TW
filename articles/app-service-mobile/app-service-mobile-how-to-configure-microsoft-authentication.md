---
title: "如何為您的應用程式服務應用程式設定 Microsoft 帳戶驗證"
description: "了解如何為您的應用程式服務應用程式設定 Microsoft 帳戶驗證。"
author: mattchenderson
services: app-service
documentationcenter: 
manager: syntaxc4
editor: 
ms.assetid: ffbc6064-edf6-474d-971c-695598fd08bf
ms.service: app-service
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 67386b03ae4cc683fe00e11e8dad19d1442eff09
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-your-app-service-application-to-use-microsoft-account-login"></a><span data-ttu-id="f7035-103">如何設定 App Service 應用程式以使用 Microsoft 帳戶登入</span><span class="sxs-lookup"><span data-stu-id="f7035-103">How to configure your App Service application to use Microsoft Account login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="f7035-104">本主題說明如何設定 Azure App Service，以使用 Microsoft 帳戶作為驗證提供者。</span><span class="sxs-lookup"><span data-stu-id="f7035-104">This topic shows you how to configure Azure App Service to use Microsoft Account as an authentication provider.</span></span> 

## <span data-ttu-id="f7035-105"><a name="register-microsoft-account"> </a>使用 Microsoft 帳戶註冊應用程式</span><span class="sxs-lookup"><span data-stu-id="f7035-105"><a name="register-microsoft-account"> </a>Register your app with Microsoft Account</span></span>
1. <span data-ttu-id="f7035-106">登入 [Azure 入口網站]，然後瀏覽到您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f7035-106">Log on to the [Azure portal], and navigate to your application.</span></span> <span data-ttu-id="f7035-107">複製 **URL**，以供稍後使用 Microsoft 帳戶來設定應用程式。</span><span class="sxs-lookup"><span data-stu-id="f7035-107">Copy your **URL**, which later you use to configure your app with Microsoft Account.</span></span>
2. <span data-ttu-id="f7035-108">瀏覽到 Microsoft 帳戶開發人員中心的 [我的應用程式] 頁面，並視需要使用您的 Microsoft 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="f7035-108">Navigate to the [My Applications] page in the Microsoft Account Developer Center, and log on with your Microsoft account, if required.</span></span>
3. <span data-ttu-id="f7035-109">按一下 [新增應用程式]，然後輸入應用程式名稱，再按一下 [建立應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f7035-109">Click **Add an app**, then type an application name, and click **Create application**.</span></span>
4. <span data-ttu-id="f7035-110">請記下 [應用程式識別碼] ，因為稍後您將會用到此資訊。</span><span class="sxs-lookup"><span data-stu-id="f7035-110">Make a note of the **Application ID**, as you will need it later.</span></span> 
5. <span data-ttu-id="f7035-111">在 [平台] 下，按一下 [新增平台]  ，然後選取 [網站]。</span><span class="sxs-lookup"><span data-stu-id="f7035-111">Under "Platforms," click **Add Platform** and select "Web".</span></span>
6. <span data-ttu-id="f7035-112">在 [重新導向 URI] 下，提供應用程式的端點，然後按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="f7035-112">Under "Redirect URIs" supply the endpoint for your application, then click **Save**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="f7035-113">重新導向 URI 是您的應用程式 URL 加上路徑 /.auth/login/microsoftaccount/callback。</span><span class="sxs-lookup"><span data-stu-id="f7035-113">Your redirect URI is the URL of your application appended with the path, */.auth/login/microsoftaccount/callback*.</span></span> <span data-ttu-id="f7035-114">例如， `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`。</span><span class="sxs-lookup"><span data-stu-id="f7035-114">For example, `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.</span></span>   
   > <span data-ttu-id="f7035-115">請確實使用 HTTPS 配置。</span><span class="sxs-lookup"><span data-stu-id="f7035-115">Make sure that you are using the HTTPS scheme.</span></span>
   
7. <span data-ttu-id="f7035-116">在 [應用程式密碼] 下，按一下 [產生新密碼] 。</span><span class="sxs-lookup"><span data-stu-id="f7035-116">Under "Application Secrets," click **Generate New Password**.</span></span> <span data-ttu-id="f7035-117">請記下出現的值。</span><span class="sxs-lookup"><span data-stu-id="f7035-117">Make note of the value that appears.</span></span> <span data-ttu-id="f7035-118">一旦您離開此頁面，就不會再次顯示。</span><span class="sxs-lookup"><span data-stu-id="f7035-118">Once you leave the page, it will not be displayed again.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="f7035-119">密碼是重要的安全性認證。</span><span class="sxs-lookup"><span data-stu-id="f7035-119">The password is an important security credential.</span></span> <span data-ttu-id="f7035-120">請勿與任何人共用密碼，或在用戶端應用程式內散佈密碼。</span><span class="sxs-lookup"><span data-stu-id="f7035-120">Do not share the password with anyone or distribute it within a client application.</span></span>

## <span data-ttu-id="f7035-121"><a name="secrets"> </a>將 Microsoft 帳戶資訊新增至 App Service 應用程式</span><span class="sxs-lookup"><span data-stu-id="f7035-121"><a name="secrets"> </a>Add Microsoft Account information to your App Service application</span></span>
1. <span data-ttu-id="f7035-122">回到 [Azure 入口網站]，瀏覽至您的應用程式，按一下 [設定] > [驗證/授權]。</span><span class="sxs-lookup"><span data-stu-id="f7035-122">Back in the [Azure portal], navigate to your application, click **Settings** > **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="f7035-123">如果 [驗證/授權] 功能未啟用，請切換至 [開啟] 。</span><span class="sxs-lookup"><span data-stu-id="f7035-123">If the Authentication / Authorization feature is not enabled, switch it **On**.</span></span>
3. <span data-ttu-id="f7035-124">按一下 [Microsoft 帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="f7035-124">Click **Microsoft Account**.</span></span> <span data-ttu-id="f7035-125">貼上先前取得的 [應用程式識別碼] 與 [應用程式密碼] 值，然後選擇性啟用應用程式需要的任何範圍。</span><span class="sxs-lookup"><span data-stu-id="f7035-125">Paste in the Application ID and Password values which you obtained previously, and optionally enable any scopes your application requires.</span></span> <span data-ttu-id="f7035-126">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="f7035-126">Then click **OK**.</span></span>
   
    ![][1]
   
    <span data-ttu-id="f7035-127">App Service 預設會提供驗證，但不會限制對您網站內容和 API 的已授權存取。</span><span class="sxs-lookup"><span data-stu-id="f7035-127">By default, App Service provides authentication but does not restrict authorized access to your site content and APIs.</span></span> <span data-ttu-id="f7035-128">您必須在應用程式程式碼中授權使用者。</span><span class="sxs-lookup"><span data-stu-id="f7035-128">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="f7035-129">(選擇性) 若要限制只有透過 Microsoft 帳戶授權的使用者可以存取您的網站，請將 [要求未經驗證時所採取的動作] 設為 [Microsoft 帳戶]。</span><span class="sxs-lookup"><span data-stu-id="f7035-129">(Optional) To restrict access to your site to only users authenticated by Microsoft account, set **Action to take when request is not authenticated** to **Microsoft Account**.</span></span> <span data-ttu-id="f7035-130">這會要求所有的要求都經過驗證，且所有未經驗證的要求會重新導向至 Microsoft 帳戶以進行驗證。</span><span class="sxs-lookup"><span data-stu-id="f7035-130">This requires that all requests be authenticated, and all unauthenticated requests are redirected to Microsoft account for authentication.</span></span>
5. <span data-ttu-id="f7035-131">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="f7035-131">Click **Save**.</span></span>

<span data-ttu-id="f7035-132">現在，您已可在應用程式中使用 Microsoft 帳戶進行驗證。</span><span class="sxs-lookup"><span data-stu-id="f7035-132">You are now ready to use Microsoft Account for authentication in your app.</span></span>

## <span data-ttu-id="f7035-133"><a name="related-content"> </a>相關內容</span><span class="sxs-lookup"><span data-stu-id="f7035-133"><a name="related-content"> </a>Related content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/app-service-microsoftaccount-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/mobile-app-microsoftaccount-settings.png

<!-- URLs. -->

[我的應用程式]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Azure 入口網站]: https://portal.azure.com/
