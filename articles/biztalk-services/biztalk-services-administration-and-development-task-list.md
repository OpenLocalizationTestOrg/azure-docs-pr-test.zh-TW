---
title: "aaaAdministration 和 BizTalk 服務的開發工作清單 |Microsoft 文件"
description: "部署 Azure BizTalk 服務的規劃和作業協助。"
services: biztalk-services
documentationcenter: 
author: msftman
manager: erikre
editor: 
ms.assetid: 0ab70b5b-1a88-4ba5-b329-ec51b785010e
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2016
ms.author: deonhe
ms.openlocfilehash: 544c6b23fcbc2267598b713dbe1626699099d181
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="administration-and-development-task-list-in-biztalk-services"></a>BizTalk 服務的管理與開發工作清單

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

## <a name="getting-started"></a>開始使用
當使用 Microsoft Azure BizTalk 服務，有幾個內部部署和雲端元件 tooconsider。 tooget 啟動，請考慮下列程序流程 hello:  

| 步驟 | 負責人 | 工作 | 相關連結 |
| --- | --- | --- | --- |
| 1. |系統管理員 |建立 hello Microsoft Azure 訂用帳戶使用 Microsoft 帳戶或組織帳戶 |[Azure 傳統入口網站](http://go.microsoft.com/fwlink/p/?LinkID=213885) |
| 2. |系統管理員 |建立或佈建「BizTalk 服務」。 |[使用 Azure 傳統入口網站建立「BizTalk 服務」](http://go.microsoft.com/fwlink/p/?LinkID=302280) |
| 3. |系統管理員 |註冊您或貴公司的「BizTalk 服務」部署 |[註冊和更新 BizTalk 服務部署在 hello BizTalk 服務入口網站](https://msdn.microsoft.com/library/azure/hh689837.aspx) |
| 4. |系統管理員 |適用於 hello 應用程式使用 BizTalk Adapter 服務 tooconnect tooan 在內部部署的特定業務 (LOB) 系統，或使用佇列或主題目的地。  建立 hello Azure 服務匯流排命名空間。 此命名空間、 服務匯流排簽發者名稱和服務匯流排簽發者金鑰值 toohello 開發人員提供。 |[作法：建立或修改服務匯流排服務命名空間](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md)與[取得簽發者名稱和簽發者金鑰值](biztalk-issuer-name-issuer-key.md) |
| 5. |開發人員 |安裝 hello SDK，並在 Visual Studio 中建立 hello BizTalk 服務專案。 |[安裝 Azure BizTalk 服務 SDK](https://msdn.microsoft.com/library/azure/hh689760.aspx) 與[在 Azure 上建立豐富傳訊端點](https://msdn.microsoft.com/library/azure/hh689766.aspx) |
| 6. |開發人員 |部署 BizTalk 服務在 Azure 裝載您 BizTalk 服務專案 tooyour。 |[部署和重新整理 hello BizTalk 服務專案](https://msdn.microsoft.com/library/azure/hh689881.aspx) |
| 7. |系統管理員 |適用於使用 EDI。  您可以加入夥伴和建立協議 hello Microsoft Azure BizTalk 服務入口網站上。 當您建立協議時，您可以加入 hello 橋接器和/或 hello 開發人員 toohello 協議設定所建立的轉換。 |[在 BizTalk 服務入口網站上設定 EDI、 AS2 和 EDIFACT](https://msdn.microsoft.com/library/azure/hh689853.aspx) |
| 8. |系統管理員 |使用 hello Azure 傳統入口網站，監視您的 BizTalk 服務，包括效能標準的 hello 健全狀況。 |[BizTalk 服務：儀表板、監視和調整索引標籤](http://go.microsoft.com/fwlink/p/?LinkID=302281) |
| 9. |系統管理員 |使用 hello Microsoft Azure BizTalk 服務入口網站，管理 hello hello 橋接器檔案被處理時，BizTalk 服務和追蹤訊息所使用的成品。 |[使用 hello BizTalk 服務入口網站](https://msdn.microsoft.com/library/azure/dn874043.aspx) |
| 10. |系統管理員 |建立備份計劃 tooback 向上 hello BizTalk 服務。 |[業務持續性和 BizTalk 服務的災害復原](https://msdn.microsoft.com/library/azure/dn509557.aspx) |

## <a name="next-steps"></a>後續步驟
[教學課程和範例](https://msdn.microsoft.com/library/azure/hh689895.aspx)

[在 Visual Studio 中建立 hello 專案](https://msdn.microsoft.com/library/azure/hh689811.aspx)

[安裝 Azure BizTalk 服務 SDK](https://msdn.microsoft.com/library/azure/hh689760.aspx)

## <a name="concepts"></a>概念
[在 Visual Studio 中建立 hello 專案](https://msdn.microsoft.com/library/azure/hh689811.aspx)  
[EDI、 AS2 和 EDIFACT 傳訊 (企業 tooBusiness)](https://msdn.microsoft.com/library/azure/hh689898.aspx)  

## <a name="other-resources"></a>其他資源
[新增來源、目的地和橋接器傳訊端點](https://msdn.microsoft.com/library/azure/hh689877.aspx)  
[學習和建立訊息對應與轉換](https://msdn.microsoft.com/library/azure/hh689905.aspx)  
[使用 hello BizTalk 配接器服務 (BAS)](https://msdn.microsoft.com/library/azure/hh689889.aspx)  
[Azure BizTalk 服務](http://go.microsoft.com/fwlink/p/?LinkID=303664)

