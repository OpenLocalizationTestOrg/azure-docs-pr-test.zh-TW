---
title: "將 VM 的 D: 磁碟機設為資料磁碟 | Microsoft Docs"
description: "說明如何為 Windows VM 變更磁碟機代號，讓您能夠使用 D: 磁碟機做為資料磁碟機。"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 0867a931-0055-4e31-8403-9b38a3eeb904
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: cynthn
ms.openlocfilehash: 7667175c01be2421bfc3badd83b1d8aaeb29bfde
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-d-drive-as-a-data-drive-on-a-windows-vm"></a><span data-ttu-id="3da43-103">使用 D: 磁碟機作為 Windows VM 上的資料磁碟機</span><span class="sxs-lookup"><span data-stu-id="3da43-103">Use the D: drive as a data drive on a Windows VM</span></span>
<span data-ttu-id="3da43-104">如果您的應用程式需要使用 D 磁碟機來儲存資料，請遵循下列指示，使用不同的磁碟機代號來代表暫存磁碟。</span><span class="sxs-lookup"><span data-stu-id="3da43-104">If your application needs to use the D drive to store data, follow these instructions to use a different drive letter for the temporary disk.</span></span> <span data-ttu-id="3da43-105">切勿使用暫存磁碟儲存需要保留的資料。</span><span class="sxs-lookup"><span data-stu-id="3da43-105">Never use the temporary disk to store data that you need to keep.</span></span>

<span data-ttu-id="3da43-106">如果您調整虛擬機器大小或 **停止 (解除配置)** 虛擬機器，這可能會導致虛擬機器置於新的 Hypervisor。</span><span class="sxs-lookup"><span data-stu-id="3da43-106">If you resize or **Stop (Deallocate)** a virtual machine, this may trigger placement of the virtual machine to a new hypervisor.</span></span> <span data-ttu-id="3da43-107">已規劃或未規劃的維護事件也可能會觸發這個放置動作。</span><span class="sxs-lookup"><span data-stu-id="3da43-107">A planned or unplanned maintenance event may also trigger this placement.</span></span> <span data-ttu-id="3da43-108">在此案例中，暫存磁碟會重新指派給第一個可用的磁碟機代號。</span><span class="sxs-lookup"><span data-stu-id="3da43-108">In this scenario, the temporary disk will be reassigned to the first available drive letter.</span></span> <span data-ttu-id="3da43-109">如果您的應用程式特別需要 D: 磁碟機，必須依照這些步驟，暫時移動 pagefile.sys、連接新的資料磁碟並為其指派代號 D，然後將 pagefile.sys 移回暫存磁碟機。</span><span class="sxs-lookup"><span data-stu-id="3da43-109">If you have an application that specifically requires the D: drive, you need to follow these steps to temporarily move the pagefile.sys, attach a new data disk and assign it the letter D and then move the pagefile.sys back to the temporary drive.</span></span> <span data-ttu-id="3da43-110">一旦完成後，如果 VM 移到不同的 Hypervisor，Azure 將不會收回 D:。</span><span class="sxs-lookup"><span data-stu-id="3da43-110">Once complete, Azure will not take back the D: if the VM moves to a different hypervisor.</span></span>

<span data-ttu-id="3da43-111">如需有關 Azure 如何使用暫存磁碟的詳細資訊，請參閱 [了解 Microsoft Azure 虛擬機器上的暫存磁碟機](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="3da43-111">For more information about how Azure uses the temporary disk, see [Understanding the temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span></span>

## <a name="attach-the-data-disk"></a><span data-ttu-id="3da43-112">連接資料磁碟</span><span class="sxs-lookup"><span data-stu-id="3da43-112">Attach the data disk</span></span>
<span data-ttu-id="3da43-113">首先，您需要將資料磁碟連接到虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="3da43-113">First, you'll need to attach the data disk to the virtual machine.</span></span> <span data-ttu-id="3da43-114">若要使用入口網站來執行此操作，請參閱[如何在 Azure 入口網站連接受控資料磁碟](attach-managed-disk-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="3da43-114">To do this using the portal, see [How to attach a managed data disk in the Azure portal](attach-managed-disk-portal.md).</span></span>

## <a name="temporarily-move-pagefilesys-to-c-drive"></a><span data-ttu-id="3da43-115">暫時將 pagefile.sys 移到 C 磁碟機</span><span class="sxs-lookup"><span data-stu-id="3da43-115">Temporarily move pagefile.sys to C drive</span></span>
1. <span data-ttu-id="3da43-116">連接至虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="3da43-116">Connect to the virtual machine.</span></span> 
2. <span data-ttu-id="3da43-117">使用滑鼠右鍵按一下 [開始] 功能表，然後選取 [系統]。</span><span class="sxs-lookup"><span data-stu-id="3da43-117">Right-click the **Start** menu and select **System**.</span></span>
3. <span data-ttu-id="3da43-118">在左側功能表中，選取 [進階系統設定] 。</span><span class="sxs-lookup"><span data-stu-id="3da43-118">In the left-hand menu, select **Advanced system settings**.</span></span>
4. <span data-ttu-id="3da43-119">在 [效能] 區段中，選取 [設定]。</span><span class="sxs-lookup"><span data-stu-id="3da43-119">In the **Performance** section, select **Settings**.</span></span>
5. <span data-ttu-id="3da43-120">選取 [進階]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3da43-120">Select the **Advanced** tab.</span></span>
6. <span data-ttu-id="3da43-121">在 [虛擬記憶體] 區段中，選取 [變更]。</span><span class="sxs-lookup"><span data-stu-id="3da43-121">In the **Virtual memory** section, select **Change**.</span></span>
7. <span data-ttu-id="3da43-122">選取 **C** 磁碟機，然後依序按一下 [系統管理大小] 和 [設定]。</span><span class="sxs-lookup"><span data-stu-id="3da43-122">Select the **C** drive and then click **System managed size** and then click **Set**.</span></span>
8. <span data-ttu-id="3da43-123">選取 **D** 磁碟機，然後依序按一下 [沒有分頁檔] 和 [設定]。</span><span class="sxs-lookup"><span data-stu-id="3da43-123">Select the **D** drive and then click **No paging file** and then click **Set**.</span></span>
9. <span data-ttu-id="3da43-124">按一下 [套用]。</span><span class="sxs-lookup"><span data-stu-id="3da43-124">Click Apply.</span></span> <span data-ttu-id="3da43-125">您將會收到一則警告，表示電腦必須重新啟動，才能讓變更生效。</span><span class="sxs-lookup"><span data-stu-id="3da43-125">You will get a warning that the computer needs to be restarted for the changes to take affect.</span></span>
10. <span data-ttu-id="3da43-126">重新啟動虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="3da43-126">Restart the virtual machine.</span></span>

## <a name="change-the-drive-letters"></a><span data-ttu-id="3da43-127">變更磁碟機代號</span><span class="sxs-lookup"><span data-stu-id="3da43-127">Change the drive letters</span></span>
1. <span data-ttu-id="3da43-128">重新啟動 VM 之後，再次登入 VM。</span><span class="sxs-lookup"><span data-stu-id="3da43-128">Once the VM restarts, log back on to the VM.</span></span>
2. <span data-ttu-id="3da43-129">按一下 [開始] 功能表，然後輸入 **diskmgmt.msc** 並按下 Enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="3da43-129">Click the **Start** menu and type **diskmgmt.msc** and hit Enter.</span></span> <span data-ttu-id="3da43-130">隨即會啟動「磁碟管理」。</span><span class="sxs-lookup"><span data-stu-id="3da43-130">Disk Management will start.</span></span>
3. <span data-ttu-id="3da43-131">使用滑鼠右鍵按一下 **D**、暫存磁碟機，然後選取 [變更磁碟機代號及路徑]。</span><span class="sxs-lookup"><span data-stu-id="3da43-131">Right-click on **D**, the Temporary Storage drive, and select **Change Drive Letter and Paths**.</span></span>
4. <span data-ttu-id="3da43-132">在磁碟機代號下方，選取新的磁碟機 (例如 **T**)，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="3da43-132">Under Drive letter, select a new drive such as **T** and then click **OK**.</span></span> 
5. <span data-ttu-id="3da43-133">使用滑鼠右鍵按一下資料磁碟，然後選取 [變更磁碟機代號及路徑] 。</span><span class="sxs-lookup"><span data-stu-id="3da43-133">Right-click on the data disk, and select **Change Drive Letter and Paths**.</span></span>
6. <span data-ttu-id="3da43-134">在 [磁碟機代號] 下方，選取磁碟機 **D**，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="3da43-134">Under Drive letter, select drive **D** and then click **OK**.</span></span> 

## <a name="move-pagefilesys-back-to-the-temporary-storage-drive"></a><span data-ttu-id="3da43-135">將 pagefile.sys 移回暫存磁碟機</span><span class="sxs-lookup"><span data-stu-id="3da43-135">Move pagefile.sys back to the temporary storage drive</span></span>
1. <span data-ttu-id="3da43-136">使用滑鼠右鍵按一下 [開始] 功能表，然後選取 [系統]。</span><span class="sxs-lookup"><span data-stu-id="3da43-136">Right-click the **Start** menu and select **System**</span></span>
2. <span data-ttu-id="3da43-137">在左側功能表中，選取 [進階系統設定] 。</span><span class="sxs-lookup"><span data-stu-id="3da43-137">In the left-hand menu, select **Advanced system settings**.</span></span>
3. <span data-ttu-id="3da43-138">在 [效能] 區段中，選取 [設定]。</span><span class="sxs-lookup"><span data-stu-id="3da43-138">In the **Performance** section, select **Settings**.</span></span>
4. <span data-ttu-id="3da43-139">選取 [進階]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3da43-139">Select the **Advanced** tab.</span></span>
5. <span data-ttu-id="3da43-140">在 [虛擬記憶體] 區段中，選取 [變更]。</span><span class="sxs-lookup"><span data-stu-id="3da43-140">In the **Virtual memory** section, select **Change**.</span></span>
6. <span data-ttu-id="3da43-141">選取作業系統磁碟機 **C**，然後依序按一下 [沒有分頁檔] 和 [設定]。</span><span class="sxs-lookup"><span data-stu-id="3da43-141">Select the OS drive **C** and click **No paging file** and then click **Set**.</span></span>
7. <span data-ttu-id="3da43-142">選取暫存磁碟機 **T**，然後依序按一下 [系統管理大小] 和 [設定]。</span><span class="sxs-lookup"><span data-stu-id="3da43-142">Select the temporary storage drive **T** and then click **System managed size** and then click **Set**.</span></span>
8. <span data-ttu-id="3da43-143">按一下 [Apply (套用)] 。</span><span class="sxs-lookup"><span data-stu-id="3da43-143">Click **Apply**.</span></span> <span data-ttu-id="3da43-144">您將會收到一則警告，表示電腦必須重新啟動，才能讓變更生效。</span><span class="sxs-lookup"><span data-stu-id="3da43-144">You will get a warning that the computer needs to be restarted for the changes to take affect.</span></span>
9. <span data-ttu-id="3da43-145">重新啟動虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="3da43-145">Restart the virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3da43-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3da43-146">Next steps</span></span>
* <span data-ttu-id="3da43-147">您可以[連接其他資料磁碟](attach-managed-disk-portal.md)來增加虛擬機器可以使用的儲存體。</span><span class="sxs-lookup"><span data-stu-id="3da43-147">You can increase the storage available to your virtual machine by [attaching a additional data disk](attach-managed-disk-portal.md).</span></span>

