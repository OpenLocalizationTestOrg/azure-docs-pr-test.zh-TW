---
title: "aaaIntroduction tooAzure 網路監看員 |Microsoft 文件"
description: "此頁面提供的 hello 網路監看員監視的服務概觀，並以視覺化方式檢視網路連線在 Azure 中的資源"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 14bc2266-99e3-42a2-8d19-bd7257fec35e
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/11/2017
ms.author: gwallace
ms.openlocfilehash: 283b3fa6add05d9bad6d5dbdae1524344d1bfc7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-network-monitoring-overview"></a>Azure 網路監視概觀

客戶可藉由安排和組合各種個別的網路資源 (例如 VNet、ExpressRoute、應用程式閘道、負載平衡器等等)，在 Azure 中建置端對端網路。 使用每個 hello 網路資源的監視。 我們 toothis 監視做為資源層級的監視。

hello 結束 tooend 網路可具有複雜的組態和資源，建立複雜的案例需要的案例為基礎的監視透過網路監看員之間的互動。

本文將探討案例和資源層級的監視。 Azure 中的網路監視功能相當完善，主要涵蓋類別有二種︰

* [**網路監看員**](#network-watcher) -提供以案例為基礎監視使用中網路監看員的 hello 功能。 這項服務包括封包擷取、下一個躍點、IP 流量驗證、安全性群組檢視、NSG 流量記錄。 案例層級監視提供結束 tooend 檢視中對比 tooindividual 網路資源監視的網路資源。
* [**資源監視**](#network-resource-level-monitoring) - 資源層級監視由診斷記錄、計量、疑難排解和資源健全狀況這四個功能所組成。 所有這些功能是建置在 hello 網路資源層級。

## <a name="network-watcher"></a>網路監看員

網路監看員是地區和服務，可讓您 toomonitor 診斷層級網路案例中，，然後從 Azure 的情況。 網路診斷和使用網路監看員的視覺化工具，可協助您了解、 診斷，以及取得 Azure insights tooyour 網路。

網路監看員目前具有下列功能的 hello:

* **[拓樸](network-watcher-topology-overview.md)** -提供網路層級檢視顯示 hello 各種 connect 和資源群組中的網路資源之間的關聯。
* **[變動的封包擷取](network-watcher-packet-capture-overview.md)** - 擷取進出虛擬機器的封包資料。 進階篩選選項和微調的控制項，例如無法 tooset 加上時間和大小限制會提供彈性。 hello 封包資料可以儲存在 blob 存放區或 hello.cap 格式的本機磁碟上。
* **[IP 流量驗證](network-watcher-ip-flow-verify-overview.md)** - 根據流量資訊 5-tuple 封包參數 (目的地 IP、來源 IP、目的地連接埠、來源連接埠和通訊協定) 檢查是否允許或拒絕封包。 如果安全性群組遭拒絕 hello 封包，hello 規則，並拒絕 hello 封包的群組會傳回。
* **[下一個躍點](network-watcher-next-hop-overview.md)** -決定 hello 封包路由傳送 hello Azure 網路網狀架構，讓您 toodiagnose 任何設定錯誤的使用者定義的路由中下一個躍點。
* **[安全性的群組檢視](network-watcher-security-group-view-overview.md)** -取得 hello 有效且套用安全性規則，可在 VM 上套用。
* **[NSG 流程記錄](network-watcher-nsg-flow-logging-overview.md)** -網路安全性群組的流程記錄可讓您 toocapture 記錄相關的 tootraffic 允許或拒絕 hello 群組中的 hello 安全性規則。 hello 流程是由 5-tuple 資訊 – 來源 IP、 目的地 IP、 來源連接埠，目的地連接埠和通訊協定定義。
* **[虛擬網路閘道與連接疑難排解](network-watcher-troubleshoot-manage-rest.md)** -提供 hello 能力 tootroubleshoot 虛擬網路閘道與連線。
* **[訂用帳戶限制的網路](#network-subscription-limits)** -可讓您限制對 tooview 網路資源使用狀況。
* **[設定診斷記錄](#diagnostic-logs)** – 提供單一窗格 tooenable 或停用網路資源的資源群組中的診斷記錄檔。
* **[連線能力 （預覽）](network-watcher-connectivity-overview.md)**  -確認 hello 可能會建立從虛擬機器 tooa 指定端點的直接 TCP 連接。

### <a name="role-based-access-control-rbac-in-network-watcher"></a>網路監看員的角色型存取控制 (RBAC)

網路監看員會使用 hello[所有存取控制 (RBAC) 模型](../active-directory/role-based-access-control-what-is.md)。 需要下列權限的 hello hello 網路監看員。 重要 toomake 確定用於初始網路監看員應用程式開發介面或從 hello 入口網站中使用網路監看員該 hello 角色擁有 hello 需要存取它。

|資源| 權限|
|---|---| 
|Microsoft.Storage/ |讀取|
|Microsoft.Authorization/| 讀取| 
|Microsoft.Resources/subscriptions/resourceGroups/| 讀取|
|Microsoft.Storage/storageAccounts/listServiceSas/ | 動作|
|Microsoft.Storage/storageAccounts/listAccountSas/ |動作|
|Microsoft.Storage/storageAccounts/listKeys/ | 動作|
|Microsoft.Compute/virtualMachines/ |讀取|
|Microsoft.Compute/virtualMachines/ |寫入|
|Microsoft.Compute/virtualMachineScaleSets/ |讀取|
|Microsoft.Compute/virtualMachineScaleSets/ |寫入|
|Microsoft.Network/networkWatchers/packetCaptures/ |讀取|
|Microsoft.Network/networkWatchers/packetCaptures/| 寫入|
|Microsoft.Network/networkWatchers/packetCaptures/| 刪除|
|Microsoft.Network/networkWatchers/ |寫入 |
|Microsoft.Network/networkWatchers/| 讀取 |
|Microsoft.Insights/alertRules/ |*|
|Microsoft.Support/ | *|

### <a name="network-subscription-limits"></a>網路訂用帳戶限制

網路訂用帳戶限制為您提供的每個訂用帳戶中針對 hello 的可用資源的最大數目的區域中的 hello 網路資源的 hello 使用量的詳細資料。

![網路訂用帳戶限制][nsl]

## <a name="network-resource-level-monitoring"></a>網路資源層級監視

下列功能的 hello 可供資源層級的監視：

### <a name="audit-log"></a>稽核記錄檔

Hello 的網路組態的一部分執行的作業記錄。 這些記錄檔可以在 hello Azure 入口網站中檢視，或使用 Microsoft 工具，例如 Power BI 或協力廠商工具來擷取。 稽核記錄檔皆可透過 hello 入口網站、 PowerShell、 CLI 和 Rest API。 如需稽核記錄的詳細資訊，請參閱[使用 Resource Manager 來稽核作業](../resource-group-audit.md)

針對所有網路資源所進行的作業都會有稽核記錄。

### <a name="metrics"></a>度量

計量是在一段時間內所收集到的效能測量數據和計數器。 計量目前適用於應用程式閘道。 度量可以是使用的 tootrigger 警示臨界值為基礎。 請參閱[應用程式閘道診斷](../application-gateway/application-gateway-diagnostics.md)tooview 度量可以列印文件的是，請使用的 toocreate 警示。

![計量檢視][metrics]

### <a name="diagnostic-logs"></a>診斷記錄檔

定期和即時事件建立的網路資源，登入傳送 tooan 事件中心 」 或 「 記錄分析的儲存體帳戶。 這些記錄檔提供深入了解資源的 hello 健全狀況。 您可以在 Power BI 和 Log Analytics 等工具中檢視這些記錄。 toolearn tooview 診斷記錄檔的瀏覽[記錄分析](../log-analytics/log-analytics-azure-networking-analytics.md)。

診斷記錄適用於[負載平衡器](../load-balancer/load-balancer-monitor-log.md)、[網路安全性群組](../virtual-network/virtual-network-nsg-manage-log.md)、路由和[應用程式閘道](../application-gateway/application-gateway-diagnostics.md)。

網路監看員提供診斷記錄檢視。 此檢視包含所有支援診斷記錄的網路資源。 從這個檢視中，您可以方便且快速地啟用和停用網路資源。

![logs][logs]

### <a name="troubleshooting"></a>疑難排解

hello 疑難排解刀鋒視窗中，在 hello 入口網站的經驗提供網路資源上今天 toodiagnose 個別資源相關聯的常見問題。 使用下列的網路資源，ExpressRoute、 VPN 閘道、 應用程式閘道、 網路安全性記錄檔、 路由、 DNS、 負載平衡器和 Traffic Manager 的 hello 這項體驗。 toolearn 進一步了解資源層級進行疑難排解，請瀏覽[Azure 疑難排解的診斷和解決問題](https://azure.microsoft.com/blog/azure-troubleshoot-diagonse-resolve-issues/)

![疑難排解資訊][TS]

### <a name="resource-health"></a>資源健康情況

定期執行提供的網路資源的 hello 健全狀況。 這類資源包括 VPN 閘道與 VPN 通道。 在 hello Azure 入口網站上存取資源健全狀況。 toolearn 深入了解資源健全狀況，請瀏覽[資源健全狀況概觀](../resource-health/resource-health-overview.md)

## <a name="next-steps"></a>後續步驟

在了解網路監看員之後，您可以接著學習︰

請勿在您的 VM 上的封包擷取造訪[hello Azure 入口網站中的變數的封包擷取](network-watcher-packet-capture-manage-portal.md)

使用[警示觸發的封包擷取](network-watcher-alert-triggered-packet-capture.md)執行主動監視和診斷。

使用開放原始碼工具，透過[使用 Wireshark 分析封包擷取](network-watcher-deep-packet-inspection.md)來偵測安全性弱點。

深入了解一些 hello 另一個索引鍵[網路功能](../networking/networking-overview.md)的 Azure。

<!--Image references-->
[TS]: ./media/network-watcher-monitoring-overview/troubleshooting.png
[logs]: ./media/network-watcher-monitoring-overview/logs.png
[metrics]: ./media/network-watcher-monitoring-overview/metrics.png
[nsl]: ./media/network-watcher-monitoring-overview/nsl.png











