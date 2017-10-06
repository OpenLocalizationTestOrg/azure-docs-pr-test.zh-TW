---
title: "在 Azure 中的多個 IP 組態上的平衡 aaaLoad |Microsoft 文件"
description: "在主要和次要 IP 組態間進行負載平衡。"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: na
ms.assetid: 244907cd-b275-4494-aaf7-dcfc4d93edfe
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2017
ms.author: kumud
ms.openlocfilehash: 8619493b8102e9d158d428fe6c59ecf3f32edc32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-balancing-on-multiple-ip-configurations-using-hello-azure-portal"></a>多個 IP 組態使用 hello Azure 入口網站上的負載平衡

> [!div class="op_single_selector"]
> * [入口網站](load-balancer-multiple-ip.md)
> * [PowerShell](load-balancer-multiple-ip-powershell.md)
> * [CLI](load-balancer-multiple-ip-cli.md)

本文說明如何 toouse Azure 負載平衡器與多個 IP 位址上的次要網路介面 (NIC)。此案例中，我們有兩個 Vm 執行 Windows，每個都有主要和次要的 nic。 每個次要 hello Nic 有兩個 IP 組態。 每部 VM 都裝載 contoso.com 和 fabrikam.com 兩個網站。每個網站會繫結的 tooone 的 hello hello 次要 NIC 上的 IP 組態 我們使用 Azure 負載平衡器 tooexpose 兩個前端 IP 位址，一個用於每個網站，toodistribute 流量 toohello 個別的 IP 組態 hello 網站。 這種情況下使用 hello 跨前端，以及兩個後端集區 IP 位址相同的連接埠號碼。

![LB 案例影像](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

##<a name="prerequisites"></a>必要條件
這個範例假設您有資源群組名稱*contosofabrikam*以 hello 下列組態：
 -  包含虛擬網路，名為*myVNet*，呼叫的兩個 Vm *VM1*和*VM2*分別內 hello 相同可用性設定組具名*myAvailset*. 
 - 每個 VM 各有主要 NIC 和次要 NIC。 hello 主要名為 Nic *VM1NIC1*和*VM2NIC1*和 hello 次要命名 Nic *VM1NIC2*和*VM2NIC2*。 如需如何建立具有多個 NIC 之 VM 的詳細資訊，請參閱[使用 PowerShell 建立具有多個 NIC 的 VM](../virtual-network/virtual-network-deploy-multinic-arm-ps.md)。

## <a name="steps-tooload-balance-on-multiple-ip-configurations"></a>多個 IP 組態步驟 tooload 餘額

遵循下列步驟下, 面這篇文章所述的 tooachieve hello 案例：

### <a name="step-1-configure-hello-secondary-nics-for-each-vm"></a>步驟 1： 設定每個 VM hello 次要 Nic

在虛擬網路中，每個 VM，請加入設定的 IP 組態 hello 次要 NIC，如下所示：  

1. 從瀏覽器瀏覽 toohello Azure 入口網站： http://portal.azure.com 並使用您的 Azure 帳戶登入。
2. 左側 hello 頂端囉 」 畫面，按一下 hello 資源群組圖示，然後再按一下 Vm 位於 hello 資源群組 hello (例如， *contosofabrikam*)。 hello**資源群組**刀鋒視窗，其中列出所有 hello 資源以及 hello hello Vm 的網路介面現在會顯示。
3. toohello 次要複本的每個 VM NIC 新增 IP 設定，如下所示：
    1. 選取您想要 tooadd hello IP 組態的 hello 網路介面。
    2. 在 hello 刀鋒視窗中出現的 hello NIC，您選取，按一下  **IP 組態**。 然後按一下 **新增**朝向 hello 顯示 hello 刀鋒視窗的頂端。
    3. 在 hello**新增的 IP 組態**刀鋒視窗中，加入第二個 IP 組態 toohello NIC，如下所示： 
        1. 輸入次要的 IP 組態的名稱 (例如，針對 VM1 和 VM2 名稱 hello 做為 IP 組態*VM1NIC2 ipconfig2*和*VM2NIC2 ipconfig2*分別)。
        2. 針對 [私人 IP 位址]，為 [配置] 選取 [靜態]。
        3. 按一下 [確定] 。
        4. Hello 第二個 IP 組態 hello 次要 NIC 完成時，它會顯示在 hello **IP 組態**hello 指定 NIC 的 設定 刀鋒視窗

### <a name="step-2-create-a-load-balancer"></a>步驟 2：建立負載平衡器

如下所示建立負載平衡器︰

1. 從瀏覽器瀏覽 toohello Azure 入口網站： http://portal.azure.com 並使用您的 Azure 帳戶登入。
2. 在 hello 左邊囉 」 畫面，按一下 **新增** > **網路** > **負載平衡器**。 接下來，按一下 [建立]。
3. 在 hello**建立負載平衡器**刀鋒視窗中，輸入您的負載平衡器的名稱。 在此我們將其稱為 mylb。
4. 在 [公用 IP 位址] 底下建立稱為 **PublicIP1** 的新公用 IP。
5. 在資源群組下選取 hello Vm 的現有的資源群組 (例如， *contosofabrikam*)。 接著選取適當位置，然後按一下確定。 hello 負載平衡器會啟動 toodeploy 和 toosuccessfully 完整部署時將會需要幾分鐘。
6. 一旦部署之後，hello 負載平衡器會顯示為資源群組中的資源。

### <a name="step-3-configure-hello-frontend-ip-pool"></a>步驟 3： 設定 hello 前端 IP 集區

為每個網站 (Contoso 和 Fabrikam) 設定前端 IP 集區，如下所示︰

1. 在 hello 入口網站中，按一下 **更多服務**> 類型**公用 IP 位址**在 hello 篩選 方塊中，然後按一下**公用 IP 位址**。 按一下**新增**朝向 hello 顯示 hello 刀鋒視窗的頂端。
2. 為這兩個網站 (contoso 和 fabrikam) 設定兩個公用 IP 位址 (PublicIP1 和 PublicIP2)，如下所示︰
    1. 輸入前端 IP 位址的名稱。
    2. 如**資源群組**，選取 hello hello Vm 的現有的資源群組 (例如， *contosofabrikam*)。
    3. 如**位置**，選取 hello 相同的位置，如 hello Vm。
    4. 按一下 [確定] 。
    5. 一旦建立 hello 兩個公用 IP 位址，它們會同時顯示在 hello**公用 IP**位址刀鋒視窗。
3. 在 hello 入口網站中，按一下 **更多服務**> 類型**負載平衡器**在 hello 篩選 方塊中，然後按一下**負載平衡器**。  
4. 選取 hello 負載平衡器 (*mylb*) 您想 tooadd hello 前端 IP 集區。
5. 在 [設定] 底下選取 [前端集區]。 然後按一下 **新增**朝向 hello 顯示 hello 刀鋒視窗的頂端。
6. 輸入前端 IP 位址的名稱 (farbikamfe 或 *contosofe)。
7. 按一下**IP 位址**在 hello**選擇公用 IP 位址**刀鋒視窗中，選取 hello 您前端的 IP 位址 (*PublicIP1*或*PublicIP2*).
8. 重複步驟 3 too7 內這個區段 toocreate hello 第二個前端 IP 位址。
9. 這兩個前端 IP 位址 hello 前端 IP 集區組態完成時，會顯示在 hello**前端 IP 集區**刀鋒視窗，您的負載平衡器。 
    
### <a name="step-4-configure-hello-backend-pool"></a>步驟 4： 設定 hello 後端集區   
設定 hello 後端位址集區上您的負載平衡器，為每個網站 （Contoso 和 Fabrikam），如下所示：
        
1. 在 hello 入口網站中，按一下 **更多服務**> 在 hello 篩選方塊中，輸入負載平衡器，然後按一下**負載平衡器**。  
2. 選取 hello 負載平衡器 (*mylb*) 您想要 tooadd hello 後端集區。
3. 在 [設定] 底下選取 [後端集區]。 輸入後端集區的名稱 (例如，contosopool 或 fabrikampool)。 然後按一下 hello**新增**朝 hello 顯示 hello 刀鋒視窗頂端的按鈕。 
4. 在 [關聯到] 中，選取 [可用性設定組]。
5. 在 [可用性設定組] 中，選取 [myAvailset]。
6. 如下所示為這兩個 VM 新增目標網路 IP 組態 (請參閱圖 2)︰  
    1. 如**目標虛擬機器**，選取 hello 想 tooadd toohello 後端集區 （例如，VM1 或 vm2 的情況） 的 VM。
    2. 如**網路 IP 設定**，請選取該 vm （例如，VM1NIC2 ipconfig2 或 VM2NIC2 ipconfig2） hello 次要 Nic IP 設定。
    ![LB 案例影像](./media/load-balancer-multiple-ip/lb-backendpool.PNG)
            
        **圖 2**: hello 負載平衡器設定的後端集區  
7. 按一下 [確定] 。
8. 當 hello 後端集區設定已完成時，這兩個後端位址集區會顯示在 [hello**後端集區] 刀鋒視窗**您的負載平衡器。

### <a name="step-5-configure-a-health-probe-for-your-load-balancer"></a>步驟 5︰設定負載平衡器的健康狀態探查
設定負載平衡器的健康狀態探查，如下所示︰
    1. 在 hello 入口網站中，按一下 更多服務 > 在 hello 篩選方塊中，輸入負載平衡器，然後按一下**負載平衡器**。  
    2. 選取您想要 tooadd hello 後端集區的 hello 負載平衡器。
    3. 在 [設定] 下，選取 [健康狀態探查]。 然後按一下 **新增**朝向 hello 顯示 hello 刀鋒視窗的頂端。
    4. 輸入 hello 健全狀況探查 (例如，HTTP) 的名稱，然後按一下**確定**。

### <a name="step-6-configure-load-balancing-rules"></a>步驟 6：設定負載平衡規則
為每個網站設定負載平衡規則 (HTTPc 和 HTTPf)，如下所示︰
    
1. 在 [設定] 下，選取 [健康狀態探查]。 然後按一下 **新增**朝向 hello 顯示 hello 刀鋒視窗的頂端。
2. 如**名稱**，輸入 hello 負載平衡規則的名稱 (例如， *HTTPc* contoso 或*HTTPf* fabrikam)
3. 前端 IP 位址，選取 hello hello 前端 IP 位址 (例如*Contosofe*或*Fabrikamfe*)
4. 如**連接埠**和**後端連接埠**，保留 hello 預設值**80**。
5. 在 [浮動 IP (伺服器直接回傳)] 中，按一下 [啟用]。
6. 按一下 [確定] 。
7. 重複步驟 1 too6 這個區段 toocreate hello 第二個負載平衡器規則中。
8. Hello 負載平衡規則已完成設定，這兩個規則 ((*HTTPc*和*HTTPf*) 會顯示在 hello**負載平衡規則**刀鋒視窗，您的負載平衡器。

### <a name="step-7-configure-dns-records"></a>步驟 7︰設定 DNS 記錄
最後，您必須設定 DNS 資源記錄 toopoint toohello 各自的前端 IP 位址的 hello 負載平衡器。 您可以在 Azure DNS 中裝載網域。 如需搭配使用 Azure DNS 與 Load Balancer 的詳細資訊，請參閱[使用 Azure DNS 搭配其他 Azure 服務](../dns/dns-for-azure-services.md)。

## <a name="next-steps"></a>後續步驟
- 深入了解如何 toocombine 負載平衡服務在 Azure 中[在 Azure 中使用負載平衡服務](../traffic-manager/traffic-manager-load-balancing-azure.md)。
- 了解如何在 Azure toomanage 中使用不同類型的記錄檔，以及疑難排解負載平衡器中的[Azure 負載平衡器的記錄分析](../load-balancer/load-balancer-monitor-log.md)。
