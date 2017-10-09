---
title: "Service Fabric 應用程式的 aaaConfigure hello 升級 |Microsoft 文件"
description: "了解如何 tooconfigure hello 升級 Service Fabric 應用程式使用 Microsoft Visual Studio 的設定。"
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
ms.openlocfilehash: 8ca50aa9d911f3c98f017490c8fe29011e8d80cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-upgrade-of-a-service-fabric-application-in-visual-studio"></a><span data-ttu-id="c29fe-103">Service Fabric 應用程式的 hello 升級 Visual Studio 中設定</span><span class="sxs-lookup"><span data-stu-id="c29fe-103">Configure hello upgrade of a Service Fabric application in Visual Studio</span></span>
<span data-ttu-id="c29fe-104">Visual Studio tools for Azure Service Fabric 提供升級支援發行 toolocal 或遠端叢集。</span><span class="sxs-lookup"><span data-stu-id="c29fe-104">Visual Studio tools for Azure Service Fabric provide upgrade support for publishing toolocal or remote clusters.</span></span> <span data-ttu-id="c29fe-105">有三種情況，您想在其中 tooupgrade 您應用程式 tooa 較新版本而不是取代 hello 應用程式在測試和偵錯期間：</span><span class="sxs-lookup"><span data-stu-id="c29fe-105">There are three scenarios in which you want tooupgrade your application tooa newer version instead of replacing hello application during testing and debugging:</span></span>

* <span data-ttu-id="c29fe-106">應用程式資料 hello 升級期間將不會遺失。</span><span class="sxs-lookup"><span data-stu-id="c29fe-106">Application data won't be lost during hello upgrade.</span></span>
* <span data-ttu-id="c29fe-107">可用性維持高的所以將不會有任何服務中斷，hello 在升級期間，是否有足夠的服務執行個體分散到升級網域。</span><span class="sxs-lookup"><span data-stu-id="c29fe-107">Availability remains high so there won't be any service interruption during hello upgrade, if there are enough service instances spread across upgrade domains.</span></span>
* <span data-ttu-id="c29fe-108">在應用程式進行升級時，可以對該應用程式進行測試。</span><span class="sxs-lookup"><span data-stu-id="c29fe-108">Tests can be run against an application while it's being upgraded.</span></span>

## <a name="parameters-needed-tooupgrade"></a><span data-ttu-id="c29fe-109">需要 tooupgrade 參數。</span><span class="sxs-lookup"><span data-stu-id="c29fe-109">Parameters needed tooupgrade</span></span>
<span data-ttu-id="c29fe-110">您可以選擇的部署類型有兩種：一般或升級。</span><span class="sxs-lookup"><span data-stu-id="c29fe-110">You can choose from two types of deployment: regular or upgrade.</span></span> <span data-ttu-id="c29fe-111">標準的部署會清除任何先前的部署資訊和 hello 叢集上的資料，同時升級部署會保留它。</span><span class="sxs-lookup"><span data-stu-id="c29fe-111">A regular deployment erases any previous deployment information and data on hello cluster, while an upgrade deployment preserves it.</span></span> <span data-ttu-id="c29fe-112">當您升級 Visual Studio 中的 Service Fabric 應用程式時，您需要 tooprovide 應用程式升級參數和健全狀況檢查原則。</span><span class="sxs-lookup"><span data-stu-id="c29fe-112">When you upgrade a Service Fabric application in Visual Studio, you need tooprovide application upgrade parameters and health check policies.</span></span> <span data-ttu-id="c29fe-113">說明參數的應用程式升級控制項 hello 升級，而健康情況檢查原則可讓您判斷 hello 升級是否成功。</span><span class="sxs-lookup"><span data-stu-id="c29fe-113">Application upgrade parameters help control hello upgrade, while health check policies determine whether hello upgrade was successful.</span></span> <span data-ttu-id="c29fe-114">如需詳細資訊，請參閱 [Service Fabric 應用程式升級：升級參數](service-fabric-application-upgrade-parameters.md) 。</span><span class="sxs-lookup"><span data-stu-id="c29fe-114">See [Service Fabric application upgrade: upgrade parameters](service-fabric-application-upgrade-parameters.md) for more details.</span></span>

<span data-ttu-id="c29fe-115">有三種升級模式：Monitored、UnmonitoredAuto 及 UnmonitoredManual。</span><span class="sxs-lookup"><span data-stu-id="c29fe-115">There are three upgrade modes: *Monitored*, *UnmonitoredAuto*, and *UnmonitoredManual*.</span></span>

* <span data-ttu-id="c29fe-116">監視升級會自動執行 hello 升級應用程式健全狀況檢查。</span><span class="sxs-lookup"><span data-stu-id="c29fe-116">A Monitored upgrade automates hello upgrade and application health check.</span></span>
* <span data-ttu-id="c29fe-117">UnmonitoredAuto 升級自動化 hello 升級，但略過 hello 應用程式健全狀況檢查。</span><span class="sxs-lookup"><span data-stu-id="c29fe-117">An UnmonitoredAuto upgrade automates hello upgrade, but skips hello application health check.</span></span>
* <span data-ttu-id="c29fe-118">當您進行 UnmonitoredManual 升級時，您需要 toomanually 升級每個升級網域。</span><span class="sxs-lookup"><span data-stu-id="c29fe-118">When you do an UnmonitoredManual upgrade, you need toomanually upgrade each upgrade domain.</span></span>

<span data-ttu-id="c29fe-119">每一種升級模式都需要一組不同的參數。</span><span class="sxs-lookup"><span data-stu-id="c29fe-119">Each upgrade mode requires different sets of parameters.</span></span> <span data-ttu-id="c29fe-120">請參閱[應用程式升級參數](service-fabric-application-upgrade-parameters.md)toolearn 更多關於 hello 可用的升級選項。</span><span class="sxs-lookup"><span data-stu-id="c29fe-120">See [Application upgrade parameters](service-fabric-application-upgrade-parameters.md) toolearn more about hello available upgrade options.</span></span>

## <a name="upgrade-a-service-fabric-application-in-visual-studio"></a><span data-ttu-id="c29fe-121">在 Visual Studio 中升級 Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="c29fe-121">Upgrade a Service Fabric application in Visual Studio</span></span>
<span data-ttu-id="c29fe-122">如果您使用 hello Visual Studio Service Fabric 工具 tooupgrade Service Fabric 應用程式，您可以指定發佈程序 toobe 升級，而不是標準的部署方式是檢查 hello **hello 應用程式升級**檢查方塊。</span><span class="sxs-lookup"><span data-stu-id="c29fe-122">If you’re using hello Visual Studio Service Fabric tools tooupgrade a Service Fabric application, you can specify a publish process toobe an upgrade rather than a regular deployment by checking hello **Upgrade hello application** check box.</span></span>

### <a name="tooconfigure-hello-upgrade-parameters"></a><span data-ttu-id="c29fe-123">tooconfigure hello 升級參數</span><span class="sxs-lookup"><span data-stu-id="c29fe-123">tooconfigure hello upgrade parameters</span></span>
1. <span data-ttu-id="c29fe-124">按一下 hello**設定**按鈕下一步 toohello 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="c29fe-124">Click hello **Settings** button next toohello check box.</span></span> <span data-ttu-id="c29fe-125">hello**編輯升級參數** 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="c29fe-125">hello **Edit Upgrade Parameters** dialog box appears.</span></span> <span data-ttu-id="c29fe-126">hello**編輯升級參數**對話方塊支援 hello 監視、 UnmonitoredAuto 和 UnmonitoredManual 升級模式。</span><span class="sxs-lookup"><span data-stu-id="c29fe-126">hello **Edit Upgrade Parameters** dialog box supports hello Monitored, UnmonitoredAuto, and UnmonitoredManual upgrade modes.</span></span>
2. <span data-ttu-id="c29fe-127">選取您想 toouse，然後填寫 hello 參數方格 hello 升級模式。</span><span class="sxs-lookup"><span data-stu-id="c29fe-127">Select hello upgrade mode that you want toouse and then fill out hello parameter grid.</span></span>

    <span data-ttu-id="c29fe-128">每個參數都有預設值。</span><span class="sxs-lookup"><span data-stu-id="c29fe-128">Each parameter has default values.</span></span> <span data-ttu-id="c29fe-129">hello 選擇性參數*DefaultServiceTypeHealthPolicy*接受輸入雜湊資料表。</span><span class="sxs-lookup"><span data-stu-id="c29fe-129">hello optional parameter *DefaultServiceTypeHealthPolicy* takes a hash table input.</span></span> <span data-ttu-id="c29fe-130">以下是範例的 hello 雜湊資料表輸入格式*DefaultServiceTypeHealthPolicy*:</span><span class="sxs-lookup"><span data-stu-id="c29fe-130">Here’s an example of hello hash table input format for *DefaultServiceTypeHealthPolicy*:</span></span>

    ```
    @{ ConsiderWarningAsError = "false"; MaxPercentUnhealthyDeployedApplications = 0; MaxPercentUnhealthyServices = 0; MaxPercentUnhealthyPartitionsPerService = 0; MaxPercentUnhealthyReplicasPerPartition = 0 }
    ```

    <span data-ttu-id="c29fe-131">*ServiceTypeHealthPolicyMap*在 hello 會採用雜湊資料表輸入另一個選擇性參數是下列格式：</span><span class="sxs-lookup"><span data-stu-id="c29fe-131">*ServiceTypeHealthPolicyMap* is another optional parameter that takes a hash table input in hello following format:</span></span>

    ```    
    @ {"ServiceTypeName" : "MaxPercentUnhealthyPartitionsPerService,MaxPercentUnhealthyReplicasPerPartition,MaxPercentUnhealthyServices"}
    ```

    <span data-ttu-id="c29fe-132">以下是一個真實範例：</span><span class="sxs-lookup"><span data-stu-id="c29fe-132">Here's a real-life example:</span></span>

    ```
    @{ "ServiceTypeName01" = "5,10,5"; "ServiceTypeName02" = "5,5,5" }
    ```
3. <span data-ttu-id="c29fe-133">如果您選取 UnmonitoredManual 升級模式，您必須手動啟動 PowerShell 主控台 toocontinue 並完成 hello 升級程序。</span><span class="sxs-lookup"><span data-stu-id="c29fe-133">If you select UnmonitoredManual upgrade mode, you must manually start a PowerShell console toocontinue and finish hello upgrade process.</span></span> <span data-ttu-id="c29fe-134">請參閱太[Service Fabric 應用程式升級： 進階主題](service-fabric-application-upgrade-advanced.md)toolearn 如何手動升級運作方式。</span><span class="sxs-lookup"><span data-stu-id="c29fe-134">Refer too[Service Fabric application upgrade: advanced topics](service-fabric-application-upgrade-advanced.md) toolearn how manual upgrade works.</span></span>

## <a name="upgrade-an-application-by-using-powershell"></a><span data-ttu-id="c29fe-135">使用 PowerShell 升級應用程式</span><span class="sxs-lookup"><span data-stu-id="c29fe-135">Upgrade an application by using PowerShell</span></span>
<span data-ttu-id="c29fe-136">您可以使用 PowerShell cmdlet tooupgrade Service Fabric 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c29fe-136">You can use PowerShell cmdlets tooupgrade a Service Fabric application.</span></span> <span data-ttu-id="c29fe-137">如需詳細資訊，請參閱 [Service Fabric 應用程式升級教學課程](service-fabric-application-upgrade-tutorial.md)和 [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c29fe-137">See [Service Fabric application upgrade tutorial](service-fabric-application-upgrade-tutorial.md) and [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx) for detailed information.</span></span>

## <a name="specify-a-health-check-policy-in-hello-application-manifest-file"></a><span data-ttu-id="c29fe-138">Hello 應用程式資訊清單檔中指定的健全狀況檢查原則</span><span class="sxs-lookup"><span data-stu-id="c29fe-138">Specify a health check policy in hello application manifest file</span></span>
<span data-ttu-id="c29fe-139">Service Fabric 應用程式中的每個服務可以有其本身的健全狀況原則參數，覆寫 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="c29fe-139">Every service in a Service Fabric application can have its own health policy parameters that override hello default values.</span></span> <span data-ttu-id="c29fe-140">您可以提供這些 hello 應用程式資訊清單檔中的參數值。</span><span class="sxs-lookup"><span data-stu-id="c29fe-140">You can provide these parameter values in hello application manifest file.</span></span>

<span data-ttu-id="c29fe-141">hello 下列範例顯示如何 tooapply 唯一的健全狀況檢查 hello 應用程式資訊清單中的每個服務的原則。</span><span class="sxs-lookup"><span data-stu-id="c29fe-141">hello following example shows how tooapply a unique health check policy for each service in hello application manifest.</span></span>

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
## <a name="next-steps"></a><span data-ttu-id="c29fe-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c29fe-142">Next steps</span></span>
<span data-ttu-id="c29fe-143">如需有關部署應用程式的詳細資訊，請參閱 [在 Azure Service Fabric 中部署現有的應用程式](service-fabric-deploy-existing-app.md)。</span><span class="sxs-lookup"><span data-stu-id="c29fe-143">For more information about deploying an application, see [Deploy an existing application in Azure Service Fabric](service-fabric-deploy-existing-app.md).</span></span>