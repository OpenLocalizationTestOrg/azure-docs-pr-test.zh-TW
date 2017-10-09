---
title: "新增多個 VPN 閘道站對站連線 tooa VNet: Azure 入口網站： 資源管理員 |Microsoft 文件"
description: "新增多站台 S2S 連線 tooa VPN 閘道具有現有連線"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f3e8b165-f20a-42ab-afbb-bf60974bb4b1
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: cherylmc
ms.openlocfilehash: b8c9ff454967f509dcef725f8bcec8564fad9b00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection"></a>新增站對站連線 tooa VNet 與現有的 VPN 閘道連線

> [!div class="op_single_selector"]
> * [Azure 入口網站](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [PowerShell (傳統)](vpn-gateway-multi-site.md)
>
> 

這篇文章會引導您使用 hello Azure 入口網站 tooadd 站台對站 (S2S) 連線 tooa VPN 閘道具有現有連線。 這種類型通常是連接的參照的 tooas"多站台 」 設定。 您可以加入 S2S 連線 tooa VNet 已 S2S 連線、 點對站連線或 VNet 對 VNet 連線。 新增連線有一些限制。 檢查 hello[開始之前](#before)此發行項 tooverify 之前啟動您的組態 > 一節。 

本文適用於使用 hello Resource Manager 部署模型所建立的 tooVNets 具有 RouteBased VPN 閘道。 這些步驟不會套用 tooExpressRoute /-網站共存連接組態。 如需有關並存連線的資訊，請參閱 [ExpressRoute/S2S 並存連線](../expressroute/expressroute-howto-coexist-resource-manager.md)。

### <a name="deployment-models-and-methods"></a>部署模型和方法
[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

當此組態有新文章和額外工具可以使用時，我們就會更新此資料表。 發行項可用時，我們直接連結 tooit 這個資料表中。

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="before"></a>開始之前
請確認下列項目 hello:

* 您尚未建立 ExpressRoute/S2S 並存連線。
* 您已使用具有現有連線的 hello Resource Manager 部署模型所建立的虛擬網路。
* 您的 VNet 的 hello 虛擬網路閘道是 RouteBased。 如果您有 PolicyBased VPN 閘道，則必須刪除 hello 虛擬網路閘道，並建立新的 VPN 閘道為 RouteBased。
* 沒有任何 hello 位址範圍重疊任何 hello 連接到此 VNet 的 Vnet。
* 您擁有相容的 VPN 裝置和人能夠 tooconfigure 它。 請參閱 [關於 VPN 裝置](vpn-gateway-about-vpn-devices.md)。 如果您不熟悉設定 VPN 裝置，或不熟悉 hello IP 位址範圍位於您的內部部署網路組態，您需要 toocoordinate 的人可以為您提供這些詳細資料。
* 您的 VPN 裝置有對外開放的公用 IP 位址。 此 IP 位址不能位於 NAT 後方。

## <a name="part1"></a>第 1 部分 - 設定連線
1. 從瀏覽器中，瀏覽 toohello [Azure 入口網站](http://portal.azure.com)且如有需要，使用您的 Azure 帳戶登入。
2. 按一下**所有資源**並找出您**虛擬網路閘道**hello 清單中的資源，然後按一下它。
3. 在 hello**虛擬網路閘道**刀鋒視窗中，按一下 **連線**。
   
    ![連接刀鋒視窗](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "連接刀鋒視窗e")<br>
4. 在 hello**連線**刀鋒視窗中，按一下  **+ 加**。
   
    ![新增連接按鈕](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "新增連接按鈕")<br>
5. 在 hello**加入連接**刀鋒視窗中，填寫下列欄位的 hello:
   
   * **名稱：** hello 想 toogive toohello 站台，您要建立 hello 連接的名稱。
   * **連線類型：**選取 [站對站 (IPSec)]。
     
     ![新增連接 刀鋒視窗](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "新增連接 刀鋒視窗")<br>

## <a name="part2"></a>第 2 部分 - 新增區域網路閘道
1. 按一下 [區域網路閘道] > [選擇區域網路閘道]。 這會開啟 hello**選擇區域網路閘道**刀鋒視窗。
   
    ![選擇區域網路閘道](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "選擇區域網路閘道")<br>
2. 按一下**建立新**tooopen hello**建立區域網路閘道**刀鋒視窗。
   
    ![建立區域網路閘道刀鋒視窗](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "建立區域網路閘道")<br>
3. 在 hello**建立區域網路閘道**刀鋒視窗中，填寫下列欄位的 hello:
   
   * **名稱：** hello 想 toogive toohello 區域網路閘道資源的名稱。
   * **IP 位址：** hello hello VPN 裝置，您想要 tooconnect hello 站台上的公用 IP 位址。
   * **位址空間：** hello 位址空間的 toobe 路由 toohello 新區域網路網站。
4. 按一下**確定**上 hello**建立區域網路閘道**刀鋒視窗 toosave hello 變更。

## <a name="part3"></a>第 3 部分-新增 hello 共用的金鑰，並建立 hello 連線
1. 在 hello**加入連接**刀鋒視窗中，新增您想 toouse toocreate 連線 hello 共用的金鑰。 您可以從您的 VPN 裝置取得 hello 共用的金鑰或組成這裡並再設定您的 VPN 裝置 toouse hello 相同的共用金鑰。 重要的是 hello 索引鍵是完全 hello hello 相同。
   
    ![共用金鑰](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "共用金鑰")<br>
2. 在 hello hello 刀鋒視窗底部，按一下 **確定**toocreate hello 連線。

## <a name="part4"></a>第 4 部分-請確認 hello VPN 連線


[!INCLUDE [vpn-gateway-verify-connection-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="next-steps"></a>後續步驟

一旦完成您的連線，您可以將虛擬機器 tooyour 虛擬網路。 請參閱 hello 虛擬機器[學習路徑](https://azure.microsoft.com/documentation/learning-paths/virtual-machines)如需詳細資訊。
