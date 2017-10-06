---
title: "aaaConnect 應用程式和整合的工作流程-Azure 邏輯應用程式資料 |Microsoft 文件"
description: "使用 Azure Logic Apps 來連接應用程式和整合資料，以建立工作流程並自動化程序。"
author: kevinlam1
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 07765c05-72a6-4169-a8ab-f6420bfbaf07
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/23/2017
ms.author: klam
ms.openlocfilehash: 53d4e165bb2205ddd56c1950719389725267ddea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-logic-apps"></a>什麼是 Logic Apps？
邏輯應用程式提供方式 toosimplify，並且實作 hello 雲端中的可擴充的整合和工作流程。 它提供視覺化設計工具 toomodel 和自動化程序當做一系列稱為工作流程的步驟。  有[多連接器](../connectors/apis-list.md)跨 hello 雲端和內部 tooquickly 整合跨服務和通訊協定。  邏輯應用程式開頭的觸發程序 （類似 '時將帳戶加入 tooDynamics CRM'） 和之後引發就可以開始的動作、 轉換、 轉換和條件邏輯多種組合。

使用 Logic Apps 的 hello 優點 hello 如下：  

* 設計複雜的程序使用簡單 toounderstand 設計工具，以節省時間
* 順暢地實作模式和工作流程，，原本是在程式碼中的難以 tooimplement
* 從範本快速開始使用
* 使用自己的自訂 API、程式碼和動作來自訂邏輯應用程式
* 連接和跨內部 g-mail 不同系統 hello 雲端
* 利用頂級整合支援打造 BizTalk Server、API 管理、Azure Functions 和 Azure 服務匯流排

邏輯應用程式是完全受管理的 iPaaS （整合平台即服務） 讓開發人員不 toohave tooworry 建置裝載、 延展性、 可用性及管理相關。  邏輯應用程式會自動 toomeet 需求向上延展。

![流程應用程式設計工具](media/logic-apps-what-are-logic-apps/LogicAppCapture2.png)

如先前所述，您可以使用 Logic Apps 將商務程序自動化。 以下是一些範例︰  

* 移動檔案上傳到 Azure 儲存體的 tooan FTP 伺服器
* 處理並路由傳送跨內部部署與雲端系統的訂單
* 監視特定的主題相關的所有推文、 分析 hello 情緒和建立警示和工作需要後續追蹤的項目。

所有從 hello 視覺化設計工具，而不需要撰寫一行程式碼，您可以設定這類的案例。 [立即開始建置邏輯應用程式][create]。  撰寫後 - 邏輯應用程式可能會 [快速部署並重新設定](../logic-apps/logic-apps-create-deploy-template.md) 於多個環境和區域。

## <a name="why-logic-apps"></a>為什麼要使用 Logic Apps？
邏輯應用程式將帶入 hello 企業整合空間的速度和延展性。  hello 容易使用的 hello 設計工具中，各種可用的觸發程序和動作，以及功能強大的管理工具進行集中管理您應用程式開發介面比以往更簡單。  當企業移往 digitalization，Logic Apps 可讓您 tooconnect 舊版和尖端系統在一起。

此外，與我們[企業整合帳戶][ biztalk]您可以調整 toomature 整合案例與 hello 冪[XML 訊息][xml]，[交易夥伴管理][tpm]，以及其他更多。

* **設計工具，輕鬆 toouse** -Logic Apps 可以設計的端對端 hello 瀏覽器中，或使用 Visual Studio tools。 觸發程序-從 GitHub 問題會建立簡單的排程 toowhen 的開頭。 然後協調任意數目的動作使用 hello 豐富圖庫的連接器。
* **輕鬆地連接 Api** -簡單 toodescribe 甚至組合工作會在程式碼中的難以 tooimplement。 邏輯應用程式可容易 tooconnect 不同的系統。 想 tooconnect 行銷方案雲端 tooyour 內部計費系統嗎？ 想 toocentralize 訊息傳送到應用程式開發介面和具有企業服務匯流排系統嗎？ 邏輯應用程式是 hello 快速、 最可靠方式 toodeliver 解決方案 toothese 問題。
* **從範本快速入門**-我們提供您開始的 toohelp[範本庫][ templates]可讓您 toorapidly 建立一些常見的解決方案。 從進階 B2B 解決方案 toosimple SaaS 連線，並，即使是幾個對於只 ' fun'-hello 圖庫是最快方式 tooget hello 入門的 Logic Apps hello 電源。
* **擴充性燒**-看不到您需要的 hello 連接器嗎？ 邏輯應用程式是設計您自己的應用程式開發介面和程式碼; toowork您可以輕鬆地建立自訂的連接器，您的應用程式開發介面應用程式 toouse 或呼叫[Azure 函式](https://functions.azure.com)tooexecute 程式碼片段的程式碼指定。 
* **真正的整合能力** - 入門容易，並且可依需求擴充。 邏輯應用程式可以輕鬆地利用 BizTalk 中，Microsoft 的業界前置整合解決方案 tooenable 整合專業人員 toobuild hello 解決方案所需 hello 的電源。 進一步了解 hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md)。

## <a name="logic-app-concepts"></a>邏輯應用程式概念
hello 以下是一些 hello 組成 hello 邏輯應用程式體驗的重要片段。 

* **工作流程**-Logic Apps 提供圖形化方式 toomodel 商務程序為一系列的步驟或工作流程。
* **管理連接器**-您的 logic apps 需要 toodata 和服務的存取。 受管理的連接器會建立特別 tooaid 您連接 tooand 處理資料時。 請參閱 hello 中立即可用的連接器清單[管理連接器][managedapis]。
* **觸發程序** - 某些受管理連接器也可以做為觸發程序。 觸發程序啟動工作流程根據特定的事件，例如電子郵件或變更您的 Azure 儲存體帳戶中的 hello 抵達的新執行的個體。
* **動作**-每個工作流程中的 hello 觸發程序呼叫的動作之後的步驟。 每個動作通常會對應 tooan managed 的連接器或自訂應用程式開發介面應用程式上的作業。
* **企業整合套件** - 在更進階的整合案例中，Logic Apps 會包含來自 BizTalk 的功能。 BizTalk 是 Microsoft 領先業界的整合平台。 hello Enterprise Integration Pack 連接器可讓您 tooeasily 包括驗證、 轉換和多個 tooyour 邏輯應用程式工作流程中。

## <a name="getting-started"></a>開始使用
* 開始使用 Logic Apps tooget 遵循 hello[建立邏輯應用程式][ create]教學課程。  
* [檢視常見的範例和案例](../logic-apps/logic-apps-examples-and-scenarios.md)
* [您可以使用 Logic Apps 自動化商務程序](http://channel9.msdn.com/Events/Build/2016/T694) 
* [深入了解如何 tooIntegrate 邏輯應用程式與系統](http://channel9.msdn.com/Events/Build/2016/P462)

[biztalk]: logic-apps-enterprise-integration-accounts.md
[appservice]: ../app-service/app-service-value-prop-what-is.md
[create]: logic-apps-create-a-logic-app.md
[managedapis]: ../connectors/apis-list.md
[tpm]: logic-apps-enterprise-integration-accounts.md
[xml]: logic-apps-enterprise-integration-b2b.md
[templates]: logic-apps-use-logic-app-templates.md
