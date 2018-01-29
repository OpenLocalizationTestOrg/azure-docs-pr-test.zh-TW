---
title: "升級和調整 Azure API 管理執行個體的規模 | Microsoft Docs"
description: "本主題描述如何升級和調整 Azure API 管理執行個體的規模。"
services: api-management
documentationcenter: 
author: vladvino
manager: anneta
editor: 
ms.service: api-management
ms.workload: integration
ms.topic: article
ms.date: 08/17/2017
ms.author: apimpm
ms.openlocfilehash: 6ae977344101c02222fd9930e26a083bf5e3f800
ms.sourcegitcommit: aaba209b9cea87cb983e6f498e7a820616a77471
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/12/2017
---
# <a name="upgrade-and-scale-an-api-management-instance"></a>升級和調整 API 管理執行個體的規模 

客戶可以新增和移除單位來調整 API 管理 (APIM) 執行個體的規模。 **單位**由專用的 Azure 資源組成，具有一定的承載容量 (以每月 API 呼叫次數表示)。 此數字不代表呼叫限制，而不是允許粗略產能規劃的最大輸送量值。 受到一些因素的影響，實際的輸送量和延遲會大不相同，例如並行連線數和速率、設定的原則種類和數目、要求和回應的大小，以及後端延遲。

每個單位的容量和價格取決於該單位所在的**階層**。 您可以選擇四個層：**開發人員**，**基本**，**標準**， **Premium**。 如果您需要為階層內的服務增加容量，請新增單位。 如果 APIM 執行個體中目前選取的階層不允許新增更多單位，則必須升級至更高的階層。 

每個單位的價格以及可用的功能 (例如，多區域部署)，取決於您為 APIM 執行個體所選擇的階層。 [定價詳細資料](https://azure.microsoft.com/pricing/details/api-management/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio)一文說明每一層的每單位價格和功能。 

>[!NOTE]
>[定價詳細資料](https://azure.microsoft.com/pricing/details/api-management/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio)一文顯示每一層單位容量的大約數字。 若要取得更精確的數字，則需要查看 API 的實際情節。 請參閱接下來的「如何規劃容量」一節。

## <a name="prerequisites"></a>必要條件

若要執行本文所述的步驟，您必須具有：

+ 有效的 Azure 訂用帳戶。

    [!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

+ APIM 執行個體。 如需詳細資訊，請參閱[建立 Azure API 管理執行個體](get-started-create-service-instance.md)。

## <a name="how-to-plan-for-capacity"></a>如何規劃容量？

若要了解是否有足夠的單位來處理流量，請測試您預期的工作負載。 

如上所述，APIM 單位每秒可處理的要求數取決於許多變數。 例如，連線模式、要求和回應的大小、每個 API 上設定的原則、傳送要求的用戶端數目。

使用**計量** (Azure 監視器功能) 來了解任何特定時刻使用多少容量。

### <a name="use-the-azure-portal-to-examine-metrics"></a>使用 Azure 入口網站檢查計量 

1. 在 [Azure 入口網站](https://portal.azure.com/)中，瀏覽至您的 APIM 執行個體。
2. 選取 [計量]。
3. 從 [可用的計量] 中選取 [容量] 計量。 

    容量計量可讓您了解租用戶中使用多少可用計算容量。 其值衍生自您的租用戶所使用的計算資源，例如記憶體、CPU 和網路佇列長度。 這不是正在處理之要求數目的直接量值。 您可藉由增加租用戶的要求負載，以及監視尖峰負載對應的容量計量值來進行測試。 您可以設定計量警示，以得知有非預期的情況發生。 例如，APIM 執行個體已超出其預期尖峰容量超過 10 分鐘。

    >[!TIP]
    > 您可以設定警示以得知服務的容量不足，或呼叫邏輯應用程式來自動新增單位，以調整規模。

## <a name="upgrade-and-scale"></a>升級和調整規模 

如先前所述，您可以選擇四個層：**開發人員**，**基本**，**標準**和**Premium**。 **開發人員**層應該用來評估服務，不適用於生產環境。 **開發人員**層沒有 SLA，您無法調整此階層的規模 (新增/移除單位)。 

**基本**，**標準**和**Premium**是生產環境層有 SLA，而且可以調整。 **基本**層便宜層具有 SLA，而且它可以縮放的最多 2 單位**標準**階層都可以擴充到最多四個單位。 可新增至**進階**層的單位數沒有限制。

**進階**層可讓您將單一 API 管理執行個體分散到您想要的 Azure 區域，而且數目不限。 最初建立 API 管理服務時，執行個體只包含一個單位，而且位於單一 Azure 區域中。 初始區域會指定為**主要**區域。 您可以輕鬆新增更多區域。 新增區域時，您需要指定想要配置的單位數。 例如，您在**主要**區域中可以有一個單位，而在其他某些區域中有五個單位。 您可以依每個區域中的流量來調整單位數。 如需詳細資訊，請參閱[如何將 Azure API 管理服務執行個體部署到多個 Azure 區域](api-management-howto-deploy-multi-region.md)。

您可以升級到任何階層，也能從任何階層降級。 請注意，升級或降級時，可以移除某些功能-例如，Vnet 或多區域部署從 Premium 層降級為標準或基本。

>[!NOTE]
>升級或調整程序需要 15 到 45 分鐘才會生效。 完成時會通知您。

### <a name="use-the-azure-portal-to-upgrade-and-scale"></a>使用 Azure 入口網站來升級和調整規模

1. 在 [Azure 入口網站](https://portal.azure.com/)中，瀏覽至您的 APIM 執行個體。
2. 選取 [級別與價格]。
3. 挑選所需階層。
4. 指定您想要新增的**單位**數。 您可以使用滑桿或輸入單位數。<br/>
    如果您選擇**進階**層，則必須先選取區域。
5. 按下 [儲存]

## <a name="next-steps"></a>後續步驟

[如何將 Azure API 管理服務執行個體部署到多個 Azure 區域](api-management-howto-deploy-multi-region.md)

