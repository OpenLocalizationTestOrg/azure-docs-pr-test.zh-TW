---
title: "aaaHow tooUse Azure 行動應用程式的 Apache Cordova 外掛程式"
description: "如何 tooUse Azure 行動應用程式的 Apache Cordova 外掛程式"
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: a56a1ce4-de0c-4f3c-8763-66252c52aa59
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: d3e0639e6478c409132af25304a2fb0f28401e98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-apache-cordova-client-library-for-azure-mobile-apps"></a><span data-ttu-id="08b6a-103">如何針對 Azure 行動應用程式的 toouse Apache Cordova 用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="08b6a-103">How toouse Apache Cordova client library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="08b6a-104">本指南將教導您 tooperform 常見的案例，使用最新的 hello [Azure 行動應用程式的 Apache Cordova 外掛程式]。</span><span class="sxs-lookup"><span data-stu-id="08b6a-104">This guide teaches you tooperform common scenarios using hello latest [Apache Cordova Plugin for Azure Mobile Apps].</span></span> <span data-ttu-id="08b6a-105">如果您是新 tooAzure 行動應用程式，請先完成[Azure 行動應用程式快速入門]toocreate 後端，建立資料表，並下載預先建立的 Apache Cordova 專案。</span><span class="sxs-lookup"><span data-stu-id="08b6a-105">If you are new tooAzure Mobile Apps, first complete [Azure Mobile Apps Quick Start] toocreate a backend, create a table, and download a pre-built Apache Cordova project.</span></span> <span data-ttu-id="08b6a-106">本指南中，我們將重點放在用戶端 hello Apache Cordova 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="08b6a-106">In this guide, we focus on hello client-side Apache Cordova Plugin.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="08b6a-107">支援的平台</span><span class="sxs-lookup"><span data-stu-id="08b6a-107">Supported platforms</span></span>
<span data-ttu-id="08b6a-108">此 SDK 可在 iOS、Android 和 Windows 裝置上支援 Apache Cordova v6.0.0 和更新版本。</span><span class="sxs-lookup"><span data-stu-id="08b6a-108">This SDK supports Apache Cordova v6.0.0 and later on iOS, Android, and Windows devices.</span></span>  <span data-ttu-id="08b6a-109">hello 平台支援如下所示：</span><span class="sxs-lookup"><span data-stu-id="08b6a-109">hello platform support is as follows:</span></span>

* <span data-ttu-id="08b6a-110">Android API 19-24 (KitKat 至 Nougat)。</span><span class="sxs-lookup"><span data-stu-id="08b6a-110">Android API 19-24 (KitKat through Nougat).</span></span>
* <span data-ttu-id="08b6a-111">iOS 8.0 版和更新版本。</span><span class="sxs-lookup"><span data-stu-id="08b6a-111">iOS versions 8.0 and later.</span></span>
* <span data-ttu-id="08b6a-112">Windows Phone 8.1。</span><span class="sxs-lookup"><span data-stu-id="08b6a-112">Windows Phone 8.1.</span></span>
* <span data-ttu-id="08b6a-113">通用 Windows 平台。</span><span class="sxs-lookup"><span data-stu-id="08b6a-113">Universal Windows Platform.</span></span>

## <span data-ttu-id="08b6a-114"><a name="Setup"></a>設定和必要條件</span><span class="sxs-lookup"><span data-stu-id="08b6a-114"><a name="Setup"></a>Setup and prerequisites</span></span>
<span data-ttu-id="08b6a-115">本指南假設您已建立包含資料表的後端。</span><span class="sxs-lookup"><span data-stu-id="08b6a-115">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="08b6a-116">本指南假設該 hello 資料表具有 hello 以這些教學課程中的 hello 資料表相同的結構描述。</span><span class="sxs-lookup"><span data-stu-id="08b6a-116">This guide assumes that hello table has hello same schema as hello tables in those tutorials.</span></span> <span data-ttu-id="08b6a-117">本指南也會假設您已經加入 hello tooyour Apache Cordova 外掛程式的程式碼。</span><span class="sxs-lookup"><span data-stu-id="08b6a-117">This guide also assumes that you have added hello Apache Cordova Plugin tooyour code.</span></span>  <span data-ttu-id="08b6a-118">如果您不這麼做，您可以加入 hello Apache Cordova 外掛程式 tooyour 專案 hello 命令列上：</span><span class="sxs-lookup"><span data-stu-id="08b6a-118">If you have not done so, you may add hello Apache Cordova plugin tooyour project on hello command line:</span></span>

```
cordova plugin add cordova-plugin-ms-azure-mobile-apps
```

<span data-ttu-id="08b6a-119">如需有關建立 [第一個 Apache Cordova 應用程式]的詳細資訊，請參閱其文件。</span><span class="sxs-lookup"><span data-stu-id="08b6a-119">For more information on creating [your first Apache Cordova app], see their documentation.</span></span>

## <span data-ttu-id="08b6a-120"><a name="ionic"></a>設定 Ionic v2 應用程式</span><span class="sxs-lookup"><span data-stu-id="08b6a-120"><a name="ionic"></a>Setting up an Ionic v2 app</span></span>

<span data-ttu-id="08b6a-121">tooproperly Ionic v2 專案設定中，第一次建立基本應用程式，並加入 hello Cordova 外掛程式：</span><span class="sxs-lookup"><span data-stu-id="08b6a-121">tooproperly configure an Ionic v2 project, first create a basic app and add hello Cordova plugin:</span></span>

```
ionic start projectName --v2
cd projectName
ionic plugin add cordova-plugin-ms-azure-mobile-apps
```

<span data-ttu-id="08b6a-122">新增下列幾行太 hello`app.component.ts` toocreate hello 用戶端物件：</span><span class="sxs-lookup"><span data-stu-id="08b6a-122">Add hello following lines too`app.component.ts` toocreate hello client object:</span></span>

```
declare var WindowsAzure: any;
var client = new WindowsAzure.MobileServiceClient("https://yoursite.azurewebsites.net");
```

<span data-ttu-id="08b6a-123">您可以立即建立，並在 hello 瀏覽器中執行 hello 專案：</span><span class="sxs-lookup"><span data-stu-id="08b6a-123">You can now build and run hello project in hello browser:</span></span>

```
ionic platform add browser
ionic run browser
```

<span data-ttu-id="08b6a-124">hello Azure 行動應用程式的 Cordova 外掛程式支援兩個 Ionic v1 和 v2 應用程式。</span><span class="sxs-lookup"><span data-stu-id="08b6a-124">hello Azure Mobile Apps Cordova plugin supports both Ionic v1 and v2 apps.</span></span>  <span data-ttu-id="08b6a-125">只有 hello Ionic v2 應用程式需要的其他宣告 hello`WindowsAzure`物件。</span><span class="sxs-lookup"><span data-stu-id="08b6a-125">Only hello Ionic v2 apps require the additional declaration for hello `WindowsAzure` object.</span></span>

[!INCLUDE [app-service-mobile-html-js-library.md](../../includes/app-service-mobile-html-js-library.md)]

## <span data-ttu-id="08b6a-126"><a name="auth"></a>作法：驗證使用者</span><span class="sxs-lookup"><span data-stu-id="08b6a-126"><a name="auth"></a>How to: Authenticate users</span></span>
<span data-ttu-id="08b6a-127">Azure App Service 支援使用各種外部識別提供者 (Facebook、Google、Microsoft 帳戶及 Twitter) 來驗證與授權應用程式使用者。</span><span class="sxs-lookup"><span data-stu-id="08b6a-127">Azure App Service supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, and Twitter.</span></span> <span data-ttu-id="08b6a-128">您可以設定權限針對特定作業的資料表 toorestrict 存取 tooonly 驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="08b6a-128">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="08b6a-129">您也可以使用伺服器指令碼中的 hello 身分識別通過驗證的使用者 tooimplement 授權規則。</span><span class="sxs-lookup"><span data-stu-id="08b6a-129">You can also use hello identity of authenticated users tooimplement authorization rules in server scripts.</span></span> <span data-ttu-id="08b6a-130">如需詳細資訊，請參閱 hello[開始使用驗證]教學課程。</span><span class="sxs-lookup"><span data-stu-id="08b6a-130">For more information, see hello [Get started with authentication] tutorial.</span></span>

<span data-ttu-id="08b6a-131">使用驗證時的 Apache Cordova 應用程式中，必須具備下列 Cordova 外掛程式的 hello:</span><span class="sxs-lookup"><span data-stu-id="08b6a-131">When using authentication in an Apache Cordova app, hello following Cordova plugins must be available:</span></span>

* <span data-ttu-id="08b6a-132">[cordova-plugin-device]</span><span class="sxs-lookup"><span data-stu-id="08b6a-132">[cordova-plugin-device]</span></span>
* <span data-ttu-id="08b6a-133">[cordova-plugin-inappbrowser]</span><span class="sxs-lookup"><span data-stu-id="08b6a-133">[cordova-plugin-inappbrowser]</span></span>

<span data-ttu-id="08b6a-134">支援兩個驗證流程：伺服器流程和用戶端流程。</span><span class="sxs-lookup"><span data-stu-id="08b6a-134">Two authentication flows are supported: a server flow and a client flow.</span></span>  <span data-ttu-id="08b6a-135">hello 伺服器流程提供 hello 最簡單的驗證體驗，因為它是倚賴 hello 提供者 web 驗證介面。</span><span class="sxs-lookup"><span data-stu-id="08b6a-135">hello server flow provides hello simplest authentication experience, as it relies on hello provider's web authentication interface.</span></span> <span data-ttu-id="08b6a-136">hello 用戶端流程可讓與裝置特定功能的更深入整合這類單一登入為依賴特定提供者裝置特有的 Sdk。</span><span class="sxs-lookup"><span data-stu-id="08b6a-136">hello client flow allows for deeper integration with device-specific capabilities such as single-sign-on as it relies on provider-specific device-specific SDKs.</span></span>

[!INCLUDE [app-service-mobile-html-js-auth-library.md](../../includes/app-service-mobile-html-js-auth-library.md)]

### <span data-ttu-id="08b6a-137"><a name="configure-external-redirect-urls"></a>做法︰設定行動 App Service 以使用外部重新導向 URL。</span><span class="sxs-lookup"><span data-stu-id="08b6a-137"><a name="configure-external-redirect-urls"></a>How to: Configure your Mobile App Service for external redirect URLs.</span></span>
<span data-ttu-id="08b6a-138">Apache Cordova 應用程式的數種使用回送功能 toohandle OAuth UI 流動。</span><span class="sxs-lookup"><span data-stu-id="08b6a-138">Several types of Apache Cordova applications use a loopback capability toohandle OAuth UI flows.</span></span>  <span data-ttu-id="08b6a-139">在 localhost 上的 OAuth UI 流量會造成問題，因為 hello 驗證服務只知道如何 tooutilize 您預設的服務。</span><span class="sxs-lookup"><span data-stu-id="08b6a-139">OAuth UI flows on localhost cause problems since hello authentication service only knows how tooutilize your service by default.</span></span>  <span data-ttu-id="08b6a-140">有問題的 OAuth UI 流程範例包括︰</span><span class="sxs-lookup"><span data-stu-id="08b6a-140">Examples of problematic OAuth UI flows include:</span></span>

* <span data-ttu-id="08b6a-141">hello Ripple 模擬器。</span><span class="sxs-lookup"><span data-stu-id="08b6a-141">hello Ripple emulator.</span></span>
* <span data-ttu-id="08b6a-142">Ionic 的即時重新載入。</span><span class="sxs-lookup"><span data-stu-id="08b6a-142">Live Reload with Ionic.</span></span>
* <span data-ttu-id="08b6a-143">在本機執行 hello 行動後端</span><span class="sxs-lookup"><span data-stu-id="08b6a-143">Running hello mobile backend locally</span></span>
* <span data-ttu-id="08b6a-144">執行比 hello 一個提供給驗證的不同 Azure App Service 中的 hello 行動後端。</span><span class="sxs-lookup"><span data-stu-id="08b6a-144">Running hello mobile backend in a different Azure App Service than hello one providing authentication.</span></span>

<span data-ttu-id="08b6a-145">請遵循這些指示 tooadd 您的本機設定 toohello 組態：</span><span class="sxs-lookup"><span data-stu-id="08b6a-145">Follow these instructions tooadd your local settings toohello configuration:</span></span>

1. <span data-ttu-id="08b6a-146">登入 toohello [Azure 入口網站]</span><span class="sxs-lookup"><span data-stu-id="08b6a-146">Log in toohello [Azure portal]</span></span>
2. <span data-ttu-id="08b6a-147">選取**所有資源**或**應用程式服務**然後按一下 [hello 行動應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="08b6a-147">Select **All resources** or **App Services** then click hello name of your Mobile App.</span></span>
3. <span data-ttu-id="08b6a-148">按一下 [工具] </span><span class="sxs-lookup"><span data-stu-id="08b6a-148">Click **Tools**</span></span>
4. <span data-ttu-id="08b6a-149">按一下**資源總管**hello 觀察功能表中，然後按一下**移**。</span><span class="sxs-lookup"><span data-stu-id="08b6a-149">Click **Resource explorer** in hello OBSERVE menu, then click **Go**.</span></span>  <span data-ttu-id="08b6a-150">新的視窗或索引標籤隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="08b6a-150">A new window or tab opens.</span></span>
5. <span data-ttu-id="08b6a-151">展開 hello **config**， **authsettings** hello 左側導覽中您站台的節點。</span><span class="sxs-lookup"><span data-stu-id="08b6a-151">Expand hello **config**, **authsettings** nodes for your site in hello left-hand navigation.</span></span>
6. <span data-ttu-id="08b6a-152">按一下 [編輯] </span><span class="sxs-lookup"><span data-stu-id="08b6a-152">Click **Edit**</span></span>
7. <span data-ttu-id="08b6a-153">尋找 hello"allowedExternalRedirectUrls"項目。</span><span class="sxs-lookup"><span data-stu-id="08b6a-153">Look for hello "allowedExternalRedirectUrls" element.</span></span>  <span data-ttu-id="08b6a-154">它可能設定 toonull 或值的陣列。</span><span class="sxs-lookup"><span data-stu-id="08b6a-154">It may be set toonull or an array of values.</span></span>  <span data-ttu-id="08b6a-155">變更 hello 值 toohello 下列值：</span><span class="sxs-lookup"><span data-stu-id="08b6a-155">Change hello value toohello following value:</span></span>

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    <span data-ttu-id="08b6a-156">Hello Url 取代為您的服務的 hello Url。</span><span class="sxs-lookup"><span data-stu-id="08b6a-156">Replace hello URLs with hello URLs of your service.</span></span>  <span data-ttu-id="08b6a-157">範例包括"http://localhost:3000 」 （適用於 hello Node.js 範例服務) 或 「 http://localhost:4400"（針對 hello Ripple 服務）。</span><span class="sxs-lookup"><span data-stu-id="08b6a-157">Examples include "http://localhost:3000" (for hello Node.js sample service), or "http://localhost:4400" (for hello Ripple service).</span></span>  <span data-ttu-id="08b6a-158">不過，這些 Url 是範例-您的情況，包括 hello 範例中所述的 hello 服務可能會不同。</span><span class="sxs-lookup"><span data-stu-id="08b6a-158">However, these URLs are examples - your situation, including for hello services mentioned in hello examples, may be different.</span></span>
8. <span data-ttu-id="08b6a-159">按一下 hello**讀/寫**hello hello 畫面右上角的按鈕。</span><span class="sxs-lookup"><span data-stu-id="08b6a-159">Click hello **Read/Write** button in hello top-right corner of hello screen.</span></span>
9. <span data-ttu-id="08b6a-160">按一下綠色的 hello**放**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="08b6a-160">Click hello green **PUT** button.</span></span>

<span data-ttu-id="08b6a-161">此時會儲存 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="08b6a-161">hello settings are saved at this point.</span></span>  <span data-ttu-id="08b6a-162">請勿關閉 hello 瀏覽器視窗中，直到 hello 設定儲存。</span><span class="sxs-lookup"><span data-stu-id="08b6a-162">Do not close hello browser window until hello settings have finished saving.</span></span>
<span data-ttu-id="08b6a-163">也新增回送 Url toohello CORS 的這些設定您的應用程式服務：</span><span class="sxs-lookup"><span data-stu-id="08b6a-163">Also add these loopback URLs toohello CORS settings for your App Service:</span></span>

1. <span data-ttu-id="08b6a-164">登入 toohello [Azure 入口網站]</span><span class="sxs-lookup"><span data-stu-id="08b6a-164">Log in toohello [Azure portal]</span></span>
2. <span data-ttu-id="08b6a-165">選取**所有資源**或**應用程式服務**然後按一下 [hello 行動應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="08b6a-165">Select **All resources** or **App Services** then click hello name of your Mobile App.</span></span>
3. <span data-ttu-id="08b6a-166">hello 設定] 刀鋒視窗會自動開啟。</span><span class="sxs-lookup"><span data-stu-id="08b6a-166">hello Settings blade opens automatically.</span></span>  <span data-ttu-id="08b6a-167">如果沒有，請按一下 [所有設定] 。</span><span class="sxs-lookup"><span data-stu-id="08b6a-167">If it doesn't, click **All Settings**.</span></span>
4. <span data-ttu-id="08b6a-168">按一下**CORS** hello 應用程式開發介面] 功能表底下。</span><span class="sxs-lookup"><span data-stu-id="08b6a-168">Click **CORS** under hello API menu.</span></span>
5. <span data-ttu-id="08b6a-169">輸入您想 tooadd hello 提供的方塊中的 hello URL，然後按 Enter。</span><span class="sxs-lookup"><span data-stu-id="08b6a-169">Enter hello URL that you wish tooadd in hello box provided and press Enter.</span></span>
6. <span data-ttu-id="08b6a-170">視需要輸入其他的 URL。</span><span class="sxs-lookup"><span data-stu-id="08b6a-170">Enter additional URLs as needed.</span></span>
7. <span data-ttu-id="08b6a-171">按一下**儲存**toosave hello 設定。</span><span class="sxs-lookup"><span data-stu-id="08b6a-171">Click **Save** toosave hello settings.</span></span>

<span data-ttu-id="08b6a-172">需要大約 10-15 秒 hello 新設定 tootake 效果。</span><span class="sxs-lookup"><span data-stu-id="08b6a-172">It takes approximately 10-15 seconds for hello new settings tootake effect.</span></span>

## <span data-ttu-id="08b6a-173"><a name="register-for-push"></a>作法：註冊推播通知</span><span class="sxs-lookup"><span data-stu-id="08b6a-173"><a name="register-for-push"></a>How to: Register for push notifications</span></span>
<span data-ttu-id="08b6a-174">安裝 hello [phonegap 外掛程式的推播]toohandle 推播通知。</span><span class="sxs-lookup"><span data-stu-id="08b6a-174">Install hello [phonegap-plugin-push] toohandle push notifications.</span></span>  <span data-ttu-id="08b6a-175">此外掛程式可以輕鬆地新增使用`cordova plugin add`命令 hello 命令列上，或透過 Visual Studio 中的 hello Git 外掛程式安裝程式。</span><span class="sxs-lookup"><span data-stu-id="08b6a-175">This plugin can be easily added using the `cordova plugin add` command on hello command line, or via hello Git plugin installer within Visual Studio.</span></span>  <span data-ttu-id="08b6a-176">以下在 Apache Cordova 應用程式中的程式碼會為您的裝置註冊推播通知：</span><span class="sxs-lookup"><span data-stu-id="08b6a-176">The following code in your Apache Cordova app registers your device for push notifications:</span></span>

```
var pushOptions = {
    android: {
        senderId: '<from-gcm-console>'
    },
    ios: {
        alert: true,
        badge: true,
        sound: true
    },
    windows: {
    }
};
pushHandler = PushNotification.init(pushOptions);

pushHandler.on('registration', function (data) {
    registrationId = data.registrationId;
    // For cross-platform, you can use hello device plugin toodetermine hello device
    // Best is toouse device.platform
    var name = 'gcm'; // For android - default
    if (device.platform.toLowerCase() === 'ios')
        name = 'apns';
    if (device.platform.toLowerCase().substring(0, 3) === 'win')
        name = 'wns';
    client.push.register(name, registrationId);
});

pushHandler.on('notification', function (data) {
    // data is an object and is whatever is sent by hello PNS - check hello format
    // for your particular PNS
});

pushHandler.on('error', function (error) {
    // Handle errors
});
```

<span data-ttu-id="08b6a-177">使用從 hello 伺服器 hello 通知中樞 SDK toosend 推播通知。</span><span class="sxs-lookup"><span data-stu-id="08b6a-177">Use hello Notification Hubs SDK toosend push notifications from hello server.</span></span>  <span data-ttu-id="08b6a-178">永遠不要直接從用戶端傳送推播通知。</span><span class="sxs-lookup"><span data-stu-id="08b6a-178">Never send push notifications directly from clients.</span></span> <span data-ttu-id="08b6a-179">這樣做，可以使用的 tootrigger 阻絕服務攻擊通知中樞或 hello PNS。</span><span class="sxs-lookup"><span data-stu-id="08b6a-179">Doing so could be used tootrigger a denial of service attack against Notification Hubs or hello PNS.</span></span>  <span data-ttu-id="08b6a-180">hello PNS 可能禁止您的流量，因為這類攻擊。</span><span class="sxs-lookup"><span data-stu-id="08b6a-180">hello PNS could ban your traffic as a result of such attacks.</span></span>

## <a name="more-information"></a><span data-ttu-id="08b6a-181">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="08b6a-181">More information</span></span>

<span data-ttu-id="08b6a-182">您可以在 [API 文件](http://azure.github.io/azure-mobile-apps-js-client/)中找到 API 詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="08b6a-182">You can find detailed API details in our [API documentation](http://azure.github.io/azure-mobile-apps-js-client/).</span></span>

<!-- URLs. -->
[Azure 入口網站]: https://portal.azure.com
[Azure Mobile Apps 快速啟動]: app-service-mobile-cordova-get-started.md
[開始使用驗證]: app-service-mobile-cordova-get-started-users.md
[Add authentication tooyour app]: app-service-mobile-cordova-get-started-users.md

[適用於 Azure Mobile Apps 的 Apache Cordova 外掛程式]: https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-apps
[第一個 Apache Cordova 應用程式]: http://cordova.apache.org/#getstarted
[phonegap-facebook-plugin]: https://github.com/wizcorp/phonegap-facebook-plugin
[phonegap-plugin-push]: https://www.npmjs.com/package/phonegap-plugin-push
[cordova-plugin-device]: https://www.npmjs.com/package/cordova-plugin-device
[cordova-plugin-inappbrowser]: https://www.npmjs.com/package/cordova-plugin-inappbrowser
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
