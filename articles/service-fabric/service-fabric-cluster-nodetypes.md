---
title: "aaaService 網狀架構節點型別與 VM 規模集 |Microsoft 文件"
description: "說明 Service Fabric 節點型別與 tooVM 規模集的關聯，以及 tooremote 連線 tooa 虛擬機器擴展集的執行個體或叢集節點的方式。"
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 5441e7e0-d842-4398-b060-8c9d34b07c48
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: chackdan
ms.openlocfilehash: 830ea2816f5864de146a77483c85de26f91c2425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="hello-relationship-between-service-fabric-node-types-and-virtual-machine-scale-sets"></a>hello Service Fabric 節點型別和虛擬機器擴展集之間的關聯性
虛擬機器擴展集是您可以使用 toodeploy 和管理虛擬機器的集合做為一組 Azure 計算資源。 在 Service Fabric 叢集中定義的每個節點類型都會安裝為不同的 VM 擴展集。 然後每個節點類型可以獨立相應增加或相應減少，可以開啟不同組的連接埠，並可以有不同的容量度量。

下列螢幕擷取畫面的 hello 示範具有兩個節點類型的叢集： 前端及後端。  每個節點類型各有五個節點。

![有兩個節點類型的叢集螢幕擷取畫面][NodeTypes]

## <a name="mapping-vm-scale-set-instances-toonodes"></a>對應虛擬機器擴展集的執行個體 toonodes
您可以看到上方，hello 虛擬機器擴展集的執行個體從執行個體 0 開始，然後向上。 hello 編號會反映在 hello 名稱。 例如，BackEnd_0 是 hello 後端虛擬機器擴展集的執行個體 0。 這個特定的 VM 調整集有五個執行個體，名稱分別是 BackEnd_0、BackEnd_1、BackEnd_2、BackEnd_3、BackEnd_4。

當您相應增加 VM 調整集，就會建立的新執行個體。 hello VM 規模調整集合名稱 + hello 下一個執行個體數字，通常會是 hello 新虛擬機器擴展集執行個體名稱。 在我們的範例中是 BackEnd_5。

## <a name="mapping-vm-scale-set-load-balancers-tooeach-node-typevm-scale-set"></a>對應 VM 規模集負載平衡器 tooeach 節點型別/VM 規模集
如果您已部署您的叢集，從 hello 入口網站，或使用我們提供，然後當您取得一份資源群組下所有資源的 hello 範例資源管理員範本，您會看到每個虛擬機器擴展集或節點類型的 hello 負載平衡器。

hello 名稱會像這樣： **LB 集&lt;NodeType 名稱&gt;**。 例如，以下螢幕擷取畫面中的 LB-sfcluster4doc-0：

![資源][Resources]

## <a name="remote-connect-tooa-vm-scale-set-instance-or-a-cluster-node"></a>遠端連接 tooa 虛擬機器擴展集的執行個體或叢集節點
在叢集中定義的每個節點類型都會安裝為不同的 VM 擴展集。  表示 hello 節點型別可以縮放向上或向下獨立和可由不同的 VM Sku。 不同於單一執行個體的 Vm，hello 虛擬機器擴展集的執行個體不會收到自己的虛擬 IP 位址。 因此，它可以是位元挑戰時您所需的 IP 位址和連接埠，您可以使用 tooremote 連接 tooa 特定執行個體。

以下是您可以依照 toodiscover hello 步驟它們。

### <a name="step-1-find-out-hello-virtual-ip-address-for-hello-node-type-and-then-inbound-nat-rules-for-rdp"></a>步驟 1： 了解 hello 節點型別 hello 虛擬 IP 位址，然後 RDP 的輸入 NAT 規則
中，您需要 tooget hello 順序 tooget 連入的 NAT 規則值所定義的 hello 資源定義的一部分**Microsoft.Network/loadBalancers**。

在 hello 入口網站中，瀏覽 toohello 負載平衡器刀鋒視窗，然後**設定**。

![LBBlade][LBBlade]

在 [設定] 中，按一下 [輸入 NAT 規則]。 這可讓您 hello IP 位址和連接埠，您可以使用 tooremote 連接 toohello 第一個虛擬機器擴展集的執行個體。 在 hello 以下螢幕擷取畫面，它是**104.42.106.156**和**3389**

![NATRules][NATRules]

### <a name="step-2-find-out-hello-port-that-you-can-use-tooremote-connect-toohello-specific-vm-scale-set-instancenode"></a>步驟 2： 了解 hello 連接埠，您可以使用 tooremote toohello 特定虛擬機器擴展集執行個體/節點連接
本文件稍早我討論 hello 虛擬機器擴展集的執行個體將 toohello 節點的對應。 我們將使用該 toofigure 出 hello 確切的通訊埠。

hello 連接埠配置以遞增順序 hello 虛擬機器擴展集的執行個體。 因此在 hello 前端節點類型的範例中，每個 hello 五個執行個體的 hello 連接埠是 hello 下列。 您 toodo 現在需要 hello 相同的對應虛擬機器擴展集執行個體。

| **VM 擴展集執行個體** | **連接埠** |
| --- | --- |
| FrontEnd_0 |3389 |
| FrontEnd_1 |3390 |
| FrontEnd_2 |3391 |
| FrontEnd_3 |3392 |
| FrontEnd_4 |3393 |
| FrontEnd_5 |3394 |

### <a name="step-3-remote-connect-toohello-specific-vm-scale-set-instance"></a>步驟 3： 遠端連線 toohello 特定虛擬機器擴展集執行個體
Hello 以下螢幕擷取畫面中使用遠端桌面連線 tooconnect toohello FrontEnd_1:

![RDP][RDP]

## <a name="how-toochange-hello-rdp-port-range-values"></a>Toochange hello RDP 連接埠值的範圍
### <a name="before-cluster-deployment"></a>叢集部署之前
當您設定 hello 叢集使用的資源管理員範本時，您可以指定 hello 範圍 hello **inboundNatPools**。

移 toohello 資源定義**Microsoft.Network/loadBalancers**。 下，您會發現 hello 描述**inboundNatPools**。  取代 hello *frontendPortRangeStart*和*frontendPortRangeEnd*值。

![inboundNatPools][InboundNatPools]

### <a name="after-cluster-deployment"></a>叢集部署之後
這是稍微複雜，而且可能會導致 hello Vm 被回收。 您現在就必須使用 Azure PowerShell tooset 新值。 請確定您的電腦已安裝 Azure PowerShell 1.0+ 或更新版本。 如果您有不這麼做之前，我們強烈建議您遵循所述的 hello 步驟[如何 tooinstall 和設定 Azure PowerShell。](/powershell/azure/overview)

Azure 帳戶登入 tooyour。 如果這個 PowerShell 命令因為某些原因無法運作，您應該檢查 Azure PowerShell 是否已正確安裝。

```
Login-AzureRmAccount
```

執行下列 tooget 詳細資料，您的負載平衡器上的 hello 和您看到的 hello 描述的 hello 值**inboundNatPools**:

```
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load balancer name>
```

現在設定*frontendPortRangeEnd*和*frontendPortRangeStart* toohello 您想要的值。

```
$PropertiesObject = @{
    #Property = value;
}
Set-AzureRmResource -PropertyObject $PropertiesObject -ResourceGroupName <RG name> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load Balancer name> -ApiVersion <use hello API version that get returned> -Force
```


## <a name="next-steps"></a>後續步驟
* [Hello 「 任何位置部署 」 功能與使用 Azure 管理叢集的比較概觀](service-fabric-deploy-anywhere.md)
* [叢集安全性](service-fabric-cluster-security.md)
* [ Service Fabric SDK 和開始使用](service-fabric-get-started.md)

<!--Image references-->
[NodeTypes]: ./media/service-fabric-cluster-nodetypes/NodeTypes.png
[Resources]: ./media/service-fabric-cluster-nodetypes/Resources.png
[InboundNatPools]: ./media/service-fabric-cluster-nodetypes/InboundNatPools.png
[LBBlade]: ./media/service-fabric-cluster-nodetypes/LBBlade.png
[NATRules]: ./media/service-fabric-cluster-nodetypes/NATRules.png
[RDP]: ./media/service-fabric-cluster-nodetypes/RDP.png
