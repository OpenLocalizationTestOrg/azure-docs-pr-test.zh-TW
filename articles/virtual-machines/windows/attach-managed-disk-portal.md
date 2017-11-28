---
title: "將受管理的資料磁碟連結到 Windows VM - Azure | Microsoft Docs"
description: "如何在 Azure 入口網站中使用 Resource Manager 部署模型，將新的受管理資料磁碟連結到 Windows VM。"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: cynthn
ms.openlocfilehash: f0cf88a06c5470ef173b22e7213419a6c8760723
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-attach-a-managed-data-disk-to-a-windows-vm-in-the-azure-portal"></a><span data-ttu-id="543d0-103">如何在 Azure 入口網站中將受管理的資料磁碟連結到 Windows VM</span><span class="sxs-lookup"><span data-stu-id="543d0-103">How to attach a managed data disk to a Windows VM in the Azure portal</span></span>

<span data-ttu-id="543d0-104">本文示範如何透過 Azure 入口網站將新的受管理資料磁碟連結到 Windows 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="543d0-104">This article shows you how to attach a new managed data disk to Windows virtual machines through the Azure portal.</span></span> <span data-ttu-id="543d0-105">這麼做之前，請先檢閱下列提示：</span><span class="sxs-lookup"><span data-stu-id="543d0-105">Before you do this, review these tips:</span></span>

* <span data-ttu-id="543d0-106">虛擬機器的大小會控制您可以連接的資料磁碟數目。</span><span class="sxs-lookup"><span data-stu-id="543d0-106">The size of the virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="543d0-107">如需詳細資訊，請參閱 [虛擬機器的大小](sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="543d0-107">For details, see [Sizes for virtual machines](sizes.md).</span></span>
* <span data-ttu-id="543d0-108">對於新的磁碟，當您連接的時候 Azure 會建立該磁碟，所以您不需要建立它。</span><span class="sxs-lookup"><span data-stu-id="543d0-108">For a new disk, you don't need to create it first because Azure creates it when you attach it.</span></span>

<span data-ttu-id="543d0-109">您也可以[使用 Powershell 連接資料磁碟](attach-disk-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="543d0-109">You can also [attach a data disk using Powershell](attach-disk-ps.md).</span></span>



## <a name="add-a-data-disk"></a><span data-ttu-id="543d0-110">新增資料磁碟</span><span class="sxs-lookup"><span data-stu-id="543d0-110">Add a data disk</span></span>
1. <span data-ttu-id="543d0-111">在左側功能表中，按一下 [虛擬機器]。</span><span class="sxs-lookup"><span data-stu-id="543d0-111">In the menu on the left, click **Virtual Machines**.</span></span>
2. <span data-ttu-id="543d0-112">然後從清單中選取虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="543d0-112">Select the virtual machine from the list.</span></span>
3. <span data-ttu-id="543d0-113">在 [虛擬機器] 刀鋒視窗中，按一下 [磁碟]。</span><span class="sxs-lookup"><span data-stu-id="543d0-113">On the virtual machine blade, click **Disks**.</span></span>
   4. <span data-ttu-id="543d0-114">在 [磁碟] 刀鋒視窗上，按一下 [+ 新增資料磁碟]。</span><span class="sxs-lookup"><span data-stu-id="543d0-114">On the **Disks** blade, click **+ Add data disk**.</span></span>
5. <span data-ttu-id="543d0-115">在新磁碟的下拉式清單中，選取 [建立空的]。</span><span class="sxs-lookup"><span data-stu-id="543d0-115">In the drop-down for the new disk, select **Create empty**.</span></span>
6. <span data-ttu-id="543d0-116">在 [建立受管理磁碟] 刀鋒視窗中，輸入磁碟名稱並視需要調整其他設定。</span><span class="sxs-lookup"><span data-stu-id="543d0-116">In the **Create managed disk** blade, type in a name for the disk and adjust the other settings as necessary.</span></span> <span data-ttu-id="543d0-117">完成之後，請按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="543d0-117">When you are done, click **Create**.</span></span>
7. <span data-ttu-id="543d0-118">在 [磁碟] 刀鋒視窗中，按一下 [儲存] 以儲存 VM 的新磁碟設定。</span><span class="sxs-lookup"><span data-stu-id="543d0-118">In the **Disks** blade, click save to save the new disk configuration for the VM.</span></span>
6. <span data-ttu-id="543d0-119">在 Azure 建立磁碟並將其連接至虛擬機器之後，該新磁碟就會列在虛擬機器之磁碟設定中的 [資料磁碟] 底下。</span><span class="sxs-lookup"><span data-stu-id="543d0-119">After Azure creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.</span></span>


## <a name="initialize-a-new-data-disk"></a><span data-ttu-id="543d0-120">初始化新的資料磁碟</span><span class="sxs-lookup"><span data-stu-id="543d0-120">Initialize a new data disk</span></span>

1. <span data-ttu-id="543d0-121">連線至 VM。</span><span class="sxs-lookup"><span data-stu-id="543d0-121">Connect to the VM.</span></span>
1. <span data-ttu-id="543d0-122">按一下 VM 內部的 [開始] 功能表，然後輸入 **diskmgmt.msc** 並按下 **Enter** 鍵。</span><span class="sxs-lookup"><span data-stu-id="543d0-122">Click the start menu inside the VM and type **diskmgmt.msc** and hit **Enter**.</span></span> <span data-ttu-id="543d0-123">這將會啟動磁碟管理嵌入式管理單元。</span><span class="sxs-lookup"><span data-stu-id="543d0-123">This will start the Disk Management snap-in.</span></span>
2. <span data-ttu-id="543d0-124">磁碟管理將會辨識出您擁有新的、未初始化的磁碟，且會隨即顯示「初始化磁碟」視窗。</span><span class="sxs-lookup"><span data-stu-id="543d0-124">Disk Management will recognize that you have a new, un-initialized disk and the Initialize Disk window will pop up.</span></span>
3. <span data-ttu-id="543d0-125">請確定已選取新磁碟，並按一下 [確定] 將磁碟初始化。</span><span class="sxs-lookup"><span data-stu-id="543d0-125">Make sure the new disk is selected and click **OK** to initialize it.</span></span>
4. <span data-ttu-id="543d0-126">新的磁碟現在將會顯示為 [未配置]。</span><span class="sxs-lookup"><span data-stu-id="543d0-126">The new disk will now appear as **unallocated**.</span></span> <span data-ttu-id="543d0-127">以滑鼠右鍵按一下磁碟上的任何位置，並選取 [新增簡單磁碟區]。</span><span class="sxs-lookup"><span data-stu-id="543d0-127">Right-click anywhere on the disk and select **New simple volume**.</span></span> <span data-ttu-id="543d0-128">[新增簡單磁碟區精靈] 將會隨即啟動。</span><span class="sxs-lookup"><span data-stu-id="543d0-128">The **New Simple Volume Wizard** will start.</span></span>
5. <span data-ttu-id="543d0-129">逐一執行精靈的所有步驟，保留所有預設值，並在完成後選取 [完成]。</span><span class="sxs-lookup"><span data-stu-id="543d0-129">Go through the wizard, keeping all of the defaults, when you are done select **Finish**.</span></span>
6. <span data-ttu-id="543d0-130">關閉磁碟管理。</span><span class="sxs-lookup"><span data-stu-id="543d0-130">Close Disk Management.</span></span>
7. <span data-ttu-id="543d0-131">您將會看到快顯視窗，說明您必須先將新的磁碟格式化之後才能使用。</span><span class="sxs-lookup"><span data-stu-id="543d0-131">You will get a pop-up that you need to format the new disk before you can use it.</span></span> <span data-ttu-id="543d0-132">按一下 [格式化磁碟]。</span><span class="sxs-lookup"><span data-stu-id="543d0-132">Click **Format disk**.</span></span>
8. <span data-ttu-id="543d0-133">在 [格式化新磁碟] 對話方塊中，檢查設定，然後按一下 [開始]。</span><span class="sxs-lookup"><span data-stu-id="543d0-133">In the **Format new disk** dialog, check the settings and then click **Start**.</span></span>
9. <span data-ttu-id="543d0-134">系統會向您顯示警告，說明格式化磁碟將會清除所有資料，請按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="543d0-134">You will get a warning that formatting the disks will erase all of the data, click **OK**.</span></span>
10. <span data-ttu-id="543d0-135">格式化完成之後，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="543d0-135">When the format is complete, click **OK**.</span></span>

## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="543d0-136">搭配使用 TRIM 與標準儲存體</span><span class="sxs-lookup"><span data-stu-id="543d0-136">Use TRIM with standard storage</span></span>

<span data-ttu-id="543d0-137">如果您使用標準儲存體 (HDD)，您應該啟用 TRIM。</span><span class="sxs-lookup"><span data-stu-id="543d0-137">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="543d0-138">TRIM 會捨棄磁碟上未使用的區塊，因此您只需支付實際使用的儲存體。</span><span class="sxs-lookup"><span data-stu-id="543d0-138">TRIM discards unused blocks on the disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="543d0-139">如果您建立大型檔案，然後將它們刪除，這便可節省成本。</span><span class="sxs-lookup"><span data-stu-id="543d0-139">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="543d0-140">您可以執行此命令來檢查 TRIM 設定。</span><span class="sxs-lookup"><span data-stu-id="543d0-140">You can run this command to check the TRIM setting.</span></span> <span data-ttu-id="543d0-141">在您的 Windows VM 上開啟命令提示字元並輸入︰</span><span class="sxs-lookup"><span data-stu-id="543d0-141">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="543d0-142">如果命令傳回 0，則已正確啟用 TRIM。</span><span class="sxs-lookup"><span data-stu-id="543d0-142">If the command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="543d0-143">如果傳回 1，請執行下列命令來啟用 TRIM：</span><span class="sxs-lookup"><span data-stu-id="543d0-143">If it returns 1, run the following command to enable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

<span data-ttu-id="543d0-144">從磁碟中刪除資料之後，您可以使用 TRIM 來執行重組，以確保 TRIM 作業正確排清：</span><span class="sxs-lookup"><span data-stu-id="543d0-144">After deleting data from your disk, you can ensure the TRIM operations flush properly by running defrag with TRIM:</span></span>

```
defrag.exe <volume:> -l
```

<span data-ttu-id="543d0-145">您也可以確保已透過格式化磁碟區，修剪整個磁碟區。</span><span class="sxs-lookup"><span data-stu-id="543d0-145">You can also ensure the entire volume is trimmed by formatting the volume.</span></span>

## <a name="next-steps"></a><span data-ttu-id="543d0-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="543d0-146">Next steps</span></span>
<span data-ttu-id="543d0-147">如果您的應用程式需要使用 D: 磁碟機來儲存資料，可以[變更 Windows 暫存磁碟的磁碟機代號](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="543d0-147">If you application needs to use the D: drive to store data, you can [change the drive letter of the Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
