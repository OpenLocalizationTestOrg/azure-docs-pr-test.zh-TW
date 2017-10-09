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
# <a name="delete-a-service-fabric-cluster-on-azure-and-hello-resources-it-uses"></a><span data-ttu-id="80a99-103">刪除 Azure 與 hello 的資源，它會使用 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="80a99-103">Delete a Service Fabric cluster on Azure and hello resources it uses</span></span>
<span data-ttu-id="80a99-104">Service Fabric 叢集所組成的許多其他 Azure 資源此外 toohello 叢集資源本身。</span><span class="sxs-lookup"><span data-stu-id="80a99-104">A Service Fabric cluster is made up of many other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="80a99-105">因此 toocompletely 刪除 Service Fabric 叢集，您也需要的 toodelete 所有 hello 則由的資源。</span><span class="sxs-lookup"><span data-stu-id="80a99-105">So toocompletely delete a Service Fabric cluster you also need toodelete all hello resources it is made of.</span></span>
<span data-ttu-id="80a99-106">有兩個選項： hello 叢集中任一個刪除 hello 資源群組處於 （這會刪除 hello 叢集資源和 hello 資源群組中的任何其他資源） 或明確刪除 hello 叢集資源，以及它有相關聯的資源 （但不是 其他資源 hello 資源群組中）。</span><span class="sxs-lookup"><span data-stu-id="80a99-106">You have two options: Either delete hello resource group that hello cluster is in (which deletes hello cluster resource and any other resources in hello resource group) or specifically delete hello cluster resource and it's associated resources (but not other resources in hello resource group).</span></span>

> [!NOTE]
> <span data-ttu-id="80a99-107">正在刪除 hello 叢集資源**不**刪除所有 hello 所組成的 Service Fabric 叢集的其他資源。</span><span class="sxs-lookup"><span data-stu-id="80a99-107">Deleting hello cluster resource **does not** delete all hello other resources that your Service Fabric cluster is composed of.</span></span>
> 
> 

## <a name="delete-hello-entire-resource-group-rg-that-hello-service-fabric-cluster-is-in"></a><span data-ttu-id="80a99-108">刪除 hello 整個資源群組 (RG) hello Service Fabric 叢集處於</span><span class="sxs-lookup"><span data-stu-id="80a99-108">Delete hello entire resource group (RG) that hello Service Fabric cluster is in</span></span>
<span data-ttu-id="80a99-109">這是 hello 您刪除所有與您的叢集，包括 hello 資源群組相關聯的 hello 資源最簡單方式 tooensure。</span><span class="sxs-lookup"><span data-stu-id="80a99-109">This is hello easiest way tooensure that you delete all hello resources associated with your cluster, including hello resource group.</span></span> <span data-ttu-id="80a99-110">您可以刪除 hello 資源群組使用 PowerShell 或透過 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="80a99-110">You can delete hello resource group using PowerShell or through hello Azure portal.</span></span> <span data-ttu-id="80a99-111">如果您的資源群組擁有的資源不相關的 tooService 網狀架構叢集，您可以刪除特定的資源。</span><span class="sxs-lookup"><span data-stu-id="80a99-111">If your resource group has resources that are not related tooService fabric cluster, then you can delete specific resources.</span></span>

### <a name="delete-hello-resource-group-using-azure-powershell"></a><span data-ttu-id="80a99-112">刪除使用 Azure PowerShell hello 資源群組</span><span class="sxs-lookup"><span data-stu-id="80a99-112">Delete hello resource group using Azure PowerShell</span></span>
<span data-ttu-id="80a99-113">您也可以藉由執行下列 Azure PowerShell cmdlet 的 hello 刪除 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="80a99-113">You can also delete hello resource group by running hello following Azure PowerShell cmdlets.</span></span> <span data-ttu-id="80a99-114">請確定您的電腦已安裝 Azure PowerShell 1.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="80a99-114">Make sure Azure PowerShell 1.0 or greater is installed on your computer.</span></span> <span data-ttu-id="80a99-115">如果您有不這麼做之前，請依照下列所述的 hello 步驟[如何 tooinstall 和設定 Azure PowerShell。](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="80a99-115">If you have not done this before, follow hello steps outlined in [How tooinstall and Configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="80a99-116">開啟 PowerShell 視窗並執行下列 PS 指令程式的 hello:</span><span class="sxs-lookup"><span data-stu-id="80a99-116">Open a PowerShell window and run hello following PS cmdlets:</span></span>

```powershell
Login-AzureRmAccount

Remove-AzureRmResourceGroup -Name <name of ResouceGroup> -Force
```

<span data-ttu-id="80a99-117">如果您未使用 hello，就會收到提示 tooconfirm hello 刪除*-Force*選項。</span><span class="sxs-lookup"><span data-stu-id="80a99-117">You will get a prompt tooconfirm hello deletion if you did not use hello *-Force* option.</span></span> <span data-ttu-id="80a99-118">在確認上 hello RG，並刪除它所包含的所有 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="80a99-118">On confirmation hello RG and all hello resources it contains are deleted.</span></span>

### <a name="delete-a-resource-group-in-hello-azure-portal"></a><span data-ttu-id="80a99-119">刪除資源群組中 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="80a99-119">Delete a resource group in hello Azure portal</span></span>
1. <span data-ttu-id="80a99-120">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="80a99-120">Login toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="80a99-121">瀏覽您想 toodelete toohello Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="80a99-121">Navigate toohello Service Fabric cluster you want toodelete.</span></span>
3. <span data-ttu-id="80a99-122">按一下 hello hello 叢集 essentials 頁面上的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="80a99-122">Click on hello Resource Group name on hello cluster essentials page.</span></span>
4. <span data-ttu-id="80a99-123">這會帶出 hello**資源群組 Essentials**頁面。</span><span class="sxs-lookup"><span data-stu-id="80a99-123">This brings up hello **Resource Group Essentials** page.</span></span>
5. <span data-ttu-id="80a99-124">按一下 [刪除] 。</span><span class="sxs-lookup"><span data-stu-id="80a99-124">Click **Delete**.</span></span>
6. <span data-ttu-id="80a99-125">遵循 hello 指示該頁面 toocomplete hello 刪除 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="80a99-125">Follow hello instructions on that page toocomplete hello deletion of hello resource group.</span></span>

![資源群組刪除][ResourceGroupDelete]

## <a name="delete-hello-cluster-resource-and-hello-resources-it-uses-but-not-other-resources-in-hello-resource-group"></a><span data-ttu-id="80a99-127">刪除 hello 叢集資源和 hello 資源使用，但不是 hello 資源群組中的其他資源</span><span class="sxs-lookup"><span data-stu-id="80a99-127">Delete hello cluster resource and hello resources it uses, but not other resources in hello resource group</span></span>
<span data-ttu-id="80a99-128">如果您的資源群組具有相關的 toohello Service Fabric 叢集的資源想 toodelete，則它是更容易 toodelete hello 整個資源群組。</span><span class="sxs-lookup"><span data-stu-id="80a99-128">If your resource group has only resources that are related toohello Service Fabric cluster you want toodelete, then it is easier toodelete hello entire resource group.</span></span> <span data-ttu-id="80a99-129">如果您想 tooselectively 刪除 hello 資源一個接著一個資源群組中，然後執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="80a99-129">If you want tooselectively delete hello resources one-by-one in your resource group, then follow these steps.</span></span>

<span data-ttu-id="80a99-130">如果您部署您的叢集使用 hello 入口網站或從 hello 範本庫使用其中一個 hello 服務網狀架構資源管理員範本，然後 hello 叢集使用的所有 hello 資源就會以下列兩個標記的 hello 都標記。</span><span class="sxs-lookup"><span data-stu-id="80a99-130">If you deployed your cluster using hello portal or using one of hello Service Fabric Resource Manager templates from hello template gallery, then all hello resources that hello cluster uses are tagged with hello following two tags.</span></span> <span data-ttu-id="80a99-131">使用哪些資源要的 toodecide toodelete。</span><span class="sxs-lookup"><span data-stu-id="80a99-131">You can use them toodecide which resources you want toodelete.</span></span>

<span data-ttu-id="80a99-132">***標記 #1:***索引鍵 = clusterName，值 = 'hello 叢集的名稱'</span><span class="sxs-lookup"><span data-stu-id="80a99-132">***Tag#1:*** Key = clusterName, Value = 'name of hello cluster'</span></span>

<span data-ttu-id="80a99-133">Tag#2：索引鍵 = resourceName，值 = ServiceFabric</span><span class="sxs-lookup"><span data-stu-id="80a99-133">***Tag#2:*** Key = resourceName, Value = ServiceFabric</span></span>

### <a name="delete-specific-resources-in-hello-azure-portal"></a><span data-ttu-id="80a99-134">刪除 hello Azure 入口網站中的特定資源</span><span class="sxs-lookup"><span data-stu-id="80a99-134">Delete specific resources in hello Azure portal</span></span>
1. <span data-ttu-id="80a99-135">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="80a99-135">Login toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="80a99-136">瀏覽您想 toodelete toohello Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="80a99-136">Navigate toohello Service Fabric cluster you want toodelete.</span></span>
3. <span data-ttu-id="80a99-137">跳過**所有設定**hello essentials 刀鋒視窗上。</span><span class="sxs-lookup"><span data-stu-id="80a99-137">Go too**All settings** on hello essentials blade.</span></span>
4. <span data-ttu-id="80a99-138">按一下**標記**下**資源管理**hello 設定 刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="80a99-138">Click on **Tags** under **Resource Management** in hello settings blade.</span></span>
5. <span data-ttu-id="80a99-139">按一下其中一個 hello**標記**hello 標記刀鋒視窗 tooget 具有該標記的所有 hello 資源的清單中。</span><span class="sxs-lookup"><span data-stu-id="80a99-139">Click on one of hello **Tags** in hello tags blade tooget a list of all hello resources with that tag.</span></span>
   
    ![資源標記][ResourceTags]
6. <span data-ttu-id="80a99-141">一旦您擁有 hello 資源清單已加上標籤，按一下每個 hello 資源，然後予以刪除。</span><span class="sxs-lookup"><span data-stu-id="80a99-141">Once you have hello list of tagged resources, click on each of hello resources and delete them.</span></span>
   
    ![已加上標記的資源][TaggedResources]

### <a name="delete-hello-resources-using-azure-powershell"></a><span data-ttu-id="80a99-143">刪除 hello 資源使用 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="80a99-143">Delete hello resources using Azure PowerShell</span></span>
<span data-ttu-id="80a99-144">您可以藉由執行下列 Azure PowerShell cmdlet 的 hello 刪除 hello 資源一一。</span><span class="sxs-lookup"><span data-stu-id="80a99-144">You can delete hello resources one-by-one by running hello following Azure PowerShell cmdlets.</span></span> <span data-ttu-id="80a99-145">請確定您的電腦已安裝 Azure PowerShell 1.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="80a99-145">Make sure Azure PowerShell 1.0 or greater is installed on your computer.</span></span> <span data-ttu-id="80a99-146">如果您有不這麼做之前，請依照下列所述的 hello 步驟[如何 tooinstall 和設定 Azure PowerShell。](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="80a99-146">If you have not done this before, follow hello steps outlined in [How tooinstall and Configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="80a99-147">開啟 PowerShell 視窗並執行下列 PS 指令程式的 hello:</span><span class="sxs-lookup"><span data-stu-id="80a99-147">Open a PowerShell window and run hello following PS cmdlets:</span></span>

```powershell
Login-AzureRmAccount
```
<span data-ttu-id="80a99-148">Hello 資源的每個您想 toodelete，請執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="80a99-148">For each of hello resources you want toodelete, run hello following:</span></span>

```powershell
Remove-AzureRmResource -ResourceName "<name of hello Resource>" -ResourceType "<Resource Type>" -ResourceGroupName "<name of hello resource group>" -Force
```

<span data-ttu-id="80a99-149">toodelete hello 叢集資源後，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="80a99-149">toodelete hello cluster resource, run hello following:</span></span>

```powershell
Remove-AzureRmResource -ResourceName "<name of hello Resource>" -ResourceType "Microsoft.ServiceFabric/clusters" -ResourceGroupName "<name of hello resource group>" -Force
```

## <a name="next-steps"></a><span data-ttu-id="80a99-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="80a99-150">Next steps</span></span>
<span data-ttu-id="80a99-151">讀取 hello 遵循 tooalso 深入了解升級叢集和資料分割服務：</span><span class="sxs-lookup"><span data-stu-id="80a99-151">Read hello following tooalso learn about upgrading a cluster and partitioning services:</span></span>

* [<span data-ttu-id="80a99-152">了解叢集升級</span><span class="sxs-lookup"><span data-stu-id="80a99-152">Learn about cluster upgrades</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="80a99-153">了解如何分割具狀態服務來達到最大規模</span><span class="sxs-lookup"><span data-stu-id="80a99-153">Learn about partitioning stateful services for maximum scale</span></span>](service-fabric-concepts-partitioning.md)

<!--Image references-->
[ResourceGroupDelete]: ./media/service-fabric-cluster-delete/ResourceGroupDelete.PNG

[ResourceTags]: ./media/service-fabric-cluster-delete/ResourceTags.png

[TaggedResources]: ./media/service-fabric-cluster-delete/TaggedResources.PNG
