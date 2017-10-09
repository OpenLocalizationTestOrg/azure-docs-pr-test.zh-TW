---
title: "未受管理的資料磁碟 tooa Windows VM-Azure aaaAttach |Microsoft 文件"
description: "如何 tooattach 新的或現有的 unmanaged 的資料磁碟 tooa Windows VM 在 Azure 入口網站中，使用 hello hello Resource Manager 部署模型。"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3790fc59-7264-41df-b7a3-8d1226799885
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: cynthn
ms.openlocfilehash: 923a6663974143bf359970f9b0eb0d36cabcba9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-an-unmanaged-data-disk-tooa-windows-vm-in-hello-azure-portal"></a><span data-ttu-id="5b340-103">Tooattach 未受管理的資料磁碟 tooa Windows VM hello Azure 入口網站中的方式</span><span class="sxs-lookup"><span data-stu-id="5b340-103">How tooattach an unmanaged data disk tooa Windows VM in hello Azure portal</span></span>

<span data-ttu-id="5b340-104">本文將說明 tooattach 新的和現有的受管理磁碟 tooWindows 透過 hello Azure 入口網站的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5b340-104">This article shows you how tooattach both new and existing unmanaged disks tooWindows virtual machines through hello Azure portal.</span></span> <span data-ttu-id="5b340-105">您也可以[使用 PowerShell 連結資料磁碟](./attach-disk-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="5b340-105">You can also [attach a data disk using PowerShell](./attach-disk-ps.md).</span></span> <span data-ttu-id="5b340-106">這麼做之前，請先檢閱下列提示：</span><span class="sxs-lookup"><span data-stu-id="5b340-106">Before you do this, review these tips:</span></span>

* <span data-ttu-id="5b340-107">hello hello 虛擬機器大小會控制您可以將附加的資料磁碟數目。</span><span class="sxs-lookup"><span data-stu-id="5b340-107">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="5b340-108">如需詳細資訊，請參閱 [虛擬機器的大小](sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="5b340-108">For details, see [Sizes for virtual machines](sizes.md).</span></span>
* <span data-ttu-id="5b340-109">toouse 高階儲存體，您需要將 DS 系列或 GS 系列虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5b340-109">toouse Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="5b340-110">您可以使用進階或標準儲存體帳戶的磁碟搭配這些虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5b340-110">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="5b340-111">僅特定地區可用進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="5b340-111">Premium storage is available in certain regions.</span></span> <span data-ttu-id="5b340-112">如需詳細資訊，請參閱[進階儲存體：Azure 虛擬機器工作負載適用的高效能儲存體](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="5b340-112">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="5b340-113">對於新的磁碟，您不需要 toocreate 它第一次因為 Azure 會建立它時將它附加。</span><span class="sxs-lookup"><span data-stu-id="5b340-113">For a new disk, you don't need toocreate it first because Azure creates it when you attach it.</span></span>


<span data-ttu-id="5b340-114">您也可以[使用 Powershell 連接資料磁碟](attach-disk-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="5b340-114">You can also [attach a data disk using Powershell](attach-disk-ps.md).</span></span>


## <a name="find-hello-virtual-machine"></a><span data-ttu-id="5b340-115">尋找 hello 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="5b340-115">Find hello virtual machine</span></span>
1. <span data-ttu-id="5b340-116">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="5b340-116">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="5b340-117">在左側 hello hello 功能表上，按一下**虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="5b340-117">In hello menu on hello left, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="5b340-118">從 [hello] 清單中選取 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5b340-118">Select hello virtual machine from hello list.</span></span>
4. <span data-ttu-id="5b340-119">在 hello 虛擬機器刀鋒視窗中，按一下 **磁碟**。</span><span class="sxs-lookup"><span data-stu-id="5b340-119">In hello Virtual machines blade, click **Disks**.</span></span>
   
<span data-ttu-id="5b340-120">接著，依照指示來連接[新的磁碟](#option-1-attach-a-new-disk)或[現有的磁碟](#option-2-attach-an-existing-disk)。</span><span class="sxs-lookup"><span data-stu-id="5b340-120">Continue by following instructions for attaching either a [new disk](#option-1-attach-a-new-disk) or an [existing disk](#option-2-attach-an-existing-disk).</span></span>

## <a name="option-1-attach-and-initialize-a-new-disk"></a><span data-ttu-id="5b340-121">選項 1：連接新磁碟並進行初始化</span><span class="sxs-lookup"><span data-stu-id="5b340-121">Option 1: Attach and initialize a new disk</span></span>
1. <span data-ttu-id="5b340-122">在 hello**磁碟**刀鋒視窗中，按一下  **+ 新增資料磁碟**。</span><span class="sxs-lookup"><span data-stu-id="5b340-122">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="5b340-123">在 hello**附加受管理的磁碟**刀鋒視窗中，輸入的名稱中的 hello 磁碟**名稱**，然後選取  **（空的磁碟） 新增**中**來源類型**。</span><span class="sxs-lookup"><span data-stu-id="5b340-123">In hello **Attach managed disk** blade, type a name for hello disk in **Name** and then select **New (empty disk)** in **Source type**.</span></span>
3. <span data-ttu-id="5b340-124">在下**儲存體容器**，按一下 hello**瀏覽**按鈕，然後瀏覽 toohello 儲存體帳戶和容器，您會在其中喜歡 hello 儲存新 VHD toobe，然後按一下**選取**.</span><span class="sxs-lookup"><span data-stu-id="5b340-124">Under **Storage container**, click hello **Browse** button and browse toohello storage account and container where you would like hello new VHD toobe stored and then click **Select**.</span></span> 
  
   ![檢閱磁碟設定](./media/attach-disk-portal/attach-empty-unmanaged.png)
   
3. <span data-ttu-id="5b340-126">當您完成 hello hello 資料磁碟的設定之後時，按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="5b340-126">When you are done with hello settings for hello data disk, click **OK**.</span></span>
4. <span data-ttu-id="5b340-127">在 hello**磁碟**刀鋒視窗中，按一下 **儲存**tooadd hello 磁碟 toohello VM 組態。</span><span class="sxs-lookup"><span data-stu-id="5b340-127">Back in hello **Disks** blade, click **Save** tooadd hello disk toohello VM configuration.</span></span>


### <a name="initialize-a-new-data-disk"></a><span data-ttu-id="5b340-128">初始化新的資料磁碟</span><span class="sxs-lookup"><span data-stu-id="5b340-128">Initialize a new data disk</span></span>

1. <span data-ttu-id="5b340-129">Toohello 虛擬機器連線。</span><span class="sxs-lookup"><span data-stu-id="5b340-129">Connect toohello virtual machine.</span></span> <span data-ttu-id="5b340-130">如需指示，請參閱[如何 tooconnect 和登入 tooan Azure 虛擬機器執行 Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="5b340-130">For instructions, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
1. <span data-ttu-id="5b340-131">按一下 hello**啟動**hello VM 和型別內的功能表**diskmgmt.msc**並點擊**Enter**。</span><span class="sxs-lookup"><span data-stu-id="5b340-131">Click hello **Start** menu inside hello VM and type **diskmgmt.msc** and hit **Enter**.</span></span> <span data-ttu-id="5b340-132">這樣會啟動 hello 磁碟管理嵌入式管理單元。</span><span class="sxs-lookup"><span data-stu-id="5b340-132">This starts hello Disk Management snap-in.</span></span>
2. <span data-ttu-id="5b340-133">磁碟管理會辨識您有新的、 未初始化的磁碟 hello 初始化磁碟 視窗會隨即快顯。</span><span class="sxs-lookup"><span data-stu-id="5b340-133">Disk Management recognizes that you have a new, uninitialized disk and hello Initialize Disk window will pop up.</span></span>
3. <span data-ttu-id="5b340-134">請確定已選取 hello 新磁碟，然後按一下**確定**tooinitialize 它。</span><span class="sxs-lookup"><span data-stu-id="5b340-134">Make sure hello new disk is selected and click **OK** tooinitialize it.</span></span>
4. <span data-ttu-id="5b340-135">hello 新磁碟隨即顯示當做**未配置**。</span><span class="sxs-lookup"><span data-stu-id="5b340-135">hello new disk now appears as **unallocated**.</span></span> <span data-ttu-id="5b340-136">Hello 磁碟上按一下滑鼠右鍵，然後選取**新增簡單磁碟區**。</span><span class="sxs-lookup"><span data-stu-id="5b340-136">Right-click anywhere on hello disk and select **New simple volume**.</span></span> <span data-ttu-id="5b340-137">hello**新增簡單磁碟區精靈**啟動。</span><span class="sxs-lookup"><span data-stu-id="5b340-137">hello **New Simple Volume Wizard** starts.</span></span>
5. <span data-ttu-id="5b340-138">透過 hello 」 精靈，將所有 hello 預設值，當您完成選取移**完成**。</span><span class="sxs-lookup"><span data-stu-id="5b340-138">Go through hello wizard, keeping all of hello defaults, when you are done select **Finish**.</span></span>
6. <span data-ttu-id="5b340-139">關閉磁碟管理。</span><span class="sxs-lookup"><span data-stu-id="5b340-139">Close Disk Management.</span></span>
7. <span data-ttu-id="5b340-140">您會得到快顯視窗，您可以使用它之前，需要 tooformat hello 新磁碟。</span><span class="sxs-lookup"><span data-stu-id="5b340-140">You get a pop-up that you need tooformat hello new disk before you can use it.</span></span> <span data-ttu-id="5b340-141">按一下 [格式化磁碟]。</span><span class="sxs-lookup"><span data-stu-id="5b340-141">Click **Format disk**.</span></span>
8. <span data-ttu-id="5b340-142">在 hello**格式新磁碟**對話方塊檢查 hello 設定，然後按一下**啟動**。</span><span class="sxs-lookup"><span data-stu-id="5b340-142">In hello **Format new disk** dialog, check hello settings and then click **Start**.</span></span>
9. <span data-ttu-id="5b340-143">您會收到警告，格式化 hello 磁碟會清除所有 hello 資料，請按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="5b340-143">You get a warning that formatting hello disks erases all of hello data, click **OK**.</span></span>
10. <span data-ttu-id="5b340-144">完成 hello 格式時，按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="5b340-144">When hello format is complete, click **OK**.</span></span>


## <a name="option-2-attach-an-existing-disk"></a><span data-ttu-id="5b340-145">選項 2：連接現有磁碟</span><span class="sxs-lookup"><span data-stu-id="5b340-145">Option 2: Attach an existing disk</span></span>
1. <span data-ttu-id="5b340-146">在 hello**磁碟**刀鋒視窗中，按一下  **+ 新增資料磁碟**。</span><span class="sxs-lookup"><span data-stu-id="5b340-146">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="5b340-147">在 hello**連接未受管理的磁碟**刀鋒視窗，請在**來源類型**選取**現有 blob**。</span><span class="sxs-lookup"><span data-stu-id="5b340-147">On hello **Attach unmanaged disk** blade, in **Source type** select **Existing blob**.</span></span>

    ![檢閱磁碟設定](./media/attach-disk-portal/attach-existing-unmanaged.png)

    3. <span data-ttu-id="5b340-149">按一下**瀏覽**toonavigate toohello 儲存體帳戶和容器 hello 現有 VHD 的位置。</span><span class="sxs-lookup"><span data-stu-id="5b340-149">Click **Browse** toonavigate toohello storage account and container where hello existing VHD is located.</span></span> <span data-ttu-id="5b340-150">按一下並 hello VHD，然後按一下**選取**。</span><span class="sxs-lookup"><span data-stu-id="5b340-150">Click and hello VHD and then click **Select**.</span></span>
4. <span data-ttu-id="5b340-151">按一下**確定**在 hello**附加 unmanaged 的磁碟**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="5b340-151">Click **OK** in hello **Attach unmanaged disk** blade.</span></span>
5. <span data-ttu-id="5b340-152">在 hello**磁碟**刀鋒視窗中，按一下 **儲存**tooadd hello 磁碟 toohello 組態 hello VM。</span><span class="sxs-lookup"><span data-stu-id="5b340-152">In hello **Disks** blade, click **Save** tooadd hello disk toohello configuration for hello VM.</span></span>
   


## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="5b340-153">搭配使用 TRIM 與標準儲存體</span><span class="sxs-lookup"><span data-stu-id="5b340-153">Use TRIM with standard storage</span></span>

<span data-ttu-id="5b340-154">如果您使用標準儲存體 (HDD)，您應該啟用 TRIM。</span><span class="sxs-lookup"><span data-stu-id="5b340-154">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="5b340-155">空白位置修剪會捨棄 hello 磁碟上未使用的區塊，因此您只支付您實際使用的儲存體。</span><span class="sxs-lookup"><span data-stu-id="5b340-155">TRIM discards unused blocks on hello disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="5b340-156">如果您建立大型檔案，然後將它們刪除，這便可節省成本。</span><span class="sxs-lookup"><span data-stu-id="5b340-156">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="5b340-157">您可以執行此命令 toocheck hello 修剪設定。</span><span class="sxs-lookup"><span data-stu-id="5b340-157">You can run this command toocheck hello TRIM setting.</span></span> <span data-ttu-id="5b340-158">在您的 Windows VM 上開啟命令提示字元並輸入︰</span><span class="sxs-lookup"><span data-stu-id="5b340-158">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="5b340-159">Hello 命令傳回 0，如果已正確啟用修剪。</span><span class="sxs-lookup"><span data-stu-id="5b340-159">If hello command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="5b340-160">如果它傳回 1，執行下列命令 tooenable TRIM hello:</span><span class="sxs-lookup"><span data-stu-id="5b340-160">If it returns 1, run hello following command tooenable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

<span data-ttu-id="5b340-161">從磁碟中刪除資料之後, 您就可以確保 hello 修剪作業排清正確藉由執行磁碟重組與修剪：</span><span class="sxs-lookup"><span data-stu-id="5b340-161">After deleting data from your disk, you can ensure hello TRIM operations flush properly by running defrag with TRIM:</span></span>

```
defrag.exe <volume:> -l
```

<span data-ttu-id="5b340-162">您也可以確保修剪 hello 整個磁碟區格式化 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="5b340-162">You can also ensure hello entire volume is trimmed by formatting hello volume.</span></span>


## <a name="next-steps"></a><span data-ttu-id="5b340-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5b340-163">Next steps</span></span>
<span data-ttu-id="5b340-164">如果您的應用程式需要 toouse hello d： 磁碟機 toostore 資料時，您可以[變更 hello hello Windows 暫存磁碟的磁碟機代號](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="5b340-164">If you application needs toouse hello D: drive toostore data, you can [change hello drive letter of hello Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

