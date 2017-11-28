---
title: "aaaManage HPC Pack 叢集計算節點 |Microsoft 文件"
description: "深入了解 PowerShell 指令碼工具 tooadd、 移除、 啟動，以及停止在 Azure 中的 HPC Pack 2012 R2 叢集計算節點"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 4193f03b-94e9-4704-a7ad-379abde063a9
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 5ac1142cc5da984020779434fbb7cba5ad7c14bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-number-and-availability-of-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="5b530-103">管理 hello 數目和計算節點，在 Azure 中部署 HPC Pack 叢集中的可用性</span><span class="sxs-lookup"><span data-stu-id="5b530-103">Manage hello number and availability of compute nodes in an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="5b530-104">如果您在 Azure Vm 中建立的 HPC Pack 2012 R2 叢集，您可能想 tooeasily 新增、 移除、 啟動 （佈建），或一些停止 （解除佈建） 的方式計算節點 Vm，叢集中。</span><span class="sxs-lookup"><span data-stu-id="5b530-104">If you created an HPC Pack 2012 R2 cluster in Azure VMs, you might want ways tooeasily add, remove, start (provision), or stop (deprovision) some compute node VMs in the cluster.</span></span> <span data-ttu-id="5b530-105">toodo 這些工作，執行 hello 前端節點 VM 上安裝 Azure PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="5b530-105">toodo these tasks, run Azure PowerShell scripts that are installed on hello head node VM.</span></span> <span data-ttu-id="5b530-106">這些指令碼可協助您控制 hello 數目和 HPC Pack 叢集資源的可用性，您可以控制成本。</span><span class="sxs-lookup"><span data-stu-id="5b530-106">These scripts help you control hello number and availability of your HPC Pack cluster resources so you can control costs.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="5b530-107">本文適用於僅 tooHPC Pack 2012 R2 中的叢集使用 hello 傳統部署模型所建立的 Azure。</span><span class="sxs-lookup"><span data-stu-id="5b530-107">This article applies only tooHPC Pack 2012 R2 clusters in Azure created using hello classic deployment model.</span></span> <span data-ttu-id="5b530-108">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="5b530-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> <span data-ttu-id="5b530-109">此外，本文中所述的 hello PowerShell 指令碼中沒有 HPC Pack 2016。</span><span class="sxs-lookup"><span data-stu-id="5b530-109">In addition, hello PowerShell scripts described in this article are not available in HPC Pack 2016.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b530-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="5b530-110">Prerequisites</span></span>
* <span data-ttu-id="5b530-111">**在 Azure Vm 中的 HPC Pack 2012 R2 叢集**: hello 傳統部署模型中建立與 HPC Pack 2012 R2 的叢集。</span><span class="sxs-lookup"><span data-stu-id="5b530-111">**HPC Pack 2012 R2 cluster in Azure VMs**: Create an HPC Pack 2012 R2 cluster in hello classic deployment model.</span></span> <span data-ttu-id="5b530-112">例如，您可以使用 hello hello Azure Marketplace 中的 HPC Pack 2012 R2 VM 映像和 Azure PowerShell 指令碼自動化 hello 部署。</span><span class="sxs-lookup"><span data-stu-id="5b530-112">For example, you can automate hello deployment by using hello HPC Pack 2012 R2 VM image in hello Azure Marketplace and an Azure PowerShell script.</span></span> <span data-ttu-id="5b530-113">資訊和必要條件，請參閱[以 hello HPC Pack IaaS 部署指令碼建立 HPC 叢集](hpcpack-cluster-powershell-script.md)。</span><span class="sxs-lookup"><span data-stu-id="5b530-113">For information and prerequisites, see [Create an HPC Cluster with hello HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md).</span></span>
  
    <span data-ttu-id="5b530-114">部署之後，hello 節點管理指令碼中尋找 hello %ccp\_hello 前端節點上的主目錄 %bin 資料夾。</span><span class="sxs-lookup"><span data-stu-id="5b530-114">After deployment, find hello node management scripts in hello %CCP\_HOME%bin folder on hello head node.</span></span> <span data-ttu-id="5b530-115">系統管理員身分執行每個 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="5b530-115">Run each of hello scripts as an administrator.</span></span>
* <span data-ttu-id="5b530-116">**Azure 發行設定檔案或管理憑證**： 需要 hello 前端節點上的 toodo hello 下列其中一種：</span><span class="sxs-lookup"><span data-stu-id="5b530-116">**Azure publish settings file or management certificate**: You need toodo one of hello following on hello head node:</span></span>
  
  * <span data-ttu-id="5b530-117">**匯入 hello Azure 發行設定檔**。</span><span class="sxs-lookup"><span data-stu-id="5b530-117">**Import hello Azure publish settings file**.</span></span> <span data-ttu-id="5b530-118">toodo 下列 Azure PowerShell cmdlet hello 前端節點上，執行的 hello:</span><span class="sxs-lookup"><span data-stu-id="5b530-118">toodo this, run hello following Azure PowerShell cmdlets on hello head node:</span></span>
    
    ```PowerShell
    Get-AzurePublishSettingsFile
    
    Import-AzurePublishSettingsFile –PublishSettingsFile <publish settings file>
    ```
  * <span data-ttu-id="5b530-119">**Hello 前端節點上設定 hello Azure 管理憑證**。</span><span class="sxs-lookup"><span data-stu-id="5b530-119">**Configure hello Azure management certificate on hello head node**.</span></span> <span data-ttu-id="5b530-120">如果您擁有 hello.cer 檔案，它匯入 hello CurrentUser\My 憑證存放區，然後再執行下列 Azure PowerShell cmdlet （AzureCloud 或 AzureChinaCloud） 您 Azure 環境的 hello:</span><span class="sxs-lookup"><span data-stu-id="5b530-120">If you have hello .cer file, import it in hello CurrentUser\My certificate store and then run hello following Azure PowerShell cmdlet for your Azure environment (either AzureCloud or AzureChinaCloud):</span></span>
    
    ```PowerShell
    Set-AzureSubscription -SubscriptionName <Sub Name> -SubscriptionId <Sub ID> -Certificate (Get-Item Cert:\CurrentUser\My\<Cert Thrumbprint>) -Environment <AzureCloud | AzureChinaCloud>
    ```

## <a name="add-compute-node-vms"></a><span data-ttu-id="5b530-121">新增計算節點 VM</span><span class="sxs-lookup"><span data-stu-id="5b530-121">Add compute node VMs</span></span>
<span data-ttu-id="5b530-122">加入計算節點以 hello **Add-hpciaasnode.ps1**指令碼。</span><span class="sxs-lookup"><span data-stu-id="5b530-122">Add compute nodes with hello **Add-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="5b530-123">語法</span><span class="sxs-lookup"><span data-stu-id="5b530-123">Syntax</span></span>
```PowerShell
Add-HPCIaaSNode.ps1 [-ServiceName] <String> [-ImageName] <String>
 [-Quantity] <Int32> [-InstanceSize] <String> [-DomainUserName] <String> [[-DomainUserPassword] <String>]
 [[-NodeNameSeries] <String>] [<CommonParameters>]

```
### <a name="parameters"></a><span data-ttu-id="5b530-124">參數</span><span class="sxs-lookup"><span data-stu-id="5b530-124">Parameters</span></span>
* <span data-ttu-id="5b530-125">**ServiceName**: hello 新增計算節點 Vm 的雲端服務名稱加入。</span><span class="sxs-lookup"><span data-stu-id="5b530-125">**ServiceName**: Name of hello cloud service that new compute node VMs are added to.</span></span>
* <span data-ttu-id="5b530-126">**ImageName**: Azure VM 映像名稱，可透過 hello Azure 傳統入口網站或 Azure PowerShell cmdlet 取得**Get-azurevmimage**。</span><span class="sxs-lookup"><span data-stu-id="5b530-126">**ImageName**: Azure VM image name, which can be obtained through hello Azure classic portal or Azure PowerShell cmdlet **Get-AzureVMImage**.</span></span> <span data-ttu-id="5b530-127">hello 映像必須符合下列需求的 hello:</span><span class="sxs-lookup"><span data-stu-id="5b530-127">hello image must meet hello following requirements:</span></span>
  
  1. <span data-ttu-id="5b530-128">必須安裝 Windows 作業系統。</span><span class="sxs-lookup"><span data-stu-id="5b530-128">A Windows operating system must be installed.</span></span>
  2. <span data-ttu-id="5b530-129">必須安裝 HPC Pack 在 hello 運算節點角色。</span><span class="sxs-lookup"><span data-stu-id="5b530-129">HPC Pack must be installed in hello compute node role.</span></span>
  3. <span data-ttu-id="5b530-130">hello 映像必須是 hello 使用者分類，不是公用 Azure VM 映像中的私人映像。</span><span class="sxs-lookup"><span data-stu-id="5b530-130">hello image must be a private image in hello User category, not a public Azure VM image.</span></span>
* <span data-ttu-id="5b530-131">**數量**： 加入計算節點 Vm toobe 數目。</span><span class="sxs-lookup"><span data-stu-id="5b530-131">**Quantity**: Number of compute node VMs toobe added.</span></span>
* <span data-ttu-id="5b530-132">**InstanceSize**: hello 的大小計算節點 Vm。</span><span class="sxs-lookup"><span data-stu-id="5b530-132">**InstanceSize**: Size of hello compute node VMs.</span></span>
* <span data-ttu-id="5b530-133">**DomainUserName**： 網域使用者名稱，也就是使用的 toojoin hello 新 Vm toohello 網域。</span><span class="sxs-lookup"><span data-stu-id="5b530-133">**DomainUserName**: Domain user name, which is used toojoin hello new VMs toohello domain.</span></span>
* <span data-ttu-id="5b530-134">**DomainUserPassword**: hello 網域使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="5b530-134">**DomainUserPassword**: Password of hello domain user.</span></span>
* <span data-ttu-id="5b530-135">**NodeNameSeries** （選擇性）： hello 的計算節點命名模式。</span><span class="sxs-lookup"><span data-stu-id="5b530-135">**NodeNameSeries** (optional): Naming pattern for hello compute nodes.</span></span> <span data-ttu-id="5b530-136">hello 格式必須為&lt;*根\_名稱*&gt;&lt;*啟動\_數目*&gt;%。</span><span class="sxs-lookup"><span data-stu-id="5b530-136">hello format must be &lt;*Root\_Name*&gt;&lt;*Start\_Number*&gt;%.</span></span> <span data-ttu-id="5b530-137">例如，MyCN %10%表示一系列的 hello 計算從 MyCN11 開始的節點名稱。</span><span class="sxs-lookup"><span data-stu-id="5b530-137">For example, MyCN%10% means a series of hello compute node names starting from MyCN11.</span></span> <span data-ttu-id="5b530-138">如果未指定，則 hello 指令碼會使用 hello 設定 hello HPC 叢集中節點命名序列。</span><span class="sxs-lookup"><span data-stu-id="5b530-138">If not specified, hello script uses hello configured node naming series in hello HPC cluster.</span></span>

### <a name="example"></a><span data-ttu-id="5b530-139">範例</span><span class="sxs-lookup"><span data-stu-id="5b530-139">Example</span></span>
<span data-ttu-id="5b530-140">hello 下列範例會將 20 大型運算節點 Vm hello 雲端服務中*hpcservice1 中新增*根據 hello VM 映像， *hpccnimage1*。</span><span class="sxs-lookup"><span data-stu-id="5b530-140">hello following example adds 20 size Large compute node VMs in hello cloud service *hpcservice1*, based on hello VM image *hpccnimage1*.</span></span>

```PowerShell
Add-HPCIaaSNode.ps1 –ServiceName hpcservice1 –ImageName hpccniamge1
–Quantity 20 –InstanceSize Large –DomainUserName <username>
-DomainUserPassword <password>
```


## <a name="remove-compute-node-vms"></a><span data-ttu-id="5b530-141">移除計算節點 VM</span><span class="sxs-lookup"><span data-stu-id="5b530-141">Remove compute node VMs</span></span>
<span data-ttu-id="5b530-142">移除計算節點以 hello **Remove-hpciaasnode.ps1**指令碼。</span><span class="sxs-lookup"><span data-stu-id="5b530-142">Remove compute nodes with hello **Remove-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="5b530-143">語法</span><span class="sxs-lookup"><span data-stu-id="5b530-143">Syntax</span></span>
```PowerShell
Remove-HPCIaaSNode.ps1 -Name <String[]> [-DeleteVHD] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]

Remove-HPCIaaSNode.ps1 -Node <Object> [-DeleteVHD] [-Force] [-Confirm] [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="5b530-144">參數</span><span class="sxs-lookup"><span data-stu-id="5b530-144">Parameters</span></span>
* <span data-ttu-id="5b530-145">**名稱**： 移除叢集節點 toobe 的名稱。</span><span class="sxs-lookup"><span data-stu-id="5b530-145">**Name**: Names of cluster nodes toobe removed.</span></span> <span data-ttu-id="5b530-146">支援萬用字元。</span><span class="sxs-lookup"><span data-stu-id="5b530-146">Wildcards are supported.</span></span> <span data-ttu-id="5b530-147">hello 參數集名稱為 Name。</span><span class="sxs-lookup"><span data-stu-id="5b530-147">hello parameter set name is Name.</span></span> <span data-ttu-id="5b530-148">您不能指定兩個 hello**名稱**和**節點**參數。</span><span class="sxs-lookup"><span data-stu-id="5b530-148">You can't specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="5b530-149">**節點**: hello HpcNode 物件物件 hello 節點 toobe 移除，可以透過 hello HPC PowerShell cmdlet 取得[Get-hpcnode 取得](https://technet.microsoft.com/library/dn887927.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5b530-149">**Node**: hello HpcNode object for hello nodes toobe removed, which can be obtained through hello HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="5b530-150">hello 參數集名稱為節點。</span><span class="sxs-lookup"><span data-stu-id="5b530-150">hello parameter set name is Node.</span></span> <span data-ttu-id="5b530-151">您不能指定兩個 hello**名稱**和**節點**參數。</span><span class="sxs-lookup"><span data-stu-id="5b530-151">You can't specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="5b530-152">**DeleteVHD** （選擇性）： 設定 toodelete 相關聯的 hello hello 會移除的 Vm 磁碟。</span><span class="sxs-lookup"><span data-stu-id="5b530-152">**DeleteVHD** (optional): Setting toodelete hello associated disks for hello VMs that are removed.</span></span>
* <span data-ttu-id="5b530-153">**強制**（選擇性）： 移除之前，先設定 tooforce HPC 節點離線。</span><span class="sxs-lookup"><span data-stu-id="5b530-153">**Force** (optional): Setting tooforce HPC nodes offline before removing them.</span></span>
* <span data-ttu-id="5b530-154">**確認**（選擇性）： hello 命令在執行之前確認提示。</span><span class="sxs-lookup"><span data-stu-id="5b530-154">**Confirm** (optional): Prompt for confirmation before executing hello command.</span></span>
* <span data-ttu-id="5b530-155">**WhatIf**： 如果您執行 hello 命令，而不實際執行 hello 命令設定 toodescribe 什麼會發生。</span><span class="sxs-lookup"><span data-stu-id="5b530-155">**WhatIf**: Setting toodescribe what would happen if you executed hello command without actually executing hello command.</span></span>

### <a name="example"></a><span data-ttu-id="5b530-156">範例</span><span class="sxs-lookup"><span data-stu-id="5b530-156">Example</span></span>
<span data-ttu-id="5b530-157">hello 下列範例會強制離線 hello 節點名稱開頭*為 Hpcnode-cn-CN-*並加以移除 hello 節點和其相關聯的磁碟。</span><span class="sxs-lookup"><span data-stu-id="5b530-157">hello following example forces offline hello nodes with names beginning *HPCNode-CN-* and them removes hello nodes and their associated disks.</span></span>

```PowerShell
Remove-HPCIaaSNode.ps1 –Name HPCNodeCN-* –DeleteVHD -Force
```

## <a name="start-compute-node-vms"></a><span data-ttu-id="5b530-158">啟動計算節點 VM</span><span class="sxs-lookup"><span data-stu-id="5b530-158">Start compute node VMs</span></span>
<span data-ttu-id="5b530-159">開始計算節點以 hello **Start-hpciaasnode.ps1**指令碼。</span><span class="sxs-lookup"><span data-stu-id="5b530-159">Start compute nodes with hello **Start-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="5b530-160">語法</span><span class="sxs-lookup"><span data-stu-id="5b530-160">Syntax</span></span>
```PowerShell
Start-HPCIaaSNode.ps1 -Name <String[]> [<CommonParameters>]

Start-HPCIaaSNode.ps1 -Node <Object> [<CommonParameters>]
```
### <a name="parameters"></a><span data-ttu-id="5b530-161">參數</span><span class="sxs-lookup"><span data-stu-id="5b530-161">Parameters</span></span>
* <span data-ttu-id="5b530-162">**名稱**: hello 叢集節點 toobe 名稱開始。</span><span class="sxs-lookup"><span data-stu-id="5b530-162">**Name**: Names of hello cluster nodes toobe started.</span></span> <span data-ttu-id="5b530-163">支援萬用字元。</span><span class="sxs-lookup"><span data-stu-id="5b530-163">Wildcards are supported.</span></span> <span data-ttu-id="5b530-164">hello 參數集名稱為 Name。</span><span class="sxs-lookup"><span data-stu-id="5b530-164">hello parameter set name is Name.</span></span> <span data-ttu-id="5b530-165">您不能指定兩個 hello**名稱**和**節點**參數。</span><span class="sxs-lookup"><span data-stu-id="5b530-165">You cannot specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="5b530-166">**節點**-hello HpcNode 物件物件 hello 節點 toobe 啟動，可以透過 hello HPC PowerShell cmdlet 取得[Get-hpcnode 取得](https://technet.microsoft.com/library/dn887927.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5b530-166">**Node**- hello HpcNode object for hello nodes toobe started, which can be obtained through hello HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="5b530-167">hello 參數集名稱為節點。</span><span class="sxs-lookup"><span data-stu-id="5b530-167">hello parameter set name is Node.</span></span> <span data-ttu-id="5b530-168">您不能指定兩個 hello**名稱**和**節點**參數。</span><span class="sxs-lookup"><span data-stu-id="5b530-168">You cannot specify both hello **Name** and **Node** parameters.</span></span>

### <a name="example"></a><span data-ttu-id="5b530-169">範例</span><span class="sxs-lookup"><span data-stu-id="5b530-169">Example</span></span>
<span data-ttu-id="5b530-170">hello 下列範例會啟動節點名稱開頭*為 Hpcnode-cn-CN-*。</span><span class="sxs-lookup"><span data-stu-id="5b530-170">hello following example starts nodes with names beginning *HPCNode-CN-*.</span></span>

```PowerShell
Start-HPCIaaSNode.ps1 –Name HPCNodeCN-*
```

## <a name="stop-compute-node-vms"></a><span data-ttu-id="5b530-171">停止計算節點 VM</span><span class="sxs-lookup"><span data-stu-id="5b530-171">Stop compute node VMs</span></span>
<span data-ttu-id="5b530-172">停止運算節點以 hello **Stop-hpciaasnode.ps1**指令碼。</span><span class="sxs-lookup"><span data-stu-id="5b530-172">Stop compute nodes with hello **Stop-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="5b530-173">語法</span><span class="sxs-lookup"><span data-stu-id="5b530-173">Syntax</span></span>
```PowerShell
Stop-HPCIaaSNode.ps1 -Name <String[]> [-Force] [<CommonParameters>]

Stop-HPCIaaSNode.ps1 -Node <Object> [-Force] [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="5b530-174">參數</span><span class="sxs-lookup"><span data-stu-id="5b530-174">Parameters</span></span>
* <span data-ttu-id="5b530-175">**名稱**-停止 hello 叢集節點 toobe 的名稱。</span><span class="sxs-lookup"><span data-stu-id="5b530-175">**Name**- Names of hello cluster nodes toobe stopped.</span></span> <span data-ttu-id="5b530-176">支援萬用字元。</span><span class="sxs-lookup"><span data-stu-id="5b530-176">Wildcards are supported.</span></span> <span data-ttu-id="5b530-177">hello 參數集名稱為 Name。</span><span class="sxs-lookup"><span data-stu-id="5b530-177">hello parameter set name is Name.</span></span> <span data-ttu-id="5b530-178">您不能指定兩個 hello**名稱**和**節點**參數。</span><span class="sxs-lookup"><span data-stu-id="5b530-178">You cannot specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="5b530-179">**節點**: hello HpcNode 物件物件 hello 節點 toobe 停止，可以透過 hello HPC PowerShell cmdlet 取得[Get-hpcnode 取得](https://technet.microsoft.com/library/dn887927.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5b530-179">**Node**: hello HpcNode object for hello nodes toobe stopped, which can be obtained through hello HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="5b530-180">hello 參數集名稱為節點。</span><span class="sxs-lookup"><span data-stu-id="5b530-180">hello parameter set name is Node.</span></span> <span data-ttu-id="5b530-181">您不能指定兩個 hello**名稱**和**節點**參數。</span><span class="sxs-lookup"><span data-stu-id="5b530-181">You cannot specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="5b530-182">**強制**（選擇性）： 設定 tooforce HPC 節點離線之前加以停止。</span><span class="sxs-lookup"><span data-stu-id="5b530-182">**Force** (optional): Setting tooforce HPC nodes offline before stopping them.</span></span>

### <a name="example"></a><span data-ttu-id="5b530-183">範例</span><span class="sxs-lookup"><span data-stu-id="5b530-183">Example</span></span>
<span data-ttu-id="5b530-184">hello 下列範例會強制離線的節點名稱開頭*為 Hpcnode-cn-CN-*和停駐點然後 hello 節點。</span><span class="sxs-lookup"><span data-stu-id="5b530-184">hello following example forces offline nodes with names beginning *HPCNode-CN-* and then stops hello nodes.</span></span>

```PowerShell
Stop-HPCIaaSNode.ps1 –Name HPCNodeCN-* -Force
```

## <a name="next-steps"></a><span data-ttu-id="5b530-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5b530-185">Next steps</span></span>
* <span data-ttu-id="5b530-186">tooautomatically 成長或壓縮 hello 根據目前的工作負載 hello 工作及工作 hello 叢集上的叢集節點，請參閱[自動擴增和縮減 Azure 相應 toohello 叢集工作負載中helloHPCPack叢集資源](hpcpack-cluster-node-autogrowshrink.md).</span><span class="sxs-lookup"><span data-stu-id="5b530-186">tooautomatically grow or shrink hello cluster nodes according to hello current workload of jobs and tasks on hello cluster, see [Automatically grow and shrink hello HPC Pack cluster resources in Azure according toohello cluster workload](hpcpack-cluster-node-autogrowshrink.md).</span></span>

