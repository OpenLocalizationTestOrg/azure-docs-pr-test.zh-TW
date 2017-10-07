---
title: "請 hello VM 資料磁碟的 d： 磁碟機 |Microsoft 文件"
description: "描述如何 toochange 磁碟機代號為 Windows vm 以便您可以使用 hello d： 磁碟機的資料磁碟機。"
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
ms.openlocfilehash: 43939da1a890ac4049266487951e3889aa0ed9d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-d-drive-as-a-data-drive-on-a-windows-vm"></a><span data-ttu-id="38940-103">Hello d： 磁碟機做為 Windows VM 上的資料磁碟機</span><span class="sxs-lookup"><span data-stu-id="38940-103">Use hello D: drive as a data drive on a Windows VM</span></span>
<span data-ttu-id="38940-104">如果您的應用程式需要 toouse hello D 磁碟機 toostore 資料，請遵循這些指示 toouse hello 暫存磁碟的不同磁碟機代號。</span><span class="sxs-lookup"><span data-stu-id="38940-104">If your application needs toouse hello D drive toostore data, follow these instructions toouse a different drive letter for hello temporary disk.</span></span> <span data-ttu-id="38940-105">絕對不要使用，您需要 tookeep hello 暫存磁碟 toostore 資料。</span><span class="sxs-lookup"><span data-stu-id="38940-105">Never use hello temporary disk toostore data that you need tookeep.</span></span>

<span data-ttu-id="38940-106">如果您調整大小或**停止 （取消配置）**的虛擬機器，這可能會觸發 hello 虛擬機器 tooa 新 hypervisor 的位置。</span><span class="sxs-lookup"><span data-stu-id="38940-106">If you resize or **Stop (Deallocate)** a virtual machine, this may trigger placement of hello virtual machine tooa new hypervisor.</span></span> <span data-ttu-id="38940-107">已規劃或未規劃的維護事件也可能會觸發這個放置動作。</span><span class="sxs-lookup"><span data-stu-id="38940-107">A planned or unplanned maintenance event may also trigger this placement.</span></span> <span data-ttu-id="38940-108">在此案例中，hello 暫存磁碟會重新指派的 toohello 第一個可用的磁碟機代號。</span><span class="sxs-lookup"><span data-stu-id="38940-108">In this scenario, hello temporary disk will be reassigned toohello first available drive letter.</span></span> <span data-ttu-id="38940-109">如果您有特別需要 hello d： 磁碟機的應用程式，您需要 toofollow，這些步驟 tootemporarily 移動 hello pagefile.sys，將新的資料磁碟，並將它指派 hello 代號為 D，然後移動 hello pagefile.sys 回 toohello 暫存磁碟機。</span><span class="sxs-lookup"><span data-stu-id="38940-109">If you have an application that specifically requires hello D: drive, you need toofollow these steps tootemporarily move hello pagefile.sys, attach a new data disk and assign it hello letter D and then move hello pagefile.sys back toohello temporary drive.</span></span> <span data-ttu-id="38940-110">完成後，Azure 將不會傳回 hello d： 如果 hello VM 移 tooa 不同 hypervisor。</span><span class="sxs-lookup"><span data-stu-id="38940-110">Once complete, Azure will not take back hello D: if hello VM moves tooa different hypervisor.</span></span>

<span data-ttu-id="38940-111">如需 Azure 的 hello 暫存磁碟的使用方式的詳細資訊，請參閱[了解 hello 暫存磁碟機上的 Microsoft Azure 虛擬機器](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="38940-111">For more information about how Azure uses hello temporary disk, see [Understanding hello temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span></span>

## <a name="attach-hello-data-disk"></a><span data-ttu-id="38940-112">附加 hello 資料磁碟</span><span class="sxs-lookup"><span data-stu-id="38940-112">Attach hello data disk</span></span>
<span data-ttu-id="38940-113">首先，您必須 tooattach hello 資料磁碟 toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="38940-113">First, you'll need tooattach hello data disk toohello virtual machine.</span></span> <span data-ttu-id="38940-114">toodo 此使用 hello 入口網站，請參閱[tooattach managed 資料 hello Azure 入口網站中的磁碟](attach-managed-disk-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="38940-114">toodo this using hello portal, see [How tooattach a managed data disk in hello Azure portal](attach-managed-disk-portal.md).</span></span>

## <a name="temporarily-move-pagefilesys-tooc-drive"></a><span data-ttu-id="38940-115">暫時移動 pagefile.sys tooC 磁碟機</span><span class="sxs-lookup"><span data-stu-id="38940-115">Temporarily move pagefile.sys tooC drive</span></span>
1. <span data-ttu-id="38940-116">Toohello 虛擬機器連線。</span><span class="sxs-lookup"><span data-stu-id="38940-116">Connect toohello virtual machine.</span></span> 
2. <span data-ttu-id="38940-117">以滑鼠右鍵按一下 hello**啟動**功能表，然後選取**系統**。</span><span class="sxs-lookup"><span data-stu-id="38940-117">Right-click hello **Start** menu and select **System**.</span></span>
3. <span data-ttu-id="38940-118">在 hello 左側功能表中選取**進階系統設定**。</span><span class="sxs-lookup"><span data-stu-id="38940-118">In hello left-hand menu, select **Advanced system settings**.</span></span>
4. <span data-ttu-id="38940-119">在 hello**效能**區段中，選取**設定**。</span><span class="sxs-lookup"><span data-stu-id="38940-119">In hello **Performance** section, select **Settings**.</span></span>
5. <span data-ttu-id="38940-120">選取 hello**進階** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="38940-120">Select hello **Advanced** tab.</span></span>
6. <span data-ttu-id="38940-121">在 hello**虛擬記憶體**區段中，選取**變更**。</span><span class="sxs-lookup"><span data-stu-id="38940-121">In hello **Virtual memory** section, select **Change**.</span></span>
7. <span data-ttu-id="38940-122">選取 hello **C**磁碟機，然後按一下**系統管理大小**，然後按一下**設定**。</span><span class="sxs-lookup"><span data-stu-id="38940-122">Select hello **C** drive and then click **System managed size** and then click **Set**.</span></span>
8. <span data-ttu-id="38940-123">選取 hello **D**磁碟機，然後按一下**沒有分頁檔**，然後按一下**設定**。</span><span class="sxs-lookup"><span data-stu-id="38940-123">Select hello **D** drive and then click **No paging file** and then click **Set**.</span></span>
9. <span data-ttu-id="38940-124">按一下 [套用]。</span><span class="sxs-lookup"><span data-stu-id="38940-124">Click Apply.</span></span> <span data-ttu-id="38940-125">您會收到警告，該 hello 電腦需要 toobe hello 變更 tootake 會影響重新啟動。</span><span class="sxs-lookup"><span data-stu-id="38940-125">You will get a warning that hello computer needs toobe restarted for hello changes tootake affect.</span></span>
10. <span data-ttu-id="38940-126">重新啟動 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="38940-126">Restart hello virtual machine.</span></span>

## <a name="change-hello-drive-letters"></a><span data-ttu-id="38940-127">變更 hello 磁碟機代號</span><span class="sxs-lookup"><span data-stu-id="38940-127">Change hello drive letters</span></span>
1. <span data-ttu-id="38940-128">一次 hello VM 重新啟動時，登入 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="38940-128">Once hello VM restarts, log back on toohello VM.</span></span>
2. <span data-ttu-id="38940-129">按一下 hello**啟動**功能表和型別**diskmgmt.msc**並按下 Enter。</span><span class="sxs-lookup"><span data-stu-id="38940-129">Click hello **Start** menu and type **diskmgmt.msc** and hit Enter.</span></span> <span data-ttu-id="38940-130">隨即會啟動「磁碟管理」。</span><span class="sxs-lookup"><span data-stu-id="38940-130">Disk Management will start.</span></span>
3. <span data-ttu-id="38940-131">以滑鼠右鍵按一下**D**，hello 暫存磁碟機，然後選取 **變更磁碟機代號及路徑**。</span><span class="sxs-lookup"><span data-stu-id="38940-131">Right-click on **D**, hello Temporary Storage drive, and select **Change Drive Letter and Paths**.</span></span>
4. <span data-ttu-id="38940-132">在磁碟機代號下方，選取新的磁碟機 (例如 **T**)，然後按一下確定。</span><span class="sxs-lookup"><span data-stu-id="38940-132">Under Drive letter, select a new drive such as **T** and then click **OK**.</span></span> 
5. <span data-ttu-id="38940-133">以滑鼠右鍵按一下 hello 資料磁碟，然後選取**變更磁碟機代號及路徑**。</span><span class="sxs-lookup"><span data-stu-id="38940-133">Right-click on hello data disk, and select **Change Drive Letter and Paths**.</span></span>
6. <span data-ttu-id="38940-134">在 磁碟機代號 下方，選取磁碟機 **D**，然後按一下確定。</span><span class="sxs-lookup"><span data-stu-id="38940-134">Under Drive letter, select drive **D** and then click **OK**.</span></span> 

## <a name="move-pagefilesys-back-toohello-temporary-storage-drive"></a><span data-ttu-id="38940-135">將 pagefile.sys 後 toohello 暫存磁碟機</span><span class="sxs-lookup"><span data-stu-id="38940-135">Move pagefile.sys back toohello temporary storage drive</span></span>
1. <span data-ttu-id="38940-136">以滑鼠右鍵按一下 hello**啟動**功能表，然後選取**系統**</span><span class="sxs-lookup"><span data-stu-id="38940-136">Right-click hello **Start** menu and select **System**</span></span>
2. <span data-ttu-id="38940-137">在 hello 左側功能表中選取**進階系統設定**。</span><span class="sxs-lookup"><span data-stu-id="38940-137">In hello left-hand menu, select **Advanced system settings**.</span></span>
3. <span data-ttu-id="38940-138">在 hello**效能**區段中，選取**設定**。</span><span class="sxs-lookup"><span data-stu-id="38940-138">In hello **Performance** section, select **Settings**.</span></span>
4. <span data-ttu-id="38940-139">選取 hello**進階** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="38940-139">Select hello **Advanced** tab.</span></span>
5. <span data-ttu-id="38940-140">在 hello**虛擬記憶體**區段中，選取**變更**。</span><span class="sxs-lookup"><span data-stu-id="38940-140">In hello **Virtual memory** section, select **Change**.</span></span>
6. <span data-ttu-id="38940-141">選取 hello 作業系統磁碟機**C**按一下**沒有分頁檔**，然後按一下**設定**。</span><span class="sxs-lookup"><span data-stu-id="38940-141">Select hello OS drive **C** and click **No paging file** and then click **Set**.</span></span>
7. <span data-ttu-id="38940-142">選取 hello 暫存磁碟機**T** ，然後按一下**系統管理大小**，然後按一下**設定**。</span><span class="sxs-lookup"><span data-stu-id="38940-142">Select hello temporary storage drive **T** and then click **System managed size** and then click **Set**.</span></span>
8. <span data-ttu-id="38940-143">按一下 [Apply (套用)] 。</span><span class="sxs-lookup"><span data-stu-id="38940-143">Click **Apply**.</span></span> <span data-ttu-id="38940-144">您會收到警告，該 hello 電腦需要 toobe hello 變更 tootake 會影響重新啟動。</span><span class="sxs-lookup"><span data-stu-id="38940-144">You will get a warning that hello computer needs toobe restarted for hello changes tootake affect.</span></span>
9. <span data-ttu-id="38940-145">重新啟動 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="38940-145">Restart hello virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="38940-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="38940-146">Next steps</span></span>
* <span data-ttu-id="38940-147">您可以增加 hello 儲存體可用 tooyour 虛擬機器的[附加額外的資料磁碟](attach-managed-disk-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="38940-147">You can increase hello storage available tooyour virtual machine by [attaching a additional data disk](attach-managed-disk-portal.md).</span></span>

