---
title: "aaaMonitor 作業、 事件與負載平衡器的計數器 |Microsoft 文件"
description: "了解 tooenable 警示的事件，並探查 Azure 負載平衡器的健全狀況狀態記錄"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 56656d74-0241-4096-88c8-aa88515d676d
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: ac53c2254e06cad780ad6144c5c30f0085d12576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-for-azure-load-balancer"></a>Azure 負載平衡器的記錄檔分析

您可以在 Azure toomanage 中使用不同類型的記錄檔，並進行疑難排解的負載平衡器。 這些記錄檔的某些可以存取透過 hello 入口網站。 從 Azure Blob 儲存體可以擷取所有記錄，並且在不同的工具中進行檢視 (例如 Excel 和 PowerBI)。 您可以深入了解 hello 不同類型的記錄檔從 hello 下方的清單。

* **稽核記錄檔：**您可以使用[Azure 稽核記錄檔](../monitoring-and-diagnostics/insights-debugging-with-events.md)（之前稱為操作記錄檔） tooview 要提交的 tooyour Azure 訂閱，且其狀態的所有作業。 依預設，會啟用稽核記錄檔，並可以在 hello Azure 入口網站中檢視。
* **警示事件記錄檔：**您可以使用此記錄 tooview 警示 rasied hello 負載平衡器。 hello 狀態 hello 負載平衡器會收集每隔五分鐘。 只有在引發負載平衡器警示事件時，才會寫入此記錄檔。
* **健全狀況探查記錄檔：**您可以使用您的健全狀況探查，例如您的後端集區中沒有接收要求從 hello 負載平衡器健全狀況探查失敗的執行個體的 hello 數目所偵測到此記錄 tooview 問題。 此記錄檔會寫入 toowhen 沒有 hello 健全狀況探查狀態的變更。

> [!IMPORTANT]
> 記錄檔分析目前僅適用於網際網路面向的負載平衡器。 記錄檔只可供部署在 hello Resource Manager 部署模型中的資源。 您無法使用記錄檔 hello 傳統部署模型中的資源。 如需 hello 部署模型的詳細資訊，請參閱[了解資源管理員部署和傳統部署](../azure-resource-manager/resource-manager-deployment-model.md)。

## <a name="enable-logging"></a>啟用記錄

每個 Resource Manager 資源都會自動啟用稽核記錄。 您需要 tooenable 事件和健全狀況探查記錄 toostart 收集 hello 資料可透過這些記錄檔。 使用下列步驟 tooenable 記錄 hello。

登入 toohello [Azure 入口網站](http://portal.azure.com)。 如果您還沒有負載平衡器，請先 [建立負載平衡器](load-balancer-get-started-internet-arm-ps.md) 再繼續。

1. 在 hello 入口網站中，按一下 **瀏覽**。
2. 選取 [負載平衡器]。

    ![入口網站 - 負載平衡器](./media/load-balancer-monitor-log/load-balancer-browse.png)

3. 選取現有的負載平衡器 >> [所有設定]。
4. 右側 hello hello 對話方塊 hello hello 負載平衡器名稱下，捲動太**監視**，按一下 **診斷**。

    ![入口網站 - 負載平衡器 - 設定](./media/load-balancer-monitor-log/load-balancer-settings.png)

5. 在 hello**診斷**窗格下**狀態**，選取**上**。
6. 按一下 [儲存體帳戶]。
7. 在 [記錄] 下方，選取現有的儲存體帳戶或建立一個新的。 使用 hello 滑桿 toodetermine 過去事件資料會儲存在 hello 事件記錄檔的天數。 
8. 按一下 [儲存] 。

    ![入口網站 - 診斷記錄檔](./media/load-balancer-monitor-log/load-balancer-diagnostics.png)

> [!NOTE]
> 稽核記錄檔不需要個別的儲存體帳戶。 hello 使用的儲存體事件和健全狀況探查記錄將會產生服務費用。

## <a name="audit-log"></a>稽核記錄檔

根據預設，會產生 hello 稽核記錄。 hello 記錄檔會保留 90 天，在 Azure 的事件記錄檔存放區中。 深入了解這些記錄檔讀取 hello[檢視的事件，並稽核記錄檔](../monitoring-and-diagnostics/insights-debugging-with-events.md)發行項。

## <a name="alert-event-log"></a>警示事件記錄檔

您必須對每一個負載平衡器進行啟用，才會產生此記錄檔。 hello 事件記錄以 JSON 格式，儲存在您指定當您啟用 hello 記錄的 hello 儲存體帳戶。 hello 以下是事件的範例。

```json
{
    "time": "2016-01-26T10:37:46.6024215Z",
    "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
    "category": "LoadBalancerAlertEvent",
    "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
    "operationName": "LoadBalancerProbeHealthStatus",
    "properties": {
        "eventName": "Resource Limits Hit",
        "eventDescription": "Ports exhausted",
        "eventProperties": {
            "public ip address": "40.117.227.32"
        }
    }
}
```

hello JSON 輸出會顯示 hello *eventname*屬性會描述 hello 負載平衡器的 hello 原因建立警示。 在此情況下，產生的 hello 警示已到期 tooTCP 連接埠耗盡來源 IP NAT 限制所造成 (SNAT)。

## <a name="health-probe-log"></a>健全狀況探查記錄檔

如果您已如上所述對每一個負載平衡器進行啟用，才會產生此記錄檔。 hello 資料會儲存在您指定當您啟用 hello 記錄的 hello 儲存體帳戶。 會建立名為 ' insights-記錄檔-loadbalancerprobehealthstatus' 的容器，並會記錄下列資料的 hello:

```json
{
    "records":[
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 1,
            "healthPercentage": 50.000000
        }
    },
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 0,
            "healthPercentage": 100.000000
        }
    }]
}
```

hello JSON 輸出會顯示以 hello 屬性欄位 hello 基本資訊 hello 探查健全狀態。 hello *dipDownCount*屬性會顯示 hello 後端不接收網路流量，因為 toofailed 探查回應其上的執行個體的 hello 總數。

## <a name="view-and-analyze-hello-audit-log"></a>檢視及分析 hello 稽核記錄檔

您可以檢視及分析稽核記錄檔資料，使用任何 hello 下列方法：

* **Azure 工具：**從 Azure PowerShell，hello Azure 命令列介面 (CLI) (hello Azure REST API，透過 hello 稽核記錄檔中擷取資訊或 hello Azure preview 入口網站。 每個方法的逐步指示的詳細 hello[稽核與資源管理員作業](../azure-resource-manager/resource-group-audit.md)發行項。
* **Power BI︰**如果您還沒有 [Power BI](https://powerbi.microsoft.com/pricing) 帳戶，您可以免費試用。 使用 hello [Power BI 的 Azure 稽核記錄內容套件](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs)、 您可以分析資料與預先設定的儀表板，或您可以自訂檢視 toosuit 您的需求。

## <a name="view-and-analyze-hello-health-probe-and-event-log"></a>檢視及分析 hello 健全狀況探查和事件記錄檔

您需要 tooconnect tooyour 儲存體帳戶，並擷取事件和健全狀況探查記錄檔的 hello JSON 記錄項目。 一旦您下載 hello JSON 檔案，您可以將它們轉換 tooCSV 和 Excel、 power Bi 或任何其他資料視覺效果工具中的檢視。

> [!TIP]
> 如果您熟悉 Visual Studio 和變更值的常數和變數在 C# 中的基本概念，您可以使用 hello[記錄轉換器工具](https://github.com/Azure-Samples/networking-dotnet-log-converter)可從 GitHub 取得。

## <a name="additional-resources"></a>其他資源

* [使用 Power BI 視覺化您的 Azure 稽核記錄檔](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) 部落格文章。
* [在 Power BI 和其他工具中檢視和分析 Azure 稽核記錄](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) 部落格文章。

## <a name="next-steps"></a>後續步驟

[了解負載平衡器偵查](load-balancer-custom-probe-overview.md)
