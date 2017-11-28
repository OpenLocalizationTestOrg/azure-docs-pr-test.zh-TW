---
title: "aaaHow tooUse hello Azure 行動應用程式的 JavaScript SDK"
description: "如何 tooUse v Azure 行動應用程式"
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
ms.openlocfilehash: 3fcbb0c5bd6918a285bdafa1946ba0bd47bb21b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-javascript-client-library-for-azure-mobile-apps"></a><span data-ttu-id="e1eff-103">如何 tooUse hello Azure 行動應用程式的 JavaScript 用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="e1eff-103">How tooUse hello JavaScript client library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="e1eff-104">本指南將教導您 tooperform 常見的案例，使用最新的 hello [Azure 行動應用程式的 JavaScript SDK]。</span><span class="sxs-lookup"><span data-stu-id="e1eff-104">This guide teaches you tooperform common scenarios using hello latest [JavaScript SDK for Azure Mobile Apps].</span></span> <span data-ttu-id="e1eff-105">如果您是新 tooAzure 行動應用程式，請先完成[Azure 行動應用程式快速入門]toocreate 後端及建立資料表。</span><span class="sxs-lookup"><span data-stu-id="e1eff-105">If you are new tooAzure Mobile Apps, first complete [Azure Mobile Apps Quick Start] toocreate a backend and create a table.</span></span> <span data-ttu-id="e1eff-106">在本指南中，我們會著重在使用 HTML/JavaScript Web 應用程式中的 hello 行動後端。</span><span class="sxs-lookup"><span data-stu-id="e1eff-106">In this guide, we focus on using hello mobile backend in HTML/JavaScript Web applications.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="e1eff-107">支援的平台</span><span class="sxs-lookup"><span data-stu-id="e1eff-107">Supported platforms</span></span>
<span data-ttu-id="e1eff-108">我們限制瀏覽器支援 toohello 目前，和最後一個版本的 hello 主要瀏覽器： Google Chrome、 Microsoft Edge、 Microsoft Internet Explorer 和 Mozilla Firefox。</span><span class="sxs-lookup"><span data-stu-id="e1eff-108">We limit browser support toohello current and last versions of hello major browsers:  Google Chrome, Microsoft Edge, Microsoft Internet Explorer, and Mozilla Firefox.</span></span>  <span data-ttu-id="e1eff-109">我們預期 hello SDK toofunction 任何較新型的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="e1eff-109">We expect hello SDK toofunction with any relatively modern browser.</span></span>

<span data-ttu-id="e1eff-110">hello 發佈套件為通用 JavaScript 模組，讓它支援 AMD 的全域與 CommonJS 格式。</span><span class="sxs-lookup"><span data-stu-id="e1eff-110">hello package is distributed as a Universal JavaScript Module, so it supports globals, AMD, and CommonJS formats.</span></span>

## <span data-ttu-id="e1eff-111"><a name="Setup"></a>設定和必要條件</span><span class="sxs-lookup"><span data-stu-id="e1eff-111"><a name="Setup"></a>Setup and prerequisites</span></span>
<span data-ttu-id="e1eff-112">本指南假設您已建立包含資料表的後端。</span><span class="sxs-lookup"><span data-stu-id="e1eff-112">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="e1eff-113">本指南假設該 hello 資料表具有 hello 以這些教學課程中的 hello 資料表相同的結構描述。</span><span class="sxs-lookup"><span data-stu-id="e1eff-113">This guide assumes that hello table has hello same schema as hello tables in those tutorials.</span></span>

<span data-ttu-id="e1eff-114">安裝 Azure 行動應用程式 JavaScript SDK hello 可透過 hello`npm`命令：</span><span class="sxs-lookup"><span data-stu-id="e1eff-114">Installing hello Azure Mobile Apps JavaScript SDK can be done via hello `npm` command:</span></span>

```
npm install azure-mobile-apps-client --save
```

<span data-ttu-id="e1eff-115">hello 程式庫也可用為 ES2015 模組，例如 Browserify 和 Webpack，以及為 AMD 程式庫的 CommonJS 環境內。</span><span class="sxs-lookup"><span data-stu-id="e1eff-115">hello library can also be used as an ES2015 module, within CommonJS environments such as Browserify and Webpack and as an AMD library.</span></span>  <span data-ttu-id="e1eff-116">例如：</span><span class="sxs-lookup"><span data-stu-id="e1eff-116">For example:</span></span>

```
# For ECMAScript 5.1 CommonJS
var WindowsAzure = require('azure-mobile-apps-client');
# For ES2015 modules
import * as WindowsAzure from 'azure-mobile-apps-client';
```

<span data-ttu-id="e1eff-117">您也可以直接從我們 CDN 下載使用的預先建立的 hello SDK 版本：</span><span class="sxs-lookup"><span data-stu-id="e1eff-117">You can also use a pre-built version of hello SDK by downloading directly from our CDN:</span></span>

```html
<script src="https://zumo.blob.core.windows.net/sdk/azure-mobile-apps-client.min.js"></script>
```

[!INCLUDE [app-service-mobile-html-js-library](../../includes/app-service-mobile-html-js-library.md)]

## <span data-ttu-id="e1eff-118"><a name="auth"></a>作法：驗證使用者</span><span class="sxs-lookup"><span data-stu-id="e1eff-118"><a name="auth"></a>How to: Authenticate users</span></span>
<span data-ttu-id="e1eff-119">Azure App Service 支援使用各種外部識別提供者 (Facebook、Google、Microsoft 帳戶及 Twitter) 來驗證與授權應用程式使用者。</span><span class="sxs-lookup"><span data-stu-id="e1eff-119">Azure App Service supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, and Twitter.</span></span> <span data-ttu-id="e1eff-120">您可以設定權限針對特定作業的資料表 toorestrict 存取 tooonly 驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="e1eff-120">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="e1eff-121">您也可以使用伺服器指令碼中的 hello 身分識別通過驗證的使用者 tooimplement 授權規則。</span><span class="sxs-lookup"><span data-stu-id="e1eff-121">You can also use hello identity of authenticated users tooimplement authorization rules in server scripts.</span></span> <span data-ttu-id="e1eff-122">如需詳細資訊，請參閱 hello[開始使用驗證]教學課程。</span><span class="sxs-lookup"><span data-stu-id="e1eff-122">For more information, see hello [Get started with authentication] tutorial.</span></span>

<span data-ttu-id="e1eff-123">支援兩個驗證流程：伺服器流程和用戶端流程。</span><span class="sxs-lookup"><span data-stu-id="e1eff-123">Two authentication flows are supported: a server flow and a client flow.</span></span>  <span data-ttu-id="e1eff-124">hello 伺服器流程提供 hello 最簡單的驗證體驗，因為它是倚賴 hello 提供者 web 驗證介面。</span><span class="sxs-lookup"><span data-stu-id="e1eff-124">hello server flow provides hello simplest authentication experience, as it relies on hello provider's web authentication interface.</span></span> <span data-ttu-id="e1eff-125">hello 用戶端流程可讓與裝置特定功能的更深入整合這類單一登入因為這樣必須提供者特有的 Sdk。</span><span class="sxs-lookup"><span data-stu-id="e1eff-125">hello client flow allows for deeper integration with device-specific capabilities such as single-sign-on as it relies on provider-specific SDKs.</span></span>

[!INCLUDE [app-service-mobile-html-js-auth-library](../../includes/app-service-mobile-html-js-auth-library.md)]

### <span data-ttu-id="e1eff-126"><a name="configure-external-redirect-urls"></a>做法︰設定行動 App Service 以使用外部重新導向 URL。</span><span class="sxs-lookup"><span data-stu-id="e1eff-126"><a name="configure-external-redirect-urls"></a>How to: Configure your Mobile App Service for external redirect URLs.</span></span>
<span data-ttu-id="e1eff-127">JavaScript 應用程式的數種使用回送功能 toohandle OAuth UI 流動。</span><span class="sxs-lookup"><span data-stu-id="e1eff-127">Several types of JavaScript applications use a loopback capability toohandle OAuth UI flows.</span></span>  <span data-ttu-id="e1eff-128">這些功能包括：</span><span class="sxs-lookup"><span data-stu-id="e1eff-128">These capabilities include:</span></span>

* <span data-ttu-id="e1eff-129">在本機執行服務</span><span class="sxs-lookup"><span data-stu-id="e1eff-129">Running your service locally</span></span>
* <span data-ttu-id="e1eff-130">使用即時重新載入以 hello Ionic 架構</span><span class="sxs-lookup"><span data-stu-id="e1eff-130">Using Live Reload with hello Ionic Framework</span></span>
* <span data-ttu-id="e1eff-131">重新導向 tooApp 服務進行驗證。</span><span class="sxs-lookup"><span data-stu-id="e1eff-131">Redirecting tooApp Service for authentication.</span></span>

<span data-ttu-id="e1eff-132">在本機執行會造成問題，因為根據預設，應用程式服務驗證，才設定 tooallow 從您的行動裝置應用程式後端的存取。</span><span class="sxs-lookup"><span data-stu-id="e1eff-132">Running locally can cause problems because, by default, App Service authentication is only configured tooallow access from your Mobile App backend.</span></span> <span data-ttu-id="e1eff-133">使用下列步驟 toochange hello 應用程式服務設定 tooenable 驗證時在本機執行 hello 伺服器 hello:</span><span class="sxs-lookup"><span data-stu-id="e1eff-133">Use hello following steps toochange hello App Service settings tooenable authentication when running hello server locally:</span></span>

1. <span data-ttu-id="e1eff-134">登入 toohello [Azure 入口網站]</span><span class="sxs-lookup"><span data-stu-id="e1eff-134">Log in toohello [Azure portal]</span></span>
2. <span data-ttu-id="e1eff-135">瀏覽 tooyour 行動裝置應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="e1eff-135">Navigate tooyour Mobile App backend.</span></span>
3. <span data-ttu-id="e1eff-136">選取**資源總管**在 hello**開發工具**功能表。</span><span class="sxs-lookup"><span data-stu-id="e1eff-136">Select **Resource explorer** in hello **DEVELOPMENT TOOLS** menu.</span></span>
4. <span data-ttu-id="e1eff-137">按一下**移**tooopen hello 資源總管，您的行動裝置應用程式後端，在新的索引標籤或視窗中。</span><span class="sxs-lookup"><span data-stu-id="e1eff-137">Click **Go** tooopen hello resource explorer for your Mobile App backend in a new tab or window.</span></span>
5. <span data-ttu-id="e1eff-138">展開 hello **config** > **authsettings**您應用程式節點。</span><span class="sxs-lookup"><span data-stu-id="e1eff-138">Expand hello **config** > **authsettings** node for your app.</span></span>
6. <span data-ttu-id="e1eff-139">按一下 hello**編輯**按鈕 tooenable 編輯 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="e1eff-139">Click hello **Edit** button tooenable editing of hello resource.</span></span>
7. <span data-ttu-id="e1eff-140">尋找 hello **allowedExternalRedirectUrls**元素，其應為 null。</span><span class="sxs-lookup"><span data-stu-id="e1eff-140">Find hello **allowedExternalRedirectUrls** element, which should be null.</span></span> <span data-ttu-id="e1eff-141">在陣列中新增 URL：</span><span class="sxs-lookup"><span data-stu-id="e1eff-141">Add your URLs in an array:</span></span>

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    <span data-ttu-id="e1eff-142">Hello hello 陣列中的 Url 取代為您的服務，即在此範例中的 hello Url `http://localhost:3000` hello 本機 Node.js 範例服務。</span><span class="sxs-lookup"><span data-stu-id="e1eff-142">Replace hello URLs in hello array with hello URLs of your service, which in this example is `http://localhost:3000` for hello local Node.js sample service.</span></span> <span data-ttu-id="e1eff-143">您也可以使用`http://localhost:4400`hello Ripple 服務或某些其他 URL，根據您的應用程式的設定方式。</span><span class="sxs-lookup"><span data-stu-id="e1eff-143">You could also use `http://localhost:4400` for hello Ripple service or some other URL, depending on how your app is configured.</span></span>
8. <span data-ttu-id="e1eff-144">在 hello hello 頁面頂端，按一下 [**讀/寫**，然後按一下 [**放**toosave 您的更新。</span><span class="sxs-lookup"><span data-stu-id="e1eff-144">At hello top of hello page, click **Read/Write**, then click **PUT** toosave your updates.</span></span>

<span data-ttu-id="e1eff-145">您也需要 tooadd hello 相同回送 Url toohello CORS 白名單的設定：</span><span class="sxs-lookup"><span data-stu-id="e1eff-145">You also need tooadd hello same loopback URLs toohello CORS whitelist settings:</span></span>

1. <span data-ttu-id="e1eff-146">瀏覽後 toohello [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="e1eff-146">Navigate back toohello [Azure portal].</span></span>
2. <span data-ttu-id="e1eff-147">瀏覽 tooyour 行動裝置應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="e1eff-147">Navigate tooyour Mobile App backend.</span></span>
3. <span data-ttu-id="e1eff-148">按一下**CORS**在 hello **API**功能表。</span><span class="sxs-lookup"><span data-stu-id="e1eff-148">Click **CORS** in hello **API** menu.</span></span>
4. <span data-ttu-id="e1eff-149">輸入每個 URL 中空白 hello**允許出處**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="e1eff-149">Enter each URL in hello empty **Allowed Origins** text box.</span></span>  <span data-ttu-id="e1eff-150">隨即會建立新的文字方塊。</span><span class="sxs-lookup"><span data-stu-id="e1eff-150">A new text box is created.</span></span>
5. <span data-ttu-id="e1eff-151">按一下 [儲存] </span><span class="sxs-lookup"><span data-stu-id="e1eff-151">Click **SAVE**</span></span>

<span data-ttu-id="e1eff-152">Hello 後端的更新之後，您將應用程式中是無法 toouse hello 新的回送 Url。</span><span class="sxs-lookup"><span data-stu-id="e1eff-152">After hello backend updates, you will be able toouse hello new loopback URLs in your app.</span></span>

<!-- URLs. -->
[Azure Mobile Apps 快速啟動]: app-service-mobile-cordova-get-started.md
[開始使用驗證]: app-service-mobile-cordova-get-started-users.md
[Add authentication tooyour app]: app-service-mobile-cordova-get-started-users.md

[Azure 入口網站]: https://portal.azure.com/
[適用於 Azure Mobile Apps 的 JavaScript SDK]: https://www.npmjs.com/package/azure-mobile-apps-client
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
