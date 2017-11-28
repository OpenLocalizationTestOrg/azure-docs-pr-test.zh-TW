---
title: "Azure Mobile Engagement Web SDK 升級程序 | Microsoft Docs"
description: "Azure Mobile Engagement Web SDK 的最新更新與程序"
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
ms.openlocfilehash: afa8037dcb7a53042fa606e2c4014b442d4be326
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-mobile-engagement-web-sdk-upgrade-procedures"></a><span data-ttu-id="fc630-103">Azure Mobile Engagement Web SDK 升級程序</span><span class="sxs-lookup"><span data-stu-id="fc630-103">Azure Mobile Engagement Web SDK upgrade procedures</span></span>
<span data-ttu-id="fc630-104">如果您已經將舊版 Azure Mobile Engagement Web SDK 整合到您的 Web 應用程式，則當您升級 SDK 時需要考慮下列幾點。</span><span class="sxs-lookup"><span data-stu-id="fc630-104">If you have already integrated an earlier version of the Azure Mobile Engagement Web SDK into your web application, you need to consider the following points when you upgrade the SDK.</span></span>

<span data-ttu-id="fc630-105">如果您略過多個版本的 Mobile Engagement Web SDK，您可能需要在升級程序期間完成數個程序。</span><span class="sxs-lookup"><span data-stu-id="fc630-105">If you skipped multiple versions of the Mobile Engagement Web SDK, you might need to complete several procedures during the upgrade process.</span></span> <span data-ttu-id="fc630-106">例如，如果您從 1.4.0 移轉到 1.6.0，請先遵循從從 1.4.0 升級到 1.5.0 的程序。</span><span class="sxs-lookup"><span data-stu-id="fc630-106">For example, if you migrate from 1.4.0 to 1.6.0, first follow the procedures to upgrade from 1.4.0 to 1.5.0.</span></span> <span data-ttu-id="fc630-107">然後，遵循從 1.5.0 升級到 1.6.0 的程序。</span><span class="sxs-lookup"><span data-stu-id="fc630-107">Then, follow the procedures to upgrade from 1.5.0 to 1.6.0.</span></span>

<span data-ttu-id="fc630-108">不論您要從哪一個版本升級，都要使用最新版的 azure-engagement.js 檔案來取代舊版檔案。</span><span class="sxs-lookup"><span data-stu-id="fc630-108">Whichever version you upgrade from, replace any earlier version of the file azure-engagement.js with the latest version of the file.</span></span>

## <a name="upgrade-from-121-to-200"></a><span data-ttu-id="fc630-109">從 1.2.1 升級到 2.0.0</span><span class="sxs-lookup"><span data-stu-id="fc630-109">Upgrade from 1.2.1 to 2.0.0</span></span>
<span data-ttu-id="fc630-110">本節說明如何將 Mobile Engagement Web SDK 整合從 Capptain SAS 提供的 Capptain 服務移轉到 Azure Mobile Engagement 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fc630-110">This section describes how to migrate a Mobile Engagement Web SDK integration from the Capptain service, offered by Capptain SAS, to an Azure Mobile Engagement app.</span></span> <span data-ttu-id="fc630-111">如果您是從較早版本移轉，請參閱 Capptain 網站，先移轉到 1.2.1 後再套用以下程序。</span><span class="sxs-lookup"><span data-stu-id="fc630-111">If you are migrating from an earlier version, please consult the Capptain website to first migrate to 1.2.1, and then apply the following procedures.</span></span>

<span data-ttu-id="fc630-112">此版本的 Mobile Engagement Web SDK 不支援 Samsung Smart TV、Opera TV、webOS 或 Reach 功能。</span><span class="sxs-lookup"><span data-stu-id="fc630-112">This version of the Mobile Engagement Web SDK doesn't support Samsung Smart TV, Opera TV, webOS, or the Reach feature.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fc630-113">Capptain 和 Azure Mobile Engagement 不是同一個服務。</span><span class="sxs-lookup"><span data-stu-id="fc630-113">Capptain and Azure Mobile Engagement are not the same service.</span></span> <span data-ttu-id="fc630-114">下列程序只會強調說明如何移轉用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="fc630-114">The following procedure highlights only how to migrate the client app.</span></span> <span data-ttu-id="fc630-115">移轉應用程式中的 Mobile Engagement Web SDK，不會將您的資料從 Capptain 伺服器移轉到 Mobile Engagement 伺服器。</span><span class="sxs-lookup"><span data-stu-id="fc630-115">Migrating the Mobile Engagement Web SDK in the app will not migrate your data from a Capptain server to a Mobile Engagement server.</span></span>
> 
> 

### <a name="javascript-files"></a><span data-ttu-id="fc630-116">JavaScript 檔案</span><span class="sxs-lookup"><span data-stu-id="fc630-116">JavaScript files</span></span>
<span data-ttu-id="fc630-117">使用 azure-engagement.js 檔案來取代 capptain-sdk.js 檔案，然後據以更新您的指令碼匯入。</span><span class="sxs-lookup"><span data-stu-id="fc630-117">Replace the file capptain-sdk.js with the file azure-engagement.js, and then update your script imports accordingly.</span></span>

### <a name="remove-capptain-reach"></a><span data-ttu-id="fc630-118">移除 Capptain Reach</span><span class="sxs-lookup"><span data-stu-id="fc630-118">Remove Capptain Reach</span></span>
<span data-ttu-id="fc630-119">此版本的 Mobile Engagement Web SDK 不支援 Reach 功能。</span><span class="sxs-lookup"><span data-stu-id="fc630-119">This version of the Mobile Engagement Web SDK doesn't support the Reach feature.</span></span> <span data-ttu-id="fc630-120">如果您將 Capptain Reach 整合到您的應用程式，就需要加以移除。</span><span class="sxs-lookup"><span data-stu-id="fc630-120">If you integrated Capptain Reach into your application, you need to remove it.</span></span>

<span data-ttu-id="fc630-121">從您的頁面移除 Reach CSS 匯入，並移除相關的 .css 檔案 (預設為 capptain-reach.css)。</span><span class="sxs-lookup"><span data-stu-id="fc630-121">Remove the Reach CSS import from your page and delete the related .css file (capptain-reach.css, by default).</span></span>

<span data-ttu-id="fc630-122">刪除下列 Reach 資源：關閉影像 (預設為 capptain-close.png) 和品牌圖示 (預設為 capptain-notification-icon)。</span><span class="sxs-lookup"><span data-stu-id="fc630-122">Delete the following Reach resources: the close image (capptain-close.png, by default) and the brand icon (capptain-notification-icon, by default).</span></span>

<span data-ttu-id="fc630-123">移除用於應用程式內通知的 Reach UI。</span><span class="sxs-lookup"><span data-stu-id="fc630-123">Remove the Reach UI for in-app notifications.</span></span> <span data-ttu-id="fc630-124">預設配置看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="fc630-124">The default layout looks like this:</span></span>

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

<span data-ttu-id="fc630-125">移除用於文字和 Web 宣告和輪詢的 Reach UI。</span><span class="sxs-lookup"><span data-stu-id="fc630-125">Remove the Reach UI for text and web announcements and polls.</span></span> <span data-ttu-id="fc630-126">預設配置看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="fc630-126">The default layout looks like this:</span></span>

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

<span data-ttu-id="fc630-127">從您的組態中移除 `reach` 物件 (如果存在)。</span><span class="sxs-lookup"><span data-stu-id="fc630-127">Remove the `reach` object from your configuration, if it exists.</span></span> <span data-ttu-id="fc630-128">它看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="fc630-128">It looks like this:</span></span>

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

<span data-ttu-id="fc630-129">移除所有其他的 Reach 自訂，例如類別。</span><span class="sxs-lookup"><span data-stu-id="fc630-129">Remove any other Reach customization, such as categories.</span></span>

### <a name="remove-deprecated-apis"></a><span data-ttu-id="fc630-130">移除已被取代的 API</span><span class="sxs-lookup"><span data-stu-id="fc630-130">Remove deprecated APIs</span></span>
<span data-ttu-id="fc630-131">在 Mobile Engagement Web SDK 中，某些來自 Capptain 的 API 已被取代。</span><span class="sxs-lookup"><span data-stu-id="fc630-131">Some APIs from Capptain are deprecated in the Mobile Engagement Web SDK.</span></span>

<span data-ttu-id="fc630-132">移除針對下列 API 的所有呼叫：`agent.connect`、`agent.disconnect`、`agent.pause` 及 `agent.sendMessageToDevice`。</span><span class="sxs-lookup"><span data-stu-id="fc630-132">Remove any calls to the following APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, and `agent.sendMessageToDevice`.</span></span>

<span data-ttu-id="fc630-133">從您的 Capptain 組態移除下列回呼的所有執行個體：`onConnected`、`onDisconnected`、`onDeviceMessageReceived` 及 `onPushMessageReceived`。</span><span class="sxs-lookup"><span data-stu-id="fc630-133">Remove any instances of the following callbacks from your Capptain configuration: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, and `onPushMessageReceived`.</span></span>

### <a name="configuration"></a><span data-ttu-id="fc630-134">組態</span><span class="sxs-lookup"><span data-stu-id="fc630-134">Configuration</span></span>
<span data-ttu-id="fc630-135">Mobile Engagement 使用連接字串來設定 SDK 識別碼，例如應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="fc630-135">Mobile Engagement uses a connection string to configure SDK identifiers, for example, the application identifier.</span></span>

<span data-ttu-id="fc630-136">使用您的連接字串來取代應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="fc630-136">Replace the application ID with your connection string.</span></span> <span data-ttu-id="fc630-137">請注意，適用於 SDK 組態的全域物件會從 `capptain` 變更為 `azureEngagement`。</span><span class="sxs-lookup"><span data-stu-id="fc630-137">Note that the global object for the SDK configuration changes from `capptain` to `azureEngagement`.</span></span>

<span data-ttu-id="fc630-138">移轉前：</span><span class="sxs-lookup"><span data-stu-id="fc630-138">Before migration:</span></span>

    window.capptain = {
      appId: ...,
      [...]
    };

<span data-ttu-id="fc630-139">移轉後：</span><span class="sxs-lookup"><span data-stu-id="fc630-139">After migration:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

<span data-ttu-id="fc630-140">您應用程式的連接字串會顯示於 Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="fc630-140">The connection string for your application is displayed in the Azure Portal.</span></span>

### <a name="javascript-apis"></a><span data-ttu-id="fc630-141">JavaScript API</span><span class="sxs-lookup"><span data-stu-id="fc630-141">JavaScript APIs</span></span>
<span data-ttu-id="fc630-142">全域 JavaScript 物件 `window.capptain` 已重新命名為 `window.azureEngagement`，但您可以針對 API 呼叫使用 `window.engagement` 別名。</span><span class="sxs-lookup"><span data-stu-id="fc630-142">The global JavaScript object `window.capptain` has been renamed `window.azureEngagement` but you can use the `window.engagement` alias for API calls.</span></span> <span data-ttu-id="fc630-143">您無法使用此別名來定義 SDK 組態。</span><span class="sxs-lookup"><span data-stu-id="fc630-143">You can't use the alias to define the SDK configuration.</span></span>

<span data-ttu-id="fc630-144">例如，`capptain.deviceId` 會變成 `engagement.deviceId`，`capptain.agent.startActivity` 會變成 `engagement.agent.startActivity`，依此類推。</span><span class="sxs-lookup"><span data-stu-id="fc630-144">For instance, `capptain.deviceId` becomes `engagement.deviceId`, `capptain.agent.startActivity` becomes `engagement.agent.startActivity`, and so on.</span></span>

