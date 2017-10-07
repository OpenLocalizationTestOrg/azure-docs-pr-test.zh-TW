---
title: "在 Azure 記錄分析的分析解決方案 aaaDNS |Microsoft 文件"
description: "設定並使用記錄分析 toogather 深入了解安全性、 效能和作業上的 DNS 基礎結構中的 hello DNS 分析解決方案。"
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f44a40c4-820a-406e-8c40-70bd8dc67ae7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.openlocfilehash: be7982c54b65ba0c4b1c15ae7516d02eced313f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="gather-insights-about-your-dns-infrastructure-with-hello-dns-analytics-preview-solution"></a>收集深入了解您的 DNS 基礎結構，以 hello DNS 分析預覽方案

![DNS 分析符號](./media/log-analytics-dns/dns-analytics-symbol.png)

本文說明向上 tooset 並用 hello Azure Log Analytics toogather 深入了解安全性、 效能和作業上的 DNS 基礎結構中的 Azure DNS 分析解決方案。

DNS 分析可協助您︰

- 識別用戶端，再試一次 tooresolve 惡意的網域名稱。
- 指出過時的資源記錄。
- 指出經常查詢的網域名稱和 Talkative DNS 用戶端。
- 檢視 DNS 伺服器上的要求負載。
- 檢視動態 DNS 註冊失敗。

hello 方案會收集、 分析，並將相互關聯的 Windows DNS 分析和稽核記錄和其他相關的資料，從您的 DNS 伺服器。

## <a name="connected-sources"></a>連接的來源

hello 下表描述此解決方案所支援的 hello 連接來源：

| **連線的來源** | **支援** | **說明** |
| --- | --- | --- |
| [Windows 代理程式](log-analytics-windows-agents.md) | 是 | hello 方案會從 Windows 代理程式收集 DNS 資訊。 |
| [Linux 代理程式](log-analytics-linux-agents.md) | 否 | hello 解決方案不會收集從直接 Linux 代理程式的 DNS 資訊。 |
| [System Center Operations Manager 管理群組](log-analytics-om-agents.md) | 是 | hello 方案會從已連線的 Operations Manager 管理群組中的代理程式收集 DNS 資訊。 不需要從 hello Operations Manager 代理程式 toohello Operations Management Suite 的直接連接。 從 hello 管理群組 toohello Operations Management Suite 儲存機制，就會轉送資料。 |
| [Azure 儲存體帳戶](log-analytics-azure-storage.md) | 否 | Hello 方案不使用 azure 儲存體。 |

### <a name="data-collection-details"></a>資料收集詳細資料

hello 方案 DNS 清查和 DNS 事件相關的資料從伺服器中收集 hello DNS 記錄分析代理程式安裝。 然後上傳 tooLog 分析和 hello 方案儀表板中顯示這項資料。 清查相關的資料，例如 DNS 伺服器、 區域和資源記錄的 hello 數目會收集執行 hello DNS PowerShell cmdlet。 hello 資料會更新一次每兩天。 hello 相關的事件從收集的資料接近即時 hello[分析和稽核記錄檔](https://technet.microsoft.com/library/dn800669.aspx#enhanc)提供增強的 DNS 記錄和 Windows Server 2012 R2 中的診斷功能。

## <a name="configuration"></a>組態

使用下列資訊 tooconfigure hello 解決方案 hello:

- 您必須擁有[Windows](log-analytics-windows-agents.md)或[Operations Manager](log-analytics-om-agents.md)想 toomonitor 每部 DNS 伺服器上的代理程式。
- 您可以從 hello 加入 hello DNS 分析方案 tooyour Operations Management Suite 工作區[Azure Marketplace](https://aka.ms/dnsanalyticsazuremarketplace)。 您也可以使用 hello 程序中所述[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。

hello 方案會開始收集資料，而不需要再做進一步設定 hello。 不過，您可以使用下列組態 toocustomize 資料集合的 hello。

### <a name="configure-hello-solution"></a>設定 hello 解決方案

在 [hello 方案儀表板上按一下**組態**tooopen hello DNS 分析組態] 頁面。 您可以進行兩種類型的組態變更︰

- **列入白名單的網域名稱**。 hello 解決方案不會處理所有的 hello 查閱查詢。 它會維護一份網域名稱尾碼的白名單。 toohello 符合此白名單中的網域名稱尾碼的網域名稱解析的 hello 查閱查詢不會處理 hello 方案。 未處理在允許清單中網域名稱，可幫助傳送 tooLog 分析 toooptimize hello 資料。 hello 預設允許清單包含常用的公用網域名稱，例如 www.google.com 和 www.facebook.com。您可以捲動檢視 hello 完成的預設清單。

 您可以修改 hello 清單 tooadd 想 tooview 查閱 insights 的任何網域名稱尾碼。 您也可以移除不想 tooview 查閱 insights 的任何網域名稱尾碼。

- **Talkative 用戶端閾值**。 針對以 hello 反白顯示 hello 的查閱要求數目超過 hello 臨界值的 DNS 用戶端**DNS 用戶端**刀鋒視窗。 hello 預設閾值是 1000。 您可以編輯 hello 臨界值。

    ![列入白名單的網域名稱](./media/log-analytics-dns/dns-config.png)

## <a name="management-packs"></a>管理組件

如果您使用 hello Microsoft Monitoring Agent tooconnect tooyour Operations Management Suite 工作區，hello 下列管理組件會安裝：

- Microsoft DNS 資料收集器智慧套件 (Microsft.IntelligencePacks.Dns)

如果您的 Operations Manager 管理群組連線的 tooyour Operations Management Suite 工作區，hello 下列管理組件會安裝在 Operations Manager 時將方案加入。 這些管理組件不需要任何組態或維護：

- Microsoft DNS 資料收集器智慧套件 (Microsft.IntelligencePacks.Dns)
- Microsoft System Center Advisor DNS 分析組態 (Microsoft.IntelligencePack.Dns.Configuration)

如需有關解決方案管理組件的更新方式的詳細資訊，請參閱[Operations Manager 連線 tooLog 分析](log-analytics-om-agents.md)。

## <a name="use-hello-dns-analytics-solution"></a>使用 hello DNS 分析解決方案

本章節將說明所有 hello 儀表板函式以及 toouse 它們。

加入 hello 方案 tooyour 工作區之後，在 hello Operations Management Suite 概觀 頁面上的 hello 方案磚會提供您的 DNS 基礎結構的簡短摘要。 它包含 hello 收集 hello 資料位置的 DNS 伺服器的數目。 它也包含 hello 提出用戶端 tooresolve 惡意中網域 hello 過去 24 小時內的要求數目。 當您按一下 hello 磚時，hello 方案儀表板隨即開啟。

![DNS 分析圖格](./media/log-analytics-dns/dns-tile.png)

### <a name="solution-dashboard"></a>解決方案儀表板

hello 方案儀表板會顯示摘要的資訊 hello hello 解決方案的各種功能。 它也包含連結 toohello 詳細鑑識分析和診斷檢視。 根據預設，hello 資料會顯示 hello 過去七天。 您可以變更 hello 日期和時間範圍使用 hello**日期時間選擇控制項**hello 下列影像所示：

![時間選取控制項](./media/log-analytics-dns/dns-time.png)

hello 方案儀表板會顯示下列刀鋒視窗的 hello:

**DNS 安全性**。 報表 hello 嘗試 toocommunicate 與惡意網域的 DNS 用戶端。 藉由使用 Microsoft threat intelligence 摘要，DNS 分析可偵測用戶端嘗試 tooaccess 惡意網域的 Ip。 在許多情況下，惡意程式碼感染的裝置 」 撥出 「 toohello"命令和控制 」 center hello 所解決的惡意網域的 hello 惡意程式碼的網域名稱。

![[DNS 安全性] 刀鋒視窗](./media/log-analytics-dns/dns-security-blade.png)

當您按一下 hello 清單中的用戶端 IP 時，記錄搜尋會開啟，並顯示 hello 個別查詢的 hello 查閱詳細資料。 在下列範例的 hello，DNS 分析偵測到 hello 通訊透過[IRCbot](https://www.microsoft.com/security/portal/threat/encyclopedia/entry.aspx?Name=Win32/IRCbot):

![顯示 ircbot 的記錄搜尋結果](./media/log-analytics-dns/ircbot.png)

hello 資訊可協助您 tooidentify:

- 用戶端起始 hello 通訊的 IP。
- 解析 toohello 惡意 IP 的網域名稱。
- Hello 網域名稱解析成 IP 位址。
- 惡意 IP 位址。
- Hello 問題的嚴重性。
- 將列入黑名單 hello 惡意 IP 的原因。
- 偵測時間。

**查詢的網域**。 提供 hello 由您的環境中的 hello DNS 用戶端正在查詢最常出現網域名稱。 您可以檢視所有的 hello 網域名稱，查詢的 hello 清單。 您可以也向下鑽研到特定的網域名稱在記錄搜尋中的 hello 查閱要求詳細資料。

![[查詢的網域] 刀鋒視窗](./media/log-analytics-dns/domains-queried-blade.png)

**DNS 用戶端**。 報表 hello 用戶端*違反 hello 閾值*hello 選時段中的查詢數目。 您可以檢視 hello 清單的所有 hello DNS 用戶端以及由它們在記錄搜尋中的 hello 查詢 hello 詳細資料。

![[DNS 用戶端] 刀鋒視窗](./media/log-analytics-dns/dns-clients-blade.png)

**動態 DNS 註冊**。 報告名稱註冊失敗。 位址的所有註冊失敗[資源記錄](https://en.wikipedia.org/wiki/List_of_DNS_record_types)（類型 A 和 AAAA） 會反白顯示 hello 用戶端提出 hello 註冊要求的 Ip。 然後，您可以使用此資訊 toofind hello 失敗的根本原因 hello 註冊依照下列步驟：

1. 尋找嘗試 tooupdate hello 區域 hello 用戶端的 hello 名稱的授權。

2. 使用 hello 方案 toocheck hello 清查資訊該區域。

3. Hello 區域為啟用，請確認該 hello 動態更新。

4. 檢查 hello 區域是否設定為安全動態更新與否。

    ![[動態 DNS 註冊] 刀鋒視窗](./media/log-analytics-dns/dynamic-dns-reg-blade.png)

**名稱註冊要求**。 hello 上方磚會顯示成功和失敗的 DNS 動態更新要求的趨勢線。 hello 較低的磚會列出傳送失敗的 DNS 更新要求 toohello DNS 伺服器，請依照 hello 失敗次數的 hello 前 10 個用戶端。

![[名稱註冊要求] 刀鋒視窗 ](./media/log-analytics-dns/name-reg-req-blade.png)

**範例 DDI 分析查詢**。 包含一份 hello 最常見的搜尋查詢直接擷取未經處理的分析資料。

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![範例查詢](./media/log-analytics-dns/queries.png)

您可以使用這些查詢做為起點，建立自己的查詢以供自訂報告。 hello 查詢連結 toohello DNS 分析記錄搜尋 頁面會顯示結果：

- **DNS 伺服器清單**。 顯示所有 DNS 伺服器的清單，包含其相關聯的 FQDN、網域名稱、樹系名稱和伺服器的 IP。
- **DNS 區域清單**。 顯示 hello 相關聯的區域名稱、 與動態更新狀態、 名稱伺服器，DNSSEC 簽署狀態的所有 DNS 區域的清單。
- **未使用的資源記錄**。 顯示所有 hello 未使用/過時資源記錄的清單。 此清單包含 hello 資源記錄名稱、 資源記錄類型、 相關聯的 hello DNS 伺服器，記錄的產生時間和區域名稱。 您可以使用此清單 tooidentify hello DNS 資源記錄便無法再使用中。 根據這項資訊，您可以移除這些項目從 hello DNS 伺服器。
- **DNS 伺服器查詢負載**。 顯示資訊，以便讓您可以取得檢視方塊的 hello DNS 載入您的 DNS 伺服器上。 這項資訊可協助您規劃 hello 伺服器 hello 容量。 您可以移 toohello**度量**toochange hello 檢視 tooa 圖形視覺效果 索引標籤。 這個檢視可協助您了解如何 hello DNS 負載分散您的 DNS 伺服器。 它會顯示每部伺服器的 DNS 查詢速率趨勢。

    ![DNS 伺服器查詢記錄搜尋結果](./media/log-analytics-dns/dns-servers-query-load.png)

- **DNS 區域的查詢負載**。 Hello hello 解決方案所管理的 DNS 伺服器上會顯示 hello hello 的所有區域的 DNS 區域-查詢-秒統計資料。 按一下 hello**度量**toochange hello hello 結果的詳細的記錄 tooa 圖形視覺化檢視 索引標籤。
- **設定事件**。 顯示所有 hello DNS 設定變更事件和相關聯的訊息。 您可以篩選時間 hello 事件，事件識別碼、 DNS 伺服器，根據這些事件或工作分類。 hello 資料可協助您在特定時間稽核所做的變更 toospecific DNS 伺服器。
- **DNS 分析記錄**。 Hello 解決方案管理的所有 hello DNS 伺服器上會顯示所有的 hello 分析事件。 然後，您可以篩選時間 hello 事件，事件識別碼、 DNS 伺服器，進行 hello 查閱查詢和查詢類型的工作類別目錄的用戶端 IP 根據這些事件。 DNS 伺服器分析事件可讓追蹤 hello DNS 伺服器上的活動。 每次 hello 伺服器傳送或接收 DNS 資訊時，會記錄分析的事件。

### <a name="search-by-using-dns-analytics-log-search"></a>使用 DNS 分析記錄搜尋來搜尋

在 hello 記錄搜尋 頁面上，您可以建立查詢。 您可以使用 facet 控制項來篩選搜尋結果。 您也可以建立進階的查詢 tootransform、 篩選和報告結果。 使用下列查詢的 hello 啟動：

1. 在 hello**搜尋查詢方塊**，型別`Type=DnsEvents`tooview 所有 hello hello hello 解決方案管理的 DNS 伺服器所產生的 DNS 事件。 hello 結果清單 hello 記錄資料的所有事件相關的 toolookup 查詢、 動態的註冊和組態變更。

    ![DnsEvents 記錄搜尋](./media/log-analytics-dns/log-search-dnsevents.png)  

    a. 查閱查詢 tooview hello 記錄資料選取**LookUpQuery**為 hello**子型別**從左邊 hello hello facet 控制篩選器。 列出所有 hello 查閱查詢事件所選的時段的資料表會顯示。

    b. 選取之動態註冊，tooview hello 記錄資料**DynamicRegistration**為 hello**子型別**從左邊 hello hello facet 控制篩選器。 列出所有 hello 動態登錄事件 hello 選的時段的資料表會顯示。

    c. tooview hello 記錄資料，組態變更，選取**ConfigurationChange**為 hello**子型別**從左邊 hello hello facet 控制篩選器。 列出所有選取的時間週期的 hello 組態變更事件的資料表會顯示。

2. 在 hello**搜尋查詢方塊**，型別`Type=DnsInventory`tooview 所有 hello hello hello 解決方案管理的 DNS 伺服器的 DNS 清查相關資料。 hello 結果清單 hello DNS 伺服器、 DNS 區域與資源記錄的記錄資料。

    ![DnsInventory 記錄搜尋](./media/log-analytics-dns/log-search-dnsinventory.png)

## <a name="feedback"></a>意見反應

提供意見反應的方式有兩種：

- **UserVoice**. 張貼想法 DNS 分析功能 toowork 上。 請瀏覽 hello [Operations Management Suite 的 UserVoice 網頁](https://aka.ms/dnsanalyticsuservoice)。
- **加入我們的行列**。 我們有興趣一律擁有新客戶加入我們 cohorts tooget 早期存取 toonew 功能，協助我們改善 DNS 分析。 如果您想加入我們的行列，請填妥這份[快速問卷調查 (英文)](https://aka.ms/dnsanalyticssurvey)。

## <a name="next-steps"></a>後續步驟

[搜尋記錄](log-analytics-log-searches.md)tooview 詳細記錄的 DNS 記錄。
