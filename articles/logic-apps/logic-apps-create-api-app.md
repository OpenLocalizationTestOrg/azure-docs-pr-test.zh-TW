---
title: "aaaCreate web 應用程式開發介面 （& s) REST Api 與連接器-Azure 邏輯應用程式 |Microsoft 文件"
description: "在使用 Azure 邏輯應用程式的系統整合的工作流程中建立 web 應用程式開發介面 （& s) REST Api toocall 您的應用程式開發介面、 服務或系統"
keywords: "web API, REST API, 連接器, 工作流程, 系統整合"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: bd229179-7199-4aab-bae0-1baf072c7659
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/26/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 2792204d1d298a6f810e75211c1789ee204c2fdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-custom-apis-as-connectors-for-logic-apps"></a>建立自訂 API 作為 Logic Apps 的連接器

雖然 Azure 邏輯應用程式提供了[100 + 內建連接器](../connectors/apis-list.md)，您可以使用邏輯應用程式工作流程中，您可能會想 toocall 應用程式開發介面，系統中，與服務未與連接器可用。 您可以建立您自己自訂的 Api，提供邏輯應用程式中的動作和觸發程序 toouse。 以下是其他您可能想的原因 toocreate 自己 Api 太使用與邏輯應用程式中的連接器：

* 延伸您目前的系統整合及資料整合工作流程。
* 協助客戶使用您服務 toomanage professional 或個人的工作。
* 展開 hello 觸達、 搜尋功能，以及使用您的服務。

基本上，連接器是使用 REST 作為隨插即用介面、[Swagger 中繼資料格式](http://swagger.io/specification/)作為文件，以及 JSON 作為其資料交換格式的 web API。 因為連接器是透過 HTTP 端點進行通訊的 REST API，您可以使用諸如 .NET、Java 或 Node.js 等任何語言來建置連接器。 您也可以在裝載您 Api [Azure App Service](../app-service/app-service-value-prop-what-is.md)、 平台做為服務 (PaaS) 供應項目，提供一種 hello 最佳、 簡單的方法，和擴充性最高裝載應用程式開發介面。 

針對自訂 Api toowork 與邏輯應用程式，可以提供您的 API [*動作*](./logic-apps-what-are-logic-apps.md#logic-app-concepts)邏輯應用程式工作流程中執行的特定工作。 您的 API 也可作為[*觸發程序*](./logic-apps-what-are-logic-apps.md#logic-app-concepts)，當新資料或事件符合指定的條件時，能啟動邏輯應用程式工作流程。 本主題描述常見的模式，您可以遵循建置動作和觸發程序在 API 中，根據您想要應用程式開發介面 tooprovide 的 hello 行為。

> [!TIP] 
> 雖然您可以部署與您 Api [web 應用程式](../app-service-web/app-service-web-overview.md)，請考慮部署與您 Api [API apps](../app-service-api/app-service-api-apps-why-best-platform.md)，這可讓您的工作更容易當您建置、 裝載，並使用 Api hello 雲端與內部部署。 您不需要 toochange 任何程式碼在您的應用程式開發介面中--只部署 tooan API 應用程式程式碼。 了解如何太[建置應用程式開發介面應用程式使用 ASP.NET 建立](../app-service-api/app-service-api-dotnet-get-started.md)， [Java](../app-service-api/app-service-api-java-api-app.md)，或[Node.js](../app-service-api/app-service-api-nodejs-api-app.md)。 
>
> 如需內建的邏輯應用程式的 API 應用程式範例，請瀏覽 hello [Azure 邏輯應用程式 GitHub 儲存機制](http://github.com/logicappsio)或[部落格](http://aka.ms/logicappsblog)。

## <a name="helpful-tools"></a>實用工具

自訂 API 最適合搭配邏輯應用程式時也有 hello API [Swagger 文件](http://swagger.io/specification/)描述 hello API 的作業和參數。
許多程式庫，例如[Swashbuckle](https://github.com/domaindrivendev/Swashbuckle)，自動為您產生 hello Swagger 檔案。 tooannotate hello 的顯示名稱、 屬性類型等等的 Swagger 檔案，您也可以使用[TRex](https://github.com/nihaue/TRex) ，讓您的 Swagger 檔案也適用於邏輯應用程式。

<a name="actions"></a>

## <a name="action-patterns"></a>動作模式

邏輯應用程式 tooperform 工作，應該提供您的自訂 API [*動作*](./logic-apps-what-are-logic-apps.md#logic-app-concepts)。 您的應用程式開發介面中每項作業會將對應 tooan 動作。 基本的動作是可接受 HTTP 要求並傳回 HTTP 回應的控制器。 例如，邏輯應用程式傳送的 HTTP 要求 tooyour web 應用程式或應用程式開發介面應用程式。 您的應用程式接著會傳回 HTTP 回應，應用程式可以處理以及 hello 邏輯的內容。

針對標準動作，您可以在 API 中撰寫 HTTP 要求方法，並在 Swagger 檔案中描述該方法。 接著，您可以使用 [HTTP 動作](../connectors/connectors-native-http.md)或 [HTTP + Swagger](../connectors/connectors-native-http-swagger.md) 動作直接呼叫您的 API。 根據預設，必須傳回回應 hello 內[要求逾時限制](./logic-apps-limits-and-config.md)。 

![標準動作模式](./media/logic-apps-create-api-app/standard-action.png)

<a name="pattern-overview"></a>toomake 邏輯應用程式等候您的 API 完成時間執行的工作，您的 API 可以依照 hello[非同步輪詢模式](#async-pattern)或 hello[非同步 webhook 模式](#webhook-actions)本主題中所述。 例如，可協助您以視覺化方式檢視這些模式的行為不同，假設 hello 程序來排序從由於這家蛋糕店的自訂蛋糕。 hello 輪詢模式會反映在您呼叫 hello 由於這家蛋糕店每隔 20 分鐘 toocheck hello 蛋糕是否就緒的 hello 行為。 hello webhook 模式會反映在 hello 由於這家蛋糕店會要求您輸入您的電話號碼讓它們可以在 hello 蛋糕就緒時呼叫您的 hello 行為。

如需範例，請瀏覽 hello[邏輯應用程式 GitHub 儲存機制](https://github.com/logicappsio)。 此外，深入了解[動作的使用量計量](logic-apps-pricing.md)。

<a name="async-pattern"></a>

### <a name="perform-long-running-tasks-with-hello-polling-action-pattern"></a>執行長時間執行工作以 hello 輪詢模式動作

您的 API 執行工作無法執行時間超過 hello toohave[要求逾時限制](./logic-apps-limits-and-config.md)，您可以使用 hello 非同步輪詢模式。 這種模式都有個別的執行緒，但保持作用中連線 toohello Logic Apps 引擎適用於您應用程式開發介面執行。 這樣一來，hello 邏輯應用程式不會逾時或您的 API 完成工作之前，繼續 hello hello 工作流程中的下一個步驟。

以下是一般模式將 hello:

1. 請確定該 hello 引擎能夠識別您的應用程式開發介面已接受 hello 要求，並啟動工作。
2. 當 hello 引擎進行後續要求的作業狀態時，可讓 hello 引擎知道您的 API 完成時 hello 工作。
3. 傳回相關的資料 toohello 引擎，所以 hello 邏輯應用程式工作流程才能繼續。

<a name="bakery-polling-action"></a>現在套用 hello 先前由於這家蛋糕店比喻 toohello 輪詢模式，再想像您呼叫由於這家蛋糕店和順序自訂蛋糕傳遞。 hello hello 蛋糕的製作程序需要的時間，而且您不想 hello 電話 toowait hello 由於這家蛋糕店 hello 蛋糕上時。 hello 由於這家蛋糕店確認您的訂單，您就可以呼叫 hello 蛋糕狀態每隔 20 分鐘。 20 分鐘傳遞之後，您呼叫 hello 蛋糕店，但它們會告訴您無法完成您的蛋糕，以及您應該呼叫在另一個 20 分鐘。 此回往來程序會繼續直到您呼叫，並 hello 由於這家蛋糕店告訴您，您的訂單備妥，並提供您的蛋糕。 

現在讓我們來對應回此輪詢模式。 hello 由於這家蛋糕店代表自訂 API 中，而您 hello 蛋糕客戶，代表 hello Logic Apps 引擎。 當 hello 引擎呼叫您的 API，透過要求時，您的 API 確認 hello 要求並予以回應 hello 時間間隔，hello 引擎可以檢查工作狀態時。 hello 引擎會繼續檢查工作狀態，直到您的 API 回應 hello 工作完成時，以及傳回資料 tooyour 邏輯應用程式，然後繼續進行工作流程。 

![輪詢動作模式](./media/logic-apps-create-api-app/custom-api-async-action-pattern.png)

以下是您的應用程式開發介面 toofollow，hello 應用程式開發介面的檢視方塊中所述的 hello 特定步驟：

1. 當您的 API 會取得 HTTP 要求 toostart 工作，立即傳回 HTTP`202 ACCEPTED`回應 hello`location`稍後在此步驟中所述的標頭。 這個回應可讓的 hello 引擎能夠識別您的 API 取得的 Logic Apps hello 接受的 hello 要求裝載 （資料輸入） 的要求，並立即處理。 
   
   hello`202 ACCEPTED`回應應包含這些標頭：
   
   * *需要*: A`location`標頭，指定 hello 絕對路徑 tooa URL hello Logic Apps 引擎可以請檢查您的 API 作業狀態

   * *選擇性*: A`retry-after`標頭，指定 hello 的秒數 hello 引擎應等待檢查 hello`location`作業狀態的 URL。 

     根據預設，hello 引擎會檢查每隔 20 秒。 toospecify 不同的間隔，包括 hello`retry-after`標頭和 hello 數秒，直到 hello 下一次輪詢。

2. Hello Logic Apps hello 指定時間結束之後，引擎輪詢 hello `location` URL toocheck 作業狀態。 您的 API 應執行這些檢查，並傳回這些回應：
   
   * 如果 hello 工作完成時，會傳回 HTTP`200 OK`回應，以及 hello 回應裝載 （hello 下一個步驟的輸入）。

   * 如果 hello 作業仍在處理中，則傳回另一個 HTTP`202 ACCEPTED`回應，但包含 hello 相同 hello 原始回應標頭。

當您的 API 會遵循這種模式時，您不需要 toodo 任何項目在 hello 邏輯應用程式工作流程定義 toocontinue 檢查工作狀態。 當 hello 引擎取得 HTTP`202 ACCEPTED`回應，有效`location`標頭、 hello 引擎方面 hello 非同步模式和檢查 hello`location`標頭，直到您的 API 會傳回非 202 回應為止。

> [!TIP]
> 如需非同步模式範例，請檢閱此 [GitHub 中的非同步控制器回應範例](https://github.com/logicappsio/LogicAppsAsyncResponseSample)。

<a name="webhook-actions"></a>

### <a name="perform-long-running-tasks-with-hello-webhook-action-pattern"></a>執行長時間執行工作與 hello webhook 動作模式

或者，您可以使用 hello webhook 模式針對長時間執行工作和非同步處理。 此模式沒有 hello 邏輯應用程式暫停，並等候從您的應用程式開發介面 toofinish 才能繼續工作流程處理的"callback"。 此回呼是 HTTP POST 時，會傳送訊息 tooa URL 事件發生時。 

<a name="bakery-webhook-action"></a>現在套用 hello 先前由於這家蛋糕店比喻 toohello webhook 模式，再想像您呼叫由於這家蛋糕店和順序自訂蛋糕傳遞。 hello hello 蛋糕的製作程序需要的時間，而且您不想 hello 電話 toowait hello 由於這家蛋糕店 hello 蛋糕上時。 hello 由於這家蛋糕店確認您的訂單，但這次，您可以讓您的電話號碼讓它們可以呼叫您完成 hello 蛋糕。 這次 hello 由於這家蛋糕店會告訴您訂單已就緒，而且提供您的蛋糕。

當我們對應回此 webhook 模式時，hello 由於這家蛋糕店代表您自訂 API 中的，同時您、 hello 蛋糕客戶、 代表 hello Logic Apps 引擎。 hello 引擎會呼叫您的 API，透過要求，並包含"callback"URL。
當 hello 作業完成時，您的 API 會使用 hello URL toonotify hello 引擎，並傳回資料 tooyour 邏輯應用程式，然後繼續進行工作流程。 

對於此模式，設定您控制器上的兩個端點：`subscribe` 和 `unsubscribe`

*  `subscribe`端點： hello 邏輯應用程式執行到您的 API hello 工作流程中的動作，當引擎呼叫 hello`subscribe`端點。 這個步驟會導致 hello 邏輯應用程式 toocreate 回呼 URL 會儲存您的 API，並且工作完成時，然後等待 hello 回呼，從您的 API。 您的 API (call back) 使用 HTTP POST toohello URL，然後輸入的 toohello 邏輯應用程式的形式傳遞任何傳回的內容和標頭。

* `unsubscribe`端點： hello Logic Apps 如果取消 hello 邏輯應用程式執行時，引擎會呼叫 hello`unsubscribe`端點。 您的 API 可以取消註冊 hello 回呼 URL，並停止任何處理程序在必要時。

![Webhook 動作模式](./media/logic-apps-create-api-app/custom-api-webhook-action-pattern.png)

> [!NOTE]
> 目前，hello 邏輯應用程式的設計工具並不支援透過 Swagger 探索 webhook 端點。 因此對於此模式中，您需要 tooadd [ **Webhook**動作](../connectors/connectors-native-webhook.md)並指定 hello URL、 標頭和要求主體。 另請參閱[工作流程動作與觸發程序](logic-apps-workflow-actions-triggers.md#api-connection-webhook-action)。 toopass hello 回呼 URL 中的，您可以使用 hello`@listCallbackUrl()`中 hello 前一個欄位的任何必要的工作流程函式。

> [!TIP]
> 如需範例 webhook 模式，請檢閱此 [GitHub 中的 webhook 觸發程序範例](https://github.com/logicappsio/LogicAppTriggersExample/blob/master/LogicAppTriggers/Controllers/WebhookTriggerController.cs)。

<a name="triggers"></a>

## <a name="trigger-patterns"></a>觸發程序模式

您的自訂 API 可作為[*觸發程序*](./logic-apps-what-are-logic-apps.md#logic-app-concepts)，當新資料或事件符合指定的條件時，能啟動邏輯應用程式。 這個觸發程序可以定期檢查，或是等候並接聽您服務端點上的新資料或事件。 如果新的資料或事件符合指定的條件的 hello，hello 觸發程序引發並啟動 hello 邏輯應用程式正在接聽 toothat 觸發程序。 toostart logic apps 如此一來您的 API 可以依照 hello [*輪詢觸發程序*](#polling-triggers)或 hello [ *webhook 觸發程序*](#webhook-triggers)模式。 這些模式是針對類似 tootheir 對應項目[輪詢動作](#async-pattern)和[webhook 動作](#webhook-actions)。 此外，深入了解[觸發程序的使用量計量](logic-apps-pricing.md)。

<a name="polling-triggers"></a>

### <a name="check-for-new-data-or-events-regularly-with-hello-polling-trigger-pattern"></a>新的資料或事件定期檢查以 hello 輪詢觸發程序模式

A*輪詢觸發程序*作用很像 hello[輪詢動作](#async-pattern)本主題先前所述。 hello Logic Apps 引擎會定期呼叫，並檢查 hello 觸發程序的結束點的新資料或事件。 如果 hello 引擎發現新的資料或事件符合您指定的條件，就會引發 hello 觸發程序。 然後，hello 引擎會建立處理 hello 資料做為輸入的邏輯應用程式執行個體。 

![輪詢觸發程序](./media/logic-apps-create-api-app/custom-api-polling-trigger-pattern.png)

> [!NOTE]
> 每個輪詢要求都會計算為動作執行，即使未建立邏輯應用程式執行個體時亦然。 tooprevent 處理 hello 相同的資料多次，觸發程序應該清除已讀取並傳遞 toohello 邏輯應用程式資料。

輪詢觸發程序，從 hello API 的觀點來描述特定步驟如下：

| 找到新資料或事件了嗎？  | API 回應 | 
| ------------------------- | ------------ |
| 已找到 | 傳回 HTTP`200 OK`與 hello 回應裝載 （下一個步驟的輸入） 的狀態。 <br/>此回應建立的邏輯應用程式執行個體，並啟動 hello 工作流程。 |
| 找不到 | 傳回包含 `location` 標頭和 `retry-after` 標頭的 HTTP`202 ACCEPTED` 狀態。 <br/>觸發程序，hello`location`標頭也應該包含`triggerState`查詢參數，通常是"timestamp"。 您的 API 可以使用此識別碼 tootrack hello 上次 hello 邏輯應用程式所觸發。 |

例如，tooperiodically 檢查您的服務對新檔案，您可能會建立具有這些行為的輪詢觸發程序：

| 要求是否包含 `triggerState`？ | API 回應 |
| -------------------------------- | -------------|
| 否 | 傳回 HTTP`202 ACCEPTED`狀態加上一個`location`具有標頭`triggerState`設 toohello 目前的時間和 hello`retry-after`間隔 too15 秒數。 |
| 是 | 請檢查您的服務的 hello 之後加入的檔案`DateTime`如`triggerState`。 |

| 找到的檔案數 | API 回應 |
| --------------------- | -------------|
| 單一檔案 | 傳回 HTTP`200 OK`狀態和 hello 的內容承載、 更新`triggerState`toohello `DateTime` hello 傳回的檔案，並設定`retry-after`間隔 too15 秒數。 |
| 多個檔案 | 傳回一個檔案，在階段與 HTTP`200 OK`狀態、 更新`triggerState`，並設定 hello`retry-after`間隔 too0 秒數。 </br>下列步驟讓 hello 引擎知道更多資料可用，但該 hello 引擎應該立即從 hello 中的 hello URL 要求 hello 資料`location`標頭。 |
| 沒有任何檔案 | 傳回 HTTP`202 ACCEPTED`狀態，請不要變更`triggerState`，和集合 hello`retry-after`間隔 too15 秒數。 |

> [!TIP]
> 如需範例輪詢觸發程序模式，請檢閱此 [GitHub 中的輪詢觸發程序控制器範例](https://github.com/logicappsio/LogicAppTriggersExample/blob/master/LogicAppTriggers/Controllers/PollTriggerController.cs)。

<a name="webhook-triggers"></a>

### <a name="wait-and-listen-for-new-data-or-events-with-hello-webhook-trigger-pattern"></a>等候和接聽新的資料或與 hello webhook 觸發程序模式的事件

Webhook 觸發程序是推送觸發程序，會等候並接聽您服務端點中的新資料或事件。 如果新的資料或事件符合 hello 指定的條件，hello 引發觸發程序，並建立的邏輯應用程式執行個體，然後處理 hello 資料做為輸入。
Webhook 觸發程序作用很像 hello [webhook 動作](#webhook-actions)之前所述，本主題中，並使用設定`subscribe`和`unsubscribe`端點。 

* `subscribe`端點： hello Logic Apps 當您新增及儲存 webhook 觸發程序邏輯應用程式中時，引擎會呼叫 hello`subscribe`端點。 這個步驟會導致 hello 邏輯應用程式 toocreate 回呼 URL 儲存您的 API。 當新的資料或事件符合 hello 指定的條件時，您的 API 呼叫回 HTTP POST toohello url。 hello 內容裝載和標頭傳遞做為輸入的 toohello 邏輯應用程式。

* `unsubscribe`端點： hello Logic Apps 如果刪除 hello webhook 觸發程序或整個邏輯應用程式時，引擎會呼叫 hello`unsubscribe`端點。 您的 API 可以取消註冊 hello 回呼 URL，並停止任何處理程序在必要時。

![Webhook 觸發程序](./media/logic-apps-create-api-app/custom-api-webhook-trigger-pattern.png)

> [!NOTE]
> 目前，hello 邏輯應用程式的設計工具並不支援透過 Swagger 探索 webhook 端點。 因此對於此模式中，您需要 tooadd [ **Webhook**觸發程序](../connectors/connectors-native-webhook.md)並指定 hello URL、 標頭和要求主體。 另請參閱 [HTTPWebhook 觸發程序](logic-apps-workflow-actions-triggers.md#httpwebhook-trigger)。 toopass hello 回呼 URL 中的，您可以使用 hello`@listCallbackUrl()`中 hello 前一個欄位的任何必要的工作流程函式。
>
> tooprevent 處理 hello 相同的資料多次，觸發程序應該清除已讀取並傳遞 toohello 邏輯應用程式資料。

> [!TIP]
> 如需範例 webhook 模式，請檢閱此 [GitHub 中的 webhook 觸發程序控制器範例](https://github.com/logicappsio/LogicAppTriggersExample/blob/master/LogicAppTriggers/Controllers/WebhookTriggerController.cs)。

## <a name="deploy-call-and-secure-custom-apis"></a>部署、呼叫並保護自訂 API

建立您的自訂 API 之後，請設定您的 API 以進行部署，讓您可安全地呼叫它們。 了解如何太[部署，請呼叫，和邏輯應用程式的自訂 Api](./logic-apps-custom-hosted-api.md)。

## <a name="publish-custom-apis-tooazure"></a>發行自訂應用程式開發介面 tooAzure

toomake 您自訂應用程式開發介面提供公用用途，在 Azure 中，會送出提名 toohello [Microsoft Azure 認證計劃](https://azure.microsoft.com/marketplace/programs/certified/logic-apps/)。

## <a name="get-help"></a>取得說明

如需自訂 API 的特定說明，請連絡 [customapishelp@microsoft.com](mailto:customapishelp@microsoft.com)。

tooask 問題、 解答的問題，以及執行其他 Azure 邏輯應用程式使用者，請參閱瀏覽 hello [Azure 邏輯應用程式論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)。

toohelp 改善邏輯應用程式和連接器、 票選或送出意見在 hello [Logic Apps 使用者意見反應網站](http://aka.ms/logicapps-wish)。 

## <a name="next-steps"></a>後續步驟

* [動作和觸發程序的使用量計量](logic-apps-pricing.md)
* [處理內容類型](./logic-apps-content-type.md)
* [處理錯誤和例外狀況](./logic-apps-exception-handling.md)
* [安全存取 tooyour 邏輯應用程式](./logic-apps-securing-a-logic-app.md)
* [透過 HTTP 端點呼叫、觸發或巢狀處理 Logic Apps](./logic-apps-http-endpoint.md)