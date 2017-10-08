---
title: "aaaCreate 網際網路對向負載平衡器-Azure 入口網站 |Microsoft 文件"
description: "了解如何使用資源管理員 toocreate 網際網路對向負載平衡器 hello Azure 入口網站"
services: load-balancer
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: aa9d26ca-3d8a-4a99-83b7-c410dd20b9d0
ms.service: load-balancer
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: annahar
ms.openlocfilehash: 390ba8ec1474c54cf2c0022c4a3c219d21b1a659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-facing-load-balancer-using-hello-azure-portal"></a>建立使用 hello Azure 入口網站的網際網路對向負載平衡器

> [!div class="op_single_selector"]
> * [入口網站](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [範本](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

本文涵蓋 hello Resource Manager 部署模型。 您也可以[學習 toocreate 網際網路對向負載平衡器使用傳統部署的方式](load-balancer-get-started-internet-classic-portal.md)

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

這涵蓋 hello 一連串個別的工作已完成的 toobe toocreate 負載平衡器，並詳細說明什麼正在進行 tooaccomplish hello 目標。

## <a name="what-is-required-toocreate-an-internet-facing-load-balancer"></a>什麼是必要的 toocreate 網際網路對向負載平衡器？

您需要 toocreate 並設定下列物件 toodeploy 負載平衡器的 hello。

* 前端 IP 組態 - 包含傳入網路流量的公用 IP 位址。
* 後端位址集區-包含 hello 虛擬機器 tooreceive 從 hello 負載平衡器的網路流量的網路介面 (Nic)。
* 負載平衡規則-包含對應 hello 負載平衡器 tooport hello 後端位址集區中的公用連接埠的規則。
* 輸入 NAT 規則-包含 hello 負載平衡器 tooa 通訊埠上的特定虛擬機器 hello 後端位址集區中的公用通訊埠對應規則。
* 探查-包含 hello 後端位址集區中的虛擬機器執行個體的健全狀況探查使用 toocheck 可用性。

您可以在 [Azure Resource Manager 的負載平衡器支援](load-balancer-arm.md)中取得關於負載平衡器元件與 Azure Resource Manager 的詳細資訊。

## <a name="set-up-a-load-balancer-in-azure-portal"></a>在 Azure 入口網站設定負載平衡器

> [!IMPORTANT]
> 此範例假設您擁有稱為 **myVNet**的虛擬網路。 請參閱太[建立虛擬網路](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)toodo 這。 它也會假設沒有子網路內**myVNet**呼叫**LB 子網路是**和呼叫的兩個 Vm **web1**和**web2**分別內hello 相同可用性設定組，稱為**myAvailSet**中**myVNet**。 請參閱太[此連結](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)toocreate Vm。

1. 從瀏覽器瀏覽 toohello Azure 入口網站： [http://portal.azure.com](http://portal.azure.com)並使用您的 Azure 帳戶登入。
2. 在 hello 左邊囉 」 畫面上選取**新增** > **網路** > **負載平衡器。**
3. 在 hello**建立負載平衡器**刀鋒視窗中，輸入您的負載平衡器的名稱。 在此我們將其稱為 **myLoadBalancer**。
4. 在 [類型] 底下選取 [公用]。
5. 在 [公用 IP 位址] 底下建立稱為 **myPublicIP** 的新公用 IP。
6. 在 [資源群組] 底下選取 [myRG] 。 選取適當 位置，然後按一下確定。 hello 負載平衡器會啟動 toodeploy 和 toosuccessfully 完整部署時將會需要幾分鐘。

    ![更新負載平衡器的資源群組](./media/load-balancer-get-started-internet-portal/1-load-balancer.png)

## <a name="create-a-back-end-address-pool"></a>建立後端位址集區

1. 順利部署負載平衡器之後，請從資源內加以選取。 在 [設定] 底下選取 [後端集區]。 輸入後端集區的名稱。 然後按一下 hello**新增**朝 hello 顯示 hello 刀鋒視窗頂端的按鈕。
2. 按一下**新增虛擬機器**在 hello**新增後端集區**刀鋒視窗。  選取 [可用性設定組] 底下的 [選擇可用性設定組]，然後選取 [myAvailSet]。 接下來，選取**選擇 hello 虛擬機器**底下 hello hello 刀鋒視窗中的 虛擬機器 區段，然後按一下  **web1**和**web2**，hello 兩個 Vm 建立負載平衡。 請確定兩者都有藍色的核取記號 toohello 左 hello 圖所示。 然後按一下 **選取**hello 中後面接著確定該刀鋒視窗中**選擇虛擬機器**刀鋒視窗，然後**確定**hello 中**新增後端集區**刀鋒視窗。

    ![加入 toohello 後端位址集區- ](./media/load-balancer-get-started-internet-portal/3-load-balancer-backend-02.png)

3. 檢查 toomake 確定您的通知下拉式清單中已有更新的同時 hello Vm 有關儲存 hello 負載平衡器後端集區中增加 tooupdating hello 網路介面**web1**和**web2**。

## <a name="create-a-probe-lb-rule-and-nat-rules"></a>建立探查、LB 規則和 NAT 規則

1. 建立健全狀況探查。

    在負載平衡器的 [設定] 底下選取 [探查]。 然後按一下 **新增**位於 hello hello 刀鋒視窗的頂端。

    有兩種方式 tooconfigure 探查： HTTP 或 TCP。 此範例示範 HTTP，但您可以透過類似方式設定 TCP。
    更新 hello 所需的資訊。 如前所述， **myLoadBalancer** 會對連接埠 80 上的流量進行負載平衡。 選取的 hello 路徑為 HealthProbe.aspx、 間隔是 15 秒，而狀況不良閾值為 2。 完成之後，按一下**確定**toocreate hello 探查。

    將指標停留 hello 'i' 圖示 toolearn 深入了解這些個別的設定，並且可變更的 toocater tooyour 需求的方式。

    ![新增探查](./media/load-balancer-get-started-internet-portal/4-load-balancer-probes.png)

2. 建立負載平衡器規則。

    負載平衡中 hello 規則上按一下您負載平衡器的 [設定] 區段。 在 hello 新刀鋒視窗中，按一下**新增**。 為規則命名。 在這裡，其名稱為 HTTP。 選擇 hello 的前端連接埠與後端連接埠。 在這裡，兩者皆選擇 80。 選擇**LB 後端**做為後端集區，並且先前建立的 hello **HealthProbe**為 hello 探查。 您可以根據 tooyour 需求設定其他組態。 然後按一下 [確定] toosave hello 負載平衡規則。

    ![新增負載平衡規則](./media/load-balancer-get-started-internet-portal/5-load-balancing-rules.png)

3. 建立輸入 NAT 規則

    按一下您負載平衡器的 hello [設定] 區段下方的輸入 NAT 規則。 在 hello 新刀鋒視窗中，按一下 **新增**。 然後為輸入 NAT 規則命名。 在此我們將其稱為 **inboundNATrule1**。 hello 目的地應該的 hello 先前建立的公用 IP。 選取服務下的 自訂，然後選取您想要 toouse hello 通訊協定。 此處選取 TCP。 輸入 hello 連接埠，3441，和 hello 目標連接埠，在此情況下，3389。 然後按一下 [確定] toosave 此規則。

    Hello 第一個規則建立之後，請針對 hello 第二個輸入 NAT 規則通訊埠 3442 tooTarget 連接埠 3389 從呼叫 inboundNATrule2 重複此步驟。

    ![新增輸入 NAT 規則](./media/load-balancer-get-started-internet-portal/6-load-balancer-inbound-nat-rules.png)

## <a name="remove-a-load-balancer"></a>移除負載平衡器

toodelete 負載平衡器，您想要 tooremove 選取 hello 負載平衡器。 在 hello*負載平衡器*刀鋒視窗中，按一下 **刪除**位於 hello hello 刀鋒視窗的頂端。 然後在提示時選取 [是]  。

## <a name="next-steps"></a>後續步驟

[開始設定內部負載平衡器](load-balancer-get-started-ilb-arm-cli.md)

[設定負載平衡器分配模式](load-balancer-distribution-mode.md)

[設定負載平衡器的閒置 TCP 逾時設定](load-balancer-tcp-idle-timeout.md)
