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
# <a name="azure-mobile-engagement-web-sdk"></a>Azure Mobile Engagement Web SDK
從這裡開始針對所有 hello 詳細說明如何在 web 應用程式的 Azure Mobile Engagement toointegrate。 如果您想要 toogive 它才能開始使用您自己的 web 應用程式，再試一次看到我們[15 分鐘的教學課程](mobile-engagement-web-app-get-started.md)。

## <a name="integration-procedures"></a>整合程序
1. 深入了解[如何在 web 應用程式中的 toointegrate Mobile Engagement](mobile-engagement-web-integrate-engagement.md)。
2. 如需標記的計劃實作，了解[toouse hello 如何進階標記您的 web 應用程式中的應用程式開發介面的 Mobile Engagement](mobile-engagement-web-use-engagement-api.md)。

## <a name="release-notes"></a>版本資訊
### <a name="202-10182016"></a>2.0.2 (10/18/2016)
* 已修正使用私密瀏覽時的當機問題 (Safari)。
* 已修正停用 Cookie 之瀏覽器的當機問題。

對於所有版本，請參閱 hello[完成版本資訊](mobile-engagement-web-release-notes.md)。

## <a name="upgrade-procedures"></a>升級程序
### <a name="upgrade-from-121-too200"></a>1.2.1 從升級 too2.0.0
hello 下列章節說明如何 toomigrate hello Capptain 服務整合在 Mobile Engagement Web SDK 所提供 Capptain SAS，tooan Azure Mobile Engagement 應用程式。 如果您要從移轉稍早的版本比 1.2.1，，請參閱 hello Capptain 網站 toomigrate too1.2.1 第一次，然後再套用 hello 下列程序。

此版的 hello Mobile Engagement Web SDK 不支援 Samsung 智慧電視、 Opera 電視、 webOS 或 hello 觸達功能。

> [!IMPORTANT]
> Capptain 和 Azure Mobile Engagement 不是 hello 相同的服務，和下列程序的 hello 反白顯示如何只 toomigrate hello 用戶端應用程式。 移轉 hello Mobile Engagement Web SDK hello 應用程式中的不會移轉您的資料從 Capptain 伺服器 tooa Mobile Engagement 伺服器。
> 
> 

#### <a name="javascript-files"></a>JavaScript 檔案
取代 hello 檔案 capptain-sdk.js 以 hello 檔案 azure engagement.js，，，然後據此更新指令碼匯入。

#### <a name="remove-capptain-reach"></a>移除 Capptain Reach
此版的 hello Mobile Engagement Web SDK 不支援 hello 觸達功能。 如果您有整合 Capptain 觸達至您的應用程式，您需要 tooremove 它。

從您網頁移除 hello 到達 CSS 匯入，並刪除 hello 相關的.css 檔案 (capptain-reach.css，依預設)。

刪除下列觸達資源 hello: hello 關閉映像 (capptain-close.png，依預設) 和 hello 商標圖示 （capptain-通知-圖示，依預設）。

移除應用程式內通知的 hello 到達 UI。 hello 預設版面配置看起來像這樣：

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

移除文字和網頁的宣告與輪詢 hello 到達 UI。 hello 預設版面配置看起來像這樣：

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

移除 hello`reach`如果存在的話，從您的組態物件。 它看起來像這樣：

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

移除所有其他的 Reach 自訂，例如類別。

#### <a name="remove-deprecated-apis"></a>移除已被取代的 API
在 hello Mobile Engagement Web SDK 已被取代 Capptain 從某些應用程式開發介面。

移除下列應用程式開發介面的任何呼叫 toohello: `agent.connect`， `agent.disconnect`， `agent.pause`，和`agent.sendMessageToDevice`。

移除任何 hello Capptain 組態中的下列回呼： `onConnected`， `onDisconnected`， `onDeviceMessageReceived`，和`onPushMessageReceived`。

#### <a name="configuration"></a>組態
Mobile Engagement 會使用連接字串 tooconfigure SDK 識別項，例如 hello 應用程式識別項。

取代您的連接字串中的 hello 應用程式識別碼。 請注意該 hello 全域物件，如 hello SDK 組態變更從`capptain`太`azureEngagement`。

移轉前：

    window.capptain = {
      appId: ...,
      [...]
    };

移轉後：

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

您的應用程式的 hello 連接字串會顯示在 hello Azure 入口網站。

#### <a name="javascript-apis"></a>JavaScript API
hello 全域 JavaScript 物件`window.capptain`已重新命名`window.azureEngagement`，但是您可以使用 hello `window.engagement` API 呼叫的別名。 您無法使用此別名 toodefine hello SDK 組態。

例如，`capptain.deviceId` 會變成 `engagement.deviceId`，`capptain.agent.startActivity` 會變成 `engagement.agent.startActivity`，依此類推。

如果您已經為您的應用程式整合較早版本的 hello Azure Mobile Engagement Web SDK，請閱讀[升級程序](mobile-engagement-web-upgrade-procedure.md)。

