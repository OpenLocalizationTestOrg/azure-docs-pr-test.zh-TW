---
title: "將虛擬網路連結到 ExpressRoute 電路：Azure 入口網站 | Microsoft Docs"
description: "本文件提供如何將虛擬網路 (Vnet) 連結到 ExpressRoute 循環的概觀。"
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
ms.openlocfilehash: 34caed9323ae3067d1dc17ab9c62ebf7a9be855b
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="connect-a-virtual-network-to-an-expressroute-circuit"></a>將虛擬網路連線到 ExpressRoute 電路
> [!div class="op_single_selector"]
> * [Azure 入口網站](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [Azure CLI](howto-linkvnet-cli.md)
> * [影片 - Azure 入口網站](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell (傳統)](expressroute-howto-linkvnet-classic.md)
> 

本文會協助您使用 Resource Manager 部署模型和 Azure 入口網站將虛擬網路 (VNet) 連結到 Azure ExpressRoute 線路。 虛擬網路可以位於相同的訂用帳戶中，或屬於另一個訂用帳戶。

## <a name="before-you-begin"></a>開始之前
* 開始設定之前，請先檢閱[必要條件](expressroute-prerequisites.md)、[路由需求](expressroute-routing.md)及[工作流程](expressroute-workflows.md)。
* 您必須擁有作用中的 ExpressRoute 線路。
  
  * 遵循指示來 [建立 ExpressRoute 線路](expressroute-howto-circuit-portal-resource-manager.md) ，並由您的連線提供者來啟用該線路。
  * 確定您已針對循環設定了 Azure 私用對等。 請參閱 [設定路由](expressroute-howto-routing-portal-resource-manager.md) 一文，以取得路由指示。
  * 請確定已設定 Azure 私用對等，且已開啟您的網路與 Microsoft 之間的 BGP 對等，讓您可以啟用端對端連線。
  * 請確定您有已建立且完整佈建的虛擬網路和虛擬網路閘道。 請依照指示[為 ExpressRoute 建立虛擬網路閘道](expressroute-howto-add-gateway-resource-manager.md)。 ExpressRoute 的虛擬網路閘道會使用 GatewayType 'ExpressRoute'，而不是 VPN。

* 您最多可以將 10 個虛擬網路連結至標準 ExpressRoute 電路。 在使用標準 ExpressRoute 電路時，所有虛擬網路都必須位於相同的地理政治區域內。 
* 如果您已啟用 ExpressRoute 高階附加元件，則可連結 ExpressRoute 電路的地理政治區域以外的虛擬網路，或是將大量的虛擬網路連線到 ExpressRoute 電路。 如需高階附加元件的詳細資訊，請參閱 [常見問題集](expressroute-faqs.md) 。
* 您可以在開始前先[觀看影片](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)來進一步了解步驟。

## <a name="connect-a-virtual-network-in-the-same-subscription-to-a-circuit"></a>將相同訂用帳戶中的虛擬網路連接到線路

### <a name="to-create-a-connection"></a>建立連線

> [!NOTE]
> 如果您的對等互連是由第 3 層提供者設定，就不會顯示 BGP 組態資訊。 如果線路處於佈建狀態，您應該能夠建立連線。
>

1. 確認正確設定您的 ExpressRoute 電路和 Azure 私人對等互連。 請遵循[建立 ExpressRoute 線路](expressroute-howto-circuit-arm.md)和[設定路由](expressroute-howto-routing-arm.md)中的指示。 ExpressRoute 線路看起來應該像下圖：

    ![刪除 ExpressRoute 線路螢幕擷取畫面](./media/expressroute-howto-linkvnet-portal-resource-manager/routing1.png)
   
2. 您現在可以開始佈建將虛擬網路閘道連結至 ExpressRoute 線路的連線。 按一下 [連接] > [新增] 開啟 [新增連線] 刀鋒視窗，然後設定各值。

    ![新增連線螢幕擷取畫面](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub1.png)  

3. 順利設定連線後，您的連線物件就會顯示連接資訊。

     ![連線物件螢幕擷取畫面](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub2.png)

### <a name="to-delete-a-connection"></a>刪除連接
您可以選取連接刀鋒視窗上的 **刪除** 圖示來刪除連接。

## <a name="connect-a-virtual-network-in-a-different-subscription-to-a-circuit"></a>將不同訂用帳戶中的虛擬網路連接到線路
您可以讓多個訂用帳戶共用 ExpressRoute 線路。 下圖顯示簡單的圖解，示範多個訂用帳戶共用 ExpressRoute 線路的方式。

![跨訂用帳戶的連線能力](./media/expressroute-howto-linkvnet-portal-resource-manager/cross-subscription.png)

- 大型雲端內的每個較小型雲端，會用來代表屬於組織內不同部門的訂用帳戶。
- 組織內的每個部門都可以使用自己的訂用帳戶來部署它們的服務，但可共用單一 ExpressRoute 線路，以連線回內部部署網路。
- 單一部門 (在此範例中：IT) 可以擁有 ExpressRoute 循環。 組織內的其他訂用帳戶可以使用 ExpressRoute 線路以及與線路相關聯的授權，包括連結到其他 Azure Active Directory 租用戶的訂用帳戶和 Enterprise 合約的註冊項目。 

    > [!NOTE]
    > ExpressRoute 循環擁有者需支付專用循環的連線和頻寬費用。 所有虛擬網路都會共用相同的頻寬。
    > 
    >

### <a name="administration---circuit-owners-and-circuit-users"></a>系統管理 - 線路擁有者和線路使用者

「線路擁有者」是 ExpressRoute 線路資源的已授權「進階使用者」。 電路擁有者能夠建立可由「電路使用者」兌換的授權。 線路使用者是虛擬網路閘道的擁有者，與 ExpressRoute 線路位於不同的訂用帳戶內。 電路使用者可以兌換授權 (每個虛擬網路一個授權)。

電路擁有者能夠隨時修改及撤銷授權。 如果撤銷授權，則在存取權遭撤銷的訂用帳戶中，所有連結連線均會被刪除。

### <a name="circuit-owner-operations"></a>循環擁有者作業

**建立連線授權**

電路擁有者會建立授權。 這樣即會建立授權金鑰，讓電路使用者可用來將其虛擬網路閘道連接到 ExpressRoute 電路。 一個授權僅適用於一個連線。

1. 在 [ExpressRoute] 刀鋒視窗中，按一下 [授權]，然後輸入授權的**名稱**並按一下 [儲存]。

    ![授權](./media/expressroute-howto-linkvnet-portal-resource-manager/authorization.png)

2. 儲存組態之後，複製**資源識別碼**和**授權金鑰**。

    ![授權金鑰](./media/expressroute-howto-linkvnet-portal-resource-manager/authkey.png)

**刪除連線授權**

您可以選取連接刀鋒視窗上的 **刪除** 圖示來刪除連接。

### <a name="circuit-user-operations"></a>循環使用者作業

線路使用者需要具備資源識別碼，以及線路擁有者所提供的授權金鑰。 

**兌換連線授權**

1.  按一下 [+新增] 按鈕。

    ![Click New](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection1.png)

2.  在 Marketplace 中搜尋**連線**、選取它，然後按一下 [建立]。

    ![搜尋連線](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection2.png)

3.  確定 [連線類型] 設定為 [ExpressRoute]。


4.  填入詳細資料，然後在 [基本] 刀鋒視窗中按一下 [確定]。

    ![基本概念刀鋒視窗](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection3.png)

5.  在 [設定] 刀鋒視窗中選取 [虛擬網路閘道]，並選取 [兌換授權] 核取方塊。

6.  輸入**授權金鑰**和**對等線路 URI**，並提供連線名稱。 按一下 [SERVICEPRINCIPAL] 。

    ![設定刀鋒視窗](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection4.png)

7. 在 [摘要] 刀鋒視窗中檢閱資訊，然後按一下 [確定]。


**釋出連線授權**

您可以藉由刪除將 ExpressRoute 線路連結到虛擬網路的連線來釋出授權。

## <a name="next-steps"></a>後續步驟
如需有關 ExpressRoute 的詳細資訊，請參閱 [ExpressRoute 常見問題集](expressroute-faqs.md)。
