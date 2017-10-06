---
title: "建立 hello Marketplace 資料服務之先決條件 aaaTechnical |Microsoft 文件"
description: "了解建立資料服務 toodeploy hello 需求及 hello Azure Marketplace 上銷售"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: aaff609a-1cd1-4146-98f4-d04166b0fce0
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 2bba4282473fed63c3fcab43043a97e179705844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="technical-pre-requisites-for-creating-a-data-service-offer-for-hello-azure-marketplace"></a>Hello Azure Marketplace 提供的技術建立資料服務的必要元件
> [!IMPORTANT]
> 目前我們已不再針對任何新的資料服務發行者進行上架。新的 Dataservice 將不會獲得核准以列出於清單上。 如果您有商務 una aplicación SaaS 希望 toopublish AppSource 上，您可以找到更多資訊[這裡](https://appsource.microsoft.com/partners)。 如果您的 IaaS 應用程式或開發人員服務您會像在 Azure Marketplace toopublish 中，您可以找到更多資訊[這裡](https://azure.microsoft.com/marketplace/programs/certified/)。
> 
> 

閱讀 hello 程序開始前，徹底，並了解為何，會執行每個步驟。 盡量，您應該準備您的公司資訊和其他資料，下載必要的工具和/或建立技術元件開始 hello 供應項目建立處理程序之前。

您應該有下列項目之後，再開始 hello 程序的 hello:

## <a name="make-a-decision-on-what-technology-will-be-used-toopublish-your-data-service-offer"></a>決定何種技術會使用的 toopublish 您資料服務供應項目
在 Azure Marketplace 中發行資料服務時，發行者可以從多種技術中選擇所要使用的技術。 hello 主要技術支援，如下所述。 無論何種技術使用的 toopublish hello 資料服務，hello 使用者會耗用 hello 資料透過 hello **OData 摘要**Azure Marketplace 服務所公開。 如需 OData 服務的完整資訊，請前往 [http://www.odata.org/](http://www.odata.org/)

## <a name="sql-azure-database"></a>SQL Azure Database
發行者必須負責在 SQL Azure 中備妥資料集。 您將需要 toosubscribe tooAzure 佈建資料庫的適當大小，並將您的資料上傳到 SQL Azure 資料庫。 發行者也是負責 tookeep 其保持最新的資料。 您可以找到詳細資訊，關於訂閱 tooAzure 服務[https://azure.microsoft.com/services/sql-database/](https://azure.microsoft.com/services/sql-database/)

將 hello 資料移至 SQL Azure 時，資料表和檢視表，可以公開 hello Azure Marketplace。 hello 「 發行者 」 可以指定哪些資料行和資料表/檢視表是公開的 toohello 使用者。 Hello 使用者可以查詢哪些資料行，然後 hello 裝載只傳回何者，也可以指定進一步的 hello 內容提供者。 這可讓更多的彈性的 hello 資料庫中的資料都應該公開高層級。 可查詢的資料行需要 toobe 受到一或多個資料庫索引。

## <a name="rest-based-web-service"></a>採用 REST 的 Web 服務
支援通訊協定： **僅 HTTPS**

現有 REST 型服務可以透過 Azure Marketplace hello 公開。 因為 hello 資料集一律為公開的 toohello 使用者為 OData 摘要，hello Azure Marketplace 服務 toobe 無法 toomap 需要 hello 服務 tooa 基礎的 OData 服務。 toodo 因此 hello 基礎的 REST 端點需要 tooexpose 做為 HTTP 參數的所有參數。

hello 裝載需要 toobe 可以對應至 ATOM 回應格式。 因此 hello 回應 hello 服務需要 toobe 以 XML 格式，而且只能包含一個重複的項目，其中包含 hello 裝載值 （例如資料錄集）。 hello Azure Marketplace 服務會對應到 hello 項目節點內的屬性節點重複節點 toohello 項目節點 ATOM 和 hello 裝載值中的 hello。

授權資訊 （例如 API 金鑰，驗證語彙基元，等等） 需要 toobe 也支援做為 HTTP 參數，或在 hello HTTP 標頭 （機碼值組） – 基本驗證提供。 有效的索引鍵需要 toobe 提供，並透過 Azure Marketplace 的所有要求都會都經過該金鑰。 監視和計費的使用者會發生在 hello Azure Marketplace 的圖層。

Hello 服務所傳回的錯誤需要 toobe 對應到 HTTP 狀態碼。 萬一 hello 服務會傳回 XML，其中包含 hello 錯誤這些即將 toobe 對應 hello Azure Marketplace 服務 tooHTTP 狀態碼。

## <a name="soap-based-web-services"></a>採用 SOAP 的 Web 服務
通訊協定： **僅 HTTPS**

hello 需求是相同 hello 如 hello REST 型服務 > 一節所示。 hello 唯一的差別是也可以張貼 toohello 發行者服務透過 Azure Marketplace 所做的每個要求使用的 XML 主體中提供參數。 這表示 HTTP 參數 hello 使用者提供在 hello 前端會被轉譯為 XML 文件以 hello 要求 toohello 內容提供者的 web 服務發佈的 XML 項目。

## <a name="odata-based-web-services"></a>採用 OData 的 Web 服務
通訊協定： **僅 HTTPS**

資料可以公開為 OData 服務 tooAzure Marketplace。 hello 系統進行 toopass hello 服務透過，取代 hello Azure Marketplace 服務根目錄的所有後續呼叫會瀏覽 Azure Marketplace tooensure hello 服務根目錄的 hello。

OData 服務不只需要 toogo 針對在 hello 後端資料庫。 OData 支援任何種類的儲存體或商務邏輯 toodrive hello 服務。

## <a name="next-steps"></a>後續步驟
現在，您會檢閱 hello 必要元件，並完成 hello 必要工作，您可以繼續進行建立您資料服務供應項目中所述的 hello 與 hello[資料服務的發行指導](marketplace-publishing-data-service-creation.md)。

或者，如果您想要 tooreview hello 整體處理序和 hello 個別發行項每個發行階段的 hello，請瀏覽 hello 文章[快速入門： 如何 toopublish 優惠 toohello Azure Marketplace](marketplace-publishing-getting-started.md)。

[link-acct]:marketplace-publishing-accounts-creation-registration.md
