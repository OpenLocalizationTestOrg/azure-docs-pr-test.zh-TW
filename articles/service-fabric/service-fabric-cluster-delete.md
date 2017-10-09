---
title: "aaaDelete Azure 叢集和其資源 |Microsoft 文件"
description: "了解如何 toocompletely 刪除 Service Fabric 叢集包含 hello 叢集中任一個刪除 hello 資源群組，或藉由選擇性地刪除資源。"
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: de422950-2d22-4ddb-ac47-dd663a946a7e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/24/2017
ms.author: chackdan
ms.openlocfilehash: 5c15a4184644da715cd69397f2150de86ab433ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="delete-a-service-fabric-cluster-on-azure-and-hello-resources-it-uses"></a>刪除 Azure 與 hello 的資源，它會使用 Service Fabric 叢集
Service Fabric 叢集所組成的許多其他 Azure 資源此外 toohello 叢集資源本身。 因此 toocompletely 刪除 Service Fabric 叢集，您也需要的 toodelete 所有 hello 則由的資源。
有兩個選項： hello 叢集中任一個刪除 hello 資源群組處於 （這會刪除 hello 叢集資源和 hello 資源群組中的任何其他資源） 或明確刪除 hello 叢集資源，以及它有相關聯的資源 （但不是 其他資源 hello 資源群組中）。

> [!NOTE]
> 正在刪除 hello 叢集資源**不**刪除所有 hello 所組成的 Service Fabric 叢集的其他資源。
> 
> 

## <a name="delete-hello-entire-resource-group-rg-that-hello-service-fabric-cluster-is-in"></a>刪除 hello 整個資源群組 (RG) hello Service Fabric 叢集處於
這是 hello 您刪除所有與您的叢集，包括 hello 資源群組相關聯的 hello 資源最簡單方式 tooensure。 您可以刪除 hello 資源群組使用 PowerShell 或透過 hello Azure 入口網站。 如果您的資源群組擁有的資源不相關的 tooService 網狀架構叢集，您可以刪除特定的資源。

### <a name="delete-hello-resource-group-using-azure-powershell"></a>刪除使用 Azure PowerShell hello 資源群組
您也可以藉由執行下列 Azure PowerShell cmdlet 的 hello 刪除 hello 資源群組。 請確定您的電腦已安裝 Azure PowerShell 1.0 或更新版本。 如果您有不這麼做之前，請依照下列所述的 hello 步驟[如何 tooinstall 和設定 Azure PowerShell。](/powershell/azure/overview)

開啟 PowerShell 視窗並執行下列 PS 指令程式的 hello:

```powershell
Login-AzureRmAccount

Remove-AzureRmResourceGroup -Name <name of ResouceGroup> -Force
```

如果您未使用 hello，就會收到提示 tooconfirm hello 刪除*-Force*選項。 在確認上 hello RG，並刪除它所包含的所有 hello 資源。

### <a name="delete-a-resource-group-in-hello-azure-portal"></a>刪除資源群組中 hello Azure 入口網站
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 瀏覽您想 toodelete toohello Service Fabric 叢集。
3. 按一下 hello hello 叢集 essentials 頁面上的資源群組名稱。
4. 這會帶出 hello**資源群組 Essentials**頁面。
5. 按一下 [刪除] 。
6. 遵循 hello 指示該頁面 toocomplete hello 刪除 hello 資源群組。

![資源群組刪除][ResourceGroupDelete]

## <a name="delete-hello-cluster-resource-and-hello-resources-it-uses-but-not-other-resources-in-hello-resource-group"></a>刪除 hello 叢集資源和 hello 資源使用，但不是 hello 資源群組中的其他資源
如果您的資源群組具有相關的 toohello Service Fabric 叢集的資源想 toodelete，則它是更容易 toodelete hello 整個資源群組。 如果您想 tooselectively 刪除 hello 資源一個接著一個資源群組中，然後執行下列步驟。

如果您部署您的叢集使用 hello 入口網站或從 hello 範本庫使用其中一個 hello 服務網狀架構資源管理員範本，然後 hello 叢集使用的所有 hello 資源就會以下列兩個標記的 hello 都標記。 使用哪些資源要的 toodecide toodelete。

***標記 #1:***索引鍵 = clusterName，值 = 'hello 叢集的名稱'

Tag#2：索引鍵 = resourceName，值 = ServiceFabric

### <a name="delete-specific-resources-in-hello-azure-portal"></a>刪除 hello Azure 入口網站中的特定資源
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 瀏覽您想 toodelete toohello Service Fabric 叢集。
3. 跳過**所有設定**hello essentials 刀鋒視窗上。
4. 按一下**標記**下**資源管理**hello 設定 刀鋒視窗中。
5. 按一下其中一個 hello**標記**hello 標記刀鋒視窗 tooget 具有該標記的所有 hello 資源的清單中。
   
    ![資源標記][ResourceTags]
6. 一旦您擁有 hello 資源清單已加上標籤，按一下每個 hello 資源，然後予以刪除。
   
    ![已加上標記的資源][TaggedResources]

### <a name="delete-hello-resources-using-azure-powershell"></a>刪除 hello 資源使用 Azure PowerShell
您可以藉由執行下列 Azure PowerShell cmdlet 的 hello 刪除 hello 資源一一。 請確定您的電腦已安裝 Azure PowerShell 1.0 或更新版本。 如果您有不這麼做之前，請依照下列所述的 hello 步驟[如何 tooinstall 和設定 Azure PowerShell。](/powershell/azure/overview)

開啟 PowerShell 視窗並執行下列 PS 指令程式的 hello:

```powershell
Login-AzureRmAccount
```
Hello 資源的每個您想 toodelete，請執行下列 hello:

```powershell
Remove-AzureRmResource -ResourceName "<name of hello Resource>" -ResourceType "<Resource Type>" -ResourceGroupName "<name of hello resource group>" -Force
```

toodelete hello 叢集資源後，執行下列 hello:

```powershell
Remove-AzureRmResource -ResourceName "<name of hello Resource>" -ResourceType "Microsoft.ServiceFabric/clusters" -ResourceGroupName "<name of hello resource group>" -Force
```

## <a name="next-steps"></a>後續步驟
讀取 hello 遵循 tooalso 深入了解升級叢集和資料分割服務：

* [了解叢集升級](service-fabric-cluster-upgrade.md)
* [了解如何分割具狀態服務來達到最大規模](service-fabric-concepts-partitioning.md)

<!--Image references-->
[ResourceGroupDelete]: ./media/service-fabric-cluster-delete/ResourceGroupDelete.PNG

[ResourceTags]: ./media/service-fabric-cluster-delete/ResourceTags.png

[TaggedResources]: ./media/service-fabric-cluster-delete/TaggedResources.PNG
