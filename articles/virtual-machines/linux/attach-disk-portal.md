---
title: "將資料磁碟連結到 Linux VM | Microsoft Docs"
description: "如何在 Azure 入口網站中，使用資源管理員部署模型，將新的或現有的資料磁碟連結到 Linux VM。"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 5e1c6212-976c-4962-a297-177942f90907
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: cynthn
ms.openlocfilehash: 1599ee241c3d9fb3623ebd89ae30f2795cae1930
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-attach-a-data-disk-to-a-linux-vm-in-the-azure-portal"></a><span data-ttu-id="5a15e-103">如何在 Azure 入口網站中將資料磁碟連結到 Linux VM</span><span class="sxs-lookup"><span data-stu-id="5a15e-103">How to attach a data disk to a Linux VM in the Azure portal</span></span>
<span data-ttu-id="5a15e-104">本文示範如何透過 Azure 入口網站將新的及現有的磁碟連結到 Linux 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5a15e-104">This article shows you how to attach both new and existing disks to a Linux virtual machine through the Azure portal.</span></span> <span data-ttu-id="5a15e-105">您也可以[在 Azure 入口網站中將資料磁碟連結到 Windows VM](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="5a15e-105">You can also [attach a data disk to a Windows VM in the Azure portal](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="5a15e-106">您可以選擇使用 Azure 受控磁碟或非受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="5a15e-106">You can choose to use either Azure Managed Disks or unmanaged disks.</span></span> <span data-ttu-id="5a15e-107">受控磁碟是由 Azure 平台處理，不需要任何準備或位置來儲存它們。</span><span class="sxs-lookup"><span data-stu-id="5a15e-107">Managed disks are handled by the Azure platform and do not require any preparation or location to store them.</span></span> <span data-ttu-id="5a15e-108">非受控磁碟需要儲存體帳戶且[套用一些配額和限制](../../azure-subscription-service-limits.md#storage-limits)。</span><span class="sxs-lookup"><span data-stu-id="5a15e-108">Unmanaged disks require a storage account and have some [quotas and limits that apply](../../azure-subscription-service-limits.md#storage-limits).</span></span> <span data-ttu-id="5a15e-109">如需 Azure 受控磁碟的詳細資訊，請參閱 [Azure 受控磁碟概觀](../windows/managed-disks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="5a15e-109">For more information about Azure Managed Disks, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="5a15e-110">將磁碟附加至 VM 之前，請檢閱下列提示︰</span><span class="sxs-lookup"><span data-stu-id="5a15e-110">Before you attach disks to your VM, review these tips:</span></span>

* <span data-ttu-id="5a15e-111">虛擬機器的大小會控制您可以連接的資料磁碟數目。</span><span class="sxs-lookup"><span data-stu-id="5a15e-111">The size of the virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="5a15e-112">如需詳細資訊，請參閱 [虛擬機器的大小](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="5a15e-112">For details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="5a15e-113">若要使用進階儲存體，您需要 DS 系列或 GS 系列的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5a15e-113">To use Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="5a15e-114">您可以使用進階或標準磁碟搭配這些虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5a15e-114">You can use both Premium and Standard disks with these virtual machines.</span></span> <span data-ttu-id="5a15e-115">僅特定地區可用進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="5a15e-115">Premium storage is available in certain regions.</span></span> <span data-ttu-id="5a15e-116">如需詳細資訊，請參閱[進階儲存體：Azure 虛擬機器工作負載適用的高效能儲存體](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="5a15e-116">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="5a15e-117">附加至虛擬機器的磁碟實際上是 Azure 中儲存的 .vhd 檔案。</span><span class="sxs-lookup"><span data-stu-id="5a15e-117">Disks attached to virtual machines are actually .vhd files stored in Azure.</span></span> <span data-ttu-id="5a15e-118">如需詳細資訊，請參閱 [有關虛擬機器的磁碟和 VHD](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="5a15e-118">For details, see [About disks and VHDs for virtual machines](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="find-the-virtual-machine"></a><span data-ttu-id="5a15e-119">尋找虛擬機器</span><span class="sxs-lookup"><span data-stu-id="5a15e-119">Find the virtual machine</span></span>
1. <span data-ttu-id="5a15e-120">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="5a15e-120">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="5a15e-121">在 [中樞] 功能表上，按一下 [虛擬機器] 。</span><span class="sxs-lookup"><span data-stu-id="5a15e-121">On the Hub menu, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="5a15e-122">然後從清單中選取虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5a15e-122">Select the virtual machine from the list.</span></span>
4. <span data-ttu-id="5a15e-123">在 [虛擬機器] 刀鋒視窗上的 [程式集] 中，按一下 [磁碟]。</span><span class="sxs-lookup"><span data-stu-id="5a15e-123">To the Virtual machines blade, in **Essentials**, click **Disks**.</span></span>
   
    ![開啟磁碟設定](./media/attach-disk-portal/find-disk-settings.png)

<span data-ttu-id="5a15e-125">接著，依照指示來附加[受控磁碟](#use-azure-managed-disks)或[非受控磁碟](#use-unmanaged-disks)。</span><span class="sxs-lookup"><span data-stu-id="5a15e-125">Continue by following instructions for attaching either a [managed disk](#use-azure-managed-disks) or [unmanaged disk](#use-unmanaged-disks).</span></span>

## <a name="use-azure-managed-disks"></a><span data-ttu-id="5a15e-126">使用 Azure 受控磁碟</span><span class="sxs-lookup"><span data-stu-id="5a15e-126">Use Azure Managed Disks</span></span>

### <a name="attach-a-new-disk"></a><span data-ttu-id="5a15e-127">附加新的磁碟</span><span class="sxs-lookup"><span data-stu-id="5a15e-127">Attach a new disk</span></span>

1. <span data-ttu-id="5a15e-128">在 [磁碟] 刀鋒視窗上，按一下 [+ 新增資料磁碟]。</span><span class="sxs-lookup"><span data-stu-id="5a15e-128">On the **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="5a15e-129">按一下 [名稱] 的下拉式選單，然後選取 [建立磁碟]：</span><span class="sxs-lookup"><span data-stu-id="5a15e-129">Click the drop-down menu for **Name** and select **Create disk**:</span></span>

    ![建立 Azure 受控磁碟](./media/attach-disk-portal/create-new-md.png)

3. <span data-ttu-id="5a15e-131">輸入受控磁碟的名稱。</span><span class="sxs-lookup"><span data-stu-id="5a15e-131">Enter a name for your managed disk.</span></span> <span data-ttu-id="5a15e-132">檢閱預設設定，視需要進行更新，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="5a15e-132">Review the default settings, update as necessary, and then click **Create**.</span></span>
   
   ![檢閱磁碟設定](./media/attach-disk-portal/create-new-md-settings.png)

4. <span data-ttu-id="5a15e-134">按一下 [儲存] 以建立受控磁碟並更新 VM 組態︰</span><span class="sxs-lookup"><span data-stu-id="5a15e-134">Click **Save** to create the managed disk and update the VM configuration:</span></span>

   ![儲存新的 Azure 受控磁碟](./media/attach-disk-portal/confirm-create-new-md.png)

5. <span data-ttu-id="5a15e-136">在 Azure 建立磁碟並將其連接至虛擬機器之後，該新磁碟就會列在虛擬機器之磁碟設定中的 [資料磁碟] 底下。</span><span class="sxs-lookup"><span data-stu-id="5a15e-136">After Azure creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.</span></span> <span data-ttu-id="5a15e-137">當受控磁碟是最上層資源時，磁碟會出現在資源群組的根目錄︰</span><span class="sxs-lookup"><span data-stu-id="5a15e-137">As managed disks are a top-level resource, the disk appears at the root of the resource group:</span></span>

   ![資源群組中的 Azure 受控磁碟](./media/attach-disk-portal/view-md-resource-group.png)

### <a name="attach-an-existing-disk"></a><span data-ttu-id="5a15e-139">連接現有磁碟</span><span class="sxs-lookup"><span data-stu-id="5a15e-139">Attach an existing disk</span></span>
1. <span data-ttu-id="5a15e-140">在 [磁碟] 刀鋒視窗上，按一下 [+ 新增資料磁碟]。</span><span class="sxs-lookup"><span data-stu-id="5a15e-140">On the **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="5a15e-141">按一下 [名稱] 的下拉式選單，以檢視您的 Azure 訂用帳戶可存取的現有受控磁碟清單。</span><span class="sxs-lookup"><span data-stu-id="5a15e-141">Click the drop-down menu for **Name** to view a list of existing managed disks accessible to your Azure subscription.</span></span> <span data-ttu-id="5a15e-142">選取要附加的受控磁碟︰</span><span class="sxs-lookup"><span data-stu-id="5a15e-142">Select the managed disk to attach:</span></span>

   ![附加現有的 Azure 受控磁碟](./media/attach-disk-portal/select-existing-md.png)

3. <span data-ttu-id="5a15e-144">按一下 [儲存] 以附加現有的受控磁碟並更新 VM 組態︰</span><span class="sxs-lookup"><span data-stu-id="5a15e-144">Click **Save** to attach the existing managed disk and update the VM configuration:</span></span>
   
   ![儲存 Azure 受控磁碟更新](./media/attach-disk-portal/confirm-attach-existing-md.png)

4. <span data-ttu-id="5a15e-146">Azure 將磁碟連接至虛擬機器之後，該磁碟會列在虛擬機器磁碟設定中的 [資料磁碟] 下面。</span><span class="sxs-lookup"><span data-stu-id="5a15e-146">After Azure attaches the disk to the virtual machine, it's listed in the virtual machine's disk settings under **Data Disks**.</span></span>

## <a name="use-unmanaged-disks"></a><span data-ttu-id="5a15e-147">使用非受控磁碟</span><span class="sxs-lookup"><span data-stu-id="5a15e-147">Use unmanaged disks</span></span>

### <a name="attach-a-new-disk"></a><span data-ttu-id="5a15e-148">附加新的磁碟</span><span class="sxs-lookup"><span data-stu-id="5a15e-148">Attach a new disk</span></span>

1. <span data-ttu-id="5a15e-149">在 [磁碟] 刀鋒視窗上，按一下 [+ 新增資料磁碟]。</span><span class="sxs-lookup"><span data-stu-id="5a15e-149">On the **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="5a15e-150">檢閱預設設定，視需要進行更新，然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="5a15e-150">Review the default settings, update as necessary, and then click **OK**.</span></span>
   
   ![檢閱磁碟設定](./media/attach-disk-portal/attach-new.png)
3. <span data-ttu-id="5a15e-152">在 Azure 建立磁碟並將其連接至虛擬機器之後，該新磁碟就會列在虛擬機器之磁碟設定中的 [資料磁碟] 底下。</span><span class="sxs-lookup"><span data-stu-id="5a15e-152">After Azure creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.</span></span>

### <a name="attach-an-existing-disk"></a><span data-ttu-id="5a15e-153">連接現有磁碟</span><span class="sxs-lookup"><span data-stu-id="5a15e-153">Attach an existing disk</span></span>
1. <span data-ttu-id="5a15e-154">在 [磁碟] 刀鋒視窗上，按一下 [+ 新增資料磁碟]。</span><span class="sxs-lookup"><span data-stu-id="5a15e-154">On the **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="5a15e-155">在 [連結現有磁碟] 底下，按一下 [VHD 檔案]。</span><span class="sxs-lookup"><span data-stu-id="5a15e-155">Under **Attach existing disk**, click **VHD File**.</span></span>
   
   ![連接現有磁碟](./media/attach-disk-portal/attach-existing.png)
3. <span data-ttu-id="5a15e-157">在 [儲存體帳戶] 底下，選取持有該 .vhd 檔案的帳戶和容器。</span><span class="sxs-lookup"><span data-stu-id="5a15e-157">Under **Storage accounts**, select the account and container that holds the .vhd file.</span></span>
   
   ![尋找 VHD 位置](./media/attach-disk-portal/find-storage-container.png)
4. <span data-ttu-id="5a15e-159">選取 .vhd 檔案。</span><span class="sxs-lookup"><span data-stu-id="5a15e-159">Select the .vhd file.</span></span>
5. <span data-ttu-id="5a15e-160">在 [連結現有磁碟] 底下，您剛才選取的檔案會列在 [VHD 檔案] 底下。</span><span class="sxs-lookup"><span data-stu-id="5a15e-160">Under **Attach existing disk**, the file you just selected is listed under **VHD File**.</span></span> <span data-ttu-id="5a15e-161">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="5a15e-161">Click **OK**.</span></span>
6. <span data-ttu-id="5a15e-162">Azure 將磁碟連接至虛擬機器之後，該磁碟會列在虛擬機器磁碟設定中的 [資料磁碟] 下面。</span><span class="sxs-lookup"><span data-stu-id="5a15e-162">After Azure attaches the disk to the virtual machine, it's listed in the virtual machine's disk settings under **Data Disks**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="5a15e-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5a15e-163">Next steps</span></span>
<span data-ttu-id="5a15e-164">加入磁碟後，您需要準備它以便使用。</span><span class="sxs-lookup"><span data-stu-id="5a15e-164">After the disk is added, you need to prepare it for use.</span></span> <span data-ttu-id="5a15e-165">如需詳細資訊，請參閱這篇[做法：在 Linux 中初始化新的資料磁碟](add-disk.md)。</span><span class="sxs-lookup"><span data-stu-id="5a15e-165">For more information, see [How to: Initialize a new data disk in Linux](add-disk.md).</span></span>
