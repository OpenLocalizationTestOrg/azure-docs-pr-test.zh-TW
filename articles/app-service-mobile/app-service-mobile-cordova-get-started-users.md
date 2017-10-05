---
title: "使用 Mobile Apps 在 Apache Cordova 上新增驗證 | Microsoft Docs"
description: "了解如何在 Azure App Service 中使用 Mobile Apps，透過眾多識別提供者驗證 Apache Cordova 應用程式使用者，包括 Google、Facebook、Twitter 和 Microsoft。"
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
ms.openlocfilehash: b7362b7f26859de541f792e714502851d74c98e5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-apache-cordova-app"></a><span data-ttu-id="dd5f6-103">新增驗證至您的 Apache Cordova 應用程式</span><span class="sxs-lookup"><span data-stu-id="dd5f6-103">Add authentication to your Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a><span data-ttu-id="dd5f6-104">Summary</span><span class="sxs-lookup"><span data-stu-id="dd5f6-104">Summary</span></span>
<span data-ttu-id="dd5f6-105">在本教學課程中，您可以使用支援的身分識別提供者，將驗證加入 Apache Cordova 上的 TodoList 快速入門專案。</span><span class="sxs-lookup"><span data-stu-id="dd5f6-105">In this tutorial, you add authentication to the todolist quickstart project on Apache Cordova using a supported identity provider.</span></span> <span data-ttu-id="dd5f6-106">本教學課程以 [開始使用 Mobile Apps] 為基礎，您必須先完成該教學課程。</span><span class="sxs-lookup"><span data-stu-id="dd5f6-106">This tutorial is based on the [Get started with Mobile Apps] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="dd5f6-107"><a name="register"></a>註冊應用程式進行驗證，並設定應用程式服務</span><span class="sxs-lookup"><span data-stu-id="dd5f6-107"><a name="register"></a>Register your app for authentication and configure the App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

[<span data-ttu-id="dd5f6-108">觀看示範類似步驟的影片</span><span class="sxs-lookup"><span data-stu-id="dd5f6-108">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-8-Azure-authentication)

## <span data-ttu-id="dd5f6-109"><a name="permissions"></a>限制只有通過驗證的使用者具有權限</span><span class="sxs-lookup"><span data-stu-id="dd5f6-109"><a name="permissions"></a>Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="dd5f6-110">現在，您可以驗證是否已停用後端的匿名存取。</span><span class="sxs-lookup"><span data-stu-id="dd5f6-110">Now, you can verify that anonymous access to your backend has been disabled.</span></span> <span data-ttu-id="dd5f6-111">在 Visual Studio 中：</span><span class="sxs-lookup"><span data-stu-id="dd5f6-111">In Visual Studio:</span></span>

* <span data-ttu-id="dd5f6-112">開啟您完成[開始使用 Mobile Apps] 教學課程時所建立的專案。</span><span class="sxs-lookup"><span data-stu-id="dd5f6-112">Open the project that you created when you completed the tutorial [Get started with Mobile Apps].</span></span>
* <span data-ttu-id="dd5f6-113">在 **Google Android 模擬器**中執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="dd5f6-113">Run your application in the **Google Android Emulator**.</span></span>
* <span data-ttu-id="dd5f6-114">應用程式啟動後，確認有顯示「非預期的連接失敗」。</span><span class="sxs-lookup"><span data-stu-id="dd5f6-114">Verify that an Unexpected Connection Failure is shown after the app starts.</span></span>

<span data-ttu-id="dd5f6-115">接下來，將應用程式更新為在使用者從行動應用程式後端要求資源之前，先驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="dd5f6-115">Next, update the app to authenticate users before requesting resources from the Mobile App backend.</span></span>

## <span data-ttu-id="dd5f6-116"><a name="add-authentication"></a>將驗證新增至應用程式</span><span class="sxs-lookup"><span data-stu-id="dd5f6-116"><a name="add-authentication"></a>Add authentication to the app</span></span>
1. <span data-ttu-id="dd5f6-117">在 **Visual Studio** 中開啟您的專案，然後開啟 `www/index.html` 檔案進行編輯。</span><span class="sxs-lookup"><span data-stu-id="dd5f6-117">Open your project in **Visual Studio**, then open the `www/index.html` file for editing.</span></span>
2. <span data-ttu-id="dd5f6-118">找出 head 區段中的 `Content-Security-Policy` 中繼標籤。</span><span class="sxs-lookup"><span data-stu-id="dd5f6-118">Locate the `Content-Security-Policy` meta tag in the head section.</span></span>  <span data-ttu-id="dd5f6-119">將 OAuth 主機新增至允許的來源清單。</span><span class="sxs-lookup"><span data-stu-id="dd5f6-119">Add the OAuth host to the list of allowed sources.</span></span>

   | <span data-ttu-id="dd5f6-120">提供者</span><span class="sxs-lookup"><span data-stu-id="dd5f6-120">Provider</span></span> | <span data-ttu-id="dd5f6-121">SDK 提供者名稱</span><span class="sxs-lookup"><span data-stu-id="dd5f6-121">SDK Provider Name</span></span> | <span data-ttu-id="dd5f6-122">OAuth 主機</span><span class="sxs-lookup"><span data-stu-id="dd5f6-122">OAuth Host</span></span> |
   |:--- |:--- |:--- |
   | <span data-ttu-id="dd5f6-123">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dd5f6-123">Azure Active Directory</span></span> | <span data-ttu-id="dd5f6-124">aad</span><span class="sxs-lookup"><span data-stu-id="dd5f6-124">aad</span></span> | <span data-ttu-id="dd5f6-125">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="dd5f6-125">https://login.microsoftonline.com</span></span> |
   | <span data-ttu-id="dd5f6-126">Facebook</span><span class="sxs-lookup"><span data-stu-id="dd5f6-126">Facebook</span></span> | <span data-ttu-id="dd5f6-127">Facebook</span><span class="sxs-lookup"><span data-stu-id="dd5f6-127">facebook</span></span> | <span data-ttu-id="dd5f6-128">https://www.facebook.com</span><span class="sxs-lookup"><span data-stu-id="dd5f6-128">https://www.facebook.com</span></span> |
   | <span data-ttu-id="dd5f6-129">Google</span><span class="sxs-lookup"><span data-stu-id="dd5f6-129">Google</span></span> | <span data-ttu-id="dd5f6-130">Google</span><span class="sxs-lookup"><span data-stu-id="dd5f6-130">google</span></span> | <span data-ttu-id="dd5f6-131">https://accounts.google.com</span><span class="sxs-lookup"><span data-stu-id="dd5f6-131">https://accounts.google.com</span></span> |
   | <span data-ttu-id="dd5f6-132">Microsoft</span><span class="sxs-lookup"><span data-stu-id="dd5f6-132">Microsoft</span></span> | <span data-ttu-id="dd5f6-133">microsoftaccount</span><span class="sxs-lookup"><span data-stu-id="dd5f6-133">microsoftaccount</span></span> | <span data-ttu-id="dd5f6-134">https://login.live.com</span><span class="sxs-lookup"><span data-stu-id="dd5f6-134">https://login.live.com</span></span> |
   | <span data-ttu-id="dd5f6-135">Twitter</span><span class="sxs-lookup"><span data-stu-id="dd5f6-135">Twitter</span></span> | <span data-ttu-id="dd5f6-136">Twitter</span><span class="sxs-lookup"><span data-stu-id="dd5f6-136">twitter</span></span> | <span data-ttu-id="dd5f6-137">https://api.twitter.com</span><span class="sxs-lookup"><span data-stu-id="dd5f6-137">https://api.twitter.com</span></span> |

    <span data-ttu-id="dd5f6-138">content-security-policy (針對 Azure Active Directory 實作) 的範例如下所示：</span><span class="sxs-lookup"><span data-stu-id="dd5f6-138">An example Content-Security-Policy (implemented for Azure Active Directory) is as follows:</span></span>

        <meta http-equiv="Content-Security-Policy" content="default-src 'self'
            data: gap: https://login.microsoftonline.com https://yourapp.azurewebsites.net; style-src 'self'">

    <span data-ttu-id="dd5f6-139">使用上表中的 OAuth 主機取代 `https://login.microsoftonline.com`。</span><span class="sxs-lookup"><span data-stu-id="dd5f6-139">Replace `https://login.microsoftonline.com` with the OAuth host from the preceding table.</span></span>  <span data-ttu-id="dd5f6-140">如需 content-security-policy 中繼標籤的詳細資訊，請參閱 [Content-Security-Policy 文件]。</span><span class="sxs-lookup"><span data-stu-id="dd5f6-140">For more information about the content-security-policy meta tag, see the [Content-Security-Policy documentation].</span></span>

    <span data-ttu-id="dd5f6-141">在適當的行動裝置上使用時，某些驗證提供者不需要變更 Content-Security-Policy。</span><span class="sxs-lookup"><span data-stu-id="dd5f6-141">Some authentication providers do not require Content-Security-Policy changes when used on appropriate mobile devices.</span></span>  <span data-ttu-id="dd5f6-142">例如，在 Android 裝置上使用 Google 驗證時不需要 Content-Security-Policy 變更。</span><span class="sxs-lookup"><span data-stu-id="dd5f6-142">For example, no Content-Security-Policy changes are required when using Google authentication on an Android device.</span></span>

3. <span data-ttu-id="dd5f6-143">開啟 `www/js/index.js` 檔案進行編輯，找出 `onDeviceReady()` 方法，並在用戶端建立程式碼底下新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="dd5f6-143">Open the `www/js/index.js` file for editing, locate the `onDeviceReady()` method, and under the client  creation code add the following code:</span></span>

        // Login to the service
        client.login('SDK_Provider_Name')
            .then(function () {

                // BEGINNING OF ORIGINAL CODE

                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh the todoItems
                refreshDisplay();

                // Wire up the UI Event Handler for the Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                // END OF ORIGINAL CODE

            }, handleError);

    <span data-ttu-id="dd5f6-144">此程式碼會取代現有用於建立資料表參考和重新整理 UI 的程式碼。</span><span class="sxs-lookup"><span data-stu-id="dd5f6-144">This code replaces the existing code that creates the table reference and refreshes the UI.</span></span>

    <span data-ttu-id="dd5f6-145">login () 方法會開始向提供者驗證。</span><span class="sxs-lookup"><span data-stu-id="dd5f6-145">The login() method starts authentication with the provider.</span></span> <span data-ttu-id="dd5f6-146">login() 方法是會傳回 JavaScript Promise 的非同步函式。</span><span class="sxs-lookup"><span data-stu-id="dd5f6-146">The login() method is an async function that returns a JavaScript Promise.</span></span>  <span data-ttu-id="dd5f6-147">初始化作業的其餘部分會置於承諾回應中，如此就不會在 login() 方法完成之前執行。</span><span class="sxs-lookup"><span data-stu-id="dd5f6-147">The rest of the initialization is placed inside the promise response so that it is not executed until the login() method completes.</span></span>

4. <span data-ttu-id="dd5f6-148">在您剛才加入的程式碼中，使用您的登入提供者名稱取代 `SDK_Provider_Name` 。</span><span class="sxs-lookup"><span data-stu-id="dd5f6-148">In the code that you just added, replace `SDK_Provider_Name` with the name of your login provider.</span></span> <span data-ttu-id="dd5f6-149">例如，針對 Azure Active Directory，請使用 `client.login('aad')`。</span><span class="sxs-lookup"><span data-stu-id="dd5f6-149">For example, for Azure Active Directory, use `client.login('aad')`.</span></span>
5. <span data-ttu-id="dd5f6-150">執行專案。</span><span class="sxs-lookup"><span data-stu-id="dd5f6-150">Run your project.</span></span>  <span data-ttu-id="dd5f6-151">當專案完成初始化時，您的應用程式會針對選擇的驗證提供者顯示 OAuth 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="dd5f6-151">When the project has finished initializing, your application shows the OAuth login page for the chosen authentication provider.</span></span>

## <span data-ttu-id="dd5f6-152"><a name="next-steps"></a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="dd5f6-152"><a name="next-steps"></a>Next Steps</span></span>
* <span data-ttu-id="dd5f6-153">深入了解 Azure App Service [驗證相關資訊] 。</span><span class="sxs-lookup"><span data-stu-id="dd5f6-153">Learn more [About Authentication] with Azure App Service.</span></span>
* <span data-ttu-id="dd5f6-154">將 [推播通知] 新增至 Apache Cordova 應用程式，以繼續本教學課程。</span><span class="sxs-lookup"><span data-stu-id="dd5f6-154">Continue the tutorial by adding [Push Notifications] to your Apache Cordova app.</span></span>

<span data-ttu-id="dd5f6-155">了解如何使用 SDK。</span><span class="sxs-lookup"><span data-stu-id="dd5f6-155">Learn how to use the SDKs.</span></span>

* <span data-ttu-id="dd5f6-156">[Apache Cordova SDK]</span><span class="sxs-lookup"><span data-stu-id="dd5f6-156">[Apache Cordova SDK]</span></span>
* <span data-ttu-id="dd5f6-157">[ASP.NET Server SDK]</span><span class="sxs-lookup"><span data-stu-id="dd5f6-157">[ASP.NET Server SDK]</span></span>
* <span data-ttu-id="dd5f6-158">[Node.js Server SDK]</span><span class="sxs-lookup"><span data-stu-id="dd5f6-158">[Node.js Server SDK]</span></span>

<!-- URLs. -->
<span data-ttu-id="dd5f6-159">[開始使用 Mobile Apps]: app-service-mobile-cordova-get-started.md</span><span class="sxs-lookup"><span data-stu-id="dd5f6-159">[Get started with Mobile Apps]: app-service-mobile-cordova-get-started.md</span></span>
<span data-ttu-id="dd5f6-160">[Content-Security-Policy 文件]: https://cordova.apache.org/docs/en/latest/guide/appdev/whitelist/index.html</span><span class="sxs-lookup"><span data-stu-id="dd5f6-160">[Content-Security-Policy documentation]: https://cordova.apache.org/docs/en/latest/guide/appdev/whitelist/index.html</span></span>
<span data-ttu-id="dd5f6-161">[推播通知]: app-service-mobile-cordova-get-started-push.md</span><span class="sxs-lookup"><span data-stu-id="dd5f6-161">[Push Notifications]: app-service-mobile-cordova-get-started-push.md</span></span>
<span data-ttu-id="dd5f6-162">[驗證相關資訊]: app-service-mobile-auth.md</span><span class="sxs-lookup"><span data-stu-id="dd5f6-162">[About Authentication]: app-service-mobile-auth.md</span></span>
<span data-ttu-id="dd5f6-163">[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md</span><span class="sxs-lookup"><span data-stu-id="dd5f6-163">[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md</span></span>
<span data-ttu-id="dd5f6-164">[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md</span><span class="sxs-lookup"><span data-stu-id="dd5f6-164">[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md</span></span>
<span data-ttu-id="dd5f6-165">[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md</span><span class="sxs-lookup"><span data-stu-id="dd5f6-165">[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md</span></span>
