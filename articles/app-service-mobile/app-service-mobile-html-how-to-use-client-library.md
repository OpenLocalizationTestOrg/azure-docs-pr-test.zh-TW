---
title: "如何使用適用於 Azure Mobile Apps 的 JavaScript SDK"
description: "如何使用適用於 Azure Mobile Apps 的 v"
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 53b78965-caa3-4b22-bb67-5bd5c19d03c4
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 0c4b4de560d70592f5bbdee28b56a7686b5689f4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-the-javascript-client-library-for-azure-mobile-apps"></a><span data-ttu-id="2c114-103">如何使用適用於 Azure Mobile Apps 的 JavaScript 用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="2c114-103">How to Use the JavaScript client library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="2c114-104">本指南將教導您使用最新的 [適用於 Azure Mobile Apps 的 JavaScript SDK]執行一般案例。</span><span class="sxs-lookup"><span data-stu-id="2c114-104">This guide teaches you to perform common scenarios using the latest [JavaScript SDK for Azure Mobile Apps].</span></span> <span data-ttu-id="2c114-105">如果您不熟悉 Azure Mobile Apps，請先完成 [Azure 行動應用程式快速入門] 建立後端，並建立資料表。</span><span class="sxs-lookup"><span data-stu-id="2c114-105">If you are new to Azure Mobile Apps, first complete [Azure Mobile Apps Quick Start] to create a backend and create a table.</span></span> <span data-ttu-id="2c114-106">在本指南中，我們會著重在使用 HTML/JavaScript Web 應用程式中的行動後端。</span><span class="sxs-lookup"><span data-stu-id="2c114-106">In this guide, we focus on using the mobile backend in HTML/JavaScript Web applications.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="2c114-107">支援的平台</span><span class="sxs-lookup"><span data-stu-id="2c114-107">Supported platforms</span></span>
<span data-ttu-id="2c114-108">我們將瀏覽器支援限制在下列主要瀏覽器的當前最新版本：Google Chrome、Microsoft Edge、Microsoft Internet Explorer 和 Mozilla Firefox。</span><span class="sxs-lookup"><span data-stu-id="2c114-108">We limit browser support to the current and last versions of the major browsers:  Google Chrome, Microsoft Edge, Microsoft Internet Explorer, and Mozilla Firefox.</span></span>  <span data-ttu-id="2c114-109">我們預期 SDK 可與任何相對近期的瀏覽器搭配運作。</span><span class="sxs-lookup"><span data-stu-id="2c114-109">We expect the SDK to function with any relatively modern browser.</span></span>

<span data-ttu-id="2c114-110">套件會以通用 JavaScript 模組的形式來散發，因此能夠支援全域、AMD 和 CommonJS 格式。</span><span class="sxs-lookup"><span data-stu-id="2c114-110">The package is distributed as a Universal JavaScript Module, so it supports globals, AMD, and CommonJS formats.</span></span>

## <span data-ttu-id="2c114-111"><a name="Setup"></a>設定和必要條件</span><span class="sxs-lookup"><span data-stu-id="2c114-111"><a name="Setup"></a>Setup and prerequisites</span></span>
<span data-ttu-id="2c114-112">本指南假設您已建立包含資料表的後端。</span><span class="sxs-lookup"><span data-stu-id="2c114-112">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="2c114-113">本指南假設資料表的結構描述與這些教學課程中的資料表相同。</span><span class="sxs-lookup"><span data-stu-id="2c114-113">This guide assumes that the table has the same schema as the tables in those tutorials.</span></span>

<span data-ttu-id="2c114-114">安裝 Azure Mobile Apps JavaScript SDK 可透過 `npm` 命令完成︰</span><span class="sxs-lookup"><span data-stu-id="2c114-114">Installing the Azure Mobile Apps JavaScript SDK can be done via the `npm` command:</span></span>

```
npm install azure-mobile-apps-client --save
```

<span data-ttu-id="2c114-115">程式庫也可在 CommonJS 環境 (例如 Browserify 和 Webpack) 內部做為 ES2015 模組和 AMD 程式庫使用。</span><span class="sxs-lookup"><span data-stu-id="2c114-115">The library can also be used as an ES2015 module, within CommonJS environments such as Browserify and Webpack and as an AMD library.</span></span>  <span data-ttu-id="2c114-116">例如：</span><span class="sxs-lookup"><span data-stu-id="2c114-116">For example:</span></span>

```
# For ECMAScript 5.1 CommonJS
var WindowsAzure = require('azure-mobile-apps-client');
# For ES2015 modules
import * as WindowsAzure from 'azure-mobile-apps-client';
```

<span data-ttu-id="2c114-117">您也可以直接從我們 CDN 下載預先建置 SDK 版本來使用︰</span><span class="sxs-lookup"><span data-stu-id="2c114-117">You can also use a pre-built version of the SDK by downloading directly from our CDN:</span></span>

```html
<script src="https://zumo.blob.core.windows.net/sdk/azure-mobile-apps-client.min.js"></script>
```

[!INCLUDE [app-service-mobile-html-js-library](../../includes/app-service-mobile-html-js-library.md)]

## <span data-ttu-id="2c114-118"><a name="auth"></a>作法：驗證使用者</span><span class="sxs-lookup"><span data-stu-id="2c114-118"><a name="auth"></a>How to: Authenticate users</span></span>
<span data-ttu-id="2c114-119">Azure App Service 支援使用各種外部識別提供者 (Facebook、Google、Microsoft 帳戶及 Twitter) 來驗證與授權應用程式使用者。</span><span class="sxs-lookup"><span data-stu-id="2c114-119">Azure App Service supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, and Twitter.</span></span> <span data-ttu-id="2c114-120">您可以在資料表上設定權限，以限制僅有通過驗證使用者可以存取特定操作。</span><span class="sxs-lookup"><span data-stu-id="2c114-120">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="2c114-121">您也可以在伺服器指令碼中，使用驗證的使用者的身分識別來實作授權規則。</span><span class="sxs-lookup"><span data-stu-id="2c114-121">You can also use the identity of authenticated users to implement authorization rules in server scripts.</span></span> <span data-ttu-id="2c114-122">如需詳細資訊，請參閱 [開始使用驗證] 教學課程。</span><span class="sxs-lookup"><span data-stu-id="2c114-122">For more information, see the [Get started with authentication] tutorial.</span></span>

<span data-ttu-id="2c114-123">支援兩個驗證流程：伺服器流程和用戶端流程。</span><span class="sxs-lookup"><span data-stu-id="2c114-123">Two authentication flows are supported: a server flow and a client flow.</span></span>  <span data-ttu-id="2c114-124">由於伺服器流程採用提供者的 Web 驗證介面，因此所提供的驗證體驗也最為簡單。</span><span class="sxs-lookup"><span data-stu-id="2c114-124">The server flow provides the simplest authentication experience, as it relies on the provider's web authentication interface.</span></span> <span data-ttu-id="2c114-125">用戶端流程依賴提供者專屬的 SDK，可以與裝置特有的功能深入整合，例如單一登入。</span><span class="sxs-lookup"><span data-stu-id="2c114-125">The client flow allows for deeper integration with device-specific capabilities such as single-sign-on as it relies on provider-specific SDKs.</span></span>

[!INCLUDE [app-service-mobile-html-js-auth-library](../../includes/app-service-mobile-html-js-auth-library.md)]

### <span data-ttu-id="2c114-126"><a name="configure-external-redirect-urls"></a>做法︰設定行動 App Service 以使用外部重新導向 URL。</span><span class="sxs-lookup"><span data-stu-id="2c114-126"><a name="configure-external-redirect-urls"></a>How to: Configure your Mobile App Service for external redirect URLs.</span></span>
<span data-ttu-id="2c114-127">有數種類型的 JavaScript 應用程式會使用回送功能來處理 OAuth UI 流程。</span><span class="sxs-lookup"><span data-stu-id="2c114-127">Several types of JavaScript applications use a loopback capability to handle OAuth UI flows.</span></span>  <span data-ttu-id="2c114-128">這些功能包括：</span><span class="sxs-lookup"><span data-stu-id="2c114-128">These capabilities include:</span></span>

* <span data-ttu-id="2c114-129">在本機執行服務</span><span class="sxs-lookup"><span data-stu-id="2c114-129">Running your service locally</span></span>
* <span data-ttu-id="2c114-130">搭配 Ionic 架構使用即時重新載入</span><span class="sxs-lookup"><span data-stu-id="2c114-130">Using Live Reload with the Ionic Framework</span></span>
* <span data-ttu-id="2c114-131">重新導向至 App Service 以進行驗證。</span><span class="sxs-lookup"><span data-stu-id="2c114-131">Redirecting to App Service for authentication.</span></span>

<span data-ttu-id="2c114-132">在本機執行會造成問題，因為根據預設，App Service 驗證只設定為允許從您的行動裝置應用程式後端來存取。</span><span class="sxs-lookup"><span data-stu-id="2c114-132">Running locally can cause problems because, by default, App Service authentication is only configured to allow access from your Mobile App backend.</span></span> <span data-ttu-id="2c114-133">請使用下列步驟來變更 App Service 設定，以便在本機執行伺服器時啟用驗證：</span><span class="sxs-lookup"><span data-stu-id="2c114-133">Use the following steps to change the App Service settings to enable authentication when running the server locally:</span></span>

1. <span data-ttu-id="2c114-134">登入 [Azure 入口網站]</span><span class="sxs-lookup"><span data-stu-id="2c114-134">Log in to the [Azure portal]</span></span>
2. <span data-ttu-id="2c114-135">瀏覽至行動裝置應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="2c114-135">Navigate to your Mobile App backend.</span></span>
3. <span data-ttu-id="2c114-136">選取 [開發工具] 功能表中的 [資源總管]。</span><span class="sxs-lookup"><span data-stu-id="2c114-136">Select **Resource explorer** in the **DEVELOPMENT TOOLS** menu.</span></span>
4. <span data-ttu-id="2c114-137">按一下 [執行]  ，在新的索引標籤或視窗中開啟行動裝置應用程式後端的資源總管。</span><span class="sxs-lookup"><span data-stu-id="2c114-137">Click **Go** to open the resource explorer for your Mobile App backend in a new tab or window.</span></span>
5. <span data-ttu-id="2c114-138">展開應用程式的 [config]  >  [authsettings] 節點。</span><span class="sxs-lookup"><span data-stu-id="2c114-138">Expand the **config** > **authsettings** node for your app.</span></span>
6. <span data-ttu-id="2c114-139">按一下 [編輯]  按鈕來啟用資源的編輯。</span><span class="sxs-lookup"><span data-stu-id="2c114-139">Click the **Edit** button to enable editing of the resource.</span></span>
7. <span data-ttu-id="2c114-140">尋找 **allowedExternalRedirectUrls** 元素，此元素應該是 null。</span><span class="sxs-lookup"><span data-stu-id="2c114-140">Find the **allowedExternalRedirectUrls** element, which should be null.</span></span> <span data-ttu-id="2c114-141">在陣列中新增 URL：</span><span class="sxs-lookup"><span data-stu-id="2c114-141">Add your URLs in an array:</span></span>

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    <span data-ttu-id="2c114-142">使用您服務的 URL 取代陣列中的 URL，在此範例中為本機 Node.js 範例服務的 `http://localhost:3000` 。</span><span class="sxs-lookup"><span data-stu-id="2c114-142">Replace the URLs in the array with the URLs of your service, which in this example is `http://localhost:3000` for the local Node.js sample service.</span></span> <span data-ttu-id="2c114-143">根據您應用程式的設定方式而定，您也可以使用 Ripple 服務的 `http://localhost:4400` 或一些其他的 URL。</span><span class="sxs-lookup"><span data-stu-id="2c114-143">You could also use `http://localhost:4400` for the Ripple service or some other URL, depending on how your app is configured.</span></span>
8. <span data-ttu-id="2c114-144">在頁面頂端，按一下 [讀取/寫入]，然後按一下 [PUT] 以儲存您的更新。</span><span class="sxs-lookup"><span data-stu-id="2c114-144">At the top of the page, click **Read/Write**, then click **PUT** to save your updates.</span></span>

<span data-ttu-id="2c114-145">您還需要將相同的回送 URL 加入至 CORS 白名單設定：</span><span class="sxs-lookup"><span data-stu-id="2c114-145">You also need to add the same loopback URLs to the CORS whitelist settings:</span></span>

1. <span data-ttu-id="2c114-146">瀏覽回 [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="2c114-146">Navigate back to the [Azure portal].</span></span>
2. <span data-ttu-id="2c114-147">瀏覽至行動裝置應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="2c114-147">Navigate to your Mobile App backend.</span></span>
3. <span data-ttu-id="2c114-148">按一下 [API] 功能表中的 [CORS]。</span><span class="sxs-lookup"><span data-stu-id="2c114-148">Click **CORS** in the **API** menu.</span></span>
4. <span data-ttu-id="2c114-149">在空的 [允許的原點]  文字方塊中輸入每一個 URL。</span><span class="sxs-lookup"><span data-stu-id="2c114-149">Enter each URL in the empty **Allowed Origins** text box.</span></span>  <span data-ttu-id="2c114-150">隨即會建立新的文字方塊。</span><span class="sxs-lookup"><span data-stu-id="2c114-150">A new text box is created.</span></span>
5. <span data-ttu-id="2c114-151">按一下 [儲存] </span><span class="sxs-lookup"><span data-stu-id="2c114-151">Click **SAVE**</span></span>

<span data-ttu-id="2c114-152">後端更新之後，您就可以在應用程式中使用新的回送 URL。</span><span class="sxs-lookup"><span data-stu-id="2c114-152">After the backend updates, you will be able to use the new loopback URLs in your app.</span></span>

<!-- URLs. -->
<span data-ttu-id="2c114-153">[Azure 行動應用程式快速入門]: app-service-mobile-cordova-get-started.md</span><span class="sxs-lookup"><span data-stu-id="2c114-153">[Azure Mobile Apps Quick Start]: app-service-mobile-cordova-get-started.md</span></span>
<span data-ttu-id="2c114-154">[開始使用驗證]: app-service-mobile-cordova-get-started-users.md</span><span class="sxs-lookup"><span data-stu-id="2c114-154">[Get started with authentication]: app-service-mobile-cordova-get-started-users.md</span></span>
[Add authentication to your app]: app-service-mobile-cordova-get-started-users.md

<span data-ttu-id="2c114-155">[Azure 入口網站]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="2c114-155">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="2c114-156">[適用於 Azure Mobile Apps 的 JavaScript SDK]: https://www.npmjs.com/package/azure-mobile-apps-client</span><span class="sxs-lookup"><span data-stu-id="2c114-156">[JavaScript SDK for Azure Mobile Apps]: https://www.npmjs.com/package/azure-mobile-apps-client</span></span>
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
