---
title: "aaaAzure 服務網狀架構容器監視和診斷 |Microsoft 文件"
description: "深入了解如何 toomonitor 並診斷在 Microsoft Azure Service Fabric 協調與 OMS 的容器解決方案的容器。"
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
ms.date: 05/10/2017
ms.author: dekapur
ms.openlocfilehash: cd79111cf78b9d76a60d489bb9953587aa06186d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-windows-server-containers-with-oms"></a>使用 OMS 監視 Windows Server 容器

## <a name="oms-containers-solution"></a>OMS 容器解決方案

hello Operations Management Suite (OMS) 小組已發行容器解決方案，以診斷和監視的容器。 Service Fabric 方案，連同此方案處於協調服務網狀架構上很棒的工具 toomonitor 容器部署。 以下是 hello 方案中的哪些 hello 儀表板看起來像的簡單範例：

![基本 OMS 儀表板](./media/service-fabric-diagnostics-containers-windowsserver/oms-containers-dashboard.png)

它也會收集不同類型的記錄檔所能查詢在 hello OMS 記錄分析工具中，而且可以使用的 toovisualize 任何度量或正在產生的事件。 hello 所收集的記錄類型包括：

1. ContainerInventory︰顯示容器位置、名稱和映像的相關資訊
2. ContainerImageInventory︰已部署映像相關資訊，包括 ID 或大小
3. ContainerLog︰特定的錯誤記錄檔、 docker 記錄檔 (stdout 等) 及其他項目
4. ContainerServiceLog：已執行的 docker 精露命令
5. 效能： 包括容器效能計數器 cpu、 記憶體、 網路流量、 磁碟 i/o 和自訂度量以從 hello 裝載機器

本文涵蓋 hello 步驟需要的 tooset 容器監視您的叢集設定。 toolearn 更多關於 OMS 的容器解決方案，請參閱其[文件](../log-analytics/log-analytics-containers.md)。

## <a name="1-set-up-a-service-fabric-cluster"></a>1.設定 Service Fabric 叢集

使用找到的 hello Azure Resource Manager 範本建立叢集[這裡](https://github.com/dkkapur/Service-Fabric/tree/master/ARM%20Templates/SF%20OMS%20Sample)。 請確定 tooadd 唯一的 OMS 工作區名稱。 此範本也預設的 toodeploying hello 預覽中的叢集建立的 Service Fabric (v255.255)，也就是說，它不能用在生產環境中，並不能升級 tooa Service Fabric 版本不同。 如果您決定 toouse 這個範本的長期或生產環境使用，請變更 hello 版本 tooa 穩定版本號碼。

一旦設定 hello 叢集之後，請確認您已安裝 hello 適當的憑證，並確定您能夠 tooconnect toohello 叢集。

確認您的資源群組已正確設定，時的標題 toohello [Azure 入口網站](https://portal.azure.com/)和尋找 hello 部署。 hello 資源群組應該包含所有的 hello 服務網狀架構資源，而且也有 記錄分析解決方案，以及服務網狀架構方案。

如需修改現有的 Service Fabric 叢集：
* 確認已啟用診斷 (如果沒有，請啟用它透過[更新 hello 虛擬機器規模集](/rest/api/virtualmachinescalesets/create-or-update-a-set))
* 建立透過 hello Azure Marketplace 以 「 服務網狀架構分析 」 解決方案加入 OMS 工作區
* 在 hello hello 叢集的資源群組處於中編輯 hello hello Service Fabric 方案 toopick hello （設定 wad） 適當 Azure 儲存體資料表中資料的資料來源
* 加入 hello 代理程式做為[延伸 toohello 虛擬機器規模集](/powershell/module/azurerm.compute/add-azurermvmssextension)透過 PowerShell 或透過更新 hello 的虛擬機器規模集 （上述的相同連結、 toomodify hello Resource Manager 範本）

## <a name="2-deploy-a-container"></a>2.部署容器

Hello 叢集已就緒，而且在您確認您可以存取它，一旦部署容器 tooit。 如果您選擇 toouse hello 預覽版本所設定的 hello 範本，您也可以探索 Service Fabric 新 docker 撰寫功能。 要記住 hello 第一次的容器映像部署的 tooa 叢集，花幾分鐘的時間 toodownload hello 映像依據其大小。

## <a name="3-add-hello-containers-solution"></a>3.新增 hello 容器解決方案

在 hello Azure 入口網站中建立容器的資源 (在 hello 監視 + 管理類別目錄) 透過 Azure Marketplace。 

![新增容器解決方案](./media/service-fabric-diagnostics-containers-windowsserver/containers-solution.png)

在 hello 建立步驟中，它會要求 OMS 工作區。 選取 hello 與 hello 部署上面所建立。 此步驟新增您的 OMS 工作區中的容器解決方案，並會自動偵測 hello 範本所部署的 hello OMS 代理程式。 hello 代理程式會開始收集資料 hello hello 叢集中的容器處理程序，並在 10-15 分鐘內，您應該會看到 hello 方案亮燈如 hello 映像的 hello 儀表板上面所示的資料。

## <a name="4-next-steps"></a>4.後續步驟

OMS 提供各種工具，在 [hello] 工作區 toomake 如果更有用了。 瀏覽下列選項 toocustomize hello 方案 tooyour 需求 hello:
- 取得以 hello 請[記錄搜尋和查詢](../log-analytics/log-analytics-log-searches.md)做為記錄分析的一部分提供的功能
- 設定特定的效能計數器向上 hello OMS 代理程式 toopick (移 toohello 工作區首頁 > 設定 > 資料 > Windows 效能計數器)
- 設定 OMS tooset[自動化警示](../log-analytics/log-analytics-alerts.md)規則 tooaid 中偵測及診斷
