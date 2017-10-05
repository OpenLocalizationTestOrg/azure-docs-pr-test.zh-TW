---
title: "將未受管理的資料磁碟連結到 Windows VM - Azure | Microsoft Docs"
description: "如何在 Azure 入口網站中使用 Resource Manager 部署模型，將新的或現有的未受管理資料磁碟連結到 Windows VM。"
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
ms.openlocfilehash: c0886302c82641f8cc1a00d3972870d58ba8afb4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-attach-an-unmanaged-data-disk-to-a-windows-vm-in-the-azure-portal"></a><span data-ttu-id="a0d86-103">如何在 Azure 入口網站中將未受管理的資料磁碟連結到 Windows VM</span><span class="sxs-lookup"><span data-stu-id="a0d86-103">How to attach an unmanaged data disk to a Windows VM in the Azure portal</span></span>

<span data-ttu-id="a0d86-104">本文示範如何透過 Azure 入口網站將新的及現有的未受管理磁碟連結到 Windows 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a0d86-104">This article shows you how to attach both new and existing unmanaged disks to Windows virtual machines through the Azure portal.</span></span> <span data-ttu-id="a0d86-105">您也可以[使用 PowerShell 連結資料磁碟](./attach-disk-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="a0d86-105">You can also [attach a data disk using PowerShell](./attach-disk-ps.md).</span></span> <span data-ttu-id="a0d86-106">這麼做之前，請先檢閱下列提示：</span><span class="sxs-lookup"><span data-stu-id="a0d86-106">Before you do this, review these tips:</span></span>

* <span data-ttu-id="a0d86-107">虛擬機器的大小會控制您可以連接的資料磁碟數目。</span><span class="sxs-lookup"><span data-stu-id="a0d86-107">The size of the virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="a0d86-108">如需詳細資訊，請參閱 [虛擬機器的大小](sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="a0d86-108">For details, see [Sizes for virtual machines](sizes.md).</span></span>
* <span data-ttu-id="a0d86-109">若要使用進階儲存體，您需要 DS 系列或 GS 系列的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a0d86-109">To use Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="a0d86-110">您可以使用進階或標準儲存體帳戶的磁碟搭配這些虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a0d86-110">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="a0d86-111">僅特定地區可用進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="a0d86-111">Premium storage is available in certain regions.</span></span> <span data-ttu-id="a0d86-112">如需詳細資訊，請參閱[進階儲存體：Azure 虛擬機器工作負載適用的高效能儲存體](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="a0d86-112">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="a0d86-113">對於新的磁碟，當您連接的時候 Azure 會建立該磁碟，所以您不需要建立它。</span><span class="sxs-lookup"><span data-stu-id="a0d86-113">For a new disk, you don't need to create it first because Azure creates it when you attach it.</span></span>


<span data-ttu-id="a0d86-114">您也可以[使用 Powershell 連接資料磁碟](attach-disk-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="a0d86-114">You can also [attach a data disk using Powershell](attach-disk-ps.md).</span></span>


## <a name="find-the-virtual-machine"></a><span data-ttu-id="a0d86-115">尋找虛擬機器</span><span class="sxs-lookup"><span data-stu-id="a0d86-115">Find the virtual machine</span></span>
1. <span data-ttu-id="a0d86-116">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="a0d86-116">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="a0d86-117">在左側功能表中，按一下 [虛擬機器]。</span><span class="sxs-lookup"><span data-stu-id="a0d86-117">In the menu on the left, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="a0d86-118">然後從清單中選取虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a0d86-118">Select the virtual machine from the list.</span></span>
4. <span data-ttu-id="a0d86-119">在 [虛擬機器] 刀鋒視窗中，按一下 [磁碟]。</span><span class="sxs-lookup"><span data-stu-id="a0d86-119">In the Virtual machines blade, click **Disks**.</span></span>
   
<span data-ttu-id="a0d86-120">接著，依照指示來連接[新的磁碟](#option-1-attach-a-new-disk)或[現有的磁碟](#option-2-attach-an-existing-disk)。</span><span class="sxs-lookup"><span data-stu-id="a0d86-120">Continue by following instructions for attaching either a [new disk](#option-1-attach-a-new-disk) or an [existing disk](#option-2-attach-an-existing-disk).</span></span>

## <a name="option-1-attach-and-initialize-a-new-disk"></a><span data-ttu-id="a0d86-121">選項 1：連接新磁碟並進行初始化</span><span class="sxs-lookup"><span data-stu-id="a0d86-121">Option 1: Attach and initialize a new disk</span></span>
1. <span data-ttu-id="a0d86-122">在 [磁碟] 刀鋒視窗上，按一下 [+ 新增資料磁碟]。</span><span class="sxs-lookup"><span data-stu-id="a0d86-122">On the **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="a0d86-123">在 [連結受管理的磁碟] 刀鋒視窗中，於 [名稱] 中輸入磁碟名稱，然後在 [來源類型] 中選取 [新增 (空磁碟)]。</span><span class="sxs-lookup"><span data-stu-id="a0d86-123">In the **Attach managed disk** blade, type a name for the disk in **Name** and then select **New (empty disk)** in **Source type**.</span></span>
3. <span data-ttu-id="a0d86-124">在 [儲存體容器] 下，按一下 [瀏覽] 按鈕並瀏覽至您要用於儲存新 VHD 的儲存體帳戶與容器，然後按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="a0d86-124">Under **Storage container**, click the **Browse** button and browse to the storage account and container where you would like the new VHD to be stored and then click **Select**.</span></span> 
  
   ![檢閱磁碟設定](./media/attach-disk-portal/attach-empty-unmanaged.png)
   
3. <span data-ttu-id="a0d86-126">當您完成資料磁碟的設定之後，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="a0d86-126">When you are done with the settings for the data disk, click **OK**.</span></span>
4. <span data-ttu-id="a0d86-127">回到 [磁碟] 刀鋒視窗，按一下 [儲存] 以將磁碟新增到 VM 設定。</span><span class="sxs-lookup"><span data-stu-id="a0d86-127">Back in the **Disks** blade, click **Save** to add the disk to the VM configuration.</span></span>


### <a name="initialize-a-new-data-disk"></a><span data-ttu-id="a0d86-128">初始化新的資料磁碟</span><span class="sxs-lookup"><span data-stu-id="a0d86-128">Initialize a new data disk</span></span>

1. <span data-ttu-id="a0d86-129">連接至虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a0d86-129">Connect to the virtual machine.</span></span> <span data-ttu-id="a0d86-130">如需指示，請參閱 [如何連接和登入執行 Windows 的 Azure 虛擬機器](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="a0d86-130">For instructions, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
1. <span data-ttu-id="a0d86-131">按一下 VM 內部的 [開始] 功能表，然後輸入 **diskmgmt.msc** 並按下 **Enter** 鍵。</span><span class="sxs-lookup"><span data-stu-id="a0d86-131">Click the **Start** menu inside the VM and type **diskmgmt.msc** and hit **Enter**.</span></span> <span data-ttu-id="a0d86-132">這會啟動磁碟管理嵌入式管理單元。</span><span class="sxs-lookup"><span data-stu-id="a0d86-132">This starts the Disk Management snap-in.</span></span>
2. <span data-ttu-id="a0d86-133">磁碟管理會辨識出您擁有新的、未初始化的磁碟，且會隨即顯示「初始化磁碟」視窗。</span><span class="sxs-lookup"><span data-stu-id="a0d86-133">Disk Management recognizes that you have a new, uninitialized disk and the Initialize Disk window will pop up.</span></span>
3. <span data-ttu-id="a0d86-134">請確定已選取新磁碟，並按一下 [確定] 將磁碟初始化。</span><span class="sxs-lookup"><span data-stu-id="a0d86-134">Make sure the new disk is selected and click **OK** to initialize it.</span></span>
4. <span data-ttu-id="a0d86-135">新的磁碟現在會顯示為 [未配置]。</span><span class="sxs-lookup"><span data-stu-id="a0d86-135">The new disk now appears as **unallocated**.</span></span> <span data-ttu-id="a0d86-136">以滑鼠右鍵按一下磁碟上的任何位置，並選取 [新增簡單磁碟區]。</span><span class="sxs-lookup"><span data-stu-id="a0d86-136">Right-click anywhere on the disk and select **New simple volume**.</span></span> <span data-ttu-id="a0d86-137">[新增簡單磁碟區精靈] 會隨即啟動。</span><span class="sxs-lookup"><span data-stu-id="a0d86-137">The **New Simple Volume Wizard** starts.</span></span>
5. <span data-ttu-id="a0d86-138">逐一執行精靈的所有步驟，保留所有預設值，並在完成後選取 [完成]。</span><span class="sxs-lookup"><span data-stu-id="a0d86-138">Go through the wizard, keeping all of the defaults, when you are done select **Finish**.</span></span>
6. <span data-ttu-id="a0d86-139">關閉磁碟管理。</span><span class="sxs-lookup"><span data-stu-id="a0d86-139">Close Disk Management.</span></span>
7. <span data-ttu-id="a0d86-140">您會看到快顯視窗，說明您必須先將新的磁碟格式化之後才能使用。</span><span class="sxs-lookup"><span data-stu-id="a0d86-140">You get a pop-up that you need to format the new disk before you can use it.</span></span> <span data-ttu-id="a0d86-141">按一下 [格式化磁碟]。</span><span class="sxs-lookup"><span data-stu-id="a0d86-141">Click **Format disk**.</span></span>
8. <span data-ttu-id="a0d86-142">在 [格式化新磁碟] 對話方塊中，檢查設定，然後按一下 [開始]。</span><span class="sxs-lookup"><span data-stu-id="a0d86-142">In the **Format new disk** dialog, check the settings and then click **Start**.</span></span>
9. <span data-ttu-id="a0d86-143">系統會向您顯示警告，說明格式化磁碟會清除所有資料，請按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="a0d86-143">You get a warning that formatting the disks erases all of the data, click **OK**.</span></span>
10. <span data-ttu-id="a0d86-144">格式化完成之後，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="a0d86-144">When the format is complete, click **OK**.</span></span>


## <a name="option-2-attach-an-existing-disk"></a><span data-ttu-id="a0d86-145">選項 2：連接現有磁碟</span><span class="sxs-lookup"><span data-stu-id="a0d86-145">Option 2: Attach an existing disk</span></span>
1. <span data-ttu-id="a0d86-146">在 [磁碟] 刀鋒視窗上，按一下 [+ 新增資料磁碟]。</span><span class="sxs-lookup"><span data-stu-id="a0d86-146">On the **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="a0d86-147">在 [連結未受管理的磁碟] 刀鋒視窗中，於 [來源類型] 中選取 [現有 Blob]。</span><span class="sxs-lookup"><span data-stu-id="a0d86-147">On the **Attach unmanaged disk** blade, in **Source type** select **Existing blob**.</span></span>

    ![檢閱磁碟設定](./media/attach-disk-portal/attach-existing-unmanaged.png)

    3. <span data-ttu-id="a0d86-149">按一下 [瀏覽] 以瀏覽至現有 VHD 所在的儲存體帳戶和容器。</span><span class="sxs-lookup"><span data-stu-id="a0d86-149">Click **Browse** to navigate to the storage account and container where the existing VHD is located.</span></span> <span data-ttu-id="a0d86-150">按一下 VHD，然後按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="a0d86-150">Click and the VHD and then click **Select**.</span></span>
4. <span data-ttu-id="a0d86-151">在 [連結未受管理的磁碟] 刀鋒視窗中按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="a0d86-151">Click **OK** in the **Attach unmanaged disk** blade.</span></span>
5. <span data-ttu-id="a0d86-152">在 [磁碟] 刀鋒視窗中，按一下 [儲存] 以將磁碟新增到 VM 設定。</span><span class="sxs-lookup"><span data-stu-id="a0d86-152">In the **Disks** blade, click **Save** to add the disk to the configuration for the VM.</span></span>
   


## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="a0d86-153">搭配使用 TRIM 與標準儲存體</span><span class="sxs-lookup"><span data-stu-id="a0d86-153">Use TRIM with standard storage</span></span>

<span data-ttu-id="a0d86-154">如果您使用標準儲存體 (HDD)，您應該啟用 TRIM。</span><span class="sxs-lookup"><span data-stu-id="a0d86-154">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="a0d86-155">TRIM 會捨棄磁碟上未使用的區塊，因此您只需支付實際使用的儲存體。</span><span class="sxs-lookup"><span data-stu-id="a0d86-155">TRIM discards unused blocks on the disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="a0d86-156">如果您建立大型檔案，然後將它們刪除，這便可節省成本。</span><span class="sxs-lookup"><span data-stu-id="a0d86-156">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="a0d86-157">您可以執行此命令來檢查 TRIM 設定。</span><span class="sxs-lookup"><span data-stu-id="a0d86-157">You can run this command to check the TRIM setting.</span></span> <span data-ttu-id="a0d86-158">在您的 Windows VM 上開啟命令提示字元並輸入︰</span><span class="sxs-lookup"><span data-stu-id="a0d86-158">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="a0d86-159">如果命令傳回 0，則已正確啟用 TRIM。</span><span class="sxs-lookup"><span data-stu-id="a0d86-159">If the command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="a0d86-160">如果傳回 1，請執行下列命令來啟用 TRIM：</span><span class="sxs-lookup"><span data-stu-id="a0d86-160">If it returns 1, run the following command to enable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

<span data-ttu-id="a0d86-161">從磁碟中刪除資料之後，您可以使用 TRIM 來執行重組，以確保 TRIM 作業正確排清：</span><span class="sxs-lookup"><span data-stu-id="a0d86-161">After deleting data from your disk, you can ensure the TRIM operations flush properly by running defrag with TRIM:</span></span>

```
defrag.exe <volume:> -l
```

<span data-ttu-id="a0d86-162">您也可以確保已透過格式化磁碟區，修剪整個磁碟區。</span><span class="sxs-lookup"><span data-stu-id="a0d86-162">You can also ensure the entire volume is trimmed by formatting the volume.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a0d86-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a0d86-163">Next steps</span></span>
<span data-ttu-id="a0d86-164">如果您的應用程式需要使用 D: 磁碟機來儲存資料，可以[變更 Windows 暫存磁碟的磁碟機代號](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="a0d86-164">If you application needs to use the D: drive to store data, you can [change the drive letter of the Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

