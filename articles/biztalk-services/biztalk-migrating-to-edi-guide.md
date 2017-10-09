---
title: "aaaMigrating BizTalk Server EDI 方案 tooBizTalk 服務技術指南 |Microsoft 文件"
description: "移轉 EDI tooMABS;Microsoft Azure BizTalk 服務"
services: biztalk-services
documentationcenter: na
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 61c179fa-3f37-495b-8016-dee7474fd3a6
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 34cca3c939a6a7845a860ead6858287000d03ee7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-biztalk-server-edi-solutions-toobiztalk-services-technical-guide"></a>移轉 BizTalk Server EDI 方案 tooBizTalk Services： 技術指南

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

作者：Tim Wieman 和 Nitin Mehrotra

審稿者：Karthik Bharthy

撰寫工具：Microsoft Azure BizTalk 服務 – 2014 年 2 月版本。

## <a name="introduction"></a>簡介
電子資料交換 (EDI) 是其中一個 hello 的商務資料以電子方式交換，也稱為企業對企業 」 或 B2B 交易最普遍的方法。 BizTalk Server 已經支援 EDI 達十年以上，因為 hello 初始 BizTalk Sever 版本。 使用 BizTalk 服務，Microsoft 會持續支援 EDI 解決方案的 hello hello Microsoft Azure 平台上。 B2B 交易大部分外部 tooan 組織，而且因此更容易 tooimplement 雲端平台上實作時。 Microsoft Azure 透過 BizTalk 服務提供這項功能。

雖然某些客戶在 BizTalk 服務視為新 EDI 解決方案的 「 綠地 」 平台，許多客戶會有目前的 BizTalk Server EDI 解決方案，他們可能會想 toomigrate tooAzure。 因為 BizTalk 服務 EDI 架構根據的 hello 相同索引鍵的實體為 BizTalk Server EDI 架構 （交易夥伴、 實體、 協議），它可能 toomigrate BizTalk Server EDI 成品 tooBizTalk 服務。

本文將討論一些 hello 差異與移轉 BizTalk Server EDI 成品 tooBizTalk 相關服務。 本文件假設讀者擁有 BizTalk Server EDI 處理和交易夥伴合約的實用知識。 如需有關 BizTalk Server EDI 的詳細資訊，請參閱 [使用 BizTalk Server 的交易夥伴管理](https://msdn.microsoft.com/library/bb259970.aspx)。

## <a name="which-version-of-biztalk-server-edi-artifacts-can-be-migrated-toobiztalk-services"></a>可以是哪個版本的 BizTalk Server EDI 成品移轉 tooBizTalk 服務？
hello BizTalk Server EDI 模組已大幅增強 BizTalk Server 2010，當它時，已經 tooinclude 夥伴、 設定檔以及協議。 BizTalk 服務會使用 hello 交易夥伴的相同模型 tooorganize hello 和 hello 內那些交易夥伴的商務部門。 如此一來，成品從 BizTalk Server 2010 和更新版本的版本 tooBizTalk 移轉 EDI 服務，更直接轉送程序。 toomigrate EDI 成品相關聯版本先前 tooBizTalk Server 2010，您必須先升級 tooBizTalk Server 2010，然後再將 EDI 成品移轉 tooBizTalk 服務。

## <a name="scenariosmessage-flow"></a>案例/訊息流程
做為 BizTalk Server，BizTalk 服務中的 EDI 處理是使用交易夥伴管理 (TPM) 方案所建置。 hello TPM 方案具有下列主要元件的 hello:

* 交易夥伴，代表 B2B 交易中的組織。
* 設定檔，代表交易夥伴內的部門。
* 交易夥伴協議 （或合約），代表 hello 的商務協議，兩個夥伴/設定檔。

hello 下列圖例顯示 hello 相似之處，以及 BizTalk Server EDI 方案與 BizTalk 服務 EDI 方案之間的差異：

![][EDImessageflow]

hello 的主要差異，並在 BizTalk Server EDI 方案流程之間的相似處，而 BizTalk 服務：

* 如同 BizTalk Server 會使用 EDIReceive 管線 tooreceive EDI 訊息和 EDISend 管線 toosend EDI 訊息，BizTalk 服務會使用 EDI 接收橋接器 tooreceive 和 EDI 傳送橋接器 toosend 出 EDI 訊息。 在 BizTalk Server hello 管線與協議相關聯透過傳送或接收埠。 BizTalk 服務的 hello 協議代表 hello 傳送或接收橋接器。
* 在 BizTalk Server 中，hello EDIReceive 管線處理 hello EDI 訊息後 hello 訊息會是印的 tooa SQL Server 資料庫。 hello EdiSend 管線然後挑選 hello SQL Server 資料庫中的 hello 訊息、 加以處理，並再將它送出 toohello 交易夥伴。
  
    BizTalk 服務的 hello EDI 接收橋接器處理 hello EDI 訊息之後，它會路由傳送 hello 訊息 tooan 外部處理序。 hello 外部處理序無法在 Microsoft Azure 或內部部署上執行。 hello 外部處理序應該路由傳送 hello 訊息 toohello EDI 傳送橋接器;hello 傳送橋接器本質上不提取 hello 訊息。 之後處理 hello 訊息，EDI 傳送橋接器的 hello 會路由傳送 hello 訊息 toohello 交易夥伴。

BizTalk 服務提供方便使用組態經驗 tooquickly 建立及部署 B2B 協議之間沒有設定任何 Microsoft Azure 計算執行個體 （Web 或背景工作角色），交易夥伴、 任何 Microsoft Azure SQL 資料庫或任何Microsoft Azure 儲存體帳戶。 更複雜的案例需要在工作流程或其他服務處理輸入"邊緣 hello 「 交易夥伴協議，也就是交易夥伴協議 EDI 橋接器處理之前或之後。 在詳細資料，hello 下列事件序列發生在 BizTalk 服務中處理 EDI 訊息的期間。

1. 從交易夥伴 Fabrikam 接收 EDI 訊息。  從交易夥伴接收 EDI 訊息，BizTalk 服務可支援傳輸通訊協定，例如 FTP、SFTP、AS2 和 HTTP/S。
2. 交易夥伴協議接收端處理 hello 反組譯 hello EDI 訊息 tooXML 格式。  您可以路由傳送 hello 反組譯 EDI 訊息 （XML 格式） tooService 匯流排端點的服務匯流排轉送端點、 服務匯流排主題、 服務匯流排佇列或 BizTalk 服務橋接器等。
3. hello 分解的 XML 訊息無法然後會收到 hello 端點進行進一步的自訂處理。  無法在內部部署元件或 Microsoft Azure 計算執行個體 toofurther 程序 hello 訊息在 Windows Workflow (WF) 或 Windows Communication Foundation (WCF) 服務中，例如處理這些端點。
4. hello 「 傳送端處理 」 的交易夥伴協議 hello 然後會 hello XML 訊息組合成 EDI 格式，並傳送 tootrading 夥伴 Contoso。  Tootrading 夥伴傳送 EDI 訊息，BizTalk 服務支援的 hello 相同通訊協定與用來接收 EDI 訊息。

本文將進一步提供的概念性指引移轉某些 hello 不同 BizTalk Server EDI 成品 tooBizTalk 服務。

## <a name="sendreceive-ports-tootrading-partners"></a>傳送/接收埠 tooTrading 夥伴
在 BizTalk Server 中設定接收位置與接收埠 tooreceive EDI/XML 訊息從交易夥伴，並設定傳送埠 toosend EDI/XML 訊息 tootrading 夥伴。 您再將繫結這些連接埠 tooa，交易夥伴協議使用 hello BizTalk Server 管理主控台。 在 BizTalk 服務中，您在何處接收來自交易夥伴和您傳送訊息 tootrading 夥伴會設定為交易夥伴協議本身 （做為傳輸設定的一部分） 的 hello 一部分的訊息中的 hello 位置 hello BizTalk 服務入口網站.  因此您實際上沒有 hello 的概念 」 傳送連接埠 」 和 「 接收位置 」 本身，在 BizTalk 服務中。 如需詳細資訊，請參閱 [建立協議](https://msdn.microsoft.com/library/windowsazure/hh689908.aspx)。

## <a name="pipelines-bridges"></a>管線 (橋接器)
在 BizTalk Server EDI 中，管線會是也可以包含自訂邏輯，以特定的處理能力時，所需的 hello 應用程式的訊息處理實體。 BizTalk 服務的對等的 hello 則是 EDI 橋接器。 不過在 BizTalk 服務中，現在請 hello EDI 橋接器是 「 關閉 」。  也就是說，您無法加入您自己的自訂活動 tooan EDI 橋接器。 之前或之後 hello 訊息進入 hello 橋接器設定為 hello 交易夥伴協議的一部分，必須進行任何自訂處理外部應用程式中的 hello EDI 橋接器。 EAI 橋接器已 hello 選項 toodo 自訂處理。 如果您想要自訂處理，您可以使用 EAI 橋接器之前或之後 hello EDI 橋接器處理 hello 訊息。 如需詳細資訊，請參閱[tooInclude 自訂程式碼在橋接器中如何](https://msdn.microsoft.com/library/azure/dn232389.aspx)。

您可以插入發佈/訂閱流程與自訂程式碼和/或使用服務匯流排訊息佇列和主題，交易夥伴協議的 hello 收到 hello 訊息之前或之後 hello 協議處理 hello 訊息，並將其路由 tooa 服務匯流排端點。

請參閱**案例/訊息流程**hello 訊息流程模式本主題中。

## <a name="agreements"></a>合約
如果您已熟悉 BizTalk Server 2010 交易夥伴協議用於 EDI 處理的 hello，然後交易夥伴協議的 BizTalk 服務不會感到陌生。 大部分的設定是 hello 相同的 hello 合約並使用 hello 相同的詞彙。 在某些情況下，hello 協議設定是較簡單的比較的 toohello BizTalk Server 中的相同設定。 Microsoft Azure BizTalk 服務支援 X12、EDIFACT 和 AS2 傳輸。

Microsoft Azure BizTalk 服務也提供**TPM 資料移轉**工具 toomigrate 交易夥伴和協議從 BizTalk Server 交易夥伴模組 tooBizTalk Services 入口網站。 hello TPM 資料移轉工具會提供工具封裝的一部分，其可以從下載 hello [MABS SDK](http://go.microsoft.com/fwlink/p/?LinkId=235057)。 hello 套件也會包含提供指示 toouse hello 工具，以及基本的疑難排解資訊 hello 工具讀我檔案。

## <a name="schemas"></a>結構描述
BizTalk 服務提供可在 BizTalk 服務方案中使用的 EDI 結構描述。  此外，BizTalk Server EDI 結構描述也可用以 BizTalk 服務因為跨 BizTalk Server 與 BizTalk 服務相同 hello hello EDI 結構描述根節點。 因此，您將會是能 toodirectly 需要您的 BizTalk Server EDI 結構描述，在您開發使用 BizTalk 服務的 hello EDI 解決方案中使用它們。 您也可以下載 hello 結構描述從 hello [MABS SDK](http://go.microsoft.com/fwlink/p/?LinkId=235057)。

## <a name="maps-transforms"></a>對應 (轉換)
BizTalk Server 中的對應在 BizTalk 服務中稱為「轉換」。 服務可能是其中一個 BizTalk Server tooBizTalk 中的對應移轉 hello 更複雜的工作 tooachieve （取決於對應複雜性）。 使用 BizTalk 服務的 hello 對應工具會與 hello BizTalk 對應工具不同。 即使 hello 對應程式看起來大部分 hello 相同，hello 基本對應格式不同。 hello 運算質 (稱為**對應作業**BizTalk 服務的) 可用 toohello 使用者也可以使用的不同。  事實上，您無法在 BizTalk 服務中直接使用 BizTalk 對應。 此外，並非所有 BizTalk Server 中可用的 hello 運算質都可用以在 BizTalk 服務中的對應作業。

### <a name="new-transform-operations"></a>新的轉換作業
雖然 hello 可用的轉換對應作業清單似乎與 hello BizTalk Server 對應程式相當不同，BizTalk 服務轉換有 hello 相同工作的完成新的方式。 例如，BizTalk 服務轉換有 **清單作業** 可用。 這不是 hello BizTalk 對應工具中可用。  hello**清單作業**toocreate 可讓您和操作 「 清單 」，清單是一組項目 （也稱為 「 資料列 」），而且每個項目可以有多個成員 （也稱為 「 資料行 」）。  您可以排序 hello 清單中，根據條件、 等等的選取項目。

BizTalk 服務轉換中的新功能的另一個範例是 hello**迴圈作業**。  很難 toocreate 巢狀迴圈 hello BizTalk Server 對應程式中。  因此，hello 迴圈對應作業不會新增 BizTalk 服務轉換 hello。

另一個範例是 hello **If-Then-Else**運算式對應作業。  執行 if-then-其他的作業可以在 hello BizTalk 對應工具，但是它需要多個運算質 tooaccomplish 看似簡單的工作。

### <a name="migrating-biztalk-server-maps"></a>移轉 BizTalk Server 對應
Microsoft Azure BizTalk 服務可提供工具 toomigrate BizTalk Server 對應 tooBizTalk 服務轉換。 hello **BTMMigrationTool**使用一部分 hello**工具**套件提供以 hello [BizTalk 服務 SDK 下載](http://go.microsoft.com/fwlink/p/?LinkId=235057)。 如需 hello 工具的詳細資訊，請參閱[轉換 BizTalk 服務轉換 BizTalk 對應 tooa](https://msdn.microsoft.com/library/windowsazure/hh949812.aspx)。

您也可以查看有 Pereira，BizTalk MVP 的範例上如何太[移轉 BizTalk Server 對應 tooBizTalk 服務轉換](http://social.technet.microsoft.com/wiki/contents/articles/23220.migrating-biztalk-server-maps-to-windows-azure-biztalk-services-wabs-maps.aspx)。

## <a name="orchestrations"></a>協調流程
如果您需要 toomigrate BizTalk Server 協調流程處理 tooMicrosoft Azure，hello 協調流程需要 toobe 重寫，因為 Microsoft Azure 不支援 BizTalk Server 協調流程的執行。  您可以重寫 hello Windows Workflow Foundation 4.0 (WF4) 服務中的協調流程功能。  這會是完全重寫，因為沒有目前無法從 BizTalk Server 協調流程 tooWF4 移轉。 以下是 Windows 工作流程的一些資源：

* [*如何 toointegrate WCF 工作流程服務與 Service Bus 佇列和主題*](https://msdn.microsoft.com/library/azure/hh709041.aspx)由 Paolo Salvatori。 
* [*建置應用程式與 Windows Workflow Foundation 和 Azure*工作階段](http://go.microsoft.com/fwlink/p/?LinkId=237314)hello Build 2011 會議。
* [*Windows Workflow Foundation 開發人員中心*](http://go.microsoft.com/fwlink/p/?LinkId=237315) (位於 MSDN 上)。
* [*Windows Workflow Foundation 4 (WF4) 文件*](https://msdn.microsoft.com/library/dd489441.aspx) (位於 MSDN 上)。

## <a name="other-considerations"></a>其他考量
以下是您在使用 BizTalk 服務時必須考量的一些事項。

### <a name="fallback-agreements"></a>後援合約
BizTalk Server EDI 處理有 「 後援協議 」 的 hello 概念。  到目前為止，BizTalk 服務「沒有」  後援合約的概念。  請參閱 BizTalk 文件集主題[hello 角色的協議 EDI 處理](http://go.microsoft.com/fwlink/p/?LinkId=237317)和[設定全域或後援協議屬性](https://msdn.microsoft.com/library/bb245981.aspx)如需在 BizTalk 中如何使用後援協議的資訊伺服器。

### <a name="routing-toomultiple-destinations"></a>路由 toomultiple 目的地
BizTalk 服務橋接器以其目前狀態不支援路由訊息 toomultiple 目的地使用發行-訂閱模型。 而是從 BizTalk 服務橋接器 tooa 服務匯流排主題，如此即可在多個端點上有多個訂用帳戶 tooreceive hello 訊息的訊息無法路由傳送。

## <a name="conclusion"></a>結論
Microsoft Azure BizTalk 服務會在一般的里程碑 tooadd 更新特性和功能。 每次更新時，我們期待 toosupporting 增加功能 toofacilitate 建立端對端解決方案使用 BizTalk 服務和其他 Azure 的技術。

## <a name="see-also"></a>另請參閱
[使用 Azure 開發企業應用程式](https://msdn.microsoft.com/library/azure/hh674490.aspx)

[EDImessageflow]: ./media/biztalk-migrating-to-edi-guide/IC719455.png
