---
title: "針對在傳統部署中刪除 Azure 儲存體帳戶、容器或 VHD 進行疑難排解 | Microsoft Docs"
description: "針對在傳統部署中刪除 Azure 儲存體帳戶、容器或 VHD 進行疑難排解"
services: storage
documentationcenter: 
author: genlin
manager: felixwu
editor: tysonn
tags: storage
ms.assetid: 0f7a8243-d8dc-432a-9d37-1272a0cb3a5c
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 9f3e824414ad6c1a0aba98a3d549ee63ddc7272f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-deleting-azure-storage-accounts-containers-or-vhds-in-a-classic-deployment"></a><span data-ttu-id="1c745-103">針對在傳統部署中刪除 Azure 儲存體帳戶、容器或 VHD 進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="1c745-103">Troubleshoot deleting Azure storage accounts, containers, or VHDs in a classic deployment</span></span>
[!INCLUDE [storage-selector-cannot-delete-storage-account-container-vhd](../../includes/storage-selector-cannot-delete-storage-account-container-vhd.md)]

<span data-ttu-id="1c745-104">當您嘗試刪除 [Azure 入口網站](https://portal.azure.com/)或 [Azure 傳統入口網站](https://manage.windowsazure.com/)中的 Azure 儲存體帳戶、容器或 VHD 時，可能會收到錯誤。</span><span class="sxs-lookup"><span data-stu-id="1c745-104">You might receive errors when you try to delete the Azure storage account, container, or VHD in the [Azure portal](https://portal.azure.com/) or the [Azure classic portal](https://manage.windowsazure.com/).</span></span> <span data-ttu-id="1c745-105">下列情況可能造成問題︰</span><span class="sxs-lookup"><span data-stu-id="1c745-105">The issues can be caused by the following circumstances:</span></span>

* <span data-ttu-id="1c745-106">當您刪除 VM 時，磁碟和 VHD 不會自動刪除。</span><span class="sxs-lookup"><span data-stu-id="1c745-106">When you delete a VM, the disk and VHD are not automatically deleted.</span></span> <span data-ttu-id="1c745-107">這可能是儲存體帳戶刪除失敗的原因。</span><span class="sxs-lookup"><span data-stu-id="1c745-107">That might be the reason for failure on storage account deletion.</span></span> <span data-ttu-id="1c745-108">我們不會刪除磁碟，讓您可以使用該磁碟來裝載另一個 VM。</span><span class="sxs-lookup"><span data-stu-id="1c745-108">We don't delete the disk so that you can use the disk to mount another VM.</span></span>
* <span data-ttu-id="1c745-109">磁碟上仍有租用或有與磁碟相關聯的 blob。</span><span class="sxs-lookup"><span data-stu-id="1c745-109">There is still a lease on a disk or the blob that's associated with the disk.</span></span>
* <span data-ttu-id="1c745-110">仍有正在使用 Blob、容器或儲存體帳戶的 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="1c745-110">There is still a VM image that is using a blob, container, or storage account.</span></span>

<span data-ttu-id="1c745-111">若本文中未提及您的 Azure 問題，請造訪 [MSDN 及 Stack Overflow 上的 Azure 論壇](https://azure.microsoft.com/support/forums/)。</span><span class="sxs-lookup"><span data-stu-id="1c745-111">If your Azure issue is not addressed in this article, visit the Azure forums on [MSDN and the Stack Overflow](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="1c745-112">您可以在這些論壇上張貼您的問題，或將問題貼到 Twitter 上的 @AzureSupport。</span><span class="sxs-lookup"><span data-stu-id="1c745-112">You can post your issue on these forums or to @AzureSupport on Twitter.</span></span> <span data-ttu-id="1c745-113">此外，您也可以選取 [Azure 支援](https://azure.microsoft.com/support/options/)網站上的 [取得支援]，來提出 Azure 支援要求。</span><span class="sxs-lookup"><span data-stu-id="1c745-113">Also, you can file an Azure support request by selecting **Get support** on the [Azure support](https://azure.microsoft.com/support/options/) site.</span></span>

## <a name="symptoms"></a><span data-ttu-id="1c745-114">徵兆</span><span class="sxs-lookup"><span data-stu-id="1c745-114">Symptoms</span></span>
<span data-ttu-id="1c745-115">下列章節列出您在嘗試刪除 Azure 儲存體帳戶、容器或 VHD 時可能收到的常見錯誤。</span><span class="sxs-lookup"><span data-stu-id="1c745-115">The following section lists common errors that you might receive when you try to delete the Azure storage accounts, containers, or VHDs.</span></span>

### <a name="scenario-1-unable-to-delete-a-storage-account"></a><span data-ttu-id="1c745-116">案例 1：無法刪除儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="1c745-116">Scenario 1: Unable to delete a storage account</span></span>
<span data-ttu-id="1c745-117">當您在 [Azure 入口網站](https://portal.azure.com/)中瀏覽至傳統儲存體帳戶，並選取 [刪除] 時，可能會出現妨礙刪除儲存體帳戶的物件清單︰</span><span class="sxs-lookup"><span data-stu-id="1c745-117">When you navigate to the classic storage account in the [Azure portal](https://portal.azure.com/) and select **Delete**, you may be presented with a list of objects that are preventing deletion of the storage account:</span></span>

  ![刪除儲存體帳戶時發生錯誤的映像](./media/storage-cannot-delete-storage-account-container-vhd/newerror.png)

<span data-ttu-id="1c745-119">當您在 [Azure 傳統入口網站](https://manage.windowsazure.com/)中瀏覽至儲存體帳戶，並選取 [刪除]時，您可能會看到下列其中一個錯誤︰</span><span class="sxs-lookup"><span data-stu-id="1c745-119">When you navigate to the storage account in the [Azure classic portal](https://manage.windowsazure.com/) and select **Delete**, you might see one of the following errors:</span></span>

- <span data-ttu-id="1c745-120">儲存體帳戶 StorageAccountName 包含 VM 映像。確認這些 VM 映像已移除之後再刪除此儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1c745-120">*Storage account StorageAccountName contains VM Images. Ensure these VM Images are removed before deleting this storage account.*</span></span>

- <span data-ttu-id="1c745-121">*無法刪除儲存體帳戶 <vm-storage-account-name>。無法刪除儲存體帳戶 <vm-storage-account-name>：儲存體帳戶 <vm-storage-account-name> 有些作用中的映像及/或磁碟。確認這些映像及/或磁碟已移除之後再刪除此儲存體帳戶。」*</span><span class="sxs-lookup"><span data-stu-id="1c745-121">*Failed to delete storage account <vm-storage-account-name>. Unable to delete storage account <vm-storage-account-name>: 'Storage account <vm-storage-account-name> has some active image(s) and/or disk(s). Ensure these image(s) and/or disk(s) are removed before deleting this storage account.'.*</span></span>

- <span data-ttu-id="1c745-122">*儲存體帳戶 <vm-storage-account-name> 有某些作用中的映像及/或磁碟，例如 xxxxxxxxx- xxxxxxxxx-O-209490240936090599。確認這些映像及/或磁碟已移除之後再刪除此儲存體帳戶。*</span><span class="sxs-lookup"><span data-stu-id="1c745-122">*Storage account <vm-storage-account-name> has some active image(s) and/or disk(s), e.g. xxxxxxxxx- xxxxxxxxx-O-209490240936090599. Ensure these image(s) and/or disk(s) are removed before deleting this storage account.*</span></span>

- <span data-ttu-id="1c745-123">*儲存體帳戶 <vm-storage-account-name> 已有 1 個具備作用中映像及/或磁碟成品的容器。請確定這些成品已從映像儲存機制移除之後再刪除此儲存體帳戶。*</span><span class="sxs-lookup"><span data-stu-id="1c745-123">*Storage account <vm-storage-account-name> has 1 container(s) which have an active image and/or disk artifacts. Ensure those artifacts are removed from the image repository before deleting this storage account*.</span></span>

- <span data-ttu-id="1c745-124">*提交失敗的儲存體帳戶 <vm-storage-account-name> 已有 1 個具備作用中映像及/或磁碟成品的容器。請確定這些成品已從映像儲存機制移除之後再刪除此儲存體帳戶。當您嘗試刪除儲存體帳戶，而且具有與其相關聯的磁碟仍在作用中時，您會看到一則訊息，告訴您有需要刪除的作用中磁碟*。</span><span class="sxs-lookup"><span data-stu-id="1c745-124">*Submit Failed Storage account <vm-storage-account-name> has 1 container(s) which have an active image and/or disk artifacts. Ensure those artifacts are removed from the image repository before deleting this storage account. When you attempt to delete a storage account and there are still active disks associated with it, you will see a message telling you there are active disks that need to be deleted*.</span></span>

### <a name="scenario-2-unable-to-delete-a-container"></a><span data-ttu-id="1c745-125">案例 2：無法刪除容器</span><span class="sxs-lookup"><span data-stu-id="1c745-125">Scenario 2: Unable to delete a container</span></span>
<span data-ttu-id="1c745-126">當您嘗試刪除儲存體容器時，您可能會看到下列錯誤︰</span><span class="sxs-lookup"><span data-stu-id="1c745-126">When you try to delete the storage container, you might see the following error:</span></span>

<span data-ttu-id="1c745-127">無法刪除儲存體容器 <container name>。*錯誤：「目前容器上沒有租用，且要求中沒有指定任何租用識別碼*。</span><span class="sxs-lookup"><span data-stu-id="1c745-127">*Failed to delete storage container <container name>. Error: 'There is currently a lease on the container and no lease ID was specified in the request*.</span></span>

<span data-ttu-id="1c745-128">或</span><span class="sxs-lookup"><span data-stu-id="1c745-128">Or</span></span>

<span data-ttu-id="1c745-129">「下列虛擬機器磁碟使用這個容器中的 Blob，因此無法刪除容器: VirtualMachineDiskName1, VirtualMachineDiskName2, ...」</span><span class="sxs-lookup"><span data-stu-id="1c745-129">*The following virtual machine disks use blobs in this container, so the container cannot be deleted: VirtualMachineDiskName1, VirtualMachineDiskName2, ...*</span></span>

### <a name="scenario-3-unable-to-delete-a-vhd"></a><span data-ttu-id="1c745-130">案例 3：無法刪除 VHD</span><span class="sxs-lookup"><span data-stu-id="1c745-130">Scenario 3: Unable to delete a VHD</span></span>
<span data-ttu-id="1c745-131">在您刪除 VM，然後嘗試刪除相關聯的 blob 之後，您可能會收到下列訊息︰</span><span class="sxs-lookup"><span data-stu-id="1c745-131">After you delete a VM and then try to delete the blobs for the associated VHDs, you might receive the following message:</span></span>

<span data-ttu-id="1c745-132">*無法刪除 blob 'path/XXXXXX-XXXXXX-os-1447379084699.vhd'。錯誤：「目前 blob 上沒有租用，且要求中沒有指定任何租用識別碼。*</span><span class="sxs-lookup"><span data-stu-id="1c745-132">*Failed to delete blob 'path/XXXXXX-XXXXXX-os-1447379084699.vhd'. Error: 'There is currently a lease on the blob and no lease ID was specified in the request.*</span></span>

<span data-ttu-id="1c745-133">或</span><span class="sxs-lookup"><span data-stu-id="1c745-133">Or</span></span>

<span data-ttu-id="1c745-134">「Blob 'BlobName.vhd' 正當做虛擬機器磁碟 'VirtualMachineDiskName' 使用，因此無法刪除。」</span><span class="sxs-lookup"><span data-stu-id="1c745-134">*Blob 'BlobName.vhd' is in use as virtual machine disk 'VirtualMachineDiskName', so the blob cannot be deleted.*</span></span>

## <a name="solution"></a><span data-ttu-id="1c745-135">方案</span><span class="sxs-lookup"><span data-stu-id="1c745-135">Solution</span></span>
<span data-ttu-id="1c745-136">若要解決最常見的問題，請嘗試下列方法︰</span><span class="sxs-lookup"><span data-stu-id="1c745-136">To resolve the most common issues, try the following method:</span></span>

### <a name="step-1-delete-any-disks-that-are-preventing-deletion-of-the-storage-account-container-or-vhd"></a><span data-ttu-id="1c745-137">步驟 1︰刪除任何會阻止您刪除儲存體帳戶、容器或 VHD 的磁碟</span><span class="sxs-lookup"><span data-stu-id="1c745-137">Step 1: Delete any disks that are preventing deletion of the storage account, container, or VHD</span></span>
1. <span data-ttu-id="1c745-138">切換至 [Azure 傳統入口網站](https://manage.windowsazure.com/)。</span><span class="sxs-lookup"><span data-stu-id="1c745-138">Switch to the [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="1c745-139">選取 [虛擬機器] > [磁碟]。</span><span class="sxs-lookup"><span data-stu-id="1c745-139">Select **VIRTUAL MACHINE** > **DISKS**.</span></span>

    ![Azure 傳統入口網站上虛擬機器上的磁碟影像。](./media/storage-cannot-delete-storage-account-container-vhd/VMUI.png)
3. <span data-ttu-id="1c745-141">找出與您想要刪除的儲存體帳戶、容器或 VHD 相關聯的磁碟。</span><span class="sxs-lookup"><span data-stu-id="1c745-141">Locate the disks that are associated with the storage account, container, or VHD that you want to delete.</span></span> <span data-ttu-id="1c745-142">檢查磁碟的位置時，您會發現相關聯的儲存體帳戶、容器或 VHD。</span><span class="sxs-lookup"><span data-stu-id="1c745-142">When you check the location of the disk, you will find the associated storage account, container, or VHD.</span></span>

    ![顯示 Azure 傳統入口網站上磁碟的位置資訊的影像](./media/storage-cannot-delete-storage-account-container-vhd/DiskLocation.png)
4. <span data-ttu-id="1c745-144">使用下列其中一種方法刪除磁碟：</span><span class="sxs-lookup"><span data-stu-id="1c745-144">Delete the disks by using one of the following methods:</span></span>

  - <span data-ttu-id="1c745-145">如果在磁碟的 [已連接到] 欄位上沒有列出 VM，您可以直接刪除磁碟。</span><span class="sxs-lookup"><span data-stu-id="1c745-145">If  there is no VM listed on the **Attached To** field of the disk, you can delete the disk directly.</span></span>

  - <span data-ttu-id="1c745-146">如果磁碟是資料磁碟，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1c745-146">If the disk is a data disk, follow these steps:</span></span>

    1. <span data-ttu-id="1c745-147">檢查磁碟所連接之 VM 的名稱。</span><span class="sxs-lookup"><span data-stu-id="1c745-147">Check the name of the VM that the disk is attached to.</span></span>
    2. <span data-ttu-id="1c745-148">移至 [虛擬機器] > [執行個體]，然後尋找 VM。</span><span class="sxs-lookup"><span data-stu-id="1c745-148">Go to **Virtual Machines** > **Instances**, and then locate the VM.</span></span>
    3. <span data-ttu-id="1c745-149">確定沒有任何項目會主動使用磁碟。</span><span class="sxs-lookup"><span data-stu-id="1c745-149">Make sure that nothing is actively using the disk.</span></span>
    4. <span data-ttu-id="1c745-150">選取入口網站底部的 [卸離磁碟] 以卸離磁碟。</span><span class="sxs-lookup"><span data-stu-id="1c745-150">Select **Detach Disk** at the bottom of the portal to detach the disk.</span></span>
    5. <span data-ttu-id="1c745-151">移至 [虛擬機器] > [磁碟]，並等候 [已連接到] 欄位轉為空白。</span><span class="sxs-lookup"><span data-stu-id="1c745-151">Go to **Virtual Machines** > **Disks**, and wait for the **Attached To** field to turn blank.</span></span> <span data-ttu-id="1c745-152">這表示磁碟已成功從 VM 卸離。</span><span class="sxs-lookup"><span data-stu-id="1c745-152">This indicates the disk has successfully detached from the VM.</span></span>
    6. <span data-ttu-id="1c745-153">選取 [虛擬機器] > [磁碟] 底部的 [刪除] 來刪除磁碟。</span><span class="sxs-lookup"><span data-stu-id="1c745-153">Select **Delete** at the bottom of **Virtual Machines** > **Disks** to delete the disk.</span></span>

  - <span data-ttu-id="1c745-154">如果磁碟是作業系統磁碟 ([包含作業系統] 欄位有值，例如 Windows) 並已連接到 VM，請遵循下列步驟來刪除 VM。</span><span class="sxs-lookup"><span data-stu-id="1c745-154">If the disk is an OS disk (the **Contains OS** field has a value like Windows) and attached to a VM, follow these steps to delete the VM.</span></span> <span data-ttu-id="1c745-155">作業系統磁碟無法卸離，因此我們必須刪除 VM 才能釋放租用。</span><span class="sxs-lookup"><span data-stu-id="1c745-155">The OS disk cannot be detached, so we have to delete the VM to release the lease.</span></span>

    1. <span data-ttu-id="1c745-156">檢查 [資料磁碟] 所連接到的虛擬機器名稱。</span><span class="sxs-lookup"><span data-stu-id="1c745-156">Check the name of the Virtual Machine the Data Disk is attached to.</span></span>  
    2. <span data-ttu-id="1c745-157">移至 [虛擬機器] > [執行個體]，然後選取磁碟所連接到的 VM。</span><span class="sxs-lookup"><span data-stu-id="1c745-157">Go to **Virtual Machines** > **Instances**, and then select the VM that the disk is attached to.</span></span>
    3. <span data-ttu-id="1c745-158">確定沒有正在使用虛擬機器的項目，而且您不再需要虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1c745-158">Make sure that nothing is actively using the virtual machine, and that you no longer need the virtual machine.</span></span>
    4. <span data-ttu-id="1c745-159">選取磁碟所連接到的 VM，然後選取 [刪除] > [刪除已連接磁碟]。</span><span class="sxs-lookup"><span data-stu-id="1c745-159">Select the VM the disk is attached to, then select **Delete** > **Delete the attached disks**.</span></span>
    5. <span data-ttu-id="1c745-160">移至 [虛擬機器] > [磁碟]，並等候磁碟消失。</span><span class="sxs-lookup"><span data-stu-id="1c745-160">Go to **Virtual Machines** > **Disks**, and wait for the disk to disappear.</span></span>  <span data-ttu-id="1c745-161">這可能需要幾分鐘才會完成，且您可能需要重新整理頁面。</span><span class="sxs-lookup"><span data-stu-id="1c745-161">It may take a few minutes for this to occur, and you may need to refresh the page.</span></span>
    6. <span data-ttu-id="1c745-162">如果磁碟沒有消失，請等候 [已連接到] 欄位轉為空白。</span><span class="sxs-lookup"><span data-stu-id="1c745-162">If the disk does not disappear, wait for the **Attached To** field to turn blank.</span></span> <span data-ttu-id="1c745-163">這表示磁碟已完全從 VM 卸離。</span><span class="sxs-lookup"><span data-stu-id="1c745-163">This indicates the disk has fully detached from the VM.</span></span>  <span data-ttu-id="1c745-164">接著，選取磁碟，然後選取頁面底部的 [刪除] 以刪除磁碟。</span><span class="sxs-lookup"><span data-stu-id="1c745-164">Then, select the disk, and select **Delete** at the bottom of the page to delete the disk.</span></span>


   > [!NOTE]
   > <span data-ttu-id="1c745-165">如果磁碟連接到 VM，您將無法刪除它。</span><span class="sxs-lookup"><span data-stu-id="1c745-165">If a disk is attached to a VM, you will not be able to delete it.</span></span> <span data-ttu-id="1c745-166">磁碟會以非同步的方式中斷連接已刪除的 VM。</span><span class="sxs-lookup"><span data-stu-id="1c745-166">Disks are detached from a deleted VM asynchronously.</span></span> <span data-ttu-id="1c745-167">刪除 VM 之後，可能需要幾分鐘，此欄位才能清除。</span><span class="sxs-lookup"><span data-stu-id="1c745-167">It might take a few minutes after the VM is deleted for this field to clear up.</span></span>
   >
   >


### <a name="step-2-delete-any-vm-images-that-are-preventing-deletion-of-the-storage-account-or-container"></a><span data-ttu-id="1c745-168">步驟 2︰刪除任何會阻止您刪除儲存體帳戶或容器的 VM 映像</span><span class="sxs-lookup"><span data-stu-id="1c745-168">Step 2: Delete any VM Images that are preventing deletion of the storage account or container</span></span>
1. <span data-ttu-id="1c745-169">切換至 [Azure 傳統入口網站](https://manage.windowsazure.com/)。</span><span class="sxs-lookup"><span data-stu-id="1c745-169">Switch to the [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="1c745-170">選取 [虛擬機器] > [映像]，然後刪除與儲存體帳戶、容器或 VHD 相關聯的映像。</span><span class="sxs-lookup"><span data-stu-id="1c745-170">Select **VIRTUAL MACHINE** > **IMAGES**, and then delete the images that are associated with the storage account, container, or VHD.</span></span>

    <span data-ttu-id="1c745-171">接下來，嘗試再次刪除儲存體帳戶、容器或 VHD。</span><span class="sxs-lookup"><span data-stu-id="1c745-171">After that, try to delete the storage account, container, or VHD again.</span></span>

> [!WARNING]
> <span data-ttu-id="1c745-172">請務必先備份您想要儲存的任何資料，再刪除帳戶。</span><span class="sxs-lookup"><span data-stu-id="1c745-172">Be sure to back up anything you want to save before you delete the account.</span></span> <span data-ttu-id="1c745-173">刪除 VHD、blob、資料表、佇列或檔案就是永久刪除。</span><span class="sxs-lookup"><span data-stu-id="1c745-173">Once you delete a VHD, blob, table, queue, or file, it is permanently deleted.</span></span> <span data-ttu-id="1c745-174">確定資源不在使用中。</span><span class="sxs-lookup"><span data-stu-id="1c745-174">Ensure that the resource is not in use.</span></span>
>
>

## <a name="about-the-stopped-deallocated-status"></a><span data-ttu-id="1c745-175">關於已停止 (已解除配置) 狀態</span><span class="sxs-lookup"><span data-stu-id="1c745-175">About the Stopped (deallocated) status</span></span>
<span data-ttu-id="1c745-176">已在傳統部署模型中建立並已保留的 VM 將在 [Azure 入口網站](https://portal.azure.com/)或 [Azure 傳統入口網站](https://manage.windowsazure.com/)上具有 [已停止 (已解除配置)] 狀態。</span><span class="sxs-lookup"><span data-stu-id="1c745-176">VMs that were created in the classic deployment model and that have been retained will have the **Stopped (deallocated)** status on either the [Azure portal](https://portal.azure.com/) or [Azure classic portal](https://manage.windowsazure.com/).</span></span>

<span data-ttu-id="1c745-177">**Azure 傳統入口網站**：</span><span class="sxs-lookup"><span data-stu-id="1c745-177">**Azure classic portal**:</span></span>

![Azure 入口網站上 VM 的已停止 (已解除配置) 狀態。](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo2.png)

<span data-ttu-id="1c745-179">**Azure 入口網站**︰</span><span class="sxs-lookup"><span data-stu-id="1c745-179">**Azure portal**:</span></span>

![Azure 傳統入口網站上 VM 的已停止 (已解除配置) 狀態。](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo1.png)

<span data-ttu-id="1c745-181">「已停止 (已解除配置)」狀態會釋出電腦資源，例如 CPU、記憶體和網路。</span><span class="sxs-lookup"><span data-stu-id="1c745-181">A "Stopped (deallocated)" status releases the computer resources, such as the CPU, memory, and network.</span></span> <span data-ttu-id="1c745-182">不過，磁碟仍會保留，以便您可在需要時快速重新建立 VM。</span><span class="sxs-lookup"><span data-stu-id="1c745-182">The disks, however, are still retained so that you can quickly re-create the VM if necessary.</span></span> <span data-ttu-id="1c745-183">這些磁碟都建立在由 Azure 儲存體提供的 VHD 上。</span><span class="sxs-lookup"><span data-stu-id="1c745-183">These disks are created on top of VHDs, which are backed by Azure storage.</span></span> <span data-ttu-id="1c745-184">儲存體帳戶具有這些 VHD，而磁碟有這些 VHD 上的租用。</span><span class="sxs-lookup"><span data-stu-id="1c745-184">The storage account has these VHDs, and the disks have leases on those VHDs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c745-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1c745-185">Next steps</span></span>
* [<span data-ttu-id="1c745-186">刪除儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="1c745-186">Delete a storage account</span></span>](storage-create-storage-account.md#delete-a-storage-account)
