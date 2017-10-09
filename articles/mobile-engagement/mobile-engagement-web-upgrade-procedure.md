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
# <a name="azure-mobile-engagement-web-sdk-upgrade-procedures"></a>Azure Mobile Engagement Web SDK 升級程序
如果您已經整合到您的 web 應用程式較早版本的 hello Azure Mobile Engagement Web SDK，您需要下列點，當您升級 hello SDK tooconsider hello。

如果您略過多個版本的 hello Mobile Engagement Web SDK，您可能需要 toocomplete 數個程序期間 hello 升級程序。 例如，如果您從 1.4.0 移轉 too1.6.0，第一個後續 hello 程序從 1.4.0 tooupgrade too1.5.0。 然後，遵循 1.5.0 hello 程序 tooupgrade too1.6.0。

任何版本升級，從任何舊版的 hello 檔案 azure engagement.js 取代 hello hello 檔案最新版本。

## <a name="upgrade-from-121-too200"></a>1.2.1 從升級 too2.0.0
本章節描述如何 toomigrate hello Capptain 服務整合在 Mobile Engagement Web SDK 所提供 Capptain SAS，tooan Azure Mobile Engagement 應用程式。 如果您要移轉從較早的版本，請參閱 hello Capptain 網站 toofirst 移轉 too1.2.1，然後再套用 hello 下列程序。

此版的 hello Mobile Engagement Web SDK 不支援 Samsung 智慧電視、 Opera 電視、 webOS 或 hello 觸達功能。

> [!IMPORTANT]
> Capptain 和 Azure Mobile Engagement 不是 hello 相同的服務。 下列程序的 hello 反白顯示如何只 toomigrate hello 用戶端應用程式。 移轉 hello Mobile Engagement Web SDK hello 應用程式中的不會移轉您的資料從 Capptain 伺服器 tooa Mobile Engagement 伺服器。
> 
> 

### <a name="javascript-files"></a>JavaScript 檔案
取代 hello 檔案 capptain-sdk.js 以 hello 檔案 azure engagement.js，，，然後據此更新指令碼匯入。

### <a name="remove-capptain-reach"></a>移除 Capptain Reach
此版的 hello Mobile Engagement Web SDK 不支援 hello 觸達功能。 如果您 Capptain 觸達整合至您的應用程式時，您需要 tooremove 它。

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

### <a name="remove-deprecated-apis"></a>移除已被取代的 API
在 hello Mobile Engagement Web SDK 已被取代 Capptain 從某些應用程式開發介面。

移除下列應用程式開發介面的任何呼叫 toohello: `agent.connect`， `agent.disconnect`， `agent.pause`，和`agent.sendMessageToDevice`。

移除任何執行個體的 hello Capptain 組態中的下列回呼： `onConnected`， `onDisconnected`， `onDeviceMessageReceived`，和`onPushMessageReceived`。

### <a name="configuration"></a>組態
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

### <a name="javascript-apis"></a>JavaScript API
hello 全域 JavaScript 物件`window.capptain`已重新命名`window.azureEngagement`但您可以使用 hello `window.engagement` API 呼叫的別名。 您無法使用 hello 別名 toodefine hello SDK 設定。

例如，`capptain.deviceId` 會變成 `engagement.deviceId`，`capptain.agent.startActivity` 會變成 `engagement.agent.startActivity`，依此類推。

