---
title: "在 Microsoft Azure 中的度量的 aaaOverview |Microsoft 文件"
description: "Microsoft Azure 中的度量及其用法概觀"
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 405ec51c-0946-4ec9-b535-60f65c4a5bd1
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2017
ms.author: johnkem
ms.openlocfilehash: 2b97f51e0554dae95a929241ae1f0e25e5c215ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-metrics-in-microsoft-azure"></a>Microsoft Azure 中的度量概觀
本文章說明度量資訊是在 Microsoft Azure 中，其優點，以及如何使用它們的 toostart。  

## <a name="what-are-metrics"></a>何謂度量？
Azure 監視器可讓您 tooconsume 遙測 toogain 掌握 hello 效能和您的工作負載在 Azure 上的健全狀況。 hello Azure 的遙測資料的最重要型別是 hello 度量 （也稱為效能計數器） 發出的大部分的 Azure 資源。 Azure 監視提供數種方式 tooconfigure，並使用監視和疑難排解這些度量資訊。

## <a name="what-can-you-do-with-metrics"></a>度量能讓您做什麼？
度量是重要的遙測資料來源，並啟用您 toodo hello 下列工作：

* **追蹤 hello 效能**之資源 （例如 VM、 網站或邏輯應用程式） 繪製其入口網站的圖表上的度量，釘選圖表 tooa 儀表板。
* **取得問題的通知**影響 hello 之資源的效能，當度量超出某個臨界值時。
* **設定自動化動作**，例如自動調整資源，或在度量超出特定的閾值時觸發 Runbook。
* **執行進階分析**或報告您資源的效能或使用量趨勢。
* **封存**hello 之資源的效能或健全狀況歷程記錄**相容性或稽核**用途。

## <a name="what-are-hello-characteristics-of-metrics"></a>度量的 hello 特性有哪些？
度量具有下列特性的 hello:

* 所有度量皆有**一分鐘的頻率**。 您收到公制值每隔一分鐘從您的資源，提供您附近 hello 狀態和健全狀況之資源的即時可視性。
* 度量**可立即使用**。 您不需要 tooopt 中的，或將額外的診斷設定。
* 您可以針對每個度量存取 **30 天的歷程記錄** 。 您可以快速查看 hello 最近和每月的趨勢 hello 效能或資源的健全狀況。

您也可以：

* 設定度量**警示規則，傳送通知或採用自動化動作**hello 度量超出您設定的 hello 閾值的時。 自動調整規模是一種特殊的自動化的動作，可讓 tooscale 資源 toomeet 的內送要求，或在您的網站或運算資源時載入。 您可以設定自動調整規模設定規則 tooscale in 或 out 根據跨越臨界值的度量。

* **路由**所有度量 Application Insights 或記錄分析 (OMS) tooenable 立即分析、 搜尋和自訂警示的度量資料是來自您的資源。 您也可以串流處理度量 tooan 事件中心，讓您 toothen 將它們路由傳送 tooAzure 串流分析或 toocustom 幾乎是即時分析的應用程式。 您需要設定使用診斷設定的事件中樞串流。

* **封存計量 toostorage**較長的保留或用於產生離線報表。 當您設定您為資源的診斷設定時，您可以路由您度量 tooAzure Blob 儲存體。

* 輕鬆地探索，存取，以及**檢視的所有度量**透過 hello Azure 入口網站，當您選取的資源，並繪製 hello 度量圖表上的。

* **取用**透過 hello 度量 hello 新的 Azure 監視 REST Api。

* **查詢**度量使用 hello PowerShell cmdlet 或 hello 跨平台 REST API。

  ![Azure 監視器中的度量路由](./media/monitoring-overview-metrics/Metrics_Overview_v4.png)

## <a name="access-metrics-via-hello-portal"></a>透過 hello 入口網站存取的度量
以下是如何 toocreate 度量圖表使用 hello Azure 入口網站的快速逐步解說。

### <a name="tooview-metrics-after-creating-a-resource"></a>建立資源之後 tooview 度量
1. 開啟 hello Azure 入口網站。
2. 建立 Azure App Service 網站。
3. 建立網站之後，請繼續 toohello**概觀**hello 網站的刀鋒視窗。
4. 您可以用 [監視] 圖格的形式檢視新度量。 然後，您可以編輯 hello 磚，並選取多個度量。

   ![Azure 監視器中的資源度量](./media/monitoring-overview-metrics/MetricsOverview1.png)

### <a name="tooaccess-all-metrics-in-a-single-place"></a>tooaccess 在單一位置的所有標準
1. 開啟 hello Azure 入口網站。
2. 瀏覽新 toohello**監視器**索引標籤，然後再與選取的 hello**度量**其下方的選項。
3. 從 hello 下拉式清單中，選取您的訂用帳戶、 資源群組和 hello hello 資源名稱。
4. 檢視 hello 可用的度量清單。 然後選取您感興趣，並繪製它的 hello 度量。
5. 您可以釘選它 toohello 儀表板按一下 hello hello 右上角的釘選。

   ![在 Azure 監視器中的單一位置存取所有度量](./media/monitoring-overview-metrics/MetricsOverview2.png)

> [!NOTE]
> 您可以從 VM (以 Azure Resource Manager 為基礎) 存取主機層級的度量和虛擬機器擴展集，而不需要任何額外的診斷設定。 這些新的主機層級度量可供 Windows 和 Linux 執行個體使用。 這些度量不 toobe hello 您擁有存取 toowhen 您開啟 Azure 診斷 Vm 或虛擬機器擴展集上的客體作業系統層級度量的問題感到困惑。 toolearn 進一步了解設定診斷功能，請參閱[何謂 Microsoft Azure 診斷](../azure-diagnostics.md)。
>
>

## <a name="access-metrics-via-hello-rest-api"></a>透過 hello REST API 存取度量
可透過 hello Azure 監視應用程式開發介面存取 azure 度量。 有兩個 API 可協助您探索及存取度量：

* 使用 hello [Azure 監視的標準定義 REST API](https://msdn.microsoft.com/library/mt743621.aspx) tooaccess hello 度量可用服務清單。
* 使用 hello [Azure 監視度量 REST API](https://msdn.microsoft.com/library/mt743622.aspx) tooaccess hello 實際度量資料。

> [!NOTE]
> 本文章涵蓋透過 hello hello 度量[標準的新 API](https://msdn.microsoft.com/library/dn931930.aspx) Azure 資源。 hello hello 新標準定義 API 的 API 版本是 2016年-03-01 和標準應用程式開發介面的 hello 版本是 2016年-09-01。 使用 hello 2014-04-01 版應用程式開發介面，可以存取 hello 舊版度量定義和度量。
>
>

如需使用 hello Azure 監視 REST Api 的詳細逐步解說，請參閱[Azure 監視 REST API 逐步解說](monitoring-rest-api-walkthrough.md)。

## <a name="export-metrics"></a>匯出度量
您可以移 toohello**診斷設定**刀鋒視窗底下 hello**監視器**度量的索引標籤和檢視表 hello 匯出選項。 您可以選取度量 （和診斷記錄檔） toobe 路由 tooBlob 儲存體、 tooAzure 事件中心或使用案例所提到的 tooOMS 先前在本文中。

 ![在 Azure 監視器中匯出度量選項](./media/monitoring-overview-metrics/MetricsOverview3.png)

您可以透過 Resource Manager 範本、[PowerShell](insights-powershell-samples.md)、[Azure CLI](insights-cli-samples.md) 或 [REST API](https://msdn.microsoft.com/library/dn931943.aspx) 來進行設定。

## <a name="take-action-on-metrics"></a>對度量採取動作
tooreceive 通知或採取自動動作的度量資料，您可以設定警示的規則或自動調整規模設定。

### <a name="configure-alert-rules"></a>設定警示規則
您可以設定度量的警示規則。 這些警示規則可以檢查度量是否已超過某個臨界值， 然後可以透過電子郵件通知您或任何自訂指令碼會引發可以是使用的 toorun webhook。 您也可以使用 hello webhook tooconfigure 第三方產品整合。

 ![Azure 監視器中的度量和警示規則](./media/monitoring-overview-metrics/MetricsOverview4.png)

### <a name="autoscale-your-azure-resources"></a>自動調整您的 Azure 資源
某些 Azure 資源支援 hello 的縮放比例出或多個執行個體 toohandle 您的工作負載。 TooApp 服務 (Web 應用程式)、 虛擬機器擴展集和傳統的 Azure 雲端服務，適用於自動調整規模。 當某些度量資訊會影響您的工作負載超出您所指定的臨界值時，您可以設定自動調整規模規則 tooscale 或放大。 如需詳細資訊，請參閱 [自動調整的概觀](monitoring-overview-autoscale.md)。

 ![Azure 監視器中的度量和自動調整](./media/monitoring-overview-metrics/MetricsOverview5.png)

## <a name="learn-about-supported-services-and-metrics"></a>了解支援的服務和度量
Azure 監視器是新的度量基礎結構。 它支援下列 hello Azure 入口網站與 hello 新版 hello Azure 監視應用程式開發介面中的 Azure 服務的 hello:

* VM (Azure Resource Manager 架構)
* 虛擬機器擴展集
* Batch
* 事件中樞命名空間
* 服務匯流排命名空間 (僅限進階 SKU)
* SQL Database (第 12 版)
* SQL 彈性集區
* 網站
* Web 伺服器陣列
* Logic Apps
* IoT 中樞
* Redis 快取
* 網路：應用程式閘道
* 搜尋

您可以檢視所有 hello 支援服務並在其度量的詳細的清單[Azure 監視度量-每個資源類型的支援度量](monitoring-supported-metrics.md)。

## <a name="next-steps"></a>後續步驟
請參閱 toohello 整篇文章的連結。 此外，請了解：  

* [自動調整規模的常用計量](insights-autoscale-common-metrics.md)
* [如何 toocreate 警示規則](insights-alerts-portal.md)
* [使用 Log Analytics 分析來自 Azure 儲存體的記錄](../log-analytics/log-analytics-azure-storage.md)
