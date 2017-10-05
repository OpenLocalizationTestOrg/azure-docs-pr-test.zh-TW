---
title: "使用 Mobile Apps 在 Android 上新增驗證 | Microsoft Docs"
description: "了解如何使用 Azure App Service 的 Mobile Apps 功能，透過眾多識別提供者驗證 Android 應用程式使用者，包括 Google、Facebook、Twitter 和 Microsoft。"
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 1fc8e7c1-6c3c-40f4-9967-9cf5e21fc4e1
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 81331142aa6110d4e29e6fb30a90ce6e3a853439
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-android-app"></a><span data-ttu-id="aeb6d-103">將驗證加入 Android 應用程式中</span><span class="sxs-lookup"><span data-stu-id="aeb6d-103">Add authentication to your Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a><span data-ttu-id="aeb6d-104">摘要</span><span class="sxs-lookup"><span data-stu-id="aeb6d-104">Summary</span></span>
<span data-ttu-id="aeb6d-105">在本教學課程中，您可以使用支援的身分識別提供者，將驗證加入 Android 上的 TodoList 快速入門專案。</span><span class="sxs-lookup"><span data-stu-id="aeb6d-105">In this tutorial, you add authentication to the todolist quickstart project on Android by using a supported identity provider.</span></span> <span data-ttu-id="aeb6d-106">本教學課程以[開始使用 Mobile Apps] 為基礎，您必須先完成該教學課程。</span><span class="sxs-lookup"><span data-stu-id="aeb6d-106">This tutorial is based on the [Get started with Mobile Apps] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="aeb6d-107"><a name="register"></a>註冊應用程式進行驗證，並設定 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="aeb6d-107"><a name="register"></a>Register your app for authentication and configure Azure App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="aeb6d-108"><a name="redirecturl"></a>將您的應用程式新增至允許的外部重新導向 URL</span><span class="sxs-lookup"><span data-stu-id="aeb6d-108"><a name="redirecturl"></a>Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="aeb6d-109">安全的驗證會要求您為應用程式定義新的 URL 配置。</span><span class="sxs-lookup"><span data-stu-id="aeb6d-109">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="aeb6d-110">這讓驗證系統能夠在驗證程序完成之後，重新導向回到您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="aeb6d-110">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="aeb6d-111">我們會在這整個教學課程中使用 URL 配置 appname。</span><span class="sxs-lookup"><span data-stu-id="aeb6d-111">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="aeb6d-112">不過，您可以使用任何您選擇的 URL 結構描述。</span><span class="sxs-lookup"><span data-stu-id="aeb6d-112">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="aeb6d-113">它對於您的行動應用程式而言應該是唯一的。</span><span class="sxs-lookup"><span data-stu-id="aeb6d-113">It should be unique to your mobile application.</span></span> <span data-ttu-id="aeb6d-114">在伺服器端啟用重新導向：</span><span class="sxs-lookup"><span data-stu-id="aeb6d-114">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="aeb6d-115">在 [Azure 入口網站] 中，選取您的 App Service。</span><span class="sxs-lookup"><span data-stu-id="aeb6d-115">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="aeb6d-116">按一下 [驗證/授權] 功能表選項。</span><span class="sxs-lookup"><span data-stu-id="aeb6d-116">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="aeb6d-117">在 [允許的外部重新導向 URL] 中，輸入 `appname://easyauth.callback`。</span><span class="sxs-lookup"><span data-stu-id="aeb6d-117">In the **Allowed External Redirect URLs**, enter `appname://easyauth.callback`.</span></span>  <span data-ttu-id="aeb6d-118">此字串中的 appname 是您行動應用程式的 URL 配置。</span><span class="sxs-lookup"><span data-stu-id="aeb6d-118">The _appname_ in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="aeb6d-119">它必須遵循通訊協定的標準 URL 規格 (只使用字母和數字，並以字母為開頭)。</span><span class="sxs-lookup"><span data-stu-id="aeb6d-119">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="aeb6d-120">請記下您選擇的字串，因為您將需要在數個位置中使用該 URL 配置來調整您的行動應用程式程式碼。</span><span class="sxs-lookup"><span data-stu-id="aeb6d-120">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="aeb6d-121">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="aeb6d-121">Click **OK**.</span></span>

5. <span data-ttu-id="aeb6d-122">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="aeb6d-122">Click **Save**.</span></span>

## <span data-ttu-id="aeb6d-123"><a name="permissions"></a>限制只有通過驗證的使用者具有權限</span><span class="sxs-lookup"><span data-stu-id="aeb6d-123"><a name="permissions"></a>Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

* <span data-ttu-id="aeb6d-124">在 Android Studio 中，開啟您使用[開始使用 Mobile Apps] 教學課程完成的專案。</span><span class="sxs-lookup"><span data-stu-id="aeb6d-124">In Android Studio, open the project you completed with the tutorial [Get started with Mobile Apps].</span></span> <span data-ttu-id="aeb6d-125">從 [執行] 功能表按一下 [執行應用程式] 並確認應用程式啟動之後會引發無法處理的例外狀況，狀態碼為 401 (未授權)。</span><span class="sxs-lookup"><span data-stu-id="aeb6d-125">From the **Run** menu, click **Run app**, and verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span>

     <span data-ttu-id="aeb6d-126">發生此例外狀況是因為應用程式嘗試以未驗證的使用者身分來存取後端，但 *TodoItem* 資料表現在需要驗證。</span><span class="sxs-lookup"><span data-stu-id="aeb6d-126">This exception happens because the app attempts to access the back end as an unauthenticated user, but the *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="aeb6d-127">接下來，您要將應用程式更新為在要求 Mobile Apps 後端的資源之前必須驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="aeb6d-127">Next, you update the app to authenticate users before requesting resources from the Mobile Apps back end.</span></span> 

## <a name="add-authentication-to-the-app"></a><span data-ttu-id="aeb6d-128">將驗證新增至應用程式</span><span class="sxs-lookup"><span data-stu-id="aeb6d-128">Add authentication to the app</span></span>
[!INCLUDE [mobile-android-authenticate-app](../../includes/mobile-android-authenticate-app.md)]



## <span data-ttu-id="aeb6d-129"><a name="cache-tokens"></a>在用戶端快取驗證權杖</span><span class="sxs-lookup"><span data-stu-id="aeb6d-129"><a name="cache-tokens"></a>Cache authentication tokens on the client</span></span>
[!INCLUDE [mobile-android-authenticate-app-with-token](../../includes/mobile-android-authenticate-app-with-token.md)]

## <a name="next-steps"></a><span data-ttu-id="aeb6d-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="aeb6d-130">Next steps</span></span>
<span data-ttu-id="aeb6d-131">現在您已經完成了這個基本驗證的教學課程，可以考慮繼續進行下列其中一個教學課程：</span><span class="sxs-lookup"><span data-stu-id="aeb6d-131">Now that you completed this basic authentication tutorial, consider continuing on to one of the following tutorials:</span></span>

* <span data-ttu-id="aeb6d-132">[將推播通知新增至 Android 應用程式](app-service-mobile-android-get-started-push.md)。</span><span class="sxs-lookup"><span data-stu-id="aeb6d-132">[Add push notifications to your Android app](app-service-mobile-android-get-started-push.md).</span></span>
  <span data-ttu-id="aeb6d-133">了解如何設定 Mobile Apps 後端，使用 Azure 通知中樞來傳送推播通知。</span><span class="sxs-lookup"><span data-stu-id="aeb6d-133">Learn how to configure your Mobile Apps back end to use Azure notification hubs to send push notifications.</span></span>
* <span data-ttu-id="aeb6d-134">[啟用 Android 應用程式的離線同步處理](app-service-mobile-android-get-started-offline-data.md)。</span><span class="sxs-lookup"><span data-stu-id="aeb6d-134">[Enable offline sync for your Android app](app-service-mobile-android-get-started-offline-data.md).</span></span>
  <span data-ttu-id="aeb6d-135">了解如何使用 Mobile Apps 後端，將離線支援新增至應用程式。</span><span class="sxs-lookup"><span data-stu-id="aeb6d-135">Learn how to add offline support to your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="aeb6d-136">使用離線同步處理時，使用者可與行動應用程式進行互動&mdash;檢視、新增或修改資料&mdash;即使沒有網路連線進也可行。</span><span class="sxs-lookup"><span data-stu-id="aeb6d-136">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->
[Register your app for authentication and configure Mobile Services]: #register
[Restrict table permissions to authenticated users]: #permissions
[Add authentication to the app]: #add-authentication
[Store authentication tokens on the client]: #cache-tokens
[Refresh expired tokens]: #refresh-tokens
[Next Steps]:#next-steps


<!-- URLs. -->
<span data-ttu-id="aeb6d-137">[開始使用 Mobile Apps]: app-service-mobile-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="aeb6d-137">[Get started with Mobile Apps]: app-service-mobile-android-get-started.md</span></span>
