---
title: "aaaScale Service Fabric 叢集 in 或 out |Microsoft 文件"
description: "縮放 Service Fabric 叢集 in 或 out toomatch 視需要設定每個節點型別/虛擬機器擴展集自動調整規模規則。 新增或移除節點 tooa Service Fabric 叢集"
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: aeb76f63-7303-4753-9c64-46146340b83d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/22/2017
ms.author: chackdan
ms.openlocfilehash: 37cfeaf80edc016cf6de017d1c2dc6fbcb8acc2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-service-fabric-cluster-in-or-out-using-auto-scale-rules"></a>使用自動調整規模規則相應縮小或放大 Service Fabric 叢集
虛擬機器擴展集是 Azure 計算資源，您可以使用 toodeploy 和管理的虛擬機器作為一組的集合。 在 Service Fabric 叢集中定義的每個節點類型都會安裝為不同的虛擬機器擴展集。 然後每個節點類型可以獨立相應縮小或放大，可以開啟不同組的連接埠，並可以有不同的容量度量。 深入了解在 hello [Service Fabric nodetypes](service-fabric-cluster-nodetypes.md)文件。 由於 hello Service Fabric 節點型別，在叢集中的虛擬機器擴展集在 hello 後端進行，您會需要每個節點型別/虛擬機器擴展集 tooset 自動調整規模規則。

> [!NOTE]
> 您的訂用帳戶必須擁有足夠的核心 tooadd hello 這個叢集所組成的新 Vm。 沒有模型驗證目前，因此您會取得部署階段失敗，如果任何 hello 配額限制會叫用。
> 
> 

## <a name="choose-hello-node-typevirtual-machine-scale-set-tooscale"></a>選擇 hello 節點型別/虛擬機器擴展集 tooscale
目前，您不使用 hello 入口網站的虛擬機器擴展集無法 toospecify hello 自動調整規模規則，因此讓我們使用 Azure PowerShell （1.0 +） toolist hello 節點型別然後再加入自動調整規模規則 toothem。

虛擬機器擴展集的 tooget hello 清單構成您叢集，請執行下列 cmdlet 的 hello:

```powershell
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Compute/VirtualMachineScaleSets

Get-AzureRmVmss -ResourceGroupName <RGname> -VMScaleSetName <Virtual Machine scale set name>
```

## <a name="set-auto-scale-rules-for-hello-node-typevirtual-machine-scale-set"></a>設定自動調整規模規則的 hello 節點型別/虛擬機器規模集
如果您的叢集有多個節點類型，然後重複此作業對於每個節點型別/虛擬機器規模設定的 tooscale （in 或 out）。 會將節點帳戶 hello 數目，您必須有設定自動調整之前。 您已選擇 hello 可靠性層級有驅動 hello hello 主要節點類型，您必須擁有的節點數目下限。 深入了解 [可靠性層級](service-fabric-cluster-capacity.md)。

> [!NOTE]
> 縮小 hello 主要節點類型 tooless 多於 hello 最小數目進行 hello 叢集不穩定，或將它關機。 這可能導致資料遺失對於您的應用程式與 hello 系統服務。
> 
> 

目前 hello 自動調整規模功能不受到 hello 載入 tooService 網狀架構可能會報告您的應用程式。 因此在此時間 hello 自動調整規模，就是單純地驅動 hello 效能計數器，所發出的每個 hello 虛擬機器規模集執行個體。  

請遵循下列指示[總每個虛擬機器擴展集自動調整規模 tooset](../virtual-machine-scale-sets/virtual-machine-scale-sets-autoscale-overview.md)。

> [!NOTE]
> 在向下調整的案例中，除非您的節點型別具有金級 」 或 「 銀級持久性層級，您需要 toocall hello[移除 ServiceFabricNodeState cmdlet](https://msdn.microsoft.com/library/azure/mt125993.aspx) hello 適當的節點名稱。
> 
> 

## <a name="manually-add-vms-tooa-node-typevirtual-machine-scale-set"></a>手動新增 Vm tooa 節點型別/虛擬機器規模集
請依照 hello 範例/hello 中指示[快速入門範本庫](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing)toochange hello 數目中每個節點類型的 Vm。 

> [!NOTE]
> 新增 Vm 需要時間，所以不要期待 hello 新增 toobe 瞬間完成。 因此也會在時間 tooallow 超過 10 分鐘才能供 hello 複本 hello 的 VM 容量規劃 tooadd 容量/服務執行個體 tooget 放置。
> 
> 

## <a name="manually-remove-vms-from-hello-primary-node-typevirtual-machine-scale-set"></a>手動移除 hello 主要節點類型/虛擬機器規模集的 Vm
> [!NOTE]
> hello 服務網狀架構系統服務在 hello 主要節點類型，在叢集中執行。 所以應該永遠不會關機或調降 hello 該節點型別中的執行個體數目小於哪些 hello 可靠性層保證。 請參閱太[hello 可靠性層級的詳細資訊](service-fabric-cluster-capacity.md)。 
> 
> 

您需要 tooexecute hello 下列步驟會一次一個 VM 執行個體。 這可讓 hello 系統服務 （以及您可設定狀態的服務） toobe 正常關閉您要移除 hello VM 執行個體和其他節點上建立的新複本。

1. 執行[停用 ServiceFabricNode](https://msdn.microsoft.com/library/mt125852.aspx)與意圖 'RemoveNode' toodisable hello 節點將 tooremove （hello 最大執行個體在該節點類型）。
2. 執行[Get ServiceFabricNode](https://msdn.microsoft.com/library/mt125856.aspx) toomake 確定該 hello 節點已確實轉換 toodisabled。 如果沒有，請等到 hello 節點停用。 您無法加快此步驟的速度。
3. 請依照 hello 範例/hello 中指示[快速入門範本庫](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing)toochange hello Vm 數目加一該的 Nodetype。 移除 hello 執行個體是 hello 最高的 VM 執行個體。 
4. 重複步驟 1 到 3，如有需要但永遠不會縮小 hello hello 主要節點類型小於需要哪些 hello 可靠性層中的執行個體數目。 請參閱太[hello 可靠性層級的詳細資訊](service-fabric-cluster-capacity.md)。 

## <a name="manually-remove-vms-from-hello-non-primary-node-typevirtual-machine-scale-set"></a>手動移除 hello 非主要節點類型/虛擬機器規模集的 Vm
> [!NOTE]
> 可設定狀態的服務，您需要節點 toobe 數目一律 toomaintain 可用性和保留狀態，您的服務。 在 hello 非常小，您需要節點等於 toohello 目標複本集的計數 hello 磁碟分割/服務的 hello 的數目。 
> 
> 

您需要 hello 執行 hello 遵循步驟一個 VM 執行個體一次。 這可 hello 系統服務 （以及您可設定狀態的服務） toobe 正常關機 hello 上要移除的 VM 執行個體，而且新的複本建立的其他位置。

1. 執行[停用 ServiceFabricNode](https://msdn.microsoft.com/library/mt125852.aspx)與意圖 'RemoveNode' toodisable hello 節點將 tooremove （hello 最大執行個體在該節點類型）。
2. 執行[Get ServiceFabricNode](https://msdn.microsoft.com/library/mt125856.aspx) toomake 確定該 hello 節點已確實轉換 toodisabled。 如果不是等到 hello 節點停用。 您無法加快此步驟的速度。
3. 請依照 hello 範例/hello 中指示[快速入門範本庫](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing)toochange hello Vm 數目加一該的 Nodetype。 這會立即移除 hello 最高的 VM 執行個體。 
4. 重複步驟 1 到 3，如有需要但永遠不會縮小 hello hello 主要節點類型小於需要哪些 hello 可靠性層中的執行個體數目。 請參閱太[hello 可靠性層級的詳細資訊](service-fabric-cluster-capacity.md)。

## <a name="behaviors-you-may-observe-in-service-fabric-explorer"></a>Service Fabric Explorer 可能出現的行為
當您擴充叢集 hello Service Fabric 總管將會反映 hello 數字的節點 （虛擬機器規模集執行個體） 是 hello 叢集的一部分。  不過，當您調整叢集清單中，您會看到 hello 移除節點/VM 執行個體顯示在狀況不良狀態，除非您呼叫[移除 ServiceFabricNodeState cmd](https://msdn.microsoft.com/library/mt125993.aspx) hello 適當的節點名稱。   

以下是這種行為的 hello 說明。

hello Service Fabric 總管中所列的節點會反映出 hello Service Fabric 系統服務 (FM 特別) 知道有/有的節點 hello 叢集的 hello 數目。 當您調整 hello 虛擬機器擴展集時，hello VM 已刪除，但是 FM 系統服務仍然會認為該 hello 節點 （也就是對應的 toohello 已刪除的 VM） 將回來。 因此 Service Fabric 總管會繼續 toodisplay 該節點 （雖然 hello 健全狀況狀態可能是錯誤或不明）。

在訂單 toomake 確定節點已移除的 VM 時，您會有兩個選項：

1) 選擇金級 」 或 「 銀級持久性層級 (可立即) 的 hello 叢集中的節點型別，可讓您 hello 基礎結構整合。 這將會自動 hello 節點從我們的系統服務 (FM) 狀態時移除您向下調整。
請參閱太[hello 持久性層級的詳細資訊](service-fabric-cluster-capacity.md)

2) 一旦已縮小 hello VM 執行個體，您需要 toocall hello[移除 ServiceFabricNodeState cmdlet](https://msdn.microsoft.com/library/mt125993.aspx)。

> [!NOTE]
> 服務網狀架構叢集節點 toobe 數目向上在需要所有 hello 時間順序 toomaintain 可用性和保留狀態-參照 tooas 「 維持仲裁 」。 因此，它是向 hello 叢集中的所有 hello 機器通常不安全 tooshut 除非您先執行[狀態的完整備份](service-fabric-reliable-services-backup-restore.md)。
> 
> 

## <a name="next-steps"></a>後續步驟
讀取 hello 遵循 tooalso 深入了解規劃叢集的容量、 升級叢集，以及資料分割服務：

* [規劃叢集容量](service-fabric-cluster-capacity.md)
* [叢集升級](service-fabric-cluster-upgrade.md)
* [分割具狀態服務以達最大規模](service-fabric-concepts-partitioning.md)

<!--Image references-->
[BrowseServiceFabricClusterResource]: ./media/service-fabric-cluster-scale-up-down/BrowseServiceFabricClusterResource.png
[ClusterResources]: ./media/service-fabric-cluster-scale-up-down/ClusterResources.png
