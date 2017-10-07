---
title: "Azure 函式的 aaaBest 作法 |Microsoft 文件"
description: "了解 Azure Functions 的最佳作法與模式。"
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "azure functions, 模式, 最佳作法, 函數, 事件處理, webhook, 動態計算, 無伺服器架構"
ms.assetid: 9058fb2f-8a93-4036-a921-97a0772f503c
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/13/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bd3d826b75267a740e355b008943a48f71ebd339
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-hello-performance-and-reliability-of-azure-functions"></a>最佳化 hello 效能和可靠性的 Azure 函式

本文提供指引 tooimprove hello 效能和可靠性的函式應用程式。 


## <a name="avoid-long-running-functions"></a>避免長時間執行的函式

大型長時間執行的函式可能會造成非預期的逾時問題。 函式可以變得很大，因為 toomany Node.js 相依性的。 匯入相依性也可能會造成載入時間增加，而導致未預期的逾時。 系統會以明確和隱含方式載入相依性。 您的程式碼載入的單一模組可能會載入其本身的其他模組。  

在可能時，將大型函式重構為較小的函式集，共用運作並快速傳回回應。 例如，webhook 或 HTTP 觸發程序函式可能需要在特定時間限制; 內的通知回應很常見的 webhook toorequire 立即回應。 您可以將 hello HTTP 觸發程序裝載傳遞至處理佇列的觸發程序函式的佇列 toobe。 此方法可讓您 toodefer hello 實際工作，並立即的回應傳回。


## <a name="cross-function-communication"></a>跨函式通訊

整合多個函式，通常是最佳作法 toouse 儲存體佇列的跨函式的通訊。  hello 主要原因是儲存體佇列的成本較低，更容易 tooprovision。 

儲存體佇列中的個別訊息僅限於大小 too64 KB。 如果您需要 toopass 函式之間的較大訊息時，Azure 服務匯流排佇列可能是使用的 toosupport 向上 too256 KB 的訊息大小。

如果您需要在處理之前篩選訊息，服務匯流排主題會很實用。

事件中心是有用的 toosupport 大量通訊。


## <a name="write-functions-toobe-stateless"></a>撰寫函式 toobe 無狀態 

若可能，Functions 應該是無狀態和具有等冪性。 將任何必要的狀態資訊與您的資料產生關聯。 例如，正在處理訂單就可能具有相關聯的 `state` 成員。 函式無法處理 hello 函式本身仍無狀態時，依據該狀態的順序。 

特別建議計時器觸發程序使用等冪函式。 例如，如果您有絕對必須執行一天一次的項目，將它寫入讓它可以執行任何 hello 一天的時間與 hello 相同的結果。 沒有特定的一天的工作時，就可以結束 hello 函式。 也表示上次執行失敗，toocomplete，接下來執行的 hello 應該挑選中斷的位置。


## <a name="write-defensive-functions"></a>編寫防禦性函式

假設您的函式可能隨時會遇到例外狀況。 設計您的函式與 hello 能力 toocontinue 從先前的失敗點 hello 下一步 執行期間。 請考慮需要 hello 下列動作的案例：

1. 查詢資料庫中的 10,000 個資料列。
2. 為每個向 hello 列進一步這些資料列 tooprocess 建立佇列訊息。
 
根據系統的複雜程度，您可能會有︰相關的下游服務行為不當、網路中斷或到達配額限制等等。這所有方面都隨時會影響您的函式。 您需要 toodesign 準備您的函式 toobe。

如果在插入這些項目中的 5,000 個至佇列以進行處理之後發生失敗，您的程式碼如何因應？ 追蹤集合中您已完成的項目。 否則，您可能下一次又將它們插入。 這對您的工作流程會有嚴重影響。 

如果已經處理佇列項目，可讓函式 toobe 無作業。

利用下防禦措施已提供您使用在 hello Azure 函式平台的元件。 例如，請參閱**處理佇列有害訊息**hello 文件中[Azure 儲存體佇列觸發程序](functions-bindings-storage-queue.md#trigger)。
 

## <a name="dont-mix-test-and-production-code-in-hello-same-function-app"></a>請勿混合測試和生產環境中的程式碼 hello 相同函式應用程式

函式應用程式內的 Functions 會共用資源。 例如，共用記憶體。 如果您在生產環境中使用的函式應用程式，不加入測試相關的函式和資源 tooit。 在實際執行程式碼執行期間可能導致發生未預期的額外負荷。

對於在實際執行函式應用程式中載入的項目，請務必小心。 記憶體會平均值 hello 應用程式中的每個函式。

如果您在多個 .Net 函式中參考某個共用組件，請將它置於通用的共用資料夾中。 參考陳述式的類似 toohello，下列範例與 hello 組件： 

    #r "..\Shared\MyAssembly.dll". 

否則，很容易 tooaccidentally 部署的 hello 函式相同的行為方式之間的二進位檔的多個測試版本。

請勿在實際執行程式碼中使用詳細資訊記錄。 它對效能會有負面影響。



## <a name="use-async-code-but-avoid-blocking-calls"></a>使用非同步程式碼但避免封鎖呼叫

非同步程式設計是建議的最佳作法。 不過，一律避免參考 hello`Result`屬性或呼叫`Wait`方法`Task`執行個體。 這個方法會導致 toothread 耗盡。


[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="next-steps"></a>後續步驟
如需詳細資訊，請參閱下列資源的 hello:

因為 Azure Functions 使用 Azure App Service，所以您也應該充分了解 Azure App Service 指導方針。
* [HTTP 效能最佳化的模式與做法](https://docs.microsoft.com/azure/architecture/antipatterns/improper-instantiation/)

