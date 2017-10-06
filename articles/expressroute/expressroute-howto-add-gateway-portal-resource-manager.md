---
title: "新增虛擬網路閘道 tooa VNet expressroute： 入口網站： Azure |Microsoft 文件"
description: "這篇文章會引導您完成新增虛擬網路閘道 tooan 已經建立 ExpressRoute 的資源管理員 VNet。"
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/17/2017
ms.author: cherylmc
ms.openlocfilehash: 9e922af1f3676eeebc569b57c3ae3a22d4e0b395
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-hello-azure-portal"></a>Expressroute 使用 hello Azure 入口網站設定虛擬網路閘道
> [!div class="op_single_selector"]
> * [Resource Manager - Azure 入口網站](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [Resource Manager - PowerShell](expressroute-howto-add-gateway-resource-manager.md)
> * [傳統 - PowerShell](expressroute-howto-add-gateway-classic.md)
> * [影片 - Azure 入口網站](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

本文將引導您完成 hello 步驟 tooadd 虛擬網路閘道已存在的 VNet。 本文將引導您完成 hello 步驟 tooadd、 調整大小，並移除虛擬網路 (VNet) 閘道預先存在的 vnet。 此組態的 hello 步驟是特別針對使用將用於 ExpressRoute 組態中的 hello Resource Manager 部署模型所建立的 Vnet。 如需有關 ExpressRoute 之虛擬網路閘道和閘道組態設定的詳細資訊，請參閱[關於 ExpressRoute 的虛擬網路閘道](expressroute-about-virtual-network-gateways.md)。 


## <a name="before-beginning"></a>開始之前

此工作會使用 VNet 的 hello 步驟 hello 下列組態的參考清單中的 hello 值為基礎。 我們會在範例步驟中使用此清單。 您可以複製 hello 清單 toouse，做為參考，取代您自己 hello 值。

**組態參考清單**

* 虛擬網路名稱 = "TestVNet"
* 虛擬網路位址空間 = 192.168.0.0/16
* 子網路名稱 = "FrontEnd" 
    * 子網路位址空間 = "192.168.1.0/24"
* 資源群組 = "TestRG"
* 位置 = "美國東部"
* 閘道器子網路名稱："GatewaySubnet"，您必須一律將閘道器子網路命名為 *GatewaySubnet*。
    * 閘道子網路位址空間 = "192.168.200.0/26"
* 閘道名稱 = "ERGW"
* 閘道 IP 名稱 = "MyERGWVIP"
* 閘道類型 = "ExpressRoute"，ExpressRoute 組態需要這個類型。
* 閘道公用 IP 名稱 = "MyERGWVIP"

您可以先檢視這些步驟的[影片](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)，再開始進行設定。

## <a name="create-hello-gateway-subnet"></a>建立 hello 閘道子網路

1. 在 hello[入口網站](http://portal.azure.com)，瀏覽您想要的虛擬網路閘道 toocreate toohello 資源管理員虛擬網路。
2. 在 hello**設定**> 一節的 VNet 刀鋒視窗中，按一下 **子網路**tooexpand hello 子網路 刀鋒視窗。
3. 在 hello**子網路**刀鋒視窗中，按一下  **+ 閘道子網路**tooopen hello**加入子網路**刀鋒視窗。 
   
    ![加入 hello 閘道子網路](./media/expressroute-howto-add-gateway-portal-resource-manager/addgwsubnet.png "加入 hello 閘道子網路")


4. hello**名稱**對於您的子網路會自動填入 hello 值 'GatewaySubnet'。 為了讓 Azure toorecognize hello 子網路時需要這個值為 hello 閘道子網路。 調整自動填滿的 hello**位址範圍**值 toomatch 組態需求。 建議您以 /27 或更大的值 (/26、/25 等) 建立閘道子網路。 然後，按一下 **確定**toosave hello 值，並建立 hello 閘道子網路。

    ![加入 hello 子網路](./media/expressroute-howto-add-gateway-portal-resource-manager/addsubnetgw.png "加入 hello 子網路")

## <a name="create-hello-virtual-network-gateway"></a>建立 hello 虛擬網路閘道

1. 在 hello 入口網站，在 hello 左邊，按一下   **+** 在搜尋中輸入虛擬網路閘道 '。 找出**虛擬網路閘道**hello 搜尋中傳回，並按一下 hello 項目。 在 hello**虛擬網路閘道**刀鋒視窗中，按一下 **建立**在 hello hello 刀鋒視窗的底部。 這會開啟 hello**建立虛擬網路閘道**刀鋒視窗。
2. 在 hello**建立虛擬網路閘道**刀鋒視窗中，您的虛擬網路閘道的 hello 值中的填滿。

    ![建立虛擬網路閘道刀鋒視窗欄位](./media/expressroute-howto-add-gateway-portal-resource-manager/gw.png "建立虛擬網路閘道刀鋒視窗欄位")
3. **名稱**：為您的閘道命名。 這不是 hello 與命名閘道子網路相同。 它的 hello 您所建立的 hello 閘道物件名稱。
4. **閘道類型**︰選取 [ExpressRoute]。
5. **SKU**： 從 hello 下拉式清單中選取 hello 閘道 SKU。
6. **位置**： 調整 hello**位置**欄位 toopoint toohello 位置虛擬網路所在的位置。 Hello 位置並未指向 toohello 區域虛擬網路所在的位置，如果 hello 虛擬網路不會出現在下拉式清單中 「 選擇虛擬網路' hello。
7. 選擇 hello 虛擬網路 toowhich 想 tooadd 此閘道。 按一下**虛擬網路**tooopen hello**選擇虛擬網路**刀鋒視窗。 選取 hello VNet。 如果您沒有看到您的 VNet，請確定 hello**位置**欄位指向您的虛擬網路所在的 toohello 區域。
9. 選擇公用 IP 位址。 按一下**公用 IP 位址**tooopen hello**選擇公用 IP 位址**刀鋒視窗。 按一下**+ 建立新**tooopen hello**建立公用 IP 位址 刀鋒視窗**。 輸入公用 IP 位址的名稱。 此刀鋒視窗中建立的公用 IP 位址動態指派公用 IP 位址物件 toowhich。 按一下**確定**toosave 您變更 toothis 刀鋒視窗。
10. **訂用帳戶**： 確認該 hello 正確選取訂用帳戶。
11. **資源群組**： 此設定由 hello 您選取的虛擬網路。
12. 不會調整 hello**位置**您所指定 hello 先前的設定之後。
13. 請確認 hello 設定。 如果您希望您的閘道 tooappear hello 儀表板上，您可以選取**Pin toodashboard**在 hello hello 刀鋒視窗的底部。
14. 按一下**建立**toobegin 建立 hello 閘道。 hello 設定會進行驗證，並將部署的 hello 閘道。 建立虛擬網路閘道可能佔用 too45 分鐘 toocomplete。

## <a name="next-steps"></a>後續步驟
建立 hello VNet 閘道之後，您可以連結您的 VNet tooan ExpressRoute 電路。 請參閱[連結 ExpressRoute 電路的虛擬網路 tooan](expressroute-howto-linkvnet-portal-resource-manager.md)。
