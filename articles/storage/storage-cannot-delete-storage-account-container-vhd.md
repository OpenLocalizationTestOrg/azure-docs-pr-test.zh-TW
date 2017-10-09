---
title: "在傳統的部署中刪除 Azure 儲存體帳戶、 容器或 Vhd aaaTroubleshoot |Microsoft 文件"
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
ms.openlocfilehash: 6bbfa032e1968718c623227bb426d553e2951075
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deleting-azure-storage-accounts-containers-or-vhds-in-a-classic-deployment"></a><span data-ttu-id="718e6-103">針對在傳統部署中刪除 Azure 儲存體帳戶、容器或 VHD 進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="718e6-103">Troubleshoot deleting Azure storage accounts, containers, or VHDs in a classic deployment</span></span>
[!INCLUDE [storage-selector-cannot-delete-storage-account-container-vhd](../../includes/storage-selector-cannot-delete-storage-account-container-vhd.md)]

<span data-ttu-id="718e6-104">當您嘗試在 hello toodelete hello Azure 儲存體帳戶、 容器或 VHD 時，您可能會收到錯誤[Azure 入口網站](https://portal.azure.com/)或 hello [Azure 傳統入口網站](https://manage.windowsazure.com/)。</span><span class="sxs-lookup"><span data-stu-id="718e6-104">You might receive errors when you try toodelete hello Azure storage account, container, or VHD in hello [Azure portal](https://portal.azure.com/) or hello [Azure classic portal](https://manage.windowsazure.com/).</span></span> <span data-ttu-id="718e6-105">hello 問題可能被因下列情況下的 hello:</span><span class="sxs-lookup"><span data-stu-id="718e6-105">hello issues can be caused by hello following circumstances:</span></span>

* <span data-ttu-id="718e6-106">當您刪除 VM 時，hello 磁碟和 VHD 不會自動刪除。</span><span class="sxs-lookup"><span data-stu-id="718e6-106">When you delete a VM, hello disk and VHD are not automatically deleted.</span></span> <span data-ttu-id="718e6-107">可能 hello 上刪除儲存體帳戶的失敗原因。</span><span class="sxs-lookup"><span data-stu-id="718e6-107">That might be hello reason for failure on storage account deletion.</span></span> <span data-ttu-id="718e6-108">我們不刪除 hello 磁碟，以便您可以使用 hello 磁碟 toomount 另一個 VM。</span><span class="sxs-lookup"><span data-stu-id="718e6-108">We don't delete hello disk so that you can use hello disk toomount another VM.</span></span>
* <span data-ttu-id="718e6-109">仍與 hello 磁碟相關聯的磁碟或 hello blob 上的租用。</span><span class="sxs-lookup"><span data-stu-id="718e6-109">There is still a lease on a disk or hello blob that's associated with hello disk.</span></span>
* <span data-ttu-id="718e6-110">仍有正在使用 Blob、容器或儲存體帳戶的 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="718e6-110">There is still a VM image that is using a blob, container, or storage account.</span></span>

<span data-ttu-id="718e6-111">如果這份文件中並未提及您的 Azure 問題，請瀏覽 hello Azure 論壇上[MSDN 和 hello 堆疊溢位](https://azure.microsoft.com/support/forums/)。</span><span class="sxs-lookup"><span data-stu-id="718e6-111">If your Azure issue is not addressed in this article, visit hello Azure forums on [MSDN and hello Stack Overflow](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="718e6-112">您可以在這些論壇張貼您的問題或too@AzureSupportTwitter 上。</span><span class="sxs-lookup"><span data-stu-id="718e6-112">You can post your issue on these forums or too@AzureSupport on Twitter.</span></span> <span data-ttu-id="718e6-113">此外，您可以藉由選取檔案 Azure 支援人員要求**取得支援**上 hello [Azure 支援](https://azure.microsoft.com/support/options/)站台。</span><span class="sxs-lookup"><span data-stu-id="718e6-113">Also, you can file an Azure support request by selecting **Get support** on hello [Azure support](https://azure.microsoft.com/support/options/) site.</span></span>

## <a name="symptoms"></a><span data-ttu-id="718e6-114">徵兆</span><span class="sxs-lookup"><span data-stu-id="718e6-114">Symptoms</span></span>
<span data-ttu-id="718e6-115">hello 下列區段會列出當您嘗試 toodelete hello Azure 儲存體帳戶、 容器或 Vhd 時，您可能會收到的常見錯誤。</span><span class="sxs-lookup"><span data-stu-id="718e6-115">hello following section lists common errors that you might receive when you try toodelete hello Azure storage accounts, containers, or VHDs.</span></span>

### <a name="scenario-1-unable-toodelete-a-storage-account"></a><span data-ttu-id="718e6-116">案例 1： 無法 toodelete 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="718e6-116">Scenario 1: Unable toodelete a storage account</span></span>
<span data-ttu-id="718e6-117">當您瀏覽 toohello 傳統儲存體帳戶中 hello [Azure 入口網站](https://portal.azure.com/)選取**刪除**，您可能會看到阻止 hello 儲存體帳戶刪除的物件清單：</span><span class="sxs-lookup"><span data-stu-id="718e6-117">When you navigate toohello classic storage account in hello [Azure portal](https://portal.azure.com/) and select **Delete**, you may be presented with a list of objects that are preventing deletion of hello storage account:</span></span>

  ![錯誤的映像時刪除 hello 儲存體帳戶](./media/storage-cannot-delete-storage-account-container-vhd/newerror.png)

<span data-ttu-id="718e6-119">當您瀏覽 toohello 儲存體帳戶中 hello [Azure 傳統入口網站](https://manage.windowsazure.com/)選取**刪除**，您可能會看到下列錯誤 hello 的其中一個：</span><span class="sxs-lookup"><span data-stu-id="718e6-119">When you navigate toohello storage account in hello [Azure classic portal](https://manage.windowsazure.com/) and select **Delete**, you might see one of hello following errors:</span></span>

- <span data-ttu-id="718e6-120">儲存體帳戶 StorageAccountName 包含 VM 映像。確認這些 VM 映像已移除之後再刪除此儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="718e6-120">*Storage account StorageAccountName contains VM Images. Ensure these VM Images are removed before deleting this storage account.*</span></span>

- <span data-ttu-id="718e6-121">*無法 toodelete 儲存體帳戶 < vm 的儲存體帳戶的名稱 >。無法 toodelete 儲存體帳戶 < vm 的儲存體帳戶的名稱 >: ' < vm 的儲存體帳戶的名稱 > 的儲存體帳戶有一些作用中的映像及/或磁碟。確認這些映像及/或磁碟已移除之後再刪除此儲存體帳戶。」*</span><span class="sxs-lookup"><span data-stu-id="718e6-121">*Failed toodelete storage account <vm-storage-account-name>. Unable toodelete storage account <vm-storage-account-name>: 'Storage account <vm-storage-account-name> has some active image(s) and/or disk(s). Ensure these image(s) and/or disk(s) are removed before deleting this storage account.'.*</span></span>

- <span data-ttu-id="718e6-122">*儲存體帳戶 <vm-storage-account-name> 有某些作用中的映像及/或磁碟，例如 xxxxxxxxx- xxxxxxxxx-O-209490240936090599。確認這些映像及/或磁碟已移除之後再刪除此儲存體帳戶。*</span><span class="sxs-lookup"><span data-stu-id="718e6-122">*Storage account <vm-storage-account-name> has some active image(s) and/or disk(s), e.g. xxxxxxxxx- xxxxxxxxx-O-209490240936090599. Ensure these image(s) and/or disk(s) are removed before deleting this storage account.*</span></span>

- <span data-ttu-id="718e6-123">*儲存體帳戶 <vm-storage-account-name> 已有 1 個具備作用中映像及/或磁碟成品的容器。請移除這些成品，hello 映像儲存機制中刪除這個儲存體帳戶之前*。</span><span class="sxs-lookup"><span data-stu-id="718e6-123">*Storage account <vm-storage-account-name> has 1 container(s) which have an active image and/or disk artifacts. Ensure those artifacts are removed from hello image repository before deleting this storage account*.</span></span>

- <span data-ttu-id="718e6-124">*提交失敗的儲存體帳戶 <vm-storage-account-name> 已有 1 個具備作用中映像及/或磁碟成品的容器。請刪除這個儲存體帳戶之前先移除這些成品從 hello 映像儲存機制。當您嘗試 toodelete 儲存體帳戶且有與其相關聯的磁碟仍在作用中時，您會看到訊息，告知您有使用中磁碟需要刪除 toobe*。</span><span class="sxs-lookup"><span data-stu-id="718e6-124">*Submit Failed Storage account <vm-storage-account-name> has 1 container(s) which have an active image and/or disk artifacts. Ensure those artifacts are removed from hello image repository before deleting this storage account. When you attempt toodelete a storage account and there are still active disks associated with it, you will see a message telling you there are active disks that need toobe deleted*.</span></span>

### <a name="scenario-2-unable-toodelete-a-container"></a><span data-ttu-id="718e6-125">案例 2： 無法 toodelete 容器</span><span class="sxs-lookup"><span data-stu-id="718e6-125">Scenario 2: Unable toodelete a container</span></span>
<span data-ttu-id="718e6-126">當您嘗試 toodelete hello 儲存體容器時，您可能會看到下列錯誤 hello:</span><span class="sxs-lookup"><span data-stu-id="718e6-126">When you try toodelete hello storage container, you might see hello following error:</span></span>

<span data-ttu-id="718e6-127">*失敗的 toodelete 儲存體容器<container name>。錯誤: ' 目前沒有租用 hello 容器和 hello 要求中指定任何租用識別碼*。</span><span class="sxs-lookup"><span data-stu-id="718e6-127">*Failed toodelete storage container <container name>. Error: 'There is currently a lease on hello container and no lease ID was specified in hello request*.</span></span>

<span data-ttu-id="718e6-128">或</span><span class="sxs-lookup"><span data-stu-id="718e6-128">Or</span></span>

<span data-ttu-id="718e6-129">*hello 下列虛擬機器磁碟使用在此容器中的 blob，因此無法刪除 hello 容器： VirtualMachineDiskName1、 VirtualMachineDiskName2，...*</span><span class="sxs-lookup"><span data-stu-id="718e6-129">*hello following virtual machine disks use blobs in this container, so hello container cannot be deleted: VirtualMachineDiskName1, VirtualMachineDiskName2, ...*</span></span>

### <a name="scenario-3-unable-toodelete-a-vhd"></a><span data-ttu-id="718e6-130">案例 3： 無法 toodelete VHD</span><span class="sxs-lookup"><span data-stu-id="718e6-130">Scenario 3: Unable toodelete a VHD</span></span>
<span data-ttu-id="718e6-131">刪除 VM，然後再試一次 toodelete hello blob hello 相關聯的 Vhd 之後，您可能會收到下列訊息的 hello:</span><span class="sxs-lookup"><span data-stu-id="718e6-131">After you delete a VM and then try toodelete hello blobs for hello associated VHDs, you might receive hello following message:</span></span>

<span data-ttu-id="718e6-132">*失敗的 toodelete blob ' 路徑/XXXXXX XXXXXX-os-1447379084699.vhd'。錯誤: ' 目前沒有租用 hello blob 上，而且 hello 要求中指定任何租用識別碼。*</span><span class="sxs-lookup"><span data-stu-id="718e6-132">*Failed toodelete blob 'path/XXXXXX-XXXXXX-os-1447379084699.vhd'. Error: 'There is currently a lease on hello blob and no lease ID was specified in hello request.*</span></span>

<span data-ttu-id="718e6-133">或</span><span class="sxs-lookup"><span data-stu-id="718e6-133">Or</span></span>

<span data-ttu-id="718e6-134">*Blob 'BlobName.vhd' 是正當做虛擬機器磁碟 'VirtualMachineDiskName'，因此無法刪除 hello blob。*</span><span class="sxs-lookup"><span data-stu-id="718e6-134">*Blob 'BlobName.vhd' is in use as virtual machine disk 'VirtualMachineDiskName', so hello blob cannot be deleted.*</span></span>

## <a name="solution"></a><span data-ttu-id="718e6-135">方案</span><span class="sxs-lookup"><span data-stu-id="718e6-135">Solution</span></span>
<span data-ttu-id="718e6-136">tooresolve hello 最常見的問題，請嘗試下列方法 hello:</span><span class="sxs-lookup"><span data-stu-id="718e6-136">tooresolve hello most common issues, try hello following method:</span></span>

### <a name="step-1-delete-any-disks-that-are-preventing-deletion-of-hello-storage-account-container-or-vhd"></a><span data-ttu-id="718e6-137">步驟 1： 刪除任何導致無法刪除 hello 儲存體帳戶、 容器或 VHD 的磁碟</span><span class="sxs-lookup"><span data-stu-id="718e6-137">Step 1: Delete any disks that are preventing deletion of hello storage account, container, or VHD</span></span>
1. <span data-ttu-id="718e6-138">切換 toohello [Azure 傳統入口網站](https://manage.windowsazure.com/)。</span><span class="sxs-lookup"><span data-stu-id="718e6-138">Switch toohello [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="718e6-139">選取 [虛擬機器] > [磁碟]。</span><span class="sxs-lookup"><span data-stu-id="718e6-139">Select **VIRTUAL MACHINE** > **DISKS**.</span></span>

    ![Azure 傳統入口網站上虛擬機器上的磁碟影像。](./media/storage-cannot-delete-storage-account-container-vhd/VMUI.png)
3. <span data-ttu-id="718e6-141">找出 hello 與 hello 儲存體帳戶、 容器或您想 toodelete VHD 相關聯的磁碟。</span><span class="sxs-lookup"><span data-stu-id="718e6-141">Locate hello disks that are associated with hello storage account, container, or VHD that you want toodelete.</span></span> <span data-ttu-id="718e6-142">當您檢查 hello hello 磁碟位置時，您會發現 hello 相關聯的儲存體帳戶、 容器或 VHD。</span><span class="sxs-lookup"><span data-stu-id="718e6-142">When you check hello location of hello disk, you will find hello associated storage account, container, or VHD.</span></span>

    ![顯示 Azure 傳統入口網站上磁碟的位置資訊的影像](./media/storage-cannot-delete-storage-account-container-vhd/DiskLocation.png)
4. <span data-ttu-id="718e6-144">使用其中一種 hello 下列方法刪除 hello 磁碟：</span><span class="sxs-lookup"><span data-stu-id="718e6-144">Delete hello disks by using one of hello following methods:</span></span>

  - <span data-ttu-id="718e6-145">如果沒有任何 VM 就會列在 hello**附加至**欄位的 hello 磁碟，您可以直接刪除 hello 磁碟。</span><span class="sxs-lookup"><span data-stu-id="718e6-145">If  there is no VM listed on hello **Attached To** field of hello disk, you can delete hello disk directly.</span></span>

  - <span data-ttu-id="718e6-146">如果資料磁碟 hello 磁碟，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="718e6-146">If hello disk is a data disk, follow these steps:</span></span>

    1. <span data-ttu-id="718e6-147">請檢查的 hello hello 磁碟的 VM 連接至 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="718e6-147">Check hello name of hello VM that hello disk is attached to.</span></span>
    2. <span data-ttu-id="718e6-148">跳過**虛擬機器** > **執行個體**，然後找出 hello VM。</span><span class="sxs-lookup"><span data-stu-id="718e6-148">Go too**Virtual Machines** > **Instances**, and then locate hello VM.</span></span>
    3. <span data-ttu-id="718e6-149">請確定不會主動使用 hello 磁碟。</span><span class="sxs-lookup"><span data-stu-id="718e6-149">Make sure that nothing is actively using hello disk.</span></span>
    4. <span data-ttu-id="718e6-150">選取**卸離磁碟**底部 hello hello 入口 toodetach hello 磁碟。</span><span class="sxs-lookup"><span data-stu-id="718e6-150">Select **Detach Disk** at hello bottom of hello portal toodetach hello disk.</span></span>
    5. <span data-ttu-id="718e6-151">跳過**虛擬機器** > **磁碟**，並等候 hello**附加至**欄位 tooturn 空白。</span><span class="sxs-lookup"><span data-stu-id="718e6-151">Go too**Virtual Machines** > **Disks**, and wait for hello **Attached To** field tooturn blank.</span></span> <span data-ttu-id="718e6-152">這表示已成功中斷與 hello VM 連結 hello 磁碟。</span><span class="sxs-lookup"><span data-stu-id="718e6-152">This indicates hello disk has successfully detached from hello VM.</span></span>
    6. <span data-ttu-id="718e6-153">選取**刪除**底部的 hello**虛擬機器** > **磁碟**toodelete hello 磁碟。</span><span class="sxs-lookup"><span data-stu-id="718e6-153">Select **Delete** at hello bottom of **Virtual Machines** > **Disks** toodelete hello disk.</span></span>

  - <span data-ttu-id="718e6-154">如果 hello 磁碟是作業系統磁碟 (hello**包含 OS**欄位有值，例如 Windows) 及附加的 tooa VM，請遵循下列步驟 toodelete hello VM。</span><span class="sxs-lookup"><span data-stu-id="718e6-154">If hello disk is an OS disk (hello **Contains OS** field has a value like Windows) and attached tooa VM, follow these steps toodelete hello VM.</span></span> <span data-ttu-id="718e6-155">無法中斷 hello 作業系統磁碟，因此我們 toodelete hello VM toorelease hello 租用。</span><span class="sxs-lookup"><span data-stu-id="718e6-155">hello OS disk cannot be detached, so we have toodelete hello VM toorelease hello lease.</span></span>

    1. <span data-ttu-id="718e6-156">請檢查資料磁碟附加至 hello 虛擬機器 hello hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="718e6-156">Check hello name of hello Virtual Machine hello Data Disk is attached to.</span></span>  
    2. <span data-ttu-id="718e6-157">跳過**虛擬機器** > **執行個體**，並選取 hello hello 磁碟的 VM 會附加至。</span><span class="sxs-lookup"><span data-stu-id="718e6-157">Go too**Virtual Machines** > **Instances**, and then select hello VM that hello disk is attached to.</span></span>
    3. <span data-ttu-id="718e6-158">請確定不會主動使用 hello 虛擬機器，並確認您不再需要 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="718e6-158">Make sure that nothing is actively using hello virtual machine, and that you no longer need hello virtual machine.</span></span>
    4. <span data-ttu-id="718e6-159">選取 hello VM hello 磁碟已連接，然後選取**刪除** > **刪除 hello 附加磁碟**。</span><span class="sxs-lookup"><span data-stu-id="718e6-159">Select hello VM hello disk is attached to, then select **Delete** > **Delete hello attached disks**.</span></span>
    5. <span data-ttu-id="718e6-160">跳過**虛擬機器** > **磁碟**，並等候 hello 磁碟 toodisappear。</span><span class="sxs-lookup"><span data-stu-id="718e6-160">Go too**Virtual Machines** > **Disks**, and wait for hello disk toodisappear.</span></span>  <span data-ttu-id="718e6-161">可能需要幾分鐘，讓此 toooccur，，您可能需要 toorefresh hello 頁面。</span><span class="sxs-lookup"><span data-stu-id="718e6-161">It may take a few minutes for this toooccur, and you may need toorefresh hello page.</span></span>
    6. <span data-ttu-id="718e6-162">如果 hello 磁碟並未消失，等候 hello**附加至**欄位 tooturn 空白。</span><span class="sxs-lookup"><span data-stu-id="718e6-162">If hello disk does not disappear, wait for hello **Attached To** field tooturn blank.</span></span> <span data-ttu-id="718e6-163">這表示已完全中斷與 hello VM 連結 hello 磁碟。</span><span class="sxs-lookup"><span data-stu-id="718e6-163">This indicates hello disk has fully detached from hello VM.</span></span>  <span data-ttu-id="718e6-164">接著，選取 hello 磁碟，並選取**刪除**底部 hello hello 分頁 toodelete hello 磁碟。</span><span class="sxs-lookup"><span data-stu-id="718e6-164">Then, select hello disk, and select **Delete** at hello bottom of hello page toodelete hello disk.</span></span>


   > [!NOTE]
   > <span data-ttu-id="718e6-165">如果磁碟已附加的 tooa VM，就能 toodelete 它。</span><span class="sxs-lookup"><span data-stu-id="718e6-165">If a disk is attached tooa VM, you will not be able toodelete it.</span></span> <span data-ttu-id="718e6-166">磁碟會以非同步的方式中斷連接已刪除的 VM。</span><span class="sxs-lookup"><span data-stu-id="718e6-166">Disks are detached from a deleted VM asynchronously.</span></span> <span data-ttu-id="718e6-167">可能需要幾分鐘後，設定此欄位 tooclear 刪除 hello VM。</span><span class="sxs-lookup"><span data-stu-id="718e6-167">It might take a few minutes after hello VM is deleted for this field tooclear up.</span></span>
   >
   >


### <a name="step-2-delete-any-vm-images-that-are-preventing-deletion-of-hello-storage-account-or-container"></a><span data-ttu-id="718e6-168">步驟 2： 刪除，無法刪除 hello 儲存體帳戶或容器的 VM 映像</span><span class="sxs-lookup"><span data-stu-id="718e6-168">Step 2: Delete any VM Images that are preventing deletion of hello storage account or container</span></span>
1. <span data-ttu-id="718e6-169">切換 toohello [Azure 傳統入口網站](https://manage.windowsazure.com/)。</span><span class="sxs-lookup"><span data-stu-id="718e6-169">Switch toohello [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="718e6-170">選取**虛擬機器** > **映像**，然後再刪除 hello 與 hello 儲存體帳戶、 容器或 VHD 相關聯的映像。</span><span class="sxs-lookup"><span data-stu-id="718e6-170">Select **VIRTUAL MACHINE** > **IMAGES**, and then delete hello images that are associated with hello storage account, container, or VHD.</span></span>

    <span data-ttu-id="718e6-171">在這之後，重試 toodelete hello 儲存體帳戶、 容器或 VHD。</span><span class="sxs-lookup"><span data-stu-id="718e6-171">After that, try toodelete hello storage account, container, or VHD again.</span></span>

> [!WARNING]
> <span data-ttu-id="718e6-172">刪除 hello 帳戶之前，您有想 toosave 來確定 tooback 任何項目。</span><span class="sxs-lookup"><span data-stu-id="718e6-172">Be sure tooback up anything you want toosave before you delete hello account.</span></span> <span data-ttu-id="718e6-173">刪除 VHD、blob、資料表、佇列或檔案就是永久刪除。</span><span class="sxs-lookup"><span data-stu-id="718e6-173">Once you delete a VHD, blob, table, queue, or file, it is permanently deleted.</span></span> <span data-ttu-id="718e6-174">請確認 hello 資源不是使用中。</span><span class="sxs-lookup"><span data-stu-id="718e6-174">Ensure that hello resource is not in use.</span></span>
>
>

## <a name="about-hello-stopped-deallocated-status"></a><span data-ttu-id="718e6-175">關於 hello 已停止 （取消配置） 狀態</span><span class="sxs-lookup"><span data-stu-id="718e6-175">About hello Stopped (deallocated) status</span></span>
<span data-ttu-id="718e6-176">建立 hello 傳統部署模型中，並保留的 Vm 將會有 hello**已停止 （取消配置）**狀態任一 hello [Azure 入口網站](https://portal.azure.com/)或[Azure 傳統入口網站](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="718e6-176">VMs that were created in hello classic deployment model and that have been retained will have hello **Stopped (deallocated)** status on either hello [Azure portal](https://portal.azure.com/) or [Azure classic portal](https://manage.windowsazure.com/).</span></span>

<span data-ttu-id="718e6-177">**Azure 傳統入口網站**：</span><span class="sxs-lookup"><span data-stu-id="718e6-177">**Azure classic portal**:</span></span>

![Azure 入口網站上 VM 的已停止 (已解除配置) 狀態。](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo2.png)

<span data-ttu-id="718e6-179">**Azure 入口網站**︰</span><span class="sxs-lookup"><span data-stu-id="718e6-179">**Azure portal**:</span></span>

![Azure 傳統入口網站上 VM 的已停止 (已解除配置) 狀態。](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo1.png)

<span data-ttu-id="718e6-181">「 已停止 （取消配置） 」 狀態釋放 hello 電腦資源，例如 hello CPU、 記憶體和網路。</span><span class="sxs-lookup"><span data-stu-id="718e6-181">A "Stopped (deallocated)" status releases hello computer resources, such as hello CPU, memory, and network.</span></span> <span data-ttu-id="718e6-182">hello 磁碟，不過，仍保留，因此您可以快速 hello VM 必要時重新建立。</span><span class="sxs-lookup"><span data-stu-id="718e6-182">hello disks, however, are still retained so that you can quickly re-create hello VM if necessary.</span></span> <span data-ttu-id="718e6-183">這些磁碟都建立在由 Azure 儲存體提供的 VHD 上。</span><span class="sxs-lookup"><span data-stu-id="718e6-183">These disks are created on top of VHDs, which are backed by Azure storage.</span></span> <span data-ttu-id="718e6-184">hello 儲存體帳戶的這些 Vhd，並 hello 磁碟的 Vhd 上的租用。</span><span class="sxs-lookup"><span data-stu-id="718e6-184">hello storage account has these VHDs, and hello disks have leases on those VHDs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="718e6-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="718e6-185">Next steps</span></span>
* [<span data-ttu-id="718e6-186">刪除儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="718e6-186">Delete a storage account</span></span>](storage-create-storage-account.md#delete-a-storage-account)
