---
title: "服務網狀架構以程式設計方式調整 aaaAzure |Microsoft 文件"
description: "調整 Azure Service Fabric 叢集或以程式設計的方式，根據 toocustom 觸發程序"
services: service-fabric
documentationcenter: .net
author: mjrousos
manager: jonjung
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: mikerou
ms.openlocfilehash: a0c6499b1a143a173006248cf8a15380632637e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-service-fabric-cluster-programmatically"></a>以程式設計方式調整 Service Fabric 叢集 

在關於[叢集調整](./service-fabric-cluster-scale-up-down.md)的文件中探討了 Azure Service Fabric 叢集調整的基本概念。 該文章探討如何以虛擬機器擴展集為基礎來建置 Service Fabric 叢集，以及如何以手動方式或自動調整規則來加以調整。 本文件則探討如何以程式設計方法讓 Azure 調整作業能夠配合更進階的案例。 

## <a name="reasons-for-programmatic-scaling"></a>以程式設計方式調整的原因
在許多案例中，以手動方式或透過自動調整規則來調整是不錯的解決方案。 在其他情況下，不過，它們可能不是右符合 hello。 潛在缺點 toothese 方法包括：

- 手動調整會要求您在 toolog 且明確地調整作業的要求。 如果調整作業需要經常進行或難以預料會在何時進行，這個方法可能就不是合適的解決方案。
- 當自動調整規模規則移除虛擬機器規模集的執行個體時，他們不要自動移除該節點的知識相關聯的 hello Service Fabric 叢集除非 hello 節點型別具有銀級或金級持久性層級。 自動調整規模規則才有作用大規模 hello 設定層級 （而不是在 hello Service Fabric 級），因為自動調整規模規則可以移除 Service Fabric 節點，而不會關閉它們依正常程序。 以這種方式粗糙地移除節點，會在相應縮小作業完成後留下「準刪除」的 Service Fabric 節點狀態。 個人 （或服務） 需要 tooperiodically 清除 hello Service Fabric 叢集中移除的節點狀態。
  - 請注意，持久性等級為金級或銀級的節點類型會自動清除已移除的節點。  
- 雖然自動調整規則支援[許多計量](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md)，但這組計量的數量仍然有限。 如果您的案例所需要的調整是以該組計量所未涵蓋的一些計量為基礎，則自動調整規則可能不是很好的選擇。

根據這些限制，您可能希望 tooimplement 多自訂自動調整的模型。 

## <a name="scaling-apis"></a>調整 API
Azure 應用程式開發介面存在可讓應用程式 tooprogrammatically 工作虛擬機器擴展集與 Service Fabric 叢集。 如果現有的自動調整規模選項不適用於您案例，這些 Api 使得可能 tooimplement 自訂縮放邏輯。 

其中一個方法 tooimplementing '首頁-變' 的自動調整功能是 tooadd 新無狀態服務 toohello Service Fabric 應用程式 toomanage 調整作業。 Hello 服務內`RunAsync`方法，觸發程序的一組可以判斷是否需要 （包括檢查參數，例如最大叢集大小和縮放比例 cooldowns） 縮放比例。   

hello 用於虛擬機器規模集互動的應用程式開發介面 (這兩個 toocheck hello 目前虛擬機器執行個體數目和 toomodify 它) 為 hello [fluent 應用程式開發的 Azure 管理計算文件庫](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/)。 hello fluent 應用程式開發的計算程式庫提供方便使用 API 與虛擬機器擴展集互動。

toointeract hello Service Fabric 叢集本身，以使用[System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient)。

當然，hello 調整程式碼不需要當做服務 toorun hello 叢集 toobe 縮放中。 同時`IAzure`和`FabricClient`可以 tootheir 相關聯的 Azure 資源從遠端連線，因此 hello 擴充服務可以輕鬆地是主控台應用程式或從外部 hello Service Fabric 應用程式執行的 Windows 服務。 

## <a name="credential-management"></a>認證管理
撰寫服務 toohandle 縮放比例的一項挑戰是 hello 服務必須能夠 tooaccess 不使用互動式登入虛擬機器小數位數設定資源。 存取 hello Service Fabric 叢集如果很容易 hello 擴充服務正在修改自己的 Service Fabric 應用程式，但認證需要的 tooaccess hello 規模集。 您可以使用在 toolog，[服務主體](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure)建立 hello [Azure CLI 2.0](https://github.com/azure/azure-cli)。

可以建立服務主體以 hello 下列步驟：

1. 登入 Azure CLI toohello (`az login`) 具有存取 toohello 虛擬機器規模的使用者設定
2. 建立 hello 服務主體`az ad sp create-for-rbac`
    1. 請記下 hello appId （他處呼叫 '用戶端 ID'）、 名稱、 密碼及租用戶，以供稍後使用。
    2. 您還需要訂用帳戶識別碼，若要檢視此識別碼，請使用 `az account list`

hello fluent 應用程式開發的計算程式庫可以使用登入這些認證，如下所示 (請注意核心 fluent 應用程式開發的 Azure 型別想`IAzure`位於 hello [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/)封裝):

```C#
var credentials = new AzureCredentials(new ServicePrincipalLoginInformation {
                ClientId = AzureClientId,
                ClientSecret = 
                AzureClientKey }, AzureTenantId, AzureEnvironment.AzureGlobalCloud);
IAzure AzureClient = Azure.Authenticate(credentials).WithSubscription(AzureSubscriptionId);

if (AzureClient?.SubscriptionId == AzureSubscriptionId)
{
    ServiceEventSource.Current.ServiceMessage(Context, "Successfully logged into Azure");
}
else
{
    ServiceEventSource.Current.ServiceMessage(Context, "ERROR: Failed toologin tooAzure");
}
```

登入之後，可以透過 `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity` 來查詢擴展集的執行個體計數。

## <a name="scaling-out"></a>相應放大
使用 hello fluent 應用程式開發 Azure 計算 SDK，可加入執行個體 toohello 虛擬機器擴展集與少數呼叫-

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);
var newCapacity = (int)Math.Min(MaximumNodeCount, scaleSet.Capacity + 1);
scaleSet.Update().WithCapacity(newCapacity).Apply(); 
``` 

或者，也可以使用 PowerShell Cmdlet 來管理虛擬機器擴展集大小。 [`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss)可以擷取 hello 虛擬機器規模集物件。 hello 目前的容量會儲存在 hello`.sku.capacity`屬性。 Hello 虛擬機器擴展集在 Azure 中變更 hello 容量 toohello 所需的值之後，可以更新以 hello [ `Update-AzureRmVmss` ](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss)命令。

時以手動方式加入的節點，將規模調整集合執行個體應該是所有的所需的 toostart 包含新的 Service Fabric 節點由於 hello 規模調整集合範本延伸 tooautomatically 加入新的執行個體 toohello Service Fabric 叢集。 

## <a name="scaling-in"></a>相應縮小

中的縮放比例是類似 tooscaling 出。hello 實際上會變更的實際虛擬機器規模集 hello 相同。 但就如先前所討論的，Service Fabric 只會自動清除持久性為金級或銀級的已移除節點。 因此，您也可以在 hello 銅級持久性小數位數的情況下，它是以 hello Service Fabric 需要 toointeract 叢集下移除 hello 節點 toobe tooshut 然後 tooremove 其狀態。

準備 hello 節點關機包括找出 hello 節點 toobe 移除 （hello 最近加入的節點） 並停用它。 對於非種子節點，可以藉由比較 `NodeInstanceId` 來找到較新的節點。 

```C#
using (var client = new FabricClient())
{
    var mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync())
        .Where(n => n.NodeType.Equals(NodeTypeToScale, StringComparison.OrdinalIgnoreCase))
        .Where(n => n.NodeStatus == System.Fabric.Query.NodeStatus.Up)
        .OrderByDescending(n => n.NodeInstanceId)
        .FirstOrDefault();
```

請注意，*種子*節點看上去不 tooalways 遵循 hello 慣例，會先移除更大的執行個體識別碼。

一旦找到 hello 節點 toobe 移除，可以停用和移除使用 hello 相同`FabricClient`執行個體和 hello`IAzure`從先前的執行個體。

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);

// Remove hello node from hello Service Fabric cluster
ServiceEventSource.Current.ServiceMessage(Context, $"Disabling node {mostRecentLiveNode.NodeName}");
await client.ClusterManager.DeactivateNodeAsync(mostRecentLiveNode.NodeName, NodeDeactivationIntent.RemoveNode);

// Wait (up tooa timeout) for hello node toogracefully shutdown
var timeout = TimeSpan.FromMinutes(5);
var waitStart = DateTime.Now;
while ((mostRecentLiveNode.NodeStatus == System.Fabric.Query.NodeStatus.Up || mostRecentLiveNode.NodeStatus == System.Fabric.Query.NodeStatus.Disabling) &&
        DateTime.Now - waitStart < timeout)
{
    mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync()).FirstOrDefault(n => n.NodeName == mostRecentLiveNode.NodeName);
    await Task.Delay(10 * 1000);
}

// Decrement VMSS capacity
var newCapacity = (int)Math.Max(MinimumNodeCount, scaleSet.Capacity - 1); // Check min count 

scaleSet.Update().WithCapacity(newCapacity).Apply(); 
```

與相應放大規模時相同，如果偏好使用指令碼處理方法，在這裡也可以使用修改虛擬機器擴展集容量的 PowerShell Cmdlet。 一旦移除 hello 虛擬機器執行個體時，就可以移除 Service Fabric 節點狀態。

```C#
await client.ClusterManager.RemoveNodeStateAsync(mostRecentLiveNode.NodeName);
```

## <a name="potential-drawbacks"></a>可能的缺點

Hello 前面程式碼片段所示，建立縮放的服務提供 hello 高程度的控制權和自訂您的應用程式上的縮放行為。 這很適合用於需要精確控制應用程式相應縮小或放大之時機或方式的案例。不過，伴隨此控制能力而來的是程式碼會變得複雜。 使用這種方式表示您需要 tooown 調整為非一般的程式碼。

處理 Service Fabric 調整的方式取決於您的案例。 縮放比例不常見，如果 hello 能力 tooadd 或移除節點，則手動可能足夠。 更複雜的情況下，自動調整規模規則和以程式設計方式公開 hello 能力 tooscale 的 Sdk 提供功能強大的替代項目。

## <a name="next-steps"></a>後續步驟

tooget 啟動實作您自己的自動調整的邏輯，會將您自己熟悉 hello 下列概念和有用的 Api:

- [以手動方式或透過自動調整規則進行調整](./service-fabric-cluster-scale-up-down.md)
- [適用於 .NET 的 Fluent Azure 管理程式庫](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (適用於與 Service Fabric 叢集的基礎虛擬機器擴展集互動)
- [System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (適用於與 Service Fabric 叢集及其節點互動)
