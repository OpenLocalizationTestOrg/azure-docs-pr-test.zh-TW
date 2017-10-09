---
title: "Mobile Engagement Web SDK 整合 aaaAzure |Microsoft 文件"
description: "hello 最新更新和 hello Azure Mobile Engagement Web SDK 的程序"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: b5daa2a2-942b-489d-aa1d-568c3b25e56f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 02/29/2016
ms.author: piyushjo
ms.openlocfilehash: 99613b68b615bec4ddcfcc8e4e0133ce9d887bad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-mobile-engagement-in-a-web-application"></a>在 Web 應用程式中整合 Azure Mobile Engagement
> [!div class="op_single_selector"]
> * [Windows Universal](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-integrate-engagement.md)
> 
> 

本文章中的 hello 程序描述 hello 最簡單方式 tooactivate hello 分析和監視 Azure Mobile Engagement 中 web 應用程式中的函式。

請遵循 hello 步驟 tooactivate hello 記錄報表所需的 toocompute 有關使用者、 工作階段、 活動、 當機，以及 technicals 的所有統計資料。 應用程式相關的統計資料，例如事件、 錯誤和工作，您必須啟動記錄報表以手動方式使用 hello Azure Mobile Engagement 應用程式開發介面。 如需詳細資訊，了解[toouse hello 進階 Mobile Engagement 應用程式開發介面中的 web 應用程式所標記的方式](mobile-engagement-web-use-engagement-api.md)。

## <a name="introduction"></a>簡介
[下載 hello Azure Mobile Engagement Web SDK](http://aka.ms/P7b453)。
Mobile Engagement Web SDK 隨附為單一的 JavaScript 檔案的 hello，azure-engagement.js，您擁有 tooinclude 網站或 web 應用程式的每一頁中。

> [!IMPORTANT]
> 執行這個指令碼之前，您必須執行指令碼或程式碼片段，您必須撰寫 tooconfigure Mobile Engagement 應用程式。
> 
> 

## <a name="browser-compatibility"></a>瀏覽器相容性
hello Mobile Engagement Web SDK 會使用原生的 JSON 編碼和解碼，此外 （依賴 hello W3C CORS 規格） 的 toocross 網域 AJAX 要求。 它是與 hello 下列瀏覽器相容：

* Microsoft Edge 12+
* Internet Explorer 10+
* Firefox 3.5+
* Chrome 4+
* Safari 6+
* Opera 12+

## <a name="configure-mobile-engagement"></a>設定 Mobile Engagement
撰寫指令碼建立的全域`azureEngagement`JavaScript 物件，如下列範例中的 hello。 因為您的網站可能包含多個頁面，此範例假設這個指令碼包含於每個頁面中。 在此範例中，名為 hello JavaScript 物件`azure-engagement-conf.js`。

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
    };

hello`connectionString`值，您的應用程式會顯示 hello Azure 入口網站。

> [!NOTE]
> `appVersionName` 和 `appVersionCode` 是選擇性的。 不過，我們建議您設定它們，讓分析可以處理版本資訊。
> 
> 

## <a name="include-mobile-engagement-scripts-in-your-pages"></a>在頁面中包含 Mobile Engagement 指令碼
其中一種 hello 下列方式加入 Mobile Engagement 指令碼 tooyour 頁面：

    <head>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </head>

或是這個：

    <body>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </body>

## <a name="alias"></a>Alias
載入 hello Mobile Engagement Web SDK 指令碼之後，它會建立 hello **engagement**別名 tooaccess hello SDK Api。 您無法使用此別名 toodefine hello SDK 組態。 此別名將用來做為此文件中的參考。

請注意，是否與另一個全域變數，從您網頁衝突 hello 預設別名，您可以重新定義它 hello 組態中，如下所示載入 hello Mobile Engagement Web SDK 之前：

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
      alias:'anotherAlias'
    };

## <a name="basic-reporting"></a>基本報告
Mobile Engagement 中的基本報告涵蓋了工作階段層級的統計資料，例如使用者、工作階段、活動和當機的相關統計資料。

### <a name="session-tracking"></a>工作階段追蹤
Mobile Engagement 工作階段被分成一系列活動，每一個都可透過名稱來識別。

在傳統網站中，我們建議您在每個網站頁面上宣告不同的活動。 為網站或 web 應用程式中的 hello 本頁永遠不會變更，您可能想 tootrack hello 活動規模較小，例如 hello 網頁內。

是，toostart 或變更 hello 目前的使用者活動，呼叫 hello`engagement.agent.startActivity`函式。 例如：

    <body onload="yourOnload()">

    <!-- -->

    yourOnload = function() {
      [...]
      engagement.agent.startActivity('welcome');
    };

hello Mobile Engagement 伺服器自動結束 hello 應用程式頁面上關閉後的 3 分鐘內開啟的工作階段。

或者，您可以呼叫 `engagement.agent.endActivity`手動結束工作階段。 這會將目前使用者活動 too'Idle hello。 '  hello 工作階段會結束 10 秒之後，除非新太呼叫`engagement.agent.startActivity`繼續 hello 工作階段。

您可以在 hello 全域 engagement 物件設定 hello 10 秒鐘的延遲，如下所示：

    engagement.sessionTimeout = 2000; // 2 seconds
    // or
    engagement.sessionTimeout = 0; // end hello session as soon as endActivity is called

> [!NOTE]
> 您無法使用`engagement.agent.endActivity`在 hello`onunload`回呼因為您無法進行 AJAX 呼叫在這個階段。
> 
> 

## <a name="advanced-reporting"></a>進階報告
（選擇性） 如果您想 tooreport 應用程式特定事件、 錯誤和工作，您會需要 toouse hello Mobile Engagement 應用程式開發介面。 您可以透過 hello 存取 hello Mobile Engagement 應用程式開發介面`engagement.agent`物件。

您可以存取所有進階功能在 Mobile Engagement hello Mobile Engagement 應用程式開發介面中的 hello。 hello API hello 文件中詳述[toouse hello 進階 Mobile Engagement 應用程式開發介面中的 web 應用程式所標記的方式](mobile-engagement-web-use-engagement-api.md)。

## <a name="customize-hello-urls-used-for-ajax-calls"></a>自訂使用 AJAX 呼叫的 hello Url
您可以自訂 Url Mobile Engagement Web SDK 會使用該 hello。 例如，tooredefine hello 記錄 URL （hello SDK 結束點的記錄），您可以覆寫 hello 組態如下所示：

    window.azureEngagement = {
      ...
      urls: {
        ...        
        getLoggerUrl: function() {
        return 'someProxy/log';
        }
      }
    };

您的 URL 函式會傳回字串的開頭`/`， `//`， `http://`，或`https://`，不是 hello 預設配置。 根據預設，hello`https://`配置用於這些 Url。 如果您想 toocustomize hello 預設配置，來覆寫 hello 組態，像這樣：

    window.azureEngagement = {
      ...
      urls: {
        ...         
        scheme: '//'
      }
    };
