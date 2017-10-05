---
title: "管理 HPC Pack 叢集計算節點 |Microsoft Docs"
description: "了解可在 Azure 中新增、移除、啟動和停止 HPC Pack 2012 R2 叢集計算節點的 PowerShell 指令碼工具"
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
ms.openlocfilehash: dc9f354191b9e80ff6a01bd401a874c6998bda79
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-the-number-and-availability-of-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="c1ba3-103">在 Azure 的 HPC Pack 叢集中管理計算節點的數目和可用性</span><span class="sxs-lookup"><span data-stu-id="c1ba3-103">Manage the number and availability of compute nodes in an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="c1ba3-104">如果您已在 Azure VM 中建立 HPC Pack 2012 R2 叢集，您可能會需要可輕易地在叢集中新增、移除、啟動 (佈建) 或停止 (解除佈建) 一些計算節點 VM 的方法。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-104">If you created an HPC Pack 2012 R2 cluster in Azure VMs, you might want ways to easily add, remove, start (provision), or stop (deprovision) some compute node VMs in the cluster.</span></span> <span data-ttu-id="c1ba3-105">若要執行這些工作，請執行安裝在前端節點 VM 上的 Azure PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-105">To do these tasks, run Azure PowerShell scripts that are installed on the head node VM.</span></span> <span data-ttu-id="c1ba3-106">這些指令碼可協助您控制 HPC Pack 叢集資源的數目和可用性，讓您得以控制成本。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-106">These scripts help you control the number and availability of your HPC Pack cluster resources so you can control costs.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="c1ba3-107">本文適用於 Azure 中使用傳統部署模型建立的 HPC Pack 2012 R2 叢集。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-107">This article applies only to HPC Pack 2012 R2 clusters in Azure created using the classic deployment model.</span></span> <span data-ttu-id="c1ba3-108">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>
> <span data-ttu-id="c1ba3-109">此外，本文中所述的 PowerShell 指令碼不適用於 HPC Pack 2016。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-109">In addition, the PowerShell scripts described in this article are not available in HPC Pack 2016.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1ba3-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="c1ba3-110">Prerequisites</span></span>
* <span data-ttu-id="c1ba3-111">**Azure VM 中的 HPC Pack 2012 R2 叢集**：在傳統部署模型中建立 HPC Pack 2012 R2 叢集。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-111">**HPC Pack 2012 R2 cluster in Azure VMs**: Create an HPC Pack 2012 R2 cluster in the classic deployment model.</span></span> <span data-ttu-id="c1ba3-112">例如，您可以使用 Azure Marketplace 中的 HPC Pack 2012 R2 VM 映像和 Azure PowerShell 指令碼，將部署自動化。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-112">For example, you can automate the deployment by using the HPC Pack 2012 R2 VM image in the Azure Marketplace and an Azure PowerShell script.</span></span> <span data-ttu-id="c1ba3-113">如需相關資訊和必要條件，請參閱[使用 HPC Pack IaaS 部署指令碼建立 HPC 叢集](hpcpack-cluster-powershell-script.md)。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-113">For information and prerequisites, see [Create an HPC Cluster with the HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md).</span></span>
  
    <span data-ttu-id="c1ba3-114">部署之後，會在前端節點的 %CCP\_HOME%bin 資料夾中發現節點管理指令碼。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-114">After deployment, find the node management scripts in the %CCP\_HOME%bin folder on the head node.</span></span> <span data-ttu-id="c1ba3-115">以系統管理員身分執行每個指令碼。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-115">Run each of the scripts as an administrator.</span></span>
* <span data-ttu-id="c1ba3-116">**Azure 發佈設定檔或管理憑證**：您必須前端節點上執行下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="c1ba3-116">**Azure publish settings file or management certificate**: You need to do one of the following on the head node:</span></span>
  
  * <span data-ttu-id="c1ba3-117">**匯入 Azure 發佈設定檔**。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-117">**Import the Azure publish settings file**.</span></span> <span data-ttu-id="c1ba3-118">若要這麼做，請在前端節點上執行下列 Azure PowerShell Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="c1ba3-118">To do this, run the following Azure PowerShell cmdlets on the head node:</span></span>
    
    ```PowerShell
    Get-AzurePublishSettingsFile
    
    Import-AzurePublishSettingsFile –PublishSettingsFile <publish settings file>
    ```
  * <span data-ttu-id="c1ba3-119">**前端節點上設定 Azure 管理憑證**。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-119">**Configure the Azure management certificate on the head node**.</span></span> <span data-ttu-id="c1ba3-120">如果您有 .cer 檔案，請在 CurrentUser\My certificate store 中將其匯入，並為您的 Azure 環境 (AzureCloud 或 AzureChinaCloud) 執行下列 Azure PowerShell Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="c1ba3-120">If you have the .cer file, import it in the CurrentUser\My certificate store and then run the following Azure PowerShell cmdlet for your Azure environment (either AzureCloud or AzureChinaCloud):</span></span>
    
    ```PowerShell
    Set-AzureSubscription -SubscriptionName <Sub Name> -SubscriptionId <Sub ID> -Certificate (Get-Item Cert:\CurrentUser\My\<Cert Thrumbprint>) -Environment <AzureCloud | AzureChinaCloud>
    ```

## <a name="add-compute-node-vms"></a><span data-ttu-id="c1ba3-121">新增計算節點 VM</span><span class="sxs-lookup"><span data-stu-id="c1ba3-121">Add compute node VMs</span></span>
<span data-ttu-id="c1ba3-122">使用 **Add-HpcIaaSNode.ps1** 指令碼新增計算節點。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-122">Add compute nodes with the **Add-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="c1ba3-123">語法</span><span class="sxs-lookup"><span data-stu-id="c1ba3-123">Syntax</span></span>
```PowerShell
Add-HPCIaaSNode.ps1 [-ServiceName] <String> [-ImageName] <String>
 [-Quantity] <Int32> [-InstanceSize] <String> [-DomainUserName] <String> [[-DomainUserPassword] <String>]
 [[-NodeNameSeries] <String>] [<CommonParameters>]

```
### <a name="parameters"></a><span data-ttu-id="c1ba3-124">參數</span><span class="sxs-lookup"><span data-stu-id="c1ba3-124">Parameters</span></span>
* <span data-ttu-id="c1ba3-125">**ServiceName**：會新增計算節點 VM 之雲端服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-125">**ServiceName**: Name of the cloud service that new compute node VMs are added to.</span></span>
* <span data-ttu-id="c1ba3-126">**ImageName**：Azure VM 映像名稱，透過 Azure 傳統入口網站或 Azure PowerShell Cmdlet **Get-AzureVMImage** 可以取得此名稱。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-126">**ImageName**: Azure VM image name, which can be obtained through the Azure classic portal or Azure PowerShell cmdlet **Get-AzureVMImage**.</span></span> <span data-ttu-id="c1ba3-127">這些映像必須符合下列需求：</span><span class="sxs-lookup"><span data-stu-id="c1ba3-127">The image must meet the following requirements:</span></span>
  
  1. <span data-ttu-id="c1ba3-128">必須安裝 Windows 作業系統。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-128">A Windows operating system must be installed.</span></span>
  2. <span data-ttu-id="c1ba3-129">必須在計算節點角色中安裝 HPC Pack。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-129">HPC Pack must be installed in the compute node role.</span></span>
  3. <span data-ttu-id="c1ba3-130">映像必須是使用者類別中的私人映像，而不是公用 Azure VM 映像。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-130">The image must be a private image in the User category, not a public Azure VM image.</span></span>
* <span data-ttu-id="c1ba3-131">**Quantity**：要新增的計算節點 VM 數目。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-131">**Quantity**: Number of compute node VMs to be added.</span></span>
* <span data-ttu-id="c1ba3-132">**InstanceSize**：計算節點 VM 的大小。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-132">**InstanceSize**: Size of the compute node VMs.</span></span>
* <span data-ttu-id="c1ba3-133">**DomainUserName**：網域使用者名稱，用來將新的 VM 加入網域中。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-133">**DomainUserName**: Domain user name, which is used to join the new VMs to the domain.</span></span>
* <span data-ttu-id="c1ba3-134">**DomainUserPassword**：網域使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-134">**DomainUserPassword**: Password of the domain user.</span></span>
* <span data-ttu-id="c1ba3-135">**NodeNameSeries** (選用)：計算節點的命名模式。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-135">**NodeNameSeries** (optional): Naming pattern for the compute nodes.</span></span> <span data-ttu-id="c1ba3-136">格式必須為 &lt;*Root\_Name*&gt;&lt;*Start\_Number*&gt;%。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-136">The format must be &lt;*Root\_Name*&gt;&lt;*Start\_Number*&gt;%.</span></span> <span data-ttu-id="c1ba3-137">例如，MyCN%10% 表示從 MyCN11 開始的一系列計算節點名稱。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-137">For example, MyCN%10% means a series of the compute node names starting from MyCN11.</span></span> <span data-ttu-id="c1ba3-138">如果未指定，指令碼會使用 HPC 叢集中已設定的節點命名序列。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-138">If not specified, the script uses the configured node naming series in the HPC cluster.</span></span>

### <a name="example"></a><span data-ttu-id="c1ba3-139">範例</span><span class="sxs-lookup"><span data-stu-id="c1ba3-139">Example</span></span>
<span data-ttu-id="c1ba3-140">下列範例會根據 VM 映像 *hpccnimage1*，在雲端服務 *hpcservice1* 中新增 20 個大型計算節點 VM。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-140">The following example adds 20 size Large compute node VMs in the cloud service *hpcservice1*, based on the VM image *hpccnimage1*.</span></span>

```PowerShell
Add-HPCIaaSNode.ps1 –ServiceName hpcservice1 –ImageName hpccniamge1
–Quantity 20 –InstanceSize Large –DomainUserName <username>
-DomainUserPassword <password>
```


## <a name="remove-compute-node-vms"></a><span data-ttu-id="c1ba3-141">移除計算節點 VM</span><span class="sxs-lookup"><span data-stu-id="c1ba3-141">Remove compute node VMs</span></span>
<span data-ttu-id="c1ba3-142">使用 **Remove-HpcIaaSNode.ps1** 指令碼移除計算節點。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-142">Remove compute nodes with the **Remove-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="c1ba3-143">語法</span><span class="sxs-lookup"><span data-stu-id="c1ba3-143">Syntax</span></span>
```PowerShell
Remove-HPCIaaSNode.ps1 -Name <String[]> [-DeleteVHD] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]

Remove-HPCIaaSNode.ps1 -Node <Object> [-DeleteVHD] [-Force] [-Confirm] [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="c1ba3-144">參數</span><span class="sxs-lookup"><span data-stu-id="c1ba3-144">Parameters</span></span>
* <span data-ttu-id="c1ba3-145">**Name**：要移除之叢集節點的名稱。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-145">**Name**: Names of cluster nodes to be removed.</span></span> <span data-ttu-id="c1ba3-146">支援萬用字元。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-146">Wildcards are supported.</span></span> <span data-ttu-id="c1ba3-147">參數集名稱是 Name。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-147">The parameter set name is Name.</span></span> <span data-ttu-id="c1ba3-148">您無法同時指定 **Name** 和 **Node** 參數。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-148">You can't specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="c1ba3-149">**Node**：要移除之節點的 HpcNode 物件，可透過 HPC PowerShell Cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx)取得。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-149">**Node**: The HpcNode object for the nodes to be removed, which can be obtained through the HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="c1ba3-150">參數集名稱是 Node。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-150">The parameter set name is Node.</span></span> <span data-ttu-id="c1ba3-151">您無法同時指定 **Name** 和 **Node** 參數。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-151">You can't specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="c1ba3-152">**DeleteVHD** (選擇性)：針對已移除的 VM 進行相關磁碟的刪除時所使用的設定。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-152">**DeleteVHD** (optional): Setting to delete the associated disks for the VMs that are removed.</span></span>
* <span data-ttu-id="c1ba3-153">**Force** (選擇性)：在移除 HPC 節點前強制使其離線的設定。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-153">**Force** (optional): Setting to force HPC nodes offline before removing them.</span></span>
* <span data-ttu-id="c1ba3-154">**Confirm** (選擇性)：執行命令前先行確認的提示。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-154">**Confirm** (optional): Prompt for confirmation before executing the command.</span></span>
* <span data-ttu-id="c1ba3-155">**WhatIf**：用來說明您所執行的命令未實際執行時將會有何狀況的設定。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-155">**WhatIf**: Setting to describe what would happen if you executed the command without actually executing the command.</span></span>

### <a name="example"></a><span data-ttu-id="c1ba3-156">範例</span><span class="sxs-lookup"><span data-stu-id="c1ba3-156">Example</span></span>
<span data-ttu-id="c1ba3-157">下列範例會使名稱開頭為 *HPCNode-CN-* 的節點強制離線，然後移除節點及其相關聯的磁碟。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-157">The following example forces offline the nodes with names beginning *HPCNode-CN-* and them removes the nodes and their associated disks.</span></span>

```PowerShell
Remove-HPCIaaSNode.ps1 –Name HPCNodeCN-* –DeleteVHD -Force
```

## <a name="start-compute-node-vms"></a><span data-ttu-id="c1ba3-158">啟動計算節點 VM</span><span class="sxs-lookup"><span data-stu-id="c1ba3-158">Start compute node VMs</span></span>
<span data-ttu-id="c1ba3-159">使用 **Start-HpcIaaSNode.ps1** 指令碼啟動計算節點。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-159">Start compute nodes with the **Start-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="c1ba3-160">語法</span><span class="sxs-lookup"><span data-stu-id="c1ba3-160">Syntax</span></span>
```PowerShell
Start-HPCIaaSNode.ps1 -Name <String[]> [<CommonParameters>]

Start-HPCIaaSNode.ps1 -Node <Object> [<CommonParameters>]
```
### <a name="parameters"></a><span data-ttu-id="c1ba3-161">參數</span><span class="sxs-lookup"><span data-stu-id="c1ba3-161">Parameters</span></span>
* <span data-ttu-id="c1ba3-162">**Name**：要啟動之叢集節點的名稱。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-162">**Name**: Names of the cluster nodes to be started.</span></span> <span data-ttu-id="c1ba3-163">支援萬用字元。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-163">Wildcards are supported.</span></span> <span data-ttu-id="c1ba3-164">參數集名稱是 Name。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-164">The parameter set name is Name.</span></span> <span data-ttu-id="c1ba3-165">您無法同時指定 **Name** 和 **Node** 參數。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-165">You cannot specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="c1ba3-166">**Node**- 要啟動之節點的 HpcNode 物件，可透過 HPC PowerShell Cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx)取得。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-166">**Node**- The HpcNode object for the nodes to be started, which can be obtained through the HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="c1ba3-167">參數集名稱是 Node。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-167">The parameter set name is Node.</span></span> <span data-ttu-id="c1ba3-168">您無法同時指定 **Name** 和 **Node** 參數。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-168">You cannot specify both the **Name** and **Node** parameters.</span></span>

### <a name="example"></a><span data-ttu-id="c1ba3-169">範例</span><span class="sxs-lookup"><span data-stu-id="c1ba3-169">Example</span></span>
<span data-ttu-id="c1ba3-170">下列範例會啟動名稱開頭為 *HPCNode-CN-*的節點。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-170">The following example starts nodes with names beginning *HPCNode-CN-*.</span></span>

```PowerShell
Start-HPCIaaSNode.ps1 –Name HPCNodeCN-*
```

## <a name="stop-compute-node-vms"></a><span data-ttu-id="c1ba3-171">停止計算節點 VM</span><span class="sxs-lookup"><span data-stu-id="c1ba3-171">Stop compute node VMs</span></span>
<span data-ttu-id="c1ba3-172">使用 **Stop-HpcIaaSNode.ps1** 指令碼停止計算節點。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-172">Stop compute nodes with the **Stop-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="c1ba3-173">語法</span><span class="sxs-lookup"><span data-stu-id="c1ba3-173">Syntax</span></span>
```PowerShell
Stop-HPCIaaSNode.ps1 -Name <String[]> [-Force] [<CommonParameters>]

Stop-HPCIaaSNode.ps1 -Node <Object> [-Force] [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="c1ba3-174">參數</span><span class="sxs-lookup"><span data-stu-id="c1ba3-174">Parameters</span></span>
* <span data-ttu-id="c1ba3-175">**Name**- 要停止之叢集節點的名稱。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-175">**Name**- Names of the cluster nodes to be stopped.</span></span> <span data-ttu-id="c1ba3-176">支援萬用字元。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-176">Wildcards are supported.</span></span> <span data-ttu-id="c1ba3-177">參數集名稱是 Name。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-177">The parameter set name is Name.</span></span> <span data-ttu-id="c1ba3-178">您無法同時指定 **Name** 和 **Node** 參數。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-178">You cannot specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="c1ba3-179">**Node**：要停止之節點的 HpcNode 物件，可透過 HPC PowerShell Cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx)取得。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-179">**Node**: The HpcNode object for the nodes to be stopped, which can be obtained through the HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="c1ba3-180">參數集名稱是 Node。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-180">The parameter set name is Node.</span></span> <span data-ttu-id="c1ba3-181">您無法同時指定 **Name** 和 **Node** 參數。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-181">You cannot specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="c1ba3-182">**Force** (選擇性)：在停止 HPC 節點前強制使其離線的設定。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-182">**Force** (optional): Setting to force HPC nodes offline before stopping them.</span></span>

### <a name="example"></a><span data-ttu-id="c1ba3-183">範例</span><span class="sxs-lookup"><span data-stu-id="c1ba3-183">Example</span></span>
<span data-ttu-id="c1ba3-184">下列範例會使名稱開頭為 *HPCNode-CN-* 的節點強制離線，然後停止節點。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-184">The following example forces offline nodes with names beginning *HPCNode-CN-* and then stops the nodes.</span></span>

```PowerShell
Stop-HPCIaaSNode.ps1 –Name HPCNodeCN-* -Force
```

## <a name="next-steps"></a><span data-ttu-id="c1ba3-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c1ba3-185">Next steps</span></span>
* <span data-ttu-id="c1ba3-186">若要根據叢集上目前工作的工作負載，自動增加或縮減叢集節點的方法，請參閱[在 Azure 中根據叢集工作負載自動增加和縮減 HPC Pack 叢集資源](hpcpack-cluster-node-autogrowshrink.md)。</span><span class="sxs-lookup"><span data-stu-id="c1ba3-186">To automatically grow or shrink the cluster nodes according to the current workload of jobs and tasks on the cluster, see [Automatically grow and shrink the HPC Pack cluster resources in Azure according to the cluster workload](hpcpack-cluster-node-autogrowshrink.md).</span></span>

