---
title: "分析資料安全性 aaaLog |Microsoft 文件"
description: "深入了解 Log Analytics 如何保護您的隱私權和保護您的資料安全。"
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: a33bb05d-b310-4f2c-8f76-f627e600c8e7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: magoedte
ms.openlocfilehash: 130b59f22fc3dd249f32717367cc62ea25c55a21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-data-security"></a>Log Analytics 資料安全性
Microsoft 是 tooprotecting 認可您的隱私權和保護您的資料，同時提供軟體和服務，幫助您管理 hello 貴組織的 IT 基礎結構。 我們辨識時委託資料 tooothers 時，該信任需要嚴格的安全性。 Microsoft 遵守 toostrict 相容性與安全性指導方針 — 從 toooperating 服務撰寫程式碼。

保全和保護資料在 Microsoft 是第一要務。 有任何問題、 建議或關於下列資訊，包括我們的安全性原則的 hello 任一問題與我們連絡[Azure 支援選項](http://azure.microsoft.com/support/options/)。

本文說明如何收集、 處理以及受到 hello Operations Management Suite (OMS) 中的記錄分析資料。 您可以使用代理程式 tooconnect toohello web 服務、 使用 System Center Operations Manager toocollect 操作資料，或從以供記錄分析 Azure 診斷擷取資料。 hello 收集的資料會透過傳送嗨網際網路使用憑證型驗證和 SSL 3 toohello 記錄分析服務，這裝載於 Microsoft Azure。 資料壓縮 hello 代理程式所傳送之前。

hello 記錄分析服務會管理雲端架構資料安全地使用下列方法的 hello:

* 資料隔離
* 資料保留
* 實體安全性
* 事件管理
* 法規遵循
* 安全性標準認證

## <a name="data-segregation"></a>資料隔離
客戶資料的各個元件 hello OMS 服務是以邏輯方式分開。 每個組織加上標記的所有資料。 這項標記作業在整個 hello 資料生命週期持續發生，它會強制執行各種層級的 hello 服務。 每個客戶都有專用的 Azure blob 可裝載長期資料的 hello

## <a name="data-retention"></a>資料保留
索引的記錄檔搜尋資料會儲存並保留相應 tooyour 定價計劃。 如需詳細資訊，請參閱 [Log Analytics 定價](https://azure.microsoft.com/pricing/details/log-analytics/)。

Microsoft 會刪除客戶資料在關閉 hello OMS 工作區之後的 30 天。 Microsoft 也會刪除 hello hello 資料所在的 Azure 儲存體帳戶。 移除客戶資料時，不會終結任何實體磁碟機。

hello 下表列出了一些 hello OMS 中可用的解決方案和範例 hello 它們所收集的資料類型。

| **方案** | **資料類型** |
| --- | --- |
| 組態評估 |組態資料、中繼資料及狀態資料 |
| 容量規劃 |效能資料和中繼資料 |
| 反惡意程式碼 |組態資料和中繼資料 |
| 系統更新評估 |中繼資料和狀態資料 |
| 記錄檔管理 |使用者定義的事件記錄檔、Windows 事件記錄檔和/或 IIS 記錄檔 |
| 變更追蹤 |軟體清查和 Windows 服務中繼資料 |
| SQL 和 Active Directory 評估 |WMI 資料、登錄資料、效能資料和 SQL Server 動態管理檢視結果 |

hello 下表顯示資料類型的範例：

| **資料類型** | **欄位** |
| --- | --- |
| 警示 |警示名稱、警示描述、BaseManagedEntityId、問題識別碼、IsMonitorAlert、RuleId、ResolutionState、優先順序、嚴重性、分類、擁有者、ResolvedBy、TimeRaised、TimeAdded、LastModified、LastModifiedBy、LastModifiedExceptRepeatCount、TimeResolved、TimeResolutionStateLastModified、TimeResolutionStateLastModifiedInDB、RepeatCount |
| 組態 |CustomerID、AgentID、EntityID、ManagedTypeID、ManagedTypePropertyID、CurrentValue、ChangeDate |
| Event |EventId、EventOriginalID、BaseManagedEntityInternalId、RuleId、PublisherId、PublisherName、FullNumber、Number、Category、ChannelLevel、LoggingComputer、EventData、EventParameters、TimeGenerated、TimeAdded <br>**注意：**當您撰寫使用自訂欄位的事件 toohello Windows 事件記錄檔中時，OMS 會加以收集。 |
| 中繼資料 |BaseManagedEntityId、ObjectStatus、OrganizationalUnit、ActiveDirectoryObjectSid、PhysicalProcessors、NetworkName、IPAddress、ForestDNSName、NetbiosComputerName、VirtualMachineName、LastInventoryDate、HostServerNameIsVirtualMachine、IP 位址、NetbiosDomainName、LogicalProcessors、DNSName、DisplayName、DomainDnsName、ActiveDirectorySite、PrincipalName、OffsetInMinuteFromGreenwichTime |
| 效能 |ObjectName、CounterName、PerfmonInstanceName、PerformanceDataId、PerformanceSourceInternalID、SampleValue、TimeSampled、TimeAdded |
| 狀況 |StateChangeEventId、StateId、NewHealthState、OldHealthState、Context、TimeGenerated、TimeAdded、StateId2、BaseManagedEntityId、MonitorId、HealthState、LastModified、LastGreenAlertGenerated、DatabaseTimeModified |

## <a name="physical-security"></a>實體安全性
在 OMS 服務的 hello 記錄分析由 Microsoft 人員操作，並會記錄所有活動，並且可供稽核。 hello 服務會完全在 Azure 中執行，並符合 Azure 通用工程準則 hello。 您可以 hello 第 18 頁檢視 Azure 資產 hello 實體安全性的詳細[Microsoft Azure 安全性概觀](http://download.microsoft.com/download/6/0/2/6028B1AE-4AEE-46CE-9187-641DA97FC1EE/Windows%20Azure%20Security%20Overview%20v1.01.pdf)。 實體的存取權限 toosecure 區域會變更一個工作天內，也不再有責任 hello OMS 服務，包括傳送和終止的人。 您可以閱讀 hello 全域實體基礎結構我們在使用[Microsoft 資料中心](https://www.microsoft.com/en-us/server-cloud/cloud-os/global-datacenters.aspx)。

## <a name="incident-management"></a>事件管理
OMS 具備所有 Microsoft 服務都會遵守的事件管理程序。 toosummarize，我們：

* 使用共同的責任模型一部分安全性責任所屬 tooMicrosoft 和部分所屬 toohello 客戶
* 管理 Azure 安全性事件
  * 在偵測到事件時啟動調查
  * 評估 hello 影響，以及在呼叫事件回應小組成員將事件的嚴重性。 根據辨識項，hello 評估可能或可能不會導致進一步擴大 toohello 安全性回應小組。
  * 安全性回應專家 tooconduct hello 技術或鑑識調查診斷事件，必須識別內含項目、 降低及因應措施的策略。 如果 hello 安全性團隊認為客戶資料可能會非法或未經授權的公開的 tooan 個別的平行執行的 hello 客戶事件通知處理程序同時開始。  
  * 穩定，並從 hello 事件復原。 hello 事件回應小組建立復原計劃 toomitigate hello 問題。 隔離受影響系統之類的危機圍堵步驟可能會立即進行，與診斷並行。 較長的詞彙緩和措施可能必須規劃 hello 立即風險過後，會發生。  
  * 關閉 hello 事件，然後進行事後。 hello 事件回應小組建立概述 hello 詳細資料的 hello 事後事件，hello 意圖 toorevise 原則、 程序，與處理程序 tooprevent hello 事件的循環。
* 通知客戶發生了安全性事件
  * 判斷受影響的客戶和 tooprovide hello 範圍詳細通知，儘可能會受到影響的任何人
  * 建立通知 tooprovide 客戶具有夠詳細資訊，以便他們可以進行調查，對其結束和符合任何 tootheir 使用者時不會過度延遲 hello 通知處理程序所做的承諾。
  * 確認，並宣告 hello 事件，視需要。
  * 在不會導致不合理延遲並符合法律或契約承諾的情況下，以事件通知告知客戶。 安全性事件的通知會透過任何方式 Microsoft select 中，包括透過電子郵件傳遞 tooone 或多個客戶的系統管理員。
* 進行小組準備及訓練
  * Microsoft 人員會需要的 toocomplete 安全性和認知定型，可協助他們 tooidentify 和可能的安全性問題的報表。  
  * Hello Microsoft Azure 服務使用的運算子具有的加法訓練義務周圍存取 toosensitive 系統裝載客戶資料。
  * Microsoft 安全性回應人員獲得專門針對其角色的訓練

如果發生客戶資料遺失事件，我們會在一天內通知每位客戶。 不過，OMS 從未發生過客戶資料遺失。 此外，我們會複製所建立的資料並分散於各地。

如需 Microsoft 如何回應 toosecurity 事件的詳細資訊，請參閱[hello 雲端中的 Microsoft Azure 安全性回應](https://gallery.technet.microsoft.com/Azure-Security-Response-in-dd18c678/file/150826/1/Microsoft Azure Security Response in hello cloud.pdf)。

## <a name="compliance"></a>法規遵循
hello OMS 軟體開發和服務小組的資訊安全和控管程式支援其商務需求，並依照遵守 toolaws 出口法規之限制[Microsoft Azure 信任中心](https://azure.microsoft.com/support/trust-center/)和[Microsoft 信任中心的相容性](https://www.microsoft.com/en-us/TrustCenter/Compliance/default.aspx)。 上述位置也會描述 OMS 是如何建立安全性需求、識別安全性控制，以及管理和監視風險。 每年我們都會檢閱原則、標準、程序和指導方針。

每個 OMS 開發小組成員都會獲得正式的應用程式安全性訓練。 在內部，我們使用版本控制系統來開發軟體。 每個軟體專案受到 hello 版本控制系統。

Microsoft 備有會監看及評估 Microsoft 中所有服務的安全性和法規遵循小組。 資訊安全人員組成 hello 小組，他們不會產生關聯以 hello 工程部門開發 OMS。 hello 安全人員具有自己管理鏈結，並進行獨立的產品和服務 tooensure 安全性與相容性評估。

Microsoft 的董事會會收到有關 Microsoft 所有資訊安全程式的年度報表通知。

hello OMS 軟體開發和服務小組會積極地與 hello Microsoft 法律和規範小組及其他產業合作夥伴 tooacquire 各種不同的認證。

## <a name="certifications-and-attestations"></a>認證和證明
OMS 記錄分析會符合下列需求的 hello:

* [ISO/IEC 27001](http://www.iso.org/iso/home/standards/management-standards/iso27001.htm)
* [ISO/IEC 27018:2014](http://www.iso.org/iso/home/store/catalogue_tc/catalogue_detail.htm?csnumber=61498)
* [ISO 22301](https://azure.microsoft.com/en-us/blog/iso22301/)
* [付款卡產業 （PCI 相容） 資料安全標準 (PCI DSS)](https://www.microsoft.com/en-us/TrustCenter/Compliance/PCI)由 hello PCI 安全性標準委員會 （英文)。
* [服務組織控制 (SOC) 1 類型 1 和 SOC 2 類型 1](https://www.microsoft.com/en-us/TrustCenter/Compliance/SOC1-and-2) 相容
* 擁有 HIPAA 商業夥伴合約之公司的 [HIPAA 和 HITECH](https://www.microsoft.com/en-us/TrustCenter/Compliance/HIPAA)
* Windows 通用工程準則
* Microsoft 高可信度電腦運算 (英文)
* 作為 Azure 服務，OMS 會使用的 hello 元件會遵守 tooAzure 法規遵循需求。 若要深入了解，請前往 [Microsoft 信任中心法規遵循](https://www.microsoft.com/en-us/TrustCenter/Compliance/default.aspx)。

> [!NOTE]
> 在某些認證/證明中，Log Analytics 會以舊名稱 *Operational Insights* 列出。
>
>


## <a name="cloud-computing-security-data-flow"></a>雲端運算安全性資料流程
hello 圖的雲端安全性架構 hello 資料流的資訊從您的公司以及如何受到保護原狀移 toohello 記錄分析服務，最後 hello OMS 入口網站中看到您。 Hello 圖表後面詳述每個步驟的詳細資訊。

![OMS 資料收集與安全性的影像](./media/log-analytics-security/log-analytics-security-diagram.png)

## <a name="1-sign-up-for-log-analytics-and-collect-data"></a>1.註冊使用 Log Analytics 並收集資料
針對您的組織 toosend 資料 tooLog 分析，您可以設定 Windows 代理程式，在 Azure 虛擬機器或 OMS 代理程式上執行適用於 Linux 代理程式。 如果您使用 Operations Manager 代理程式，則您可以使用設定精靈在 hello Operations 主控台 tooconfigure 它們。 使用者 （這可能是您、 其他個別使用者或一群人） 建立一個或多個 OMS 帳戶 （OMS 工作區），並使用其中一個 hello 下列帳戶來註冊代理程式：

* [組織識別碼](../active-directory/sign-up-organization.md)
* [Microsoft 帳戶 - Outlook、Office Live、MSN](http://www.microsoft.com/account/default.aspx)

OMS 工作區是資料收集、彙總、分析以及呈現的位置。 成 toopartition 資料的表示，主要使用工作區和每個工作區是唯一的。 比方說，您可能會想的 toohave 實際執行資料管理的其中一個使用另一個工作區管理 OMS 工作區與測試資料。 工作區也會協助系統管理員控制使用者存取 toohello 資料。 每個工作區可以有多個與其關聯的使用者帳戶，每個使用者帳戶可以存取多個 OMS 工作區。 您必須根據資料中心區域建立工作區。 每個工作區是在 hello 區域中，主要用於 OMS 服務可用性的複寫的 tooother 資料中心。

Operations Manager 的 hello 組態精靈完成時，每個 Operations Manager 管理群組會建立與 hello 記錄分析服務的連線。 然後，您可以使用在 hello 新增電腦精靈 toochoose toosend 資料 toohello 服務允許 hello 管理群組中的哪些電腦。 對於其他代理程式類型，每個安全地連接 toohello OMS 服務。

已連線的系統與 hello 記錄分析服務之間的所有通訊都會都加密。  hello (HTTPS) 通訊協定會使用 TLS 進行加密。  hello Microsoft SDL 程序會遵循 tooensure 記錄分析是最新的密碼編譯通訊協定中的 hello 最近進階功能。

會收集 Log Analytics 資料的每個類型代理程式。 hello 收集的資料類型就會根據使用的解決方案 hello 類型。 您可以看到資料集合中的摘要[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。 此外，大部分方案都會有更詳細的集合資訊。 解決方案是預先定義的檢視、記錄搜尋查詢、資料收集規則，以及處理邏輯的組合。 只有系統管理員可以使用記錄分析 tooimport 方案。 匯入 hello 解決方案之後，它是移動的 toohello Operations Manager 管理伺服器 （如果使用），然後您所選擇的 tooany 代理程式。 之後，hello 代理程式收集 hello 資料。

## <a name="2-send-data-from-agents"></a>2.從代理程式傳送資料
您註冊使用註冊金鑰的所有代理程式類型和 hello 代理程式和使用憑證型驗證和 SSL 使用連接埠 443 的 hello 記錄分析服務之間建立安全的連線。 OMS 會使用密碼存放區 toogenerate 並維護金鑰。 私用金鑰會循環每隔 90 天，以及儲存在 Azure 中，與 hello Azure 所管理遵循嚴格的法規和相容性做法的作業。

使用 Operations Manager，您註冊工作區與 hello 記錄分析服務，並且 hello Operations Manager 管理伺服器之間建立安全的 HTTPS 連線。

對於 Azure 虛擬機器上執行的 Windows 代理程式，唯讀的儲存體金鑰是使用的 tooread Azure 資料表中的診斷事件。

如果任何代理程式無法 toocommunicate toohello 服務因為任何原因，hello 收集的資料儲存在暫時快取，而且 hello 管理伺服器會嘗試 tooresend hello 資料兩小時內每 8 分鐘。 hello 代理程式的快取的資料受到 hello 作業系統的認證存放區。 如果 hello 服務無法處理 hello 資料在兩個小時後，hello 代理程式會將佇列 hello 資料。 如果 hello 佇列已滿，OMS 會開始卸除的資料類型，從開始效能資料。 hello 代理程式佇列限制是登錄機碼，因此您可以修改它，如有必要。 收集的資料壓縮，然後傳送 toohello 服務，而略過內部部署資料庫，因此不會新增任何負載 toothem。 Hello 收集後資料會傳送，會從 hello 快取中移除。

如上面所述，從您的代理程式的資料會透過 SSL tooMicrosoft Azure 資料中心中傳送。 （選擇性） 您可以使用 ExpressRoute tooprovide 額外的安全性 hello 資料。 ExpressRoute 是方式 toodirectly 連接 tooAzure 從現有的 WAN 網路，例如多重通訊協定標籤交換 (MPLS) VPN，網路服務提供者所提供。 如需詳細資訊，請參閱 [ExpressRoute](https://azure.microsoft.com/services/expressroute/)。

## <a name="3-hello-log-analytics-service-receives-and-processes-data"></a>3.hello 記錄分析服務接收和處理資料
hello 記錄分析服務會確保內送資料是來自受信任的來源驗證憑證與使用 Azure 驗證 hello 資料完整性。 hello 未處理的原始資料會儲存為中的 blob [Microsoft Azure 儲存體](../storage/common/storage-introduction.md)且未加密。 不過，每個 Azure 儲存體 blob 會有一組的唯一索引鍵集中，可存取的只有 toothat 使用者。 hello 的類型儲存的資料取決於 hello 類型已匯入和使用 toocollect 資料的解決方案。 然後，hello 記錄分析服務會處理 hello Azure 儲存體 blob 的 hello 未經處理資料。

## <a name="4-use-log-analytics-tooaccess-hello-data"></a>4.使用記錄分析 tooaccess hello 資料
您可以使用 hello 組織帳戶或您先前設定的 Microsoft 帳戶，就可登入 tooLog 分析 hello OMS 入口網站中。 在 OMS 中的記錄分析 hello OMS 入口網站之間的所有流量會透過安全 HTTPS 通道都傳送。 當使用 hello OMS 入口網站時，工作階段識別碼所產生的 hello 使用者用戶端 （web 瀏覽器） 和資料會儲存在本機快取，直到 hello 工作階段已終止。 當終止時，會刪除 hello 快取。 未包含個人識別資訊的用戶端 Cookie 不會自動移除。 工作階段 Cookie 會標示為 HTTPOnly，並受到保護。 預先決定的閒置時間後 hello OMS 入口網站工作階段已終止。

使用 hello OMS 入口網站，您可以匯出資料 tooa CSV 檔案，而且您可以存取使用搜尋 Api 的資料。 CSV 匯出有限的 too50，每個匯出和 API 資料 000 資料列，則受限制的 too5，每一搜尋 000 資料列。

## <a name="next-steps"></a>後續步驟
* [開始使用記錄分析](log-analytics-get-started.md)toolearn 深入了解記錄分析，以及如何取得最新且正在執行，以分鐘為單位。
