---
title: "虛擬網路 tooan ExpressRoute 電路的連結： Azure 入口網站 |Microsoft 文件"
description: "本文件提供如何 toolink 虛擬網路 (Vnet) tooExpressRoute 電路的概觀。"
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f5cb5441-2fba-46d9-99a5-d1d586e7bda4
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: cherylmc
ms.openlocfilehash: 8bedcb11df7e30281fd439afdfb76cc67626a8f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit"></a>連接虛擬網路 tooan ExpressRoute 電路
> [!div class="op_single_selector"]
> * [Azure 入口網站](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [Azure CLI](howto-linkvnet-cli.md)
> * [影片 - Azure 入口網站](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell (傳統)](expressroute-howto-linkvnet-classic.md)
> 

這篇文章可協助您將虛擬網路 (Vnet) tooAzure ExpressRoute 電路連結使用 hello Resource Manager 部署模型並 hello Azure 入口網站。 虛擬網路可以在 hello 相同的訂用帳戶，或它們可以是另一個訂用帳戶的一部分。

## <a name="before-you-begin"></a>開始之前
* 檢閱 hello[必要條件](expressroute-prerequisites.md)，[路由需求](expressroute-routing.md)，和[工作流程](expressroute-workflows.md)開始設定之前。
* 您必須擁有作用中的 ExpressRoute 線路。
  
  * 請依照下列指示 hello 太[建立 ExpressRoute 電路](expressroute-howto-circuit-portal-resource-manager.md)和已啟用連線提供者的 hello 循環。
  * 確定您已針對循環設定了 Azure 私用對等。 請參閱 hello[設定路由](expressroute-howto-routing-portal-resource-manager.md)路由指示的發行項。
  * 請確認 Azure 私用對等設定，且 hello BGP 對等互連網路與 Microsoft 之間，以便您可以啟用端對端連線已啟動。
  * 請確定您有已建立且完整佈建的虛擬網路和虛擬網路閘道。 請依照下列指示 hello 太[建立 expressroute 的虛擬網路閘道](expressroute-howto-add-gateway-resource-manager.md)。 Expressroute 的虛擬網路閘道使用 hello gatewaytype 的授權 'ExpressRoute'，不是 VPN。

* 您可以連結 too10 虛擬網路 tooa 標準 ExpressRoute 電路。 所有虛擬網路必須位於 hello 相同地理政治區域時使用標準的 ExpressRoute 電路。 
* 您可以連結以外的 hello ExpressRoute 電路的 hello 地緣政治區域虛擬網路或連線較大的虛擬網路 tooyour ExpressRoute 循環數目，如果啟用 hello ExpressRoute premium 附加元件。 檢查 hello[常見問題集](expressroute-faqs.md)如需有關 hello premium 附加元件。
* 您可以[觀賞視訊](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)開頭 toobetter 了解 hello 步驟之前。

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a>連接 hello 中的虛擬網路相同的訂用帳戶 tooa 電路

### <a name="toocreate-a-connection"></a>toocreate 連接

> [!NOTE]
> BGP 組態資訊不會顯示 hello 第 3 層提供者是否設定您的對等互連。 如果您的電路位於佈建狀態，您應該能夠 toocreate 連線。
>

1. 確認正確設定您的 ExpressRoute 電路和 Azure 私人對等互連。 請依照下列中的 hello 指示[建立 ExpressRoute 電路](expressroute-howto-circuit-arm.md)和[設定路由](expressroute-howto-routing-arm.md)。 ExpressRoute 電路應該看起來像下列映像的 hello:

    ![刪除 ExpressRoute 線路螢幕擷取畫面](./media/expressroute-howto-linkvnet-portal-resource-manager/routing1.png)
   
2. 您現在可以開始佈建連線 toolink 您虛擬網路閘道 tooyour ExpressRoute 電路。 按一下**連接** > **新增**tooopen hello**加入連接**刀鋒視窗中，然後設定 hello 值。

    ![新增連線螢幕擷取畫面](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub1.png)  

3. 已成功設定您的連線之後，連線物件會顯示 hello hello 連接資訊。

     ![連線物件螢幕擷取畫面](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub2.png)

### <a name="toodelete-a-connection"></a>toodelete 連接
您可以刪除的連線，藉由選取 hello**刪除**連線 hello 刀鋒視窗上的圖示。

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a>在不同的訂用帳戶 tooa 電路的虛擬網路連線
您可以讓多個訂用帳戶共用 ExpressRoute 線路。 hello 下圖顯示簡單圖解如何共用 ExpressRoute 電路的運作方式跨多個訂用帳戶。

![跨訂用帳戶的連線能力](./media/expressroute-howto-linkvnet-portal-resource-manager/cross-subscription.png)

- Hello hello 大型雲端內的小型雲端都屬於 toodifferent 部門組織內使用的 toorepresent 訂用帳戶。
- Hello 部門 hello 組織內的每個可以使用自己的訂用帳戶來部署其服務，但它們可以共用單一 ExpressRoute 電路 tooconnect 後 tooyour 在內部部署網路。
- 單一部門 (在此範例中： IT) 可以擁有 hello ExpressRoute 電路。 Hello 組織內其他訂用帳戶可以使用 hello ExpressRoute 電路。

    > [!NOTE]
    > Hello 專用循環的連線和頻寬費用將會套用的 toohello ExpressRoute 電路擁有者。 所有虛擬網路共用 hello 相同的頻寬。
    > 
    >

### <a name="administration---circuit-owners-and-circuit-users"></a>系統管理 - 線路擁有者和線路使用者

hello '電路擁有者' 是授權的 Power hello ExpressRoute 電路資源的使用者。 hello 電路擁有者可以建立可以兌換的 「 循環的使用者 」 的授權。 循環使用者是擁有者的虛擬網路閘道，不在 hello 相同訂用帳戶，因為 hello ExpressRoute 電路。 電路使用者可以兌換授權 (每個虛擬網路一個授權)。

hello 電路擁有者隨時都有 hello 電源 toomodify 和撤銷授權。 撤銷授權會導致從已撤銷其存取權的 hello 訂用帳戶中刪除所有連結連線。

### <a name="circuit-owner-operations"></a>循環擁有者作業

**toocreate 連線授權**

hello 電路擁有者建立的授權。 這會導致 hello 建立的授權金鑰可以使用循環使用者 tooconnect 其虛擬網路閘道 toohello ExpressRoute 電路。 一個授權僅適用於一個連線。

1. 在 hello ExpressRoute 刀鋒視窗中，按一下 **授權**，然後輸入**名稱**hello 授權，然後按一下**儲存**。

    ![授權](./media/expressroute-howto-linkvnet-portal-resource-manager/authorization.png)

2. Hello 組態儲存之後，複製 hello**資源識別碼**和 hello**授權金鑰**。

    ![授權金鑰](./media/expressroute-howto-linkvnet-portal-resource-manager/authkey.png)

**toodelete 連線授權**

您可以刪除的連線，藉由選取 hello**刪除**連線 hello 刀鋒視窗上的圖示。

### <a name="circuit-user-operations"></a>循環使用者作業

hello 電路使用者需要 hello 資源 ID，以及從 hello 電路擁有者授權金鑰。 

**tooredeem 連線授權**

1.  按一下 hello **+ 新增** 按鈕。

    ![Click New](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection1.png)

2.  搜尋**「 連線 」** hello Marketplace，在選取它，然後按一下**建立**。

    ![搜尋連線](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection2.png)

3.  請確定 hello**連線類型**設定得"ExpressRoute"。


4.  填入 hello 詳細資料，然後按一下 **確定**hello 基本概念刀鋒視窗中。

    ![基本概念刀鋒視窗](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection3.png)

5.  在 hello**設定**刀鋒視窗中，選取 hello**虛擬網路閘道**並檢查 hello**兌換授權**核取方塊。

6.  輸入 hello**授權金鑰**和 hello**對等電路 URI**並提供 hello 連接名稱。 按一下 [確定] 。

    ![設定刀鋒視窗](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection4.png)

7. 檢閱在 hello hello 資訊**摘要**刀鋒視窗，然後按一下**確定**。


**toorelease 連線授權**

您可以藉由刪除連結 hello ExpressRoute 電路 toohello 虛擬網路的 hello 連接釋放授權。

## <a name="next-steps"></a>後續步驟
如需 ExpressRoute 的詳細資訊，請參閱 hello [ExpressRoute 常見問題集](expressroute-faqs.md)。
