---
title: "對應方案 aaaService 自我進度的示範 |Microsoft 文件"
description: "服務對應是一種解決方案中 Operations Management Suite (OMS)，會自動探索 Windows 上的應用程式元件和 Linux 系統和對應 hello 服務之間的通訊。  這是本身的步調的示範逐步解說使用服務對應 tooidentify 並診斷在 web 應用程式的模擬的問題。"
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 9dc437b9-e83c-45da-917c-cb4f4d8d6333
ms.service: operations-management-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: bwren
ms.openlocfilehash: 13f26241cd55a9b35c07d6ca52760a968abffc64
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="operations-management-suite-oms-self-paced-demo---service-map"></a>Operations Management Suite (OMS) 自學示範 - 服務對應
這是引導使用 hello 本身進度的示範[服務對應方案](operations-management-suite-service-map.md)在 Operations Management Suite (OMS) tooidentify 及診斷中的 web 應用程式的模擬的問題。  服務對應會自動探索 Windows 和 Linux 系統上的應用程式元件和對應 hello 服務之間的通訊。  它也會合併其他 OMS 服務 tooassist 所收集的資料中分析效能，並識別問題。  您也可以使用[記錄中記錄分析搜尋](../log-analytics/log-analytics-log-searches.md)toodrill 關閉收集中的資料順序 tooidentify hello 根本問題。


## <a name="scenario-description"></a>案例描述
您所收到 hello ACME 客戶入口網站應用程式發生效能問題的通知。  您擁有 hello 唯一資訊是這些問題啟動大約 4:00 am PST 今天。  您不確定所有 hello 元件該 hello 入口網站，是根據一組 web 伺服器以外。  

## <a name="components-and-features-used"></a>使用的元件和功能
- [服務對應解決方案](operations-management-suite-service-map.md)
- [Log Analytics 記錄搜尋](../log-analytics/log-analytics-log-searches.md)


## <a name="walk-through"></a>逐步解說

### <a name="1-connect-toohello-oms-experience-center"></a>1.連接 toohello OMS 經驗 Center
這個逐步解說會使用 hello [Operations Management Suite 經驗 Center](https://experience.mms.microsoft.com/)以提供完整的 OMS 環境，其中範例資料。 開始依照此連結，提供您的資訊，然後選取 hello**深入剖析和分析**案例。


### <a name="2-start-service-map"></a>2.啟動服務對應
按一下 hello 啟動 hello 服務對應解決方案**服務對應**磚。

![服務對應圖格](media/operations-management-suite-walkthrough-servicemap/tile.png)

hello 服務對應主控台會隨即顯示。  Hello 在左的窗格會是您已安裝的 hello 服務對應代理程式的環境中的電腦清單。  您需要選取想要從這個清單 tooview hello 電腦。

![電腦清單](media/operations-management-suite-walkthrough-servicemap/computer-list.png)


### <a name="3-view-computer"></a>3.檢視電腦
我們知道的 hello 網頁伺服器被稱為 AcmeWFE001 和 AcmeWFE002，因此這看起來像是適當起點 toostart。  按一下 [AcmeWFE001]。  這樣會顯示 hello 對應 AcmeWFE001 及其所有相依性。  您可以看到哪些處理程序的執行 hello 所選的電腦上的外部服務進行通訊。

![Web 伺服器](media/operations-management-suite-walkthrough-servicemap/web-server.png)

我們很在意 hello 效能，我們的 web 應用程式，因此按一下 hello **AcmeAppPool （IIS 應用程式集區）**程序。  這會顯示 hello 這個處理序的詳細資料，並反白顯示相依性。  

![應用程式集區](media/operations-management-suite-walkthrough-servicemap/app-pool.png)


### <a name="4-change-time-window"></a>4.變更時間範圍

我們聽到看看什麼發生當時的 hello 問題讓我們開始於上午 4:00。 按一下**時間範圍**並變更 hello 時間 too4: 00 AM PST （保留 hello 目前的日期和本地時區調整） 持續時間為 20 分鐘。

![時間選擇器](./media/operations-management-suite-walkthrough-servicemap/time-picker.png)


### <a name="5-view-alert"></a>5.檢視警示

我們現在看到該 hello **acmetomcat**相依性都有警示顯示，因此這是我們的潛在問題。  按一下中的 hello 警示圖示**acmetomcat** tooshow hello hello 警示詳細資料。  我們可以看到 CPU 使用率有重大警示並可將其展開，以取得更詳細的資料。  這可能是造成效能變慢的原因。 

![警示](./media/operations-management-suite-walkthrough-servicemap/alert.png)


### <a name="6-view-performance"></a>6.檢視效能

讓我們仔細看看 **acmetomcat**。  按一下 hello 中的權限的最上層**acmetomcat**選取**負載 Server 對應**tooshow hello 詳細資料和此機器的相依性。 我們可以再查看稍微這些效能計數器 tooverify 我們停滯。  選取 hello**效能** 索引標籤 toodisplay hello[記錄分析所收集的效能計數器](../log-analytics/log-analytics-data-sources-performance-counters.md)hello 時間範圍內。  我們可以看到，我們收到 hello 處理器和記憶體的週期峰值。

![效能](./media/operations-management-suite-walkthrough-servicemap/performance.png)


### <a name="7-view-change-tracking"></a>7.檢視變更追蹤
我們來看看是否可以找出可能造成此高使用率的原因。  按一下 hello**摘要** 索引標籤。這會提供連線、 重大警示和軟體變更失敗，例如收集 hello 電腦從 OMS 的資訊。  具有最近的有趣資訊區段應該已經展開，而且可以展開其他各節 tooinspect 所包含的資訊。


如果 [變更追蹤] 尚未開啟，則將它展開。  這會顯示 hello 所收集的資訊[變更追蹤解決方案](../log-analytics/log-analytics-change-tracking.md)。  看起來，已在這段期間範圍內進行軟體變更。  按一下**軟體**tooget 詳細資料。  備份程序是只在上午 4:00 之後加入 toohello 機器，所以這會顯示 hello 正在耗用過多資源的 toobe hello 問題。

![變更追蹤](./media/operations-management-suite-walkthrough-servicemap/change-tracking.png)



### <a name="8-view-details-in-log-search"></a>8.在記錄搜尋中檢視詳細資料
我們可以進一步驗證，請查看 hello 詳細 hello 記錄分析儲存機制中收集的效能資訊。  按一下 hello**警示**索引標籤上一次，然後在其中一個 hello**高 CPU**警示。  按一下 [在記錄搜尋中顯示]。  這會開啟您要執行 hello 記錄搜尋視窗[記錄搜尋](../log-analytics/log-analytics-log-searches.md)針對 hello 儲存機制中儲存的任何資料。  服務對應為我們已經填入 queriy tooretrieve hello 警示我們感興趣。  

![記錄搜尋](./media/operations-management-suite-walkthrough-servicemap/log-search.png)


### <a name="9-open-saved-search"></a>9.開啟已儲存的搜尋
我們來看看是否我們可以產生此警示的 hello 效能集合中取得更多詳細資料，並確認該備份的程序所造成的問題 hello 我們停滯。  變更 hello 時間範圍太**6 小時**。  然後按一下 **我的最愛**和捲動 toohello 儲存搜尋**服務對應**。  這些是我們特別為此分析所建立的查詢。  按一下 [acmetomcat CPU 的前 5 個處理程序]。

![儲存的搜尋](./media/operations-management-suite-walkthrough-servicemap/saved-search.png)


此查詢會傳回一份 hello 前 5 個處理序正在耗用處理器上**acmetomcat**。  您可以檢查 hello 查詢 tooget 簡介 toohello 查詢語言，用於記錄搜尋。  如果您想要在其他電腦上的 hello 處理序中，您可以修改 hello 查詢 tooretrieve 該資訊。

在此情況下，我們可以看到 hello 備份程序會一致地耗用約 60%的 hello 應用程式伺服器的 CPU。  這個新程序顯然是效能問題的原因。  我們的方案會很明顯地 tooremove 這個新備份關閉 hello 應用程式伺服器的軟體。  實際上，我們無法利用預期狀態設定 (DSC) 受 Azure 自動化 toodefine 原則，確保絕不會執行這些重要的系統上，此程序。


## <a name="summary-points"></a>摘要點
- 即使您不知道應用程式的所有伺服器和相依性，[服務對應](operations-management-suite-service-map.md)也會提供整個應用程式的檢視。
- 服務對應介面上的資料收集的其他 OMS 解決方案 toohelp 您識別問題時您的應用程式和其基礎結構。
- [記錄搜尋](../log-analytics/log-analytics-log-searches.md)允許您 toodrill 向下到收集 hello 記錄分析儲存機制中的特定資料。    

## <a name="next-steps"></a>後續步驟
- 深入了解[服務對應](operations-management-suite-service-map.md)。
- [部署和設定](operations-management-suite-service-map-configure.md)服務對應。
- 了解服務對應所需的 [Log Analytics](../log-analytics/log-analytics-overview.md)，其可儲存代理程式所儲存的作業資料。