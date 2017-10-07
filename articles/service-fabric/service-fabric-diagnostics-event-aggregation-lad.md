---
title: "服務網狀架構事件彙總使用 Linux Azure 診斷 aaaAzure |Microsoft 文件"
description: "了解如何使用 LAD 彙總及收集事件，來監視和診斷 Azure Service Fabric 叢集。"
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
ms.date: 07/17/2017
ms.author: dekapur
ms.openlocfilehash: aefa869219a0dd219e01e6574816fe3ce47fe472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-linux-azure-diagnostics"></a>使用 Linux Azure 診斷的事件彙總和收集
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-event-aggregation-wad.md)
> * [Linux](service-fabric-diagnostics-event-aggregation-lad.md)
>
>

執行 Azure Service Fabric 叢集時，它是個不錯的主意 toocollect hello 記錄檔儲存在集中位置的所有 hello 節點。 在中央位置擁有 hello 記錄檔可協助您分析和疑難排解問題在叢集中或在 hello 應用程式和服務在該叢集中執行的問題。

其中一種方式 tooupload 及收集記錄檔是 toouse hello Linux Azure 診斷 （年輕人） 延伸，其中上傳記錄檔 tooAzure 存放裝置，而且也 hello 選項 toosend 記錄 tooAzure Application Insights 或事件中心。 您也可以使用外部處理序 tooread hello 事件從儲存體，並放在中，已分析的平台產品，例如[OMS 記錄分析](../log-analytics/log-analytics-service-fabric.md)或另一個記錄檔剖析方案。

## <a name="log-and-event-sources"></a>記錄和事件來源

### <a name="service-fabric-platform-events"></a>Service Fabric 平台事件
Service Fabric 會透過 [LTTng](http://lttng.org) 發出少數的現成記錄，包括運作事件或執行階段事件。 這些記錄會儲存在 hello hello 叢集的資源管理員範本指定的位置。 tooget 或設定 hello 儲存體帳戶的詳細資訊，請搜尋 hello 標記**AzureTableWinFabETWQueryable**並尋找**StoreConnectionString**。

### <a name="application-events"></a>應用程式事件
 檢測軟體時，會如您在應用程式和服務的程式碼中所指定的，發出事件。 您可以使用任何撰寫文字型記錄檔的記錄解決方案，例如 LTTng。 如需詳細資訊，請參閱 hello LTTng 文件上追蹤您的應用程式。

[監視和診斷本機開發設定中的服務](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)。

## <a name="deploy-hello-diagnostics-extension"></a>Hello 診斷延伸模組部署
hello 收集記錄檔中的第一個步驟是 toodeploy hello 診斷延伸模組，每個 hello Service Fabric 叢集中的 hello Vm 上。 hello 診斷延伸模組會收集每個 VM 上的記錄檔，並將其上傳 toohello 您指定的儲存體帳戶。 hello 步驟會根據您使用 hello Azure 入口網站或 Azure 資源管理員而有所不同。

toodeploy hello 診斷延伸模組 toohello Vm 做為叢集建立一部分的 hello 叢集中設定**診斷**太**上**。 建立 hello 叢集之後，您無法使用 hello 入口網站來變更此設定。

然後，設定 Linux Azure 診斷 （年輕人） toocollect hello 檔案，並將它們放入您的儲存體帳戶。 此程序會說明案例 （[上傳您自己的記錄檔]） hello 文件中的 3[使用年輕人 toomonitor 及診斷 Linux Vm](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。 遵循此程序取得，存取 toohello 追蹤。 您可以上傳您所選擇的 hello 追蹤 tooa 視覺化檢視。

您也可以使用 Azure Resource Manager 部署 hello 診斷延伸模組。 hello 程序類似於 Windows 及 Linux 與 Windows 叢集的已記錄[toocollect 使用 Azure 診斷的記錄方式](service-fabric-diagnostics-how-to-setup-wad.md)。

您也可以使用 Operations Management Suite，如 [Operations Management Suite Log Analytics with Linux (搭配 Linux 使用 Operations Management Suite Log Analytics)](https://blogs.technet.microsoft.com/hybridcloud/2016/01/28/operations-management-suite-log-analytics-with-linux/) 中所述。

完成這項設定之後，hello 年輕人代理程式監視 hello 指定的記錄檔。 每當新的一行時附加的 toohello 檔案，它會建立可供您指定傳送的 toohello 儲存體的 syslog 項目。

## <a name="next-steps"></a>後續步驟

請參閱詳細 toounderstand 問題，問題進行疑難排解時，您應該檢查哪些事件[LTTng 文件](http://lttng.org/docs)和[使用年輕人](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。
