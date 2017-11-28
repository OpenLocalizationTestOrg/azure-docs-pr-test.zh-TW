---
title: "針對刪除 Azure 儲存體帳戶、容器或 VHD 時所發生的錯誤進行疑難排解 | Microsoft Docs"
description: "針對刪除 Azure 儲存體帳戶、容器或 VHD 時所發生的錯誤進行疑難排解"
services: storage
documentationcenter: 
author: genlin
manager: cshepard
editor: na
tags: storage
ms.assetid: 17403aa1-fe8d-45ec-bc33-2c0b61126286
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 11944dd38b1cc30106c0b76a108480c018ca39d4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-errors-when-you-delete-azure-storage-accounts-containers-or-vhds"></a><span data-ttu-id="54b41-103">針對刪除 Azure 儲存體帳戶、容器或 VHD 時所發生的錯誤進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="54b41-103">Troubleshoot errors when you delete Azure storage accounts, containers, or VHDs</span></span>

<span data-ttu-id="54b41-104">當您嘗試刪除 [Azure 入口網站](https://portal.azure.com)中的 Azure 儲存體帳戶、容器或虛擬硬碟 (VHD) 時，可能會收到錯誤。</span><span class="sxs-lookup"><span data-stu-id="54b41-104">You might receive errors when you try to delete an Azure storage account, container, or virtual hard disk (VHD) in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="54b41-105">本文提供可協助您解決 Azure Resource Manager 部署問題的疑難排解指引。</span><span class="sxs-lookup"><span data-stu-id="54b41-105">This article provides troubleshooting guidance to help resolve the problem in an Azure Resource Manager deployment.</span></span>

<span data-ttu-id="54b41-106">若本文未能解決您的 Azure 問題，請造訪 [MSDN 與 Stack Overflow](https://azure.microsoft.com/support/forums/) 上的 Azure 論壇。</span><span class="sxs-lookup"><span data-stu-id="54b41-106">If this article doesn't address your Azure problem, visit the Azure forums on [MSDN and Stack Overflow](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="54b41-107">您可以在這些論壇上張貼您的問題，或將問題貼到 Twitter 上的 @AzureSupport。</span><span class="sxs-lookup"><span data-stu-id="54b41-107">You can post your problem on these forums or to @AzureSupport on Twitter.</span></span> <span data-ttu-id="54b41-108">此外，您也可以選取 [Azure 支援](https://azure.microsoft.com/support/options/)網站上的 [取得支援]，來提出 Azure 支援要求。</span><span class="sxs-lookup"><span data-stu-id="54b41-108">Also, you can file an Azure support request by selecting **Get support** on the [Azure support](https://azure.microsoft.com/support/options/) site.</span></span>

## <a name="symptoms"></a><span data-ttu-id="54b41-109">徵兆</span><span class="sxs-lookup"><span data-stu-id="54b41-109">Symptoms</span></span>
### <a name="scenario-1"></a><span data-ttu-id="54b41-110">案例 1</span><span class="sxs-lookup"><span data-stu-id="54b41-110">Scenario 1</span></span>
<span data-ttu-id="54b41-111">當您嘗試在 Resource Manager 部署的儲存體帳戶中刪除 VHD 時，您會收到下列錯誤訊息︰</span><span class="sxs-lookup"><span data-stu-id="54b41-111">When you try to delete a VHD in a storage account in a Resource Manager deployment, you receive the following error message:</span></span>

<span data-ttu-id="54b41-112">**無法刪除 Blob 'vhds/BlobName.vhd'。錯誤：目前 blob 上沒有租用，且要求中沒有指定任何租用識別碼。**</span><span class="sxs-lookup"><span data-stu-id="54b41-112">**Failed to delete blob 'vhds/BlobName.vhd'. Error: There is currently a lease on the blob and no lease ID was specified in the request.**</span></span>

<span data-ttu-id="54b41-113">虛擬機器 (VM) 在您嘗試刪除的 VHD 上有租用，所以會發生此問題。</span><span class="sxs-lookup"><span data-stu-id="54b41-113">This problem can occur because a virtual machine (VM) has a lease on the VHD that you are trying to delete.</span></span>

### <a name="scenario-2"></a><span data-ttu-id="54b41-114">案例 2</span><span class="sxs-lookup"><span data-stu-id="54b41-114">Scenario 2</span></span>
<span data-ttu-id="54b41-115">當您嘗試在 Resource Manager 部署的儲存體帳戶中刪除容器時，您會收到下列錯誤訊息︰</span><span class="sxs-lookup"><span data-stu-id="54b41-115">When you try to delete a container in a storage account in a Resource Manager deployment, you receive the following error message:</span></span>

<span data-ttu-id="54b41-116">**無法刪除儲存體容器 'vhds'。錯誤：目前容器上沒有租用，且要求中沒有指定任何租用識別碼。**</span><span class="sxs-lookup"><span data-stu-id="54b41-116">**Failed to delete storage container 'vhds'. Error: There is currently a lease on the container and no lease ID was specified in the request.**</span></span>

<span data-ttu-id="54b41-117">容器中有 VHD 鎖定在租用狀態，所以會發生此問題。</span><span class="sxs-lookup"><span data-stu-id="54b41-117">This problem can occur because the container has a VHD that is locked in the lease state.</span></span>

### <a name="scenario-3"></a><span data-ttu-id="54b41-118">案例 3</span><span class="sxs-lookup"><span data-stu-id="54b41-118">Scenario 3</span></span>
<span data-ttu-id="54b41-119">當您嘗試在 Resource Manager 部署中刪除儲存體帳戶時，您會收到下列錯誤訊息︰</span><span class="sxs-lookup"><span data-stu-id="54b41-119">When you try to delete a storage account in a Resource Manager deployment, you receive the following error message:</span></span>

<span data-ttu-id="54b41-120">**無法刪除儲存體帳戶 'StorageAccountName'。錯誤︰無法刪除儲存體帳戶，因為正在使用其構件。**</span><span class="sxs-lookup"><span data-stu-id="54b41-120">**Failed to delete storage account 'StorageAccountName'. Error: The storage account cannot be deleted due to its artifacts being in use.**</span></span>

<span data-ttu-id="54b41-121">儲存體帳戶含有處於租用狀態的 VHD，所以會發生此問題。</span><span class="sxs-lookup"><span data-stu-id="54b41-121">This problem can occur because the storage account contains a VHD that is in the lease state.</span></span>

## <a name="solution"></a><span data-ttu-id="54b41-122">方案</span><span class="sxs-lookup"><span data-stu-id="54b41-122">Solution</span></span> 
<span data-ttu-id="54b41-123">若要解決這些問題，您必須識別造成錯誤的 VHD 和相關聯的 VM。</span><span class="sxs-lookup"><span data-stu-id="54b41-123">To resolve these problems, you must identify the VHD that is causing the error and the associated VM.</span></span> <span data-ttu-id="54b41-124">接著，將 VHD 與 VM 中斷連結 (若為資料磁碟)，或刪除使用 VHD 的 VM (若為 OS 磁碟)。</span><span class="sxs-lookup"><span data-stu-id="54b41-124">Then, detach the VHD from the VM (for data disks) or delete the VM that is using the VHD (for OS disks).</span></span> <span data-ttu-id="54b41-125">這會從 VHD 移除租用，讓 VHD 得以被刪除。</span><span class="sxs-lookup"><span data-stu-id="54b41-125">This removes the lease from the VHD and allows it to be deleted.</span></span> 

<span data-ttu-id="54b41-126">若要這麼做，請使用下列其中一種方法：</span><span class="sxs-lookup"><span data-stu-id="54b41-126">To do this, use one of the following methods:</span></span>

### <a name="method-1---use-azure-storage-explorer"></a><span data-ttu-id="54b41-127">方法 1 - 使用 Azure 儲存體總管</span><span class="sxs-lookup"><span data-stu-id="54b41-127">Method 1 - Use Azure storage explorer</span></span>

### <a name="step-1-identify-the-vhd-that-prevent-deletion-of-the-storage-account"></a><span data-ttu-id="54b41-128">步驟 1 識別導致無法刪除儲存體帳戶的 VHD</span><span class="sxs-lookup"><span data-stu-id="54b41-128">Step 1 Identify the VHD that prevent deletion of the storage account</span></span>

1. <span data-ttu-id="54b41-129">您刪除儲存體帳戶時，將收到以下訊息對話方塊：</span><span class="sxs-lookup"><span data-stu-id="54b41-129">When you delete the storage account, you will receive a message dialog such as the following:</span></span> 

    ![刪除儲存體帳戶時的訊息](././media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. <span data-ttu-id="54b41-131">檢查**磁碟 URL**，以找出導致無法刪除儲存體帳戶的儲存體帳戶和 VHD。</span><span class="sxs-lookup"><span data-stu-id="54b41-131">Check the **Disk URL** to identify the storage account and the VHD that prevents you delete the storage account.</span></span> <span data-ttu-id="54b41-132">在下列範例中，“.blob.core.windows.net “ 是儲存體帳戶名稱，"SCCM2012-2015-08-28.vhd" 是 VHD 名稱。</span><span class="sxs-lookup"><span data-stu-id="54b41-132">In the following example, the string before “.blob.core.windows.net “ is the storage account name, and "SCCM2012-2015-08-28.vhd" is the VHD name.</span></span>  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

### <a name="step-2-delete-the-vhd-by-using-azure-storage-explorer"></a><span data-ttu-id="54b41-133">步驟 2 使用 Azure 儲存體總管刪除 VHD</span><span class="sxs-lookup"><span data-stu-id="54b41-133">Step 2 Delete the VHD by using Azure Storage Explorer</span></span>

1. <span data-ttu-id="54b41-134">下載並安裝最新版 [Azure 儲存體總管](http://storageexplorer.com/)。</span><span class="sxs-lookup"><span data-stu-id="54b41-134">Download and Install the latest version of [Azure Storage Explorer](http://storageexplorer.com/).</span></span> <span data-ttu-id="54b41-135">此工具是免費的獨立應用程式，可讓您在 Windows、MacOS 和 Linux 上輕鬆處理 Azure 儲存體資料。</span><span class="sxs-lookup"><span data-stu-id="54b41-135">This tool is a standalone app from Microsoft that allows you to easily work with Azure Storage data on Windows, macOS and Linux.</span></span>
2. <span data-ttu-id="54b41-136">開啟 [Azure 儲存體總管]，選取</span><span class="sxs-lookup"><span data-stu-id="54b41-136">Open Azure Storage Explorer, select</span></span> ![帳戶圖示](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/account.png) <span data-ttu-id="54b41-138">在左列中，選取 Azure 環境中，然後登入。</span><span class="sxs-lookup"><span data-stu-id="54b41-138">on the left bar, select your Azure environment, and then sign in.</span></span>

3. <span data-ttu-id="54b41-139">選取所有訂用帳戶，或選取含有您想要刪除的儲存體帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="54b41-139">Select all subscriptions or the subscription that contains the storage account you want to delete.</span></span>

    ![新增訂用帳戶](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/addsub.png)

4. <span data-ttu-id="54b41-141">移至稍早從磁碟 URL 取得的儲存體帳戶，並選取 [Blob 容器] > [VHD]，然後搜尋導致無法刪除儲存體帳戶的 VHD。</span><span class="sxs-lookup"><span data-stu-id="54b41-141">Go to the storage account that we obtained from the disk URL earlier, select the **Blob Containers** > **vhds** and search for the VHD that prevents you delete the storage account.</span></span>
5. <span data-ttu-id="54b41-142">如果找到 VHD，請檢查 [VM 名稱] 資料行，找出使用此 VHD 的 VM。</span><span class="sxs-lookup"><span data-stu-id="54b41-142">If the VHD is found,  check the **VM Name** column to find the VM that is using this VHD.</span></span>

    ![檢查 VM](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/check-vm.png)

6. <span data-ttu-id="54b41-144">使用 Azure 入口網站從 VHD 移除租用。</span><span class="sxs-lookup"><span data-stu-id="54b41-144">Remove the lease from the VHD by using Azure portal.</span></span> <span data-ttu-id="54b41-145">如需詳細資訊，請參閱[從 VHD 移除租用](#remove-the-lease-from-the-vhd)。</span><span class="sxs-lookup"><span data-stu-id="54b41-145">For more information, see [Remove the lease from the VHD](#remove-the-lease-from-the-vhd).</span></span> 

7. <span data-ttu-id="54b41-146">移至 [Azure 儲存體總管]，以滑鼠右鍵按一下 VHD，然後選取 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="54b41-146">Go to the Azure Storage Explorer, right-click the VHD and then select delete.</span></span>

8. <span data-ttu-id="54b41-147">刪除儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="54b41-147">Delete the storage account.</span></span>

### <a name="method-2---use-azure-portal"></a><span data-ttu-id="54b41-148">方法 2 - 使用 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="54b41-148">Method 2 - Use Azure portal</span></span> 

#### <a name="step-1-identify-the-vhd-that-prevent-deletion-of-the-storage-account"></a><span data-ttu-id="54b41-149">步驟 1：識別導致無法刪除儲存體帳戶的 VHD</span><span class="sxs-lookup"><span data-stu-id="54b41-149">Step 1: Identify the VHD that prevent deletion of the storage account</span></span>

1. <span data-ttu-id="54b41-150">您刪除儲存體帳戶時，將收到以下訊息對話方塊：</span><span class="sxs-lookup"><span data-stu-id="54b41-150">When you delete the storage account, you will receive a message dialog such as the following:</span></span> 

    ![刪除儲存體帳戶時的訊息](././media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. <span data-ttu-id="54b41-152">檢查**磁碟 URL**，以找出導致無法刪除儲存體帳戶的儲存體帳戶和 VHD。</span><span class="sxs-lookup"><span data-stu-id="54b41-152">Check the **Disk URL** to identify the storage account and the VHD that prevents you delete the storage account.</span></span> <span data-ttu-id="54b41-153">在下列範例中，“.blob.core.windows.net “ 是儲存體帳戶名稱，"SCCM2012-2015-08-28.vhd" 是 VHD 名稱。</span><span class="sxs-lookup"><span data-stu-id="54b41-153">In the following example, the string before “.blob.core.windows.net “ is the storage account name, and "SCCM2012-2015-08-28.vhd" is the VHD name.</span></span>  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

2. <span data-ttu-id="54b41-154">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="54b41-154">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
3. <span data-ttu-id="54b41-155">在 [中樞] 功能表中，選取 [所有資源]。</span><span class="sxs-lookup"><span data-stu-id="54b41-155">On the Hub menu, select **All resources**.</span></span> <span data-ttu-id="54b41-156">移至儲存體帳戶，然後選取 [Blob] > [VHD]。</span><span class="sxs-lookup"><span data-stu-id="54b41-156">Go to the storage account, and then select **Blobs** > **vhds**.</span></span>

    ![入口網站的螢幕擷取畫面，醒目提示儲存體帳戶與「vhds」容器](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/opencontainer.png)

4. <span data-ttu-id="54b41-158">找出稍早從磁碟 URL 取得的 VHD。</span><span class="sxs-lookup"><span data-stu-id="54b41-158">Locate the VHD that we obtained from the disk URL earlier.</span></span> <span data-ttu-id="54b41-159">然後，判斷是哪個 VM 在使用 VHD。</span><span class="sxs-lookup"><span data-stu-id="54b41-159">Then, determine which VM is using the VHD.</span></span> <span data-ttu-id="54b41-160">通常來說，您可以藉由檢查 VHD 的名稱來判斷是哪個 VM 握有 VHD︰</span><span class="sxs-lookup"><span data-stu-id="54b41-160">Usually, you can determine which VM holds the VHD by checking name of the VHD:</span></span>

<span data-ttu-id="54b41-161">資源管理員開發模型中的 VM</span><span class="sxs-lookup"><span data-stu-id="54b41-161">VM in Resource Manager development  model</span></span>

   * <span data-ttu-id="54b41-162">作業系統磁碟一般會遵循此命名慣例︰VMName-YYYY-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="54b41-162">OS disks generally follow this naming convention: VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>
   * <span data-ttu-id="54b41-163">資料磁碟一般會遵循此命名慣例︰VMName-YYYY-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="54b41-163">Data disks generally follow this naming convention: VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>

<span data-ttu-id="54b41-164">傳統開發模型中的 VM</span><span class="sxs-lookup"><span data-stu-id="54b41-164">VM in Classic development model</span></span>

   * <span data-ttu-id="54b41-165">作業系統磁碟一般會遵循此命名慣例︰CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="54b41-165">OS disks generally follow this naming convention: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>
   * <span data-ttu-id="54b41-166">資料磁碟一般會遵循此命名慣例︰CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="54b41-166">Data disks generally follow this naming convention: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>

#### <a name="step-2-remove-the-lease-from-the-vhd"></a><span data-ttu-id="54b41-167">步驟 2︰從 VHD 移除租用</span><span class="sxs-lookup"><span data-stu-id="54b41-167">Step 2: Remove the lease from the VHD</span></span>

<span data-ttu-id="54b41-168">[從 VHD 移除租用](#remove-the-lease-from-the-vhd)，然後刪除儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="54b41-168">[Remove the lease from the VHD](#remove-the-lease-from-the-vhd), and then delete the storage account.</span></span>

## <a name="what-is-a-lease"></a><span data-ttu-id="54b41-169">租用是什麼？</span><span class="sxs-lookup"><span data-stu-id="54b41-169">What is a lease?</span></span>
<span data-ttu-id="54b41-170">租用是可用來控制 Blob (例如 VHD) 存取權的鎖定。</span><span class="sxs-lookup"><span data-stu-id="54b41-170">A lease is a lock that can be used to control access to a blob (for example, a VHD).</span></span> <span data-ttu-id="54b41-171">租用 Blob 時，只有租用的擁有者可以存取 Blob。</span><span class="sxs-lookup"><span data-stu-id="54b41-171">When a blob is leased, only the owners of the lease can access the blob.</span></span> <span data-ttu-id="54b41-172">租用非常重要，原因如下︰</span><span class="sxs-lookup"><span data-stu-id="54b41-172">A lease is important for the following reasons:</span></span>

* <span data-ttu-id="54b41-173">如果多名擁有者嘗試同時對 Blob 的相同部分寫入資料，租用可防止資料損毀。</span><span class="sxs-lookup"><span data-stu-id="54b41-173">It prevents data corruption if multiple owners try to write to the same portion of the blob at the same time.</span></span>
* <span data-ttu-id="54b41-174">租用可防止正在使用中的 Blob 遭到 (例如 VM) 刪除。</span><span class="sxs-lookup"><span data-stu-id="54b41-174">It prevents the blob from being deleted if something is actively using it (for example, a VM).</span></span>
* <span data-ttu-id="54b41-175">租用可防止正在使用中的儲存體帳戶遭到 (例如 VM) 刪除。</span><span class="sxs-lookup"><span data-stu-id="54b41-175">It prevents the storage account from being deleted if something is actively using it (for example, a VM).</span></span>

### <a name="remove-the-lease-from-the-vhd"></a><span data-ttu-id="54b41-176">從 VHD 移除租用</span><span class="sxs-lookup"><span data-stu-id="54b41-176">Remove the lease from the VHD</span></span>
<span data-ttu-id="54b41-177">如果 VHD 是作業系統磁碟，您必須刪除 VM 才能移除租用：</span><span class="sxs-lookup"><span data-stu-id="54b41-177">If the VHD is an OS disk, you must delete the VM to remove the lease:</span></span>

1. <span data-ttu-id="54b41-178">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="54b41-178">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="54b41-179">在 [中樞] 功能表上，選取 [虛擬機器]。</span><span class="sxs-lookup"><span data-stu-id="54b41-179">On the **Hub** menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="54b41-180">選取在 VHD 上握有租用的 VM。</span><span class="sxs-lookup"><span data-stu-id="54b41-180">Select the VM that holds a lease on the VHD.</span></span>
4. <span data-ttu-id="54b41-181">確定沒有正在使用虛擬機器的項目，而且您不再需要虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="54b41-181">Make sure that nothing is actively using the virtual machine, and that you no longer need the virtual machine.</span></span>
5. <span data-ttu-id="54b41-182">在 [VM 詳細資料] 刀鋒視窗頂端，選取 [刪除]，然後按一下 [是] 進行確認。</span><span class="sxs-lookup"><span data-stu-id="54b41-182">At the top of the **VM details** blade, select **Delete**, and then click **Yes** to confirm.</span></span>
6. <span data-ttu-id="54b41-183">VM 應該會遭到刪除，但 VHD 應該會保留下來。</span><span class="sxs-lookup"><span data-stu-id="54b41-183">The VM should be deleted, but the VHD can be retained.</span></span> <span data-ttu-id="54b41-184">不過，VHD 上應該不會再有租用。</span><span class="sxs-lookup"><span data-stu-id="54b41-184">However, the VHD should no longer have a lease on it.</span></span> <span data-ttu-id="54b41-185">釋放租用可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="54b41-185">It may take a few minutes for the lease to be released.</span></span> <span data-ttu-id="54b41-186">若要確認租用已遭到釋放，請移至 [所有資源] > [儲存體帳戶名稱] > [Blob] > [VHD]。</span><span class="sxs-lookup"><span data-stu-id="54b41-186">To verify that the lease is released, go to **All resources** > **Storage Account Name** > **Blobs** > **vhds**.</span></span> <span data-ttu-id="54b41-187">在 Blob 屬性 窗格中，租用狀態 值應該是 已解除鎖定。</span><span class="sxs-lookup"><span data-stu-id="54b41-187">In the **Blob properties** pane, the **Lease Status** value should be **Unlocked**.</span></span>

<span data-ttu-id="54b41-188">如果 VHD 是資料磁碟，請從 VM 中斷連結 VHD，以便移除租用：</span><span class="sxs-lookup"><span data-stu-id="54b41-188">If the VHD is a data disk, detach the VHD from the VM to remove the lease:</span></span>

1. <span data-ttu-id="54b41-189">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="54b41-189">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="54b41-190">在 [中樞] 功能表上，選取 [虛擬機器]。</span><span class="sxs-lookup"><span data-stu-id="54b41-190">On the **Hub** menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="54b41-191">選取在 VHD 上握有租用的 VM。</span><span class="sxs-lookup"><span data-stu-id="54b41-191">Select the VM that holds a lease on the VHD.</span></span>
4. <span data-ttu-id="54b41-192">選取 [VM 詳細資料] 刀鋒視窗上的 [磁碟]。</span><span class="sxs-lookup"><span data-stu-id="54b41-192">Select **Disks** on the **VM details** blade.</span></span>
5. <span data-ttu-id="54b41-193">選取在 VHD 上握有租用的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="54b41-193">Select the data disk that holds a lease on the VHD.</span></span> <span data-ttu-id="54b41-194">您可以藉由檢查 VHD 的 URL 來判斷磁碟中連接的 VHD。</span><span class="sxs-lookup"><span data-stu-id="54b41-194">You can determine which VHD is attached in the disk by checking the URL of the VHD.</span></span>
6. <span data-ttu-id="54b41-195">確實判斷沒有任何項目正在使用資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="54b41-195">Determine with certainty that nothing is actively using the data disk.</span></span>
7. <span data-ttu-id="54b41-196">按一下 [磁碟詳細資料] 刀鋒視窗上的 [中斷連結]。</span><span class="sxs-lookup"><span data-stu-id="54b41-196">Click **Detach** on the **Disk details** blade.</span></span>
8. <span data-ttu-id="54b41-197">磁碟應該會立即與 VM 中斷連結，而且 VHD 上應該不會再有租用。</span><span class="sxs-lookup"><span data-stu-id="54b41-197">The disk should now be detached from the VM, and the VHD should no longer have a lease on it.</span></span> <span data-ttu-id="54b41-198">釋放租用可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="54b41-198">It may take a few minutes for the lease to be released.</span></span> <span data-ttu-id="54b41-199">若要確認租用已遭到釋放，請移至 [所有資源] > [儲存體帳戶名稱] > [Blob] > [VHD]。</span><span class="sxs-lookup"><span data-stu-id="54b41-199">To verify that the lease has been released, go to **All resources** > **Storage Account Name** > **Blobs** > **vhds**.</span></span> <span data-ttu-id="54b41-200">在 Blob 屬性 窗格中，租用狀態 值應該是 已解除鎖定。</span><span class="sxs-lookup"><span data-stu-id="54b41-200">In the **Blob properties** pane, the **Lease Status** value should be **Unlocked**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="54b41-201">後續步驟</span><span class="sxs-lookup"><span data-stu-id="54b41-201">Next steps</span></span>
* [<span data-ttu-id="54b41-202">刪除儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="54b41-202">Delete a storage account</span></span>](storage-create-storage-account.md#delete-a-storage-account)
* [<span data-ttu-id="54b41-203">如何在 Microsoft Azure (PowerShell) 中止 blob 儲存體的鎖定租用</span><span class="sxs-lookup"><span data-stu-id="54b41-203">How to break the locked lease of blob storage in Microsoft Azure (PowerShell)</span></span>](https://gallery.technet.microsoft.com/scriptcenter/How-to-break-the-locked-c2cd6492)
