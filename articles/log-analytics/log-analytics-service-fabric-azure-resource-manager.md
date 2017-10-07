---
title: "Service Fabric 應用程式與記錄分析使用 aaaAssess hello Azure 入口網站 |Microsoft 文件"
description: "您可以使用 hello Service Fabric 方案中使用 hello Azure 入口網站 tooassess hello 風險和健全狀況服務的網狀架構應用程式的記錄分析微服務、 節點和叢集。"
services: log-analytics
documentationcenter: 
author: niniikhena
manager: jochan
editor: 
ms.assetid: 9c91aacb-c48e-466c-b792-261f25940c0c
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: nini
ms.openlocfilehash: 891c7f6e5ed511ac18599bdc280ab3dc09700fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="assess-service-fabric-applications-and-micro-services-with-hello-azure-portal"></a>評估 Service Fabric 應用程式和以 hello Azure 入口網站的微服務

> [!div class="op_single_selector"]
> * [資源管理員](log-analytics-service-fabric-azure-resource-manager.md)
> * [PowerShell](log-analytics-service-fabric.md)
>
>

![Service Fabric 符號](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

本文說明如何 toouse hello Service Fabric 方案中記錄分析 toohelp 識別及疑難排解問題跨 Service Fabric 叢集。

hello Service Fabric 解決方案會使用從您服務網狀架構的 Vm，Azure 診斷資料收集這項資料從 Azure WAD 資料表。 然後 Log Analytics 會讀取 Service Fabric 架構事件，包括**可靠的服務事件**、**動作項目事件**、**操作事件**和**自訂 ETW 事件**。 Hello 方案儀表板，您在無法 tooview 值得注意的問題和相關事件 Service Fabric 環境中。

tooget 入門 hello 方案，您需要 tooconnect Service Fabric 叢集 tooa 記錄分析工作區。 以下是三個案例 tooconsider:

1. 如果您尚未部署 Service Fabric 叢集，使用中的 hello 步驟***部署 Service Fabric 叢集連線 tooa 記錄分析工作區***toodeploy 新叢集，而且已經設定 tooreport tooLog 分析。
2. 如果您需要 toocollect 效能計數器從主機 toouse 其他 OMS 解決方案，例如安全性服務網狀架構叢集上，依照中的 hello 步驟***部署 VM 擴充功能的 Service Fabric 叢集連線 tooa 記錄分析工作區安裝。***
3. 如果您已部署 Service Fabric 叢集，而且想 tooconnect 它 tooLog 分析，請依照下列中的 hello 步驟***加入現有的儲存體帳戶 tooLog 分析。***

## <a name="deploy-a-service-fabric-cluster-connected-tooa-log-analytics-workspace"></a>部署 Service Fabric 叢集連線 tooa 記錄分析工作區。
此範本沒有 hello 遵循：

1. 部署 Azure Service Fabric 叢集已連線 tooa 記錄分析工作區。 您擁有 hello 選項 toocreate 新的工作區部署 hello 範本或輸入的 hello 名稱已存在的記錄分析工作區時。
2. 新增 hello 診斷儲存體帳戶 toohello 記錄分析工作區。
3. 可讓您記錄分析工作區中的 hello Service Fabric 方案。

[![部署 tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)

一旦您選取 hello 部署按鈕上方，hello Azure 入口網站的開啟與您 tooedit 的參數。 如果您輸入新的記錄分析工作區名稱，是確定 toocreate 新的資源群組：

![Service Fabric](./media/log-analytics-service-fabric/2.png)

![Service Fabric](./media/log-analytics-service-fabric/3.png)

接受 hello 法律條款，然後按一下**建立**toostart hello 部署。 Hello 部署完成後，您應看到 hello 新工作區，然後建立、 叢集及 hello WADServiceFabric * 加入的事件、 WADWindowsEventLogs 及 WADETWEvent 資料表：

![Service Fabric](./media/log-analytics-service-fabric/4.png)

## <a name="deploy-a-service-fabric-cluster-connected-tooa-log-analytics-workspace-with-vm-extension-installed"></a>VM 擴充功能安裝與部署 Service Fabric 叢集連線 tooa 記錄分析工作區。

此範本沒有 hello 遵循：

1. 部署 Azure Service Fabric 叢集已連線 tooa 記錄分析工作區。 您可以建立新的工作區，或是使用現有的工作區。
2. 新增 hello 診斷儲存體帳戶 toohello 記錄分析工作區。
3. 可讓 hello 記錄分析工作區中的 hello Service Fabric 方案。
4. 安裝集合 Service Fabric 叢集中的每個虛擬機器規模 hello MMA 代理程式延伸。 Hello MMA 安裝有代理程式，就能 tooview 效能度量有關您的節點。

[![部署 tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)

以下 hello 相同的步驟上方輸入的 hello 必要的參數，並開始進行部署。 同樣地，您應該看到 hello 新的工作區、 叢集和所有建立的 WAD 資料表：

![Service Fabric](./media/log-analytics-service-fabric/5.png)

### <a name="viewing-performance-data"></a>檢視效能資料

從您的節點 tooview 的效能資料：


[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

- 啟動 hello 從 hello Azure 入口網站的記錄分析工作區。
  ![Service Fabric](./media/log-analytics-service-fabric/6.png)
- 在 hello 左窗格中，移 tooSettings，然後選取資料 >> Windows 效能計數器 >> 」 新增 hello 選取效能計數器 」: ![Service Fabric](./media/log-analytics-service-fabric/7.png)
- 在記錄搜尋中，使用下列查詢 toodelve 到您的節點有關的關鍵計量 hello:

    a. 比較您的所有節點中 hello 哪些節點時發生問題過去一小時 toosee hello 平均 CPU 使用率，但在哪個時間間隔節點突然增加：

    ```
    Type=Perf ObjectName=Processor CounterName="% Processor Time"|measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/10.png)

    b. 使用此查詢檢視每個節點上可用記憶體的類似折線圖︰

    ```
    Type=Perf ObjectName=Memory CounterName="Available MBytes Memory" | measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    tooview 您的所有節點，每個節點，並顯示 Available MBytes hello 的平均實際值的清單會使用下列查詢：

    ```
    Type=Perf (ObjectName=Memory) (CounterName="Available MBytes") | measure avg(CounterValue) by Computer
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/11.png)

    c. 萬一 hello 到特定節點想 toodrill 向下的，藉由檢查 hello 每小時平均值、 最小、 最大和 75 個百分位數的 CPU 使用量，您可以 toodo 藉由使用這個查詢 （取代電腦欄位）：

    ```
    Type=Perf CounterName="% Processor Time" InstanceName=_Total Computer="BaconDC01.BaconLand.com"| measure min(CounterValue), avg(CounterValue), percentile75(CounterValue), max(CounterValue) by Computer Interval 1HOUR
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/12.png)

閱讀詳細資訊記錄分析中的效能標準，在 hello [Operations Management Suite 部落格](https://blogs.technet.microsoft.com/msoms/tag/metrics/)。


## <a name="adding-an-existing-storage-account-toolog-analytics"></a>加入現有的儲存體帳戶 tooLog 分析

這個範本只會加入您現有儲存體帳戶 tooa 新的或現有記錄分析工作區。

[![部署 tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)

> [!NOTE]
> 在 選取資源群組，如果您正在使用現有的記錄分析工作區，選取 「 使用現有 」，並搜尋 hello 資源群組中包含的 hello 記錄分析工作區。 否則建立一個新的。
> ![Service Fabric](./media/log-analytics-service-fabric/8.png)
>
>

在部署此範本之後，您將無法 toosee hello 儲存體帳戶連接 tooyour 記錄分析工作區。 在本例中，我可以加入多個儲存體帳戶 toohello Exchange 工作區上面所建立。
![Service Fabric](./media/log-analytics-service-fabric/9.png)

## <a name="view-service-fabric-events"></a>檢視 Service Fabric 事件

Hello 部署已完成並已啟用工作區中的 hello Service Fabric 方案，請選取 hello **Service Fabric**磚 hello 記錄分析入口網站 toolaunch hello Service Fabric 儀表板中。 hello 儀表板會納入 hello 下表中的 hello 資料行。 每個資料行計數對應資料行的準則 hello 指定時間範圍列出 hello 前 10 個事件。 您可以執行，即可提供 hello 整個清單的記錄搜尋**查看所有**在 hello 右下的每個資料行，或按一下 hello 資料行標頭。

| **Service Fabric 事件** | **description** |
| --- | --- |
| 值得注意的問題 |顯示問題，例如 RunAsyncFailures RunAsynCancellations 和節點關閉。 |
| 運作事件 |值得注意的運作事件，例如應用程式升級和部署。 |
| 可靠的服務事件 |值得注意的可靠服務事件，例如 Runasyncinvocations。 |
| 動作項目事件 |您的微服務產生的值得注意動作項目事件，例如動作項目方法、動作項目啟用和停用等等所擲回的例外狀況。 |
| 應用程式事件 |您的應用程式產生的所有自訂 ETW 事件。 |

![Service Fabric 儀表板](./media/log-analytics-service-fabric/sf3.png)

![Service Fabric 儀表板](./media/log-analytics-service-fabric/sf4.png)

hello 下表顯示資料收集方法，以及適用於 Service Fabric 如何收集資料的其他詳細資料。

| 平台 | 直接代理程式 | Operations Manager 代理程式 | Azure 儲存體 | 是否需要 Operations Manager？ | 透過管理群組傳送的 Operations Manager 代理程式資料 | 收集頻率 |
| --- | --- | --- | --- | --- | --- | --- |
| Windows |  |  | &#8226; |  |  |10 分鐘 |

> [!NOTE]
> 您可以按一下來變更 hello Service Fabric 方案中的這些事件 hello 範圍**資料根據過去 7 天**在 hello hello 儀表板的頂端。 您也可以顯示 hello 內產生過去七天一天或六個小時的事件。 或者，您可以選取**自訂**toospecify 自訂日期範圍。
>
>

## <a name="next-steps"></a>後續步驟

* 使用[中記錄分析記錄搜尋](log-analytics-log-searches.md)tooview 詳細 Service Fabric 事件資料。
