---
title: "Azure 受管理磁碟備份的複本 aaaCreate |Microsoft 文件"
description: "了解如何 toocreate 回最新或疑難排解磁碟 Azure 受管理磁碟 toouse 一份問題。"
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
ms.openlocfilehash: 2f33dbbee624bcd813f3c7c3e3401072d0933714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a><span data-ttu-id="086f8-103">使用受控快照集建立 VHD 的複本並儲存為 Azure 受控磁碟</span><span class="sxs-lookup"><span data-stu-id="086f8-103">Create a copy of a VHD stored as an Azure Managed Disk by using Managed Snapshots</span></span>
<span data-ttu-id="086f8-104">取得備份的受管理磁碟的快照或從 hello 快照集建立受管理磁碟並將它附加 tooa 測試虛擬機器 tootroubleshoot。</span><span class="sxs-lookup"><span data-stu-id="086f8-104">Take a snapshot of a Managed Disk for backup or create a Managed Disk from hello snapshot and attach it tooa test virtual machine tootroubleshoot.</span></span> <span data-ttu-id="086f8-105">受控快照集是 VM 受控磁碟的完整時間點複本。</span><span class="sxs-lookup"><span data-stu-id="086f8-105">A Managed Snapshot is a full point-in-time copy of a VM Managed Disk.</span></span> <span data-ttu-id="086f8-106">它會建立 VHD 的唯讀複本，而且根據預設儲存為標準受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="086f8-106">It creates a read-only copy of your VHD and, by default, stores it as a Standard Managed Disk.</span></span> <span data-ttu-id="086f8-107">如需受控磁碟的詳細資訊，請參閱 [Azure 受控磁碟概觀](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="086f8-107">For more information about Managed Disks, see [Azure Managed Disks overview](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

<span data-ttu-id="086f8-108">如需價格的詳細資訊，請參閱 [Azure 儲存體價格](https://azure.microsoft.com/pricing/details/managed-disks/)。</span><span class="sxs-lookup"><span data-stu-id="086f8-108">For information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/managed-disks/).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="086f8-109">開始之前</span><span class="sxs-lookup"><span data-stu-id="086f8-109">Before you begin</span></span>
<span data-ttu-id="086f8-110">如果您使用 PowerShell，請確定您擁有 hello hello AzureRM.Compute PowerShell 模組最新版本。</span><span class="sxs-lookup"><span data-stu-id="086f8-110">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="086f8-111">執行 hello 下列命令 tooinstall 它。</span><span class="sxs-lookup"><span data-stu-id="086f8-111">Run hello following command tooinstall it.</span></span>

```
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="086f8-112">如需詳細資訊，請參閱 [Azure PowerShell 版本控制](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="086f8-112">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>

## <a name="copy-hello-vhd-with-a-snapshot"></a><span data-ttu-id="086f8-113">使用快照集複製 hello VHD</span><span class="sxs-lookup"><span data-stu-id="086f8-113">Copy hello VHD with a snapshot</span></span>
<span data-ttu-id="086f8-114">使用 hello Azure 入口網站或 PowerShell tootake hello 受管理磁碟的快照集。</span><span class="sxs-lookup"><span data-stu-id="086f8-114">Use either hello Azure portal or PowerShell tootake a snapshot of hello Managed Disk.</span></span>

### <a name="use-azure-portal-tootake-a-snapshot"></a><span data-ttu-id="086f8-115">使用 Azure 入口網站 tootake 快照集</span><span class="sxs-lookup"><span data-stu-id="086f8-115">Use Azure portal tootake a snapshot</span></span> 

1. <span data-ttu-id="086f8-116">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="086f8-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="086f8-117">從開始 hello 左上方，按一下**新增**並搜尋**快照**。</span><span class="sxs-lookup"><span data-stu-id="086f8-117">Starting in hello upper left, click **New** and search for **snapshot**.</span></span>
3. <span data-ttu-id="086f8-118">在 hello 快照刀鋒視窗中，按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="086f8-118">In hello Snapshot blade, click **Create**.</span></span>
4. <span data-ttu-id="086f8-119">輸入**名稱**hello 快照集。</span><span class="sxs-lookup"><span data-stu-id="086f8-119">Enter a **Name** for hello snapshot.</span></span>
5. <span data-ttu-id="086f8-120">選取現有[資源群組](../../azure-resource-manager/resource-group-overview.md#resource-groups)或新的型別 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="086f8-120">Select an existing [Resource group](../../azure-resource-manager/resource-group-overview.md#resource-groups) or type hello name for a new one.</span></span> 
6. <span data-ttu-id="086f8-121">選取 Azure 資料中心的 [位置]。</span><span class="sxs-lookup"><span data-stu-id="086f8-121">Select an Azure datacenter Location.</span></span>  
7. <span data-ttu-id="086f8-122">如**來源磁碟**，選取 hello toosnapshot 管理的磁碟。</span><span class="sxs-lookup"><span data-stu-id="086f8-122">For **Source disk**, select hello Managed Disk toosnapshot.</span></span>
8. <span data-ttu-id="086f8-123">選取 hello**帳戶類型**toouse toostore hello 快照集。</span><span class="sxs-lookup"><span data-stu-id="086f8-123">Select hello **Account type** toouse toostore hello snapshot.</span></span> <span data-ttu-id="086f8-124">除非需要儲存在高效能磁碟上，否則建議選取 **Standard_LRS**。</span><span class="sxs-lookup"><span data-stu-id="086f8-124">We recommend **Standard_LRS** unless you need it stored on a high performing disk.</span></span>
9. <span data-ttu-id="086f8-125">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="086f8-125">Click **Create**.</span></span>

### <a name="use-powershell-tootake-a-snapshot"></a><span data-ttu-id="086f8-126">使用 PowerShell tootake 快照集</span><span class="sxs-lookup"><span data-stu-id="086f8-126">Use PowerShell tootake a snapshot</span></span>
<span data-ttu-id="086f8-127">hello 下列步驟顯示如何 tooget hello VHD 磁碟 toobe 複製、 建立 hello 快照設定及取得 hello 磁碟的快照集使用 hello 新增 AzureRmSnapshot cmdlet<!--Add link toocmdlet when available-->。</span><span class="sxs-lookup"><span data-stu-id="086f8-127">hello following steps show you how tooget hello VHD disk toobe copied, create hello snapshot configurations, and take a snapshot of hello disk by using hello New-AzureRmSnapshot cmdlet<!--Add link toocmdlet when available-->.</span></span> 

1. <span data-ttu-id="086f8-128">設定部分參數。</span><span class="sxs-lookup"><span data-stu-id="086f8-128">Set some parameters.</span></span> 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$location = 'southeastasia' 
$dataDiskName = 'ContosoMD_datadisk1' 
$snapshotName = 'ContosoMD_datadisk1_snapshot1'  
```
  <span data-ttu-id="086f8-129">取代 hello 參數值：</span><span class="sxs-lookup"><span data-stu-id="086f8-129">Replace hello parameter values:</span></span>
  -  <span data-ttu-id="086f8-130">「 myResourceGroup"hello VM 資源群組。</span><span class="sxs-lookup"><span data-stu-id="086f8-130">"myResourceGroup" with hello VM's resource group.</span></span>
  -  <span data-ttu-id="086f8-131">「 southeastasia"與 hello 管理快照集儲存所在的地理位置。</span><span class="sxs-lookup"><span data-stu-id="086f8-131">"southeastasia" with hello geographic location where you want your Managed Snapshot stored.</span></span> <!---How do you look these up? -->
  -  <span data-ttu-id="086f8-132">「 ContosoMD_datadisk1"hello 名稱與您想 toocopy hello VHD 磁碟。</span><span class="sxs-lookup"><span data-stu-id="086f8-132">"ContosoMD_datadisk1" with hello name of hello VHD disk that you want toocopy.</span></span>
  -  <span data-ttu-id="086f8-133">「 ContosoMD_datadisk1_snapshot1"hello 命名您想 toouse hello 新快照集。</span><span class="sxs-lookup"><span data-stu-id="086f8-133">"ContosoMD_datadisk1_snapshot1" with hello name you want toouse for hello new snapshot.</span></span>

2. <span data-ttu-id="086f8-134">收到 hello VHD 磁碟 toobe 複製。</span><span class="sxs-lookup"><span data-stu-id="086f8-134">Get hello VHD disk toobe copied.</span></span>

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $dataDiskName 
```
3. <span data-ttu-id="086f8-135">建立 hello 快照集設定。</span><span class="sxs-lookup"><span data-stu-id="086f8-135">Create hello snapshot configurations.</span></span> 

 ```powershell
$snapshot =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -CreateOption Copy -Location $location 
```
4. <span data-ttu-id="086f8-136">取得 hello 快照集。</span><span class="sxs-lookup"><span data-stu-id="086f8-136">Take hello snapshot.</span></span>

 ```powershell
New-AzureRmSnapshot -Snapshot $snapshot -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName 
```
<span data-ttu-id="086f8-137">如果您規劃 toouse hello 快照 toocreate 受管理的磁碟，並將它附加 toobe 高執行所需的 VM，使用 hello 參數`-AccountType Premium_LRS`hello 新增 AzureRmSnapshot 命令。</span><span class="sxs-lookup"><span data-stu-id="086f8-137">If you plan toouse hello snapshot toocreate a Managed Disk and attach it a VM that needs toobe high performing, use hello parameter `-AccountType Premium_LRS` with hello New-AzureRmSnapshot command.</span></span> <span data-ttu-id="086f8-138">hello 參數建立 hello 快照集，使它儲存為 Premium 管理磁碟。</span><span class="sxs-lookup"><span data-stu-id="086f8-138">hello parameter creates hello snapshot so that it's stored as a Premium Managed Disk.</span></span> <span data-ttu-id="086f8-139">進階受控磁碟的價格高於「標準」受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="086f8-139">Premium Managed Disks are more expensive than Standard.</span></span> <span data-ttu-id="086f8-140">因此，使用該參數之前，請確定您真的需要「進階」受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="086f8-140">So be sure you really need Premium before using that parameter.</span></span>


