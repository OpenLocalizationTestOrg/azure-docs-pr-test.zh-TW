---
title: "如何為您的應用程式服務應用程式設定 Twitter 驗證"
description: "了解如何為您的應用程式服務應用程式設定 Twitter 驗證。"
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: c6dc91d7-30f6-448c-9f2d-8e91104cde73
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: afde020b7817dc58ecea24eb4a09cf93d0986eb2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-your-app-service-application-to-use-twitter-login"></a><span data-ttu-id="57e6e-103">如何設定 App Service 應用程式以使用 Twitter 登入</span><span class="sxs-lookup"><span data-stu-id="57e6e-103">How to configure your App Service application to use Twitter login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="57e6e-104">本主題說明如何設定 Azure App Service，以使用 Twitter 作為驗證提供者。</span><span class="sxs-lookup"><span data-stu-id="57e6e-104">This topic shows you how to configure Azure App Service to use Twitter as an authentication provider.</span></span>

<span data-ttu-id="57e6e-105">若要完成本主題的程序，您必須具有已驗證過電子郵件地址和電話號碼的 Twitter 帳戶。</span><span class="sxs-lookup"><span data-stu-id="57e6e-105">To complete the procedure in this topic, you must have a Twitter account that has a verified email address and phone number.</span></span> <span data-ttu-id="57e6e-106">若要建立新的 Twitter 帳戶，請前往 <a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>。</span><span class="sxs-lookup"><span data-stu-id="57e6e-106">To create a new Twitter account, go to <a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>.</span></span>

## <span data-ttu-id="57e6e-107"><a name="register"> </a>向 Twitter 註冊您的應用程式</span><span class="sxs-lookup"><span data-stu-id="57e6e-107"><a name="register"> </a>Register your application with Twitter</span></span>
1. <span data-ttu-id="57e6e-108">登入 [Azure 入口網站]，然後瀏覽到您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="57e6e-108">Log on to the [Azure portal], and navigate to your application.</span></span> <span data-ttu-id="57e6e-109">複製您的 **URL**。</span><span class="sxs-lookup"><span data-stu-id="57e6e-109">Copy your **URL**.</span></span> <span data-ttu-id="57e6e-110">您將使用此 URL 設定您的 Twitter 應用程式。</span><span class="sxs-lookup"><span data-stu-id="57e6e-110">You will use this to configure your Twitter app.</span></span>
2. <span data-ttu-id="57e6e-111">瀏覽至 [Twitter Developers] 網站，使用您的 Twitter 帳戶認證登入，然後按一下 [建立新的應用程式]。</span><span class="sxs-lookup"><span data-stu-id="57e6e-111">Navigate to the [Twitter Developers] website, sign in with your Twitter account credentials, and click **Create New App**.</span></span>
3. <span data-ttu-id="57e6e-112">針對您新的應用程式輸入 [名稱]和 [說明]。</span><span class="sxs-lookup"><span data-stu-id="57e6e-112">Type in the **Name** and a **Description** for your new app.</span></span> <span data-ttu-id="57e6e-113">貼上您應用程式的 **URL** 作為 [網站]值。</span><span class="sxs-lookup"><span data-stu-id="57e6e-113">Paste in your application's **URL** for the **Website** value.</span></span> <span data-ttu-id="57e6e-114">然後，針對 [回呼 URL]，貼上您之前複製的 [回呼 URL]。</span><span class="sxs-lookup"><span data-stu-id="57e6e-114">Then, for the **Callback URL**, paste the **Callback URL** you copied earlier.</span></span> <span data-ttu-id="57e6e-115">這是您已附加路徑 /.auth/login/twitter/callback 的行動應用程式閘道器。</span><span class="sxs-lookup"><span data-stu-id="57e6e-115">This is your Mobile App gateway appended with the path, */.auth/login/twitter/callback*.</span></span> <span data-ttu-id="57e6e-116">例如： `https://contoso.azurewebsites.net/.auth/login/twitter/callback`。</span><span class="sxs-lookup"><span data-stu-id="57e6e-116">For example, `https://contoso.azurewebsites.net/.auth/login/twitter/callback`.</span></span> <span data-ttu-id="57e6e-117">請確實使用 HTTPS 配置。</span><span class="sxs-lookup"><span data-stu-id="57e6e-117">Make sure that you are using the HTTPS scheme.</span></span>
4. <span data-ttu-id="57e6e-118">在頁面底部，閱讀並接受條款。</span><span class="sxs-lookup"><span data-stu-id="57e6e-118">At the bottom the page, read and accept the terms.</span></span> <span data-ttu-id="57e6e-119">然後按一下 [ **建立 Twitter 應用程式**]。</span><span class="sxs-lookup"><span data-stu-id="57e6e-119">Then click **Create your Twitter application**.</span></span> <span data-ttu-id="57e6e-120">這會註冊應用程式並顯示應用程式詳細資料。</span><span class="sxs-lookup"><span data-stu-id="57e6e-120">This registers the app displays the application details.</span></span>
5. <span data-ttu-id="57e6e-121">按一下 [設定] 索引標籤，勾選 [允許此應用程式用來以 Twitter 登入]，然後按一下 [更新設定]。</span><span class="sxs-lookup"><span data-stu-id="57e6e-121">Click the **Settings** tab, check **Allow this application to be used to sign in with Twitter**, then click **Update Settings**.</span></span>
6. <span data-ttu-id="57e6e-122">選取 [ **金鑰和存取權杖** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="57e6e-122">Select the **Keys and Access Tokens** tab.</span></span> <span data-ttu-id="57e6e-123">記下 [消費者金鑰 (API 金鑰)] 和 [消費者密鑰 (API 密鑰)] 的值。</span><span class="sxs-lookup"><span data-stu-id="57e6e-123">Make a note of the values of **Consumer Key (API Key)** and **Consumer secret (API Secret)**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="57e6e-124">消費者密碼是重要的安全性認證。</span><span class="sxs-lookup"><span data-stu-id="57e6e-124">The consumer secret is an important security credential.</span></span> <span data-ttu-id="57e6e-125">請勿將此密碼告訴任何人或隨應用程式一起散發。</span><span class="sxs-lookup"><span data-stu-id="57e6e-125">Do not share this secret with anyone or distribute it with your app.</span></span>
   > 
   > 

## <span data-ttu-id="57e6e-126"><a name="secrets"> </a>將 Twitter 資訊新增至應用程式</span><span class="sxs-lookup"><span data-stu-id="57e6e-126"><a name="secrets"> </a>Add Twitter information to your application</span></span>
1. <span data-ttu-id="57e6e-127">回到 [Azure 入口網站]，並瀏覽到您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="57e6e-127">Back in the [Azure portal], navigate to your application.</span></span> <span data-ttu-id="57e6e-128">依序按一下 [設定] 及 [驗證/授權]。</span><span class="sxs-lookup"><span data-stu-id="57e6e-128">Click **Settings**, and then **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="57e6e-129">如果 [驗證/授權] 功能未啟用，請切換到 [開] 。</span><span class="sxs-lookup"><span data-stu-id="57e6e-129">If the Authentication / Authorization feature is not enabled, turn the switch to **On**.</span></span>
3. <span data-ttu-id="57e6e-130">按一下 [Twitter] 。</span><span class="sxs-lookup"><span data-stu-id="57e6e-130">Click **Twitter**.</span></span> <span data-ttu-id="57e6e-131">貼入您先前取得的應用程式識別碼和應用程式密鑰值。</span><span class="sxs-lookup"><span data-stu-id="57e6e-131">Paste in the App ID and App Secret values which you obtained previously.</span></span> <span data-ttu-id="57e6e-132">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="57e6e-132">Then click **OK**.</span></span>
   
   ![][1]
   
   <span data-ttu-id="57e6e-133">App Service 預設會提供驗證，但不會限制對您網站內容和 API 的已授權存取。</span><span class="sxs-lookup"><span data-stu-id="57e6e-133">By default, App Service provides authentication but does not restrict authorized access to your site content and APIs.</span></span> <span data-ttu-id="57e6e-134">您必須在應用程式程式碼中授權使用者。</span><span class="sxs-lookup"><span data-stu-id="57e6e-134">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="57e6e-135">(選擇性) 若要限制只有透過 Twitter 授權的使用者可以存取您的網站，請將 [要求未經驗證時所採取的動作] 設為 [Twitter]。</span><span class="sxs-lookup"><span data-stu-id="57e6e-135">(Optional) To restrict access to your site to only users authenticated by Twitter, set **Action to take when request is not authenticated** to **Twitter**.</span></span> <span data-ttu-id="57e6e-136">這會要求所有要求都需經過驗證，且所有未經驗證的要求都會重新導向至 Twitter 以進行驗證。</span><span class="sxs-lookup"><span data-stu-id="57e6e-136">This requires that all requests be authenticated, and all unauthenticated requests are redirected to Twitter for authentication.</span></span>
5. <span data-ttu-id="57e6e-137">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="57e6e-137">Click **Save**.</span></span>

<span data-ttu-id="57e6e-138">現在，您已可在應用程式中使用 Twitter 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="57e6e-138">You are now ready to use Twitter for authentication in your app.</span></span>

## <span data-ttu-id="57e6e-139"><a name="related-content"> </a>相關內容</span><span class="sxs-lookup"><span data-stu-id="57e6e-139"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-twitter-authentication/app-service-twitter-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-twitter-authentication/mobile-app-twitter-settings.png

<!-- URLs. -->

<span data-ttu-id="57e6e-140">[Twitter Developers]: http://go.microsoft.com/fwlink/p/?LinkId=268300</span><span class="sxs-lookup"><span data-stu-id="57e6e-140">[Twitter Developers]: http://go.microsoft.com/fwlink/p/?LinkId=268300</span></span>
<span data-ttu-id="57e6e-141">[Azure 入口網站]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="57e6e-141">[Azure portal]: https://portal.azure.com/</span></span>
[xamarin]: ../app-services-mobile-app-xamarin-ios-get-started-users.md
