---
title: "建立 Azure 受控磁碟的複本作為備份 | Microsoft Docs"
description: "了解如何建立 Azure 受控磁碟的複本作為備份，或用於針對磁碟問題進行疑難排解。"
documentationcenter: 
author: cwatson-cat
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 15eb778e-fc07-45ef-bdc8-9090193a6d20
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 2/9/2017
ms.author: cwatson
ms.openlocfilehash: a7527b12f4f0d2b45713a0c0109d81ff51293fd8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a><span data-ttu-id="bc8d4-103">使用受控快照集建立 VHD 的複本並儲存為 Azure 受控磁碟</span><span class="sxs-lookup"><span data-stu-id="bc8d4-103">Create a copy of a VHD stored as an Azure Managed Disk by using Managed Snapshots</span></span>
<span data-ttu-id="bc8d4-104">建立受控磁碟的快照集作為備份，或從快照集建立受控磁碟並將它附加至測試虛擬機器進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="bc8d4-104">Take a snapshot of a Managed Disk for backup or create a Managed Disk from the snapshot and attach it to a test virtual machine to troubleshoot.</span></span> <span data-ttu-id="bc8d4-105">受控快照集是 VM 受控磁碟的完整時間點複本。</span><span class="sxs-lookup"><span data-stu-id="bc8d4-105">A Managed Snapshot is a full point-in-time copy of a VM Managed Disk.</span></span> <span data-ttu-id="bc8d4-106">它會建立 VHD 的唯讀複本，而且根據預設儲存為標準受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="bc8d4-106">It creates a read-only copy of your VHD and, by default, stores it as a Standard Managed Disk.</span></span> <span data-ttu-id="bc8d4-107">如需受控磁碟的詳細資訊，請參閱 [Azure 受控磁碟概觀](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="bc8d4-107">For more information about Managed Disks, see [Azure Managed Disks overview](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

<span data-ttu-id="bc8d4-108">如需價格的詳細資訊，請參閱 [Azure 儲存體價格](https://azure.microsoft.com/pricing/details/managed-disks/)。</span><span class="sxs-lookup"><span data-stu-id="bc8d4-108">For information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/managed-disks/).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="bc8d4-109">開始之前</span><span class="sxs-lookup"><span data-stu-id="bc8d4-109">Before you begin</span></span>
<span data-ttu-id="bc8d4-110">如果您使用 PowerShell，請確定您擁有最新版的 AzureRM.Compute PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="bc8d4-110">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="bc8d4-111">執行下列命令來安裝它。</span><span class="sxs-lookup"><span data-stu-id="bc8d4-111">Run the following command to install it.</span></span>

```
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="bc8d4-112">如需詳細資訊，請參閱 [Azure PowerShell 版本控制](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="bc8d4-112">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>

## <a name="copy-the-vhd-with-a-snapshot"></a><span data-ttu-id="bc8d4-113">使用快照集複製 VHD</span><span class="sxs-lookup"><span data-stu-id="bc8d4-113">Copy the VHD with a snapshot</span></span>
<span data-ttu-id="bc8d4-114">使用 Azure 入口網站或 PowerShell 建立受控磁碟的快照集。</span><span class="sxs-lookup"><span data-stu-id="bc8d4-114">Use either the Azure portal or PowerShell to take a snapshot of the Managed Disk.</span></span>

### <a name="use-azure-portal-to-take-a-snapshot"></a><span data-ttu-id="bc8d4-115">使用 Azure 入口網站建立快照集</span><span class="sxs-lookup"><span data-stu-id="bc8d4-115">Use Azure portal to take a snapshot</span></span> 

1. <span data-ttu-id="bc8d4-116">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="bc8d4-116">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="bc8d4-117">從左上方開始，按一下 [新增]，搜尋**快照集**。</span><span class="sxs-lookup"><span data-stu-id="bc8d4-117">Starting in the upper left, click **New** and search for **snapshot**.</span></span>
3. <span data-ttu-id="bc8d4-118">在 [快照集] 刀鋒視窗中，按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="bc8d4-118">In the Snapshot blade, click **Create**.</span></span>
4. <span data-ttu-id="bc8d4-119">輸入快照集的 [名稱]。</span><span class="sxs-lookup"><span data-stu-id="bc8d4-119">Enter a **Name** for the snapshot.</span></span>
5. <span data-ttu-id="bc8d4-120">選取現有的[資源群組](../../azure-resource-manager/resource-group-overview.md#resource-groups)，或輸入新群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="bc8d4-120">Select an existing [Resource group](../../azure-resource-manager/resource-group-overview.md#resource-groups) or type the name for a new one.</span></span> 
6. <span data-ttu-id="bc8d4-121">選取 Azure 資料中心的 [位置]。</span><span class="sxs-lookup"><span data-stu-id="bc8d4-121">Select an Azure datacenter Location.</span></span>  
7. <span data-ttu-id="bc8d4-122">在 [來源磁碟] 中，選取要建立快照集的受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="bc8d4-122">For **Source disk**, select the Managed Disk to snapshot.</span></span>
8. <span data-ttu-id="bc8d4-123">選取用來儲存快照集的 [帳戶類型]。</span><span class="sxs-lookup"><span data-stu-id="bc8d4-123">Select the **Account type** to use to store the snapshot.</span></span> <span data-ttu-id="bc8d4-124">除非需要儲存在高效能磁碟上，否則建議選取 **Standard_LRS**。</span><span class="sxs-lookup"><span data-stu-id="bc8d4-124">We recommend **Standard_LRS** unless you need it stored on a high performing disk.</span></span>
9. <span data-ttu-id="bc8d4-125">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="bc8d4-125">Click **Create**.</span></span>

### <a name="use-powershell-to-take-a-snapshot"></a><span data-ttu-id="bc8d4-126">使用 PowerShell 建立快照集</span><span class="sxs-lookup"><span data-stu-id="bc8d4-126">Use PowerShell to take a snapshot</span></span>
<span data-ttu-id="bc8d4-127">下列步驟示範如何取得要複製的 VHD 磁碟、建立快照集設定，以及使用 New-AzureRmSnapshot Cmdlet<!--Add link to cmdlet when available--> 建立磁碟的快照集。</span><span class="sxs-lookup"><span data-stu-id="bc8d4-127">The following steps show you how to get the VHD disk to be copied, create the snapshot configurations, and take a snapshot of the disk by using the New-AzureRmSnapshot cmdlet<!--Add link to cmdlet when available-->.</span></span> 

1. <span data-ttu-id="bc8d4-128">設定部分參數。</span><span class="sxs-lookup"><span data-stu-id="bc8d4-128">Set some parameters.</span></span> 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$location = 'southeastasia' 
$dataDiskName = 'ContosoMD_datadisk1' 
$snapshotName = 'ContosoMD_datadisk1_snapshot1'  
```
  <span data-ttu-id="bc8d4-129">取代參數值︰</span><span class="sxs-lookup"><span data-stu-id="bc8d4-129">Replace the parameter values:</span></span>
  -  <span data-ttu-id="bc8d4-130">"myResourceGroup" 取代為 VM 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="bc8d4-130">"myResourceGroup" with the VM's resource group.</span></span>
  -  <span data-ttu-id="bc8d4-131">"southeastasia" 取代為要用來儲存受控快照集的地理位置。</span><span class="sxs-lookup"><span data-stu-id="bc8d4-131">"southeastasia" with the geographic location where you want your Managed Snapshot stored.</span></span> <!---How do you look these up? -->
  -  <span data-ttu-id="bc8d4-132">"ContosoMD_datadisk1" 取代為您想要複製的 VHD 磁碟名稱。</span><span class="sxs-lookup"><span data-stu-id="bc8d4-132">"ContosoMD_datadisk1" with the name of the VHD disk that you want to copy.</span></span>
  -  <span data-ttu-id="bc8d4-133">"ContosoMD_datadisk1_snapshot1" 取代為要用於新快照集的名稱。</span><span class="sxs-lookup"><span data-stu-id="bc8d4-133">"ContosoMD_datadisk1_snapshot1" with the name you want to use for the new snapshot.</span></span>

2. <span data-ttu-id="bc8d4-134">取得要複製的 VHD 磁碟。</span><span class="sxs-lookup"><span data-stu-id="bc8d4-134">Get the VHD disk to be copied.</span></span>

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $dataDiskName 
```
3. <span data-ttu-id="bc8d4-135">建立快照集設定。</span><span class="sxs-lookup"><span data-stu-id="bc8d4-135">Create the snapshot configurations.</span></span> 

 ```powershell
$snapshot =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -CreateOption Copy -Location $location 
```
4. <span data-ttu-id="bc8d4-136">建立快照集。</span><span class="sxs-lookup"><span data-stu-id="bc8d4-136">Take the snapshot.</span></span>

 ```powershell
New-AzureRmSnapshot -Snapshot $snapshot -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName 
```
<span data-ttu-id="bc8d4-137">如果您計劃使用快照集建立受控磁碟，並將它連結至必須是高效能的 VM，請在 New-AzureRmSnapshot 命令中使用參數 `-AccountType Premium_LRS`。</span><span class="sxs-lookup"><span data-stu-id="bc8d4-137">If you plan to use the snapshot to create a Managed Disk and attach it a VM that needs to be high performing, use the parameter `-AccountType Premium_LRS` with the New-AzureRmSnapshot command.</span></span> <span data-ttu-id="bc8d4-138">此參數建立的快照集會儲存為進階受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="bc8d4-138">The parameter creates the snapshot so that it's stored as a Premium Managed Disk.</span></span> <span data-ttu-id="bc8d4-139">進階受控磁碟的價格高於「標準」受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="bc8d4-139">Premium Managed Disks are more expensive than Standard.</span></span> <span data-ttu-id="bc8d4-140">因此，使用該參數之前，請確定您真的需要「進階」受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="bc8d4-140">So be sure you really need Premium before using that parameter.</span></span>


