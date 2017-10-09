---
title: "aaaAzure Mobile Engagement Web SDK 升級程序 |Microsoft 文件"
description: "Azure Mobile Engagement hello 最新更新和 hello Web SDK 的程序"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a20529b4-ec8d-4503-8ae9-09b5f0846d5b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 06/07/2016
ms.author: piyushjo
ms.openlocfilehash: a2df65904c6b56584ce6588ed26a9b79f3aa27ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-web-sdk-upgrade-procedures"></a><span data-ttu-id="25a73-103">Azure Mobile Engagement Web SDK 升級程序</span><span class="sxs-lookup"><span data-stu-id="25a73-103">Azure Mobile Engagement Web SDK upgrade procedures</span></span>
<span data-ttu-id="25a73-104">如果您已經整合到您的 web 應用程式較早版本的 hello Azure Mobile Engagement Web SDK，您需要下列點，當您升級 hello SDK tooconsider hello。</span><span class="sxs-lookup"><span data-stu-id="25a73-104">If you have already integrated an earlier version of hello Azure Mobile Engagement Web SDK into your web application, you need tooconsider hello following points when you upgrade hello SDK.</span></span>

<span data-ttu-id="25a73-105">如果您略過多個版本的 hello Mobile Engagement Web SDK，您可能需要 toocomplete 數個程序期間 hello 升級程序。</span><span class="sxs-lookup"><span data-stu-id="25a73-105">If you skipped multiple versions of hello Mobile Engagement Web SDK, you might need toocomplete several procedures during hello upgrade process.</span></span> <span data-ttu-id="25a73-106">例如，如果您從 1.4.0 移轉 too1.6.0，第一個後續 hello 程序從 1.4.0 tooupgrade too1.5.0。</span><span class="sxs-lookup"><span data-stu-id="25a73-106">For example, if you migrate from 1.4.0 too1.6.0, first follow hello procedures tooupgrade from 1.4.0 too1.5.0.</span></span> <span data-ttu-id="25a73-107">然後，遵循 1.5.0 hello 程序 tooupgrade too1.6.0。</span><span class="sxs-lookup"><span data-stu-id="25a73-107">Then, follow hello procedures tooupgrade from 1.5.0 too1.6.0.</span></span>

<span data-ttu-id="25a73-108">任何版本升級，從任何舊版的 hello 檔案 azure engagement.js 取代 hello hello 檔案最新版本。</span><span class="sxs-lookup"><span data-stu-id="25a73-108">Whichever version you upgrade from, replace any earlier version of hello file azure-engagement.js with hello latest version of hello file.</span></span>

## <a name="upgrade-from-121-too200"></a><span data-ttu-id="25a73-109">1.2.1 從升級 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="25a73-109">Upgrade from 1.2.1 too2.0.0</span></span>
<span data-ttu-id="25a73-110">本章節描述如何 toomigrate hello Capptain 服務整合在 Mobile Engagement Web SDK 所提供 Capptain SAS，tooan Azure Mobile Engagement 應用程式。</span><span class="sxs-lookup"><span data-stu-id="25a73-110">This section describes how toomigrate a Mobile Engagement Web SDK integration from hello Capptain service, offered by Capptain SAS, tooan Azure Mobile Engagement app.</span></span> <span data-ttu-id="25a73-111">如果您要移轉從較早的版本，請參閱 hello Capptain 網站 toofirst 移轉 too1.2.1，然後再套用 hello 下列程序。</span><span class="sxs-lookup"><span data-stu-id="25a73-111">If you are migrating from an earlier version, please consult hello Capptain website toofirst migrate too1.2.1, and then apply hello following procedures.</span></span>

<span data-ttu-id="25a73-112">此版的 hello Mobile Engagement Web SDK 不支援 Samsung 智慧電視、 Opera 電視、 webOS 或 hello 觸達功能。</span><span class="sxs-lookup"><span data-stu-id="25a73-112">This version of hello Mobile Engagement Web SDK doesn't support Samsung Smart TV, Opera TV, webOS, or hello Reach feature.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="25a73-113">Capptain 和 Azure Mobile Engagement 不是 hello 相同的服務。</span><span class="sxs-lookup"><span data-stu-id="25a73-113">Capptain and Azure Mobile Engagement are not hello same service.</span></span> <span data-ttu-id="25a73-114">下列程序的 hello 反白顯示如何只 toomigrate hello 用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="25a73-114">hello following procedure highlights only how toomigrate hello client app.</span></span> <span data-ttu-id="25a73-115">移轉 hello Mobile Engagement Web SDK hello 應用程式中的不會移轉您的資料從 Capptain 伺服器 tooa Mobile Engagement 伺服器。</span><span class="sxs-lookup"><span data-stu-id="25a73-115">Migrating hello Mobile Engagement Web SDK in hello app will not migrate your data from a Capptain server tooa Mobile Engagement server.</span></span>
> 
> 

### <a name="javascript-files"></a><span data-ttu-id="25a73-116">JavaScript 檔案</span><span class="sxs-lookup"><span data-stu-id="25a73-116">JavaScript files</span></span>
<span data-ttu-id="25a73-117">取代 hello 檔案 capptain-sdk.js 以 hello 檔案 azure engagement.js，，，然後據此更新指令碼匯入。</span><span class="sxs-lookup"><span data-stu-id="25a73-117">Replace hello file capptain-sdk.js with hello file azure-engagement.js, and then update your script imports accordingly.</span></span>

### <a name="remove-capptain-reach"></a><span data-ttu-id="25a73-118">移除 Capptain Reach</span><span class="sxs-lookup"><span data-stu-id="25a73-118">Remove Capptain Reach</span></span>
<span data-ttu-id="25a73-119">此版的 hello Mobile Engagement Web SDK 不支援 hello 觸達功能。</span><span class="sxs-lookup"><span data-stu-id="25a73-119">This version of hello Mobile Engagement Web SDK doesn't support hello Reach feature.</span></span> <span data-ttu-id="25a73-120">如果您 Capptain 觸達整合至您的應用程式時，您需要 tooremove 它。</span><span class="sxs-lookup"><span data-stu-id="25a73-120">If you integrated Capptain Reach into your application, you need tooremove it.</span></span>

<span data-ttu-id="25a73-121">從您網頁移除 hello 到達 CSS 匯入，並刪除 hello 相關的.css 檔案 (capptain-reach.css，依預設)。</span><span class="sxs-lookup"><span data-stu-id="25a73-121">Remove hello Reach CSS import from your page and delete hello related .css file (capptain-reach.css, by default).</span></span>

<span data-ttu-id="25a73-122">刪除下列觸達資源 hello: hello 關閉映像 (capptain-close.png，依預設) 和 hello 商標圖示 （capptain-通知-圖示，依預設）。</span><span class="sxs-lookup"><span data-stu-id="25a73-122">Delete hello following Reach resources: hello close image (capptain-close.png, by default) and hello brand icon (capptain-notification-icon, by default).</span></span>

<span data-ttu-id="25a73-123">移除應用程式內通知的 hello 到達 UI。</span><span class="sxs-lookup"><span data-stu-id="25a73-123">Remove hello Reach UI for in-app notifications.</span></span> <span data-ttu-id="25a73-124">hello 預設版面配置看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="25a73-124">hello default layout looks like this:</span></span>

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

<span data-ttu-id="25a73-125">移除文字和網頁的宣告與輪詢 hello 到達 UI。</span><span class="sxs-lookup"><span data-stu-id="25a73-125">Remove hello Reach UI for text and web announcements and polls.</span></span> <span data-ttu-id="25a73-126">hello 預設版面配置看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="25a73-126">hello default layout looks like this:</span></span>

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

<span data-ttu-id="25a73-127">移除 hello`reach`如果存在的話，從您的組態物件。</span><span class="sxs-lookup"><span data-stu-id="25a73-127">Remove hello `reach` object from your configuration, if it exists.</span></span> <span data-ttu-id="25a73-128">它看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="25a73-128">It looks like this:</span></span>

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

<span data-ttu-id="25a73-129">移除所有其他的 Reach 自訂，例如類別。</span><span class="sxs-lookup"><span data-stu-id="25a73-129">Remove any other Reach customization, such as categories.</span></span>

### <a name="remove-deprecated-apis"></a><span data-ttu-id="25a73-130">移除已被取代的 API</span><span class="sxs-lookup"><span data-stu-id="25a73-130">Remove deprecated APIs</span></span>
<span data-ttu-id="25a73-131">在 hello Mobile Engagement Web SDK 已被取代 Capptain 從某些應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="25a73-131">Some APIs from Capptain are deprecated in hello Mobile Engagement Web SDK.</span></span>

<span data-ttu-id="25a73-132">移除下列應用程式開發介面的任何呼叫 toohello: `agent.connect`， `agent.disconnect`， `agent.pause`，和`agent.sendMessageToDevice`。</span><span class="sxs-lookup"><span data-stu-id="25a73-132">Remove any calls toohello following APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, and `agent.sendMessageToDevice`.</span></span>

<span data-ttu-id="25a73-133">移除任何執行個體的 hello Capptain 組態中的下列回呼： `onConnected`， `onDisconnected`， `onDeviceMessageReceived`，和`onPushMessageReceived`。</span><span class="sxs-lookup"><span data-stu-id="25a73-133">Remove any instances of hello following callbacks from your Capptain configuration: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, and `onPushMessageReceived`.</span></span>

### <a name="configuration"></a><span data-ttu-id="25a73-134">組態</span><span class="sxs-lookup"><span data-stu-id="25a73-134">Configuration</span></span>
<span data-ttu-id="25a73-135">Mobile Engagement 會使用連接字串 tooconfigure SDK 識別項，例如 hello 應用程式識別項。</span><span class="sxs-lookup"><span data-stu-id="25a73-135">Mobile Engagement uses a connection string tooconfigure SDK identifiers, for example, hello application identifier.</span></span>

<span data-ttu-id="25a73-136">取代您的連接字串中的 hello 應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="25a73-136">Replace hello application ID with your connection string.</span></span> <span data-ttu-id="25a73-137">請注意該 hello 全域物件，如 hello SDK 組態變更從`capptain`太`azureEngagement`。</span><span class="sxs-lookup"><span data-stu-id="25a73-137">Note that hello global object for hello SDK configuration changes from `capptain` too`azureEngagement`.</span></span>

<span data-ttu-id="25a73-138">移轉前：</span><span class="sxs-lookup"><span data-stu-id="25a73-138">Before migration:</span></span>

    window.capptain = {
      appId: ...,
      [...]
    };

<span data-ttu-id="25a73-139">移轉後：</span><span class="sxs-lookup"><span data-stu-id="25a73-139">After migration:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

<span data-ttu-id="25a73-140">您的應用程式的 hello 連接字串會顯示在 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="25a73-140">hello connection string for your application is displayed in hello Azure Portal.</span></span>

### <a name="javascript-apis"></a><span data-ttu-id="25a73-141">JavaScript API</span><span class="sxs-lookup"><span data-stu-id="25a73-141">JavaScript APIs</span></span>
<span data-ttu-id="25a73-142">hello 全域 JavaScript 物件`window.capptain`已重新命名`window.azureEngagement`但您可以使用 hello `window.engagement` API 呼叫的別名。</span><span class="sxs-lookup"><span data-stu-id="25a73-142">hello global JavaScript object `window.capptain` has been renamed `window.azureEngagement` but you can use hello `window.engagement` alias for API calls.</span></span> <span data-ttu-id="25a73-143">您無法使用 hello 別名 toodefine hello SDK 設定。</span><span class="sxs-lookup"><span data-stu-id="25a73-143">You can't use hello alias toodefine hello SDK configuration.</span></span>

<span data-ttu-id="25a73-144">例如，`capptain.deviceId` 會變成 `engagement.deviceId`，`capptain.agent.startActivity` 會變成 `engagement.agent.startActivity`，依此類推。</span><span class="sxs-lookup"><span data-stu-id="25a73-144">For instance, `capptain.deviceId` becomes `engagement.deviceId`, `capptain.agent.startActivity` becomes `engagement.agent.startActivity`, and so on.</span></span>

