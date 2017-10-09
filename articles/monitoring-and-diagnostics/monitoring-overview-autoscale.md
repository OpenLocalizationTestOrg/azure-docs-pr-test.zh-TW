---
title: "在 Microsoft Azure 虛擬機器、 雲端服務和 Web 應用程式的自動調整規模的 aaaOverview |Microsoft 文件"
description: "Microsoft Azure 的自動調整概觀。 適用於 tooVirtual 機器、 雲端服務和 Web 應用程式。"
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 74bf03be-e658-4239-a214-c12424b53e4c
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2016
ms.author: robb
ms.openlocfilehash: ef68b722ea22c4149a7d7a89c5855ba761db9247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-autoscale-in-microsoft-azure-virtual-machines-cloud-services-and-web-apps"></a>Microsoft Azure 虛擬機器、雲端服務和 Web Apps 的自動調整概觀
本文說明哪些 Microsoft Azure 自動調整規模，其優點，以及 tooget 如何開始使用它。  

Azure 監視的自動調整規模太只適用於[虛擬機器擴展集](https://azure.microsoft.com/services/virtual-machine-scale-sets/)，[雲端服務](https://azure.microsoft.com/services/cloud-services/)，和[應用程式服務-Web 應用程式](https://azure.microsoft.com/services/app-service/web/)。

> [!NOTE]
> Azure 有兩種自動調整方法。 較舊版本的自動調整規模適用於 tooVirtual 機器 （可用性設定組）。 這項功能具有有限的支援，我們建議您移轉 toovirtual 機器小數位數設定為更快速且更可靠的自動調整規模的支援。 本文章中隨附上如何 toouse hello 舊技術的連結。  
>
>

## <a name="what-is-autoscale"></a>何謂自動調整？
自動調整規模可讓您 toohave hello 適量的資源在您的應用程式上執行 toohandle hello 負載。 它可讓您 tooadd 資源 toohandle 增加的負載，而且也藉由移除資源，會有某些閒置節省成本。 您指定的執行個體 toorun 最小和最大數目和新增或移除 Vm 會自動根據一組規則。 設定下限可確保即使沒有負載應用程式也會一直執行。 設定上限則可限制每小時可能產生的總成本。 您可以使用您所建立的規則自動在這兩個極端值之間進行調整。

 ![說明自動調整。 新增和移除 VM](./media/monitoring-overview-autoscale/AutoscaleConcept.png)

符合規則條件時，就會觸發一個或多個自動調整動作。 您可以新增和移除 VM，或執行其他動作。 hello 概念圖顯示此程序。  

 ![自動調整流程圖](./media/monitoring-overview-autoscale/Autoscale_Overview_v4.png)

hello 以下說明適用於 toohello hello 上圖中的部分。   

## <a name="resource-metrics"></a>資源計量
資源會發出計量，這些計量稍後會由規則處理。 度量來自不同的方法。
虛擬機器級別集合會使用遙測資料從 Azure 診斷代理程式，而 Web 應用程式和雲端服務的遙測直接來自 hello Azure 基礎結構。 一些常用的統計資料包括 CPU 使用率、記憶體使用量、執行緒計數、佇列長度和磁碟使用量。 如需可使用哪些遙測資料的清單，請參閱 [自動調整的常用度量](insights-autoscale-common-metrics.md)。

## <a name="custom-metrics"></a>自訂計量
您也可以運用自己自訂的計量 (由您的應用程式發出)。 如果您已設定您的應用程式 toosend 度量 tooApplication Insights，您可以利用是否這些度量 toomake 決策 tooscale 與否。 

## <a name="time"></a>時間
排程型規則是以 UTC 為基礎。 設定規則時必須正確設定時區。  

## <a name="rules"></a>規則
hello 圖表會顯示一個自動調整規模規則，但您可以有多個。 您可以視情況需要建立複雜的重疊規則。  規則類型包含  

* **度量型** - 例如，當 CPU 使用率高於 50% 時執行此動作。
* **時間型** - 例如，在指定時區的每星期六上午 8 點觸發 Webhook。

度量型規則會測量應用程式負載，並根據該負載新增或移除 VM。 排程為基礎的規則可讓您 tooscale 當您在負載查看時間模式，並想 tooscale 之前可能的負載增加或減少，就會發生。  

## <a name="actions-and-automation"></a>動作與自動化
規則可以觸發一個或多個類型的動作。

* **調整** - 將 VM 相應放大或相應縮小
* **電子郵件**-傳送電子郵件 toosubscription admins、 共同管理員及/或您所指定的其他電子郵件地址
* **透過 Webhook 自動執行** - 呼叫 Webhook，以觸發 Azure 內部或外部的多個複雜動作。 在 Azure 內部，您可以啟動 Azure 自動化 Runbook、Azure 函數或 Azure 邏輯應用程式。 Azure 外部的範例第三方 URL 包含 Slack 和 Twilio 等服務。

## <a name="autoscale-settings"></a>自動調整設定
自動調整規模 hello 後使用的術語和結構。

- **自動調整規模設定**是否已讀取 hello 自動調整引擎 toodetermine tooscale 向上或向下。 它包含一個或多個設定檔，hello 目標資源，並通知設定的相關資訊。

    - **自動調整設定檔**結合了下列項目：

        - **容量設定**、 hello 最小值，最大值，表示和執行個體數目的預設值。
        - **一組規則**，其中的每個規則包含觸發程序 (時間或度量) 和調整動作 (相應增加或相應減少)。
        - **循環**，會指出自動調整應該在何時讓此設定檔生效。

        您可以有多個設定檔，可讓您 tootake care of 不同重疊的需求。 您可以不同時間的日次或星期幾 hello，例如有不同的自動調整規模設定檔。

    - A**通知設定**定義自動調整規模事件發生根據滿足條件的其中一個 hello 自動調整規模設定的設定檔的 hello 準則時，應該就會發生何種通知。 自動調整規模可通知一或多個電子郵件地址，或請呼叫 tooone 或多個 webhook。


![Azure 自動調整設定、設定檔和規則結構](./media/monitoring-overview-autoscale/AzureResourceManagerRuleStructure3.png)

hello 可設定的欄位描述的完整清單位於 hello[自動調整規模 REST API](https://msdn.microsoft.com/library/dn931928.aspx)。

如需程式碼範例，請參閱

* [針對 VM 擴展集使用 Resource Manager 範本進行進階自動調整設定](insights-advanced-autoscale-virtual-machine-scale-sets.md)  
* [自動調整 REST API](https://msdn.microsoft.com/library/dn931953.aspx)

## <a name="horizontal-vs-vertical-scaling"></a>水平和垂直調整
自動調整規模只縮放的水平 （「 出 」） 增加或減少 （「 位置 」） 中 VM 執行個體的 hello 數目。  水平是更有彈性在雲端的情況下它可讓您的 Vm toohandle 負載 toorun 潛在千分位。

對比之下，垂直調整則不同。 它會保持 hello 相同數目的 Vm，但讓 hello （「 向上 」） 更多或較少 （「 向下 」） 功能強大的 Vm。 能力是以記憶體、CPU 速度、磁碟空間等項目來加以測量。垂直調整有更多限制。 它會相依於較大的硬體，快速達到上限，且可能會因區域 hello 可用性。 垂直縮放比例通常也需要 VM toostop 並重新啟動。

如需詳細資訊，請參閱[使用 Azure 自動化垂直調整 Azure 虛擬機器](../virtual-machines/linux/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

## <a name="methods-of-access"></a>存取方法
您可以透過下列途徑設定自動調整

* [Azure 入口網站](insights-how-to-scale.md)
* [PowerShell](insights-powershell-samples.md#create-and-manage-autoscale-settings)
* [跨平台命令列介面 (CLI)](insights-cli-samples.md#autoscale)
* [Azure 監視器 REST API](https://msdn.microsoft.com/library/azure/dn931953.aspx)

## <a name="supported-services-for-autoscale"></a>支援的自動調整服務
| 服務 | 結構描述與文件 |
| --- | --- |
| Web Apps |[調整 Web Apps](insights-how-to-scale.md) |
| 雲端服務 |[自動調整雲端服務](../cloud-services/cloud-services-how-to-scale.md) |
| 虛擬機器：傳統 |[調整傳統的虛擬機器可用性設定組](https://blogs.msdn.microsoft.com/kaevans/2015/02/20/autoscaling-azurevirtual-machines/) |
| 虛擬機器：Windows 擴展集 |[在 Windows 中調整虛擬機器擴展集](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) |
| 虛擬機器：Linux 擴展集 |[在 Linux 中調整虛擬機器擴展集](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) |
| 虛擬機器：Windows 範例 |[針對 VM 擴展集使用 Resource Manager 範本進行進階自動調整設定](insights-advanced-autoscale-virtual-machine-scale-sets.md) |

## <a name="next-steps"></a>後續步驟
深入了解自動調整規模，toolearn 使用自動調整規模逐步解說先前所列的 hello，或參閱 toohello 下列資源：

* [Azure 監視器自動調整的常用度量](insights-autoscale-common-metrics.md)
* [Azure 監視器自動調整的最佳作法](insights-autoscale-best-practices.md)
* [使用自動調整規模動作 toosend 電子郵件和 webhook 警示通知](insights-autoscale-to-webhook-email.md)
* [自動調整 REST API](https://msdn.microsoft.com/library/dn931953.aspx)
* [排解虛擬機器擴展集自動調整的問題](../virtual-machine-scale-sets/virtual-machine-scale-sets-troubleshoot.md)
