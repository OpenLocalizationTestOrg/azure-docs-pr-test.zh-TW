---
title: "aaaMoving ExpressRoute 電路從傳統 tooResource Manager |Microsoft 文件"
description: "此頁面提供的準備事項概觀 tooknow 有關橋接 hello 傳統和 hello 資源管理員部署模型。"
documentationcenter: na
services: expressroute
author: ganesr
manager: carmonm
editor: 
ms.assetid: bdf01217-1a98-4ec0-a08e-d84fd37f78af
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/02/2017
ms.author: ganesr
ms.openlocfilehash: c901d2cda01aec409b528d29fc937ac6afaea511
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="moving-expressroute-circuits-from-hello-classic-toohello-resource-manager-deployment-model"></a>從 hello 傳統 toohello Resource Manager 部署模型中移動的 ExpressRoute 電路
本文章提供概觀，其代表的意義 toomove hello 傳統 toohello Azure Resource Manager 部署模型從 Azure ExpressRoute 電路。

您可以使用單一 ExpressRoute 電路 tooconnect toovirtual 網路部署在傳統的 hello 和 hello 資源管理員部署模型。 ExpressRoute 電路，不論其建立方式，現在可以透過兩種部署模型連結 toovirtual 網路。

![ExpressRoute 電路連結 toovirtual 網路跨這兩種部署模型](./media/expressroute-move/expressroute-move-1.png)

## <a name="expressroute-circuits-that-are-created-in-hello-classic-deployment-model"></a>Hello 傳統部署模型中建立的 ExpressRoute 電路
Hello 傳統部署模型中建立的 ExpressRoute 電路必須移動 toobe toohello 資源管理員部署模型第一個 tooenable 連線 tooboth hello 傳統和 hello 資源管理員部署模型。 移動連線時，不會發生連線中斷的情況。 Hello 傳統部署模型中的所有電路至虛擬網路連結 (在 hello 相同訂用帳戶和跨訂用帳戶) 都會保留下來。

Hello 移動之後已順利完成，hello ExpressRoute 電路的外觀、 執行時，和操作與 ExpressRoute 電路 hello Resource Manager 部署模型中所建立的完全相同。 您現在可以建立連線 toovirtual 網路 hello Resource Manager 部署模型中。

ExpressRoute 電路已移動的 toohello Resource Manager 部署模型之後，您可以管理 hello 生命週期的 hello ExpressRoute 循環只能藉由使用 hello Resource Manager 部署模型。 這表示，您就可以執行作業，例如加入/更新/刪除對等互連，更新循環屬性 （例如頻寬、 SKU 和計費類型），以及刪除電路只在 hello Resource Manager 部署模型。 請參閱下方的 hello Resource Manager 部署模型，如需有關如何管理存取 tooboth 部署模型中建立的電路的 toohello 一節。

您沒有的 tooinvolve 您連線提供者 tooperform hello 移動。

## <a name="expressroute-circuits-that-are-created-in-hello-resource-manager-deployment-model"></a>在 hello Resource Manager 部署模型中建立 ExpressRoute 電路
您可以啟用中建立 hello 資源管理員部署模型 toobe 從這兩種部署模型可存取的 ExpressRoute 電路。 您的訂用帳戶中的任何 ExpressRoute 循環可啟用的 toobe 從這兩種部署模型存取。

* 根據預設，在 hello Resource Manager 部署模型中建立 ExpressRoute 電路並沒有存取 toohello 傳統部署模型。
* 已從 hello 傳統部署模型 toohello 資源管理員部署模型移動的 ExpressRoute 電路從來存取這兩個預設的部署模型。
* ExpressRoute 電路一定會有存取 toohello Resource Manager 部署模型中，不論是否已建立 hello 資源管理員 」 或 「 傳統部署模型中。 這表示您可以建立 toovirtual 網路中建立的連接上依照指示 hello Resource Manager 部署模型[如何 toolink 虛擬網路](expressroute-howto-linkvnet-arm.md)。
* 存取 toohello 傳統部署模型由 hello **allowClassicOperations** hello ExpressRoute 循環中的參數。

> [!IMPORTANT]
> 記載在 hello 的所有配額[服務限制](../azure-subscription-service-limits.md)頁面將套用。 例如，標準的循環可以有最多 10 個虛擬網路連結/連接跨傳統 hello 和 hello 資源管理員部署模型。
> 
> 

## <a name="controlling-access-toohello-classic-deployment-model"></a>控制存取 toohello 傳統部署模型
您可以啟用單一 ExpressRoute 電路 toolink toovirtual 網路部署模型中的設定 hello **allowClassicOperations** hello ExpressRoute 電路的參數。

設定**allowClassicOperations** tooTRUE 可讓您從這兩種部署模型 toohello ExpressRoute 電路 toolink 虛擬網路。 您也可以由下列的指引連結 toovirtual hello 傳統部署模型中的網路上[toolink 虛擬網路中的如何 hello 傳統部署模型](expressroute-howto-linkvnet-classic.md)。 您也可以由下列的指引連結 toovirtual hello Resource Manager 部署模型中的網路上[toolink 虛擬網路中的如何 hello Resource Manager 部署模型](expressroute-howto-linkvnet-arm.md)。

設定**allowClassicOperations** tooFALSE 區塊從 hello 傳統部署模型存取 toohello 循環。 不過，會保留在 hello 傳統部署模型中的所有虛擬網路連結。 在此情況下，hello ExpressRoute 電路看不到 hello 傳統部署模型中。

## <a name="supported-operations-in-hello-classic-deployment-model"></a>Hello 傳統部署模型中支援的作業
hello 遵循傳統作業支援的 ExpressRoute 電路時**allowClassicOperations** tooTRUE 設定：

* 取得 ExpressRoute 線路資訊
* 建立/更新/get/刪除虛擬網路連結 tooclassic 虛擬網路
* 建立/更新/取得/刪除跨訂用帳戶連線的虛擬網路連結授權

您無法執行 hello 下列傳統的作業時**allowClassicOperations** tooTRUE 設定：

* 建立/更新/取得/刪除 Azure 私人、Azure 公用和 Microsoft 對等的邊界閘道協定 (BGP) 對等
* 刪除 ExpressRoute 線路

## <a name="communication-between-hello-classic-and-hello-resource-manager-deployment-models"></a>傳統的 hello 與 hello 資源管理員部署模型之間的通訊
hello ExpressRoute 循環就像是傳統 hello 與 hello 資源管理員部署模型之間的橋樑。 如果這兩個虛擬網路連結的 toohello hello 傳統部署模型中的虛擬網路中的虛擬機器與 hello 資源管理員部署模型都會透過 ExpressRoute 的虛擬網路之間流量相同 ExpressRoute 電路。

彙總輸送量受限於 hello hello 虛擬網路閘道的輸送量容量。 流量不會輸入 hello 連線服務提供者的網路，或是您的網路中這種情況。 Hello Microsoft 網路內完全包含 hello 虛擬網路之間的流量。

## <a name="access-tooazure-public-and-microsoft-peering-resources"></a>存取 tooAzure 公開憑證與 Microsoft 對等的資源
您可以繼續 tooaccess 資源通常可透過 Azure 公用對等及 Microsoft 對等互連，不需要中斷。  

## <a name="whats-supported"></a>支援的項目
本節說明 ExpressRoute 線路會支援的功能：

* 您可以使用單一 ExpressRoute 電路 tooaccess 虛擬網路部署在傳統的 hello 與 hello 資源管理員部署模型。
* 您可以從 hello 傳統 toohello Resource Manager 部署模型中移動 ExpressRoute 電路。 在移動之後，hello ExpressRoute 電路的外觀、 覺得，並執行像任何其他 hello Resource Manager 部署模型中建立 ExpressRoute 電路。
* 您可以移動 hello ExpressRoute 電路。 線路連結、虛擬網路和 VPN 閘道無法透過這項作業移動。
* ExpressRoute 電路已移動的 toohello Resource Manager 部署模型之後，您可以管理 hello 生命週期的 hello ExpressRoute 循環只能藉由使用 hello Resource Manager 部署模型。 這表示，您就可以執行作業，例如加入/更新/刪除對等互連，更新循環屬性 （例如頻寬、 SKU 和計費類型），以及刪除電路只在 hello Resource Manager 部署模型。
* hello ExpressRoute 循環就像是傳統 hello 與 hello 資源管理員部署模型之間的橋樑。 如果這兩個虛擬網路連結的 toohello hello 傳統部署模型中的虛擬網路中的虛擬機器與 hello 資源管理員部署模型都會透過 ExpressRoute 的虛擬網路之間流量相同 ExpressRoute 電路。
* 傳統的 hello 和 hello 資源管理員部署模型可支援跨訂用帳戶連線。
* ExpressRoute 循環離開 hello 傳統模型 toohello Azure Resource Manager 模型之後，您可以[移轉 hello 虛擬網路連結的 toohello ExpressRoute 電路](expressroute-migration-classic-resource-manager.md)。

## <a name="whats-not-supported"></a>不支援的內容
本節說明 ExpressRoute 線路不會支援的功能：

* ExpressRoute 電路 hello 生命週期管理 hello 傳統部署模型。
* Hello 傳統部署模型角色型存取控制 (RBAC) 支援。 您無法在 hello 傳統部署模型中執行 RBAC 控制項 tooa 循環。 Hello 訂閱任何系統管理員/coadministrator 可以連結或取消連結虛擬網路 toohello 循環。

## <a name="configuration"></a>組態
請依照下列所述的 hello 指示[離開 hello 傳統 toohello Resource Manager 部署模型的 ExpressRoute 電路](expressroute-howto-move-arm.md)。

## <a name="next-steps"></a>後續步驟
* [從 hello 傳統模型 toohello Azure Resource Manager 模型移轉 hello 虛擬網路連結的 toohello ExpressRoute 電路](expressroute-migration-classic-resource-manager.md)
* 如需工作流程資訊，請參閱 [ExpressRoute 線路佈建工作流程和線路狀態](expressroute-workflows.md)。
* tooconfigure ExpressRoute 連線：
  
  * [建立 ExpressRoute 線路](expressroute-howto-circuit-arm.md)
  * [設定路由](expressroute-howto-routing-arm.md)
  * [連結虛擬網路 tooan ExpressRoute 電路](expressroute-howto-linkvnet-arm.md)

