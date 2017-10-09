---
title: "設定 ExpressRoute 電路 aaaWorkflows |Microsoft 文件"
description: "此頁面會引導您完成設定 ExpressRoute 電路和對等互連的 hello 工作流程"
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 55e0418c-e0bf-44a7-9aa1-720076df9297
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: cherylmc
ms.openlocfilehash: 8e1dfc137401e0d6d53608ae6c8de0085e182eba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-workflows-for-circuit-provisioning-and-circuit-states"></a>ExpressRoute 工作流程線路佈建和線路狀態
此頁面會引導您透過 hello 服務佈建和以高層級的路由設定工作流程。

![](./media/expressroute-workflows/expressroute-circuit-workflow.png)

hello 圖和相對應的步驟會顯示 hello 工作必須遵循順序 toohave ExpressRoute 循環佈建的端對端。 

1. 使用 PowerShell tooconfigure ExpressRoute 電路。 遵循指示進行 hello hello[建立 ExpressRoute 電路](expressroute-howto-circuit-classic.md)文件以取得更多詳細資料。
2. 順序從 hello 服務提供者的連線。 此過程視情況而異。 如需有關如何連絡您的連線服務提供者 tooorder 連線。
3. 請確定，hello 循環已佈建已順利驗證 hello ExpressRoute 循環佈建透過 PowerShell 的狀態。 
4. 設定路由網域。 如果連線提供者為您管理第 3 層，他們會為您的線路設定路由。 如果您連線服務提供者只提供第 2 層服務，您必須設定每 hello 中所述的指導方針路由[路由需求](expressroute-routing.md)和[路由組態](expressroute-howto-routing-classic.md)頁面。
   
   * 啟用 Azure 私人互連-您必須啟用此對等互連 tooconnect tooVMs / 雲端服務部署在虛擬網路內。
   * 啟用 Azure 公用對等互連-您必須啟用 Azure 公用對等互連如果您想 tooconnect tooAzure 服務裝載於公用 IP 位址。 如果您選擇的 Azure 私人互連的 tooenable 預設路由，這是需求 tooaccess Azure 資源。
   * 啟用 Microsoft 對等互連-您必須啟用 Office 365 和 Dynamics 365 這個 tooaccess。 
     
     > [!IMPORTANT]
     > 您必須確定您使用不同的 proxy 邊緣 tooconnect tooMicrosoft 比 hello 您用於 hello 網際網路。 使用的 hello hello 網際網路和 ExpressRoute 的相同邊緣會導致非對稱路由，而導致您網路的連線中斷。
     > 
     > 
     
     ![](./media/expressroute-workflows/routing-workflow.png)
5. 連結虛擬網路 tooExpressRoute 電路-您可以將虛擬網路 tooyour ExpressRoute 電路的連結。 請依照下列指示[toolink Vnet](expressroute-howto-linkvnet-arm.md) tooyour 循環。 這些 Vnet 可以在 hello 相同 Azure 訂用帳戶 hello ExpressRoute 循環，或可以位於不同的訂用帳戶。

## <a name="expressroute-circuit-provisioning-states"></a>ExpressRoute 線路佈建狀態
每個 ExpressRoute 線路有兩種狀態：

* 服務提供者佈建狀態
* 狀態

Status 代表 Microsoft 的佈建狀態。 這個屬性是設定 tooEnabled，當您建立 Expressroute 電路

hello 連線提供者佈建狀態代表 hello hello 連線提供者端的狀態。 可能是 *NotProvisioned*、*Provisioning* 或 *Provisioned*。 hello ExpressRoute 電路必須位於已佈建狀態，以便您 toobe 無法 toouse 它。

### <a name="possible-states-of-an-expressroute-circuit"></a>ExpressRoute 線路的可能狀態
此區段會列出 hello 的 ExpressRoute 電路的可能狀態。

**在建立時**

您會看見 hello ExpressRoute 電路 hello 下列狀態，只要您在執行 hello PowerShell cmdlet toocreate hello ExpressRoute 電路。

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


**當連線服務提供者處於 hello 的佈建 hello 循環的程序**

您會看到 hello ExpressRoute 電路 hello 下列狀態，只要您在傳遞 hello 服務金鑰 toohello 連線服務提供者，並在開始佈建程序的 hello。

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled


**當連線服務提供者已完成佈建程序的 hello**

您會看到 hello hello 下列狀態，只要 hello 連線服務提供者已完成 hello 佈建程序中的 ExpressRoute 電路。

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled

佈建並啟用僅限 hello 狀態 hello 循環可在適用於您 toobe 無法 toouse 它。 如果您使用第 2 層提供者，則只有當線路處於此狀態下，您才能設定路由。

**當連線服務提供者正在取消佈建 hello 循環**

如果您要求 hello 服務提供者 toodeprovision hello ExpressRoute 循環，您會看到 hello 循環設定 toohello 遵循 hello 服務提供者完成 hello 解除佈建程序之後的狀態。

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


您可以選擇 toore 啟用它，如果需要或是執行 PowerShell 指令程式 toodelete hello 循環。  

> [!IMPORTANT]
> 如果您執行 hello PowerShell cmdlet toodelete hello 循環 hello ServiceProviderProvisioningState 時佈建 」 或 「 已佈建 hello 作業將會失敗。 請先使用您的連線提供者 toodeprovision hello ExpressRoute 循環，然後刪除 hello 循環。 Microsoft 將持續 toobill hello 循環，直到您執行 hello PowerShell cmdlet toodelete hello 循環。
> 
> 

## <a name="routing-session-configuration-state"></a>路由工作階段組態狀態
hello BGP 佈建狀態可讓您得知是否已經啟用 hello Microsoft edge hello BGP 工作階段。 hello 狀態必須啟用您 toobe 無法 toouse hello 對等互連。

它是特別為 Microsoft 對等互連重要 toocheck hello BGP 工作階段狀態。 在加法 toohello BGP 佈建狀態，則呼叫另一個狀態*公告公用首碼狀態*。 hello 公告公用首碼狀態必須是在*設定*狀態，而同時向上 hello BGP 工作階段 toobe 以及您路由 toowork 端對端。 

如果 hello 公告公用首碼狀態會設 tooa*驗證所需*狀態時，未啟用 hello BGP 工作階段，如 hello 公告前置詞不符合 hello 中 hello 路由所登錄的任何數字。 

> [!IMPORTANT]
> Hello 公告公用首碼狀態是否在*進行手動驗證*狀態時，您必須開啟支援票證給[Microsoft 支援服務](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)並提供您自己沿著通告 hello IP 位址的辨識項hello 相關聯自發系統編號。
> 
> 

## <a name="next-steps"></a>後續步驟
* 設定 ExpressRoute 連線。
  
  * [建立 ExpressRoute 線路](expressroute-howto-circuit-arm.md)
  * [設定路由](expressroute-howto-routing-arm.md)
  * [連結的 VNet tooan ExpressRoute 電路](expressroute-howto-linkvnet-arm.md)

