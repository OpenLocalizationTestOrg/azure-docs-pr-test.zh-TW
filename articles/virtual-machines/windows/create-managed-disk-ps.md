---
title: "從 VHD 在 Azure 中的受管理磁碟 aaaCreate |Microsoft 文件"
description: "從 Azure 儲存體帳戶，目前正在使用 hello Resource Manager 部署模型的 VHD 建立受管理的磁碟。"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/05/2017
ms.author: cynthn
ms.openlocfilehash: 77adaac5419186ff85039fe2c4752f021aa5e448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-managed-disks-from-unmanaged-disks-in-a-storage-account"></a><span data-ttu-id="ab83c-103">從儲存體帳戶中的非受控磁碟建立受控磁碟</span><span class="sxs-lookup"><span data-stu-id="ab83c-103">Create managed disks from unmanaged disks in a storage account</span></span>

<span data-ttu-id="ab83c-104">您可以從現有的資料磁碟或 Azure 儲存體帳戶中目前的 OS 磁碟，建立受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="ab83c-104">A managed disk can be created from an existing data disk or an OS disk that is currently in an Azure storage account.</span></span> <span data-ttu-id="ab83c-105">您也可建立空的磁碟，以便作為 VM 的新資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="ab83c-105">You can also create an empty disk that can be used as a new data disk for a VM.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="ab83c-106">開始之前</span><span class="sxs-lookup"><span data-stu-id="ab83c-106">Before you begin</span></span>
<span data-ttu-id="ab83c-107">如果您使用 PowerShell，請確定您擁有 hello hello AzureRM.Compute PowerShell 模組最新版本。</span><span class="sxs-lookup"><span data-stu-id="ab83c-107">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="ab83c-108">執行 hello 下列命令 tooinstall 它。</span><span class="sxs-lookup"><span data-stu-id="ab83c-108">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="ab83c-109">如需詳細資訊，請參閱 [Azure PowerShell 版本控制](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="ab83c-109">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="create-a-managed-disk-from-a-vhd-in-an-azure-storage-account"></a><span data-ttu-id="ab83c-110">從 Azure 儲存體帳戶中的 VHD 建立受控映像</span><span class="sxs-lookup"><span data-stu-id="ab83c-110">Create a managed disk from a VHD in an Azure storage account</span></span>

<span data-ttu-id="ab83c-111">在我們的為受管理磁碟的 VHD 建立磁碟，並將它指派 toohello 參數 hello 範例**$disk1** toouse 更新版本。</span><span class="sxs-lookup"><span data-stu-id="ab83c-111">In hello example we create a disk from a VHD as managed disk and assign it toohello parameter **$disk1** toouse later.</span></span> 

<span data-ttu-id="ab83c-112">hello 受管理的磁碟將會建立在 hello **West US**位置，請在資源群組名稱**myResourceGroup**。</span><span class="sxs-lookup"><span data-stu-id="ab83c-112">hello managed disk will be created in hello **West-US** location, in a resource group named **myResourceGroup**.</span></span> <span data-ttu-id="ab83c-113">將名為 hello 磁碟**myDisk** ，將會建立名為的 VHD 檔案從**myDisk.vhd**我們先前上傳 tooa 儲存體帳戶**mystorageaccount**。</span><span class="sxs-lookup"><span data-stu-id="ab83c-113">hello disk will be named **myDisk** and it will be created from a VHD file named **myDisk.vhd** we previously uploaded tooa storage account named **mystorageaccount**.</span></span> <span data-ttu-id="ab83c-114">高階本機備援儲存體 (LRS) 中，將會建立 hello 受管理的磁碟。</span><span class="sxs-lookup"><span data-stu-id="ab83c-114">hello managed disk will be created in premium locally-redundant storage (LRS).</span></span> <span data-ttu-id="ab83c-115">StandardLRS 和 PremiumLRS 是只 hello **-AccountType**選項可用於管理的磁碟。</span><span class="sxs-lookup"><span data-stu-id="ab83c-115">StandardLRS and PremiumLRS are hello only **-AccountType** options available for managed disks.</span></span> 

1.  <span data-ttu-id="ab83c-116">設定一些參數</span><span class="sxs-lookup"><span data-stu-id="ab83c-116">Set some parameters</span></span>

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $diskName = "myDisk"
    $vhdUri = "https://mystorageaccount.blob.core.windows.net/vhds/myDisk.vhd"
    ```

2. <span data-ttu-id="ab83c-117">建立 hello 資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="ab83c-117">Create hello data disk.</span></span> 
    ```powershell
    $disk1 = New-AzureRmDisk -DiskName $diskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $vhdUri) -ResourceGroupName $rgName
    ```
    
    

## <a name="create-an-empty-data-disk-as-a-managed-disk"></a><span data-ttu-id="ab83c-118">建立空的資料磁碟作為受控磁碟</span><span class="sxs-lookup"><span data-stu-id="ab83c-118">Create an empty data disk as a managed disk</span></span>

<span data-ttu-id="ab83c-119">在 hello 範例中我們建立空的資料磁碟做為受管理的磁碟，並將它指派 toohello 參數**$dataDisk2** toouse 更新版本。</span><span class="sxs-lookup"><span data-stu-id="ab83c-119">In hello example we create an empty data disk as managed disk and assign it toohello parameter **$dataDisk2** toouse later.</span></span> <span data-ttu-id="ab83c-120">空的資料磁碟需要 toobe 初始化登入 toohello VM，並使用 diskmgmt.msc 或[使用 WinRM 和指令碼](attach-disk-ps.md#initialize-the-disk)，一旦附加的 tooa 執行 VM。</span><span class="sxs-lookup"><span data-stu-id="ab83c-120">An empty data disk will need toobe initialized logging in toohello VM and using diskmgmt.msc or [remotely using WinRM and a script](attach-disk-ps.md#initialize-the-disk), once it is attached tooa running VM.</span></span>

<span data-ttu-id="ab83c-121">hello 空的資料磁碟將會建立在 hello**中央美國西部**位置，請在資源群組名稱**myResourceGroup**。</span><span class="sxs-lookup"><span data-stu-id="ab83c-121">hello empty data disk will be created in hello **West Central US** location, in a resource group named **myResourceGroup**.</span></span> <span data-ttu-id="ab83c-122">將名為 hello 磁碟**myEmptyDataDisk**。</span><span class="sxs-lookup"><span data-stu-id="ab83c-122">hello disk will be named **myEmptyDataDisk**.</span></span> <span data-ttu-id="ab83c-123">高階本機備援儲存體 (LRS) 中，將會建立 hello 空的磁碟。</span><span class="sxs-lookup"><span data-stu-id="ab83c-123">hello empty disk will be created in premium locally-redundant storage (LRS).</span></span> <span data-ttu-id="ab83c-124">StandardLRS 和 PremiumLRS 是只 hello **-AccountType**選項可用於管理的磁碟。</span><span class="sxs-lookup"><span data-stu-id="ab83c-124">StandardLRS and PremiumLRS are hello only **-AccountType** options available for managed disks.</span></span>

<span data-ttu-id="ab83c-125">在此範例中的 hello 磁碟大小為 128 GB，但您應選擇符合您的 VM 上執行任何應用程式的 hello 需求的大小。</span><span class="sxs-lookup"><span data-stu-id="ab83c-125">hello disk size in this example is 128GB, but you should choose a size that meets hello needs of any applications running on your VM.</span></span>

1.  <span data-ttu-id="ab83c-126">設定一些參數</span><span class="sxs-lookup"><span data-stu-id="ab83c-126">Set some parameters</span></span>

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $dataDiskName = "myEmptyDataDisk"
    ```

2. <span data-ttu-id="ab83c-127">建立 hello 資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="ab83c-127">Create hello data disk.</span></span>
    ```powershell
    $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Empty -DiskSizeGB 128) -ResourceGroupName $rgName
    ```
    
## <a name="next-steps"></a><span data-ttu-id="ab83c-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ab83c-128">Next Steps</span></span>   
- <span data-ttu-id="ab83c-129">如果您已經有 VM，即可[附加資料磁碟](attach-disk-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="ab83c-129">If you already have a VM, you can [attach a data disk](attach-disk-portal.md).</span></span>
