---
title: "資料磁碟 tooa Linux VM aaaAttach |Microsoft 文件"
description: "如何 tooattach 新的或現有的資料磁碟 tooa Linux VM 在 Azure 入口網站中，使用 hello hello Resource Manager 部署模型。"
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
ms.openlocfilehash: 069c3c6f5e71a8c495342e6d0c6f3d92c4ed5053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-data-disk-tooa-linux-vm-in-hello-azure-portal"></a><span data-ttu-id="1ca21-103">Tooattach 資料磁碟 tooa Linux VM hello Azure 入口網站中的方式</span><span class="sxs-lookup"><span data-stu-id="1ca21-103">How tooattach a data disk tooa Linux VM in hello Azure portal</span></span>
<span data-ttu-id="1ca21-104">本文章將示範如何 tooattach 新的和現有磁碟 tooa Linux 虛擬機器透過 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="1ca21-104">This article shows you how tooattach both new and existing disks tooa Linux virtual machine through hello Azure portal.</span></span> <span data-ttu-id="1ca21-105">您也可以[附加 hello Azure 入口網站中的資料磁碟 tooa Windows VM](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="1ca21-105">You can also [attach a data disk tooa Windows VM in hello Azure portal](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="1ca21-106">您可以選擇 toouse 任一 Azure 受管理磁碟或受管理的磁碟。</span><span class="sxs-lookup"><span data-stu-id="1ca21-106">You can choose toouse either Azure Managed Disks or unmanaged disks.</span></span> <span data-ttu-id="1ca21-107">受管理的磁碟都由 hello Azure 平台，而且不需要任何準備或位置 toostore 它們。</span><span class="sxs-lookup"><span data-stu-id="1ca21-107">Managed disks are handled by hello Azure platform and do not require any preparation or location toostore them.</span></span> <span data-ttu-id="1ca21-108">非受控磁碟需要儲存體帳戶且[套用一些配額和限制](../../azure-subscription-service-limits.md#storage-limits)。</span><span class="sxs-lookup"><span data-stu-id="1ca21-108">Unmanaged disks require a storage account and have some [quotas and limits that apply](../../azure-subscription-service-limits.md#storage-limits).</span></span> <span data-ttu-id="1ca21-109">如需 Azure 受控磁碟的詳細資訊，請參閱 [Azure 受控磁碟概觀](../windows/managed-disks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="1ca21-109">For more information about Azure Managed Disks, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="1ca21-110">附加磁碟 tooyour VM 之前，請先檢閱下列提示：</span><span class="sxs-lookup"><span data-stu-id="1ca21-110">Before you attach disks tooyour VM, review these tips:</span></span>

* <span data-ttu-id="1ca21-111">hello hello 虛擬機器大小會控制您可以將附加的資料磁碟數目。</span><span class="sxs-lookup"><span data-stu-id="1ca21-111">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="1ca21-112">如需詳細資訊，請參閱 [虛擬機器的大小](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="1ca21-112">For details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="1ca21-113">toouse 高階儲存體，您需要將 DS 系列或 GS 系列虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1ca21-113">toouse Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="1ca21-114">您可以使用進階或標準磁碟搭配這些虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1ca21-114">You can use both Premium and Standard disks with these virtual machines.</span></span> <span data-ttu-id="1ca21-115">僅特定地區可用進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="1ca21-115">Premium storage is available in certain regions.</span></span> <span data-ttu-id="1ca21-116">如需詳細資訊，請參閱[進階儲存體：Azure 虛擬機器工作負載適用的高效能儲存體](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="1ca21-116">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="1ca21-117">磁碟附加的 toovirtual 機器是實際的.vhd 檔案儲存在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="1ca21-117">Disks attached toovirtual machines are actually .vhd files stored in Azure.</span></span> <span data-ttu-id="1ca21-118">如需詳細資訊，請參閱 [有關虛擬機器的磁碟和 VHD](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="1ca21-118">For details, see [About disks and VHDs for virtual machines](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="find-hello-virtual-machine"></a><span data-ttu-id="1ca21-119">尋找 hello 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="1ca21-119">Find hello virtual machine</span></span>
1. <span data-ttu-id="1ca21-120">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="1ca21-120">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1ca21-121">在 hello 中樞功能表中，按一下 **虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="1ca21-121">On hello Hub menu, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="1ca21-122">從 [hello] 清單中選取 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1ca21-122">Select hello virtual machine from hello list.</span></span>
4. <span data-ttu-id="1ca21-123">toohello 虛擬機器刀鋒視窗中，在**Essentials**，按一下 **磁碟**。</span><span class="sxs-lookup"><span data-stu-id="1ca21-123">toohello Virtual machines blade, in **Essentials**, click **Disks**.</span></span>
   
    ![開啟磁碟設定](./media/attach-disk-portal/find-disk-settings.png)

<span data-ttu-id="1ca21-125">接著，依照指示來附加[受控磁碟](#use-azure-managed-disks)或[非受控磁碟](#use-unmanaged-disks)。</span><span class="sxs-lookup"><span data-stu-id="1ca21-125">Continue by following instructions for attaching either a [managed disk](#use-azure-managed-disks) or [unmanaged disk](#use-unmanaged-disks).</span></span>

## <a name="use-azure-managed-disks"></a><span data-ttu-id="1ca21-126">使用 Azure 受控磁碟</span><span class="sxs-lookup"><span data-stu-id="1ca21-126">Use Azure Managed Disks</span></span>

### <a name="attach-a-new-disk"></a><span data-ttu-id="1ca21-127">附加新的磁碟</span><span class="sxs-lookup"><span data-stu-id="1ca21-127">Attach a new disk</span></span>

1. <span data-ttu-id="1ca21-128">在 hello**磁碟**刀鋒視窗中，按一下  **+ 新增資料磁碟**。</span><span class="sxs-lookup"><span data-stu-id="1ca21-128">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="1ca21-129">按一下 hello 下拉式選單，如**名稱**選取**建立磁碟**:</span><span class="sxs-lookup"><span data-stu-id="1ca21-129">Click hello drop-down menu for **Name** and select **Create disk**:</span></span>

    ![建立 Azure 受控磁碟](./media/attach-disk-portal/create-new-md.png)

3. <span data-ttu-id="1ca21-131">輸入受控磁碟的名稱。</span><span class="sxs-lookup"><span data-stu-id="1ca21-131">Enter a name for your managed disk.</span></span> <span data-ttu-id="1ca21-132">檢閱 hello 預設設定，如有必要，更新，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="1ca21-132">Review hello default settings, update as necessary, and then click **Create**.</span></span>
   
   ![檢閱磁碟設定](./media/attach-disk-portal/create-new-md-settings.png)

4. <span data-ttu-id="1ca21-134">按一下**儲存**toocreate hello 管理磁碟和更新的 hello VM 組態：</span><span class="sxs-lookup"><span data-stu-id="1ca21-134">Click **Save** toocreate hello managed disk and update hello VM configuration:</span></span>

   ![儲存新的 Azure 受控磁碟](./media/attach-disk-portal/confirm-create-new-md.png)

5. <span data-ttu-id="1ca21-136">Azure 會建立 hello 磁碟，並將其附加 toohello 虛擬機器之後下, hello 虛擬機器的磁碟設定 中列為 hello 新磁碟**資料磁碟**。</span><span class="sxs-lookup"><span data-stu-id="1ca21-136">After Azure creates hello disk and attaches it toohello virtual machine, hello new disk is listed in hello virtual machine's disk settings under **Data Disks**.</span></span> <span data-ttu-id="1ca21-137">由於受管理的磁碟是最上層資源，hello 磁碟隨即顯示 hello 資源群組的 hello 根目錄：</span><span class="sxs-lookup"><span data-stu-id="1ca21-137">As managed disks are a top-level resource, hello disk appears at hello root of hello resource group:</span></span>

   ![資源群組中的 Azure 受控磁碟](./media/attach-disk-portal/view-md-resource-group.png)

### <a name="attach-an-existing-disk"></a><span data-ttu-id="1ca21-139">連接現有磁碟</span><span class="sxs-lookup"><span data-stu-id="1ca21-139">Attach an existing disk</span></span>
1. <span data-ttu-id="1ca21-140">在 hello**磁碟**刀鋒視窗中，按一下  **+ 新增資料磁碟**。</span><span class="sxs-lookup"><span data-stu-id="1ca21-140">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="1ca21-141">按一下 hello 下拉式選單，如**名稱**tooview 的現有清單管理磁碟存取 tooyour Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1ca21-141">Click hello drop-down menu for **Name** tooview a list of existing managed disks accessible tooyour Azure subscription.</span></span> <span data-ttu-id="1ca21-142">選取受管理的 hello 磁碟 tooattach:</span><span class="sxs-lookup"><span data-stu-id="1ca21-142">Select hello managed disk tooattach:</span></span>

   ![附加現有的 Azure 受控磁碟](./media/attach-disk-portal/select-existing-md.png)

3. <span data-ttu-id="1ca21-144">按一下**儲存**tooattach hello 現有受管理磁碟和更新的 hello VM 組態：</span><span class="sxs-lookup"><span data-stu-id="1ca21-144">Click **Save** tooattach hello existing managed disk and update hello VM configuration:</span></span>
   
   ![儲存 Azure 受控磁碟更新](./media/attach-disk-portal/confirm-attach-existing-md.png)

4. <span data-ttu-id="1ca21-146">Azure 將 hello 磁碟 toohello 虛擬機器之後，它會列在下方的 hello 虛擬機器的磁碟設定**資料磁碟**。</span><span class="sxs-lookup"><span data-stu-id="1ca21-146">After Azure attaches hello disk toohello virtual machine, it's listed in hello virtual machine's disk settings under **Data Disks**.</span></span>

## <a name="use-unmanaged-disks"></a><span data-ttu-id="1ca21-147">使用非受控磁碟</span><span class="sxs-lookup"><span data-stu-id="1ca21-147">Use unmanaged disks</span></span>

### <a name="attach-a-new-disk"></a><span data-ttu-id="1ca21-148">附加新的磁碟</span><span class="sxs-lookup"><span data-stu-id="1ca21-148">Attach a new disk</span></span>

1. <span data-ttu-id="1ca21-149">在 hello**磁碟**刀鋒視窗中，按一下  **+ 新增資料磁碟**。</span><span class="sxs-lookup"><span data-stu-id="1ca21-149">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="1ca21-150">檢閱 hello 預設設定，如有必要，更新，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="1ca21-150">Review hello default settings, update as necessary, and then click **OK**.</span></span>
   
   ![檢閱磁碟設定](./media/attach-disk-portal/attach-new.png)
3. <span data-ttu-id="1ca21-152">Azure 會建立 hello 磁碟，並將其附加 toohello 虛擬機器之後下, hello 虛擬機器的磁碟設定 中列為 hello 新磁碟**資料磁碟**。</span><span class="sxs-lookup"><span data-stu-id="1ca21-152">After Azure creates hello disk and attaches it toohello virtual machine, hello new disk is listed in hello virtual machine's disk settings under **Data Disks**.</span></span>

### <a name="attach-an-existing-disk"></a><span data-ttu-id="1ca21-153">連接現有磁碟</span><span class="sxs-lookup"><span data-stu-id="1ca21-153">Attach an existing disk</span></span>
1. <span data-ttu-id="1ca21-154">在 hello**磁碟**刀鋒視窗中，按一下  **+ 新增資料磁碟**。</span><span class="sxs-lookup"><span data-stu-id="1ca21-154">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="1ca21-155">在 [連結現有磁碟] 底下，按一下 [VHD 檔案]。</span><span class="sxs-lookup"><span data-stu-id="1ca21-155">Under **Attach existing disk**, click **VHD File**.</span></span>
   
   ![連接現有磁碟](./media/attach-disk-portal/attach-existing.png)
3. <span data-ttu-id="1ca21-157">在下**儲存體帳戶**，選取 hello 帳戶和容器，其中含有 hello.vhd 檔案。</span><span class="sxs-lookup"><span data-stu-id="1ca21-157">Under **Storage accounts**, select hello account and container that holds hello .vhd file.</span></span>
   
   ![尋找 VHD 位置](./media/attach-disk-portal/find-storage-container.png)
4. <span data-ttu-id="1ca21-159">選取 hello.vhd 檔案。</span><span class="sxs-lookup"><span data-stu-id="1ca21-159">Select hello .vhd file.</span></span>
5. <span data-ttu-id="1ca21-160">在下**將現有磁碟**，您只選取的 hello 檔案列在**VHD 檔案**。</span><span class="sxs-lookup"><span data-stu-id="1ca21-160">Under **Attach existing disk**, hello file you just selected is listed under **VHD File**.</span></span> <span data-ttu-id="1ca21-161">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="1ca21-161">Click **OK**.</span></span>
6. <span data-ttu-id="1ca21-162">Azure 將 hello 磁碟 toohello 虛擬機器之後，它會列在下方的 hello 虛擬機器的磁碟設定**資料磁碟**。</span><span class="sxs-lookup"><span data-stu-id="1ca21-162">After Azure attaches hello disk toohello virtual machine, it's listed in hello virtual machine's disk settings under **Data Disks**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1ca21-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1ca21-163">Next steps</span></span>
<span data-ttu-id="1ca21-164">加入 hello 磁碟之後，您需要 tooprepare 它供使用。</span><span class="sxs-lookup"><span data-stu-id="1ca21-164">After hello disk is added, you need tooprepare it for use.</span></span> <span data-ttu-id="1ca21-165">如需詳細資訊，請參閱這篇[做法：在 Linux 中初始化新的資料磁碟](add-disk.md)。</span><span class="sxs-lookup"><span data-stu-id="1ca21-165">For more information, see [How to: Initialize a new data disk in Linux](add-disk.md).</span></span>
