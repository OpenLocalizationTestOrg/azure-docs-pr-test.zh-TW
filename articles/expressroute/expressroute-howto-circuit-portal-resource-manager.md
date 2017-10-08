---
title: "建立與修改 ExpressRoute 線路：Azure 入口網站 | Microsoft Docs"
description: "本文說明如何 toocreate，佈建、 驗證、 更新、 刪除和取消佈建 ExpressRoute 電路。"
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 68d59d59-ed4d-482f-9cbc-534ebb090613
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/07/2017
ms.author: cherylmc;ganesr
ms.openlocfilehash: 200418aed6bdebace43a2f57cf532d1c8d13cb83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit"></a>建立和修改 ExpressRoute 線路
> [!div class="op_single_selector"]
> * [Azure 入口網站](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [Azure CLI](howto-circuit-cli.md)
> * [影片 - Azure 入口網站](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell (傳統)](expressroute-howto-circuit-classic.md)
>

本文說明如何使用 Azure ExpressRoute 電路 toocreate hello Azure 入口網站與 hello Azure Resource Manager 部署模型。 hello 下列步驟也會顯示 hello 電路 toocheck hello 狀態如何更新，或刪除，並取消佈建它。


## <a name="before-you-begin"></a>開始之前
* 檢閱 hello[必要條件](expressroute-prerequisites.md)和[工作流程](expressroute-workflows.md)開始設定之前。
* 請確定您有存取 toohello [Azure 入口網站](https://portal.azure.com)。
* 確定您有權限 toocreate 新網路功能資源。 如果您沒有 hello 正確的權限，請連絡您的帳戶管理員。
* 您可以[觀賞視訊](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)順序的開頭之前 toobetter 了解 hello 步驟。

## <a name="create-and-provision-an-expressroute-circuit"></a>建立和佈建 ExpressRoute 線路
### <a name="1-sign-in-toohello-azure-portal"></a>1.登入 toohello Azure 入口網站
從瀏覽器中，瀏覽 toohello [Azure 入口網站](http://portal.azure.com)並以您的 Azure 帳戶登入。

### <a name="2-create-a-new-expressroute-circuit"></a>2.建立新的 ExpressRoute 線路
> [!IMPORTANT]
> ExpressRoute 電路將計費 hello 發出服務金鑰的時間。 請確定您執行此作業，準備好 tooprovision hello 電路 hello 連線服務提供者時。
> 
> 

1. 您可以藉由選取 hello 選項 toocreate 建立 ExpressRoute 電路，新的資源。 按一下**新增** > **網路** > **ExpressRoute**hello 下列影像所示：
   
    ![建立 ExpressRoute 線路](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit1.png)
2. 按一下 之後**ExpressRoute**，您會看到 hello**建立 ExpressRoute 電路**刀鋒視窗。 當您要填入此刀鋒視窗上的 hello 值時，請確定您指定 hello 正確 SKU 層和資料計量。
   
   *  決定要啟用 ExpressRoute 標準或 ExpressRoute 進階附加元件。 您可以指定**標準**tooget hello 標準 SKU 或**Premium** hello premium 附加元件。
   * **資料計量**決定 hello 計費的型別。 您可以指定 [計量付費] 以採用計量付費數據傳輸方案，選取 [無限制] 以採用無限制的資料方案。 請注意，您可以變更從 hello 計費類型**Metered**太**Unlimited**，但您無法變更 hello 類型從**無限制**太**Metered**.
     
     ![設定 hello SKU 層和計量資料](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit2.png)

> [!IMPORTANT]
> 請留意對等互連位置該 hello 指出 hello[實體位置](expressroute-locations.md)您與 Microsoft 的互連位置。 這是**不**太連結 「 位置 」 屬性，是指 toohello hello Azure 網路資源提供者所在的地理位置。 雖然無關，它是很好的作法 toochoose 網路資源提供者關閉地理 toohello hello 循環的對等互連位置。 
> 
> 

### <a name="3-view-hello-circuits-and-properties"></a>3.檢視 hello 電路和屬性
**檢視所有 hello 電路**

您可以檢視所有您建立選取的 hello 電路**所有資源**hello 左側功能表上。

![檢視線路](./media/expressroute-howto-circuit-portal-resource-manager/listresource.png)

**檢視 hello 屬性**

    You can view hello properties of hello circuit by selecting it. On this blade, note hello service key for hello circuit. You must copy hello circuit key for your circuit and pass it down toohello service provider toocomplete hello provisioning process. hello circuit key is specific tooyour circuit.

![檢視屬性](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

### <a name="4-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a>4.佈建傳送嗨服務金鑰 tooyour 連線服務提供者
在這個刀鋒視窗中，**提供者狀態**提供 hello 的佈建 hello 服務提供者端的目前狀態的相關資訊。 **電路狀態**hello Microsoft 側邊提供 hello 狀態。 如需循環的佈建狀態的詳細資訊，請參閱 hello[工作流程](expressroute-workflows.md#expressroute-circuit-provisioning-states)發行項。

當您建立新的 ExpressRoute 電路時，hello 電路將處於下列狀態的 hello:

提供者狀態︰未佈建<BR>
線路狀態：已啟用

![起始佈建程序](./media/expressroute-howto-circuit-portal-resource-manager/viewstatus.png)

hello 循環會變更 toohello hello 連線服務提供者會在您啟用的 hello 程序中時，下列狀態：

提供者狀態︰正在佈建<BR>
線路狀態：已啟用

您 toobe 無法 toouse ExpressRoute 電路，它必須處於下列狀態的 hello:

提供者狀態︰已佈建<BR>
線路狀態：已啟用

### <a name="5-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a>5.定期檢查 hello 狀態和 hello 循環索引鍵 hello 狀態
您可以檢視由選取感興趣的 hello 循環的 hello 屬性。 檢查 hello**提供者狀態**，並確定它已移動過**已佈建**繼續進行之前。

![線路和提供者狀態](./media/expressroute-howto-circuit-portal-resource-manager/viewstatusprovisioned.png)

### <a name="6-create-your-routing-configuration"></a>6.建立路由組態
如需逐步指示，請參閱 toohello [ExpressRoute 電路的路由組態](expressroute-howto-routing-portal-resource-manager.md)文章 toocreate 和修改循環的對等互連。

> [!IMPORTANT]
> 這些說明僅適用於 toocircuits 與提供層級 2 連線服務的服務提供者所建立。 如果您使用的服務提供者是提供受管理的第 3 層服務 (通常是 IP VPN，如 MPLS)，您的連線提供者會為您設定和管理路由。
> 
> 

### <a name="7-link-a-virtual-network-tooan-expressroute-circuit"></a>7.連結虛擬網路 tooan ExpressRoute 電路
接下來，將虛擬網路 tooyour ExpressRoute 電路的連結。 使用 hello[連結虛擬網路 tooExpressRoute 電路](expressroute-howto-linkvnet-arm.md)處理 hello Resource Manager 部署模型時，發行項。

## <a name="getting-hello-status-of-an-expressroute-circuit"></a>取得 hello 狀態的 ExpressRoute 電路
您可以藉由選取檢視 hello 的循環的狀態。 

![ExpressRoute 線路的狀態](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

## <a name="modifying-an-expressroute-circuit"></a>修改 ExpressRoute 線路
您可以修改 ExpressRoute 線路的某些屬性，而不會影響連線。

您可以 hello 遵循不中斷的情況：

* 啟用或停用 ExpressRoute 線路的 ExpressRoute 進階附加元件。
* 增加 hello 頻寬的 ExpressRoute 電路提供 hello 連接埠的容量不足。 請注意，不支援降級 hello 電路頻寬。 
* 變更計量計劃的計量資料 tooUnlimited 資料 hello。 請注意該變更 hello 計量計劃從無限制的資料 tooMetered 不支援資料。
* 您可以啟用和停用 [允許傳統作業]。

如需有關限制和限制的詳細資訊，請參閱 toohello [ExpressRoute 常見問題集](expressroute-faqs.md)。

toomodify ExpressRoute 循環中，按一下 hello**組態**hello 圖所示。

![修改線路](./media/expressroute-howto-circuit-portal-resource-manager/modifycircuit.png)

您可以修改 hello 頻寬、 SKU，計費模型，並允許傳統 hello 組態刀鋒視窗中的作業。

> [!IMPORTANT]
> 如果 hello 現有的連接埠上有足夠的容量，您可能必須 toorecreate hello ExpressRoute 電路。 如果沒有任何額外的容量可在該位置，您無法升級 hello 循環。
>
> 您無法減少 hello 頻寬的 ExpressRoute 電路不會中斷。 降級頻寬 toodeprovision hello ExpressRoute 循環會要求您，並再重新佈建新增的 ExpressRoute 電路。
> 
> 停用 premium add-on 作業可能會失敗，如果您使用大於 hello 標準循環所允許的資源。
> 
> 

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a>取消佈建和刪除 ExpressRoute 線路
您可以藉由選取 hello 刪除 ExpressRoute 電路**刪除**圖示。 請注意 hello 下列：

* 您必須取消連結從 hello ExpressRoute 電路的所有虛擬網路。 如果此作業失敗，請檢查是否已連結的任何虛擬網路 toohello 循環。
* 如果 hello ExpressRoute 電路服務提供者佈建狀態為**佈建**或**已佈建**您必須使用您的服務提供者 toodeprovision hello 電路邊。 我們將繼續 tooreserve 資源，並向您收取費用，直到完成取消佈建 hello 電路 hello 服務提供者，並通知我們。
* 如果 hello 服務提供者已解除佈建 hello 循環 (hello 佈建狀態的服務提供者設定得**未佈建**) 可接著刪除 hello 循環。 這會停止計費 hello 循環

## <a name="next-steps"></a>後續步驟
建立您的循環之後，請確定您執行 hello 遵循：

* [建立和修改 ExpressRoute 線路的路由](expressroute-howto-routing-portal-resource-manager.md)
* [連結您的虛擬網路 tooyour ExpressRoute 電路](expressroute-howto-linkvnet-arm.md)

