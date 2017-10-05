---
title: "Azure Mobile Engagement Web SDK 概觀 | Microsoft Docs"
description: "Azure Mobile Engagement Web SDK 的最新更新與程序"
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
ms.openlocfilehash: 770a83131a3e661771db50b22ce7de25b2d541cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-mobile-engagement-web-sdk"></a><span data-ttu-id="a96da-103">Azure Mobile Engagement Web SDK</span><span class="sxs-lookup"><span data-stu-id="a96da-103">Azure Mobile Engagement Web SDK</span></span>
<span data-ttu-id="a96da-104">從這裡開始取得有關如何在 Web 應用程式中整合 Azure Mobile Engagement 的所有詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a96da-104">Start here for all the details about how to integrate Azure Mobile Engagement in a web app.</span></span> <span data-ttu-id="a96da-105">如果您想要在開始使用您自己的 Web 應用程式之前，先嘗試一下，請參閱我們的 [15 分鐘教學課程](mobile-engagement-web-app-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="a96da-105">If you'd like to give it a try before getting started with your own web app, see our [15-minute tutorial](mobile-engagement-web-app-get-started.md).</span></span>

## <a name="integration-procedures"></a><span data-ttu-id="a96da-106">整合程序</span><span class="sxs-lookup"><span data-stu-id="a96da-106">Integration procedures</span></span>
1. <span data-ttu-id="a96da-107">了解 [如何在 Web 應用程式中整合 Mobile Engagement](mobile-engagement-web-integrate-engagement.md)。</span><span class="sxs-lookup"><span data-stu-id="a96da-107">Learn [how to integrate Mobile Engagement in your web app](mobile-engagement-web-integrate-engagement.md).</span></span>
2. <span data-ttu-id="a96da-108">對於標籤計劃實作，了解 [如何在 Web 應用程式中使用進階的 Mobile Engagement 標籤 API](mobile-engagement-web-use-engagement-api.md)。</span><span class="sxs-lookup"><span data-stu-id="a96da-108">For tag plan implementation, learn [how to use the advanced Mobile Engagement tagging API in your web app](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="release-notes"></a><span data-ttu-id="a96da-109">版本資訊</span><span class="sxs-lookup"><span data-stu-id="a96da-109">Release notes</span></span>
### <a name="202-10182016"></a><span data-ttu-id="a96da-110">2.0.2 (10/18/2016)</span><span class="sxs-lookup"><span data-stu-id="a96da-110">2.0.2 (10/18/2016)</span></span>
* <span data-ttu-id="a96da-111">已修正使用私密瀏覽時的當機問題 (Safari)。</span><span class="sxs-lookup"><span data-stu-id="a96da-111">Fixed crash on private browsing (Safari).</span></span>
* <span data-ttu-id="a96da-112">已修正停用 Cookie 之瀏覽器的當機問題。</span><span class="sxs-lookup"><span data-stu-id="a96da-112">Fixed crash on browsers with cookies disabled.</span></span>

<span data-ttu-id="a96da-113">如需所有版本，請參閱 [完整版本資訊](mobile-engagement-web-release-notes.md)。</span><span class="sxs-lookup"><span data-stu-id="a96da-113">For all versions, please see the [complete release notes](mobile-engagement-web-release-notes.md).</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="a96da-114">升級程序</span><span class="sxs-lookup"><span data-stu-id="a96da-114">Upgrade procedures</span></span>
### <a name="upgrade-from-121-to-200"></a><span data-ttu-id="a96da-115">從 1.2.1 升級到 2.0.0</span><span class="sxs-lookup"><span data-stu-id="a96da-115">Upgrade from 1.2.1 to 2.0.0</span></span>
<span data-ttu-id="a96da-116">下列章節說明如何將 Mobile Engagement Web SDK 整合從 Capptain SAS 提供的 Capptain 服務移轉到 Azure Mobile Engagement 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a96da-116">The following sections describe how to migrate a Mobile Engagement Web SDK integration from the Capptain service, offered by Capptain SAS, to an Azure Mobile Engagement app.</span></span> <span data-ttu-id="a96da-117">如果您是從 1.2.1 之前的版本移轉，請參閱 Capptain 網站，先移轉到 1.2.1 後再套用以下程序。</span><span class="sxs-lookup"><span data-stu-id="a96da-117">If you are migrating from a version earlier than 1.2.1, please consult the Capptain website to migrate to 1.2.1 first, and then apply the following procedures.</span></span>

<span data-ttu-id="a96da-118">此版本的 Mobile Engagement Web SDK 不支援 Samsung Smart TV、Opera TV、webOS 或 Reach 功能。</span><span class="sxs-lookup"><span data-stu-id="a96da-118">This version of the Mobile Engagement Web SDK doesn't support Samsung Smart TV, Opera TV, webOS, or the Reach feature.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a96da-119">Capptain 和 Azure Mobile Engagement 是不同的服務，反白顯示的以下程序只適用於移轉用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="a96da-119">Capptain and Azure Mobile Engagement are not the same service, and the following procedures highlight only how to migrate the client app.</span></span> <span data-ttu-id="a96da-120">移轉應用程式中的 Mobile Engagement Web SDK，不會將您的資料從 Capptain 伺服器移轉到 Mobile Engagement 伺服器。</span><span class="sxs-lookup"><span data-stu-id="a96da-120">Migrating the Mobile Engagement Web SDK in the app will not migrate your data from a Capptain server to a Mobile Engagement server.</span></span>
> 
> 

#### <a name="javascript-files"></a><span data-ttu-id="a96da-121">JavaScript 檔案</span><span class="sxs-lookup"><span data-stu-id="a96da-121">JavaScript files</span></span>
<span data-ttu-id="a96da-122">使用 azure-engagement.js 檔案來取代 capptain-sdk.js 檔案，然後據以更新您的指令碼匯入。</span><span class="sxs-lookup"><span data-stu-id="a96da-122">Replace the file capptain-sdk.js with the file azure-engagement.js, and then update your script imports accordingly.</span></span>

#### <a name="remove-capptain-reach"></a><span data-ttu-id="a96da-123">移除 Capptain Reach</span><span class="sxs-lookup"><span data-stu-id="a96da-123">Remove Capptain Reach</span></span>
<span data-ttu-id="a96da-124">此版本的 Mobile Engagement Web SDK 不支援 Reach 功能。</span><span class="sxs-lookup"><span data-stu-id="a96da-124">This version of the Mobile Engagement Web SDK doesn't support the Reach feature.</span></span> <span data-ttu-id="a96da-125">如果您將 Capptain Reach 整合到您的應用程式，就需要加以移除。</span><span class="sxs-lookup"><span data-stu-id="a96da-125">If you have integrated Capptain Reach into your application, you need to remove it.</span></span>

<span data-ttu-id="a96da-126">從您的頁面移除 Reach CSS 匯入，並移除相關的 .css 檔案 (預設為 capptain-reach.css)。</span><span class="sxs-lookup"><span data-stu-id="a96da-126">Remove the Reach CSS import from your page and delete the related .css file (capptain-reach.css, by default).</span></span>

<span data-ttu-id="a96da-127">刪除下列 Reach 資源：關閉影像 (預設為 capptain-close.png) 和品牌圖示 (預設為 capptain-notification-icon)。</span><span class="sxs-lookup"><span data-stu-id="a96da-127">Delete the following Reach resources: the close image (capptain-close.png, by default) and the brand icon (capptain-notification-icon, by default).</span></span>

<span data-ttu-id="a96da-128">移除用於應用程式內通知的 Reach UI。</span><span class="sxs-lookup"><span data-stu-id="a96da-128">Remove the Reach UI for in-app notifications.</span></span> <span data-ttu-id="a96da-129">預設配置看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="a96da-129">The default layout looks like this:</span></span>

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

<span data-ttu-id="a96da-130">移除用於文字和 Web 宣告和輪詢的 Reach UI。</span><span class="sxs-lookup"><span data-stu-id="a96da-130">Remove the Reach UI for text and web announcements and polls.</span></span> <span data-ttu-id="a96da-131">預設配置看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="a96da-131">The default layout looks like this:</span></span>

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

<span data-ttu-id="a96da-132">從您的組態中移除 `reach` 物件 (如果存在)。</span><span class="sxs-lookup"><span data-stu-id="a96da-132">Remove the `reach` object from your configuration, if it exists.</span></span> <span data-ttu-id="a96da-133">它看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="a96da-133">It looks like this:</span></span>

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

<span data-ttu-id="a96da-134">移除所有其他的 Reach 自訂，例如類別。</span><span class="sxs-lookup"><span data-stu-id="a96da-134">Remove any other Reach customization, such as categories.</span></span>

#### <a name="remove-deprecated-apis"></a><span data-ttu-id="a96da-135">移除已被取代的 API</span><span class="sxs-lookup"><span data-stu-id="a96da-135">Remove deprecated APIs</span></span>
<span data-ttu-id="a96da-136">在 Mobile Engagement Web SDK 中，某些來自 Capptain 的 API 已被取代。</span><span class="sxs-lookup"><span data-stu-id="a96da-136">Some APIs from Capptain are deprecated in the Mobile Engagement Web SDK.</span></span>

<span data-ttu-id="a96da-137">移除針對下列 API 的所有呼叫：`agent.connect`、`agent.disconnect`、`agent.pause` 及 `agent.sendMessageToDevice`。</span><span class="sxs-lookup"><span data-stu-id="a96da-137">Remove any calls to the following APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, and `agent.sendMessageToDevice`.</span></span>

<span data-ttu-id="a96da-138">從您的 Capptain 組態移除下列回呼的任何項目：`onConnected`、`onDisconnected`、`onDeviceMessageReceived` 及 `onPushMessageReceived`。</span><span class="sxs-lookup"><span data-stu-id="a96da-138">Remove any of the following callbacks from your Capptain configuration: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, and `onPushMessageReceived`.</span></span>

#### <a name="configuration"></a><span data-ttu-id="a96da-139">組態</span><span class="sxs-lookup"><span data-stu-id="a96da-139">Configuration</span></span>
<span data-ttu-id="a96da-140">Mobile Engagement 使用連接字串來設定 SDK 識別碼，例如應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="a96da-140">Mobile Engagement uses a connection string to configure SDK identifiers, for example, the application identifier.</span></span>

<span data-ttu-id="a96da-141">使用您的連接字串來取代應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="a96da-141">Replace the application ID with your connection string.</span></span> <span data-ttu-id="a96da-142">請注意，適用於 SDK 組態的全域物件會從 `capptain` 變更為 `azureEngagement`。</span><span class="sxs-lookup"><span data-stu-id="a96da-142">Note that the global object for the SDK configuration changes from `capptain` to `azureEngagement`.</span></span>

<span data-ttu-id="a96da-143">移轉前：</span><span class="sxs-lookup"><span data-stu-id="a96da-143">Before migration:</span></span>

    window.capptain = {
      appId: ...,
      [...]
    };

<span data-ttu-id="a96da-144">移轉後：</span><span class="sxs-lookup"><span data-stu-id="a96da-144">After migration:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

<span data-ttu-id="a96da-145">您應用程式的連接字串會顯示於 Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="a96da-145">The connection string for your application is displayed in the Azure portal.</span></span>

#### <a name="javascript-apis"></a><span data-ttu-id="a96da-146">JavaScript API</span><span class="sxs-lookup"><span data-stu-id="a96da-146">JavaScript APIs</span></span>
<span data-ttu-id="a96da-147">全域 JavaScript 物件 `window.capptain` 已重新命名為 `window.azureEngagement`，但您可以針對 API 呼叫使用 `window.engagement` 別名。</span><span class="sxs-lookup"><span data-stu-id="a96da-147">The global JavaScript object `window.capptain` has been renamed `window.azureEngagement`, but you can use the `window.engagement` alias for API calls.</span></span> <span data-ttu-id="a96da-148">您無法使用此別名來定義 SDK 組態。</span><span class="sxs-lookup"><span data-stu-id="a96da-148">You can't use this alias to define the SDK configuration.</span></span>

<span data-ttu-id="a96da-149">例如，`capptain.deviceId` 會變成 `engagement.deviceId`，`capptain.agent.startActivity` 會變成 `engagement.agent.startActivity`，依此類推。</span><span class="sxs-lookup"><span data-stu-id="a96da-149">For instance, `capptain.deviceId` becomes `engagement.deviceId`, `capptain.agent.startActivity` becomes `engagement.agent.startActivity`, and so on.</span></span>

<span data-ttu-id="a96da-150">如果您已經將舊版 Azure Mobile Engagement Web SDK 整合到您的 Web 應用程式，請參閱 [升級程序](mobile-engagement-web-upgrade-procedure.md)。</span><span class="sxs-lookup"><span data-stu-id="a96da-150">If you have already integrated an earlier version of the Azure Mobile Engagement Web SDK into your application, please read about [upgrade procedures](mobile-engagement-web-upgrade-procedure.md).</span></span>

