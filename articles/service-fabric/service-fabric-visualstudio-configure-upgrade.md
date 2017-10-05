---
title: "設定 Service Fabric 應用程式的升級 | Microsoft Docs"
description: "了解如何使用 Microsoft Visual Studio 來設定升級 Service Fabric 應用程式的設定。"
services: service-fabric
documentationcenter: na
author: mikkelhegn
manager: mfussell
editor: tglee
ms.assetid: 1757ba85-0b7b-4f16-8a23-2ddaa61c86c6
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/29/2017
ms.author: mikkelhegn
ms.openlocfilehash: 314b29a56e4651222822f40a116af97a7372ff2c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-the-upgrade-of-a-service-fabric-application-in-visual-studio"></a><span data-ttu-id="225c3-103">在 Visual Studio 中設定 Service Fabric 應用程式的升級</span><span class="sxs-lookup"><span data-stu-id="225c3-103">Configure the upgrade of a Service Fabric application in Visual Studio</span></span>
<span data-ttu-id="225c3-104">Azure Service Fabric 的 Visual Studio 工具提供發佈至本機或遠端叢集的升級支援。</span><span class="sxs-lookup"><span data-stu-id="225c3-104">Visual Studio tools for Azure Service Fabric provide upgrade support for publishing to local or remote clusters.</span></span> <span data-ttu-id="225c3-105">在進行測試和偵錯時，有三種情況您會想要將應用程式升級成較新的版本，而不是取代應用程式：</span><span class="sxs-lookup"><span data-stu-id="225c3-105">There are three scenarios in which you want to upgrade your application to a newer version instead of replacing the application during testing and debugging:</span></span>

* <span data-ttu-id="225c3-106">應用程式資料不會在升級期間遺失。</span><span class="sxs-lookup"><span data-stu-id="225c3-106">Application data won't be lost during the upgrade.</span></span>
* <span data-ttu-id="225c3-107">可用性仍然很高，因此，如果有足夠的服務執行個體分散到升級網域，則在升級期間不會有任何服務中斷。</span><span class="sxs-lookup"><span data-stu-id="225c3-107">Availability remains high so there won't be any service interruption during the upgrade, if there are enough service instances spread across upgrade domains.</span></span>
* <span data-ttu-id="225c3-108">在應用程式進行升級時，可以對該應用程式進行測試。</span><span class="sxs-lookup"><span data-stu-id="225c3-108">Tests can be run against an application while it's being upgraded.</span></span>

## <a name="parameters-needed-to-upgrade"></a><span data-ttu-id="225c3-109">升級所需的參數</span><span class="sxs-lookup"><span data-stu-id="225c3-109">Parameters needed to upgrade</span></span>
<span data-ttu-id="225c3-110">您可以選擇的部署類型有兩種：一般或升級。</span><span class="sxs-lookup"><span data-stu-id="225c3-110">You can choose from two types of deployment: regular or upgrade.</span></span> <span data-ttu-id="225c3-111">一般部署會將叢集上所有先前的部署資訊和資料都清除，而升級部署則會將其保留。</span><span class="sxs-lookup"><span data-stu-id="225c3-111">A regular deployment erases any previous deployment information and data on the cluster, while an upgrade deployment preserves it.</span></span> <span data-ttu-id="225c3-112">當您在 Visual Studio 中升級 Service Fabric 應用程式時，您需要提供應用程式升級參數和健康情況檢查原則。</span><span class="sxs-lookup"><span data-stu-id="225c3-112">When you upgrade a Service Fabric application in Visual Studio, you need to provide application upgrade parameters and health check policies.</span></span> <span data-ttu-id="225c3-113">應用程式升級參數可協助控制升級，而健康狀態檢查原則則可判斷升級是否成功。</span><span class="sxs-lookup"><span data-stu-id="225c3-113">Application upgrade parameters help control the upgrade, while health check policies determine whether the upgrade was successful.</span></span> <span data-ttu-id="225c3-114">如需詳細資訊，請參閱 [Service Fabric 應用程式升級：升級參數](service-fabric-application-upgrade-parameters.md) 。</span><span class="sxs-lookup"><span data-stu-id="225c3-114">See [Service Fabric application upgrade: upgrade parameters](service-fabric-application-upgrade-parameters.md) for more details.</span></span>

<span data-ttu-id="225c3-115">有三種升級模式：Monitored、UnmonitoredAuto 及 UnmonitoredManual。</span><span class="sxs-lookup"><span data-stu-id="225c3-115">There are three upgrade modes: *Monitored*, *UnmonitoredAuto*, and *UnmonitoredManual*.</span></span>

* <span data-ttu-id="225c3-116">Monitored 升級會自動進行升級和應用程式健康狀態檢查。</span><span class="sxs-lookup"><span data-stu-id="225c3-116">A Monitored upgrade automates the upgrade and application health check.</span></span>
* <span data-ttu-id="225c3-117">UnmonitoredAuto 升級會自動進行升級，但會略過應用程式健康狀態檢查。</span><span class="sxs-lookup"><span data-stu-id="225c3-117">An UnmonitoredAuto upgrade automates the upgrade, but skips the application health check.</span></span>
* <span data-ttu-id="225c3-118">執行 UnmonitoredManual 升級時，您必須手動升級每個升級網域。</span><span class="sxs-lookup"><span data-stu-id="225c3-118">When you do an UnmonitoredManual upgrade, you need to manually upgrade each upgrade domain.</span></span>

<span data-ttu-id="225c3-119">每一種升級模式都需要一組不同的參數。</span><span class="sxs-lookup"><span data-stu-id="225c3-119">Each upgrade mode requires different sets of parameters.</span></span> <span data-ttu-id="225c3-120">若要深入了解可用的升級選項，請參閱 [應用程式升級參數](service-fabric-application-upgrade-parameters.md) 。</span><span class="sxs-lookup"><span data-stu-id="225c3-120">See [Application upgrade parameters](service-fabric-application-upgrade-parameters.md) to learn more about the available upgrade options.</span></span>

## <a name="upgrade-a-service-fabric-application-in-visual-studio"></a><span data-ttu-id="225c3-121">在 Visual Studio 中升級 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="225c3-121">Upgrade a Service Fabric application in Visual Studio</span></span>
<span data-ttu-id="225c3-122">如果您要使用 Visual Studio Service Fabric 工具升級 Service Fabric 應用程式，則您可以核取 [升級應用程式]  核取方塊，將發佈程序指定為升級而非一般部署。</span><span class="sxs-lookup"><span data-stu-id="225c3-122">If you’re using the Visual Studio Service Fabric tools to upgrade a Service Fabric application, you can specify a publish process to be an upgrade rather than a regular deployment by checking the **Upgrade the application** check box.</span></span>

### <a name="to-configure-the-upgrade-parameters"></a><span data-ttu-id="225c3-123">設定升級參數</span><span class="sxs-lookup"><span data-stu-id="225c3-123">To configure the upgrade parameters</span></span>
1. <span data-ttu-id="225c3-124">按一下核取方塊旁邊的 [設定]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="225c3-124">Click the **Settings** button next to the check box.</span></span> <span data-ttu-id="225c3-125">將會顯示 [編輯升級參數]  對話方塊。</span><span class="sxs-lookup"><span data-stu-id="225c3-125">The **Edit Upgrade Parameters** dialog box appears.</span></span> <span data-ttu-id="225c3-126">[編輯升級參數]  對話方塊支援 Monitored、UnmonitoredAuto 及 UnmonitoredManual 升級模式。</span><span class="sxs-lookup"><span data-stu-id="225c3-126">The **Edit Upgrade Parameters** dialog box supports the Monitored, UnmonitoredAuto, and UnmonitoredManual upgrade modes.</span></span>
2. <span data-ttu-id="225c3-127">選取您想要使用的升級模式，然後填寫參數方格。</span><span class="sxs-lookup"><span data-stu-id="225c3-127">Select the upgrade mode that you want to use and then fill out the parameter grid.</span></span>

    <span data-ttu-id="225c3-128">每個參數都有預設值。</span><span class="sxs-lookup"><span data-stu-id="225c3-128">Each parameter has default values.</span></span> <span data-ttu-id="225c3-129">選用參數 *DefaultServiceTypeHealthPolicy* 會接受雜湊表輸入。</span><span class="sxs-lookup"><span data-stu-id="225c3-129">The optional parameter *DefaultServiceTypeHealthPolicy* takes a hash table input.</span></span> <span data-ttu-id="225c3-130">以下是 *DefaultServiceTypeHealthPolicy*的雜湊表輸入格式範例：</span><span class="sxs-lookup"><span data-stu-id="225c3-130">Here’s an example of the hash table input format for *DefaultServiceTypeHealthPolicy*:</span></span>

    ```
    @{ ConsiderWarningAsError = "false"; MaxPercentUnhealthyDeployedApplications = 0; MaxPercentUnhealthyServices = 0; MaxPercentUnhealthyPartitionsPerService = 0; MaxPercentUnhealthyReplicasPerPartition = 0 }
    ```

    <span data-ttu-id="225c3-131">*ServiceTypeHealthPolicyMap* 是另一個會接受雜湊表輸入 (格式如下) 的選擇性參數：</span><span class="sxs-lookup"><span data-stu-id="225c3-131">*ServiceTypeHealthPolicyMap* is another optional parameter that takes a hash table input in the following format:</span></span>

    ```    
    @ {"ServiceTypeName" : "MaxPercentUnhealthyPartitionsPerService,MaxPercentUnhealthyReplicasPerPartition,MaxPercentUnhealthyServices"}
    ```

    <span data-ttu-id="225c3-132">以下是一個真實範例：</span><span class="sxs-lookup"><span data-stu-id="225c3-132">Here's a real-life example:</span></span>

    ```
    @{ "ServiceTypeName01" = "5,10,5"; "ServiceTypeName02" = "5,5,5" }
    ```
3. <span data-ttu-id="225c3-133">如果您選取 UnmonitoredManual 升級模式，您必須手動啟動 PowerShell 主控台，才能繼續並完成升級程序。</span><span class="sxs-lookup"><span data-stu-id="225c3-133">If you select UnmonitoredManual upgrade mode, you must manually start a PowerShell console to continue and finish the upgrade process.</span></span> <span data-ttu-id="225c3-134">若要了解手動升級如何運作，請參閱 [Service Fabric 應用程式升級：進階主題](service-fabric-application-upgrade-advanced.md) 。</span><span class="sxs-lookup"><span data-stu-id="225c3-134">Refer to [Service Fabric application upgrade: advanced topics](service-fabric-application-upgrade-advanced.md) to learn how manual upgrade works.</span></span>

## <a name="upgrade-an-application-by-using-powershell"></a><span data-ttu-id="225c3-135">使用 PowerShell 升級應用程式</span><span class="sxs-lookup"><span data-stu-id="225c3-135">Upgrade an application by using PowerShell</span></span>
<span data-ttu-id="225c3-136">您可以使用 PowerShell Cmdlet 來升級 Service Fabric 應用程式。</span><span class="sxs-lookup"><span data-stu-id="225c3-136">You can use PowerShell cmdlets to upgrade a Service Fabric application.</span></span> <span data-ttu-id="225c3-137">如需詳細資訊，請參閱 [Service Fabric 應用程式升級教學課程](service-fabric-application-upgrade-tutorial.md)和 [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx)。</span><span class="sxs-lookup"><span data-stu-id="225c3-137">See [Service Fabric application upgrade tutorial](service-fabric-application-upgrade-tutorial.md) and [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx) for detailed information.</span></span>

## <a name="specify-a-health-check-policy-in-the-application-manifest-file"></a><span data-ttu-id="225c3-138">在應用程式資訊清單檔案中指定健康情況狀態檢查原則</span><span class="sxs-lookup"><span data-stu-id="225c3-138">Specify a health check policy in the application manifest file</span></span>
<span data-ttu-id="225c3-139">Service Fabric 應用程式中的每個服務都可以有自己的健康情況原則參數來覆寫預設值。</span><span class="sxs-lookup"><span data-stu-id="225c3-139">Every service in a Service Fabric application can have its own health policy parameters that override the default values.</span></span> <span data-ttu-id="225c3-140">您可以在應用程式資訊清單檔案中提供這些參數值。</span><span class="sxs-lookup"><span data-stu-id="225c3-140">You can provide these parameter values in the application manifest file.</span></span>

<span data-ttu-id="225c3-141">下列範例示範如何在應用程式清單中套用每個服務的唯一健康情況檢查原則。</span><span class="sxs-lookup"><span data-stu-id="225c3-141">The following example shows how to apply a unique health check policy for each service in the application manifest.</span></span>

```xml
<Policies>
    <HealthPolicy ConsiderWarningAsError="false" MaxPercentUnhealthyDeployedApplications="20">
        <DefaultServiceTypeHealthPolicy MaxPercentUnhealthyServices="20"               
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />
        <ServiceTypeHealthPolicy ServiceTypeName="ServiceTypeName1"
                MaxPercentUnhealthyServices="20"
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />      
    </HealthPolicy>
</Policies>
```
## <a name="next-steps"></a><span data-ttu-id="225c3-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="225c3-142">Next steps</span></span>
<span data-ttu-id="225c3-143">如需有關部署應用程式的詳細資訊，請參閱 [在 Azure Service Fabric 中部署現有的應用程式](service-fabric-deploy-existing-app.md)。</span><span class="sxs-lookup"><span data-stu-id="225c3-143">For more information about deploying an application, see [Deploy an existing application in Azure Service Fabric](service-fabric-deploy-existing-app.md).</span></span>