---
title: "aaaDiagnose 失敗-Azure 邏輯應用程式 |Microsoft 文件"
description: "常見的方式 toounderstand 邏輯應用程式失敗的位置"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: a6727ebd-39bd-4298-9e68-2ae98738576e
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 46d318625820034c95e6df3a71ab84c58f076dd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-logic-app-failures"></a>診斷邏輯應用程式失敗
如果您在與邏輯應用程式遇到問題或失敗，有幾個方法可協助您深入了解 hello 失敗所在。  

## <a name="azure-portal-tools"></a>Azure 入口網站工具
hello Azure 入口網站提供許多工具 toodiagnose 在每個步驟的每個邏輯應用程式。

### <a name="trigger-history"></a>觸發程序記錄

每個邏輯應用程式至少會有一個觸發程序。 如果您注意到未引發應用程式，看起來 hello 觸發程序的詳細資訊記錄在第一個項目。 您可以存取 hello hello 邏輯 app'ss 主要刀鋒視窗上的觸發程序歷程記錄。

![找出 hello 觸發程序的歷程記錄][1]

hello 觸發程序記錄列出的應用程式邏輯所做的所有觸發程序嘗試。 您可以按一下 每個觸發程序嘗試 toodrill 到 hello 詳細資料，特別是，任何輸入或輸出，hello 觸發程序嘗試產生。 如果您尋找失敗的觸發程序，請選取 hello 觸發程序嘗試並選擇 hello**輸出**連結的 tooreview 任何產生的錯誤訊息，例如，不是有效的 FTP 認證。

hello 不同的狀態，您可能會看到如下：

* **已略過**。 hello 端點輪詢的 toocheck 資料並收到回應，無可用的資料。
* **已成功**。 hello 觸發程序接收到回應，可用的資料。 此狀態的原因可能是手動觸發程序、循環觸發程序或輪詢觸發程序。 這個狀態通常會伴隨 hello**引發**狀態，但可能不是如果您有條件或 SplitOn 命令未滿足的程式碼檢視中。
* **失敗**。 已產生錯誤。

#### <a name="start-a-trigger-manually"></a>手動啟動觸發程序

如果您想 hello 邏輯應用程式 toocheck 立即不會等候 hello 下一個循環使用觸發程序時，按一下**選取的觸發程序**hello 主要刀鋒視窗 tooforce 核取上。 例如，按一下此連結與 Dropbox 觸發程序會造成 hello 工作流程 tooimmediately 輪詢 Dropbox 對新檔案。

### <a name="run-history"></a>執行記錄

每個引發的觸發程序都會導致一次執行。 您可以存取執行的資訊從 hello 主要刀鋒視窗中，其中包含許多可協助您了解 hello 工作流程期間發生什麼事的詳細資料。

![找出 hello 執行歷程記錄][2]

執行顯示 hello 下列狀態其中之一：

* **已成功**。 所有動作都已成功。 如果發生失敗，稍後在 hello 工作流程中發生的動作已處理該失敗。 也就被處理 hello 失敗狀況 toorun 設定失敗的動作之後的動作。
* **失敗**。 至少一個動作會在未處理的更新版本中 hello 工作流程的動作失敗。
* **已取消**。 hello 工作流程已執行但卻收到取消要求。
* **執行中**。 目前正在執行 hello 工作流程。 節流的工作流程，或因為 hello 目前定價方案，可能會發生這個狀態。 如需詳細資訊，請參閱[hello 定價頁面上的動作限制](https://azure.microsoft.com/pricing/details/app-service/plans/)。 設定診斷功能 （出現在 hello 執行歷程記錄 hello 圖表） 也可以提供所發生的任何節流事件的相關資訊。

當您查看執行歷程記錄時，您可以向內切入來查看詳細資訊。  

#### <a name="trigger-outputs"></a>觸發程序輸出

觸發程序輸出顯示 hello 資料來自 hello 觸發程序。 這些輸出可協助您判斷所有屬性是否如預期般傳回。

> [!NOTE]
> 如果您看見任何不了解的內容，請了解 Azure Logic Apps 如何[處理不同的內容類型](../logic-apps/logic-apps-content-type.md)。
> 

![觸發程序輸出範例][3]

#### <a name="action-inputs-and-outputs"></a>動作輸入和輸出

您可以切入 hello 輸入和輸出接收動作。 此資料是適合用來了解在 hello 大小和形狀 hello 輸出，以及找出可能產生任何錯誤訊息。

![動作輸入和輸出][4]

## <a name="debug-workflow-runtime"></a>偵錯工作流程執行階段

監視 hello 輸入、 輸出和執行中的觸發程序，以及您可以加入一些協助偵錯的步驟 tooa 工作流程。 
[RequestBin](http://requestb.in) 是一個強大的工具，您可以在工作流程中將其加入為一個步驟。 藉由使用 RequestBin，您可以設定的 HTTP 要求 inspector toodetermine hello 確切的大小、 圖形與 HTTP 要求的格式。 您可以建立 RequestBin，並將 hello URL 貼在邏輯應用程式與您想 tootest，例如本文內容、 運算式或另一個步驟輸出的 HTTP POST 動作。 執行 hello 邏輯應用程式之後，您可以重新整理產生從 hello Logic Apps 引擎時，如何形成 hello 要求您 RequestBin toosee。

<!-- image references -->
[1]: ./media/logic-apps-diagnosing-failures/triggerhistory.png
[2]: ./media/logic-apps-diagnosing-failures/runhistory.png
[3]: ./media/logic-apps-diagnosing-failures/triggeroutputslink.png
[4]: ./media/logic-apps-diagnosing-failures/actionoutputs.png
