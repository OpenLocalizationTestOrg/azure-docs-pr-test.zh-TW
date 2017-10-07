---
title: "aaaHow tooconfigure Twitter 驗證您的應用程式服務應用程式"
description: "深入了解如何 tooconfigure Twitter 驗證您的應用程式服務應用程式。"
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
ms.openlocfilehash: 0d16ac44d7b54e3567b793a904059d31ab1d8911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-twitter-login"></a><span data-ttu-id="00e91-103">如何 tooconfigure 您 App Service 應用程式 toouse Twitter 登入</span><span class="sxs-lookup"><span data-stu-id="00e91-103">How tooconfigure your App Service application toouse Twitter login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="00e91-104">本主題說明如何 tooconfigure Azure App Service toouse Twitter 做為驗證提供者。</span><span class="sxs-lookup"><span data-stu-id="00e91-104">This topic shows you how tooconfigure Azure App Service toouse Twitter as an authentication provider.</span></span>

<span data-ttu-id="00e91-105">toocomplete hello 程序，本主題中的，您必須具有 [已驗證的電子郵件地址和電話號碼的 Twitter 帳戶。</span><span class="sxs-lookup"><span data-stu-id="00e91-105">toocomplete hello procedure in this topic, you must have a Twitter account that has a verified email address and phone number.</span></span> <span data-ttu-id="00e91-106">toocreate 新的 Twitter 帳戶，跳過<a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>。</span><span class="sxs-lookup"><span data-stu-id="00e91-106">toocreate a new Twitter account, go too<a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>.</span></span>

## <span data-ttu-id="00e91-107"><a name="register"> </a>向 Twitter 註冊您的應用程式</span><span class="sxs-lookup"><span data-stu-id="00e91-107"><a name="register"> </a>Register your application with Twitter</span></span>
1. <span data-ttu-id="00e91-108">登入 toohello [Azure 入口網站]，並瀏覽 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="00e91-108">Log on toohello [Azure portal], and navigate tooyour application.</span></span> <span data-ttu-id="00e91-109">複製您的 **URL**。</span><span class="sxs-lookup"><span data-stu-id="00e91-109">Copy your **URL**.</span></span> <span data-ttu-id="00e91-110">您將使用此 tooconfigure Twitter 應用程式。</span><span class="sxs-lookup"><span data-stu-id="00e91-110">You will use this tooconfigure your Twitter app.</span></span>
2. <span data-ttu-id="00e91-111">瀏覽 toohello [Twitter 開發人員]網站，使用您的 Twitter 帳戶認證登入，然後按一下 [**建立新的應用程式**。</span><span class="sxs-lookup"><span data-stu-id="00e91-111">Navigate toohello [Twitter Developers] website, sign in with your Twitter account credentials, and click **Create New App**.</span></span>
3. <span data-ttu-id="00e91-112">型別在 hello**名稱**和**描述**新應用程式。</span><span class="sxs-lookup"><span data-stu-id="00e91-112">Type in hello **Name** and a **Description** for your new app.</span></span> <span data-ttu-id="00e91-113">貼上您的應用程式的**URL** hello**網站**值。</span><span class="sxs-lookup"><span data-stu-id="00e91-113">Paste in your application's **URL** for hello **Website** value.</span></span> <span data-ttu-id="00e91-114">然後，針對 hello**回呼 URL**，貼上 hello**回呼 URL**您之前複製。</span><span class="sxs-lookup"><span data-stu-id="00e91-114">Then, for hello **Callback URL**, paste hello **Callback URL** you copied earlier.</span></span> <span data-ttu-id="00e91-115">這是您的行動裝置應用程式閘道加上 hello 路徑*/.auth/login/twitter/callback*。</span><span class="sxs-lookup"><span data-stu-id="00e91-115">This is your Mobile App gateway appended with hello path, */.auth/login/twitter/callback*.</span></span> <span data-ttu-id="00e91-116">例如： `https://contoso.azurewebsites.net/.auth/login/twitter/callback`。</span><span class="sxs-lookup"><span data-stu-id="00e91-116">For example, `https://contoso.azurewebsites.net/.auth/login/twitter/callback`.</span></span> <span data-ttu-id="00e91-117">請確定您使用 hello HTTPS 配置。</span><span class="sxs-lookup"><span data-stu-id="00e91-117">Make sure that you are using hello HTTPS scheme.</span></span>
4. <span data-ttu-id="00e91-118">在 hello 底部 hello] 頁面上，閱讀並接受 hello 條款。</span><span class="sxs-lookup"><span data-stu-id="00e91-118">At hello bottom hello page, read and accept hello terms.</span></span> <span data-ttu-id="00e91-119">然後按一下 [ **建立 Twitter 應用程式**]。</span><span class="sxs-lookup"><span data-stu-id="00e91-119">Then click **Create your Twitter application**.</span></span> <span data-ttu-id="00e91-120">此暫存器 hello 應用程式會顯示 hello 應用程式詳細資料。</span><span class="sxs-lookup"><span data-stu-id="00e91-120">This registers hello app displays hello application details.</span></span>
5. <span data-ttu-id="00e91-121">按一下 hello**設定**索引標籤上，核取**允許 Twitter 入此應用程式使用 toobe toosign**，然後按一下 [**更新設定**。</span><span class="sxs-lookup"><span data-stu-id="00e91-121">Click hello **Settings** tab, check **Allow this application toobe used toosign in with Twitter**, then click **Update Settings**.</span></span>
6. <span data-ttu-id="00e91-122">選取 hello**機碼和存取權杖**] 索引標籤。請記下的 hello 值**取用者金鑰 （應用程式開發介面）**和**取用者密碼 （應用程式開發介面機密）**。</span><span class="sxs-lookup"><span data-stu-id="00e91-122">Select hello **Keys and Access Tokens** tab. Make a note of hello values of **Consumer Key (API Key)** and **Consumer secret (API Secret)**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="00e91-123">hello 取用者密碼是重要的安全性認證。</span><span class="sxs-lookup"><span data-stu-id="00e91-123">hello consumer secret is an important security credential.</span></span> <span data-ttu-id="00e91-124">請勿將此密碼告訴任何人或隨應用程式一起散發。</span><span class="sxs-lookup"><span data-stu-id="00e91-124">Do not share this secret with anyone or distribute it with your app.</span></span>
   > 
   > 

## <span data-ttu-id="00e91-125"><a name="secrets"></a>新增 Twitter 資訊 tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="00e91-125"><a name="secrets"> </a>Add Twitter information tooyour application</span></span>
1. <span data-ttu-id="00e91-126">在 [hello [Azure 入口網站]，瀏覽 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="00e91-126">Back in hello [Azure portal], navigate tooyour application.</span></span> <span data-ttu-id="00e91-127">依序按一下 [設定] 及 [驗證/授權]。</span><span class="sxs-lookup"><span data-stu-id="00e91-127">Click **Settings**, and then **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="00e91-128">如果 hello 驗證 / 授權功能未啟用，請開啟 hello 參數太**上**。</span><span class="sxs-lookup"><span data-stu-id="00e91-128">If hello Authentication / Authorization feature is not enabled, turn hello switch too**On**.</span></span>
3. <span data-ttu-id="00e91-129">按一下 [Twitter] 。</span><span class="sxs-lookup"><span data-stu-id="00e91-129">Click **Twitter**.</span></span> <span data-ttu-id="00e91-130">您先前取得的值貼上在應用程式識別碼 hello 與應用程式密碼。</span><span class="sxs-lookup"><span data-stu-id="00e91-130">Paste in hello App ID and App Secret values which you obtained previously.</span></span> <span data-ttu-id="00e91-131">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="00e91-131">Then click **OK**.</span></span>
   
   ![][1]
   
   <span data-ttu-id="00e91-132">根據預設，應用程式服務提供驗證但不會限制授權的存取 tooyour 網站內容和應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="00e91-132">By default, App Service provides authentication but does not restrict authorized access tooyour site content and APIs.</span></span> <span data-ttu-id="00e91-133">您必須在應用程式程式碼中授權使用者。</span><span class="sxs-lookup"><span data-stu-id="00e91-133">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="00e91-134">（選擇性） toorestrict 存取 tooyour 網站 tooonly 使用者由 Twitter 驗證設定**當要求未經驗證的動作 tootake**太**Twitter**。</span><span class="sxs-lookup"><span data-stu-id="00e91-134">(Optional) toorestrict access tooyour site tooonly users authenticated by Twitter, set **Action tootake when request is not authenticated** too**Twitter**.</span></span> <span data-ttu-id="00e91-135">這需要驗證的所有要求，而所有未經驗證的要求重新導向的 tooTwitter 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="00e91-135">This requires that all requests be authenticated, and all unauthenticated requests are redirected tooTwitter for authentication.</span></span>
5. <span data-ttu-id="00e91-136">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="00e91-136">Click **Save**.</span></span>

<span data-ttu-id="00e91-137">現在您已準備好 toouse Twitter 驗證您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="00e91-137">You are now ready toouse Twitter for authentication in your app.</span></span>

## <span data-ttu-id="00e91-138"><a name="related-content"> </a>相關內容</span><span class="sxs-lookup"><span data-stu-id="00e91-138"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-twitter-authentication/app-service-twitter-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-twitter-authentication/mobile-app-twitter-settings.png

<!-- URLs. -->

[Twitter Developers]: http://go.microsoft.com/fwlink/p/?LinkId=268300
[Azure 入口網站]: https://portal.azure.com/
[xamarin]: ../app-services-mobile-app-xamarin-ios-get-started-users.md
