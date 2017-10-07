---
title: "BizTalk 服務版本中功能的相關 aaaLearn |Microsoft 文件"
description: "比較 hello BizTalk 服務版本的 hello 功能： 釋出，開發人員、 Basic、 Standard 和 Premium。 MABS，WABS。"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: c589629f-06b1-44bb-b8ca-1db71826ea59
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 81626fa743a7190e7c78a0fd90b3054a08982b02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-editions-chart"></a>BizTalk 服務：版本圖表

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Azure BizTalk 服務提供數個版本。 使用這個版本是最適合您案例和商務需求的發行項 toodetermine。

## <a name="compare-hello-editions"></a>比較 hello 版本
**免費 (預覽)**

功能包括建立和管理混合式連線。 輕鬆 tooconnect Azure 網站 tooan 內部部署系統，例如 SQL Server 混合式連接。

**開發人員**

包括混合式連線、EAI 和 EDI 訊息處理與易於使用的交易夥伴管理入口網站、支援一般 EDI 結構描述，以及透過 X12 和 AS2 的豐富 EDI 處理。 建立連接 hello 雲端中的服務與任何 HTTP/S、 REST、 FTP、 WCF 和 SFTP 通訊協定 tooread 常見 EAI 案例，並寫入訊息。  已備妥要使用 SAP、 Oracle eBusiness、 Oracle DB、 Siebel 和 SQL Server 配接器會利用連線 tooon 內部部署 LOB 系統。 在開發人員為主的環境中，使用 Visual Studio 工具輕鬆開發和部署。 有限 toodevelopment 及測試用途只與任何服務等級協定 (SLA)。

**基本**

在混合式連線、 EAI 橋接器、 EDI 協議和 BizTalk Adapter Pack 連接包含大部分的 hello 開發人員功能，會增加。 也提供高可用性和 hello 選項 tooscale 與服務等級協定 (SLA)。

**標準**

混合式連線、 EAI 橋接器、 EDI 協議和 BizTalk Adapter Pack 連接中包含以增加的 hello 基本功能。 也提供高可用性和 hello 選項 tooscale 與服務等級協定 (SLA)。

**高級**

混合式連線、 EAI 橋接器、 EDI 協議和 BizTalk Adapter Pack 連接中包含所有 hello 標準功能，以增加而增加。 也包含保存、 高可用性，與 hello 選項 tooscale 與服務等級協定 (SLA)。

## <a name="editions-chart"></a>版本圖表
hello 下表列出 hello 差異。

<table border="1">
<tr bgcolor="FAF9F9">
        <th></th>
        <th>免費 (預覽)</th>
        <th>開發人員</th>
        <th>基本</th>
        <th>標準</th>
        <th>進階</th>
</tr>

<tr>
<td><strong>起始價格</strong></td>
<td colspan="5"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=304011">Azure BizTalk 服務價格</a> <br/><br/> <a HREF="http://azure.microsoft.com/pricing/calculator/?scenario=full">Azure 價格計算機</a></td>
</tr>
<tr>
<td><strong>預設最小組態</strong></td>
<td>1 個免費單位</td>
<td>1 個開發人員單位</td>
<td>1 個基本單位</td>
<td>1 個標準單位</td>
<td>1 個高級單位</td>
</tr>
<tr>
<td><strong>調整</strong></td>
<td>無調整</td>
<td>無調整</td>
<td>是，增加 1 個基本單位</td>
<td>是，增加 1 個標準單位</td>
<td>是，增加 1 個高級單位</td>
</tr>
<tr>
<td><strong>允許的最大相應放大</strong></td>
<td>無調整</td>
<td>無調整</td>
<td>向上 too8 單位</td>
<td>向上 too8 單位</td>
<td>向上 too8 單位</td>
</tr>
<tr>
<td><strong>每個單位的 EAI 橋接器</strong></td>
<td>未包括</td>
<td>25</td>
<td>25</td>
<td>125</td>
<td>500</td>
</tr>
<tr>
<td><strong>EDI、AS2</strong>
<br/><br/>
包括 TPM 協議</td>
<td>未包括</td>
<td>已包括。 每個單位 10 個協定。</td>
<td>已包括。 每個單位 50 個協定。</td>
<td>已包括。 每個單位 250 個協定。</td>
<td>已包括。 每個單位 1000 個協定。</td>
</tr>
<tr>
<td><strong>每個單位的混合式連線</strong></td>
<td>5</td>
<td>5</td>
<td>10</td>
<td>50</td>
<td>100</td>
</tr>
<tr>
<td><strong>每個單位的混合式連線資料傳輸 (GB)</strong></td>
<td>5</td>
<td>5</td>
<td>50</td>
<td>250</td>
<td>500</td>
</tr>
<tr>
<td><strong>BizTalk Adapter 服務連線 tooon 內部部署 LOB 系統</strong></td>
<td>未包括</td>
<td>1 個連接</td>
<td>2 個連接</td>
<td>5 個連接</td>
<td>25 個連接</td>
</tr>
<tr>
<td align="left"><strong>支援的通訊協定/系統：</strong>
<ul>
<li>HTTP</li>
<li>HTTPS</li>
<li>FTP</li>
<li>SFTP</li>
<li>WCF</li>
<li>服務匯流排 (SB)</li>
<li>Azure Blob</li>
<li>REST API</li>
</ul>
</td>
<td>未包括</td>
<td>已包括</td>
<td>已包括</td>
<td>已包括</td>
<td>已包括</td>
</tr>
<tr>
<td><strong>高可用性</strong>
<br/><br/>
有關服務等級協定 (SLA)，請參閱 <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=304011">Azure BizTalk 服務價格</a>。
</td>
<td>未包括</td>
<td>未包括</td>
<td>已包括</td>
<td>已包括</td>
<td>已包括</td>
</tr>
<tr>
<td><strong>備份與還原</strong></td>
<td>未包括</td>
<td>已包括</td>
<td>已包括</td>
<td>已包括</td>
<td>已包括</td>
</tr>
<tr>
<td><strong>追蹤</strong></td>
<td>未包括</td>
<td>已包括</td>
<td>已包括</td>
<td>已包括</td>
<td>已包括</td>
</tr>
<tr>
<td><strong>封存</strong><br/><br/>
包括收據的不可否認性 (NRR) 和下載追蹤的訊息</td>
<td>未包括</td>
<td>已包括</td>
<td>未包括</td>
<td>未包括</td>
<td>已包括</td>
</tr>
<tr>
<td><strong>使用自訂程式碼</strong></td>
<td>未包括</td>
<td>已包括</td>
<td>已包括</td>
<td>已包括</td>
<td>已包括</td>
</tr>
<tr>
<td><strong>使用轉換，包括自訂 XSLT</strong></td>
<td>未包括</td>
<td>已包括</td>
<td>已包括</td>
<td>已包括</td>
<td>已包括</td>
</tr>
</table>

> [!NOTE]
> 針對硬體故障時的備援能力，高可用性即代表在單一 BizTalk 單位內具有多個 VM。
> 
> 

## <a name="faqs"></a>常見問題集
#### <a name="what-is-a-biztalk-unit"></a>何謂 BizTalk 單位？
「 單位 」 是 Azure BizTalk 服務部署的 hello 不可部分完成的層級。 每個版本都隨附一個具有不同計算容量和記憶體的單位。 例如，基本單位的計算能力超過開發人員、標準的計算能力超過基本，依此類推。 當調整 BizTalk 服務時，您是根據單位調整。

#### <a name="what-is-hello-difference-between-biztalk-services-and-azure-biztalk-vm"></a>Hello BizTalk 服務與 Azure BizTalk VM 之間的差異為何？
BizTalk 服務會提供用於建立 hello 雲端中的整合方案，則為 true 的平台做為服務 (PaaS) 架構。 Hello PaaS 模型中，完全專注 hello 應用程式邏輯並保留所有 hello 基礎結構管理 tooMicrosoft，包括：

* 不是需要 toomanage 或修補程式的虛擬機器。
* Microsoft 確保了可用性。
* 您可以控制視藉由只要求更多或較低容量透過 hello Azure 入口網站的小數位數。

虛擬機器上的 BizTalk 伺服器提供基礎架構即服務 (IaaS) 架構。 您建立虛擬機器，並設定它們完全一樣在內部部署環境中，使其更容易 toorun 現有應用程式沒有變更程式碼的 hello 雲端中。 IaaS，就仍然必須負責 hello 虛擬機器中設定、 管理 hello 虛擬機器 （例如安裝軟體和 OS 修補程式） 和架構而實際 hello 應用程式的高可用性。

如果您正在查看如何組建新的整合方案，以將您的基礎結構管理努力降至最低，請使用 BizTalk 服務。 如果您要尋找 tooquickly 移轉您現有的 BizTalk 方案，或尋找點播環境 toodevelop 和測試 BizTalk Server 應用程式，使用 BizTalk Server 在 Azure 虛擬機器上。

#### <a name="what-is-hello-difference-between-biztalk-adapter-service-and-hybrid-connections"></a>Hello BizTalk Adapter 服務和混合式連線之間的差異為何？
hello BizTalk 配接器服務會使用 Azure BizTalk 服務。 hello BizTalk 配接器服務會使用 hello BizTalk Adapter Pack tooconnect tooan 在內部部署企業營運 (LOB) 系統。 混合式連接提供簡單、 方便的方式 tooconnect 像 hello Azure App Service 中的 Web 應用程式功能的 Azure 應用程式和 Azure 行動服務，tooan 內部資源。

#### <a name="what-does-hybrid-connection-data-transfer-gb-per-unit-mean-is-this-per-minutehourdayweekmonth-what-happens-when-hello-limit-is-reached"></a>「每單位混合式連線資料傳輸 (GB)」代表什麼意思？ 是指每分鐘/小時/日/週/月嗎？ 當到達 hello 限制時，發生什麼事？
hello 混合式連接每單位成本取決於 hello BizTalk 服務版本。 簡言之，成本取決於您傳輸的資料量。 例如，每天傳輸 10 GB 資料的成本低於每天傳輸 100 GB 的成本。 使用 hello[定價計算機](https://azure.microsoft.com/pricing/calculator/?scenario=full)toodetermine 特定成本時，BizTalk 服務。 一般而言，hello 限制會強制執行每日。 如果您超出 hello 限制時，任何超額部分負責速率為每一 GB $1 hello。

#### <a name="when-i-create-an-agreement-in-biztalk-services-why-does-hello-number-of-bridges-go-up-by-two-instead-of-just-one"></a>當我在 BizTalk 服務中建立協議時，為什麼沒有橋接器的 hello 數目向上由兩個，而不是只有一個？
每個協定由兩個不同協定組成，即傳送端通訊橋接器和接收端通訊橋接器。

#### <a name="what-happens-when-i-hit-hello-quota-limit-on-hello-number-of-bridges-or-agreements"></a>我遇到 hello 橋接器或協議的 hello 數目的配額限制時，發生什麼事？
您不能 toodeploy 任何新的橋接器或建立任何新的協議。 toodeploy 更多，您需要 tooscale 向上 hello BizTalk 服務，或更高版本，升級 tooa toomore 單位。

#### <a name="how-do-i-migrate-from-one-tier-of-biztalk-services-tooanother"></a>如何移轉的 BizTalk 服務 tooanother 一層？
hello 免費版本無法移轉或 '向上延展' tooanother 層無法備份和還原 tooanother 層。 如果您需要另一層，建立新的 BizTalk 服務使用 hello 新層。 使用 hello 免費版本，包括需要 toobe 中重新建立混合式連接所建立的任何成品 hello 新的 BizTalk 服務。 

Hello 剩餘的版本中，使用 hello 備份和還原從一層 tooanother 移轉您的成品。 例如，備份您的成品在 hello 標準層次中，然後還原其 toohello Premium 層。 [BizTalk 服務： 備份和還原](biztalk-backup-restore.md)描述 hello 支援的移轉路徑，並列出有哪些成品會備份。 請注意，混合式連線無法備份。 備份和還原 tooa 新的層之後, 您然後重新建立 hello 混合式連線。  

#### <a name="is-hello-biztalk-adapter-service-included-in-hello-service-how-do-i-receive-hello-software"></a>包含在 hello 服務 hello BizTalk Adapter 服務嗎？ 如何收到 hello 軟體？
是，hello BizTalk Adapter 服務以 hello BizTalk Adapter Pack 隨附於 hello Azure BizTalk 服務 SDK[下載](http://www.microsoft.com/download/details.aspx?id=39087)。

## <a name="next-steps"></a>後續步驟
toocreate Azure BizTalk 服務中太 hello Azure 入口網站，移至[BizTalk 服務： 佈建使用 hello Azure 入口網站](biztalk-provision-services.md)。 建立應用程式，請跳過 toostart[Azure BizTalk 服務](http://go.microsoft.com/fwlink/p/?LinkID=235197)。

## <a name="additional-resources"></a>其他資源
* [使用 hello Azure 入口網站佈建 BizTalk 服務：](biztalk-provision-services.md)<br/>
* [BizTalk 服務：佈建狀態圖](biztalk-service-state-chart.md)<br/>
* [BizTalk 服務：儀表板、監視和調整索引標籤](biztalk-dashboard-monitor-scale-tabs.md)<br/>
* [BizTalk Services: Backup and restore](biztalk-backup-restore.md)<br/>
* [BizTalk 服務：節流](biztalk-throttling-thresholds.md)<br/>
* [BizTalk 服務：簽發者名稱和簽發者金鑰](biztalk-issuer-name-issuer-key.md)<br/>
* [開始使用我要如何 hello Azure BizTalk 服務 SDK](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>

