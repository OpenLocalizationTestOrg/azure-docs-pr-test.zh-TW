---
title: "aaaAutoscale HPC Pack 叢集節點 |Microsoft 文件"
description: "自動擴增和縮減 HPC Pack 叢集計算節點，在 Azure 中的 hello 數目"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: 
editor: tysonn
ms.assetid: 38762cd1-f917-464c-ae5d-b02b1eb21e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/08/2016
ms.author: danlep
ms.openlocfilehash: 0bdf55625d337a2bbfe05677682d645a584798d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-grow-and-shrink-hello-hpc-pack-cluster-resources-in-azure-according-toohello-cluster-workload"></a><span data-ttu-id="5333c-103">自動擴增和縮減 Azure 根據 toohello 叢集工作負載中的 hello HPC Pack 叢集資源</span><span class="sxs-lookup"><span data-stu-id="5333c-103">Automatically grow and shrink hello HPC Pack cluster resources in Azure according toohello cluster workload</span></span>
<span data-ttu-id="5333c-104">如果您在 HPC Pack 叢集中部署 Azure 「 高載 」 節點，或您建立 Azure Vm 中的 HPC Pack 叢集，您可以自動成長或壓縮 hello 叢集資源，例如節點或核心根據 hello hello 叢集上的工作負載的方式。</span><span class="sxs-lookup"><span data-stu-id="5333c-104">If you deploy Azure “burst” nodes in your HPC Pack cluster, or you create an HPC Pack cluster in Azure VMs, you may want a way to automatically grow or shrink hello cluster resources such as nodes or cores according to hello workload on hello cluster.</span></span> <span data-ttu-id="5333c-105">以這種方式調整 hello 叢集資源可讓您 toouse 您的 Azure 資源更有效率地並控制其成本。</span><span class="sxs-lookup"><span data-stu-id="5333c-105">Scaling hello cluster resources in this way allows you toouse your Azure resources more efficiently and control their costs.</span></span>

<span data-ttu-id="5333c-106">本文將說明 HPC Pack 提供 tooautoscale 計算資源的兩種方式：</span><span class="sxs-lookup"><span data-stu-id="5333c-106">This article shows you two ways that HPC Pack provides tooautoscale compute resources:</span></span>

* <span data-ttu-id="5333c-107">hello HPC Pack 叢集屬性**AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="5333c-107">hello HPC Pack cluster property **AutoGrowShrink**</span></span>

* <span data-ttu-id="5333c-108">hello **AzureAutoGrowShrink.ps1** HPC PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="5333c-108">hello **AzureAutoGrowShrink.ps1** HPC PowerShell script</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="5333c-109">目前您只能自動擴增和縮減正在執行 Windows Server 作業系統的 HPC Pack 計算節點。</span><span class="sxs-lookup"><span data-stu-id="5333c-109">Currently you can only automatically grow and shrink HPC Pack compute nodes that are running a Windows Server operating system.</span></span>


## <a name="set-hello-autogrowshrink-cluster-property"></a><span data-ttu-id="5333c-110">設定 hello AutoGrowShrink 叢集屬性</span><span class="sxs-lookup"><span data-stu-id="5333c-110">Set hello AutoGrowShrink cluster property</span></span>
### <a name="prerequisites"></a><span data-ttu-id="5333c-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="5333c-111">Prerequisites</span></span>

* <span data-ttu-id="5333c-112">**HPC Pack 2012 R2 更新 2 或更新版本的叢集**-hello 叢集前端節點可以是部署在內部或 Azure VM 中。</span><span class="sxs-lookup"><span data-stu-id="5333c-112">**HPC Pack 2012 R2 Update 2 or later cluster** - hello cluster head node can be deployed either on-premises or in an Azure VM.</span></span> <span data-ttu-id="5333c-113">請參閱[設定混合式叢集使用 HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget 啟動內部部署前端節點與 Azure 「 高載 」 節點。</span><span class="sxs-lookup"><span data-stu-id="5333c-113">See [Set up a hybrid cluster with HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget started with an on-premises head node and Azure "burst" nodes.</span></span> <span data-ttu-id="5333c-114">請參閱 hello [HPC Pack IaaS 部署指令碼](hpcpack-cluster-powershell-script.md)tooquickly HPC Pack 叢集部署在 Azure Vm。</span><span class="sxs-lookup"><span data-stu-id="5333c-114">See hello [HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md) tooquickly deploy an HPC Pack cluster in Azure VMs.</span></span>

* <span data-ttu-id="5333c-115">**針對在 Azure (Resource Manager 部署模型) 中具有前端節點的叢集** - 從 HPC Pack 2016 開始，Azure Active Directory 應用程式中的憑證驗證會用於自動增加或縮減利用 Azure Resource Manager 部署的叢集 VM。</span><span class="sxs-lookup"><span data-stu-id="5333c-115">**For a cluster with a head node in Azure (Resource Manager deployment model)** - Starting in HPC Pack 2016, certificate authentication in an Azure Active Directory application is used for automatically growing and shrinking cluster VMs deployed using Azure Resource Manager.</span></span> <span data-ttu-id="5333c-116">設定憑證，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="5333c-116">Configure a certificate as follows:</span></span>

  1. <span data-ttu-id="5333c-117">叢集部署之後，連線的遠端桌面 tooone 前端節點。</span><span class="sxs-lookup"><span data-stu-id="5333c-117">After cluster deployment, connect by Remote Desktop tooone head node.</span></span>

  2. <span data-ttu-id="5333c-118">上傳 hello 憑證 （具有私密金鑰的 PFX 格式） tooeach 前端節點，並安裝 tooCert:\LocalMachine\My 和 Cert: \LocalMachine\Root。</span><span class="sxs-lookup"><span data-stu-id="5333c-118">Upload hello certificate (PFX format with private key) tooeach head node and install tooCert:\LocalMachine\My and Cert:\LocalMachine\Root.</span></span>

  3. <span data-ttu-id="5333c-119">系統管理員身分啟動 Azure PowerShell，然後執行下列命令，其中一個前端節點上的 hello:</span><span class="sxs-lookup"><span data-stu-id="5333c-119">Start Azure PowerShell as an administrator and run hello following commands on one head node:</span></span>

    ```powershell
        cd $env:CCP_HOME\bin

        Login-AzureRmAccount
    ```
        
    <span data-ttu-id="5333c-120">如果您的帳戶是在多個 Azure Active Directory 租用戶或 Azure 訂用帳戶，您可以執行下列 hello 命令 tooselect hello 正確租用戶和訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="5333c-120">If your account is in more than one Azure Active Directory tenant or Azure subscription, you can run hello following command tooselect hello correct tenant and subscription:</span></span>
  
    ```powershell
        Login-AzureRMAccount -TenantId <TenantId> -SubscriptionId <subscriptionId>
    ```     
       
    <span data-ttu-id="5333c-121">執行下列命令 tooview hello hello 目前已選取租用戶和訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="5333c-121">Run hello following command tooview hello currently selected tenant and subscription:</span></span>
    
    ```powershell
        Get-AzureRMContext
    ```

  4. <span data-ttu-id="5333c-122">執行下列指令碼的 hello</span><span class="sxs-lookup"><span data-stu-id="5333c-122">Run hello following script</span></span>

    ```powershell
        .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -CertificateThumbprint "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX" -TenantId xxxxxxxx-xxxxx-xxxxx-xxxxx-xxxxxxxxxxxx
    ```

    <span data-ttu-id="5333c-123">其中</span><span class="sxs-lookup"><span data-stu-id="5333c-123">where</span></span>

    <span data-ttu-id="5333c-124">**DisplayName** - Azure Active 應用程式顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="5333c-124">**DisplayName** - Azure Active Application display name.</span></span> <span data-ttu-id="5333c-125">如果 hello 應用程式不存在，它會建立 Azure Active Directory 中。</span><span class="sxs-lookup"><span data-stu-id="5333c-125">If hello application does not exist, it is created in Azure Active Directory.</span></span>

    <span data-ttu-id="5333c-126">**首頁**-hello hello 應用程式的首頁。</span><span class="sxs-lookup"><span data-stu-id="5333c-126">**HomePage** - hello home page of hello application.</span></span> <span data-ttu-id="5333c-127">您可以設定空的 URL，如 hello 前面範例所示。</span><span class="sxs-lookup"><span data-stu-id="5333c-127">You can configure a dummy URL, as in hello preceding example.</span></span>

    <span data-ttu-id="5333c-128">**IdentifierUri** -hello 應用程式識別項。</span><span class="sxs-lookup"><span data-stu-id="5333c-128">**IdentifierUri** - Identifier of hello application.</span></span> <span data-ttu-id="5333c-129">您可以設定空的 URL，如 hello 前面範例所示。</span><span class="sxs-lookup"><span data-stu-id="5333c-129">You can configure a dummy URL, as in hello preceding example.</span></span>

    <span data-ttu-id="5333c-130">**CertificateThumbprint** -您在步驟 1 中的 hello 前端節點安裝的 hello 憑證的指紋。</span><span class="sxs-lookup"><span data-stu-id="5333c-130">**CertificateThumbprint** - Thumbprint of hello certificate you installed on hello head node in Step 1.</span></span>

    <span data-ttu-id="5333c-131">**TenantId** - Azure Active Directory 的租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="5333c-131">**TenantId** - Tenant ID of your Azure Active Directory.</span></span> <span data-ttu-id="5333c-132">您可以從 hello Azure Active Directory 入口網站取得租用戶識別碼 hello**屬性**頁面。</span><span class="sxs-lookup"><span data-stu-id="5333c-132">You can get hello Tenant ID from hello Azure Active Directory portal **Properties** page.</span></span>

    <span data-ttu-id="5333c-133">如需 **ConfigARMAutoGrowShrinkCert.ps1** 的詳細資訊，請執行 `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`。</span><span class="sxs-lookup"><span data-stu-id="5333c-133">For more details about **ConfigARMAutoGrowShrinkCert.ps1**, run `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.</span></span>


* <span data-ttu-id="5333c-134">**針對在 Azure （傳統部署模型） 中的前端節點的叢集**-如果您使用 hello HPC Pack IaaS 部署指令碼 toocreate hello 叢集在 hello 傳統部署模型中，啟用 hello **AutoGrowShrink**叢集藉由設定 hello 叢集組態檔中的 hello AutoGrowShrink 選項屬性。</span><span class="sxs-lookup"><span data-stu-id="5333c-134">**For a cluster with a head node in Azure (classic deployment model)** - If you use hello HPC Pack IaaS deployment script toocreate hello cluster in hello classic deployment model, enable hello **AutoGrowShrink** cluster property by setting hello AutoGrowShrink option in hello cluster configuration file.</span></span> <span data-ttu-id="5333c-135">如需詳細資訊，請參閱伴隨的 hello 的 hello 文件[指令碼下載](https://www.microsoft.com/download/details.aspx?id=44949)。</span><span class="sxs-lookup"><span data-stu-id="5333c-135">For details, see hello documentation accompanying hello [script download](https://www.microsoft.com/download/details.aspx?id=44949).</span></span>

    <span data-ttu-id="5333c-136">或者，啟用 hello **AutoGrowShrink**叢集內容之後使用 HPC PowerShell 部署 hello 叢集命令 hello 之後 > 一節中所述。</span><span class="sxs-lookup"><span data-stu-id="5333c-136">Alternatively, enable hello **AutoGrowShrink** cluster property after you deploy hello cluster by using HPC PowerShell commands described in hello following section.</span></span> <span data-ttu-id="5333c-137">這個 tooprepare，第一個完成的 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5333c-137">tooprepare for this, first complete hello following steps:</span></span>

  1. <span data-ttu-id="5333c-138">Hello 前端節點上，並在 hello Azure 訂用帳戶中設定 Azure 管理憑證。</span><span class="sxs-lookup"><span data-stu-id="5333c-138">Configure an Azure management certificate on hello head node and in hello Azure subscription.</span></span> <span data-ttu-id="5333c-139">針對測試部署，您可以使用 hello Microsoft 預設 HPC Azure 自我簽署的憑證，在 hello 前端節點上安裝 HPC Pack，並再上傳該憑證 tooyour Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5333c-139">For a test deployment, you can use hello Default Microsoft HPC Azure self-signed certificate that HPC Pack installs on hello head node, and then upload that certificate tooyour Azure subscription.</span></span> <span data-ttu-id="5333c-140">選項和步驟，請參閱 hello [TechNet 文件庫指引](https://technet.microsoft.com/library/gg481759.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5333c-140">For options and steps, see hello [TechNet Library guidance](https://technet.microsoft.com/library/gg481759.aspx).</span></span>

  2. <span data-ttu-id="5333c-141">執行**regedit** hello 前端節點上，請移 tooHKLM\SOFTWARE\Micorsoft\HPC\IaasInfo，並加入的字串值。</span><span class="sxs-lookup"><span data-stu-id="5333c-141">Run **regedit** on hello head node, go tooHKLM\SOFTWARE\Micorsoft\HPC\IaasInfo, and add a string value.</span></span> <span data-ttu-id="5333c-142">設定 hello 值名稱太 「 指紋 」，以及在步驟 1 中的 hello 憑證的值資料 toohello 指紋。</span><span class="sxs-lookup"><span data-stu-id="5333c-142">Set hello Value name too“ThumbPrint”, and Value data toohello thumbprint of hello certificate in Step 1.</span></span>

### <a name="hpc-powershell-commands-tooset-hello-autogrowshrink-property"></a><span data-ttu-id="5333c-143">HPC PowerShell 命令 tooset hello AutoGrowShrink 屬性</span><span class="sxs-lookup"><span data-stu-id="5333c-143">HPC PowerShell commands tooset hello AutoGrowShrink property</span></span>
<span data-ttu-id="5333c-144">以下是範例 HPC PowerShell 命令 tooset **AutoGrowShrink**和 tootune 其行為與其他參數。</span><span class="sxs-lookup"><span data-stu-id="5333c-144">Following are sample HPC PowerShell commands tooset **AutoGrowShrink** and tootune its behavior with additional parameters.</span></span> <span data-ttu-id="5333c-145">請參閱[AutoGrowShrink 參數](#AutoGrowShrink-parameters)本文稍後的 hello 設定的完整清單。</span><span class="sxs-lookup"><span data-stu-id="5333c-145">See [AutoGrowShrink parameters](#AutoGrowShrink-parameters) later in this article for hello complete list of settings.</span></span>

<span data-ttu-id="5333c-146">toorun 這些命令時，系統管理員身分啟動 HPC PowerShell hello 叢集前端節點上。</span><span class="sxs-lookup"><span data-stu-id="5333c-146">toorun these commands, start HPC PowerShell on hello cluster head node as an administrator.</span></span>

<span data-ttu-id="5333c-147">**tooenable hello AutoGrowShrink 屬性**</span><span class="sxs-lookup"><span data-stu-id="5333c-147">**tooenable hello AutoGrowShrink property**</span></span>

```powershell
Set-HpcClusterProperty –EnableGrowShrink 1
```

<span data-ttu-id="5333c-148">**toodisable hello AutoGrowShrink 屬性**</span><span class="sxs-lookup"><span data-stu-id="5333c-148">**toodisable hello AutoGrowShrink property**</span></span>

```powershell
Set-HpcClusterProperty –EnableGrowShrink 0
```

<span data-ttu-id="5333c-149">**toochange hello 成長以分鐘為單位的間隔**</span><span class="sxs-lookup"><span data-stu-id="5333c-149">**toochange hello grow interval in minutes**</span></span>

```powershell
Set-HpcClusterProperty –GrowInterval <interval>
```

<span data-ttu-id="5333c-150">**toochange hello 壓縮以分鐘為單位的間隔**</span><span class="sxs-lookup"><span data-stu-id="5333c-150">**toochange hello shrink interval in minutes**</span></span>

```powershell
Set-HpcClusterProperty –ShrinkInterval <interval>
```

<span data-ttu-id="5333c-151">**tooview hello 目前組態 AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="5333c-151">**tooview hello current configuration of AutoGrowShrink**</span></span>

```powershell
Get-HpcClusterProperty –AutoGrowShrink
```

<span data-ttu-id="5333c-152">**從 AutoGrowShrink tooexclude 節點群組**</span><span class="sxs-lookup"><span data-stu-id="5333c-152">**tooexclude node groups from AutoGrowShrink**</span></span>

```powershell
Set-HpcClusterProperty –ExcludeNodeGroups <group1,group2,group3>
```

>[!NOTE] 
> <span data-ttu-id="5333c-153">從 HPC Pack 2016 開始支援這個參數</span><span class="sxs-lookup"><span data-stu-id="5333c-153">This parameter is supported starting in HPC Pack 2016</span></span>
>

### <a name="autogrowshrink-parameters"></a><span data-ttu-id="5333c-154">AutoGrowShrink 參數</span><span class="sxs-lookup"><span data-stu-id="5333c-154">AutoGrowShrink parameters</span></span>
<span data-ttu-id="5333c-155">hello 如下 AutoGrowShrink 參數，您可以修改使用 hello**組 HpcClusterProperty**命令。</span><span class="sxs-lookup"><span data-stu-id="5333c-155">hello following are AutoGrowShrink parameters that you can modify by using hello **Set-HpcClusterProperty** command.</span></span>

* <span data-ttu-id="5333c-156">**EnableGrowShrink** -切換 tooenable 或停用 hello **AutoGrowShrink**屬性。</span><span class="sxs-lookup"><span data-stu-id="5333c-156">**EnableGrowShrink** - Switch tooenable or disable hello **AutoGrowShrink** property.</span></span>
* <span data-ttu-id="5333c-157">**ParamSweepTasksPerCore** -參數式整理數目工作 toogrow 一個核心。</span><span class="sxs-lookup"><span data-stu-id="5333c-157">**ParamSweepTasksPerCore** - Number of parametric sweep tasks toogrow one core.</span></span> <span data-ttu-id="5333c-158">hello 預設值為 toogrow 每項工作的其中一個核心。</span><span class="sxs-lookup"><span data-stu-id="5333c-158">hello default is toogrow one core per task.</span></span>

  > [!NOTE]
  > <span data-ttu-id="5333c-159">HPC Pack QFE KB3134307 變更**ParamSweepTasksPerCore**太**TasksPerResourceUnit**。</span><span class="sxs-lookup"><span data-stu-id="5333c-159">HPC Pack QFE KB3134307 changes **ParamSweepTasksPerCore** too**TasksPerResourceUnit**.</span></span> <span data-ttu-id="5333c-160">它根據 hello 作業資源類型，而且可以是節點，通訊端或核心。</span><span class="sxs-lookup"><span data-stu-id="5333c-160">It is based on hello job resource type and can be node, socket, or core.</span></span>
  >
  >
* <span data-ttu-id="5333c-161">**GrowThreshold** -佇列的工作 tootrigger 自動成長的臨界值。</span><span class="sxs-lookup"><span data-stu-id="5333c-161">**GrowThreshold** - Threshold of queued tasks tootrigger automatic growth.</span></span> <span data-ttu-id="5333c-162">hello 預設值為 1，這表示，如果有 1 或更多的工作，在 [hello 排入佇列的狀態、 自動成長] 節點。</span><span class="sxs-lookup"><span data-stu-id="5333c-162">hello default is 1, which means that if there are 1 or more tasks in hello queued state, automatically grow nodes.</span></span>
* <span data-ttu-id="5333c-163">**GrowInterval** -分鐘 tootrigger 自動成長的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="5333c-163">**GrowInterval** - Interval in minutes tootrigger automatic growth.</span></span> <span data-ttu-id="5333c-164">hello 預設間隔是 5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="5333c-164">hello default interval is 5 minutes.</span></span>
* <span data-ttu-id="5333c-165">**ShrinkInterval** -間隔分鐘 tootrigger 自動壓縮。</span><span class="sxs-lookup"><span data-stu-id="5333c-165">**ShrinkInterval** - Interval in minutes tootrigger automatic shrinking.</span></span> <span data-ttu-id="5333c-166">hello 預設間隔是 5 分鐘。 |</span><span class="sxs-lookup"><span data-stu-id="5333c-166">hello default interval is 5 minutes.|</span></span>
* <span data-ttu-id="5333c-167">**ShrinkIdleTimes** -連續檢查 tooshrink tooindicate hello 節點數目會處於閒置狀態。</span><span class="sxs-lookup"><span data-stu-id="5333c-167">**ShrinkIdleTimes** - Number of continuous checks tooshrink tooindicate hello nodes are idle.</span></span> <span data-ttu-id="5333c-168">hello 預設值為 3 次。</span><span class="sxs-lookup"><span data-stu-id="5333c-168">hello default is 3 times.</span></span> <span data-ttu-id="5333c-169">例如，如果 hello **ShrinkInterval**為 5 分鐘，HPC Pack 檢查 hello 節點是否為閒置每隔 5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="5333c-169">For example, if hello **ShrinkInterval** is 5 minutes, HPC Pack checks whether hello node is idle every 5 minutes.</span></span> <span data-ttu-id="5333c-170">如果 hello 節點在 hello 閒置狀態 3 連續檢查 （15 分鐘） 之後，HPC Pack 會縮小該節點。</span><span class="sxs-lookup"><span data-stu-id="5333c-170">If hello nodes are in hello idle state after 3 continuous checks (15 minutes), then HPC Pack shrinks that node.</span></span>
* <span data-ttu-id="5333c-171">**ExtraNodesGrowRatio** -其他節點 toogrow 訊息傳遞介面 (MPI) 工作的百分比。</span><span class="sxs-lookup"><span data-stu-id="5333c-171">**ExtraNodesGrowRatio** - Additional percentage of nodes toogrow for Message Passing Interface (MPI) jobs.</span></span> <span data-ttu-id="5333c-172">hello 預設值為 1，表示 HPC Pack 成長節點 MPI 工作的 1%。</span><span class="sxs-lookup"><span data-stu-id="5333c-172">hello default value is 1, which means that HPC Pack grows nodes 1% for MPI jobs.</span></span>
* <span data-ttu-id="5333c-173">**GrowByMin** -切換 tooindicate 是否 hello 自動成長原則根據 hello hello 工作所需的最小資源。</span><span class="sxs-lookup"><span data-stu-id="5333c-173">**GrowByMin** - Switch tooindicate whether hello autogrow policy is based on hello minimum resources required for hello job.</span></span> <span data-ttu-id="5333c-174">hello 預設值為 false，這表示 HPC Pack 成長作業 hello hello 作業所需的最大資源為基礎的節點。</span><span class="sxs-lookup"><span data-stu-id="5333c-174">hello default is false, which means that HPC Pack grows nodes for jobs based on hello maximum resources required for hello jobs.</span></span>
* <span data-ttu-id="5333c-175">**SoaJobGrowThreshold** -臨界值的連入 SOA 要求 tootrigger hello 自動成長的程序。</span><span class="sxs-lookup"><span data-stu-id="5333c-175">**SoaJobGrowThreshold** - Threshold of incoming SOA requests tootrigger hello automatic grow process.</span></span> <span data-ttu-id="5333c-176">hello 預設值是 50000。</span><span class="sxs-lookup"><span data-stu-id="5333c-176">hello default value is 50000.</span></span>

  > [!NOTE]
  > <span data-ttu-id="5333c-177">從 HPC Pack 2012 R2 Update 3 開始支援這個參數。</span><span class="sxs-lookup"><span data-stu-id="5333c-177">This parameter is supported starting in HPC Pack 2012 R2 Update 3.</span></span>
  >
  >
* <span data-ttu-id="5333c-178">**SoaRequestsPerCore** -要求 toogrow 一個核心的連入 SOA 的數目。</span><span class="sxs-lookup"><span data-stu-id="5333c-178">**SoaRequestsPerCore** -Number of incoming SOA requests toogrow one core.</span></span> <span data-ttu-id="5333c-179">hello 預設值為 20000。</span><span class="sxs-lookup"><span data-stu-id="5333c-179">hello default value is 20000.</span></span>

  > [!NOTE]
  > <span data-ttu-id="5333c-180">從 HPC Pack 2012 R2 Update 3 開始支援這個參數。</span><span class="sxs-lookup"><span data-stu-id="5333c-180">This parameter is supported starting in HPC Pack 2012 R2 Update 3.</span></span>
  >
* <span data-ttu-id="5333c-181">**ExcludeNodeGroups** – hello 中的節點指定節點群組不會自動擴增和縮減。</span><span class="sxs-lookup"><span data-stu-id="5333c-181">**ExcludeNodeGroups** – Nodes in hello specified node groups do not automatically grow and shrink.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="5333c-182">從 HPC Pack 2016 開始支援這個參數。</span><span class="sxs-lookup"><span data-stu-id="5333c-182">This parameter is supported starting in HPC Pack 2016.</span></span>
  >

### <a name="mpi-example"></a><span data-ttu-id="5333c-183">MPI 範例</span><span class="sxs-lookup"><span data-stu-id="5333c-183">MPI example</span></span>
<span data-ttu-id="5333c-184">根據預設 HPC Pack 成長 1%的 MPI 工作的額外節點 (**ExtraNodesGrowRatio**設定 too1)。</span><span class="sxs-lookup"><span data-stu-id="5333c-184">By default HPC Pack grows 1% extra nodes for MPI jobs (**ExtraNodesGrowRatio** is set too1).</span></span> <span data-ttu-id="5333c-185">hello 的原因是 MPI 可能需要多個節點，而且當準備所有節點只能執行 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="5333c-185">hello reason is that MPI may require multiple nodes, and hello job can only run when all nodes are ready.</span></span> <span data-ttu-id="5333c-186">當 Azure 啟動節點時，有時一個節點可能需要更多時間 toostart 比其他造成閒置時等候該節點 tooget 準備其他節點 toobe。</span><span class="sxs-lookup"><span data-stu-id="5333c-186">When Azure starts nodes, occasionally one node might need more time toostart than others, causing other nodes toobe idle while waiting for that node tooget ready.</span></span> <span data-ttu-id="5333c-187">藉由增加額外的節點，HPC Pack 會減少此資源的等候時間，並可能節省成本。</span><span class="sxs-lookup"><span data-stu-id="5333c-187">By growing extra nodes, HPC Pack reduces this resource waiting time, and potentially saves costs.</span></span> <span data-ttu-id="5333c-188">tooincrease hello 百分比的 MPI 工作 （例如，too10%） 的額外節點執行類似的命令</span><span class="sxs-lookup"><span data-stu-id="5333c-188">tooincrease hello percentage of extra nodes for MPI jobs (for example, too10%), run a command similar to</span></span>

    Set-HpcClusterProperty -ExtraNodesGrowRatio 10

### <a name="soa-example"></a><span data-ttu-id="5333c-189">SOA 範例</span><span class="sxs-lookup"><span data-stu-id="5333c-189">SOA example</span></span>
<span data-ttu-id="5333c-190">根據預設， **SoaJobGrowThreshold**設定 too50000 和**SoaRequestsPerCore** too200000 設定。</span><span class="sxs-lookup"><span data-stu-id="5333c-190">By default, **SoaJobGrowThreshold** is set too50000 and **SoaRequestsPerCore** is set too200000.</span></span> <span data-ttu-id="5333c-191">如果您送出一個包含 70000 個要求的 SOA 作業，則會有一個排入佇列工作，且傳入要求為 70000。</span><span class="sxs-lookup"><span data-stu-id="5333c-191">If you submit one SOA job with 70000 requests, there is one queued task and incoming requests are 70000.</span></span> <span data-ttu-id="5333c-192">在此情況下 HPC Pack 成長 1 個核心的 hello 排入佇列的工作，與針對內送要求，成長 (70000-50000) / 20000 = 1 核心，因此在總計成長 2 核心，此 SOA 工作。</span><span class="sxs-lookup"><span data-stu-id="5333c-192">In this case HPC Pack grows 1 core for hello queued task, and for incoming requests, grows (70000 - 50000)/20000 = 1 core, so in total grows 2 cores for this SOA job.</span></span>

## <a name="run-hello-azureautogrowshrinkps1-script"></a><span data-ttu-id="5333c-193">執行 hello AzureAutoGrowShrink.ps1 指令碼</span><span class="sxs-lookup"><span data-stu-id="5333c-193">Run hello AzureAutoGrowShrink.ps1 script</span></span>
### <a name="prerequisites"></a><span data-ttu-id="5333c-194">必要條件</span><span class="sxs-lookup"><span data-stu-id="5333c-194">Prerequisites</span></span>

* <span data-ttu-id="5333c-195">**HPC Pack 2012 R2 更新 1 或更新版本的叢集**-hello **AzureAutoGrowShrink.ps1** hello %ccp_home%bin 資料夾中安裝指令碼。</span><span class="sxs-lookup"><span data-stu-id="5333c-195">**HPC Pack 2012 R2 Update 1 or later cluster** - hello **AzureAutoGrowShrink.ps1** script is installed in hello %CCP_HOME%bin folder.</span></span> <span data-ttu-id="5333c-196">hello 叢集前端節點可以是部署在內部或 Azure VM 中。</span><span class="sxs-lookup"><span data-stu-id="5333c-196">hello cluster head node can be deployed either on-premises or in an Azure VM.</span></span> <span data-ttu-id="5333c-197">請參閱[設定混合式叢集使用 HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget 啟動內部部署前端節點與 Azure 「 高載 」 節點。</span><span class="sxs-lookup"><span data-stu-id="5333c-197">See [Set up a hybrid cluster with HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget started with an on-premises head node and Azure "burst" nodes.</span></span> <span data-ttu-id="5333c-198">請參閱 hello [HPC Pack IaaS 部署指令碼](hpcpack-cluster-powershell-script.md)tooquickly HPC Pack 叢集部署在 Azure Vm，或使用[Azure 快速入門範本](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/)。</span><span class="sxs-lookup"><span data-stu-id="5333c-198">See hello [HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md) tooquickly deploy an HPC Pack cluster in Azure VMs, or use an [Azure quickstart template](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/).</span></span>
* <span data-ttu-id="5333c-199">**Azure PowerShell 1.4.0** -hello 指令碼目前取決於這個特定版本的 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="5333c-199">**Azure PowerShell 1.4.0** - hello script currently depends on this specific version of Azure PowerShell.</span></span>
* <span data-ttu-id="5333c-200">**針對 Azure 的叢集高載節點**-HPC Pack 已安裝用戶端電腦上或 hello 前端節點上執行 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="5333c-200">**For a cluster with Azure burst nodes** - Run hello script on a client computer where HPC Pack is installed, or on hello head node.</span></span> <span data-ttu-id="5333c-201">如果用戶端電腦上執行，請確定您設定 hello 變數 $env: CCP_SCHEDULER toopoint toohello 前端節點。</span><span class="sxs-lookup"><span data-stu-id="5333c-201">If running on a client computer, ensure that you set hello variable $env:CCP_SCHEDULER toopoint toohello head node.</span></span> <span data-ttu-id="5333c-202">hello Azure 「 高載 」 節點必須加入 toohello 叢集中，但它們也可能處於 hello 未部署 」 狀態。</span><span class="sxs-lookup"><span data-stu-id="5333c-202">hello Azure “burst” nodes must be added toohello cluster, but they may be in hello Not-Deployed state.</span></span>
* <span data-ttu-id="5333c-203">**叢集部署在 Azure Vm （Resource Manager 部署模型） 中的**-針對 Azure Vm 部署在 hello Resource Manager 部署模型中的叢集，hello 指令碼支援兩種方法進行 Azure 驗證： 登入 tooyour Azure 帳戶toorun hello 指令碼每次 (藉由執行`Login-AzureRmAccount`，或使用憑證設定服務主體的 tooauthenticate。</span><span class="sxs-lookup"><span data-stu-id="5333c-203">**For a cluster deployed in Azure VMs (Resource Manager deployment model)** - For a cluster of Azure VMs deployed in hello Resource Manager deployment model, hello script supports two methods for Azure authentication: sign in tooyour Azure account toorun hello script every time (by running `Login-AzureRmAccount`, or configure a service principal tooauthenticate with a certificate.</span></span> <span data-ttu-id="5333c-204">HPC Pack 提供 hello 指令碼**ConfigARMAutoGrowShrinkCert.ps** toocreate 憑證的服務主體。</span><span class="sxs-lookup"><span data-stu-id="5333c-204">HPC Pack provides hello script **ConfigARMAutoGrowShrinkCert.ps** toocreate a service principal with certificate.</span></span> <span data-ttu-id="5333c-205">hello 指令碼會建立 Azure Active Directory (Azure AD) 應用程式和服務主體，並指派 hello 參與者角色 toohello 服務主體。</span><span class="sxs-lookup"><span data-stu-id="5333c-205">hello script creates an Azure Active Directory (Azure AD) application and a service principal, and assigns hello Contributor role toohello service principal.</span></span> <span data-ttu-id="5333c-206">toorun hello 指令碼，以系統管理員身分啟動 Azure PowerShell，然後執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="5333c-206">toorun hello script, start Azure PowerShell  as administrator and run hello following commands:</span></span>

    ```powershell
    cd $env:CCP_HOME\bin

    Login-AzureRmAccount

    .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -PfxFile "d:\yourcertificate.pfx"
    ```

    <span data-ttu-id="5333c-207">如需 **ConfigARMAutoGrowShrinkCert.ps1** 的詳細資訊，請執行 `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`。</span><span class="sxs-lookup"><span data-stu-id="5333c-207">For more details about **ConfigARMAutoGrowShrinkCert.ps1**, run `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`,</span></span>

* <span data-ttu-id="5333c-208">**叢集部署 Azure 虛擬機器 （傳統部署模型） 中的**-hello 前端節點 VM 上執行 hello 指令碼，因為它相依於 hello **Start-hpciaasnode.ps1**和**Stop-hpciaasnode.ps1**所安裝的指令碼。</span><span class="sxs-lookup"><span data-stu-id="5333c-208">**For a cluster deployed in Azure VMs (classic deployment model)** - Run hello script on hello head node VM, because it depends on hello **Start-HpcIaaSNode.ps1** and **Stop-HpcIaaSNode.ps1** scripts that are installed there.</span></span> <span data-ttu-id="5333c-209">這些指令碼額外需要 Azure 管理憑證或發佈設定檔 (請參閱 [在 Azure 中的 HPC Pack 叢集管理計算節點](hpcpack-cluster-node-manage.md))。</span><span class="sxs-lookup"><span data-stu-id="5333c-209">Those scripts additionally require an Azure management certificate or publish settings file (see [Manage compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster-node-manage.md)).</span></span> <span data-ttu-id="5333c-210">請確定所有 hello 計算節點 Vm，您必須已加入 toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="5333c-210">Make sure all hello compute node VMs you need are already added toohello cluster.</span></span> <span data-ttu-id="5333c-211">它們也可能處於 hello 已停止 」 狀態。</span><span class="sxs-lookup"><span data-stu-id="5333c-211">They may be in hello Stopped state.</span></span>



### <a name="syntax"></a><span data-ttu-id="5333c-212">語法</span><span class="sxs-lookup"><span data-stu-id="5333c-212">Syntax</span></span>
```powershell
AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfActiveQueuedTasksPerNodeToGrow <Single> [-NumOfActiveQueuedTasksToGrowThreshold <Int32>]
    [-NumOfInitialNodesToGrow <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>]
    [-ShrinkCheckIdleTimes <Int32>] [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>]
    [<CommonParameters>]

AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfQueuedJobsPerNodeToGrow <Single> [-NumOfQueuedJobsToGrowThreshold <Int32>] [-NumOfInitialNodesToGrow
    <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>] [-ShrinkCheckIdleTimes <Int32>]
    [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]

AzureAutoGrowShrink.ps1 -UseLastConfigurations [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]
```
### <a name="parameters"></a><span data-ttu-id="5333c-213">參數</span><span class="sxs-lookup"><span data-stu-id="5333c-213">Parameters</span></span>
* <span data-ttu-id="5333c-214">**NodeTemplates** -hello hello 節點 toogrow 範圍和壓縮的 hello 節點範本 toodefine 名稱。</span><span class="sxs-lookup"><span data-stu-id="5333c-214">**NodeTemplates** - Names of hello node templates toodefine hello scope for hello nodes toogrow and shrink.</span></span> <span data-ttu-id="5333c-215">如果未指定 (hello 預設值是 @ （)），hello 中的所有節點**AzureNodes**節點群組都會納入範圍時**NodeType** hello 中的值為 AzureNodes，以及所有節點**ComputeNodes**節點群組都會納入範圍時**NodeType**的值為 ComputeNodes。</span><span class="sxs-lookup"><span data-stu-id="5333c-215">If not specified (hello default value is @()), all nodes in hello **AzureNodes** node group are in scope when **NodeType** has a value of AzureNodes, and all nodes in hello **ComputeNodes** node group are in scope when **NodeType** has a value of ComputeNodes.</span></span>
* <span data-ttu-id="5333c-216">**Jobtemplate** -名稱 hello 作業 hello 節點 toogrow 範本 toodefine hello 範圍。</span><span class="sxs-lookup"><span data-stu-id="5333c-216">**JobTemplates** - Names of hello job templates toodefine hello scope for hello nodes toogrow.</span></span>
* <span data-ttu-id="5333c-217">**NodeType** -hello toogrow 節點的類型，並壓縮。</span><span class="sxs-lookup"><span data-stu-id="5333c-217">**NodeType** - hello type of node toogrow and shrink.</span></span> <span data-ttu-id="5333c-218">支援的值包括：</span><span class="sxs-lookup"><span data-stu-id="5333c-218">Supported values are:</span></span>

  * <span data-ttu-id="5333c-219">**AzureNodes** - 針對內部部署或 Azure IaaS 叢集中的 Azure PaaS (高載) 節點。</span><span class="sxs-lookup"><span data-stu-id="5333c-219">**AzureNodes** – for Azure PaaS (burst) nodes in an on-premises or Azure IaaS cluster.</span></span>
  * <span data-ttu-id="5333c-220">**ComputeNodes** - 針對只在 Azure IaaS 叢集的計算節點 VM。</span><span class="sxs-lookup"><span data-stu-id="5333c-220">**ComputeNodes** - for compute node VMs only in an Azure IaaS cluster.</span></span>

* <span data-ttu-id="5333c-221">**NumOfQueuedJobsPerNodeToGrow** -所需的佇列工作數目 toogrow 一個節點。</span><span class="sxs-lookup"><span data-stu-id="5333c-221">**NumOfQueuedJobsPerNodeToGrow** - Number of queued jobs required toogrow one node.</span></span>
* <span data-ttu-id="5333c-222">**NumOfQueuedJobsToGrowThreshold** -hello 臨界值數目的佇列的工作 toostart hello 成長程序。</span><span class="sxs-lookup"><span data-stu-id="5333c-222">**NumOfQueuedJobsToGrowThreshold** - hello threshold number of queued jobs toostart hello grow process.</span></span>
* <span data-ttu-id="5333c-223">**NumOfActiveQueuedTasksPerNodeToGrow** -hello 作用中佇列工作數目所需 toogrow 一個節點。</span><span class="sxs-lookup"><span data-stu-id="5333c-223">**NumOfActiveQueuedTasksPerNodeToGrow** - hello number of active queued tasks required toogrow one node.</span></span> <span data-ttu-id="5333c-224">如果 **NumOfQueuedJobsPerNodeToGrow** 指定了大於 0 的值，則會忽略這個參數。</span><span class="sxs-lookup"><span data-stu-id="5333c-224">If **NumOfQueuedJobsPerNodeToGrow** is specified with a value greater than 0, this parameter is ignored.</span></span>
* <span data-ttu-id="5333c-225">**NumOfActiveQueuedTasksToGrowThreshold** -hello 臨界值數目的作用中佇列的工作 toostart hello 成長程序。</span><span class="sxs-lookup"><span data-stu-id="5333c-225">**NumOfActiveQueuedTasksToGrowThreshold** - hello threshold number of active queued tasks toostart hello grow process.</span></span>
* <span data-ttu-id="5333c-226">**NumOfInitialNodesToGrow** -hello 初始節點 toogrow 的最小數目，如果所有範圍中的 hello 節點**未部署**或**已停止 （取消配置）**。</span><span class="sxs-lookup"><span data-stu-id="5333c-226">**NumOfInitialNodesToGrow** - hello initial minimum number of nodes toogrow if all hello nodes in scope are **Not-Deployed** or **Stopped (Deallocated)**.</span></span>
* <span data-ttu-id="5333c-227">**GrowCheckIntervalMins** -hello 以分鐘為單位的間隔檢查 toogrow。</span><span class="sxs-lookup"><span data-stu-id="5333c-227">**GrowCheckIntervalMins** - hello interval in minutes between checks toogrow.</span></span>
* <span data-ttu-id="5333c-228">**ShrinkCheckIntervalMins** -hello 以分鐘為單位的間隔檢查 tooshrink。</span><span class="sxs-lookup"><span data-stu-id="5333c-228">**ShrinkCheckIntervalMins** - hello interval in minutes between checks tooshrink.</span></span>
* <span data-ttu-id="5333c-229">**ShrinkCheckIdleTimes** -hello 數連續壓縮檢查 (隔開**ShrinkCheckIntervalMins**) tooindicate hello 節點處於閒置狀態。</span><span class="sxs-lookup"><span data-stu-id="5333c-229">**ShrinkCheckIdleTimes** - hello number of continuous shrink checks (separated by **ShrinkCheckIntervalMins**) tooindicate hello nodes are idle.</span></span>
* <span data-ttu-id="5333c-230">**UseLastConfigurations** -hello 先前 hello 引數檔案中儲存的組態。</span><span class="sxs-lookup"><span data-stu-id="5333c-230">**UseLastConfigurations** - hello previous configurations saved in hello argument file.</span></span>
* <span data-ttu-id="5333c-231">**ArgFile**-hello hello 引數使用的檔案 toosave 的名稱，並更新 hello 組態 toorun hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="5333c-231">**ArgFile**- hello name of hello argument file used toosave and update hello configurations toorun hello script.</span></span>
* <span data-ttu-id="5333c-232">**LogFilePrefix** -hello hello 記錄檔的前置詞名稱。</span><span class="sxs-lookup"><span data-stu-id="5333c-232">**LogFilePrefix** - hello prefix name of hello log file.</span></span> <span data-ttu-id="5333c-233">您可以指定路徑。</span><span class="sxs-lookup"><span data-stu-id="5333c-233">You can specify a path.</span></span> <span data-ttu-id="5333c-234">根據預設 hello 記錄檔是寫入的 toohello 目前工作目錄。</span><span class="sxs-lookup"><span data-stu-id="5333c-234">By default hello log is written toohello current working directory.</span></span>

### <a name="example-1"></a><span data-ttu-id="5333c-235">範例 1</span><span class="sxs-lookup"><span data-stu-id="5333c-235">Example 1</span></span>
<span data-ttu-id="5333c-236">hello 下列範例會設定的 hello Azure 高載節點使用預設 AzureNode 範本 toogrow 部署和自動壓縮。</span><span class="sxs-lookup"><span data-stu-id="5333c-236">hello following example configures hello Azure burst nodes deployed with the Default AzureNode Template toogrow and shrink automatically.</span></span> <span data-ttu-id="5333c-237">如果所有節點一開始都會處於 hello**未部署**狀態時，至少 3 個節點都都已啟動。</span><span class="sxs-lookup"><span data-stu-id="5333c-237">If all the nodes are initially in hello **Not-Deployed** state, at least 3 nodes are started.</span></span> <span data-ttu-id="5333c-238">Hello 指令碼如果 hello 佇列工作數目超過 8 個，啟動節點，直到其數目超過佇列工作與 hello 比例**NumOfQueuedJobsPerNodeToGrow**。</span><span class="sxs-lookup"><span data-stu-id="5333c-238">If hello number of queued jobs exceeds 8, hello script starts nodes until their number exceeds hello ratio of queued jobs to **NumOfQueuedJobsPerNodeToGrow**.</span></span> <span data-ttu-id="5333c-239">如果發現節點 toobe 閒置 3 連續的閒置時間，會將它停止。</span><span class="sxs-lookup"><span data-stu-id="5333c-239">If a node is found toobe idle in 3 consecutive idle times, it is stopped.</span></span>

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates @('Default AzureNode
 Template') -NodeType AzureNodes -NumOfQueuedJobsPerNodeToGrow 5
 -NumOfQueuedJobsToGrowThreshold 8 -NumOfInitialNodesToGrow 3
 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 3
```

### <a name="example-2"></a><span data-ttu-id="5333c-240">範例 2</span><span class="sxs-lookup"><span data-stu-id="5333c-240">Example 2</span></span>
<span data-ttu-id="5333c-241">hello 下列範例會設定的 hello Azure 計算節點 Vm 部署的 hello 預設 ComputeNode 範本 toogrow 和自動壓縮。</span><span class="sxs-lookup"><span data-stu-id="5333c-241">hello following example configures hello Azure compute node VMs deployed with hello Default ComputeNode Template toogrow and shrink automatically.</span></span>
<span data-ttu-id="5333c-242">hello 預設工作範本所設定的 hello 作業定義的工作負載 hello 範圍 hello 叢集上。</span><span class="sxs-lookup"><span data-stu-id="5333c-242">hello jobs configured by hello Default job template define hello scope of the workload on hello cluster.</span></span> <span data-ttu-id="5333c-243">如果一開始會停止所有 hello 節點，會啟動最少 5 個節點。</span><span class="sxs-lookup"><span data-stu-id="5333c-243">If all hello nodes are initially stopped, at least 5 nodes are started.</span></span> <span data-ttu-id="5333c-244">Hello 指令碼如果 hello 作用中佇列工作數目超過 15，啟動節點，直到其數目超過作用中佇列工作的 hello 比率太**NumOfActiveQueuedTasksPerNodeToGrow**。</span><span class="sxs-lookup"><span data-stu-id="5333c-244">If hello number of active queued tasks exceeds 15, hello script starts nodes until their number exceeds hello ratio of active queued tasks too**NumOfActiveQueuedTasksPerNodeToGrow**.</span></span> <span data-ttu-id="5333c-245">如果發現節點 toobe 閒置 10 個連續的閒置時間，會將它停止。</span><span class="sxs-lookup"><span data-stu-id="5333c-245">If a node is found toobe idle in 10 consecutive idle times, it is stopped.</span></span>

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates 'Default ComputeNode Template' -JobTemplates 'Default' -NodeType ComputeNodes -NumOfActiveQueuedTasksPerNodeToGrow 10 -NumOfActiveQueuedTasksToGrowThreshold 15 -NumOfInitialNodesToGrow 5 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 10 -ArgFile 'IaaSVMComputeNodes_Arg.xml' -LogFilePrefix 'IaaSVMComputeNodes_log'
```
