---
title: "aaaAzure Mobile Engagement Web SDK 概觀 |Microsoft 文件"
description: "Azure Mobile Engagement hello 最新更新和 hello Web SDK 的程序"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 5bbc2fda-0f3f-43d0-a73d-0f2c0f8dc25b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 10/18/2016
ms.author: piyushjo
ms.openlocfilehash: 9e60a232b5eb2c41c405041a88e09d7137563513
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-web-sdk"></a><span data-ttu-id="70ac3-103">Azure Mobile Engagement Web SDK</span><span class="sxs-lookup"><span data-stu-id="70ac3-103">Azure Mobile Engagement Web SDK</span></span>
<span data-ttu-id="70ac3-104">從這裡開始針對所有 hello 詳細說明如何在 web 應用程式的 Azure Mobile Engagement toointegrate。</span><span class="sxs-lookup"><span data-stu-id="70ac3-104">Start here for all hello details about how toointegrate Azure Mobile Engagement in a web app.</span></span> <span data-ttu-id="70ac3-105">如果您想要 toogive 它才能開始使用您自己的 web 應用程式，再試一次看到我們[15 分鐘的教學課程](mobile-engagement-web-app-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="70ac3-105">If you'd like toogive it a try before getting started with your own web app, see our [15-minute tutorial](mobile-engagement-web-app-get-started.md).</span></span>

## <a name="integration-procedures"></a><span data-ttu-id="70ac3-106">整合程序</span><span class="sxs-lookup"><span data-stu-id="70ac3-106">Integration procedures</span></span>
1. <span data-ttu-id="70ac3-107">深入了解[如何在 web 應用程式中的 toointegrate Mobile Engagement](mobile-engagement-web-integrate-engagement.md)。</span><span class="sxs-lookup"><span data-stu-id="70ac3-107">Learn [how toointegrate Mobile Engagement in your web app](mobile-engagement-web-integrate-engagement.md).</span></span>
2. <span data-ttu-id="70ac3-108">如需標記的計劃實作，了解[toouse hello 如何進階標記您的 web 應用程式中的應用程式開發介面的 Mobile Engagement](mobile-engagement-web-use-engagement-api.md)。</span><span class="sxs-lookup"><span data-stu-id="70ac3-108">For tag plan implementation, learn [how toouse hello advanced Mobile Engagement tagging API in your web app](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="release-notes"></a><span data-ttu-id="70ac3-109">版本資訊</span><span class="sxs-lookup"><span data-stu-id="70ac3-109">Release notes</span></span>
### <a name="202-10182016"></a><span data-ttu-id="70ac3-110">2.0.2 (10/18/2016)</span><span class="sxs-lookup"><span data-stu-id="70ac3-110">2.0.2 (10/18/2016)</span></span>
* <span data-ttu-id="70ac3-111">已修正使用私密瀏覽時的當機問題 (Safari)。</span><span class="sxs-lookup"><span data-stu-id="70ac3-111">Fixed crash on private browsing (Safari).</span></span>
* <span data-ttu-id="70ac3-112">已修正停用 Cookie 之瀏覽器的當機問題。</span><span class="sxs-lookup"><span data-stu-id="70ac3-112">Fixed crash on browsers with cookies disabled.</span></span>

<span data-ttu-id="70ac3-113">對於所有版本，請參閱 hello[完成版本資訊](mobile-engagement-web-release-notes.md)。</span><span class="sxs-lookup"><span data-stu-id="70ac3-113">For all versions, please see hello [complete release notes](mobile-engagement-web-release-notes.md).</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="70ac3-114">升級程序</span><span class="sxs-lookup"><span data-stu-id="70ac3-114">Upgrade procedures</span></span>
### <a name="upgrade-from-121-too200"></a><span data-ttu-id="70ac3-115">1.2.1 從升級 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="70ac3-115">Upgrade from 1.2.1 too2.0.0</span></span>
<span data-ttu-id="70ac3-116">hello 下列章節說明如何 toomigrate hello Capptain 服務整合在 Mobile Engagement Web SDK 所提供 Capptain SAS，tooan Azure Mobile Engagement 應用程式。</span><span class="sxs-lookup"><span data-stu-id="70ac3-116">hello following sections describe how toomigrate a Mobile Engagement Web SDK integration from hello Capptain service, offered by Capptain SAS, tooan Azure Mobile Engagement app.</span></span> <span data-ttu-id="70ac3-117">如果您要從移轉稍早的版本比 1.2.1，，請參閱 hello Capptain 網站 toomigrate too1.2.1 第一次，然後再套用 hello 下列程序。</span><span class="sxs-lookup"><span data-stu-id="70ac3-117">If you are migrating from a version earlier than 1.2.1, please consult hello Capptain website toomigrate too1.2.1 first, and then apply hello following procedures.</span></span>

<span data-ttu-id="70ac3-118">此版的 hello Mobile Engagement Web SDK 不支援 Samsung 智慧電視、 Opera 電視、 webOS 或 hello 觸達功能。</span><span class="sxs-lookup"><span data-stu-id="70ac3-118">This version of hello Mobile Engagement Web SDK doesn't support Samsung Smart TV, Opera TV, webOS, or hello Reach feature.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="70ac3-119">Capptain 和 Azure Mobile Engagement 不是 hello 相同的服務，和下列程序的 hello 反白顯示如何只 toomigrate hello 用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="70ac3-119">Capptain and Azure Mobile Engagement are not hello same service, and hello following procedures highlight only how toomigrate hello client app.</span></span> <span data-ttu-id="70ac3-120">移轉 hello Mobile Engagement Web SDK hello 應用程式中的不會移轉您的資料從 Capptain 伺服器 tooa Mobile Engagement 伺服器。</span><span class="sxs-lookup"><span data-stu-id="70ac3-120">Migrating hello Mobile Engagement Web SDK in hello app will not migrate your data from a Capptain server tooa Mobile Engagement server.</span></span>
> 
> 

#### <a name="javascript-files"></a><span data-ttu-id="70ac3-121">JavaScript 檔案</span><span class="sxs-lookup"><span data-stu-id="70ac3-121">JavaScript files</span></span>
<span data-ttu-id="70ac3-122">取代 hello 檔案 capptain-sdk.js 以 hello 檔案 azure engagement.js，，，然後據此更新指令碼匯入。</span><span class="sxs-lookup"><span data-stu-id="70ac3-122">Replace hello file capptain-sdk.js with hello file azure-engagement.js, and then update your script imports accordingly.</span></span>

#### <a name="remove-capptain-reach"></a><span data-ttu-id="70ac3-123">移除 Capptain Reach</span><span class="sxs-lookup"><span data-stu-id="70ac3-123">Remove Capptain Reach</span></span>
<span data-ttu-id="70ac3-124">此版的 hello Mobile Engagement Web SDK 不支援 hello 觸達功能。</span><span class="sxs-lookup"><span data-stu-id="70ac3-124">This version of hello Mobile Engagement Web SDK doesn't support hello Reach feature.</span></span> <span data-ttu-id="70ac3-125">如果您有整合 Capptain 觸達至您的應用程式，您需要 tooremove 它。</span><span class="sxs-lookup"><span data-stu-id="70ac3-125">If you have integrated Capptain Reach into your application, you need tooremove it.</span></span>

<span data-ttu-id="70ac3-126">從您網頁移除 hello 到達 CSS 匯入，並刪除 hello 相關的.css 檔案 (capptain-reach.css，依預設)。</span><span class="sxs-lookup"><span data-stu-id="70ac3-126">Remove hello Reach CSS import from your page and delete hello related .css file (capptain-reach.css, by default).</span></span>

<span data-ttu-id="70ac3-127">刪除下列觸達資源 hello: hello 關閉映像 (capptain-close.png，依預設) 和 hello 商標圖示 （capptain-通知-圖示，依預設）。</span><span class="sxs-lookup"><span data-stu-id="70ac3-127">Delete hello following Reach resources: hello close image (capptain-close.png, by default) and hello brand icon (capptain-notification-icon, by default).</span></span>

<span data-ttu-id="70ac3-128">移除應用程式內通知的 hello 到達 UI。</span><span class="sxs-lookup"><span data-stu-id="70ac3-128">Remove hello Reach UI for in-app notifications.</span></span> <span data-ttu-id="70ac3-129">hello 預設版面配置看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="70ac3-129">hello default layout looks like this:</span></span>

    <!-- capptain notification -->
    <div id="capptain_notification_area" class="capptain_category_default">
      <div class="icon">
        <img src="capptain-notification-icon.png" alt="icon" />
      </div>
      <div class="content">
        <div class="title" id="capptain_notification_title"></div>
        <div class="message" id="capptain_notification_message"></div>
      </div>
      <div id="capptain_notification_image"></div>
      <div>
        <button id="capptain_notification_close">Close</button>
      </div>
    </div>

<span data-ttu-id="70ac3-130">移除文字和網頁的宣告與輪詢 hello 到達 UI。</span><span class="sxs-lookup"><span data-stu-id="70ac3-130">Remove hello Reach UI for text and web announcements and polls.</span></span> <span data-ttu-id="70ac3-131">hello 預設版面配置看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="70ac3-131">hello default layout looks like this:</span></span>

    <div id="capptain_overlay" class="capptain_category_default">
      <button id="capptain_overlay_close">x</button>
      <div id="capptain_overlay_title"></div>
      <div id="capptain_overlay_body"></div>
      <div id="capptain_overlay_poll"></div>
      <div id="capptain_overlay_buttons">
        <button id="capptain_overlay_exit"></button>
        <button id="capptain_overlay_action"></button>
      </div>
    </div>

<span data-ttu-id="70ac3-132">移除 hello`reach`如果存在的話，從您的組態物件。</span><span class="sxs-lookup"><span data-stu-id="70ac3-132">Remove hello `reach` object from your configuration, if it exists.</span></span> <span data-ttu-id="70ac3-133">它看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="70ac3-133">It looks like this:</span></span>

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

<span data-ttu-id="70ac3-134">移除所有其他的 Reach 自訂，例如類別。</span><span class="sxs-lookup"><span data-stu-id="70ac3-134">Remove any other Reach customization, such as categories.</span></span>

#### <a name="remove-deprecated-apis"></a><span data-ttu-id="70ac3-135">移除已被取代的 API</span><span class="sxs-lookup"><span data-stu-id="70ac3-135">Remove deprecated APIs</span></span>
<span data-ttu-id="70ac3-136">在 hello Mobile Engagement Web SDK 已被取代 Capptain 從某些應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="70ac3-136">Some APIs from Capptain are deprecated in hello Mobile Engagement Web SDK.</span></span>

<span data-ttu-id="70ac3-137">移除下列應用程式開發介面的任何呼叫 toohello: `agent.connect`， `agent.disconnect`， `agent.pause`，和`agent.sendMessageToDevice`。</span><span class="sxs-lookup"><span data-stu-id="70ac3-137">Remove any calls toohello following APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, and `agent.sendMessageToDevice`.</span></span>

<span data-ttu-id="70ac3-138">移除任何 hello Capptain 組態中的下列回呼： `onConnected`， `onDisconnected`， `onDeviceMessageReceived`，和`onPushMessageReceived`。</span><span class="sxs-lookup"><span data-stu-id="70ac3-138">Remove any of hello following callbacks from your Capptain configuration: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, and `onPushMessageReceived`.</span></span>

#### <a name="configuration"></a><span data-ttu-id="70ac3-139">組態</span><span class="sxs-lookup"><span data-stu-id="70ac3-139">Configuration</span></span>
<span data-ttu-id="70ac3-140">Mobile Engagement 會使用連接字串 tooconfigure SDK 識別項，例如 hello 應用程式識別項。</span><span class="sxs-lookup"><span data-stu-id="70ac3-140">Mobile Engagement uses a connection string tooconfigure SDK identifiers, for example, hello application identifier.</span></span>

<span data-ttu-id="70ac3-141">取代您的連接字串中的 hello 應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="70ac3-141">Replace hello application ID with your connection string.</span></span> <span data-ttu-id="70ac3-142">請注意該 hello 全域物件，如 hello SDK 組態變更從`capptain`太`azureEngagement`。</span><span class="sxs-lookup"><span data-stu-id="70ac3-142">Note that hello global object for hello SDK configuration changes from `capptain` too`azureEngagement`.</span></span>

<span data-ttu-id="70ac3-143">移轉前：</span><span class="sxs-lookup"><span data-stu-id="70ac3-143">Before migration:</span></span>

    window.capptain = {
      appId: ...,
      [...]
    };

<span data-ttu-id="70ac3-144">移轉後：</span><span class="sxs-lookup"><span data-stu-id="70ac3-144">After migration:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

<span data-ttu-id="70ac3-145">您的應用程式的 hello 連接字串會顯示在 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="70ac3-145">hello connection string for your application is displayed in hello Azure portal.</span></span>

#### <a name="javascript-apis"></a><span data-ttu-id="70ac3-146">JavaScript API</span><span class="sxs-lookup"><span data-stu-id="70ac3-146">JavaScript APIs</span></span>
<span data-ttu-id="70ac3-147">hello 全域 JavaScript 物件`window.capptain`已重新命名`window.azureEngagement`，但是您可以使用 hello `window.engagement` API 呼叫的別名。</span><span class="sxs-lookup"><span data-stu-id="70ac3-147">hello global JavaScript object `window.capptain` has been renamed `window.azureEngagement`, but you can use hello `window.engagement` alias for API calls.</span></span> <span data-ttu-id="70ac3-148">您無法使用此別名 toodefine hello SDK 組態。</span><span class="sxs-lookup"><span data-stu-id="70ac3-148">You can't use this alias toodefine hello SDK configuration.</span></span>

<span data-ttu-id="70ac3-149">例如，`capptain.deviceId` 會變成 `engagement.deviceId`，`capptain.agent.startActivity` 會變成 `engagement.agent.startActivity`，依此類推。</span><span class="sxs-lookup"><span data-stu-id="70ac3-149">For instance, `capptain.deviceId` becomes `engagement.deviceId`, `capptain.agent.startActivity` becomes `engagement.agent.startActivity`, and so on.</span></span>

<span data-ttu-id="70ac3-150">如果您已經為您的應用程式整合較早版本的 hello Azure Mobile Engagement Web SDK，請閱讀[升級程序](mobile-engagement-web-upgrade-procedure.md)。</span><span class="sxs-lookup"><span data-stu-id="70ac3-150">If you have already integrated an earlier version of hello Azure Mobile Engagement Web SDK into your application, please read about [upgrade procedures](mobile-engagement-web-upgrade-procedure.md).</span></span>

