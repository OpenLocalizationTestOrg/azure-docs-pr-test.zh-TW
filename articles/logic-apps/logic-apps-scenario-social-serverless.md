---
title: "aaaScenario-使用 Azure 無伺服器建立客戶 insights 儀表板 |Microsoft 文件"
description: "如何建置儀表板 toomanage 客戶，意見反應、 社交資料，以及更多 Azure 邏輯應用程式與 Azure 函式的範例。"
keywords: 
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/29/2017
ms.author: jehollan
ms.openlocfilehash: db175e895e37aa795a9c34bf4d65566bf68f8c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-real-time-customer-insights-dashboard-with-azure-logic-apps-and-azure-functions"></a>使用 Azure Logic Apps 與 Azure Functions 來建立即時的客戶深入解析儀表板

Azure 的無伺服器工具提供強大的功能 tooquickly hello 雲端中的建置和裝載應用程式而不需要 toothink 相關基礎結構。  在此案例中，我們將客戶的意見反應上建立儀表板 tootrigger、 分析使用機器學習和發行 insights 像 Power BI 或 Azure 資料湖來源。

## <a name="overview-of-hello-scenario-and-tools-used"></a>Hello 案例及使用工具的概觀

在排序 tooimplement 此解決方案中，我們將利用的無伺服器的應用程式在 Azure 中的 hello 兩個主要元件： [Azure 函式](https://azure.microsoft.com/services/functions/)和[Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/)。

邏輯應用程式是無伺服器的工作流程引擎 hello 雲端中。  它提供無伺服器的元件之間的協調流程，並且也會連接 tooover 100 個服務和應用程式開發介面。  此案例中，我們將建立邏輯應用程式 tootrigger 來自客戶的意見反應。  對回應 toocustomer 意見反應可協助 hello 連接器包括 Outlook.com、 Office 365、 問卷猴子、 Twitter 和 HTTP 要求[從 web 表單](https://blogs.msdn.microsoft.com/logicapps/2017/01/30/calling-a-logic-app-from-an-html-form/)。  如下列的 hello 工作流程，我們會監視在 Twitter 上的說明。

函式提供無伺服器 hello 雲端中的計算。  在此案例中，我們將使用來自客戶的一系列預先定義的索引鍵文字為基礎的 Azure 函式 tooflag 推文。

hello 整個方案可以是[Visual Studio 中建置](logic-apps-deploy-from-vs.md)和[做為資源範本的一部分部署](logic-apps-create-deploy-template.md)。  另外還有 hello 案例的視訊逐步解說[Channel 9 上](http://aka.ms/logicappsdemo)。

## <a name="build-hello-logic-app-tootrigger-on-customer-data"></a>Hello 邏輯應用程式 tootrigger 根據客戶資料

之後[建立邏輯應用程式](logic-apps-create-a-logic-app.md)在 Visual Studio 或 hello Azure 入口網站：

1. 針對來自 Twitter 的**新推文**新增觸發程序
2. 設定 hello 觸發程序 toolisten tootweets 關鍵字或雜湊標記上。

   > [!NOTE]
   > hello 的觸發程序的 hello 循環屬性將決定 hello 邏輯應用程式檢查新的項目，以輪詢為基礎的觸發程序的頻率

   ![Twitter 觸發程序的範例][1]

此應用程式現在會針對所有新推文引發。  我們可以採取該推文中的資料，並了解多個表示 hello 人氣。  為此，我們使用 hello [Azure 認知服務](https://azure.microsoft.com/services/cognitive-services/)toodetect 人氣的文字。

1. 按一下 [新步驟]
1. 選取或搜尋 hello**文字分析**連接器
1. 選取 hello**偵測人氣**作業
1. 如果出現提示，請提供有效的認知的服務金鑰的 hello 文字分析服務
1. 新增 hello**推文文字**hello 文字 tooanalyze 如下。

現在，我們已經 hello 推文中的資料和 insights hello 推文上時，可能相關的其他連接器的數字：
* Power BI-加入資料集的資料列 tooStreaming: Power BI 儀表板上的即時檢視排行推文。
* Azure Data Lake 的附加檔案： 將客戶資料 tooan Azure 資料湖資料集 tooinclude 加入在分析工作。
* SQL - 新增資料列︰將資料儲存在資料庫中，以供日後擷取。
* Slack - 傳送訊息︰針對需要有所行動的負面意見反應在 Slack 通道上發出警示。

Azure 函式也可以使用的 toodo 需自訂計算 hello 中的資料之上。

## <a name="enriching-hello-data-with-an-azure-function"></a>充實 hello 資料與 Azure 函式

我們可以建立函式之前，我們將在我們的 Azure 訂用帳戶中需要 toohave 函式應用程式。  Hello 入口網站中建立 Azure 函式的詳細資訊可以[在這裡找到](../azure-functions/functions-create-first-azure-function-azure-portal.md)

針對直接從邏輯應用程式呼叫函式 toobe，就需要 toohave HTTP 觸發繫結。  我們建議您使用 hello **HttpTrigger**範本。

在此案例中，hello 要求主體的 hello Azure 函式會推文中的 hello 文字。  在 hello 函式程式碼，只是邏輯上定義如果推文中的 hello 文字包含關鍵字或片語。  為簡單或複雜視 hello 案例中，無法保留 hello 函式本身。

在 hello hello 函式結尾，就只會傳回回應 toohello 邏輯應用程式的某些資料。  這可能是簡單的布林值 (例如 `containsKeyword`) 或複雜的物件。

![已設定的 Azure Function 步驟][2]

> [!TIP]
> 當從邏輯應用程式中的函式中存取複雜的回應，請使用 hello 剖析 JSON 動作。

Hello 函式儲存之後，它會加入到上面所建立的 hello 邏輯應用程式。  在 hello 邏輯應用程式：

1. 按一下 tooadd**新步驟**
1. 選取 hello **Azure 函式**連接器
1. 選取 toochoose 現有的函式，並瀏覽所建立的 toohello 函式
1. 傳送嗨**推文文字**hello**要求本文**

## <a name="running-and-monitoring-hello-solution"></a>執行且監視 hello 方案

撰寫無伺服器的協調流程中的 Logic Apps hello 優點的其中一個是 hello 豐富的偵錯和監視功能。  在 Visual Studio 中，hello Azure 入口網站，或透過 hello REST API 和 Sdk，可以從檢視任何執行 （目前或歷程記錄）。

其中一個最簡單方式 tootest hello 邏輯應用程式正在使用 hello**執行**hello 設計工具中的按鈕。  按一下**執行**會繼續直到偵測到事件時，每隔 5 秒 toopoll hello 觸發程序，並隨著 hello 執行提供的即時檢視。

Hello Azure 入口網站，或使用 hello Visual Studio Cloud Explorer 中的 hello 概觀刀鋒視窗上，您可以檢視先前執行的記錄。

## <a name="creating-a-deployment-template-for-automated-deployments"></a>建立部署範本來進行自動化部署

一旦開發的解決方案，它可以擷取，並透過 Azure 部署範本 tooany hello 世界中的 Azure 地區部署。  這不僅適用於修改參數以獲得此工作流程的不同版本，也適用於在建置和發行管線中整合此解決方案。  關於建立部署範本的詳細資料可以[在此文章中](logic-apps-create-deploy-template.md)找到。

Azure 函式也在 hello 部署範本-合併，因此可視為單一範本管理 hello 整個方案的所有相依性。  函式的部署範本的範例，請參閱 hello [Azure 快速入門範本儲存機制](https://github.com/Azure/azure-quickstart-templates/tree/master/101-function-app-create-dynamic)。

## <a name="next-steps"></a>後續步驟

* [查看 Azure Logic Apps 的其他範例和案例](logic-apps-examples-and-scenarios.md)
* [觀看關於完整建立此解決方案的影片逐步解說](http://aka.ms/logicappsdemo)
* [深入了解如何在邏輯應用程式內 toohandle 和 catch 例外狀況](logic-apps-exception-handling.md)

<!-- Image References -->
[1]: ./media/logic-apps-scenario-social-serverless/twitter.png
[2]: ./media/logic-apps-scenario-social-serverless/function.png