---
title: "行動應用程式與 Apache Cordova aaaAdd 驗證 |Microsoft 文件"
description: "深入了解如何在您的 Apache Cordova 應用程式透過不同的身分識別提供者，包括 Google、 Facebook、 Twitter 和 Microsoft Azure App Service tooauthenticate 使用者 toouse 行動應用程式。"
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 10dd6dc9-ddf5-423d-8205-00ad74929f0d
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 61a05c5ac67fd0f0bc4c9d6920954a9b464a0a8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-apache-cordova-app"></a><span data-ttu-id="a0340-103">新增驗證 tooyour Apache Cordova 應用程式</span><span class="sxs-lookup"><span data-stu-id="a0340-103">Add authentication tooyour Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a><span data-ttu-id="a0340-104">摘要</span><span class="sxs-lookup"><span data-stu-id="a0340-104">Summary</span></span>
<span data-ttu-id="a0340-105">在本教學課程中，您可以將驗證 toohello todolist 快速入門專案上使用支援的身分識別提供者的 Apache Cordova。</span><span class="sxs-lookup"><span data-stu-id="a0340-105">In this tutorial, you add authentication toohello todolist quickstart project on Apache Cordova using a supported identity provider.</span></span> <span data-ttu-id="a0340-106">本教學課程根據 hello[開始使用行動應用程式]教學課程中，您必須先完成。</span><span class="sxs-lookup"><span data-stu-id="a0340-106">This tutorial is based on hello [Get started with Mobile Apps] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="a0340-107"><a name="register"></a>註冊您的應用程式進行驗證並設定 hello 應用程式服務</span><span class="sxs-lookup"><span data-stu-id="a0340-107"><a name="register"></a>Register your app for authentication and configure hello App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

[<span data-ttu-id="a0340-108">觀看示範類似步驟的影片</span><span class="sxs-lookup"><span data-stu-id="a0340-108">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-8-Azure-authentication)

## <span data-ttu-id="a0340-109"><a name="permissions"></a>限制 tooauthenticated 使用者權限</span><span class="sxs-lookup"><span data-stu-id="a0340-109"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="a0340-110">現在，您可以確認已停用該匿名存取 tooyour 後端。</span><span class="sxs-lookup"><span data-stu-id="a0340-110">Now, you can verify that anonymous access tooyour backend has been disabled.</span></span> <span data-ttu-id="a0340-111">在 Visual Studio 中：</span><span class="sxs-lookup"><span data-stu-id="a0340-111">In Visual Studio:</span></span>

* <span data-ttu-id="a0340-112">開啟 hello 時完成 hello 教學課程所建立的專案[開始使用行動應用程式]。</span><span class="sxs-lookup"><span data-stu-id="a0340-112">Open hello project that you created when you completed hello tutorial [Get started with Mobile Apps].</span></span>
* <span data-ttu-id="a0340-113">執行您的應用程式在 hello **Google Android 模擬器**。</span><span class="sxs-lookup"><span data-stu-id="a0340-113">Run your application in hello **Google Android Emulator**.</span></span>
* <span data-ttu-id="a0340-114">請確認 hello 應用程式啟動之後，會顯示非預期的連線失敗。</span><span class="sxs-lookup"><span data-stu-id="a0340-114">Verify that an Unexpected Connection Failure is shown after hello app starts.</span></span>

<span data-ttu-id="a0340-115">接下來，從 hello 行動裝置應用程式後端要求的資源之前更新 hello tooauthenticate 的應用程式使用者。</span><span class="sxs-lookup"><span data-stu-id="a0340-115">Next, update hello app tooauthenticate users before requesting resources from hello Mobile App backend.</span></span>

## <span data-ttu-id="a0340-116"><a name="add-authentication"></a>新增驗證 toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="a0340-116"><a name="add-authentication"></a>Add authentication toohello app</span></span>
1. <span data-ttu-id="a0340-117">開啟您的專案中**Visual Studio**，然後開啟 hello`www/index.html`檔案進行編輯。</span><span class="sxs-lookup"><span data-stu-id="a0340-117">Open your project in **Visual Studio**, then open hello `www/index.html` file for editing.</span></span>
2. <span data-ttu-id="a0340-118">找出 hello `Content-Security-Policy` hello 標頭區段中的中繼標籤。</span><span class="sxs-lookup"><span data-stu-id="a0340-118">Locate hello `Content-Security-Policy` meta tag in hello head section.</span></span>  <span data-ttu-id="a0340-119">新增 hello OAuth 主機 toohello 允許來源清單。</span><span class="sxs-lookup"><span data-stu-id="a0340-119">Add hello OAuth host toohello list of allowed sources.</span></span>

   | <span data-ttu-id="a0340-120">提供者</span><span class="sxs-lookup"><span data-stu-id="a0340-120">Provider</span></span> | <span data-ttu-id="a0340-121">SDK 提供者名稱</span><span class="sxs-lookup"><span data-stu-id="a0340-121">SDK Provider Name</span></span> | <span data-ttu-id="a0340-122">OAuth 主機</span><span class="sxs-lookup"><span data-stu-id="a0340-122">OAuth Host</span></span> |
   |:--- |:--- |:--- |
   | <span data-ttu-id="a0340-123">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a0340-123">Azure Active Directory</span></span> | <span data-ttu-id="a0340-124">aad</span><span class="sxs-lookup"><span data-stu-id="a0340-124">aad</span></span> | <span data-ttu-id="a0340-125">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="a0340-125">https://login.microsoftonline.com</span></span> |
   | <span data-ttu-id="a0340-126">Facebook</span><span class="sxs-lookup"><span data-stu-id="a0340-126">Facebook</span></span> | <span data-ttu-id="a0340-127">Facebook</span><span class="sxs-lookup"><span data-stu-id="a0340-127">facebook</span></span> | <span data-ttu-id="a0340-128">https://www.facebook.com</span><span class="sxs-lookup"><span data-stu-id="a0340-128">https://www.facebook.com</span></span> |
   | <span data-ttu-id="a0340-129">Google</span><span class="sxs-lookup"><span data-stu-id="a0340-129">Google</span></span> | <span data-ttu-id="a0340-130">Google</span><span class="sxs-lookup"><span data-stu-id="a0340-130">google</span></span> | <span data-ttu-id="a0340-131">https://accounts.google.com</span><span class="sxs-lookup"><span data-stu-id="a0340-131">https://accounts.google.com</span></span> |
   | <span data-ttu-id="a0340-132">Microsoft</span><span class="sxs-lookup"><span data-stu-id="a0340-132">Microsoft</span></span> | <span data-ttu-id="a0340-133">microsoftaccount</span><span class="sxs-lookup"><span data-stu-id="a0340-133">microsoftaccount</span></span> | <span data-ttu-id="a0340-134">https://login.live.com</span><span class="sxs-lookup"><span data-stu-id="a0340-134">https://login.live.com</span></span> |
   | <span data-ttu-id="a0340-135">Twitter</span><span class="sxs-lookup"><span data-stu-id="a0340-135">Twitter</span></span> | <span data-ttu-id="a0340-136">Twitter</span><span class="sxs-lookup"><span data-stu-id="a0340-136">twitter</span></span> | <span data-ttu-id="a0340-137">https://api.twitter.com</span><span class="sxs-lookup"><span data-stu-id="a0340-137">https://api.twitter.com</span></span> |

    <span data-ttu-id="a0340-138">content-security-policy (針對 Azure Active Directory 實作) 的範例如下所示：</span><span class="sxs-lookup"><span data-stu-id="a0340-138">An example Content-Security-Policy (implemented for Azure Active Directory) is as follows:</span></span>

        <meta http-equiv="Content-Security-Policy" content="default-src 'self'
            data: gap: https://login.microsoftonline.com https://yourapp.azurewebsites.net; style-src 'self'">

    <span data-ttu-id="a0340-139">取代`https://login.microsoftonline.com`與 hello OAuth host hello 上述資料表。</span><span class="sxs-lookup"><span data-stu-id="a0340-139">Replace `https://login.microsoftonline.com` with hello OAuth host from hello preceding table.</span></span>  <span data-ttu-id="a0340-140">如需 hello meta 標記，內容安全性原則的詳細資訊，請參閱 hello[內容安全性原則文件]。</span><span class="sxs-lookup"><span data-stu-id="a0340-140">For more information about hello content-security-policy meta tag, see hello [Content-Security-Policy documentation].</span></span>

    <span data-ttu-id="a0340-141">在適當的行動裝置上使用時，某些驗證提供者不需要變更 Content-Security-Policy。</span><span class="sxs-lookup"><span data-stu-id="a0340-141">Some authentication providers do not require Content-Security-Policy changes when used on appropriate mobile devices.</span></span>  <span data-ttu-id="a0340-142">例如，在 Android 裝置上使用 Google 驗證時不需要 Content-Security-Policy 變更。</span><span class="sxs-lookup"><span data-stu-id="a0340-142">For example, no Content-Security-Policy changes are required when using Google authentication on an Android device.</span></span>

3. <span data-ttu-id="a0340-143">開啟 hello`www/js/index.js`檔案進行編輯，找出 hello`onDeviceReady()`方法，並在建立 hello 用戶端程式碼會加入下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="a0340-143">Open hello `www/js/index.js` file for editing, locate hello `onDeviceReady()` method, and under hello client  creation code add hello following code:</span></span>

        // Login toohello service
        client.login('SDK_Provider_Name')
            .then(function () {

                // BEGINNING OF ORIGINAL CODE

                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh hello todoItems
                refreshDisplay();

                // Wire up hello UI Event Handler for hello Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                // END OF ORIGINAL CODE

            }, handleError);

    <span data-ttu-id="a0340-144">此程式碼取代 hello 的現有程式碼會建立 hello 資料表參考，並重新整理 hello UI。</span><span class="sxs-lookup"><span data-stu-id="a0340-144">This code replaces hello existing code that creates hello table reference and refreshes hello UI.</span></span>

    <span data-ttu-id="a0340-145">hello login() 方法開頭 hello 提供者的驗證。</span><span class="sxs-lookup"><span data-stu-id="a0340-145">hello login() method starts authentication with hello provider.</span></span> <span data-ttu-id="a0340-146">hello login() 方法是傳回 JavaScript 承諾 async 函式。</span><span class="sxs-lookup"><span data-stu-id="a0340-146">hello login() method is an async function that returns a JavaScript Promise.</span></span>  <span data-ttu-id="a0340-147">hello rest 的 hello 初始化置於 hello 承諾回應，使它不會執行直到 hello login() 方法完成為止。</span><span class="sxs-lookup"><span data-stu-id="a0340-147">hello rest of hello initialization is placed inside hello promise response so that it is not executed until hello login() method completes.</span></span>

4. <span data-ttu-id="a0340-148">在您剛才加入的 hello 程式碼，取代`SDK_Provider_Name`與 hello 登入提供者名稱。</span><span class="sxs-lookup"><span data-stu-id="a0340-148">In hello code that you just added, replace `SDK_Provider_Name` with hello name of your login provider.</span></span> <span data-ttu-id="a0340-149">例如，針對 Azure Active Directory，請使用 `client.login('aad')`。</span><span class="sxs-lookup"><span data-stu-id="a0340-149">For example, for Azure Active Directory, use `client.login('aad')`.</span></span>
5. <span data-ttu-id="a0340-150">執行專案。</span><span class="sxs-lookup"><span data-stu-id="a0340-150">Run your project.</span></span>  <span data-ttu-id="a0340-151">當 hello 專案已完成初始化時，您的應用程式會顯示 hello 選擇驗證提供者的 hello OAuth 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="a0340-151">When hello project has finished initializing, your application shows hello OAuth login page for hello chosen authentication provider.</span></span>

## <span data-ttu-id="a0340-152"><a name="next-steps"></a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="a0340-152"><a name="next-steps"></a>Next Steps</span></span>
* <span data-ttu-id="a0340-153">深入了解 Azure App Service [驗證相關資訊] 。</span><span class="sxs-lookup"><span data-stu-id="a0340-153">Learn more [About Authentication] with Azure App Service.</span></span>
* <span data-ttu-id="a0340-154">藉由新增繼續 hello 教學課程[推播通知]tooyour Apache Cordova 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a0340-154">Continue hello tutorial by adding [Push Notifications] tooyour Apache Cordova app.</span></span>

<span data-ttu-id="a0340-155">了解如何 toouse hello Sdk。</span><span class="sxs-lookup"><span data-stu-id="a0340-155">Learn how toouse hello SDKs.</span></span>

* <span data-ttu-id="a0340-156">[Apache Cordova SDK]</span><span class="sxs-lookup"><span data-stu-id="a0340-156">[Apache Cordova SDK]</span></span>
* <span data-ttu-id="a0340-157">[ASP.NET Server SDK]</span><span class="sxs-lookup"><span data-stu-id="a0340-157">[ASP.NET Server SDK]</span></span>
* <span data-ttu-id="a0340-158">[Node.js Server SDK]</span><span class="sxs-lookup"><span data-stu-id="a0340-158">[Node.js Server SDK]</span></span>

<!-- URLs. -->
[開始使用 Mobile Apps]: app-service-mobile-cordova-get-started.md
[Content-Security-Policy 文件]: https://cordova.apache.org/docs/en/latest/guide/appdev/whitelist/index.html
[推播通知]: app-service-mobile-cordova-get-started-push.md
[驗證相關資訊]: app-service-mobile-auth.md
[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
