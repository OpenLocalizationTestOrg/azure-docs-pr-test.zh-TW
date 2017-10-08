---
title: "雲端服務配置失敗 aaaTroubleshooting |Microsoft 文件"
description: "疑難排解在 Azure 中部署雲端服務時發生的配置失敗"
services: azure-service-management, cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 529157eb-e4a1-4388-aa2b-09e8b923af74
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: dfd5cc4663ccc6ed1b27ca9df579182737363b0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-allocation-failure-when-you-deploy-cloud-services-in-azure"></a>疑難排解在 Azure 中部署雲端服務時發生的配置失敗
## <a name="summary"></a>摘要
當您部署雲端服務的執行個體 tooa 或加入新的 web 或背景工作角色執行個體時，Microsoft Azure 配置計算資源。 您到達 hello Azure 訂用帳戶限制之前執行這些作業時，您偶爾可能會收到錯誤。 本文說明 hello 一些 hello 的一般配置失敗的原因，並建議可能的補救措施。 當您計劃 hello 部署您的服務，hello 資訊可能也很有用。

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

### <a name="background--how-allocation-works"></a>背景 – 配置的運作方式
在 Azure 資料中心的 hello 伺服器會分割成叢集。 在多個叢集中嘗試新的雲端服務配置要求。 Hello 第一個執行個體與部署的 tooa 雲端服務 （在預備環境或生產），為雲端服務時取得釘選的 tooa 叢集。 任何其他部署的 hello 雲端服務將會發生在 hello 相同叢集。 在本文中，我們將參照 toothis 為 「 已釘選的 tooa 叢集 」。 下面圖 1 說明 hello 案例的標準配置，而不會嘗試在多個叢集。圖 2 說明 hello 裝載的已釘選的 tooCluster 2，其中是 hello 現有雲端服務 CS_1 因為發生配置的大小寫。

![配置圖表](./media/cloud-services-allocation-failure/Allocation1.png)

### <a name="why-allocation-failure-happens"></a>配置失敗的原因
釘選的 tooa 叢集配置要求時，有更高版本可能會因為 hello 可用的資源集區是有限的 tooa 叢集失敗 toofind 釋出資源。 此外，如果您配置的要求是已釘選的 tooa 叢集但 hello 您要求的資源類型不支援該叢集，您的要求將會失敗，hello 叢集在沒有可用的資源。 圖 3 說明 hello 案例，其中已釘選的配置失敗，因為 hello 只有候選叢集沒有可用的資源。 圖 4 說明其中釘選的配置失敗，因為只有候選群集 hello 不支援的 hello 情況 hello 即使 hello 叢集已釋放資源，請要求 VM 大小。

![釘選配置失敗](./media/cloud-services-allocation-failure/Allocation2.png)

## <a name="troubleshooting-allocation-failure-for-cloud-services"></a>雲端服務配置失敗的疑難排解
### <a name="error-message"></a>錯誤訊息
您可能會看到下列錯誤訊息的 hello:

    "Azure operation '{operation id}' failed with code Compute.ConstrainedAllocationFailed. Details: Allocation failed; unable toosatisfy constraints in request. hello requested new service deployment is bound tooan Affinity Group, or it targets a Virtual Network, or there is an existing deployment under this hosted service. Any of these conditions constrains hello new deployment toospecific Azure resources. Please retry later or try reducing hello VM size or number of role instances. Alternatively, if possible, remove hello aforementioned constraints or try deploying tooa different region."

### <a name="common-issues"></a>常見問題
以下是 hello 配置的常見案例會造成配置要求 toobe 釘選的 tooa 單一叢集。

* 部署 tooStaging 位置-如果雲端服務部署中任一個位置，然後 hello 整個雲端服務是已釘選的 tooa 特定叢集。  這表示，如果部署已經存在於 hello 生產位置，然後新的預備環境部署只可配置在 hello 相同叢集為 hello 生產位置。 如果 hello 叢集已接近其容量，hello 要求可能會失敗。
* 調整-加入新執行個體 tooan 現有的雲端服務必須配置中的 hello 相同叢集。  小型的調整要求通常可配置，但並不盡然。 如果 hello 叢集已接近其容量，hello 要求可能會失敗。
* 親和性群組-新的部署 tooan 空的雲端服務可以將任何在該區域中，叢集中的 hello 網狀架構由配置，除非 hello 雲端服務是已釘選的 tooan 同質群組。 部署 toohello 相同同質群組將會在 hello 嘗試相同的叢集。 如果 hello 叢集已接近其容量，hello 要求可能會失敗。
* 同質群組 vNet 的較舊的虛擬網路繫結的 tooaffinity 群組，而不是地區，而且這些虛擬網路中的雲端服務會釘選的 toohello 同質群組的叢集。 釘選的 hello 叢集上，將會嘗試部署的虛擬網路的 toothis 類型。 如果 hello 叢集已接近其容量，hello 要求可能會失敗。

## <a name="solutions"></a>解決方案
1. 重新部署 tooa 新的雲端服務-此解決方案為它可讓所有的叢集，在該區域中的 hello 平台 toochoose 可能 toobe 最成功。

   * Hello 工作負載 tooa 新雲端服務部署  
   * 更新 hello 或 CNAME 記錄 toopoint 流量 toohello 新的雲端服務
   * 一旦零流量即將 toohello 舊的站台，您可以刪除 hello 舊的雲端服務。 此解決方案不需要停機。
2. 刪除生產和預備位置-這個解決方案將會保留現有的 DNS 名稱，但會導致停機時間 tooyour 應用程式。

   * 刪除 hello 生產和預備位置的現有雲端服務，以便 hello 雲端服務是空的然後按一下
   * Hello 現有雲端服務中建立新的部署。 這會重新嘗試 tooallocation hello 區域中的所有叢集上。 確定 hello 雲端服務不是繫結的 tooan 同質群組。
3. 保留的 IP-此方案將會保留您現有的 IP 位址，但是會造成停機時間 tooyour 應用程式。  

   * 使用 Powershell 為您現有的部署建立 ReservedIP

     ```
     New-AzureReservedIP -ReservedIPName {new reserved IP name} -Location {location} -ServiceName {existing service name}
     ```
   * 請遵循 corresponding，進行確定 toospecify hello hello 服務 CSCFG 中新的 ReservedIP #2。
4. 移除新部署中的同質群組 - 不再建議使用同質群組。 請遵循上面 toodeploy 新的雲端服務的 #1 的步驟。 請確定雲端服務不在同質群組中。
5. 轉換 tooa 區域虛擬網路-請參閱[如何從同質群組 tooa 區域虛擬網路 (VNet) toomigrate](../virtual-network/virtual-networks-migrate-to-regional-vnet.md)。
