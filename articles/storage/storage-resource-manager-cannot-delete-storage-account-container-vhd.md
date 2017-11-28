---
title: "當您刪除 Azure 儲存體帳戶、 容器或 Vhd aaaTroubleshoot 錯誤 |Microsoft 文件"
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
ms.openlocfilehash: 77361593e2c924d39aba853e0807dc3188f50e60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-errors-when-you-delete-azure-storage-accounts-containers-or-vhds"></a><span data-ttu-id="a2197-103">針對刪除 Azure 儲存體帳戶、容器或 VHD 時所發生的錯誤進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="a2197-103">Troubleshoot errors when you delete Azure storage accounts, containers, or VHDs</span></span>

<span data-ttu-id="a2197-104">您可能會在 hello 中收到錯誤時的 Azure 儲存體帳戶、 容器或虛擬硬碟 (VHD)，請嘗試 toodelete [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="a2197-104">You might receive errors when you try toodelete an Azure storage account, container, or virtual hard disk (VHD) in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="a2197-105">本文章提供在 Azure Resource Manager 部署指南 toohelp 解析 hello 問題疑難排解。</span><span class="sxs-lookup"><span data-stu-id="a2197-105">This article provides troubleshooting guidance toohelp resolve hello problem in an Azure Resource Manager deployment.</span></span>

<span data-ttu-id="a2197-106">如果這份文件並不能解決您的 Azure 問題，請瀏覽 hello Azure 論壇上[MSDN 和堆疊溢位](https://azure.microsoft.com/support/forums/)。</span><span class="sxs-lookup"><span data-stu-id="a2197-106">If this article doesn't address your Azure problem, visit hello Azure forums on [MSDN and Stack Overflow](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="a2197-107">您可以在這些論壇張貼問題或too@AzureSupportTwitter 上。</span><span class="sxs-lookup"><span data-stu-id="a2197-107">You can post your problem on these forums or too@AzureSupport on Twitter.</span></span> <span data-ttu-id="a2197-108">此外，您可以藉由選取檔案 Azure 支援人員要求**取得支援**上 hello [Azure 支援](https://azure.microsoft.com/support/options/)站台。</span><span class="sxs-lookup"><span data-stu-id="a2197-108">Also, you can file an Azure support request by selecting **Get support** on hello [Azure support](https://azure.microsoft.com/support/options/) site.</span></span>

## <a name="symptoms"></a><span data-ttu-id="a2197-109">徵兆</span><span class="sxs-lookup"><span data-stu-id="a2197-109">Symptoms</span></span>
### <a name="scenario-1"></a><span data-ttu-id="a2197-110">案例 1</span><span class="sxs-lookup"><span data-stu-id="a2197-110">Scenario 1</span></span>
<span data-ttu-id="a2197-111">當您嘗試 toodelete 資源管理員部署的儲存體帳戶中的 VHD 時，您會收到下列錯誤訊息的 hello:</span><span class="sxs-lookup"><span data-stu-id="a2197-111">When you try toodelete a VHD in a storage account in a Resource Manager deployment, you receive hello following error message:</span></span>

<span data-ttu-id="a2197-112">**無法 toodelete blob 'vhds/BlobName.vhd'。錯誤： 目前沒有租用 hello blob 上和 hello 要求中指定任何租用識別碼。**</span><span class="sxs-lookup"><span data-stu-id="a2197-112">**Failed toodelete blob 'vhds/BlobName.vhd'. Error: There is currently a lease on hello blob and no lease ID was specified in hello request.**</span></span>

<span data-ttu-id="a2197-113">因為虛擬機器 (VM) 具有 hello 嘗試 toodelete VHD 上的租用，可能會發生此問題。</span><span class="sxs-lookup"><span data-stu-id="a2197-113">This problem can occur because a virtual machine (VM) has a lease on hello VHD that you are trying toodelete.</span></span>

### <a name="scenario-2"></a><span data-ttu-id="a2197-114">案例 2</span><span class="sxs-lookup"><span data-stu-id="a2197-114">Scenario 2</span></span>
<span data-ttu-id="a2197-115">當您嘗試 toodelete 資源管理員部署的儲存體帳戶中的容器時，您會收到下列錯誤訊息的 hello:</span><span class="sxs-lookup"><span data-stu-id="a2197-115">When you try toodelete a container in a storage account in a Resource Manager deployment, you receive hello following error message:</span></span>

<span data-ttu-id="a2197-116">**無法 toodelete 儲存體容器 'vhd'。錯誤： 目前沒有租用 hello 容器和 hello 要求中指定任何租用識別碼。**</span><span class="sxs-lookup"><span data-stu-id="a2197-116">**Failed toodelete storage container 'vhds'. Error: There is currently a lease on hello container and no lease ID was specified in hello request.**</span></span>

<span data-ttu-id="a2197-117">因為 hello 容器具有 hello 租用處於已鎖定的 VHD，可能會發生此問題。</span><span class="sxs-lookup"><span data-stu-id="a2197-117">This problem can occur because hello container has a VHD that is locked in hello lease state.</span></span>

### <a name="scenario-3"></a><span data-ttu-id="a2197-118">案例 3</span><span class="sxs-lookup"><span data-stu-id="a2197-118">Scenario 3</span></span>
<span data-ttu-id="a2197-119">當您嘗試 toodelete 資源管理員部署的儲存體帳戶時，您會收到下列錯誤訊息的 hello:</span><span class="sxs-lookup"><span data-stu-id="a2197-119">When you try toodelete a storage account in a Resource Manager deployment, you receive hello following error message:</span></span>

<span data-ttu-id="a2197-120">**無法 toodelete 儲存體帳戶 'StorageAccountName'。錯誤： 無法刪除 hello 儲存體帳戶，因為 tooits 成品正在使用中。**</span><span class="sxs-lookup"><span data-stu-id="a2197-120">**Failed toodelete storage account 'StorageAccountName'. Error: hello storage account cannot be deleted due tooits artifacts being in use.**</span></span>

<span data-ttu-id="a2197-121">因為 hello 儲存體帳戶包含在 hello 租用狀態的 VHD，可能會發生此問題。</span><span class="sxs-lookup"><span data-stu-id="a2197-121">This problem can occur because hello storage account contains a VHD that is in hello lease state.</span></span>

## <a name="solution"></a><span data-ttu-id="a2197-122">方案</span><span class="sxs-lookup"><span data-stu-id="a2197-122">Solution</span></span> 
<span data-ttu-id="a2197-123">tooresolve 這些問題，您必須識別 hello hello 錯誤造成的 VHD 和 hello 相關聯的 VM。</span><span class="sxs-lookup"><span data-stu-id="a2197-123">tooresolve these problems, you must identify hello VHD that is causing hello error and hello associated VM.</span></span> <span data-ttu-id="a2197-124">然後，卸離 hello VHD 從 hello VM （適用於資料磁碟），或刪除 hello 使用 hello VHD （適用於作業系統磁碟） 的 VM。</span><span class="sxs-lookup"><span data-stu-id="a2197-124">Then, detach hello VHD from hello VM (for data disks) or delete hello VM that is using hello VHD (for OS disks).</span></span> <span data-ttu-id="a2197-125">這會移除 hello 租用 hello VHD，並允許 toobe 刪除。</span><span class="sxs-lookup"><span data-stu-id="a2197-125">This removes hello lease from hello VHD and allows it toobe deleted.</span></span> 

<span data-ttu-id="a2197-126">toodo，使用其中一個 hello 下列方法：</span><span class="sxs-lookup"><span data-stu-id="a2197-126">toodo this, use one of hello following methods:</span></span>

### <a name="method-1---use-azure-storage-explorer"></a><span data-ttu-id="a2197-127">方法 1 - 使用 Azure 儲存體總管</span><span class="sxs-lookup"><span data-stu-id="a2197-127">Method 1 - Use Azure storage explorer</span></span>

### <a name="step-1-identify-hello-vhd-that-prevent-deletion-of-hello-storage-account"></a><span data-ttu-id="a2197-128">步驟 1 識別 hello 導致無法刪除 hello 儲存體帳戶的 VHD</span><span class="sxs-lookup"><span data-stu-id="a2197-128">Step 1 Identify hello VHD that prevent deletion of hello storage account</span></span>

1. <span data-ttu-id="a2197-129">當您刪除 hello 儲存體帳戶時，您會收到 hello 如下的訊息對話方塊：</span><span class="sxs-lookup"><span data-stu-id="a2197-129">When you delete hello storage account, you will receive a message dialog such as hello following:</span></span> 

    ![當刪除 hello 儲存體帳戶時，訊息](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. <span data-ttu-id="a2197-131">檢查 hello**磁碟 URL** tooidentify hello 儲存體帳戶和 hello VHD，讓您刪除 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a2197-131">Check hello **Disk URL** tooidentify hello storage account and hello VHD that prevents you delete hello storage account.</span></span> <span data-ttu-id="a2197-132">在下列範例的 hello，hello 之前字串 」。 account>.blob.core.windows.net"hello 儲存體帳戶名稱，而 「 SCCM2012-2015年-08-28.vhd"hello VHD 名稱。</span><span class="sxs-lookup"><span data-stu-id="a2197-132">In hello following example, hello string before “.blob.core.windows.net “ is hello storage account name, and "SCCM2012-2015-08-28.vhd" is hello VHD name.</span></span>  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

### <a name="step-2-delete-hello-vhd-by-using-azure-storage-explorer"></a><span data-ttu-id="a2197-133">使用 Azure 儲存體總管的步驟 2 Delete hello VHD</span><span class="sxs-lookup"><span data-stu-id="a2197-133">Step 2 Delete hello VHD by using Azure Storage Explorer</span></span>

1. <span data-ttu-id="a2197-134">下載並安裝 hello 最新版本[Azure 儲存體總管](http://storageexplorer.com/)。</span><span class="sxs-lookup"><span data-stu-id="a2197-134">Download and Install hello latest version of [Azure Storage Explorer](http://storageexplorer.com/).</span></span> <span data-ttu-id="a2197-135">此工具是 microsoft Windows、 macOS 和 Linux 的 Azure 儲存體資料 tooeasily 工作可讓您的獨立應用程式。</span><span class="sxs-lookup"><span data-stu-id="a2197-135">This tool is a standalone app from Microsoft that allows you tooeasily work with Azure Storage data on Windows, macOS and Linux.</span></span>
2. <span data-ttu-id="a2197-136">開啟 [Azure 儲存體總管]，選取</span><span class="sxs-lookup"><span data-stu-id="a2197-136">Open Azure Storage Explorer, select</span></span> ![帳戶圖示](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/account.png) <span data-ttu-id="a2197-138">hello 左在列上，選取您的 Azure 環境，然後再登入。</span><span class="sxs-lookup"><span data-stu-id="a2197-138">on hello left bar, select your Azure environment, and then sign in.</span></span>

3. <span data-ttu-id="a2197-139">選取所有的訂閱或 hello 訂用帳戶包含您想 toodelete hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a2197-139">Select all subscriptions or hello subscription that contains hello storage account you want toodelete.</span></span>

    ![新增訂用帳戶](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/addsub.png)

4. <span data-ttu-id="a2197-141">移 toohello 儲存體帳戶，我們取自 hello 磁碟 URL 之前，請選取 hello **Blob 容器** > **vhd**並刪除 hello 儲存體帳戶上搜尋 hello 會讓您的 VHD。</span><span class="sxs-lookup"><span data-stu-id="a2197-141">Go toohello storage account that we obtained from hello disk URL earlier, select hello **Blob Containers** > **vhds** and search for hello VHD that prevents you delete hello storage account.</span></span>
5. <span data-ttu-id="a2197-142">如果找到 hello VHD，請檢查 hello **VM 名稱**資料行 toofind hello 正在使用此 VHD 的 VM。</span><span class="sxs-lookup"><span data-stu-id="a2197-142">If hello VHD is found,  check hello **VM Name** column toofind hello VM that is using this VHD.</span></span>

    ![檢查 VM](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/check-vm.png)

6. <span data-ttu-id="a2197-144">使用 Azure 入口網站移除 hello VHD hello 租用。</span><span class="sxs-lookup"><span data-stu-id="a2197-144">Remove hello lease from hello VHD by using Azure portal.</span></span> <span data-ttu-id="a2197-145">如需詳細資訊，請參閱[移除 hello 租用 hello VHD 從](#remove-the-lease-from-the-vhd)。</span><span class="sxs-lookup"><span data-stu-id="a2197-145">For more information, see [Remove hello lease from hello VHD](#remove-the-lease-from-the-vhd).</span></span> 

7. <span data-ttu-id="a2197-146">移 toohello Azure 儲存體總管 hello VHD 上按一下滑鼠右鍵，然後選取 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="a2197-146">Go toohello Azure Storage Explorer, right-click hello VHD and then select delete.</span></span>

8. <span data-ttu-id="a2197-147">刪除 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a2197-147">Delete hello storage account.</span></span>

### <a name="method-2---use-azure-portal"></a><span data-ttu-id="a2197-148">方法 2 - 使用 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="a2197-148">Method 2 - Use Azure portal</span></span> 

#### <a name="step-1-identify-hello-vhd-that-prevent-deletion-of-hello-storage-account"></a><span data-ttu-id="a2197-149">步驟 1： 識別 hello 導致無法刪除 hello 儲存體帳戶的 VHD</span><span class="sxs-lookup"><span data-stu-id="a2197-149">Step 1: Identify hello VHD that prevent deletion of hello storage account</span></span>

1. <span data-ttu-id="a2197-150">當您刪除 hello 儲存體帳戶時，您會收到 hello 如下的訊息對話方塊：</span><span class="sxs-lookup"><span data-stu-id="a2197-150">When you delete hello storage account, you will receive a message dialog such as hello following:</span></span> 

    ![當刪除 hello 儲存體帳戶時，訊息](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. <span data-ttu-id="a2197-152">檢查 hello**磁碟 URL** tooidentify hello 儲存體帳戶和 hello VHD，讓您刪除 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a2197-152">Check hello **Disk URL** tooidentify hello storage account and hello VHD that prevents you delete hello storage account.</span></span> <span data-ttu-id="a2197-153">在下列範例的 hello，hello 之前字串 」。 account>.blob.core.windows.net"hello 儲存體帳戶名稱，而 「 SCCM2012-2015年-08-28.vhd"hello VHD 名稱。</span><span class="sxs-lookup"><span data-stu-id="a2197-153">In hello following example, hello string before “.blob.core.windows.net “ is hello storage account name, and "SCCM2012-2015-08-28.vhd" is hello VHD name.</span></span>  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

2. <span data-ttu-id="a2197-154">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="a2197-154">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
3. <span data-ttu-id="a2197-155">在 hello 中樞功能表中，選取 **所有資源**。</span><span class="sxs-lookup"><span data-stu-id="a2197-155">On hello Hub menu, select **All resources**.</span></span> <span data-ttu-id="a2197-156">移 toohello 儲存體帳戶，然後再選取**Blob** > **vhd**。</span><span class="sxs-lookup"><span data-stu-id="a2197-156">Go toohello storage account, and then select **Blobs** > **vhds**.</span></span>

    ![Hello 入口網站中，反白顯示 hello"vhds"容器與 hello 儲存體帳戶的螢幕擷取畫面](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/opencontainer.png)

4. <span data-ttu-id="a2197-158">找出 hello 我們稍早取得從 hello 磁碟 URL 的 VHD。</span><span class="sxs-lookup"><span data-stu-id="a2197-158">Locate hello VHD that we obtained from hello disk URL earlier.</span></span> <span data-ttu-id="a2197-159">然後，判斷哪些 VM 正在使用 hello VHD。</span><span class="sxs-lookup"><span data-stu-id="a2197-159">Then, determine which VM is using hello VHD.</span></span> <span data-ttu-id="a2197-160">通常，您可以判斷其 VM 保留 hello VHD 藉由檢查 hello VHD 的名稱：</span><span class="sxs-lookup"><span data-stu-id="a2197-160">Usually, you can determine which VM holds hello VHD by checking name of hello VHD:</span></span>

<span data-ttu-id="a2197-161">資源管理員開發模型中的 VM</span><span class="sxs-lookup"><span data-stu-id="a2197-161">VM in Resource Manager development  model</span></span>

   * <span data-ttu-id="a2197-162">作業系統磁碟一般會遵循此命名慣例︰VMName-YYYY-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="a2197-162">OS disks generally follow this naming convention: VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>
   * <span data-ttu-id="a2197-163">資料磁碟一般會遵循此命名慣例︰VMName-YYYY-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="a2197-163">Data disks generally follow this naming convention: VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>

<span data-ttu-id="a2197-164">傳統開發模型中的 VM</span><span class="sxs-lookup"><span data-stu-id="a2197-164">VM in Classic development model</span></span>

   * <span data-ttu-id="a2197-165">作業系統磁碟一般會遵循此命名慣例︰CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="a2197-165">OS disks generally follow this naming convention: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>
   * <span data-ttu-id="a2197-166">資料磁碟一般會遵循此命名慣例︰CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="a2197-166">Data disks generally follow this naming convention: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>

#### <a name="step-2-remove-hello-lease-from-hello-vhd"></a><span data-ttu-id="a2197-167">步驟 2: Hello 租用移除 hello VHD</span><span class="sxs-lookup"><span data-stu-id="a2197-167">Step 2: Remove hello lease from hello VHD</span></span>

<span data-ttu-id="a2197-168">[移除 hello VHD 中的 hello 租用](#remove-the-lease-from-the-vhd)，然後再刪除 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a2197-168">[Remove hello lease from hello VHD](#remove-the-lease-from-the-vhd), and then delete hello storage account.</span></span>

## <a name="what-is-a-lease"></a><span data-ttu-id="a2197-169">租用是什麼？</span><span class="sxs-lookup"><span data-stu-id="a2197-169">What is a lease?</span></span>
<span data-ttu-id="a2197-170">使用期是可以使用的 toocontrol 存取 tooa blob (例如 VHD) 的鎖定。</span><span class="sxs-lookup"><span data-stu-id="a2197-170">A lease is a lock that can be used toocontrol access tooa blob (for example, a VHD).</span></span> <span data-ttu-id="a2197-171">當 blob 租用時，只有 hello 租用的 hello 擁有者可以存取 hello blob。</span><span class="sxs-lookup"><span data-stu-id="a2197-171">When a blob is leased, only hello owners of hello lease can access hello blob.</span></span> <span data-ttu-id="a2197-172">使用期是很重要的 hello 下列原因：</span><span class="sxs-lookup"><span data-stu-id="a2197-172">A lease is important for hello following reasons:</span></span>

* <span data-ttu-id="a2197-173">它可防止資料損毀，如果多個擁有者嘗試 toowrite toohello hello blob hello 相同部分相同的時間。</span><span class="sxs-lookup"><span data-stu-id="a2197-173">It prevents data corruption if multiple owners try toowrite toohello same portion of hello blob at hello same time.</span></span>
* <span data-ttu-id="a2197-174">它會防止 hello blob 遭到刪除的項目正在使用它 (例如 VM)。</span><span class="sxs-lookup"><span data-stu-id="a2197-174">It prevents hello blob from being deleted if something is actively using it (for example, a VM).</span></span>
* <span data-ttu-id="a2197-175">它可以防止 hello 儲存體帳戶刪除如果項目正在使用它 (例如 VM)。</span><span class="sxs-lookup"><span data-stu-id="a2197-175">It prevents hello storage account from being deleted if something is actively using it (for example, a VM).</span></span>

### <a name="remove-hello-lease-from-hello-vhd"></a><span data-ttu-id="a2197-176">Hello 租用移除 hello VHD</span><span class="sxs-lookup"><span data-stu-id="a2197-176">Remove hello lease from hello VHD</span></span>
<span data-ttu-id="a2197-177">如果作業系統磁碟 hello VHD，您必須刪除 hello VM tooremove hello 租用：</span><span class="sxs-lookup"><span data-stu-id="a2197-177">If hello VHD is an OS disk, you must delete hello VM tooremove hello lease:</span></span>

1. <span data-ttu-id="a2197-178">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="a2197-178">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a2197-179">在 hello**中樞**功能表上，選取**虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="a2197-179">On hello **Hub** menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="a2197-180">選取 hello 保存租用 hello VHD 的 VM。</span><span class="sxs-lookup"><span data-stu-id="a2197-180">Select hello VM that holds a lease on hello VHD.</span></span>
4. <span data-ttu-id="a2197-181">請確定不會主動使用 hello 虛擬機器，並確認您不再需要 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a2197-181">Make sure that nothing is actively using hello virtual machine, and that you no longer need hello virtual machine.</span></span>
5. <span data-ttu-id="a2197-182">頂端的 hello hello **VM 詳細資料**刀鋒視窗中，選取**刪除**，然後按一下**是**tooconfirm。</span><span class="sxs-lookup"><span data-stu-id="a2197-182">At hello top of hello **VM details** blade, select **Delete**, and then click **Yes** tooconfirm.</span></span>
6. <span data-ttu-id="a2197-183">應刪除 hello VM，但可以保留 hello VHD。</span><span class="sxs-lookup"><span data-stu-id="a2197-183">hello VM should be deleted, but hello VHD can be retained.</span></span> <span data-ttu-id="a2197-184">不過，hello VHD 應該不會再有租用。</span><span class="sxs-lookup"><span data-stu-id="a2197-184">However, hello VHD should no longer have a lease on it.</span></span> <span data-ttu-id="a2197-185">可能需要幾分鐘，讓 hello 租用 toobe 釋出。</span><span class="sxs-lookup"><span data-stu-id="a2197-185">It may take a few minutes for hello lease toobe released.</span></span> <span data-ttu-id="a2197-186">hello 租用的 tooverify 已發行，請跳過**所有資源** > **儲存體帳戶名稱** > **Blob**  >  **vhd**。</span><span class="sxs-lookup"><span data-stu-id="a2197-186">tooverify that hello lease is released, go too**All resources** > **Storage Account Name** > **Blobs** > **vhds**.</span></span> <span data-ttu-id="a2197-187">在 hello **Blob 屬性**窗格中，hello**租用狀態**值應該是**已解除鎖定**。</span><span class="sxs-lookup"><span data-stu-id="a2197-187">In hello **Blob properties** pane, hello **Lease Status** value should be **Unlocked**.</span></span>

<span data-ttu-id="a2197-188">如果 hello VHD 資料磁碟，卸離 hello VHD 從 hello VM tooremove hello 租用：</span><span class="sxs-lookup"><span data-stu-id="a2197-188">If hello VHD is a data disk, detach hello VHD from hello VM tooremove hello lease:</span></span>

1. <span data-ttu-id="a2197-189">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="a2197-189">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a2197-190">在 hello**中樞**功能表上，選取**虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="a2197-190">On hello **Hub** menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="a2197-191">選取 hello 保存租用 hello VHD 的 VM。</span><span class="sxs-lookup"><span data-stu-id="a2197-191">Select hello VM that holds a lease on hello VHD.</span></span>
4. <span data-ttu-id="a2197-192">選取**磁碟**上 hello **VM 詳細資料**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="a2197-192">Select **Disks** on hello **VM details** blade.</span></span>
5. <span data-ttu-id="a2197-193">選取對 hello VHD 保持租用的 hello 資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="a2197-193">Select hello data disk that holds a lease on hello VHD.</span></span> <span data-ttu-id="a2197-194">您可以判斷哪些 VHD 附加在 hello 磁碟，藉由檢查 hello hello VHD URL。</span><span class="sxs-lookup"><span data-stu-id="a2197-194">You can determine which VHD is attached in hello disk by checking hello URL of hello VHD.</span></span>
6. <span data-ttu-id="a2197-195">判斷確實不主動使用 hello 資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="a2197-195">Determine with certainty that nothing is actively using hello data disk.</span></span>
7. <span data-ttu-id="a2197-196">按一下**卸離**上 hello**磁碟詳細資料**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="a2197-196">Click **Detach** on hello **Disk details** blade.</span></span>
8. <span data-ttu-id="a2197-197">hello 磁碟現在會中斷 hello VM，並 hello VHD 應該不再需要在其上的租用。</span><span class="sxs-lookup"><span data-stu-id="a2197-197">hello disk should now be detached from hello VM, and hello VHD should no longer have a lease on it.</span></span> <span data-ttu-id="a2197-198">可能需要幾分鐘，讓 hello 租用 toobe 釋出。</span><span class="sxs-lookup"><span data-stu-id="a2197-198">It may take a few minutes for hello lease toobe released.</span></span> <span data-ttu-id="a2197-199">已釋放 hello 租用的 tooverify、 跳過**所有資源** > **儲存體帳戶名稱** > **Blob**  >  **vhd**。</span><span class="sxs-lookup"><span data-stu-id="a2197-199">tooverify that hello lease has been released, go too**All resources** > **Storage Account Name** > **Blobs** > **vhds**.</span></span> <span data-ttu-id="a2197-200">在 hello **Blob 屬性**窗格中，hello**租用狀態**值應該是**已解除鎖定**。</span><span class="sxs-lookup"><span data-stu-id="a2197-200">In hello **Blob properties** pane, hello **Lease Status** value should be **Unlocked**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2197-201">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a2197-201">Next steps</span></span>
* [<span data-ttu-id="a2197-202">刪除儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="a2197-202">Delete a storage account</span></span>](storage-create-storage-account.md#delete-a-storage-account)
* [<span data-ttu-id="a2197-203">如何 toobreak hello 鎖定租用的 blob 儲存體在 Microsoft Azure (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="a2197-203">How toobreak hello locked lease of blob storage in Microsoft Azure (PowerShell)</span></span>](https://gallery.technet.microsoft.com/scriptcenter/How-to-break-the-locked-c2cd6492)
