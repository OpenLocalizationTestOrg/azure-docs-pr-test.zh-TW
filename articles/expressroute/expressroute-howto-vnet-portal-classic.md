---
title: "aaaConfigure 虛擬網路和閘道中 expressroute hello 傳統入口網站 |Microsoft 文件"
description: "這篇文章會引導您透過 expressroute 使用 hello 傳統部署模型和 hello 傳統入口網站設定虛擬網路。"
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: 688817d9-51c8-4372-9af8-33fa098c7c5a
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/20/2016
ms.author: cherylmc
ms.openlocfilehash: dd1f6c5e85dbb3ad0a53ecd81c13b4d3f5c06e66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-for-expressroute-in-hello-classic-portal"></a>Hello 傳統入口網站中建立 expressroute 的虛擬網路
這篇文章中的 hello 步驟將引導您完成使用 ExpressRoute 使用 hello 傳統部署模型和 hello 傳統入口網站設定虛擬網路和虛擬網路閘道，供使用。

如果您要尋找 hello Resource Manager 部署模型的指示，您可以使用下列文章 hello:[使用 PowerShell 建立虛擬網路](../virtual-network/virtual-networks-create-vnet-arm-ps.md)和[新增 VPN 閘道 tooa 資源管理員 VNet 的ExpressRoute](expressroute-howto-add-gateway-resource-manager.md)。

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**關於 Azure 部署模型**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="create-a-classic-vnet-and-gateway"></a>建立傳統 VNet 閘道
hello 下列步驟建立傳統的 VNet 和虛擬網路閘道。 如果您已經有傳統的 VNet，請參閱 hello[設定現有的傳統 VNet](#config) 〉 一節。

1. 登入 toohello [Azure 傳統入口網站](http://manage.windowsazure.com)。
2. 在 hello 左下角的囉 」 畫面，按一下 **新增**。 在 hello 瀏覽窗格中，按一下 **網路服務**，然後按一下**虛擬網路**。 按一下**自訂建立**toobegin hello 組態精靈。
3. 在 hello**虛擬網路詳細資料**頁面上，輸入 hello 下列：
   
   * **名稱** ：為虛擬網路命名。 當您部署您的 Vm 和 PaaS 執行個體，因此您可能不想 toomake hello 名稱太複雜時，您將使用此虛擬網路名稱。
   * **位置**– hello 位置是直接相關的 toohello 實體位置 （地區） 您希望資源 (Vm) tooreside。 例如，如果您想部署 toothis 虛擬網路 toobe 實際上位於美國東部的 hello Vm，請選取該位置。 您無法變更您在建立之後，您的虛擬網路與相關聯的 hello 區域。
4. 在 hello **DNS 伺服器和 VPN 連線能力**頁面上，輸入下列資訊，hello，然後按一下hello hello 右下方的下一步箭頭。 
   
   * **DNS 伺服器**-輸入 hello DNS 伺服器名稱和 IP 位址，或從 hello 快顯功能表中選取一個先前註冊的 DNS 伺服器。 此設定不會建立 DNS 伺服器。 它可讓您為此虛擬網路的名稱解析需 toouse toospecify hello DNS 伺服器。
   * **站台對站連線能力**-選取核取方塊的 hello**設定站對站 VPN**。
   * **ExpressRoute** -選取核取方塊的 hello**使用 ExpressRoute**。 唯有在選取 [設定站對站 VPN] 時才會出現此選項。
   * **本機網路**-會需要的 toohave ExpressRoute 的區域網路網站。 不過，萬一 hello 的 ExpressRoute 連線，hello 位址首碼指定 hello 本機網路站台將會被忽略。 相反地，hello 位址首碼通告透過 ExpressRoute 電路 hello tooMicrosoft 將用於路由之用。<BR>如果您已經建立 ExpressRoute 連線區域網路，您可以從 hello 下拉式清單中選取它。 如果未建立，請選取 [指定新的區域網路]。
5. hello**站台對站連線能力**頁面隨即出現，如果您選取新的區域網路 toospecify hello 上一個步驟中。 tooconfigure 區域網路，輸入下列資訊的 hello，然後按一下hello 下一步箭頭。 
   
   * **名稱**-您想要 toocall 本機的 hello 名稱 （在內部部署） 網路站台。
   * **位址空間** ：包括起始 IP 和 CIDR (位址計數)。 您可以指定的任何位址範圍，只要它不會與 hello 虛擬網路的位址範圍重疊。 一般而言，這會指定您的內部部署網路的 hello 位址範圍，但不是使用 ExpressRoute hello 案例，這些設定。 不過，需要此設定，順序 toocreate hello 本機網路中使用 hello 傳統入口網站時。
   * **加入位址空間** ：此設定與 ExpressRoute 無關。
6. 在 hello**虛擬網路位址空間**頁面上，輸入下列資訊的 hello，然後按一下 hello 核取記號 hello 較低的右 tooconfigure 上您的網路。 
   
   * **位址空間** ：包括起始 IP 和位址計數。 確認您指定的 hello 位址空間不將任何 hello 您對您的區域網路的位址空間重疊。
   * **新增子網路** - 包括起始 IP 和位址計數。 不需要其他子網路。
   * **加入閘道子網路**-按一下 tooadd hello 閘道子網路。 hello 閘道子網路只能用於 hello 虛擬網路閘道，而且需要這項設定。<BR>ExpressRoute 必須是/28 hello 閘道子網路 CIDR （位址計數） 或更大 (27 日 / / 26 等。)。 這可允許足夠的 IP 位址的子網路 tooallow hello 組態 toowork 中。 Hello 傳統入口網站中，如果您已選取 hello 核取方塊 toouse ExpressRoute，hello 入口網站指定的閘道子網路/28。  您無法調整 hello 傳統入口網站中的 hello CIDR 位址計數。 hello 閘道子網路將會顯示為**閘道**hello 傳統入口網站中，雖然 hello 建立 hello 閘道子網路的實際名稱實際上是**GatewaySubnet**。 使用 PowerShell 或 hello Azure 入口網站中，您可以檢視此名稱。
7. 按一下 hello hello hello 頁面底部的核取記號，且您的虛擬網路會開始 toocreate。 在完成時，您會看到**Created**底下所列**狀態**上 hello**網路**hello 傳統入口網站中的頁面。

## <a name="gw"></a>建立 hello 閘道
1. 在 hello**網路**頁面上，按一下您剛 hello 虛擬網路建立，然後按一下 **儀表板**hello 頁面頂端的 hello。
2. 在 hello 底部 hello**儀表板**頁面上，按一下**建立閘道**選取**動態路由**。 按一下**是**tooconfirm 想 toocreate 閘道。
3. 當開始建立 hello 閘道時，您會看到訊息，告訴您該 hello 閘道已啟動。 它可能會佔用 too45 hello 閘道 toocreate 分鐘的時間。
4. 連結您的網路 tooa 循環。 遵循 hello 文章中的 hello 指示[如何 toolink Vnet tooExpressRoute 電路](expressroute-howto-linkvnet-classic.md)。

## <a name="config"></a>設定 ExpressRoute 的現有傳統 VNet
如果您已經有傳統的 VNet，您可以設定它 tooconnect tooExpressRoute hello 傳統入口網站中。 hello 設定是讓相同 hello 為上述的 hello 區段，以便透過這些熟悉 hello 的區段 toobecome 讀取所需的設定。 如果您想 toocreate ExpressRoute /-網站共存連線，請參閱[本文](expressroute-howto-coexist-classic.md)hello 的步驟。 它們是不同於 hello 本文章中的步驟。

1. 在更新的 VNet 設定的 hello 其餘部分之前，您會需要 toocreate hello 區域網路。 新的區域網路，都需要設定 ExpressRoute 透過 hello 傳統入口網站時，按一下 toocreate**新增**  **>**  **網路服務** **>**  **虛擬網路**  **>**  **新增區域網路**。 請遵循 hello 精靈步驟 toocreate hello 本機網路。
2. 使用**設定**頁面 tooupdate hello 的其餘 hello 設定您的 VNet 和 tooassociate hello VNet toohello 區域網路。
3. 在之後設定 hello 設定時，請繼續 toohello[建立 hello 閘道](#gw)此發行項 toocreate hello 閘道的區段。

## <a name="next-steps"></a>後續步驟
* 如果您想 tooadd 虛擬機器 tooyour 虛擬網路，請參閱[學習路徑的虛擬機器](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/)。
* 如果您想深入了解 ExpressRoute toolearn，請參閱 hello [ExpressRoute 概觀](expressroute-introduction.md)。

