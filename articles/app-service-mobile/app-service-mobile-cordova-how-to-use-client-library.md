---
title: "如何使用適用於 Azure Mobile Apps 的 Apache Cordova 外掛程式"
description: "如何使用適用於 Azure Mobile Apps 的 Apache Cordova 外掛程式"
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
ms.openlocfilehash: ebf0e911eeada0e529f908dd3e3430c94edae763
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-apache-cordova-client-library-for-azure-mobile-apps"></a><span data-ttu-id="8f8aa-103">如何使用適用於 Azure Mobile Apps 的 Apache Cordova 用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="8f8aa-103">How to use Apache Cordova client library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="8f8aa-104">本指南說明如何使用最新的 [適用於 Azure Mobile Apps 的 Apache Cordova 外掛程式]執行一般案例。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-104">This guide teaches you to perform common scenarios using the latest [Apache Cordova Plugin for Azure Mobile Apps].</span></span> <span data-ttu-id="8f8aa-105">如果您是 Azure Mobile Apps 的新手，請先完成 [Azure Mobile Apps 快速啟動] 以建立後端、建立資料表及下載預先建置的 Apache Cordova 專案。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-105">If you are new to Azure Mobile Apps, first complete [Azure Mobile Apps Quick Start] to create a backend, create a table, and download a pre-built Apache Cordova project.</span></span> <span data-ttu-id="8f8aa-106">在本指南中，我們會著重於用戶端 Apache Cordova 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-106">In this guide, we focus on the client-side Apache Cordova Plugin.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="8f8aa-107">支援的平台</span><span class="sxs-lookup"><span data-stu-id="8f8aa-107">Supported platforms</span></span>
<span data-ttu-id="8f8aa-108">此 SDK 可在 iOS、Android 和 Windows 裝置上支援 Apache Cordova v6.0.0 和更新版本。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-108">This SDK supports Apache Cordova v6.0.0 and later on iOS, Android, and Windows devices.</span></span>  <span data-ttu-id="8f8aa-109">平台支援如下︰</span><span class="sxs-lookup"><span data-stu-id="8f8aa-109">The platform support is as follows:</span></span>

* <span data-ttu-id="8f8aa-110">Android API 19-24 (KitKat 至 Nougat)。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-110">Android API 19-24 (KitKat through Nougat).</span></span>
* <span data-ttu-id="8f8aa-111">iOS 8.0 版和更新版本。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-111">iOS versions 8.0 and later.</span></span>
* <span data-ttu-id="8f8aa-112">Windows Phone 8.1。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-112">Windows Phone 8.1.</span></span>
* <span data-ttu-id="8f8aa-113">通用 Windows 平台。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-113">Universal Windows Platform.</span></span>

## <span data-ttu-id="8f8aa-114"><a name="Setup"></a>設定和必要條件</span><span class="sxs-lookup"><span data-stu-id="8f8aa-114"><a name="Setup"></a>Setup and prerequisites</span></span>
<span data-ttu-id="8f8aa-115">本指南假設您已建立包含資料表的後端。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-115">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="8f8aa-116">本指南假設資料表的結構描述與這些教學課程中的資料表相同。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-116">This guide assumes that the table has the same schema as the tables in those tutorials.</span></span> <span data-ttu-id="8f8aa-117">本指南也假設您已將 Apache Cordova 外掛程式加入至程式碼。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-117">This guide also assumes that you have added the Apache Cordova Plugin to your code.</span></span>  <span data-ttu-id="8f8aa-118">如果您還沒有這樣做，您可以在命令列將 Apache Cordova 外掛程式新增至您的專案：</span><span class="sxs-lookup"><span data-stu-id="8f8aa-118">If you have not done so, you may add the Apache Cordova plugin to your project on the command line:</span></span>

```
cordova plugin add cordova-plugin-ms-azure-mobile-apps
```

<span data-ttu-id="8f8aa-119">如需有關建立 [第一個 Apache Cordova 應用程式]的詳細資訊，請參閱其文件。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-119">For more information on creating [your first Apache Cordova app], see their documentation.</span></span>

## <span data-ttu-id="8f8aa-120"><a name="ionic"></a>設定 Ionic v2 應用程式</span><span class="sxs-lookup"><span data-stu-id="8f8aa-120"><a name="ionic"></a>Setting up an Ionic v2 app</span></span>

<span data-ttu-id="8f8aa-121">若要適當地定 Ionic v2 專案，請先建立基本應用程式，並新增 Cordova 外掛程式：</span><span class="sxs-lookup"><span data-stu-id="8f8aa-121">To properly configure an Ionic v2 project, first create a basic app and add the Cordova plugin:</span></span>

```
ionic start projectName --v2
cd projectName
ionic plugin add cordova-plugin-ms-azure-mobile-apps
```

<span data-ttu-id="8f8aa-122">新增下列行到 `app.component.ts` 以建立用戶端專案：</span><span class="sxs-lookup"><span data-stu-id="8f8aa-122">Add the following lines to `app.component.ts` to create the client object:</span></span>

```
declare var WindowsAzure: any;
var client = new WindowsAzure.MobileServiceClient("https://yoursite.azurewebsites.net");
```

<span data-ttu-id="8f8aa-123">您現在可以在瀏覽器中建置並執行專案：</span><span class="sxs-lookup"><span data-stu-id="8f8aa-123">You can now build and run the project in the browser:</span></span>

```
ionic platform add browser
ionic run browser
```

<span data-ttu-id="8f8aa-124">Azure Mobile Apps Cordova 外掛程式同時支援 Ionic v1 與 v2 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-124">The Azure Mobile Apps Cordova plugin supports both Ionic v1 and v2 apps.</span></span>  <span data-ttu-id="8f8aa-125">只有 Ionic v2 應用程式需要 `WindowsAzure` 物件的其他宣告。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-125">Only the Ionic v2 apps require the additional declaration for the `WindowsAzure` object.</span></span>

[!INCLUDE [app-service-mobile-html-js-library.md](../../includes/app-service-mobile-html-js-library.md)]

## <span data-ttu-id="8f8aa-126"><a name="auth"></a>作法：驗證使用者</span><span class="sxs-lookup"><span data-stu-id="8f8aa-126"><a name="auth"></a>How to: Authenticate users</span></span>
<span data-ttu-id="8f8aa-127">Azure App Service 支援使用各種外部識別提供者 (Facebook、Google、Microsoft 帳戶及 Twitter) 來驗證與授權應用程式使用者。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-127">Azure App Service supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, and Twitter.</span></span> <span data-ttu-id="8f8aa-128">您可以在資料表上設定權限，以限制僅有通過驗證使用者可以存取特定操作。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-128">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="8f8aa-129">您也可以在伺服器指令碼中，使用驗證的使用者的身分識別來實作授權規則。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-129">You can also use the identity of authenticated users to implement authorization rules in server scripts.</span></span> <span data-ttu-id="8f8aa-130">如需詳細資訊，請參閱 [開始使用驗證] 教學課程。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-130">For more information, see the [Get started with authentication] tutorial.</span></span>

<span data-ttu-id="8f8aa-131">在 Apache Cordova 應用程式中使用驗證時，下列 Cordova 外掛程式必須可用：</span><span class="sxs-lookup"><span data-stu-id="8f8aa-131">When using authentication in an Apache Cordova app, the following Cordova plugins must be available:</span></span>

* <span data-ttu-id="8f8aa-132">[cordova-plugin-device]</span><span class="sxs-lookup"><span data-stu-id="8f8aa-132">[cordova-plugin-device]</span></span>
* <span data-ttu-id="8f8aa-133">[cordova-plugin-inappbrowser]</span><span class="sxs-lookup"><span data-stu-id="8f8aa-133">[cordova-plugin-inappbrowser]</span></span>

<span data-ttu-id="8f8aa-134">支援兩個驗證流程：伺服器流程和用戶端流程。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-134">Two authentication flows are supported: a server flow and a client flow.</span></span>  <span data-ttu-id="8f8aa-135">由於伺服器流程採用提供者的 Web 驗證介面，因此所提供的驗證體驗也最為簡單。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-135">The server flow provides the simplest authentication experience, as it relies on the provider's web authentication interface.</span></span> <span data-ttu-id="8f8aa-136">用戶端流程依賴提供者專屬的裝置專用 SDK，可以與裝置特有的功能深入整合，例如單一登入。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-136">The client flow allows for deeper integration with device-specific capabilities such as single-sign-on as it relies on provider-specific device-specific SDKs.</span></span>

[!INCLUDE [app-service-mobile-html-js-auth-library.md](../../includes/app-service-mobile-html-js-auth-library.md)]

### <span data-ttu-id="8f8aa-137"><a name="configure-external-redirect-urls"></a>做法︰設定行動 App Service 以使用外部重新導向 URL。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-137"><a name="configure-external-redirect-urls"></a>How to: Configure your Mobile App Service for external redirect URLs.</span></span>
<span data-ttu-id="8f8aa-138">有數種類型的 Apache Cordova 應用程式會使用回送功能來處理 OAuth UI 流程。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-138">Several types of Apache Cordova applications use a loopback capability to handle OAuth UI flows.</span></span>  <span data-ttu-id="8f8aa-139">驗證服務預設只知道如何使用您的服務，因此 localhost 上的 OAuth UI 流程會引發問題。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-139">OAuth UI flows on localhost cause problems since the authentication service only knows how to utilize your service by default.</span></span>  <span data-ttu-id="8f8aa-140">有問題的 OAuth UI 流程範例包括︰</span><span class="sxs-lookup"><span data-stu-id="8f8aa-140">Examples of problematic OAuth UI flows include:</span></span>

* <span data-ttu-id="8f8aa-141">Ripple 模擬器。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-141">The Ripple emulator.</span></span>
* <span data-ttu-id="8f8aa-142">Ionic 的即時重新載入。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-142">Live Reload with Ionic.</span></span>
* <span data-ttu-id="8f8aa-143">在本機執行行動後端</span><span class="sxs-lookup"><span data-stu-id="8f8aa-143">Running the mobile backend locally</span></span>
* <span data-ttu-id="8f8aa-144">在不同於提供驗證的 Azure App Service 中執行行動後端。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-144">Running the mobile backend in a different Azure App Service than the one providing authentication.</span></span>

<span data-ttu-id="8f8aa-145">請遵循下列指示來將您的本機設定加入組態︰</span><span class="sxs-lookup"><span data-stu-id="8f8aa-145">Follow these instructions to add your local settings to the configuration:</span></span>

1. <span data-ttu-id="8f8aa-146">登入 [Azure 入口網站]</span><span class="sxs-lookup"><span data-stu-id="8f8aa-146">Log in to the [Azure portal]</span></span>
2. <span data-ttu-id="8f8aa-147">選取 [所有資源] 或 [應用程式服務]，然後按一下行動應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-147">Select **All resources** or **App Services** then click the name of your Mobile App.</span></span>
3. <span data-ttu-id="8f8aa-148">按一下 [工具] </span><span class="sxs-lookup"><span data-stu-id="8f8aa-148">Click **Tools**</span></span>
4. <span data-ttu-id="8f8aa-149">按一下 [觀察] 功能表中的 [資源總管]，然後按一下 [前往]。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-149">Click **Resource explorer** in the OBSERVE menu, then click **Go**.</span></span>  <span data-ttu-id="8f8aa-150">新的視窗或索引標籤隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-150">A new window or tab opens.</span></span>
5. <span data-ttu-id="8f8aa-151">在左側導覽中，展開網站的 [config]、[authsettings] 節點。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-151">Expand the **config**, **authsettings** nodes for your site in the left-hand navigation.</span></span>
6. <span data-ttu-id="8f8aa-152">按一下 [編輯] </span><span class="sxs-lookup"><span data-stu-id="8f8aa-152">Click **Edit**</span></span>
7. <span data-ttu-id="8f8aa-153">尋找「allowedExternalRedirectUrls」元素。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-153">Look for the "allowedExternalRedirectUrls" element.</span></span>  <span data-ttu-id="8f8aa-154">它可能會設定為 null 或值陣列。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-154">It may be set to null or an array of values.</span></span>  <span data-ttu-id="8f8aa-155">將此值變更為下列值︰</span><span class="sxs-lookup"><span data-stu-id="8f8aa-155">Change the value to the following value:</span></span>

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    <span data-ttu-id="8f8aa-156">使用您服務的 URL 來取代 URL。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-156">Replace the URLs with the URLs of your service.</span></span>  <span data-ttu-id="8f8aa-157">範例包括 "http://localhost:3000" (適用於 Node.js 範例服務) 或 "http://localhost:4400" (適用於 Ripple 服務)。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-157">Examples include "http://localhost:3000" (for the Node.js sample service), or "http://localhost:4400" (for the Ripple service).</span></span>  <span data-ttu-id="8f8aa-158">不過，這些 URL 都是範例 - 您的情況 (包括範例中提及的服務) 可能會有差異。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-158">However, these URLs are examples - your situation, including for the services mentioned in the examples, may be different.</span></span>
8. <span data-ttu-id="8f8aa-159">按一下螢幕右上角的 [讀/寫]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-159">Click the **Read/Write** button in the top-right corner of the screen.</span></span>
9. <span data-ttu-id="8f8aa-160">按一下綠色 [PUT]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-160">Click the green **PUT** button.</span></span>

<span data-ttu-id="8f8aa-161">此時即會儲存設定。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-161">The settings are saved at this point.</span></span>  <span data-ttu-id="8f8aa-162">在設定完成儲存之前，請勿關閉瀏覽器視窗。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-162">Do not close the browser window until the settings have finished saving.</span></span>
<span data-ttu-id="8f8aa-163">此外，請將這些回送 URL 新增至 App Service 的 CORS 設定：</span><span class="sxs-lookup"><span data-stu-id="8f8aa-163">Also add these loopback URLs to the CORS settings for your App Service:</span></span>

1. <span data-ttu-id="8f8aa-164">登入 [Azure 入口網站]</span><span class="sxs-lookup"><span data-stu-id="8f8aa-164">Log in to the [Azure portal]</span></span>
2. <span data-ttu-id="8f8aa-165">選取 [所有資源] 或 [應用程式服務]，然後按一下行動應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-165">Select **All resources** or **App Services** then click the name of your Mobile App.</span></span>
3. <span data-ttu-id="8f8aa-166">[設定] 刀鋒視窗隨即自動開啟。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-166">The Settings blade opens automatically.</span></span>  <span data-ttu-id="8f8aa-167">如果沒有，請按一下 [所有設定] 。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-167">If it doesn't, click **All Settings**.</span></span>
4. <span data-ttu-id="8f8aa-168">按一下 API 功能表下方的 [CORS]  。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-168">Click **CORS** under the API menu.</span></span>
5. <span data-ttu-id="8f8aa-169">輸入在提供的方塊中輸入您希望加入的 URL，然後按 Enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-169">Enter the URL that you wish to add in the box provided and press Enter.</span></span>
6. <span data-ttu-id="8f8aa-170">視需要輸入其他的 URL。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-170">Enter additional URLs as needed.</span></span>
7. <span data-ttu-id="8f8aa-171">按一下 [儲存]  來儲存這些設定。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-171">Click **Save** to save the settings.</span></span>

<span data-ttu-id="8f8aa-172">大約需要 10-15 秒的時間，才能使新的設定生效。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-172">It takes approximately 10-15 seconds for the new settings to take effect.</span></span>

## <span data-ttu-id="8f8aa-173"><a name="register-for-push"></a>作法：註冊推播通知</span><span class="sxs-lookup"><span data-stu-id="8f8aa-173"><a name="register-for-push"></a>How to: Register for push notifications</span></span>
<span data-ttu-id="8f8aa-174">安裝 [phonegap-plugin-push] 來處理推播通知。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-174">Install the [phonegap-plugin-push] to handle push notifications.</span></span>  <span data-ttu-id="8f8aa-175">在命令列中使用 `cordova plugin add` 命令，或在 Visual Studio 內透過 Git 外掛程式安裝程式，即可輕鬆新增此外掛程式。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-175">This plugin can be easily added using the `cordova plugin add` command on the command line, or via the Git plugin installer within Visual Studio.</span></span>  <span data-ttu-id="8f8aa-176">以下在 Apache Cordova 應用程式中的程式碼會為您的裝置註冊推播通知：</span><span class="sxs-lookup"><span data-stu-id="8f8aa-176">The following code in your Apache Cordova app registers your device for push notifications:</span></span>

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
    // For cross-platform, you can use the device plugin to determine the device
    // Best is to use device.platform
    var name = 'gcm'; // For android - default
    if (device.platform.toLowerCase() === 'ios')
        name = 'apns';
    if (device.platform.toLowerCase().substring(0, 3) === 'win')
        name = 'wns';
    client.push.register(name, registrationId);
});

pushHandler.on('notification', function (data) {
    // data is an object and is whatever is sent by the PNS - check the format
    // for your particular PNS
});

pushHandler.on('error', function (error) {
    // Handle errors
});
```

<span data-ttu-id="8f8aa-177">使用通知中樞 SDK 從伺服器傳送推播通知。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-177">Use the Notification Hubs SDK to send push notifications from the server.</span></span>  <span data-ttu-id="8f8aa-178">永遠不要直接從用戶端傳送推播通知。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-178">Never send push notifications directly from clients.</span></span> <span data-ttu-id="8f8aa-179">這種方式會被用來對通知中樞或 PNS 觸發阻斷服務攻擊。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-179">Doing so could be used to trigger a denial of service attack against Notification Hubs or the PNS.</span></span>  <span data-ttu-id="8f8aa-180">PNS 可能會因為這類攻擊而禁止您的流量。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-180">The PNS could ban your traffic as a result of such attacks.</span></span>

## <a name="more-information"></a><span data-ttu-id="8f8aa-181">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="8f8aa-181">More information</span></span>

<span data-ttu-id="8f8aa-182">您可以在 [API 文件](http://azure.github.io/azure-mobile-apps-js-client/)中找到 API 詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="8f8aa-182">You can find detailed API details in our [API documentation](http://azure.github.io/azure-mobile-apps-js-client/).</span></span>

<!-- URLs. -->
<span data-ttu-id="8f8aa-183">[Azure 入口網站]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="8f8aa-183">[Azure portal]: https://portal.azure.com</span></span>
<span data-ttu-id="8f8aa-184">[Azure Mobile Apps 快速啟動]: app-service-mobile-cordova-get-started.md</span><span class="sxs-lookup"><span data-stu-id="8f8aa-184">[Azure Mobile Apps Quick Start]: app-service-mobile-cordova-get-started.md</span></span>
<span data-ttu-id="8f8aa-185">[開始使用驗證]: app-service-mobile-cordova-get-started-users.md</span><span class="sxs-lookup"><span data-stu-id="8f8aa-185">[Get started with authentication]: app-service-mobile-cordova-get-started-users.md</span></span>
[Add authentication to your app]: app-service-mobile-cordova-get-started-users.md

<span data-ttu-id="8f8aa-186">[適用於 Azure Mobile Apps 的 Apache Cordova 外掛程式]: https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-apps</span><span class="sxs-lookup"><span data-stu-id="8f8aa-186">[Apache Cordova Plugin for Azure Mobile Apps]: https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-apps</span></span>
<span data-ttu-id="8f8aa-187">[第一個 Apache Cordova 應用程式]: http://cordova.apache.org/#getstarted</span><span class="sxs-lookup"><span data-stu-id="8f8aa-187">[your first Apache Cordova app]: http://cordova.apache.org/#getstarted</span></span>
[phonegap-facebook-plugin]: https://github.com/wizcorp/phonegap-facebook-plugin
<span data-ttu-id="8f8aa-188">[phonegap-plugin-push]: https://www.npmjs.com/package/phonegap-plugin-push</span><span class="sxs-lookup"><span data-stu-id="8f8aa-188">[phonegap-plugin-push]: https://www.npmjs.com/package/phonegap-plugin-push</span></span>
<span data-ttu-id="8f8aa-189">[cordova-plugin-device]: https://www.npmjs.com/package/cordova-plugin-device</span><span class="sxs-lookup"><span data-stu-id="8f8aa-189">[cordova-plugin-device]: https://www.npmjs.com/package/cordova-plugin-device</span></span>
<span data-ttu-id="8f8aa-190">[cordova-plugin-inappbrowser]: https://www.npmjs.com/package/cordova-plugin-inappbrowser</span><span class="sxs-lookup"><span data-stu-id="8f8aa-190">[cordova-plugin-inappbrowser]: https://www.npmjs.com/package/cordova-plugin-inappbrowser</span></span>
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
