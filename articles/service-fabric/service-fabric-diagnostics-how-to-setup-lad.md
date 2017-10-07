---
title: "使用 Linux Azure 診斷程式 aaaCollect 記錄檔 |Microsoft 文件"
description: "本文說明如何設定 Azure 診斷 toocollect tooset 記錄從 Azure 中執行的服務網狀架構 Linux 叢集。"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: a160d469-8b7d-4560-82dd-8500db34a44a
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/28/2017
ms.author: subramar
ms.openlocfilehash: f61172876e744ea3e361f9ae513254239d6ba27f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="collect-logs-by-using-azure-diagnostics"></a>使用 Azure 診斷收集記錄檔
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-setup-wad.md)
> * [Linux](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

執行 Azure Service Fabric 叢集時，它是個不錯的主意 toocollect hello 記錄檔儲存在集中位置的所有 hello 節點。 在中央位置擁有 hello 記錄檔可讓您輕鬆 tooanalyze 並提升疑難排解的問題，不論其正在您的服務、 應用程式或 hello 叢集本身。 其中一種方式 tooupload 及收集記錄檔是 toouse hello Azure 診斷擴充功能，哪一個上傳記錄 tooAzure 儲存體、 Azure Application Insights 或 Azure 事件中心。 您也可以讀取儲存體或事件中心的 hello 事件並例如將它們放在產品中[記錄分析](../log-analytics/log-analytics-service-fabric.md)或另一個記錄檔剖析方案。 [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) 隨附完整的記錄檔搜尋與分析服務內建功能。

## <a name="log-sources-that-you-might-want-toocollect"></a>您可能想 toocollect 的記錄檔來源
* **Service Fabric 記錄**: hello 平台，透過從發出[LTTng](http://lttng.org)和上傳 tooyour 儲存體帳戶。 記錄檔可能會操作事件，或發出 hello 平台的執行階段事件。 這些記錄會儲存在 hello 位置指定該 hello 叢集資訊清單。 (tooget hello 儲存體帳戶詳細資料，搜尋 hello 標記**AzureTableWinFabETWQueryable**並尋找**StoreConnectionString**。)
* **應用程式事件**：從服務程式碼發出。 您可以使用任何撰寫文字型記錄檔的記錄解決方案，例如 LTTng。 如需詳細資訊，請參閱 hello LTTng 文件上追蹤您的應用程式。  

## <a name="deploy-hello-diagnostics-extension"></a>Hello 診斷延伸模組部署
hello 收集記錄檔中的第一個步驟是 toodeploy hello 診斷延伸模組，每個 hello Service Fabric 叢集中的 hello Vm 上。 hello 診斷延伸模組會收集每個 VM 上的記錄檔，並將其上傳 toohello 您指定的儲存體帳戶。 hello 步驟會根據您使用 hello Azure 入口網站或 Azure 資源管理員而有所不同。

toodeploy hello 診斷延伸模組 toohello Vm 做為叢集建立一部分的 hello 叢集中設定**診斷**太**上**。 建立 hello 叢集之後，您無法使用 hello 入口網站來變更此設定。

然後，設定 Linux Azure 診斷 （年輕人） toocollect hello 檔案，並將它們放入您的儲存體帳戶。 此程序會說明案例 （[上傳您自己的記錄檔]） hello 文件中的 3[使用年輕人 toomonitor 及診斷 Linux Vm](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。 遵循此程序取得，存取 toohello 追蹤。 您可以上傳您所選擇的 hello 追蹤 tooa 視覺化檢視。

您也可以使用 Azure Resource Manager 部署 hello 診斷延伸模組。 hello 程序類似於 Windows 及 Linux 與 Windows 叢集的已記錄[toocollect 使用 Azure 診斷的記錄方式](service-fabric-diagnostics-how-to-setup-wad.md)。

您也可以使用 Operations Management Suite，如 [Operations Management Suite Log Analytics with Linux (搭配 Linux 使用 Operations Management Suite Log Analytics)](https://blogs.technet.microsoft.com/hybridcloud/2016/01/28/operations-management-suite-log-analytics-with-linux/) 中所述。

完成這項設定之後，hello 年輕人代理程式監視 hello 指定的記錄檔。 每當新的一行時附加的 toohello 檔案，它會建立可供您指定傳送的 toohello 儲存體的 syslog 項目。

## <a name="next-steps"></a>後續步驟
請參閱詳細 toounderstand 問題，問題進行疑難排解時，您應該檢查哪些事件[LTTng 文件](http://lttng.org/docs)和[使用年輕人](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。

