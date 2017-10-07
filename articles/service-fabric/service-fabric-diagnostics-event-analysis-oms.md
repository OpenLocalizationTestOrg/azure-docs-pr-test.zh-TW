---
title: "aaaAzure 與 OMS 服務網狀架構事件分析 |Microsoft 文件"
description: "了解如何使用 OMS 視覺化及分析事件，來監視和診斷 Azure Service Fabric 叢集。"
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/26/2017
ms.author: dekapur
ms.openlocfilehash: 526519293e70982c95e31241465b87f190096f74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="event-analysis-and-visualization-with-oms"></a>使用 OMS 進行事件分析和視覺效果

Operations Management Suite (OMS) 是協助監視與應用程式的診斷功能的管理服務和 hello 雲端中裝載服務的集合。 OMS 和，提供功能的詳細概觀 tooget 讀取[OMS 是什麼？](../operations-management-suite/operations-management-suite-overview.md)

## <a name="log-analytics-and-hello-oms-workspace"></a>記錄分析和 hello OMS 工作區

Log Analytics 會從 Managed 資源 (包括 Azure 儲存體資料表或代理程式) 收集資料，並在中央存放庫中維護資料。 hello 資料然後可能用於分析、 警示與視覺效果，或進一步匯出。 Log Analytics 支援事件、效能資料或任何其他自訂資料。

設定 OMS 時，您必須存取 tooa 特定*OMS 工作區*，從可以查詢或在儀表板中視覺化資料。

OMS 記錄分析所收到資料之後，有數個*管理解決方案*所套裝的解決方案 toomonitor 內送資料，自訂的 tooseveral 案例。 這些包括*服務網狀架構分析*方案和*容器*方案，也就是兩個最相關的 hello toodiagnostics 和監視使用 Service Fabric 叢集時。 有數個其他也值得您瀏覽，以及 OMS 也可以自訂的解決方案，您可以深入了解 hello 建立[這裡](../operations-management-suite/operations-management-suite-solutions.md)。 您選擇 toouse hello 會設定為叢集的每個解決方案相同的 OMS 工作區，以及記錄分析。 工作區可讓自訂的儀表板和視覺效果的資料，以及您想要 toocollect，修改 toohello 資料處理及分析。

## <a name="setting-up-an-oms-workspace-with-hello-service-fabric-solution"></a>設定 OMS 工作區以 hello 服務網狀架構解決方案

建議您包含在您的 OMS 工作區中的 hello 服務網狀架構解決方案，因為它會提供有用的儀表板會顯示 hello 各種 hello 平台和應用程式層級，與 hello 無法 tooquery Service Fabric 的內送記錄檔通道的特定記錄檔。 以下是相當簡單的服務網狀架構解決方案的外觀，與 hello 叢集上部署的單一應用程式：

![OMS SF 解決方案](media/service-fabric-diagnostics-event-analysis-oms/service-fabric-solution.png)

有兩種方式 tooprovision 和設定 OMS 工作區中的，透過資源管理員範本，或是直接從 Azure Marketplace。 當您部署叢集，並啟用 hello 後者，如果您已經部署之診斷的叢集，請使用 hello 前者。

### <a name="deploying-oms-using-a-resource-management-template"></a>使用資源管理範本部署 OMS

這會發生在 hello 叢集建立階段-時部署叢集使用資源管理員範本、 hello 範本也可以建立新的 OMS 工作區，新增 hello 服務網狀架構解決方案 tooit，並且設定其 tooread hello 適當的儲存體的資料資料表。

>[!NOTE]
>針對此 toowork，診斷具有 toobe 啟用 hello Azure 儲存體資料表 tooexist oms / Log Analytics tooread 資訊中的。

[這裡](https://azure.microsoft.com/resources/templates/service-fabric-oms/)提供一個範例範本，您可以使用並視需求修改，以執行上述動作。 在 hello 情況下您想要更多的選用性，有一些更多範本可讓您根據其中 hello 程序中您可能設定 OMS 工作區的不同選項-它們可以位於[Service Fabric 和 OMS 範本](https://azure.microsoft.com/resources/templates/?term=service+fabric+OMS).

### <a name="deploying-oms-using-through-azure-marketplace"></a>使用 Azure Marketplace 部署 OMS

如果您偏好 tooadd OMS 工作區，在部署叢集之後，透過 tooAzure Marketplace 前端，並且尋找*」 服務網狀架構分析 」*。 只應該有一個資源，顯示 hello 「 監視 + 管理 」 分類中，如下所示：

![Marketplace 中的 OMS SF 分析](media/service-fabric-diagnostics-event-analysis-oms/service-fabric-analytics.png)

按一下 [建立] 會要求您提供 OMS 工作區。 按一下 [選取工作區]，然後按一下 [建立新的工作區]。 填寫所需的 hello 項目-這裡 hello 唯一的需求是 hello hello Service Fabric 叢集和 hello OMS 工作區應該是 hello 訂用帳戶相同。 一旦驗證所有項目，您的 OMS 工作區將會在幾分鐘內部署。 當部署完成為止時，hello 建立 hello Service Fabric 方案刀鋒視窗將仍維持開啟狀態。 請確定的 hello 相同的工作區顯示在*OMS 工作區*並點擊**建立**hello 底部 tooadd hello Service Fabric 方案 toohello 工作區。

## <a name="using-hello-oms-agent"></a>使用 hello OMS 代理程式

建議 toouse EventFlow 以及為彙總解決方案的 WAD 因為它們允許更模組化的方法 toodiagnostics 和監視。 比方說，如果您想 toochange EventFlow 程式輸出時，它會要求任何變更 tooyour 實際檢測，只要簡單的修改 tooyour 組態檔。 如果，不過，您決定 tooinvest 在 OMS 中使用，而且願意 toocontinue 用於事件分析 （沒有 toobe hello 只能您使用平台，而不是它會是至少其中一個 hello 平台），我們建議您瀏覽設定 hello [</c0>OMSagent<spanclass="notranslate">](../log-analytics/log-analytics-windows-agents.md)。</span> 您也應該使用 hello OMS 代理程式時部署容器 tooyour 叢集，如下所述。

因為您只需要 tooadd hello 代理程式做為虛擬機器擴展集延伸模組 tooyour Resource Manager 範本，確保它已安裝在每個節點上，執行此作業的 hello 程序是相當簡單。 範例資源管理員範本部署以 hello Service Fabric 的方案 （請見上方） hello OMS 工作區並將新增 hello 代理程式 tooyour 節點可以找到叢集執行[Windows](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/SF%20OMS%20Samples/Windows)或[Linux](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/SF%20OMS%20Samples/Linux)。

hello 下列 hello 優點︰

* Hello 效能計數器和度量端更多的資料
* 收集從 hello 輕鬆 tooconfigure 資料叢集，並進行變更 tooit 而不必重新部署您的應用程式或 hello 叢集，因為變更 toohello hello 代理程式設定可以完成從 hello OMS 工作區，然後只會重設 hello 代理程式自動的。 設定特定的效能計數器，請移 toohello 工作區 tooconfigure hello OMS 代理程式 toopick**首頁 > 設定 > 資料 > Windows 效能計數器**並選取您想要收集的 toosee hello 資料
* 資料就會出現比不需要儲存之前由 OMS 來挑選 toobe 快 / 記錄分析
* 更容易監視容器，因為它可以挑選 docker 記錄檔 (stdout、stderror) 和統計資料 (容器和節點層級的效能計量)

這裡 hello 主要的考量是，因為它是代理程式，它將會部署所有的應用程式，以及在叢集上應該會有一些 hello 叢集上的應用程式的影響降到最低 toohello 效能。

## <a name="monitoring-containers"></a>監視容器

在部署容器 tooa Service Fabric 叢集時，建議您使用 hello 叢集已設定與 hello OMS 代理程式，並 tooyour OMS 工作區 tooenable 監視和診斷已經加入該 hello 容器解決方案。 以下是工作區中的方案看起來像哪些 hello 容器：

![基本 OMS 儀表板](./media/service-fabric-diagnostics-event-analysis-oms/oms-containers-dashboard.png)

hello 代理程式會啟用數個特定容器的記錄檔可以在 OMS 中，查詢或使用 toovisualized 效能指標 hello 集合。 hello 所收集的記錄類型包括：

* ContainerInventory︰顯示容器位置、名稱和映像的相關資訊
* ContainerImageInventory︰已部署映像相關資訊，包括 ID 或大小
* ContainerLog︰特定的錯誤記錄檔、 docker 記錄檔 (stdout 等) 及其他項目
* ContainerServiceLog：已執行的 docker 精露命令
* 效能： 包括容器效能計數器 cpu、 記憶體、 網路流量、 磁碟 i/o 和自訂度量以從 hello 裝載機器

本文涵蓋 hello 步驟需要的 tooset 容器監視您的叢集設定。 toolearn 更多關於 OMS 的容器解決方案，請參閱其[文件](../log-analytics/log-analytics-containers.md)。

tooset 向上 hello 容器解決方案，在您的工作區，請確定您有 hello hello 上面所述的步驟部署您的叢集節點上的 OMS 代理程式。 準備 hello 叢集之後，部署容器 tooit。 要記住 hello 第一次的容器映像部署的 tooa 叢集，花幾分鐘的時間 toodownload hello 映像依據其大小。

在 Azure Marketplace 中搜尋*容器*和建立容器的資源 (在 hello 監視 + 管理類別目錄)。

![新增容器解決方案](./media/service-fabric-diagnostics-event-analysis-oms/containers-solution.png)

在 hello 建立步驟中，它會要求 OMS 工作區。 選取 hello 與 hello 部署上面所建立。 此步驟新增您的 OMS 工作區中的容器解決方案，並會自動偵測 hello 範本所部署的 hello OMS 代理程式。 hello 代理程式會開始收集資料 hello 容器中 hello 叢集，而且小於 15 分鐘的處理程序，或因此，您應該會看見 hello 方案亮燈取代資料，如 hello 映像的 hello 儀表板上面所示。


## <a name="next-steps"></a>後續步驟

瀏覽下列工作區 tooyour 需要 OMS 工具和選項 toocustomize hello:

* 在內部部署叢集，OMS 會提供可以使用的 toosend 資料 tooOMS 閘道 (HTTP 向前 Proxy)。 深入了解[電腦沒有網際網路存取 tooOMS 使用 hello OMS 閘道連線](../log-analytics/log-analytics-oms-gateway.md)
* 設定 OMS tooset[自動化警示](../log-analytics/log-analytics-alerts.md)tooaid 中偵測及診斷
* 取得以 hello 請[記錄搜尋和查詢](../log-analytics/log-analytics-log-searches.md)做為記錄分析的一部分提供的功能
