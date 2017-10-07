---
title: "aaaMonitor，診斷和疑難排解儲存體 |Microsoft 文件"
description: "使用功能，例如儲存體分析、 用戶端記錄和其他協力廠商工具 tooidentify，診斷和疑難排解 Azure 儲存體相關問題。"
services: storage
documentationcenter: 
author: fhryo-msft
manager: jahogg
editor: tysonn
ms.assetid: da57e844-705d-449d-8ed5-5607d2a6170b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: fhryo-msft
ms.openlocfilehash: 294a0bd27bd03913e01a719c0175cab827d58225
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-diagnose-and-troubleshoot-microsoft-azure-storage"></a>監視、診斷與疑難排解 Microsoft Azure 儲存體
[!INCLUDE [storage-selector-portal-monitoring-diagnosing-troubleshooting](../../includes/storage-selector-portal-monitoring-diagnosing-troubleshooting.md)]

## <a name="overview"></a>Overview
與傳統環境相比，託管於雲端環境的分散式應用程式一旦發生問題，無論要為其進行診斷或疑難排解，都更加複雜。 應用程式可以部署在 PaaS 或 IaaS 基礎架構、內部部署環境、行動裝置或是這幾種環境的組合上。 一般而言，應用程式的網路流量可能會周遊公用及私人網路和應用程式可能使用多個儲存體技術，例如 Microsoft Azure 儲存體資料表、 Blob、 佇列，或新增 tooother 資料中的檔案會儲存這類關聯式和文件的資料庫。

toomanage 這類應用程式成功您應主動監視和了解如何 toodiagnose 及疑難排解它們和其相關技術的所有層面。 為 Azure 儲存體服務的使用者，您應該持續監視 hello 儲存體服務應用程式使用的任何意外變更行為 （例如低於一般的回應時間），並使用記錄 toocollect 詳細資料和 tooanalyze深入探討的問題。 從監視和記錄您取得 hello 診斷資訊將協助您 toodetermine hello 根本原因的 hello 問題發生您應用程式。 您可以對 hello 問題進行疑難排解，並且判斷 hello 適當的步驟，您可以採取 tooremediate 它。 Azure 儲存體是的核心 Azure 服務，並形成 hello 大部分的客戶部署 toohello Azure 基礎結構的解決方案中很重要的一部分。 Azure 儲存體包含功能 toosimplify 監視、 診斷及疑難排解在雲端應用程式中的儲存體問題。

> [!NOTE]
> 區域備援儲存體 (ZRS) 的複寫類型的儲存體帳戶沒有 hello 度量或記錄功能在此時間內啟用。 
> 
> 

實際操作指南 tooend 端對端疑難排解在 Azure 儲存體的應用程式，請參閱[端對端疑難排解使用 Azure 儲存體度量和記錄、 AzCopy、 Message Analyzer](storage-e2e-troubleshooting.md)。

* [簡介]
  * [本指南架構]
* [監視儲存體服務]
  * [監視服務健康情況]
  * [監視容量]
  * [監視可用性]
  * [監視效能]
* [診斷儲存體問題]
  * [服務健康情況問題]
  * [效能問題]
  * [診斷錯誤]
  * [儲存體模擬器問題]
  * [儲存體記錄工具]
  * [使用網路記錄工具]
* [端對端追蹤]
  * [為記錄資料建立相互關聯]
  * [用戶端要求 ID]
  * [伺服器要求 ID]
  * [時間戳記]
* [疑難排解指引]
  * [度量顯示高 AverageE2ELatency 和低 AverageServerLatency]
  * [度量顯示低 AverageE2ELatency 和低 AverageServerLatency 但 hello 用戶端發生高延遲]
  * [度量顯示高 AverageServerLatency]
  * [佇列上的訊息在遞送期間出現非預期的延遲]
  * [度量顯示 PercentThrottlingError 增加]
  * [度量顯示 PercentTimeoutError 增加]
  * [度量顯示 PercentNetworkError 增加]
  * [hello 用戶端收到 HTTP 403 （禁止） 訊息]
  * [hello 用戶端接收 HTTP 404 （找不到） 訊息]
  * [hello 用戶端接收 HTTP 409 （衝突） 訊息]
  * [度量顯示低 PercentSuccess 或分析記錄檔項目所使用的作業交易狀態的 ClientOtherErrors]
  * [容量度量顯示非預期的儲存體容量使用增加]
  * [附加大量 VHD 的虛擬機器，出現非預期的重新開機情況]
  * [您的問題就會發生從開發或測試使用 hello 儲存體模擬器]
  * [您遇到安裝 hello Azure SDK for.NET 的問題]
  * [您的儲存體服務出現其他問題]
* [附錄]
  * [附錄 1： 使用 Fiddler toocapture HTTP 及 HTTPS 流量]
  * [附錄 2： 使用 Wireshark toocapture 網路流量]
  * [附錄 3： 使用 Microsoft Message Analyzer toocapture 網路流量]
  * [附錄 4： 使用 Excel tooview 度量和記錄資料]
  * [附錄 5： 監視與 Application Insights for Visual Studio Team Services]

## <a name="introduction"></a>簡介
此指南會顯示您如何 toouse 功能，例如 Azure 儲存體分析、 hello Azure 儲存體用戶端程式庫中的用戶端記錄和其他協力廠商工具 tooidentify，診斷和疑難排解 Azure 儲存體的相關問題。

![][1]

*圖 1 監視、診斷與疑難排解*

本指南是預定的 toobe 讀取主要由開發人員使用 Azure 儲存體服務和 IT 專業人員負責管理此類線上服務的線上服務。 本指南 hello 目標如下：

* toohelp 您維護 hello 健全狀況和效能的 Azure 儲存體帳戶。
* tooprovide 您與 hello 必要的處理序和工具 toohelp 您決定問題或應用程式中的問題與 tooAzure 儲存體。
* 您可採取動作來解決問題的指引相關 tooAzure 儲存體 tooprovide。

### <a name="how-this-guide-is-organized"></a>本指南架構
hello > 一節 「[監視儲存體服務]」 說明如何 toomonitor hello 健全狀況和您使用 Azure 儲存體分析度量 （儲存體度量） 的 Azure 儲存體服務的效能。

hello > 一節 「[診斷儲存體問題]」 描述 toodiagnose 發出如何使用 Azure 儲存體分析記錄 （儲存體記錄）。 它也會說明如何 tooenable 用戶端記錄使用 hello 適用於.NET 的其中一種 hello 用戶端程式庫，例如 hello 儲存體用戶端程式庫的設備或 hello Azure SDK for Java。

hello > 一節 「[端對端追蹤]」 說明如何相互關聯各種記錄檔和度量資料中所包含的 hello 資訊。

hello > 一節 「[疑難排解指引]」 提供的 hello 常見的儲存體相關的問題，可能會遇到的疑難排解指引。

hello"[附錄]"包含使用像是 Wireshark 及 netmon 等其他工具來分析網路封包資料、 Fiddler 來分析 HTTP/HTTPS 訊息和相互關聯的 Microsoft Message Analyzer 記錄資料的相關資訊。

## <a name="monitoring-your-storage-service"></a>監視您的儲存體服務
如果您熟悉 Windows 效能監視，可以將儲存體度量當成相當於 Windows 效能監視器計數的 Azure 儲存體。 在儲存體度量您會發現一組完整的度量資訊 （在 Windows 效能監視器術語的計數器），例如服務可用性、 要求 tooservice 的總數目或百分比的成功要求 tooservice （適用於 hello 的完整清單提供的指標，請參閱<a href="http://msdn.microsoft.com/library/azure/hh343264.aspx" target="_blank">儲存體分析度量資料表結構描述</a>MSDN 上)。 您可以指定是否要 hello 儲存體服務 toocollect 以及每個小時或每分鐘彙總的度量資訊。 如需有關如何 tooenable 度量和監視您的儲存體帳戶，請參閱<a href="http://go.microsoft.com/fwlink/?LinkId=510865" target="_blank">啟用儲存體度量</a>MSDN 上。

您可以選擇您想 toodisplay 中的每小時度量 hello Azure 傳統入口網站，並設定每小時度量超過特定閾值時，透過電子郵件通知系統管理員的規則 (如需詳細資訊，請參閱 hello 頁面<a href="http://msdn.microsoft.com/library/azure/dn306638.aspx" target="_blank">How to:接收警示通知及管理在 Azure 中的警示規則</a>)。 hello 儲存體服務會收集度量使用最佳的效果，但可能不會記錄每個儲存體作業。

下面圖 2 顯示 hello [監視] 頁面中 hello Azure 傳統入口網站，您可以在其中檢視度量資訊，例如可用性、 要求總數和儲存體帳戶的平均延遲數字。 通知規則也已設定總 tooalert 系統管理員如果低於特定層級的可用性。 從檢視此資料，一個可能的區域，以便調查是 hello 資料表服務成功百分比低於 100%的 (如需詳細資訊，請參閱 hello 節 「[度量顯示低 PercentSuccess 或分析記錄檔項目所使用的作業交易狀態的 ClientOtherErrors]")。

![][2]

*圖 2 在 hello Azure 傳統入口網站中檢視儲存體度量*

您應持續監視您的 Azure 應用程式 tooensure 它們皆狀況良好並執行以預期的方式：

* 建立應用程式一些基準度量將可讓您 toocompare 目前的資料並識別任何 hello 行為的 Azure 儲存體和您的應用程式的重大變更。 hello 的基準度量的值，在許多情況下，將特定的應用程式，您應該建立時的效能測試您的應用程式。
* 記錄每分鐘度量及使用這些 toomonitor 主動未預期的錯誤，例如激增錯誤計數或要求率異常。
* 記錄每小時度量和使用它們 toomonitor 平均值例如平均錯誤計數，並要求率。
* 調查潛在的問題，使用診斷工具，如稍後所述 hello > 一節 「[診斷儲存體問題]。 」

在下面圖 3 中的 hello 圖表會說明如何 hello 平均發生每小時度量可以隱藏尖峰活動中。 hello 每小時度量 hello 分鐘度量顯示真的很的 hello 波動時顯示 tooshow 的要求，穩定的速率。

![][3]

hello 本節其餘部分描述，您應監視哪些度量和原因。

### <a name="monitoring-service-health"></a>監視服務健康情況
您可以使用 hello [Azure 傳統入口網站](https://manage.windowsazure.com)tooview hello 健全狀況的 hello 儲存體服務 （和其他 Azure 服務） 在所有 hello hello 世界各地的 Azure 區域。 這可讓您 toosee 立即如果您的控制項外問題會影響 hello hello 區域用於您的應用程式中的儲存體服務。

hello Azure 傳統入口網站也可以提供會影響 hello 事件的告知各種 Azure 服務。
注意： 這項資訊是先前可供使用，歷程記錄資料，在 hello Azure 服務儀表板在<a href="http://status.azure.com" target="_blank">http://status.azure.com</a>。

因為 hello Azure 傳統入口網站會收集健全狀況資訊從內 hello Azure 資料中心 （內部向外監視），您可能也會考慮採用在外部方法 toogenerate 綜合交易定期存取您 Azure 託管從多個位置的 web 應用程式。 所提供服務的 hello<a href="http://www.keynote.com/solutions/monitoring/web-monitoring" target="_blank">專題</a>， <a href="https://www.gomeznetworks.com/?g=1" target="_blank">Gomez</a>，和 Application Insights for Visual Studio Team Services 是這種外部中的範例。 如需有關 Application Insights for Visual Studio Team Services，請參閱 hello 附錄"[附錄 5： 監視與 Application Insights for Visual Studio Team Services]。 」

### <a name="monitoring-capacity"></a>監視容量
儲存體度量只會儲存 hello blob 服務的容量度量，因為 blob 通常考慮 hello 儲存之資料的最大的比例 （hello 撰寫本文時，它不可能 toouse 儲存體度量 toomonitor hello 容量資料表和佇列）. 您可以在 hello 找到這項資料**$MetricsCapacityBlob**資料表，如果您已啟用 hello Blob 服務的監視。 儲存體度量會記錄此資料每天一次，而且您可以使用 hello hello 值**RowKey** toodetermine hello 資料列是否包含實體與相關 toouser 資料 (值**資料**) 或分析資料 （值**分析**)。 每個預存的實體包含 hello 用儲存空間量的相關資訊 (**容量**以位元組為單位) 和 hello 目前數目的容器 (**ContainerCount**) 和 blob (**ObjectCount**) hello 儲存體帳戶中的使用中。 如需有關儲存在 hello hello 容量度量**$MetricsCapacityBlob**資料表，請參閱<a href="http://msdn.microsoft.com/library/azure/hh343264.aspx" target="_blank">儲存體分析度量資料表結構描述</a>MSDN 上。

> [!NOTE]
> 您應監視早期警告您已接近 hello 容量限制的儲存體帳戶的這些值。 在 hello Azure 傳統入口網站上 hello**監視器**頁面儲存體帳戶，您可以加入警示規則 toonotify，您如果使用的彙總的存放裝置超過或低於您指定的臨界值。
> 
> 

估計的各種不同的儲存體物件，例如 blob hello 大小的說明，請參閱 hello 部落格文章<a href="http://blogs.msdn.com/b/windowsazurestorage/archive/2010/07/09/understanding-windows-azure-storage-billing-bandwidth-transactions-and-capacity.aspx" target="_blank">了解 Azure 儲存體計費 – 頻寬、 交易和容量</a>。

### <a name="monitoring-availability"></a>監視可用性
您也應該監視在 hello hello 值儲存體帳戶中監視 hello 儲存體服務的 hello 可用性**可用性**中的資料行 hello 每小時或分鐘度量資料表 — **$MetricsHourPrimaryTransactionsBlob**， **$MetricsHourPrimaryTransactionsTable**， **$MetricsHourPrimaryTransactionsQueue**， **$MetricsMinutePrimaryTransactionsBlob**， **$MetricsMinutePrimaryTransactionsTable**， **$MetricsMinutePrimaryTransactionsQueue**， **$MetricsCapacityBlob**。 hello**可用性**資料行包含表示 hello 或可用性的 hello 服務 hello 資料列代表 hello 應用程式開發介面作業的百分比值 (hello **RowKey**顯示是否 hello 資料列包含度量 hello 服務整體或特定的應用程式開發介面作業）。

任何小於 100% 的值，皆表示某些儲存體要求已經失敗。 您可以看到所檢查的失敗為何 hello hello 度量資料，例如顯示 hello 與不同的錯誤類型的要求數目的其他資料行**ServerTimeoutError**。 您應該預期 toosee**可用性**原因例如暫時性的伺服器逾時資料分割 toobetter 負載平衡要求 hello 服務不斷年秋季暫時低於 100%; 重試邏輯，用戶端應用程式中的 hello應該要處理這類間歇性的條件。 hello 頁面<a href="http://msdn.microsoft.com/library/azure/hh343260.aspx" target="_blank"></a>清單 hello 交易類型中包含的儲存體度量其**可用性**計算。

在 hello Azure 傳統入口網站上 hello**監視器**頁面儲存體帳戶，您可以加入警示規則 toonotify 您如果**可用性**針對服務低於您指定的臨界值。

hello"[疑難排解指引]」 一節說明一些常見儲存體服務問題相關的 tooavailability。

### <a name="monitoring-performance"></a>監視效能
toomonitor hello hello 儲存體服務的效能，您可以使用 hello hello 中的下列度量時，也將每小時和分鐘度量資料表。

* hello 中 hello 值**AverageE2ELatency**和**AverageServerLatency**顯示 hello 的平均時間 hello 儲存體服務或應用程式開發介面作業類型所花的 tooprocess 要求。 **AverageE2ELatency**是包含 hello 時間 tooread hello 要求的端對端延遲的量值，並新增 toohello 所花費時間 tooprocess hello 要求中傳送 hello 回應 （因此包括網路延遲一旦 hello 要求達到 hello 儲存體服務）;**AverageServerLatency**是只 hello 處理的時間量值，因此不包括任何相關的網路延遲 toocommunicating hello 用戶端。 請參閱 hello 一節 「[度量顯示高 AverageE2ELatency 和低 AverageServerLatency]"稍後在本指南的討論的原因可能會顯著的差異，這兩個值之間。
* hello 中 hello 值**TotalIngress**和**TotalEgress**資料行會顯示 hello 總資料量，以位元組為單位，傳入 tooand 移出儲存體服務或透過特定的應用程式開發介面作業類型。
* hello 中 hello 值**TotalRequests**接收的資料行顯示 hello 總數 hello 應用程式開發介面作業的儲存體服務的要求。 **TotalRequests**是 hello hello 儲存體服務收到的要求數總計。

一般來說，您需要監視這些值是否出現非預期的改變，以便察覺是否有需要進一步調查原因的問題。

在 hello Azure 傳統入口網站上 hello**監視器**頁面儲存體帳戶，您可以加入警示規則 toonotify 您是否有任何的這項服務的 hello 效能度量低於，或超過您指定的臨界值。

hello"[疑難排解指引]」 一節說明一些常見儲存體服務問題相關的 tooperformance。

## <a name="diagnosing-storage-issues"></a>診斷儲存體問題
您可以藉由許多方式來察覺應用程式裡的問題，包括：

* 嚴重錯誤，導致 hello 應用程式 toocrash 或 toostop 工作。
* 重大變更的 hello hello 上一節中所述，您要監視的度量的基準值從"[監視儲存體服務]。 」
* 您的應用程式使用者回報表示，某些特定操作無法如預期完成，或是某些功能無法正常運作。
* 您的應用程式所產生，並顯示在記錄檔或是透過其他通知方法顯示的錯誤。

一般而言，問題相關的 tooAzure 儲存體服務可分成四大類的其中一個：

* 您的應用程式發生效能問題，或是由您的使用者，報告顯示 hello 效能度量的變更。
* 沒有在一或多個區域中的 hello Azure 儲存體基礎結構發生問題。
* 您的應用程式發生錯誤，請回報您的使用者，或增加其中一種您監視 hello 錯誤計數度量所揭露。
* 在開發和測試，您可能使用 hello 本機儲存體模擬器;您可能會與相關特別 toousage hello 儲存體模擬器的一些問題。

hello 下列各節簡述 hello 步驟，您應該遵循 toodiagnose，並在每個這四種類型的問題進行疑難排解。 hello > 一節 「[疑難排解指引]"稍後在本指南中提供詳細資料可能會遇到一些常見的問題。

### <a name="service-health-issues"></a>服務健康情況問題
服務健康情況問題通常是您無法掌控的部分。 hello Azure 傳統入口網站與 Azure 服務，包括儲存體服務提供任何進行中的問題的資訊。 如果您選擇的讀取權限的地理備援儲存體，當您建立儲存體帳戶，然後在 hello 事件的資料在 hello 主要位置中，無法使用您的應用程式無法切換暫時 toohello hello 次要位置中的唯讀複本。 toodo，您的應用程式必須能夠 tooswitch 之間使用 hello 主要和次要儲存體位置，是無法 toowork 精簡的功能模式的唯讀資料。 hello Azure 儲存體用戶端程式庫可讓您 toodefine 從主要儲存體讀取失敗時，可讀取次要儲存體的重試原則。 您的應用程式也需要 toobe 注意 hello 次要位置中的 hello 資料是最終保持一致。 如需詳細資訊，請參閱 hello 部落格文章<a href="http://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/04/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx" target="_blank">Azure 儲存體備援選項和讀取權限地理備援儲存體</a>。

### <a name="performance-issues"></a>效能問題
hello 效能的應用程式可以是主觀看法，尤其是從使用者的觀點。 因此，很重要的 toohave 基準度量可用 toohelp 您識別在可能的效能問題。 許多因素可能會影響 hello 效能的觀點 hello 用戶端應用程式的 Azure 儲存體服務。 這些因素可能運作 hello 儲存體服務、 hello 用戶端，或 hello 網路基礎結構。因此，是重要 toohave 識別 hello 原點的 hello 效能問題的策略。

識別 hello hello 原因 hello 從 hello 計量的效能問題的可能位置之後，您接著可以使用 hello 記錄檔案 toofind 和詳細資訊 toodiagnose 進一步 hello 問題進行疑難排解。

hello > 一節 「[疑難排解指引]"本指南稍後會提供詳細資訊與相關的一些常見效能問題可能會發生。

### <a name="diagnosing-errors"></a>診斷錯誤
應用程式的使用者可以通知您 hello 用戶端應用程式所回報的錯誤。 儲存體度量還會記錄來自儲存體服務的不同錯誤類型計數，例如 **NetworkError**、**ClientTimeoutError** 或 **AuthorizationError**。 雖然儲存體度量只會記錄不同的錯誤類型計數，不過您還是可以藉由檢視伺服器端、用戶端與網路記錄來取得個別要求的詳細資料。 一般而言，hello hello 儲存體服務所傳回的 HTTP 狀態碼會提供 hello 要求為何失敗的指示。

> [!NOTE]
> 請記住，您應該預期 toosee 一些間歇性的錯誤： 例如，tootransient 網路狀況，因為錯誤或應用程式錯誤。
> 
> 

hello MSDN 上的下列資源可用於了解儲存體相關狀態值和錯誤碼：

* <a href="http://msdn.microsoft.com/library/azure/dd179357.aspx" target="_blank">常見的 REST API 錯誤碼</a>
* <a href="http://msdn.microsoft.com/library/azure/dd179439.aspx" target="_blank">Blob 服務錯誤碼</a>
* <a href="http://msdn.microsoft.com/library/azure/dd179446.aspx" target="_blank">佇列服務錯誤碼</a>
* <a href="http://msdn.microsoft.com/library/azure/dd179438.aspx" target="_blank">表格服務錯誤碼</a>

### <a name="storage-emulator-issues"></a>儲存體模擬器問題
hello Azure SDK 包含的儲存體模擬器，您可以在開發工作站執行。 此模擬器模擬大部分的 hello hello Azure 儲存體服務的行為，以及開發和測試期間會很有用，讓您 toorun 使用不含 hello Azure 儲存體服務的應用程式需要 Azure 訂用帳戶和 Azure 儲存體帳戶。

hello"[疑難排解指引]」 一節說明一些常見的問題使用 hello 儲存體模擬器。

### <a name="storage-logging-tools"></a>儲存體記錄工具
儲存體記錄功能可針對您的 Azure 儲存體帳戶，提供伺服器端的儲存體要求記錄服務。 如需如何 tooenable 伺服器端記錄和存取 hello 記錄資料的詳細資訊，請參閱<a href="http://go.microsoft.com/fwlink/?LinkId=510867" target="_blank">使用伺服器端記錄功能</a>MSDN 上。

hello 適用於.NET 的儲存體用戶端程式庫可讓您與您的應用程式所執行的 toostorage 作業相關的 toocollect 用戶端記錄檔資料。 如需如何 tooenable 用戶端記錄和存取 hello 記錄資料的詳細資訊，請參閱<a href="http://go.microsoft.com/fwlink/?LinkId=510868" target="_blank">用戶端記錄使用 hello 儲存體用戶端程式庫</a>MSDN 上。

> [!NOTE]
> 在某些情況下 （例如 SAS 授權失敗），使用者可能會報告的錯誤，您可以找到沒有要求資料在 hello 伺服器端儲存體記錄。 您可以使用 hello 儲存體用戶端程式庫 tooinvestigate hello 記錄功能，如果 hello hello 問題原因是 hello 用戶端上，或使用網路監視工具 tooinvestigate hello 網路。
> 
> 

### <a name="using-network-logging-tools"></a>使用網路記錄工具
您可以擷取之間 hello 用戶端和伺服器 tooprovide 詳細 hello 流量 hello 資料 hello 用戶端和伺服器的相關資訊會交換及 hello 基礎網路狀況。 有用的網路記錄工具如下：

* Fiddler (<a href="http://www.telerik.com/fiddler" target="_blank">http://www.telerik.com/fiddler</a>) 是免費的 web 偵錯 tooexamine hello 標頭和內容資料的 HTTP 和 HTTPS 要求和回應訊息，可讓您的 proxy。 如需詳細資訊，請參閱 「[附錄 1： 使用 Fiddler toocapture HTTP 及 HTTPS 流量]"。
* Microsoft 網路監視器 (Netmon) (<a href="http://www.microsoft.com/download/details.aspx?id=4865" target="_blank">http://www.microsoft.com/download/details.aspx?id=4865</a>) 和 Wireshark (<a href="http://www.wireshark.org/" target="_blank">http://www.wireshark.org/</a>) 是可用的網路通訊協定分析器可讓您 tooview 封包的詳細資訊廣泛的網路通訊協定。 如需 Wireshark 的詳細資訊，請參閱 「[附錄 2： 使用 Wireshark toocapture 網路流量]"。
* Microsoft Message Analyzer 是取代 Netmon 和會另外 toocapturing 網路封包資料的 microsoft 工具可協助您 tooview 和分析從其他工具所擷取的 hello 記錄資料。 如需詳細資訊，請參閱 「[附錄 3： 使用 Microsoft Message Analyzer toocapture 網路流量]"。
* 如果您想用戶端電腦可以透過 hello 網路連線 toohello Azure 儲存體服務的基本連線測試 toocheck tooperform，您無法這樣使用 hello 標準**ping** hello 用戶端上的工具。 不過，您可以使用 hello **tcping**工具 toocheck 連線。 **Tcping** 可從 <a href="http://www.elifulkerson.com/projects/tcping.php" target="_blank">http://www.elifulkerson.com/projects/tcping.php</a> 下載。

在許多情況下，從儲存體記錄 」 和 「 hello 儲存體用戶端程式庫的 hello 記錄資料將是足夠 toodiagnose 有問題，但在某些情況下，您可能需要的 hello 的詳細資訊，可以提供這些網路記錄工具。 例如，使用 Fiddler tooview tooview 標頭和承載資料傳送 tooand hello 從儲存體服務，讓您 tooexamine 如何用戶端應用程式的 HTTP 和 HTTPS 的訊息啟用會重試儲存體作業。 例如 Wireshark 通訊協定分析器更 hello 封包層級，讓您 tooview TCP 資料，可讓您 tootroubleshoot 遺失封包和連線問題。 Message Analyzer 可同時在 HTTP 與 TCP 網路層運作。

## <a name="end-to-end-tracing"></a>端對端追蹤
使用各種記錄檔案進行的端對端追蹤方式，是調查潛在問題的有效方法。 您可以使用從度量資料的 hello 日期/時間資訊做為 toostart hello 的 hello 記錄檔中尋找詳細的資訊可協助您疑難排解問題 hello 的表示。

### <a name="correlating-log-data"></a>為記錄資料建立相互關聯
當檢視從用戶端應用程式記錄檔，網路追蹤，且其記錄的伺服器端儲存體重大 toobe 無法 toocorrelate 要求對 hello 不同的記錄檔。 hello 記錄檔包含不同適合做為相互關聯識別碼的欄位數目。 hello 用戶端要求 id 是 hello 最有用欄位 toouse toocorrelate 中的項目 hello 不同的記錄檔。 不過有時候，可能很有用的 toouse hello 伺服器要求 id 或時間戳記。 hello 下列各節提供有關這些選項更多詳細資料。

### <a name="client-request-id"></a>用戶端要求 ID
hello 儲存體用戶端程式庫會自動產生的每個要求的唯一用戶端要求識別碼。

* 在 hello hello 儲存體用戶端程式庫的用戶端記錄建立時，hello 用戶端要求識別碼會出現在 hello**用戶端要求 ID**相關 toohello 要求每個記錄項目欄位。
* 例如 Fiddler 擷取網路追蹤，在 hello 用戶端要求識別碼會在要求訊息中視為 hello **x ms-用戶端的要求識別碼**HTTP 標頭值。
* Hello 伺服器端儲存體記錄 」 記錄檔中，會顯示 hello 用戶端要求 id，hello 用戶端要求識別碼 資料行。

> [!NOTE]
> 是可能的多個要求 tooshare hello 相同的用戶端要求 id，因為 hello 用戶端可以指派這個值 （雖然 hello 儲存體用戶端程式庫會自動指派新值）。 在從 hello 用戶端重試次數的 hello 情況下，所有嘗試都共用 hello 相同的用戶端要求識別碼。在批次 hello 用戶端送出 hello 情況下，hello 批次都有單一用戶端要求識別碼。
> 
> 

### <a name="server-request-id"></a>伺服器要求 ID
hello 儲存體服務會自動產生伺服器要求 id。

* Hello 伺服器端儲存體記錄 」 記錄檔中，在 hello 伺服器要求 id 會顯示 hello**要求識別碼標頭**資料行。
* 例如 Fiddler 擷取網路追蹤，在 hello 伺服器要求 id 會出現在回應訊息當做 hello **x ms-要求識別碼**HTTP 標頭值。
* 在 hello hello 儲存體用戶端程式庫的用戶端記錄建立時，會顯示以 hello hello 伺服器要求 id**作業文字**hello 記錄項目顯示 hello 伺服器回應的詳細資料的資料行。

> [!NOTE]
> hello 儲存體服務一律指派唯一的伺服器要求 id tooevery 要求收到，以便從 hello 用戶端每次重試嘗試和批次中每個作業都有唯一的伺服器要求 id。
> 
> 

如果 hello 儲存體用戶端程式庫會擲回**StorageException** hello 用戶端，在 hello **RequestInformation**屬性包含**RequestResult**包含的物件**ServiceRequestID**屬性。 您可以從 **OperationContext** 執行個體存取 **RequestResult** 物件。

hello 以下的程式碼範例示範如何自訂 tooset **ClientRequestId**藉由附加的值**OperationContext** hello 要求 toohello 儲存體服務的物件。 它也會示範如何 tooretrieve hello **ServerRequestId** hello 回應訊息中的值。

```csharp
//Parse hello connection string for hello storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Create an Operation Context that includes custom ClientRequestId string based on constants defined within hello application along with a Guid.
OperationContext oc = new OperationContext();
oc.ClientRequestID = String.Format("{0} {1} {2} {3}", HOSTNAME, APPNAME, USERID, Guid.NewGuid().ToString());

try
{
    CloudBlobContainer container = blobClient.GetContainerReference("democontainer");
    ICloudBlob blob = container.GetBlobReferenceFromServer("testImage.jpg", null, null, oc);  
    var downloadToPath = string.Format("./{0}", blob.Name);
    using (var fs = File.OpenWrite(downloadToPath))
    {
        blob.DownloadToStream(fs, null, null, oc);
        Console.WriteLine("\t Blob downloaded toofile: {0}", downloadToPath);
    }
}
catch (StorageException storageException)
{
    Console.WriteLine("Storage exception {0} occurred", storageException.Message);
    // Multiple results may exist due tooclient side retry logic - each retried operation will have a unique ServiceRequestId
    foreach (var result in oc.RequestResults)
    {
            Console.WriteLine("HttpStatus: {0}, ServiceRequestId {1}", result.HttpStatusCode, result.ServiceRequestID);
    }
}
```

### <a name="timestamps"></a>時間戳記
您也可以使用時間戳記 toolocate 相關記錄項目，但請注意任何的時鐘誤差 hello 用戶端之間可能存在的伺服器。 您應該搜尋的加號或減號 15 分鐘進行比對伺服器端 hello hello 用戶端上的時間戳記為基礎的項目。 請記住 hello 的 blob 中繼資料包含的度量表示 hello hello 度量 hello blob; 中所儲存的時間範圍的 hello blob這是適用於您有許多 hello 相同分鐘或小時度量 blob。

## <a name="troubleshooting-guidance"></a>疑難排解指引
本章節將協助您 hello 診斷和疑難排解的 hello 常見的問題，因此您的應用程式使用 hello Azure 儲存體服務時可能遇到。 使用下列 toolocate hello 資訊相關 tooyour 特定問題的 hello 清單。

**疑難排解決策樹**

- - -
您的問題與 toohello 效能的其中一個 hello 儲存體服務產生關聯？

* [度量顯示高 AverageE2ELatency 和低 AverageServerLatency]
* [度量顯示低 AverageE2ELatency 和低 AverageServerLatency 但 hello 用戶端發生高延遲]
* [度量顯示高 AverageServerLatency]
* [佇列上的訊息在遞送期間出現非預期的延遲]

- - -
您的問題與 toohello 可用性的其中一個 hello 儲存體服務產生關聯？

* [度量顯示 PercentThrottlingError 增加]
* [度量顯示 PercentTimeoutError 增加]
* [度量顯示 PercentNetworkError 增加]

- - -
您的用戶端應用程式是否收到來自儲存體服務的 HTTP 4XX (例如 404) 回應？

* [hello 用戶端收到 HTTP 403 （禁止） 訊息]
* [hello 用戶端接收 HTTP 404 （找不到） 訊息]
* [hello 用戶端接收 HTTP 409 （衝突） 訊息]

- - -
[度量顯示低 PercentSuccess 或分析記錄檔項目所使用的作業交易狀態的 ClientOtherErrors]

- - -
[容量度量顯示非預期的儲存體容量使用增加]

- - -
[附加大量 VHD 的虛擬機器，出現非預期的重新開機情況]

- - -
[您的問題就會發生從開發或測試使用 hello 儲存體模擬器]

- - -
[您遇到安裝 hello Azure SDK for.NET 的問題]

- - -
[您的儲存體服務出現其他問題]

- - -
### <a name="metrics-show-high-AverageE2ELatency-and-low-AverageServerLatency"></a>度量顯示高 AverageE2ELatency 與低 AverageServerLatency
hello 圖攻擊的效果從 hello Azure 傳統入口網站監視工具示範其中 hello **AverageE2ELatency**明顯高於 hello **AverageServerLatency**。

![][4]

注意 hello 儲存體服務才會計算 hello 度量**AverageE2ELatency**成功的要求，而且不同於**AverageServerLatency**，包括 hello 用戶端可以採用 toosend hello hello 時間資料和通知接收從 hello 儲存體服務。 因此，差異**AverageE2ELatency**和**AverageServerLatency**可能是因為 toohello 用戶端應用程式所緩慢 toorespond 或到期 tooconditions hello 網路上的。

> [!NOTE]
> 您也可以檢視**E2ELatency**和**ServerLatency** hello 儲存體記錄中的個別儲存體作業的記錄資料。
> 
> 

#### <a name="investigating-client-performance-issues"></a>調查用戶端效能問題
Hello 用戶端的回應速度較慢的可能原因包括擁有有限的數目的可用連線或執行緒。 藉由修改 hello 用戶端程式碼 toobe 更有效率 （例如使用非同步呼叫 toohello 儲存體服務），或使用較大的虛擬機器 （使用更多核心和更多的記憶體），您可能是無法 tooresolve hello 問題。

Hello 資料表和佇列服務的 hello Nagle 演算法也會造成高**AverageE2ELatency**相較太**AverageServerLatency**： 如需詳細資訊，請參閱文章 hello <a href="http://blogs.msdn.com/b/windowsazurestorage/archive/2010/06/25/nagle-s-algorithm-is-not-friendly-towards-small-requests.aspx" target="_blank">Nagle 的演算法是不好記往小要求</a>hello Microsoft Azure 儲存體團隊部落格上。 您可以利用 hello 停用程式碼中的 hello Nagle 演算法**ServicePointManager**類別中 hello **System.Net**命名空間。 前進行任何呼叫 toohello 資料表或佇列服務，因為這不會影響已連線應用程式中的開啟，您應該執行此動作。 hello 下列範例來自 hello **Application_Start**背景工作角色中的方法。

```csharp
var storageAccount = CloudStorageAccount.Parse(connStr);
ServicePoint tableServicePoint = ServicePointManager.FindServicePoint(storageAccount.TableEndpoint);
tableServicePoint.UseNagleAlgorithm = false;
ServicePoint queueServicePoint = ServicePointManager.FindServicePoint(storageAccount.QueueEndpoint);
queueServicePoint.UseNagleAlgorithm = false;
```

您應該檢查 hello 用戶端記錄檔 toosee 多少要求已提交您的用戶端應用程式，並檢查一般的.NET 有關在您的用戶端，例如 CPU、.NET 記憶體回收、 網路使用量或記憶體 （以開始效能瓶頸點.NET 用戶端應用程式進行疑難排解，請參閱<a href="http://msdn.microsoft.com/library/7fe0dd2y(v=vs.110).aspx" target="_blank">偵錯、 追蹤和分析</a>MSDN 上)。

#### <a name="investigating-network-latency-issues"></a>調查網路延遲問題
一般而言，高 hello 網路導致的端對端延遲是因為 tootransient 條件。 您可以使用 Wireshark 或 Microsoft Message Analyzer 之類的工具調查暫時性與永久性網路問題，例如遭到捨棄的封包。

如需有關使用 Wireshark tootroubleshoot 網路問題的詳細資訊，請參閱 「[附錄 2： 使用 Wireshark toocapture 網路流量]。 」

如需有關使用 Microsoft Message Analyzer tootroubleshoot 網路問題的詳細資訊，請參閱 「[附錄 3： 使用 Microsoft Message Analyzer toocapture 網路流量]。 」

### <a name="metrics-show-low-AverageE2ELatency-and-low-AverageServerLatency"></a>度量顯示低 AverageE2ELatency 和低 AverageServerLatency 但 hello 用戶端發生高延遲
在此案例中，hello 最可能的原因是 hello 儲存體要求到達 hello 儲存體服務中的延遲。 您應該調查原因 hello 用戶端的要求不會進行它透過 toohello blob 服務。

Hello 延遲傳送要求的用戶端的可能原因包括擁有有限的數目的可用連線或執行緒。 您也應該檢查如果 hello 用戶端正在執行多個重試次數，並在 hello 情況下調查 hello 原因。 您可以透過程式設計方式在 hello 中尋找**OperationContext** hello 要求和擷取 hello 與相關聯的物件**ServerRequestId**值。 如需詳細資訊，請參閱 hello hello > 一節中的程式碼範例 」[伺服器要求 ID]。 」

如果在 hello 用戶端有任何問題，您應該調查潛在的網路問題，例如封包遺失。 您可以使用 calcproxy.tlb Wireshark 或 Microsoft Message Analyzer tooinvestigate 網路問題。

如需有關使用 Wireshark tootroubleshoot 網路問題的詳細資訊，請參閱 「[附錄 2： 使用 Wireshark toocapture 網路流量]。 」

如需有關使用 Microsoft Message Analyzer tootroubleshoot 網路問題的詳細資訊，請參閱 「[附錄 3： 使用 Microsoft Message Analyzer toocapture 網路流量]。 」

### <a name="metrics-show-high-AverageServerLatency"></a>度量顯示高 AverageServerLatency
在高的案例中 hello **AverageServerLatency** blob 下載要求，您應該使用的 hello 儲存體記錄 」 記錄 toosee，若沒有的 hello 相同 blob （或設定 blob 的） 重複的要求。 Blob 上傳要求，您應該調查哪些區塊大小 hello 用戶端所使用 （例如，小於 64k 大小可能會導致額外負荷除非 hello 讀取也會在區塊小於 64k 區塊），以及多個用戶端會將上傳區塊 toohello 相同blob 以平行方式。 您也應該檢查 hello 數目超過每個第二個延展性目標的 hello 會導致的要求中的高峰的 hello 每分鐘度量： 另請參閱 「[度量顯示 PercentTimeoutError 增加]。 」

如果您看到高**AverageServerLatency** blob 下載要求時那里重複的要求 hello 相同的 blob 或 blob，一組然後您應該考慮使用 Azure 快取這些 blob 的快取或 hello Azure 內容傳遞網路 (CDN)。 上傳要求，您可以使用較大的區塊大小，以改善 hello 輸送量。 查詢 tootables 對於也可能 tooimplement 用戶端快取上執行相同查詢作業，且其中 hello 的 hello 用戶端不會經常變更的資料。

高**AverageServerLatency**值可以也可能表示設計不良的資料表或查詢中掃描作業的結果，或遵循 hello 附加/附加在前面的反向模式。 如需詳細資訊，請參閱「[度量顯示 PercentThrottlingError 增加]」。

> [!NOTE]
> 您可以在這裡找到完整的檢查清單，包括效能檢查清單： [Microsoft Azure 儲存體效能與延展性檢查清單](storage-performance-checklist.md)。
> 
> 

### <a name="you-are-experiencing-unexpected-delays-in-message-delivery"></a>佇列上的訊息在遞送期間出現非預期的延遲
如果您遇到 hello 時間之間的延遲應用程式將訊息 tooa 佇列和 hello 時間會變得可用 tooread hello 佇列中，則您應該採取下列步驟 toodiagnose hello 問題的 hello:

* 請確認 hello 應用程式已成功加入 hello 訊息 toohello 佇列。 檢查 hello 應用程式不會重試 hello **AddMessage**數次成功之前的方法。 hello 儲存體用戶端程式庫記錄檔會顯示任何重複的儲存體作業的重試作業。
* 請確認沒有任何時鐘誤差新增 hello 訊息 toohello 佇列和 hello hello 佇列，可讓讀取 hello 訊息的背景工作角色會出現一樣會有延遲處理中的 hello 背景工作角色。
* 請查看失敗是否會從 hello 佇列讀取 hello 訊息的 hello 背景工作角色。 如果佇列用戶端呼叫 hello **GetMessage**方法卻失敗 toorespond 確認，hello 訊息將會繼續 hello 佇列上看不到 hello **invisibilityTimeout**期限到期。 此時，hello 訊息會變成可用於處理一次。
* 檢查是否 hello 佇列長度會隨著時間不斷增加。 如果您沒有足夠的 hello 佇列上放置會其他工作者所有 hello 訊息的工作者可用 tooprocess，也可能會發生。 您也應該檢查 hello 度量 toosee 是否刪除失敗的要求和 hello 清除佇列計數的訊息，而這可能表示重複失敗的嘗試 toodelete hello 訊息。
* 檢查 hello 任何佇列作業，比預期更高的儲存體記錄 」 記錄檔**E2ELatency**和**ServerLatency**經過一段時間比平常更長時間的時間值。

### <a name="metrics-show-an-increase-in-PercentThrottlingError"></a>度量顯示 PercentThrottlingError 增加
當您超出儲存體服務的 hello 延展性目標時，就會發生節流處理錯誤。 hello 儲存體服務會執行此 tooensure 的任何單一用戶端或租用戶可以在 hello 費用的其他人使用 hello 服務。 如需儲存體帳戶之延展性目標及儲存體帳戶內資料分割之效能目標的詳細資訊，請參閱 <a href="http://msdn.microsoft.com/library/azure/dn249410.aspx" target="_blank">Azure 儲存體延展性與效能目標</a>。

如果 hello **PercentThrottlingError**計量會顯示以 hello 百分比為單位的要求失敗並發生節流錯誤的增加，您需要 tooinvestigate 兩種情況下：

* [PercentThrottlingError 的暫時性增加]
* [PercentThrottlingError 錯誤中的永久性增加]

增加**PercentThrottlingError**通常發生於 hello 相同時間增加 hello 儲存體要求數量，或當您一開始載入測試您的應用程式。 這可能也的資訊清單本身 hello 做為 「 503 伺服器忙碌 」 或 「 500 作業逾時 」 HTTP 儲存體作業的狀態訊息的用戶端。

#### <a name="transient-increase-in-PercentThrottlingError"></a>PercentThrottlingError 的暫時性增加
如果您看見 hello 值中的高峰**PercentThrottlingError** ，符合的 hello 應用程式大量活動期間，您應該在您的用戶端實作 （不是線性的） 指數型停止重試策略： 這降低 hello 立即載入 hello 磁碟分割上的，並協助您的應用程式 toosmooth 出的流量尖峰。 如需有關如何使用 tooimplement 重試原則 hello 儲存體用戶端程式庫的詳細資訊，請參閱<a href="http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.retrypolicies.aspx" target="_blank">Microsoft.WindowsAzure.Storage.RetryPolicies 命名空間</a>MSDN 上。

> [!NOTE]
> 您也可能會看到 hello 值中的高峰**PercentThrottlingError**的不一致的 hello 應用程式大量活動期間與： 這裡 hello 最可能的原因是移動資料分割 tooimprove 負載 hello 儲存體服務平衡。
> 
> 

#### <a name="permanent-increase-in-PercentThrottlingError"></a>PercentThrottlingError 錯誤中的永久性增加
如果您看到值一直很高**PercentThrottlingError**下列永久的增加交易的磁碟區，或執行您的初始載入時您的應用程式上測試，則您需要 tooevaluate您的應用程式如何使用儲存體的資料分割，它即將是否 hello 延展性目標儲存體帳戶。 例如，如果您看見期間發生節流錯誤 （其中會計算為單一磁碟分割） 的佇列上，然後您應該考慮使用其他佇列 toospread hello 交易橫跨多個資料分割。 如果您看見期間發生節流錯誤的資料表上，您需要使用不同的資料分割配置 toospread tooconsider 交易橫跨多個資料分割使用廣泛的資料分割索引鍵值。 此問題的一個常見原因是 hello 前面加上/附加反面模式，其中您選取作為 hello 資料分割索引鍵的 hello 日期，然後在某特定日期的所有資料都寫入 tooone 磁碟分割： 在負載下，這會導致寫入瓶頸。 您應該考慮採用不同的資料分割設計，或是評估使用 Blob 儲存體是否會更好。 您也應該檢查如果 hello 節流發生的結果中您的流量尖峰和調查平滑化您的要求模式的方式。

如果您的交易分散多個資料分割時，您仍然必須留意 hello 設定 hello 儲存體帳戶的延展性限制。 例如，如果您使用十個佇列每秒 2000 個 1 KB 訊息的每個處理 hello 最大值時，您會在 hello 整體 20,000 每秒的訊息 hello 儲存體帳戶的限制。 如果您需要 tooprocess 秒超過 20,000 部實體時，您應該考慮使用多個儲存體帳戶。 您應該也記住您的要求該 hello 大小和實體將會影響當 hello 儲存體服務節流處理您的用戶端： 如果您有較大的要求和實體，您可能會被調整更快。

效率不佳的查詢設計也可能導致您的資料表資料分割的 toohit hello 延展性限制。 例如，具有篩選，只選取一個百分比 hello 實體的資料分割中，但會掃描所有資料分割中的 hello 實體的查詢需要 tooaccess 每個實體。 讀取的每個實體都會計入 hello 交易總數中該資料分割;因此，您可以輕鬆地連線到 hello 延展性目標。

> [!NOTE]
> 您的效能測試作業應該會顯示應用程式中任何不敷使用的查詢設計。
> 
> 

### <a name="metrics-show-an-increase-in-PercentTimeoutError"></a>度量顯示 PercentTimeoutError 增加
您的度量顯示其中一個儲存體服務的 **PercentTimeoutError** 有增加情況。 在 hello 相同時間、 hello 用戶端收到大量的 「 500 作業逾時 」 HTTP 狀態訊息來自儲存體作業。

> [!NOTE]
> 您可能會看到移動資料分割 tooa 新伺服器負載平衡要求暫時為 hello 儲存體服務的逾時錯誤。
> 
> 

hello **PercentTimeoutError**度量是彙總的 hello 下列度量： **ClientTimeoutError**， **AnonymousClientTimeoutError**， **SASClientTimeoutError**， **ServerTimeoutError**， **AnonymousServerTimeoutError**，和**SASServerTimeoutError**。

hello 伺服器逾時被因 hello 伺服器上發生錯誤。 因為 hello 伺服器上的作業已超過 hello hello client 中; 所指定的逾時，就可能發生 hello 用戶端逾時例如，使用 hello 儲存體用戶端程式庫的用戶端時，可以透過 hello 設定作業逾時**ServerTimeout**屬性 hello **QueueRequestOptions**類別。

伺服器逾時表示發生需要進一步調查的 hello 儲存體服務問題。 如果到達 hello 服務和 tooidentify hello 延展性限制任何爆增情形，可能會造成這個問題的流量，您可以使用標準 toosee。 Hello 問題為間歇性，它可能是因為 tooload 平衡 hello 服務中的活動。 如果 hello 問題持續發生，且不會因達到 hello 服務的 hello 延展性限制的應用程式，您應該要引發的支援問題。 為用戶端逾時，您必須決定是否 hello 逾時，在 hello 用戶端設定 tooan 適當的值以及任一變更 hello 逾時值 hello 用戶端設定，或調查如何改善 hello 作業效能的 hello hello 儲存體服務中，為藉由資料表查詢最佳化或減少 hello 大小的訊息範例。

### <a name="metrics-show-an-increase-in-PercentNetworkError"></a>度量顯示 PercentNetworkError 增加
您的度量顯示其中一個儲存體服務的 **PercentNetworkError** 有增加情況。 hello **PercentNetworkError**度量是彙總的 hello 下列度量： **networkerror 的應用程式**， **AnonymousNetworkError**，和**SASNetworkError**。 Hello 儲存體服務會偵測網路錯誤 hello 用戶端儲存體要求時，會發生這些。

hello 這個錯誤最常見的原因是用戶端 hello 儲存體服務中的逾時到期前中斷連線。 在您的用戶端 toounderstand 為何和何時 hello 用戶端中斷連接從 hello 儲存體服務中，您應該調查 hello 程式碼。 您也可以使用 Wireshark、 Microsoft Message Analyzer 或 hello 用戶端從 Tcping tooinvestigate 網路連線問題。 這些工具，請參閱 hello[附錄]。

### <a name="the-client-is-receiving-403-messages"></a>hello 用戶端收到 HTTP 403 （禁止） 訊息
如果用戶端應用程式會擲回 HTTP 403 （禁止） 錯誤，可能的原因是該 hello 用戶端傳送的儲存體要求 （雖然其他可能的原因包括時鐘誤差，無效的索引鍵，和空白時使用過期共用存取簽章 (SAS)標頭）。 如果已過期的 SAS 金鑰 hello 可能的原因，不會看到 hello 伺服器端儲存體記錄的記錄資料中的任何項目。 hello 下表顯示 hello hello 說明這個問題發生的儲存體用戶端程式庫所產生的用戶端記錄檔中的範例：

| 來源 | 詳細程度 | 詳細程度 | 用戶端要求 ID | 作業內容 |
| --- | --- | --- | --- | --- |
| Microsoft.WindowsAzure.Storage |資訊 |3 |85d077ab-… |從主要位置開始作業 (依據位置模式 PrimaryOnly)。 |
| Microsoft.WindowsAzure.Storage |資訊 |3 |85d077ab -… |啟動同步要求 toohttps://domemaildist.blob.core.windows.netazureimblobcontainer/blobCreatedViaSAS.txt?sv=2014-02-14&amp;sr-iov = c&amp;si = mypolicy&amp;sig = OFnd4Rd7z01fIvh %2bmcr6zbudih2f5ikm%2FyhNYZEmJNQ %3d&amp;api-version = 2014年-02-14。 |
| Microsoft.WindowsAzure.Storage |資訊 |3 |85d077ab -… |等候回應。 |
| Microsoft.WindowsAzure.Storage |警告 |2 |85d077ab -… |等待回應時擲回例外狀況： hello 遠端伺服器傳回錯誤: (403) 禁止... |
| Microsoft.WindowsAzure.Storage |資訊 |3 |85d077ab -… |收到回應。 狀態碼 = 403，要求 ID = 9d67c64a-64ed-4b0d-9515-3b14bbcdc63d，Content-MD5 =，ETag = . |
| Microsoft.WindowsAzure.Storage |警告 |2 |85d077ab -… |Hello 作業期間擲回的例外狀況： hello 遠端伺服器傳回錯誤: (403) 禁止... |
| Microsoft.WindowsAzure.Storage |資訊 |3 |85d077ab -… |檢查是否 hello 應該重新嘗試操作。 重試計數 = 0 時，HTTP 狀態碼 = 403，例外狀況 = hello 遠端伺服器傳回錯誤: (403) 禁止... |
| Microsoft.WindowsAzure.Storage |資訊 |3 |85d077ab -… |hello 下一個位置已經設定 tooPrimary，根據 hello 位置模式。 |
| Microsoft.WindowsAzure.Storage |錯誤 |1 |85d077ab -… |重試原則不允許重試。 失敗與 hello 遠端伺服器傳回錯誤: (403) 禁止。 |

在此案例中，您應該調查原因 hello SAS 權杖即將到期之前 hello 用戶端會傳送 hello 語彙基元 toohello 伺服器：

* 一般而言，您不應該設定當您建立的用戶端 toouse SAS 立即的開始時間。 如果小產生 hello SAS 使用 hello 主機之間時鐘差異 hello 目前時間與 hello 儲存體服務，它就可能會針對 hello 儲存體服務 tooreceive 尚未生效的 SAS。
* 您不應該設定極短暫的 SAS 到期時間。 同樣地，產生的 hello 主機之間的小時鐘差異 hello SAS 和 hello 儲存體服務可能會導致 tooa SAS 明顯比預期提早過期。
* 沒有 hello hello SAS 金鑰中的版本參數 (例如**sv = 2012年-02-12**) 比對 hello 版的 hello 您使用的儲存體用戶端程式庫。 您應該一律使用 hello 的 hello 儲存體用戶端程式庫的最新版本。 如需有關 SAS 權杖 	版本設定，請參閱 [Microsoft Azure 儲存體新功能](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/14/what-s-new-for-microsoft-azure-storage-at-teched-2014.aspx)。
* * 如果您重新產生儲存體存取金鑰 (按一下**管理存取金鑰**hello Azure 傳統入口網站中的儲存體帳戶中的任何頁面上) 可能會使任何現有的 SAS 權杖。 如果您產生 SAS 權杖與用戶端應用程式 toocache 長時間的到期時間，這可能是發生問題。

如果您使用 hello 儲存體用戶端程式庫 toogenerate SAS 權杖，它是簡單 toobuild 有效的語彙基元。 不過，如果您是使用 hello 儲存體 REST API，並以手動方式建構 hello SAS 權杖您應該仔細閱讀 hello 主題<a href="http://msdn.microsoft.com/library/azure/ee395415.aspx" target="_blank">使用共用存取簽章的委派存取</a>MSDN 上。

### <a name="the-client-is-receiving-404-messages"></a>hello 用戶端接收 HTTP 404 （找不到） 訊息
若從 hello 伺服器 hello 用戶端應用程式接收 HTTP 404 （找不到） 訊息時，則表示該 hello 物件 hello 用戶端嘗試 toouse （例如實體、 資料表、 blob、 容器或佇列） 不存在於 hello 儲存體服務。 這種情況有數種可能的原因，例如：

* [hello 用戶端或另一個處理序之前遭到刪除 hello 物件]
* [共用存取簽章 (SAS) 授權問題]
* [用戶端 JavaScript 程式碼沒有權限 tooaccess hello 物件]
* [網路失敗]

#### <a name="client-previously-deleted-the-object"></a>hello 用戶端或另一個處理序之前遭到刪除 hello 物件
Hello 用戶端嘗試 tooread、 更新或刪除資料，通常是對儲存體服務中的案例中輕鬆 tooidentify hello 伺服器端記錄從 hello 儲存體服務中刪除有問題的 hello 物件先前的作業。 通常，hello 記錄資料會顯示另一個使用者或處理序已刪除的 hello 物件。 Hello 伺服器端儲存體記錄 」 記錄檔中，hello 作業類型和要求的物件索引鍵資料行顯示當用戶端刪除物件。

在用戶端嘗試 tooinsert 物件 hello 案例中，它可能不會立即為什麼這會導致 HTTP 404 （找不到） 回應的 hello 用戶端會建立新的物件。 不過，如果 hello 用戶端會建立的 blob，它必須能夠 toofind hello blob 容器，如果 hello 用戶端會建立訊息，它必須能夠 toofind 佇列中，如果 hello 用戶端會將資料列它必須是能夠 toofind hello 資料表。

您可以使用 hello 儲存體用戶端程式庫 toogain 的更詳細的了解當 hello 用戶端傳送的特定要求 toohello 儲存體服務中的 hello 用戶端記錄檔。

hello hello 儲存體用戶端程式庫產生的下列用戶端記錄檔會說明 hello 問題時 hello 用戶端找不到 hello 容器建立 hello blob。 此記錄檔包含 hello 下列儲存體作業的詳細資料：

| 要求 ID | 作業 |
| --- | --- |
| 07b26a5d-... |**DeleteIfExists**方法 toodelete hello blob 容器。 請注意，這項作業包括**HEAD**要求 toocheck hello hello 容器是否存在。 |
| e2d06d78… |**CreateIfNotExists**方法 toocreate hello blob 容器。 請注意，這項作業包括**HEAD**檢查 hello hello 容器是否存在的要求。 hello **HEAD**傳回 404 訊息，但是仍會繼續。 |
| de8b1c3c-... |**UploadFromStream**方法 toocreate hello blob。 hello**放**404 訊息要求會失敗 |

記錄項目：

| 要求 ID | 作業內容 |
| --- | --- |
| 07b26a5d-... |正在啟動 toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer 同步要求。 |
| 07b26a5d-... |StringToSign = HEAD............x-ms-client-request-id:07b26a5d-....x-ms-date:Tue, 03 Jun 2014 10:33:11 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer.restype:container. |
| 07b26a5d-... |等候回應。 |
| 07b26a5d-... |收到回應。 狀態碼 = 200，要求 ID = eeead849-...Content-MD5 =，ETag =    &quot;0x8D14D2DC63D059B&quot;。 |
| 07b26a5d-... |回應標頭已成功處理，與 hello hello 作業其餘部分繼續進行。 |
| 07b26a5d-... |正在下載回應內文。 |
| 07b26a5d-... |作業順利完成。 |
| 07b26a5d-... |正在啟動 toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer 同步要求。 |
| 07b26a5d-... |StringToSign = DELETE............x-ms-client-request-id:07b26a5d-....x-ms-date:Tue, 03 Jun 2014 10:33:12    GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer.restype:container. |
| 07b26a5d-... |等候回應。 |
| 07b26a5d-... |收到回應。 狀態碼 = 202，要求 ID = 6ab2a4cf-...，Content-MD5 = ，ETag = . |
| 07b26a5d-... |回應標頭已成功處理，與 hello hello 作業其餘部分繼續進行。 |
| 07b26a5d-... |正在下載回應內文。 |
| 07b26a5d-... |作業順利完成。 |
| e2d06d78-... |開始非同步要求 toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer。</td> |
| e2d06d78-... |StringToSign = HEAD............x-ms-client-request-id:e2d06d78-....x-ms-date:Tue, 03 Jun 2014 10:33:12 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer.restype:container. |
| e2d06d78-... |等候回應。 |
| de8b1c3c-... |正在啟動 toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer/blobCreated.txt 同步要求。 |
| de8b1c3c-... |StringToSign = PUT...64.qCmF+TQLPhq/YYK50mP9ZQ==........x-ms-blob-type:BlockBlob.x-ms-client-request-id:de8b1c3c-....x-ms-date:Tue, 03 Jun 2014 10:33:12 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer/blobCreated.txt. |
| de8b1c3c-... |正在準備 toowrite 要求資料。 |
| e2d06d78-... |等待回應時擲回例外狀況： hello 遠端伺服器傳回錯誤: (404) 找不到資料庫... |
| e2d06d78-... |收到回應。 狀態碼 = 404，要求 ID = 353ae3bc-...，Content-MD5 = ，ETag = . |
| e2d06d78-... |回應標頭已成功處理，與 hello hello 作業其餘部分繼續進行。 |
| e2d06d78-... |正在下載回應內文。 |
| e2d06d78-... |作業順利完成。 |
| e2d06d78-... |開始非同步要求 toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer。 |
| e2d06d78-... |StringToSign = PUT...0.........x-ms-client-request-id:e2d06d78-....x-ms-date:Tue, 03 Jun 2014 10:33:12 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer.restype:container. |
| e2d06d78-... |等候回應。 |
| de8b1c3c-... |正在寫入要求資料。 |
| de8b1c3c-... |等候回應。 |
| e2d06d78-... |等待回應時擲回例外狀況： hello 遠端伺服器傳回錯誤: (409) 衝突... |
| e2d06d78-... |收到回應。 狀態碼 = 409，要求 ID = c27da20e-...，Content-MD5 = ，ETag = . |
| e2d06d78-... |正在下載錯誤回應內文。 |
| de8b1c3c-... |等待回應時擲回例外狀況： hello 遠端伺服器傳回錯誤: (404) 找不到資料庫... |
| de8b1c3c-... |收到回應。 狀態碼 = 404，回應 ID = 0eaeab3e-...，Content-MD5 = ，ETag = . |
| de8b1c3c-... |Hello 作業期間擲回的例外狀況： hello 遠端伺服器傳回錯誤: (404) 找不到資料庫... |
| de8b1c3c-... |重試原則不允許重試。 失敗與 hello 遠端伺服器傳回錯誤: (404) 找不到資料庫... |
| e2d06d78-... |重試原則不允許重試。 失敗與 hello 遠端伺服器傳回錯誤: (409) 衝突... |

在此範例中，hello 記錄檔會顯示該 hello 用戶端會交錯源自 hello **CreateIfNotExists**方法 (...要求識別碼 e2d06d78) 與 hello 源自 hello **UploadFromStream**方法 (de8b1c3c-...）。發生此問題因為 hello 用戶端應用程式會叫用這些方法以非同步的方式。 您應該修改它建立 hello 容器嘗試 tooupload 任何資料 tooa blob 容器中的 hello 用戶端 tooensure hello 非同步程式碼。 理想的情況是，您應該事先建立所有容器。

#### <a name="SAS-authorization-issue"></a>共用存取簽章 (SAS) 授權問題
如果 hello 用戶端應用程式嘗試 toouse 不包含 hello hello 作業的必要權限的 SAS 金鑰，hello 儲存體服務會傳回 HTTP 404 （找不到） 訊息 toohello 用戶端。 在 hello 相同時，您也會看到的非零值**SASAuthorizationError** hello 標準中。

hello 下表顯示從 hello 儲存體記錄 」 記錄檔的範例伺服器端記錄檔訊息：

| 名稱 | 值 |
| --- | --- |
| 要求開始時間 | 2014-05-30T06:17:48.4473697Z |
| 作業類型     | GetBlobProperties            |
| 要求狀態     | SASAuthorizationError        |
| HTTP 狀態碼   | 404                          |
| 驗證類型| Sas                          |
| 服務類型       | Blob                         |
| 要求 URL        | https://domemaildist.blob.core.windows.net/azureimblobcontainer/blobCreatedViaSAS.txt |
| nbsp;              |   ?sv=2014-02-14&sr=c&si=mypolicy&sig=XXXXX&;api-version=2014-02-14 |
| 要求 ID 標頭  | a1f348d5-8032-4912-93ef-b393e5252a3b |
| 用戶端要求 ID  | 2d064953-8436-4ee0-aa0c-65cb874f7929 |

您應該調查為什麼用戶端應用程式正在嘗試 tooperform 它未被授與的權限的作業。

#### <a name="JavaScript-code-does-not-have-permission"></a>用戶端 JavaScript 程式碼沒有權限 tooaccess hello 物件
如果您使用 JavaScript 用戶端 hello 儲存體服務傳回 HTTP 404 訊息，您檢查下列 hello 瀏覽器中的 JavaScript 錯誤 hello:

```
SEC7120: Origin http://localhost:56309 not found in Access-Control-Allow-Origin header.
SCRIPT7002: XMLHttpRequest: Network Error 0x80070005, Access is denied.
```

> [!NOTE]
> 您可以使用 hello F12 開發人員工具，您會將用戶端 JavaScript 問題進行疑難排解時，hello 瀏覽器和 hello 儲存體服務之間交換的 Internet Explorer tootrace hello 訊息中。
> 
> 

這些錯誤的發生原因 hello web 瀏覽器實作 hello<a href="http://www.w3.org/Security/wiki/Same_Origin_Policy" target="_blank">相同來源原則</a>來自於可防止網頁呼叫 hello 網域 hello 頁面上的不同網域中的應用程式開發介面的安全性限制。

toowork 周圍 hello JavaScript 問題，您可以設定跨原始資源共用 (CORS) hello 儲存體服務 hello 用戶端正在存取。 如需詳細資訊，請參閱 MSDN 上的 <a href="http://msdn.microsoft.com/library/azure/dn535601.aspx" target="_blank">Azure 儲存體服務的跨來源資源共用 (CORS) 支援</a>。

hello，下列程式碼範例顯示如何 tooconfigure 您的 blob 服務 tooallow JavaScript hello Contoso 網域 tooaccess 中執行您的 blob 儲存體服務中的 blob:

```csharp
CloudBlobClient client = new CloudBlobClient(blobEndpoint, new StorageCredentials(accountName, accountKey));
// Set hello service properties.
ServiceProperties sp = client.GetServiceProperties();
sp.DefaultServiceVersion = "2013-08-15";
CorsRule cr = new CorsRule();
cr.AllowedHeaders.Add("*");
cr.AllowedMethods = CorsHttpMethods.Get | CorsHttpMethods.Put;
cr.AllowedOrigins.Add("http://www.contoso.com");
cr.ExposedHeaders.Add("x-ms-*");
cr.MaxAgeInSeconds = 5;
sp.Cors.CorsRules.Clear();
sp.Cors.CorsRules.Add(cr);
client.SetServiceProperties(sp);
```

#### <a name="network-failure"></a>網路失敗
在某些情況下，遺失的網路封包可能會導致 toohello 儲存體服務會傳回 HTTP 404 訊息 toohello 用戶端。 例如，用戶端應用程式從 hello 表格服務中刪除實體時您看到 hello 用戶端擲回儲存體例外狀況報告 「 HTTP 404 （找不到） 」 與 hello 表格服務的狀態訊息。 當您調查 hello 資料表儲存體服務中的 hello 資料表時，您會看到 hello 服務未刪除 hello 實體，因為要求。

hello hello 用戶端中的例外狀況詳細資料包括指派 hello 表格服務的 hello 要求 hello 要求識別碼 (7e84f12d...): 您可以使用此資訊 toolocate hello 要求詳細資料中 hello 伺服器端儲存體記錄搜尋中 hello **要求識別碼標頭**hello 記錄檔中的資料行。 您也可以使用 hello 度量 tooidentify 時失敗，例如這發生，然後搜尋 hello 根據 hello 時間 hello 度量的記錄檔記錄這個錯誤。 Hello 刪除此記錄項目顯示失敗並出現 「 HTTP (404) 用戶端其他錯誤 」 狀態訊息。 hello 相同記錄檔項目也包括 hello hello hello 中的用戶端所產生的要求識別碼**用戶端要求 id**資料行 (813ea74f...)。

hello 伺服器端記錄檔也包含另一個項目以 hello 相同**用戶端要求 id**值 (813ea74f...) 成功刪除作業 hello 相同的實體，並從 hello 相同用戶端。 這項作業成功刪除 hello 無法的刪除要求之前的非常短時間內發生。

此案例的 hello 最可能的原因是傳送 hello 實體 toohello 資料表服務成功，但未收到收條 hello 伺服器 （可能是因為 tooa 暫時性網路問題） 將 delete 要求該 hello 用戶端。 hello 用戶端再自動重試 hello 作業 (使用 hello 相同**用戶端要求 id**)，且此重試失敗，因為 hello 實體已被刪除。

如果此問題持續發生，您應該調查 hello 用戶端為何無法 tooreceive hello 表格服務發出的通知。 如果 hello 問題為間歇性，您應該捕捉 hello 「 HTTP (404) 找不到 」 錯誤和記錄在 hello 用戶端，但允許 hello 用戶端 toocontinue。

### <a name="the-client-is-receiving-409-messages"></a>hello 用戶端接收 HTTP 409 （衝突） 訊息
hello 下表顯示內容擷取自兩個用戶端作業的 hello 伺服器端記錄： **DeleteIfExists**立即接著**CreateIfNotExists**使用 hello 相同的 blob 容器名稱。 請注意，每個用戶端作業會導致兩個要求傳送 toohello server，第一次**GetContainerProperties**要求 toocheck hello 容器已存在，後面再接著 hello **DeleteContainer**或**CreateContainer**要求。

| Timestamp | 作業 | 結果 | 容器名稱 | 用戶端要求 ID |
| --- | --- | --- | --- | --- |
| 05:10:13.7167225 |GetContainerProperties |200 |mmcont |c9f52c89-… |
| 05:10:13.8167325 |DeleteContainer |202 |mmcont |c9f52c89-… |
| 05:10:13.8987407 |GetContainerProperties |404 |mmcont |bc881924-… |
| 05:10:14.2147723 |CreateContainer |409 |mmcont |bc881924-… |

hello hello 用戶端應用程式中的程式碼會刪除，然後立即重新建立 blob 容器使用 hello 相同的名稱： hello **CreateIfNotExists**方法 （用戶端要求 ID bc881924-...） 會因 hello HTTP 409 （衝突），最後發生錯誤。 當用戶端刪除 blob 容器、 資料表或佇列沒有之前一小段時間 hello 名稱再次變為無法使用。

hello 用戶端應用程式應該使用唯一容器名稱，只要它會建立新的容器，如果常 hello 刪除/重新建立模式。

### <a name="metrics-show-low-percent-success"></a>度量顯示低 PercentSuccess，或是分析記錄項目內含具有 ClientOtherErrors 交易狀態的作業項目
hello **PercentSuccess**度量擷取的作業都順利完成其 HTTP 狀態碼為基礎的 hello 百分比。 作業的狀態碼 2XX 計數為成功，而與 3XX、 4XX 和 5XX 範圍中的狀態碼的作業會視為不成功和較低的 hello **PercentSucess**公制值。 在 hello 伺服器端儲存記錄檔，這些作業會記錄交易狀態為**ClientOtherErrors**。

這些作業已成功完成，因此不會影響其他度量資訊，例如可用性的重要 toonote 它。 以下作業範例顯示作業已成功執行，但卻出現不成功的 HTTP 狀態碼：

* **ResourceNotFound** (未找到 404)，例如從 GET tooa blob，要求不存在。
* **ResouceAlreadyExists** (409 衝突)，例如從**CreateIfNotExist** hello 資源已經存在的作業。
* **ConditionNotMet** (未修改 304)，例如從的條件式作業，例如當用戶端傳送**ETag**值和 HTTP**如果 If-none-Match**標頭 toorequest 影像才hello 最後一個作業之後更新。

您可以找到常見 REST API 錯誤碼 hello 儲存體服務會傳回在 hello 頁面上的一份<a href="http://msdn.microsoft.com/library/azure/dd179357.aspx" target="_blank">常見的 REST API 錯誤碼</a>。

### <a name="capacity-metrics-show-an-unexpected-increase"></a>容量度量顯示非預期的儲存體容量使用增加
如果您看到突然，突如其來的變化容量使用量，在儲存體帳戶，您可以調查 hello 原因第一次查看可用性度量資訊。比方說，無法的刪除要求的 hello 數目的增加可能導致 tooan 增加中您用來當做應用程式特定的清除作業，您可能預期 toobe 釋放的空間可能不會如預期般運作 （適用於 blob 儲存體的 hello 數量範例中，因為用來釋放空間 hello SAS 權杖已過期)。

### <a name="you-are-experiencing-unexpected-reboots"></a>附加大量 VHD 的 Azure 虛擬機器出現非預期的重新開機情況
如果在 Azure 虛擬機器 (VM) 具有大量的 hello 中附加 Vhd 相同的儲存體帳戶，您可能會超出 hello 造成 hello VM toofail 個人儲存體帳戶的延展性目標。 您應該檢查 hello hello 儲存體帳戶的分鐘度量 (**TotalRequests**/**TotalIngress**/**TotalEgress**) 尖峰超過 hello 延展性目標儲存體帳戶。 參閱 hello"[度量顯示 PercentThrottlingError 增加]」 的協助判斷節流發生儲存體帳戶。

一般情況下，每個個別的輸入或輸出作業，從虛擬機器的 VHD 上會轉譯太**取得頁面**或**Put Page** hello 基礎分頁 blob 上的作業。 因此，您可以使用 hello IOPS 的估計環境 tootune 多少 Vhd，您可以在單一儲存體帳戶中根據擁有 hello 應用程式的特定行為。 我們不建議單一儲存體帳戶內具備超過 40 的磁碟。 請參閱<a href="http://msdn.microsoft.com/library/azure/dn249410.aspx" target="_blank">Azure 儲存體延展性和效能目標</a>如 hello 目前延展性目標儲存體帳戶的詳細資訊，特別是 hello 總要求率和總頻寬為 hello 類型的儲存體帳戶使用.
如果您已超過 hello 延展性目標儲存體帳戶，您應該將您的 Vhd，多個不同的儲存體帳戶 tooreduce hello 活動中每個個別的帳戶。

### <a name="your-issue-arises-from-using-the-storage-emulator"></a>您的問題就會發生從開發或測試使用 hello 儲存體模擬器
通常，您會在開發期間使用 hello 儲存體模擬器並測試 tooavoid hello Azure 儲存體帳戶的需求。 當您使用 hello 儲存體模擬器可能會發生的 hello 一般問題包括：

* [功能"X"hello 儲存體模擬器中無法運作]
* [錯誤 「 hello 其中一個 hello HTTP 標頭的值不正確格式的 hello 中 」 時使用 hello 儲存體模擬器]
* [執行中的 hello 儲存體模擬器需要系統管理權限]

#### <a name="feature-X-is-not-working"></a>功能"X"hello 儲存體模擬器中無法運作
hello 儲存體模擬器不支援的所有 hello hello Azure 儲存體服務，例如 hello 檔案服務功能。 如需詳細資訊，請參閱<a href="http://msdn.microsoft.com/library/azure/gg433135.aspx" target="_blank">之間的差異 hello 儲存體模擬器和 Azure 儲存體服務</a>MSDN 上。

Hello 儲存那些功能的模擬器不支援，使用 hello 雲端中的 hello Azure 儲存體服務。

#### <a name="error-HTTP-header-not-correct-format"></a>錯誤 「 hello 其中一個 hello HTTP 標頭的值不正確格式的 hello 中 」 時使用 hello 儲存體模擬器
您要測試您的應用程式使用 hello 儲存體用戶端程式庫針對 hello 本機儲存體模擬器和方法呼叫，例如**CreateIfNotExists**失敗，並且 hello 錯誤訊息 「 hello 其中一個 hello HTTP 標頭的值不是在hello 正確格式。 」 這表示該 hello hello 您使用的儲存體模擬器版本不支援 hello hello 儲存體用戶端程式庫會使用的版本。 hello 儲存體用戶端程式庫將 hello 標頭加入**x ms 版本**tooall hello 要求它。 如果 hello 儲存體模擬器無法辨識 hello 中的 hello 值**x ms 版本**標頭，它會拒絕 hello 要求。

您可以使用 hello 存放媒體櫃用戶端記錄檔 toosee hello 值 hello **x ms 版本標頭**傳送。 您也可以查看 hello hello 值**x ms 版本標頭**如果您使用 Fiddler tootrace hello 要求從用戶端應用程式。

如果您安裝並使用 hello 的 hello 儲存體用戶端程式庫的最新版本，而無須更新 hello 儲存體模擬器，通常就會發生這種情況。 您應該安裝 hello hello 儲存體模擬器，最新版本，或使用，而非 hello 模擬器雲端存放裝置開發和測試。

#### <a name="storage-emulator-requires-administrative-privileges"></a>執行中的 hello 儲存體模擬器需要系統管理權限
當您執行 hello 儲存體模擬器時，會提示系統管理員認證。 這只會發生您要初始化 hello 儲存體模擬器進行 hello 第一次。 初始化 hello 儲存體模擬器之後，您不需要系統管理權限 toorun 再試一次。

如需詳細資訊，請參閱<a href="http://msdn.microsoft.com/library/azure/gg433132.aspx" target="_blank">所使用 hello 命令列工具初始化 hello 儲存體模擬器</a>msdn （您也可以初始化 hello 儲存體模擬器，在 Visual Studio 中，也需要系統管理權限）。

### <a name="you-are-encountering-problems-installing-the-Windows-Azure-SDK"></a>您遇到安裝 hello Azure SDK for.NET 的問題
當您嘗試 tooinstall hello SDK 時，它無法嘗試 tooinstall hello 儲存體模擬器在本機電腦上。 hello 安裝記錄檔包含下列訊息的 hello 的其中一個：

* CAQuietExec： 錯誤： 無法 tooaccess SQL 執行個體
* CAQuietExec： 錯誤： 無法 toocreate 資料庫

hello 的原因是現有的 LocalDB 安裝的問題。 根據預設，hello 儲存體模擬器會使用 LocalDB toopersist 資料時，它會模擬 hello Azure 儲存體服務。 您可以執行下列命令，在命令提示字元視窗中的嘗試 tooinstall hello SDK 之前的 hello 來重設您的 LocalDB 執行個體。

```
sqllocaldb stop v11.0
sqllocaldb delete v11.0
delete %USERPROFILE%\WAStorageEmulatorDb3*.*
sqllocaldb create v11.0
```

hello**刪除**命令會移除先前安裝的 hello 儲存體模擬器中的任何舊的資料庫檔案。

### <a name="you-have-a-different-issue-with-a-storage-service"></a>您的儲存體服務出現其他問題
如果 hello 先前的疑難排解章節未包含有與儲存體服務的 hello 問題，您應該採用 hello 遵循方法 toodiagnosing 和疑難排解您的問題。

* 如果沒有從您的預期基準線行為的任何變更，請檢查度量 toosee。 從 hello 度量，您可能無法 toodetermine 是否 hello 問題是暫時性或永久性，以及哪一個儲存體作業 hello 問題會影響。
* 您可以使用 hello toohelp 搜尋您所發生的任何錯誤的詳細資訊的伺服器端記錄資料的度量資訊。 這項資訊可以協助您疑難排解並解決 hello 問題。
* 如果 hello 伺服器端記錄檔中的 hello 資訊不足夠 tootroubleshoot hello 問題成功，您可以使用 hello 儲存體用戶端程式庫用戶端記錄檔 tooinvestigate hello 行為的用戶端應用程式和 Fiddler Wireshark 之類的工具Microsoft Message Analyzer tooinvestigate 和您的網路。

如需有關如何使用 Fiddler 的詳細資訊，請參閱 「[附錄 1： 使用 Fiddler toocapture HTTP 及 HTTPS 流量]。 」

如需使用 Wireshark 的詳細資訊，請參閱 「[附錄 2： 使用 Wireshark toocapture 網路流量]。 」

如需有關使用 Microsoft Message Analyzer 的詳細資訊，請參閱 「[附錄 3： 使用 Microsoft Message Analyzer toocapture 網路流量]。 」

## <a name="appendices"></a>附錄
hello 附錄說明數個工具，診斷和疑難排解 Azure 儲存體 （和其他服務） 的問題時可能非常有用。 這些工具並非 Azure 儲存體內建的工具，有些則是協力廠商的產品。 因此，若這些附錄中所討論的 hello 工具未涵蓋的任何支援協議，您可能與 Microsoft Azure 或 Azure 儲存體，而因此做為您的評估程序的一部分，您應該檢查提供的 hello 授權和支援選項這些工具的 hello 提供者。

### <a name="appendix-1"></a>附錄 1： 使用 Fiddler toocapture HTTP 和 HTTPS 流量
Fiddler 會相當有用的工具來分析您的用戶端應用程式與 hello 您使用的 Azure 儲存體服務之間的 hello HTTP 及 HTTPS 流量。 您可以從 <a href="http://www.telerik.com/fiddler" target="_blank">http://www.telerik.com/fiddler</a> 下載 Fiddler。

> [!NOTE]
> Fiddler 可解碼 HTTPS 流量。您應該仔細閱讀 hello Fiddler 文件 toounderstand 解其運作，以及 toounderstand hello 安全性含義。
> 
> 

本附錄提供簡短的逐步解說的 tooconfigure Fiddler toocapture hello 本機電腦已安裝 Fiddler 與 hello Azure 儲存體服務的位置之間的流量。

Fiddler 一經啟動後，就會開始擷取本機電腦上的 HTTP 與 HTTPS 流量。 hello 以下是一些有用的命令控制 Fiddler:

* 停止與開始擷取流量。 Hello 主功能表上，前往 太**檔案**，然後按一下**擷取流量**tootoggle 擷取開啟和關閉。
* 儲存擷取的流量資料。 Hello 主功能表上，前往 太**檔案**，按一下 **儲存**，然後按一下**所有工作階段**： 這可讓您在工作階段封存檔 toosave hello 流量。 您可以重新載入工作階段保存稍後進行分析，或如果要求 tooMicrosoft 支援傳送。

toolimit hello 數量 Fiddler 擷取的流量，您可以使用您在 hello 中設定的篩選**篩選** 索引標籤 hello 下列螢幕擷取畫面顯示擷取唯一傳送的流量 toohello 篩選**contosoemaildist.table.core.windows.net**儲存體端點：

![][5]

### <a name="appendix-2"></a>附錄 2： 使用 Wireshark toocapture 網路流量
Wireshark 是網路通訊協定分析器，可讓您 tooview 封包的詳細資訊廣泛的網路通訊協定。 您可以從 <a href="http://www.wireshark.org/" target="_blank">http://www.wireshark.org/</a> 下載 Wireshark。

hello 下列程序顯示如何 toocapture 封包的詳細資訊從 hello 本機電腦的流量 Wireshark toohello 表格服務安裝在您的 Azure 儲存體帳戶。

1. 在本機電腦上啟動 Wireshark。
2. 在 hello**啟動**區段、 選取 hello 區域網路介面或介面所連接的 toohello 網際網路。
3. 按一下 [擷取選項] 。
4. 新增篩選器 toohello**擷取篩選器**文字方塊。 例如，**裝載 contosoemaildist.table.core.windows.net**傳送 tooor 從 hello 表格服務端點中 hello 封包只會設定 Wireshark toocapture **contosoemaildist**儲存體帳戶。 如需「擷取篩選器」的完整清單，請參閱 <a href="http://wiki.wireshark.org/CaptureFilters" target="_blank">http://wiki.wireshark.org/CaptureFilters</a>。
   
   ![][6]
5. 按一下 [啟動] 。 Wireshark 現在將會擷取所有 hello 封包傳送嗨表格服務端點從 tooor，當您在本機電腦上使用用戶端應用程式。
6. 當您完成時，在 hello 主功能表上，按一下**擷取**然後**停止**。
7. toosave hello 擷取資料 Wireshark 擷取檔案中，hello 主功能表上，按一下**檔案**然後**儲存**。

WireShark 會反白顯示 hello 存在於任何錯誤**packetlist**視窗。 您也可以使用 hello**專家資訊**視窗 (按一下**分析**，然後**專家資訊**) tooview 的錯誤和警告摘要。

![][7]

您也可以選擇 tooview hello TCP 資料，因為 hello 應用程式層會看見 hello TCP 資料上按一下滑鼠右鍵，然後選取它**遵循 TCP 資料流**。 當您不使用擷取篩選器而擷取到傾印時，這個方法會特別有用。 如需詳細資訊，請參閱<a href="http://www.wireshark.org/docs/wsug_html_chunked/ChAdvFollowTCPSection.html" target="_blank">這裡</a>。

![][8]

> [!NOTE]
> 如需有關使用 Wireshark 的詳細資訊，請參閱 hello <a href="http://www.wireshark.org/docs/wsug_html_chunked/" target="_blank">Wireshark 使用者指南</a>。
> 
> 

### <a name="appendix-3"></a>附錄 3： 使用 Microsoft Message Analyzer toocapture 網路流量
您可以在類似的方式 tooFiddler，使用 Microsoft Message Analyzer toocapture HTTP 和 HTTPS 流量，並擷取類似的方式 tooWireshark 的網路流量。

#### <a name="configure-a-web-tracing-session-using-microsoft-message-analyzer"></a>使用 Microsoft Message Analyzer 設定 Web 追蹤工作階段
web 追蹤工作階段使用 Microsoft Message Analyzer，執行 hello Microsoft Message Analyzer 應用程式的 HTTP 與 HTTPS 流量然後再針對 hello tooconfigure**檔案**功能表上，按一下 **擷取/追蹤**。 在可用的追蹤案例的 hello 清單中選取**Web Proxy**。 接著在 hello**追蹤案例設定**面板 中 hello **HostnameFilter**文字方塊中，加入您的儲存體端點 （您可以查詢這些 hello Azure 傳統入口網站中的名稱） 的 hello 名稱。 比方說，如果 hello Azure 儲存體帳戶名稱是**contosodata**，您應該將新增下列 toohello hello **HostnameFilter**文字方塊中：

```
contosodata.blob.core.windows.net contosodata.table.core.windows.net contosodata.queue.core.windows.net
```

> [!NOTE]
> 空格字元會分隔 hello 主機名稱。
> 
> 

當您準備好 toostart 收集追蹤資料，請按一下 hello **Start With**  按鈕。

如需有關 Microsoft Message Analyzer hello **Web Proxy**追蹤，請參閱<a href="http://technet.microsoft.com/library/jj674814.aspx" target="_blank">PEF WebProxy 提供者</a>TechNet 上。

內建的 hello **Web Proxy** Microsoft Message Analyzer 中的追蹤根據 Fiddler; 它可以擷取用戶端的 HTTPS 流量，並顯示未加密的 HTTPS 訊息。 hello **Web Proxy**追蹤適用於設定本機 proxy，讓它存取 toounencrypted 訊息的所有 HTTP 和 HTTPS 流量。

#### <a name="diagnosing-network-issues-using-microsoft-message-analyzer"></a>使用 Microsoft Message Analyzer 診斷網路問題
此外 toousing hello Microsoft Message Analyzer **Web Proxy**追蹤 toocapture 詳細資料的 hello hello 用戶端應用程式與 hello 儲存體服務之間的 HTTP/HTTPs 流量，您也可以使用 hello 內建**本機連結層**追蹤 toocapture 網路封包資訊。 這樣做可讓您 toocapture 資料類似 toothat 您可以擷取與 Wireshark 及診斷網路問題例如丟棄的封包。

hello 下列螢幕擷取畫面顯示範例**本機連結層**追蹤某些**資訊**中 hello 訊息**DiagnosisTypes**資料行。 按一下圖示在 hello **DiagnosisTypes**資料行會顯示 hello hello 訊息詳細資料。 在此範例中，hello 伺服器重新傳輸訊息 #305，因為它未收到收條 hello 用戶端：

![][9]

當您在 Microsoft Message Analyzer 建立 hello 追蹤工作階段時，您可以指定篩選器 tooreduce hello 雜訊數量 hello 追蹤中。 在 hello**擷取 / 追蹤**可讓您定義 hello 追蹤頁面按一下 hello**設定**連結旁太**Microsoft Windows-NDIS PacketCapture**。 下列螢幕擷取畫面的 hello 顯示 hello 三個儲存體服務的 IP 位址的 TCP 流量篩選器的組態：

![][10]

如需 hello Microsoft 郵件分析器本機連結層級追蹤的詳細資訊，請參閱<a href="http://technet.microsoft.com/library/jj659264.aspx" target="_blank">PEF-NDIS-PacketCapture 提供者</a>TechNet 上。

### <a name="appendix-4"></a>附錄 4： 使用 Excel tooview 度量和記錄資料
許多工具，可讓您從 Azure 資料表儲存體中分隔的格式，可輕鬆 tooload hello 資料的 excel 檢視及分析 toodownload hello 儲存體度量資料。 來自 Azure Blob 儲存體的儲存體記錄資料已經使用分隔格式，方便您直接載入 Excel。 不過，您將需要以 hello 資訊為基礎的 tooadd 適當的資料行標題<a href="http://msdn.microsoft.com/library/azure/hh343259.aspx" target="_blank">儲存體分析記錄格式</a>和<a href="http://msdn.microsoft.com/library/azure/hh343264.aspx" target="_blank">儲存體分析度量資料表結構描述</a>。

tooimport 儲存體記錄資料至 Excel 之後您下載它從 blob 儲存體：

* 在 hello**資料**功能表上，按一下 **從文字**。
* 瀏覽 toohello 記錄檔要 tooview**匯入**。
* 在步驟 1 的 hello**文字匯入精靈**，選取**分隔**。

在步驟 1 的 hello**文字匯入精靈**，選取**分號**為 hello 唯一分隔符號，然後選擇 為 hello 雙引號**文字限定詞**。 然後按一下 **完成**選擇 tooplace hello 活頁簿中的位置。

### <a name="appendix-5"></a>附錄 5：使用 Application Insights for Visual Studio Team Services 監視
您也可以使用 hello Application Insights 功能 Visual Studio Team Services 的效能和可用性監視的一部分。 這項工具可以：

* 確保您的 Web 服務可用且迅速回應。 無論您的應用程式的網站或裝置應用程式，使用 web 服務，可從各地 hello world，測試您的 URL 每隔幾分鐘並可讓您知道是否有問題。
* 快速診斷 Web 服務中的任何效能問題或例外。 了解 CPU 或其他資源是否過度使用，從例外中取得堆疊追蹤資料，並且輕鬆地搜尋記錄追蹤項目。 如果 hello 應用程式的效能低於可接受的限制，我們可以傳送給您電子郵件。 我們可以同時監視 .NET 與 Java Web 服務。

在 hello 時間寫入 Application Insights 處於預覽狀態。 您可以在 <a href="http://msdn.microsoft.com/library/azure/dn481095.aspx" target="_blank">MSDN 上的 Application Insights for Visual Studio Team Services</a> 找到更多資訊。

<!--Anchors-->
[簡介]: #introduction
[本指南架構]: #how-this-guide-is-organized

[監視儲存體服務]: #monitoring-your-storage-service
[監視服務健康情況]: #monitoring-service-health
[監視容量]: #monitoring-capacity
[監視可用性]: #monitoring-availability
[監視效能]: #monitoring-performance

[診斷儲存體問題]: #diagnosing-storage-issues
[服務健康情況問題]: #service-health-issues
[效能問題]: #performance-issues
[診斷錯誤]: #diagnosing-errors
[儲存體模擬器問題]: #storage-emulator-issues
[儲存體記錄工具]: #storage-logging-tools
[使用網路記錄工具]: #using-network-logging-tools

[端對端追蹤]: #end-to-end-tracing
[為記錄資料建立相互關聯]: #correlating-log-data
[用戶端要求 ID]: #client-request-id
[伺服器要求 ID]: #server-request-id
[時間戳記]: #timestamps

[疑難排解指引]: #troubleshooting-guidance
[度量顯示高 AverageE2ELatency 和低 AverageServerLatency]: #metrics-show-high-AverageE2ELatency-and-low-AverageServerLatency
[度量顯示低 AverageE2ELatency 和低 AverageServerLatency 但 hello 用戶端發生高延遲]: #metrics-show-low-AverageE2ELatency-and-low-AverageServerLatency
[度量顯示高 AverageServerLatency]: #metrics-show-high-AverageServerLatency
[佇列上的訊息在遞送期間出現非預期的延遲]: #you-are-experiencing-unexpected-delays-in-message-delivery

[度量顯示 PercentThrottlingError 增加]: #metrics-show-an-increase-in-PercentThrottlingError
[PercentThrottlingError 的暫時性增加]: #transient-increase-in-PercentThrottlingError
[PercentThrottlingError 錯誤中的永久性增加]: #permanent-increase-in-PercentThrottlingError
[度量顯示 PercentTimeoutError 增加]: #metrics-show-an-increase-in-PercentTimeoutError
[度量顯示 PercentNetworkError 增加]: #metrics-show-an-increase-in-PercentNetworkError

[hello 用戶端收到 HTTP 403 （禁止） 訊息]: #the-client-is-receiving-403-messages
[hello 用戶端接收 HTTP 404 （找不到） 訊息]: #the-client-is-receiving-404-messages
[hello 用戶端或另一個處理序之前遭到刪除 hello 物件]: #client-previously-deleted-the-object
[共用存取簽章 (SAS) 授權問題]: #SAS-authorization-issue
[用戶端 JavaScript 程式碼沒有權限 tooaccess hello 物件]: #JavaScript-code-does-not-have-permission
[網路失敗]: #network-failure
[hello 用戶端接收 HTTP 409 （衝突） 訊息]: #the-client-is-receiving-409-messages

[度量顯示低 PercentSuccess 或分析記錄檔項目所使用的作業交易狀態的 ClientOtherErrors]: #metrics-show-low-percent-success
[容量度量顯示非預期的儲存體容量使用增加]: #capacity-metrics-show-an-unexpected-increase
[附加大量 VHD 的虛擬機器，出現非預期的重新開機情況]: #you-are-experiencing-unexpected-reboots
[您的問題就會發生從開發或測試使用 hello 儲存體模擬器]: #your-issue-arises-from-using-the-storage-emulator
[功能"X"hello 儲存體模擬器中無法運作]: #feature-X-is-not-working
[錯誤 「 hello 其中一個 hello HTTP 標頭的值不正確格式的 hello 中 」 時使用 hello 儲存體模擬器]: #error-HTTP-header-not-correct-format
[執行中的 hello 儲存體模擬器需要系統管理權限]: #storage-emulator-requires-administrative-privileges
[您遇到安裝 hello Azure SDK for.NET 的問題]: #you-are-encountering-problems-installing-the-Windows-Azure-SDK
[您的儲存體服務出現其他問題]: #you-have-a-different-issue-with-a-storage-service

[附錄]: #appendices
[附錄 1： 使用 Fiddler toocapture HTTP 及 HTTPS 流量]: #appendix-1
[附錄 2： 使用 Wireshark toocapture 網路流量]: #appendix-2
[附錄 3： 使用 Microsoft Message Analyzer toocapture 網路流量]: #appendix-3
[附錄 4： 使用 Excel tooview 度量和記錄資料]: #appendix-4
[附錄 5： 監視與 Application Insights for Visual Studio Team Services]: #appendix-5

<!--Image references-->
[1]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/overview.png
[2]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/portal-screenshot.png
[3]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/hour-minute-metrics.png
[4]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/high-e2e-latency.png
[5]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/fiddler-screenshot.png
[6]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/wireshark-screenshot-1.png
[7]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/wireshark-screenshot-2.png
[8]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/wireshark-screenshot-3.png
[9]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/mma-screenshot-1.png
[10]: ./media/storage-monitoring-diagnosing-troubleshooting-classic-portal/mma-screenshot-2.png
