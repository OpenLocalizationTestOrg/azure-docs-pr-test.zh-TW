---
title: "aaaMutiple Vip 的雲端服務"
description: "多個 Vip 的概觀以及如何 tooset 雲端服務上的多個 Vip"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 85f6d26a-3df5-4b8e-96a1-92b2793b5284
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: b3e0f2b24968cb75a7064484a09ffe94505bb70b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multiple-vips-for-a-cloud-service"></a>為單一雲端服務設定多個 VIP

您可以透過公用網際網路所使用的 IP 位址提供的 azure 的 hello 存取 Azure 雲端服務。 這個公用 IP 位址是參照的 tooas VIP (虛擬 IP)，因為它連結 toohello Azure 負載平衡器，並不 hello hello 雲端服務內的虛擬機器 (VM) 執行個體。 您可以使用單一 VIP 來存取雲端服務中的任何 VM 執行個體。

不過，有可能需要多個 VIP 案例做為進入點 toohello 相同雲端服務。 比方說，您的雲端服務可以裝載多個不同的客戶裝載每個站台需要 SSL 連線使用 hello 預設連接埠 443，或租用戶的網站。 在此案例中，您會為每個網站需要 toohave 不同的公用對外 IP 位址。 hello 圖說明典型的多租用戶 web 裝載的具有需要多個 SSL 憑證上 hello 相同公用連接埠。

![多重 VIP SSL 案例](./media/load-balancer-multivip/Figure1.png)

在上述所有 Vip 使用 hello hello 範例相同的公用連接埠 (443) 和流量會重新導向的 tooone 或多個負載平衡的 Vm hello 內部 IP 位址的 hello 雲端服務裝載 hello 的所有網站的唯一私用連接埠。

> [!NOTE]
> 另一種情況需要 hello 使用 hello 多個 Vip 裝載多個 SQL AlwaysOn 可用性群組接聽程式 hello 相同設定的虛擬機器上。

Vip 是動態的根據預設，這表示 hello 實際的 IP 位址指派 toohello 雲端服務會隨著時間變更。 tooprevent，種情況，您可以保留 VIP 為您的服務。 toolearn 深入了解保留 Vip，請參閱[保留公用 IP](../virtual-network/virtual-networks-reserved-public-ip.md)。

> [!NOTE]
> 如需有關 VIP 和保留的 IP 的定價資訊，請參閱 [IP 位址定價](https://azure.microsoft.com/pricing/details/ip-addresses/) 。

您可以使用 PowerShell tooverify hello 您的雲端服務所使用的 Vip，以及新增和移除 Vip、 建立關聯的 VIP tooan 端點，並設定負載平衡的特定 VIP 上。

## <a name="limitations"></a>限制

此時，多重 VIP 功能是限制的 toohello 下列案例：

* **僅限 IaaS**。 您只能針對包含 VM 的雲端服務啟用多重 VIP。 您無法在具有角色執行個體的 PaaS 案例中使用多重 VIP。
* **僅限 PowerShell**。 您只能使用 PowerShell 來管理多重 VIP。

這些限制都是暫時的，隨時可能變更。 請確定 toorevisit 此頁面 tooverify 未來變更。

## <a name="how-tooadd-a-vip-tooa-cloud-service"></a>Tooadd VIP tooa 雲端服務的方式
tooadd VIP tooyour 服務，執行下列 PowerShell 命令的 hello:

```powershell
Add-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

此命令會顯示結果類似 toohello，下列範例：

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Add-AzureVirtualIP   4bd7b638-d2e7-216f-ba38-5221233d70ce Succeeded

## <a name="how-tooremove-a-vip-from-a-cloud-service"></a>如何從雲端服務的 VIP tooremove
tooremove hello VIP 加入 tooyour 服務在上面，執行下列 PowerShell 命令的 hello 的 hello 範例：

```powershell
Remove-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

> [!IMPORTANT]
> 如果不有任何相關聯的端點 tooit，您只可以移除 VIP。


## <a name="how-tooretrieve-vip-information-from-a-cloud-service"></a>如何從雲端服務的 tooretrieve VIP 資訊
tooretrieve hello Vip 相關聯的雲端服務，執行下列 PowerShell 指令碼的 hello:

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

hello 指令碼會顯示結果類似 toohello，下列範例：

    Address         : 191.238.74.148
    IsDnsProgrammed : True
    Name            : Vip1
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip2
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip3
    ReservedIPName  :
    ExtensionData   :

在此範例中，hello 雲端服務都有 3 Vip:

* **Vip1**是 hello 預設 VIP，但您知道，因為設定 tootrue IsDnsProgrammedName hello 值。
* **Vip2** 和 **Vip3** 因為沒有任何 IP 位址而不會予以使用。 此外，它們只能將使用如果您將端點 toohello VIP 產生關聯。

> [!NOTE]
> 有額外的 VIP 與端點相關聯時，才會向您的訂用帳戶收費。 如需定價的詳細資訊，請參閱 [IP 位址定價](https://azure.microsoft.com/pricing/details/ip-addresses/)。

## <a name="how-tooassociate-a-vip-tooan-endpoint"></a>如何 tooassociate VIP tooan 端點

在雲端服務 tooan 端點上，執行下列 PowerShell 命令的 hello tooassociate VIP:

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -Protocol tcp -LocalPort 8080 -PublicPort 80 -VirtualIPName Vip2 |
    Update-AzureVM
```

hello 命令會建立稱為 「 連結的 toohello VIP 端點*Vip2*連接埠上*80*，並將它連結 toohello 名為 VM *myVM1*雲端服務中名為*myService*使用*TCP*連接埠上*8080*。

tooverify hello 組態，執行下列 PowerShell 命令的 hello:

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

hello 輸出看起來類似下列範例的 toohello:

    Address         : 191.238.74.148
    IsDnsProgrammed : True
    Name            : Vip1
    ReservedIPName  :
    ExtensionData   :

    Address         : 191.238.74.13
    IsDnsProgrammed :
    Name            : Vip2
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip3
    ReservedIPName  :
    ExtensionData   :

## <a name="how-tooenable-load-balancing-on-a-specific-vip"></a>如何 tooenable 上的負載平衡的特定 VIP

您可以將單一 VIP 與多部虛擬機器產生關聯，以達到負載平衡。 例如，假設您有名為 *myService* 的雲端服務，以及名為 *myVM1* 和 *myVM2* 的兩部虛擬機器。 而您的雲端服務有多重 VIP，其中一個名為 *Vip2*。 如果您想要的所有流量 tooport tooensure *81*上*Vip2*之間平均*myVM1*和*myVM2*連接埠上*8181*，請執行 hello 下列 PowerShell 指令碼：

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2 -DefaultProbe |
    Update-AzureVM

Get-AzureVM -ServiceName myService -Name myVM2 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2  -DefaultProbe |
    Update-AzureVM
```

您也可以更新您的負載平衡器 toouse 不同的 VIP。 例如，如果您要執行 hello 下列 PowerShell 命令，將變更 hello 負載平衡集 toouse 名為 Vip1 VIP:

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName myService -LBSetName myLBSet -VirtualIPName Vip1
```

## <a name="next-steps"></a>後續步驟

[Azure 負載平衡器的 Log Analytics](load-balancer-monitor-log.md)

[網際網路面向的負載平衡器概觀](load-balancer-internet-overview.md)

[開始使用網際網路面向的負載平衡器](load-balancer-get-started-internet-arm-ps.md)

[虛擬網路概觀](../virtual-network/virtual-networks-overview.md)

[保留的 IP REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx)
