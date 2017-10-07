---
title: "從 BizTalk 服務 tooAzure Logic Apps aaaMove 應用程式 |Microsoft 文件"
description: "移動或移轉 Azure BizTalk 服務 MABS tooLogic 應用程式"
services: logic-apps
documentationcenter: 
author: jonfancey
manager: anneta
editor: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: ladocs; jonfan; mandia
ms.openlocfilehash: b3b065b90a37002f72305b0fc866c24231fb5f9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-from-biztalk-services-toologic-apps"></a>從 BizTalk 服務 tooLogic 應用程式

Microsoft Azure BizTalk 服務 (MABS) 即將停用。 使用此主題 toomove 您 MABS 整合解決方案 tooAzure 邏輯應用程式。 

## <a name="overview"></a>概觀

BizTalk 服務包含兩個子服務：

1.  Microsoft BizTalk 服務混合式連線
2.  EAI 和 EDI 橋接器架構整合

如果您要尋找 toomove 混合式連線，然後[Azure 應用程式服務的混合式連線](../app-service/app-service-hybrid-connections.md)描述 hello 變更與此服務的功能。 Azure 混合式連線取代了 BizTalk 服務混合式連線。 Azure 的混合式連線適用於 Azure 應用程式服務，並提供在 hello Azure 入口網站中。 Azure 的混合式連線也會提供新的混合式連線管理員 toomanage，現有的 BizTalk 服務混合式連線，並在您建立新的混合式連線 hello 入口網站。 Azure App Service 混合式連線已正式上市 (GA)。

Logic Apps EAI 和 EDI 橋接器架構整合，為 hello 取代。 邏輯應用程式提供所有 hello 與 BizTalk 服務和多個相同的功能。 邏輯應用程式提供雲端規模消費型工作流程和協調流程功能可讓您 tooquickly 和輕鬆建立複雜的整合方案使用瀏覽器，或使用 Visual Studio 中的工具。

下表中的 hello 提供 BizTalk 服務功能對應 tooLogic 應用程式。

| BizTalk 服務   | Logic Apps            | 目的                  |
| ------------------ | --------------------- | ---------------------------- |
| 連接器          | 連接器             | 傳送及接收資料   |
| 橋接器             | 邏輯應用程式             | 管線處理器           |
| 驗證階段     | XML 驗證動作      | 驗證 XML 文件的結構描述             |
| 擴充階段       | 資料權杖      | 將屬性升級為訊息或針對路由決策升級屬性             |
| 轉換階段    | 轉換動作      | 從一種格式 tooanother 轉換 XML 訊息             |
| 解碼階段       | 一般檔案解碼動作      | 從一般檔案 tooXML 轉換             |
| 編碼階段       |  一般檔案編碼動作      | 從 XML tooflat 檔案轉換             |
| 訊息檢查       |  Azure Functions 或 API Apps      | 在您的整合中執行自訂程式碼             |
| 路由動作      |  條件或 Switch      | 路由訊息 tooone 的 hello 指定連接器             |

BizTalk 服務中有許多不同類型的成品。

## <a name="connectors"></a>連接器
BizTalk 服務的連接器可讓橋接器 toosend 和接收資料，包括啟用 http 要求/回應互動的雙向橋接器。 在邏輯應用程式，會使用相同的詞彙的 hello。 邏輯應用程式中的連接器提供的 hello 相同用途，而且也包含 [超過 140 可以連接 tooa 眾多技術和服務，則這兩個內部部署使用 hello （取代 hello BizTalk 服務所使用的 BizTalk 配接器服務） 在內部部署資料閘道，部署和雲端 SaaS 和 PaaS 服務，例如 OneDrive、 Office365、 Dynamics CRM 和更多。

在 BizTalk 服務中的來源為有限的 tooFTP、 SFTP 和服務匯流排佇列或主題訂用帳戶。

![](media/logic-apps-move-from-mabs/sources.png)

每個橋接器已依預設，已設定執行階段位址 hello 與 hello 的 hello 橋接器的相對位址屬性的 HTTP 端點。 tooachieve 相同邏輯應用程式，請使用 hello 與 hello[要求和回應](../connectors/connectors-native-reqres.md)動作。

## <a name="xml-processing-and-bridges"></a>XML 處理和橋接器
在 [BizTalk 服務橋接器是一種類似 tooa 處理管線。 一個橋接器可以使用連接器，從接收的資料，並執行一些處理 hello 資料，然後將它傳送 tooanother 系統。 邏輯應用程式沒有 hello 支援 hello 相同管線為基礎的互動模式為 BizTalk 服務和也提供了許多其他整合模式的相同。 hello [XML 要求-回覆橋接器](https://msdn.microsoft.com/library/azure/hh689781.aspx)BizTalk 服務中稱為 VETER 管線可以的階段所組成：

* (V) 驗證
* (E) 擴充
* (T) 轉換
* (E) 擴充
* (R) 路由

Hello 下列影像所示，hello 處理會要求和回覆之間分割，並允許控制項 hello 要求和 hello 分開 （例如，針對每個使用不同的對應） 的回覆路徑：

![](media/logic-apps-move-from-mabs/xml-request-reply.png)

此外，XML 單向橋接器 hello 開頭和結尾的處理，新增解碼和編碼階段與 hello 通過橋接器包含單一的 「 擴充 」 階段。

### <a name="message-processing-and-decodingencoding"></a>訊息處理和解碼/編碼
在 BizTalk 服務中，您可以接收 XML 訊息的類型不同，並判斷 hello 收到 hello 訊息的比對結構描述。 執行這個動作是在 hello**訊息類型**hello 階段接收處理管線。 然後，hello 解碼階段會使用偵測到的 hello 訊息類型 toodecode 使用 hello 提供結構描述。 如果 hello 結構描述是 flatfile 結構描述，它會將轉換傳入 flatfile tooXML hello。 

Logic Apps 提供類似的功能。 您收到 flatfile 透過各種不同的通訊協定使用 hello 不同連接器觸發程序 （檔案系統、 FTP、 HTTP 等等），並使用 hello[一般檔案解碼](../logic-apps/logic-apps-enterprise-integration-flatfile.md)動作 tooconvert hello 內送資料 tooXML。 您可以直接 toologic 應用程式，而不需要任何變更，然後再上傳結構描述 tooyour 整合帳戶來移動現有的一般檔案結構描述。

### <a name="validation"></a>驗證
Hello 內送資料是轉換的 tooXML （或 XML 是否收到 hello 訊息格式） 之後，驗證就會執行 toodetermine 如果 hello 訊息遵守 tooyour XSD 結構描述。 toodo 這在邏輯應用程式，使用 hello [XML 驗證](../logic-apps/logic-apps-enterprise-integration-xml-validation.md)動作。 同樣地，您可以使用 hello 相同的結構描述從 BizTalk 服務不進行任何變更。

### <a name="transform-messages"></a>轉換訊息
BizTalk 服務的 hello 轉換階段會將一個 XML 為基礎之訊息格式 tooanother 轉換。 這是藉由套用地圖中，使用 hello TRFM 為基礎的對應工具。 在邏輯應用程式，hello 程序相似。 hello 轉換動作會執行對應的整合帳戶。 hello 主要差異是，在邏輯應用程式中的對應中以 XSLT 格式。 XSLT 包括 hello 能力 tooreuse 現有您已經有，包括 BizTalk server 所建立的對應包含運算質的 XSLT。 

### <a name="routing-rules"></a>路由規則
BizTalk 服務會在哪個端點/連接器 toosend 內送訊息/資料建立路由的決策。 其中一個預先設定的端點數目 hello 能力 tooselect 是可能使用 hello 路由篩選選項：

![](media/logic-apps-move-from-mabs/route-filter.png)

Logic Apps 提供具有[條件](../logic-apps/logic-apps-use-logic-app-features.md)和 [Switch](../logic-apps/logic-apps-switch-case.md) 的更複雜邏輯功能，以啟用進階控制流程和路由。 「如果」只有兩個選項，使用**條件**最能達成 BizTalk 服務中的路由篩選轉換。 如果有兩個以上的選項，則使用 **switch**。

### <a name="enrich"></a>擴充
hello 處理 BizTalk 服務的 「 擴充 」 階段新增與接收的 hello 資料相關聯的屬性 toohello 訊息內容。 例如，升級屬性 toouse 路由 （討論如下） 從資料庫查詢，或藉由擷取使用 XPath 運算式的值。 邏輯應用程式提供存取 tooall 內容資料的輸出從上述動作，讓您直接 tooreplicate hello 相同的行為。 例如，使用 hello `Get Row` SQL 連線的動作，您傳回資料從 SQL Server 資料庫，以及使用 hello 資料以進行路由決策動作。 同樣地，連入的服務匯流排上的屬性則觸發程序的佇列訊息是定址，以及使用 hello xpath 工作流程定義語言運算式的 XPath。

### <a name="use-custom-code"></a>使用自訂程式碼
BizTalk 服務提供 hello 能力太[執行自訂程式碼](https://msdn.microsoft.com/library/azure/dn232389.aspx)上傳您自己的組件中。 這藉由 hello [IMessageInspector](https://msdn.microsoft.com/library/microsoft.biztalk.services.imessageinspector.aspx)介面。 Hello 橋接器的每個階段包括提供 hello.Net 您建立的類型可實作此介面的兩個屬性 （[On Enter Inspector 和 [On Exit Inspector）。 自訂程式碼可讓您 tooperform 更複雜處理 hello 資料，以及執行一般商務邏輯的組件中重複使用現有的程式碼。 

邏輯應用程式提供兩種主要方法 tooexecute 自訂程式碼： Azure 函式和 API 應用程式。 您可以建立 Azure Functions，並從 Logic Apps 呼叫。 請參閱[透過 Azure Functions 新增並執行適用於 Logic Apps 的自訂程式碼](../logic-apps/logic-apps-azure-functions.md)。 您自己的觸發程序和動作，請使用應用程式開發介面應用程式，Azure 應用程式服務，toocreate 的一部分。 深入了解[使用邏輯應用程式建立自訂的應用程式開發介面 toouse](../logic-apps/logic-apps-create-api-app.md)。 

如果您從 BizTalk 服務呼叫的 assmeblies 中有自訂程式碼，您可以移動這個程式碼 tooAzure 函式，或是自訂應用程式開發介面建立 API 應用程式。視您正在實作。 比方說，如果您包裝 Logic Apps 沒有連接器的另一個服務的程式碼，然後建立 API 應用程式，並使用您 API 應用程式提供邏輯應用程式中的 hello 動作。 如果您有 helper 函式或程式庫，Azure 函式就會很有可能 hello 最適大小。

### <a name="edi-processing-and-trading-partner-management"></a>EDI 處理和交易夥伴管理
BizTalk 服務包含 EDI 和 B2B 處理，並支援 AS2 (Applicability Statement 2)、X12 和 EDIFACT。 Logic Apps 也是。 在 BizTalk 服務中，您建立 EDI 橋接器和建立/管理交易夥伴和協議 hello 專用的追蹤和管理網站中。

在邏輯應用程式，此功能隨附於 hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md)。 這包含 EDI 和 B2B 處理的 hello 整合帳戶和 B2B 動作。 hello[整合帳戶](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md)是使用的 toocreate 和管理[交易夥伴](../logic-apps/logic-apps-enterprise-integration-partners.md)和[協議](../logic-apps/logic-apps-enterprise-integration-agreements.md)。 一旦您建立整合帳戶時，您可以將一個或多個邏輯應用程式 toohello 帳戶建立關聯。 一旦建立關聯，您可以使用交易夥伴資訊邏輯應用程式中的 hello B2B 動作 tooaccess。 提供 hello 下列動作：

* AS2 編碼
* AS2 解碼
* X12 編碼
* X12 解碼
* EDIFACT 編碼
* EDIFACT 解碼

不同於 BizTalk 服務，這些動作會分開 hello 傳輸通訊協定。 因此當您建立您的 logic apps，您必須在哪一個連接器使用 toosend 和接收資料的更多彈性。 比方說，它是從電子郵件附件可能 tooreceive X12 檔案，並接著處理邏輯應用程式中的這些檔案。 

## <a name="manage-and-monitor"></a>管理和監視
交易夥伴管理，以及 hello 專用入口網站的 BizTalk 服務提供追蹤功能 toomonitor 及疑難排解問題。 

邏輯應用程式提供更豐富的追蹤和監視功能中 hello [Azure 入口網站](../logic-apps/logic-apps-monitor-your-logic-apps.md)，並以 hello [Operations Management Suite B2B 解決方案](../logic-apps/logic-apps-monitor-b2b-message.md); 包含使項目上的行動應用程式當您在 hello 移動。

## <a name="high-availability"></a>高可用性
tooachieve 高可用性 (HA) 在 BizTalk 服務中的，您會使用多個執行個體中指定的地區 tooshare hello 處理負載。 使用 Logic Apps，區域中會內建 HA，無需額外費用。 若要在區域之外對 BizTalk 服務中的 B2B 處理進行災害復原，則需要備份和還原程序。 在邏輯應用程式，跨地區的主動/被動[DR 功能](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md)提供; 可讓在不同區域的業務續航力整合帳戶之間的 hello B2B 資料同步處理。

## <a name="next"></a>下一步
* [什麼是 Logic Apps](logic-apps-what-are-logic-apps.md)
* [建立第一個邏輯應用程式](logic-apps-create-a-logic-app.md)，或使用[預先建置的範本](logic-apps-use-logic-app-templates.md)來快速上手  
* [檢視所有 hello 可用的連接器](../connectors/apis-list.md)您可以使用邏輯應用程式中
