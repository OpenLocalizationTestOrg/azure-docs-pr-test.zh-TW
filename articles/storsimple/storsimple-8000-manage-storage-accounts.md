---
title: "管理 Microsoft Azure StorSimple 8000 系列裝置的 StorSimple 儲存體帳戶認證 | Microsoft Docs"
description: "說明如何使用 StorSimple 裝置管理員的 [設定] 頁面來新增、編輯、刪除或替換儲存體帳戶的安全性金鑰。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: 36058ad69ea670998b50cf9038741c294a5b79ab
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-storsimple-device-manager-service-to-manage-your-storage-account-credentials"></a><span data-ttu-id="d706d-103">使用 StorSimple 裝置管理員服務來管理儲存體帳戶認證</span><span class="sxs-lookup"><span data-stu-id="d706d-103">Use the StorSimple Device Manager service to manage your storage account credentials</span></span>

## <a name="overview"></a><span data-ttu-id="d706d-104">概觀</span><span class="sxs-lookup"><span data-stu-id="d706d-104">Overview</span></span>

<span data-ttu-id="d706d-105">StorSimple 裝置管理員服務的刀鋒視窗中，[設定] 區段會顯示所有可在 StorSimple 裝置管理員服務中建立的全域服務參數。</span><span class="sxs-lookup"><span data-stu-id="d706d-105">The **Configuration** section in the StorSimple Device Manager service blade presents all the global service parameters that can be created in the StorSimple Device Manager service.</span></span> <span data-ttu-id="d706d-106">這些參數可以套用到與該服務連線的所有裝置，還包括：</span><span class="sxs-lookup"><span data-stu-id="d706d-106">These parameters can be applied to all the devices connected to the service, and include:</span></span>

* <span data-ttu-id="d706d-107">儲存體帳戶認證</span><span class="sxs-lookup"><span data-stu-id="d706d-107">Storage account credentials</span></span>
* <span data-ttu-id="d706d-108">頻寬範本</span><span class="sxs-lookup"><span data-stu-id="d706d-108">Bandwidth templates</span></span> 
* <span data-ttu-id="d706d-109">存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="d706d-109">Access control records</span></span> 

<span data-ttu-id="d706d-110">本教學課程說明如何新增、編輯或刪除儲存體帳戶認證，或替換儲存體帳戶的安全性金鑰。</span><span class="sxs-lookup"><span data-stu-id="d706d-110">This tutorial explains how to add, edit, or delete storage account credentials, or rotate the security keys for a storage account.</span></span>

 ![儲存體帳戶認證的清單](./media/storsimple-8000-manage-storage-accounts/createnewstorageacct6.png)  

<span data-ttu-id="d706d-112">儲存體帳戶包含的認證可供 StorSimple 裝置用來存取雲端服務提供者的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d706d-112">Storage accounts contain the credentials that the StorSimple device uses to access your storage account with your cloud service provider.</span></span> <span data-ttu-id="d706d-113">對於 Microsoft Azure 儲存體帳戶，像是帳戶名稱與主要存取金鑰就屬於這些認證。</span><span class="sxs-lookup"><span data-stu-id="d706d-113">For Microsoft Azure storage accounts, these are credentials such as the account name and the primary access key.</span></span> 

<span data-ttu-id="d706d-114">在 [儲存體帳戶認證] 刀鋒視窗上，為訂用帳戶計費而建立的所有儲存體帳戶都會以表格顯示，其中包含下列資訊：</span><span class="sxs-lookup"><span data-stu-id="d706d-114">On the **Storage account credentials** blade, all storage accounts that are created for the billing subscription are displayed in a tabular format containing the following information:</span></span>

* <span data-ttu-id="d706d-115">**名稱** – 帳戶建立時獲指派的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="d706d-115">**Name** – The unique name assigned to the account when it was created.</span></span>
* <span data-ttu-id="d706d-116">**啟用 SSL** – 是否已啟用 SSL 並透過安全通道進行裝置對雲端的通訊。</span><span class="sxs-lookup"><span data-stu-id="d706d-116">**SSL enabled** – Whether the SSL is enabled and device-to-cloud communication is over the secure channel.</span></span>
* <span data-ttu-id="d706d-117">**使用者** – 使用該儲存體帳戶的的磁碟區數目。</span><span class="sxs-lookup"><span data-stu-id="d706d-117">**Used by** – The number of volumes using the storage account.</span></span>

<span data-ttu-id="d706d-118">與儲存體帳戶相關可執行的最常見工作如下：</span><span class="sxs-lookup"><span data-stu-id="d706d-118">The most common tasks related to storage accounts that can be performed are:</span></span>

* <span data-ttu-id="d706d-119">新增儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="d706d-119">Add a storage account</span></span> 
* <span data-ttu-id="d706d-120">編輯儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="d706d-120">Edit a storage account</span></span> 
* <span data-ttu-id="d706d-121">刪除儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="d706d-121">Delete a storage account</span></span> 
* <span data-ttu-id="d706d-122">替換儲存體帳戶的金鑰</span><span class="sxs-lookup"><span data-stu-id="d706d-122">Key rotation of storage accounts</span></span> 

## <a name="types-of-storage-accounts"></a><span data-ttu-id="d706d-123">儲存體帳戶類型</span><span class="sxs-lookup"><span data-stu-id="d706d-123">Types of storage accounts</span></span>

<span data-ttu-id="d706d-124">有三種儲存體帳戶類型能與 StorSimple 裝置搭配使用。</span><span class="sxs-lookup"><span data-stu-id="d706d-124">There are three types of storage accounts that can be used with your StorSimple device.</span></span>

* <span data-ttu-id="d706d-125">**自動產生的儲存體帳戶** – 正如其名，這類型的儲存體帳戶是在初次建立服務時自動產生。</span><span class="sxs-lookup"><span data-stu-id="d706d-125">**Auto-generated storage accounts** – As the name suggests, this type of storage account is automatically generated when the service is first created.</span></span> <span data-ttu-id="d706d-126">若要深入了解如何建立此儲存體帳戶，請參閱[部署您的內部部署 StorSimple 裝置](storsimple-8000-deployment-walkthrough-u2.md)中的[步驟 1：建立新的服務](storsimple-8000-deployment-walkthrough-u2.md#step-1-create-a-new-service)。</span><span class="sxs-lookup"><span data-stu-id="d706d-126">To learn more about how this storage account is created, see [Step 1: Create a new service](storsimple-8000-deployment-walkthrough-u2.md#step-1-create-a-new-service) in [Deploy your on-premises StorSimple device](storsimple-8000-deployment-walkthrough-u2.md).</span></span> 
* <span data-ttu-id="d706d-127">**服務訂用帳戶中的儲存體帳戶** – 這些是與相同服務訂用帳戶相關聯的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d706d-127">**Storage accounts in the service subscription** – These are the Azure storage accounts that are associated with the same subscription as that of the service.</span></span> <span data-ttu-id="d706d-128">若要深入了解如何建立這些儲存體帳戶，請參閱 [關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="d706d-128">To learn more about how these storage accounts are created, see [About Azure Storage Accounts](../storage/common/storage-create-storage-account.md).</span></span> 
* <span data-ttu-id="d706d-129">**服務訂用帳戶外的儲存體帳戶** – 這些是與服務毫無關聯的 Azure 儲存體帳戶，而且可能在服務建立之前便已存在 。</span><span class="sxs-lookup"><span data-stu-id="d706d-129">**Storage accounts outside of the service subscription** – These are the Azure storage accounts that are not associated with your service and likely existed before the service was created.</span></span>

## <a name="add-a-storage-account"></a><span data-ttu-id="d706d-130">新增儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="d706d-130">Add a storage account</span></span>

<span data-ttu-id="d706d-131">您可以提供唯一的易記名稱以及與儲存體帳戶(搭配指定的雲端服務提供者) 連結的存取認證來新增儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d706d-131">You can add a storage account by providing a unique friendly name and access credentials that are linked to the storage account (with the specified cloud service provider).</span></span> <span data-ttu-id="d706d-132">您也能選擇啟用安全通訊端層 (SSL) 模式，建立裝置與雲端之間網路通訊的安全通道。</span><span class="sxs-lookup"><span data-stu-id="d706d-132">You also have the option of enabling the secure sockets layer (SSL) mode to create a secure channel for network communication between your device and the cloud.</span></span>

<span data-ttu-id="d706d-133">您可以為指定的雲端服務提供者建立多個帳戶。</span><span class="sxs-lookup"><span data-stu-id="d706d-133">You can create multiple accounts for a given cloud service provider.</span></span> <span data-ttu-id="d706d-134">不過，請注意，建立儲存體帳戶之後，您無法變更雲端服務提供者。</span><span class="sxs-lookup"><span data-stu-id="d706d-134">Be aware, however, that after a storage account is created, you cannot change the cloud service provider.</span></span>

<span data-ttu-id="d706d-135">儲存體帳戶在儲存時，服務會嘗試與您的雲端服務提供者通訊。</span><span class="sxs-lookup"><span data-stu-id="d706d-135">While the storage account is being saved, the service attempts to communicate with your cloud service provider.</span></span> <span data-ttu-id="d706d-136">此時會驗證您提供的認證與存取資料。</span><span class="sxs-lookup"><span data-stu-id="d706d-136">The credentials and the access material that you supplied will be authenticated at this time.</span></span> <span data-ttu-id="d706d-137">只有當驗證成功時，才會建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d706d-137">A storage account is created only if the authentication succeeds.</span></span> <span data-ttu-id="d706d-138">如果驗證失敗，則會顯示適當的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="d706d-138">If the authentication fails, then an appropriate error message will be displayed.</span></span>

<span data-ttu-id="d706d-139">使用下列程序來新增 Azure 儲存體帳戶認證︰</span><span class="sxs-lookup"><span data-stu-id="d706d-139">Use the following procedures to add Azure storage account credentials:</span></span>

* <span data-ttu-id="d706d-140">若要新增儲存體帳戶認證，而且其 Azure 訂用帳戶與裝置管理員服務相同</span><span class="sxs-lookup"><span data-stu-id="d706d-140">To add a storage account credential that has the same Azure subscription as the Device Manager service</span></span>
* <span data-ttu-id="d706d-141">若要新增裝置管理員服務訂用帳戶外的 Azure 儲存體帳戶認證</span><span class="sxs-lookup"><span data-stu-id="d706d-141">To add an Azure storage account credential that is outside of the Device Manager service subscription</span></span>

[!INCLUDE [add-a-storage-account-update2](../../includes/storsimple-8000-configure-new-storage-account-u2.md)]

#### <a name="to-add-an-azure-storage-account-credential-outside-of-the-storsimple-device-manager-service-subscription"></a><span data-ttu-id="d706d-142">若要新增 StorSimple 裝置管理員服務訂用帳戶外的 Azure 儲存體帳戶認證</span><span class="sxs-lookup"><span data-stu-id="d706d-142">To add an Azure storage account credential outside of the StorSimple Device Manager service subscription</span></span>

1. <span data-ttu-id="d706d-143">請瀏覽至您的 StorSimple 裝置管理員服務，選取它並按兩下。</span><span class="sxs-lookup"><span data-stu-id="d706d-143">Navigate to your StorSimple Device Manager service, select and double-click it.</span></span> <span data-ttu-id="d706d-144">這會開啟 [概觀] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d706d-144">This opens the **Overview** blade.</span></span>
2. <span data-ttu-id="d706d-145">在 [設定] 區段內選取 [儲存體帳戶認證]。</span><span class="sxs-lookup"><span data-stu-id="d706d-145">Select **Storage account credentials** within the **Configuration** section.</span></span> <span data-ttu-id="d706d-146">這樣會列出與 StorSimple 裝置管理員服務相關聯的任何現有儲存體帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="d706d-146">This lists any existing storage account credentials associated with the StorSimple Device Manager service.</span></span>
3. <span data-ttu-id="d706d-147">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="d706d-147">Click **Add**.</span></span>
4. <span data-ttu-id="d706d-148">在 [新增儲存體帳戶認證] 刀鋒視窗中，執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="d706d-148">In the **Add a storage account credential** blade, do the following:</span></span>
   
    1. <span data-ttu-id="d706d-149">在 [訂用帳戶] 中，選取 [其他]。</span><span class="sxs-lookup"><span data-stu-id="d706d-149">For **Subscription**, select **Other**.</span></span>
   
    2. <span data-ttu-id="d706d-150">提供 Azure 儲存體帳戶認證的名稱。</span><span class="sxs-lookup"><span data-stu-id="d706d-150">Provide the name of your Azure storage account credential.</span></span>
   
    3. <span data-ttu-id="d706d-151">在 [儲存體帳戶存取金鑰]文字方塊中，提供 Azure 儲存體帳戶認證的主要「存取金鑰」。</span><span class="sxs-lookup"><span data-stu-id="d706d-151">In the **Storage account access key** text box, supply the primary Access Key for your Azure storage account credential.</span></span> <span data-ttu-id="d706d-152">若要取得此金鑰，請移至 Azure 儲存體服務，選取您的儲存體帳戶認證，然後按一下 [管理帳戶金鑰]。</span><span class="sxs-lookup"><span data-stu-id="d706d-152">To get this key, go to the Azure Storage service, select your storage account credential, and click **Manage account keys**.</span></span> <span data-ttu-id="d706d-153">現在，您可以複製主要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="d706d-153">You can now copy the primary access key.</span></span>
   
    4. <span data-ttu-id="d706d-154">若要啟用 SSL，請按一下 [啟用] 按鈕，為 StorSimple 裝置管理員服務與雲端之間的網路通訊建立安全通道。</span><span class="sxs-lookup"><span data-stu-id="d706d-154">To enable SSL, click the **Enable** button to create a secure channel for network communication between your StorSimple Device Manager service and the cloud.</span></span> <span data-ttu-id="d706d-155">只有當您在私人雲端內操作時，才按一下 [停用] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d706d-155">Click the **Disable** button only if you are operating within a private cloud.</span></span>
   
    5. <span data-ttu-id="d706d-156">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="d706d-156">Click **Add**.</span></span> <span data-ttu-id="d706d-157">成功建立儲存體帳戶認證之後會通知您。</span><span class="sxs-lookup"><span data-stu-id="d706d-157">You are notified after the storage account credential is successfully created.</span></span>

5. <span data-ttu-id="d706d-158">新建立的儲存體帳戶認證會顯示在 [StorSimple 設定裝置管理員服務] 刀鋒視窗的 [儲存體帳戶認證] 下方。</span><span class="sxs-lookup"><span data-stu-id="d706d-158">The newly created storage account credential is displayed on the StorSimple Configure Device Manager service blade under **Storage account credentials**.</span></span>
   


## <a name="edit-a-storage-account"></a><span data-ttu-id="d706d-159">編輯儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="d706d-159">Edit a storage account</span></span>

<span data-ttu-id="d706d-160">您可以編輯磁碟區容器所使用的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d706d-160">You can edit a storage account that is used by a volume container.</span></span> <span data-ttu-id="d706d-161">如果您編輯的儲存體帳戶目前正在使用中，唯一可修改的欄位就是儲存體帳戶的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="d706d-161">If you edit a storage account that is currently in use, the only field available to modify is the access key for the storage account.</span></span> <span data-ttu-id="d706d-162">您可以提供新的儲存體存取金鑰，並儲存更新的設定。</span><span class="sxs-lookup"><span data-stu-id="d706d-162">You can supply the new storage access key and save the updated settings.</span></span>

#### <a name="to-edit-a-storage-account"></a><span data-ttu-id="d706d-163">若要編輯儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="d706d-163">To edit a storage account</span></span>

1. <span data-ttu-id="d706d-164">移至您的 StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="d706d-164">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="d706d-165">在 [設定] 區段中，按一下 [儲存體帳戶認證]。</span><span class="sxs-lookup"><span data-stu-id="d706d-165">In the **Configuration** section, click **Storage account credentials**.</span></span>

    ![儲存體帳戶認證](./media/storsimple-8000-manage-storage-accounts/editstorageacct1.png)

2. <span data-ttu-id="d706d-167">在 [儲存體帳戶認證] 刀鋒視窗中，從儲存體帳戶認證清單中，選取並按一下您要編輯的項目。</span><span class="sxs-lookup"><span data-stu-id="d706d-167">In the **Storage account credentials** blade, from the list of storage account credentials, select and click the one you wish to edit.</span></span> 

3. <span data-ttu-id="d706d-168">您可以修改 [啟用 SSL] 選項。</span><span class="sxs-lookup"><span data-stu-id="d706d-168">You can modify the **Enable SSL** selection.</span></span> <span data-ttu-id="d706d-169">您也可以按一下 [更多]，然後選取 [同步存取金鑰] 以替換您的儲存體帳戶存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="d706d-169">You can also click **More...** and then select **Sync access key to rotate** your storage account access keys.</span></span> <span data-ttu-id="d706d-170">如需如何執行金鑰替換的詳細資訊，請參閱[儲存體帳戶的金鑰替換](#key-rotation-of-storage-accounts)。</span><span class="sxs-lookup"><span data-stu-id="d706d-170">Go to [Key rotation of storage accounts](#key-rotation-of-storage-accounts) for more information on how to perform key rotation.</span></span> <span data-ttu-id="d706d-171">修改設定之後，按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="d706d-171">After you have modified the settings, click **Save**.</span></span> 

    ![儲存編輯好的儲存體帳戶認證](./media/storsimple-8000-manage-storage-accounts/editstorageacct3.png)

4. <span data-ttu-id="d706d-173">系統提示您進行確認時，按一下 [是] 。</span><span class="sxs-lookup"><span data-stu-id="d706d-173">When prompted for confirmation, click **Yes**.</span></span> 

    ![確認修改](./media/storsimple-8000-manage-storage-accounts/editstorageacct4.png)

<span data-ttu-id="d706d-175">儲存體帳戶的設定將會更新並儲存。</span><span class="sxs-lookup"><span data-stu-id="d706d-175">The settings will be updated and saved for your storage account.</span></span> 

## <a name="delete-a-storage-account"></a><span data-ttu-id="d706d-176">刪除儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="d706d-176">Delete a storage account</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d706d-177">只有在其未由磁碟區容器使用時，您才可以刪除儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d706d-177">You can delete a storage account only if it is not used by a volume container.</span></span> <span data-ttu-id="d706d-178">如果磁碟區容器正在使用儲存體帳戶，請先刪除磁碟區容器，然後再刪除相關聯的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d706d-178">If a storage account is being used by a volume container, first delete the volume container and then delete the associated storage account.</span></span>

#### <a name="to-delete-a-storage-account"></a><span data-ttu-id="d706d-179">若要刪除儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="d706d-179">To delete a storage account</span></span>

1. <span data-ttu-id="d706d-180">移至您的 StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="d706d-180">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="d706d-181">在 [設定] 區段中，按一下 [儲存體帳戶認證]。</span><span class="sxs-lookup"><span data-stu-id="d706d-181">In the **Configuration** section, click **Storage account credentials**.</span></span>

2. <span data-ttu-id="d706d-182">在儲存體帳戶的表格式清單中，將滑鼠停留在您想要刪除的帳戶上方。</span><span class="sxs-lookup"><span data-stu-id="d706d-182">In the tabular list of storage accounts, hover over the account that you wish to delete.</span></span> <span data-ttu-id="d706d-183">以滑鼠右鍵按一下以叫用操作功能表，然後按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="d706d-183">Right-click to invoke the context menu and click **Delete**.</span></span>

    ![刪除儲存體帳戶認證](./media/storsimple-8000-manage-storage-accounts/deletestorageacct1.png)

3. <span data-ttu-id="d706d-185">當系統提示您確認時，按一下 [是]  繼續進行刪除。</span><span class="sxs-lookup"><span data-stu-id="d706d-185">When prompted for confirmation, click **Yes** to continue with the deletion.</span></span> <span data-ttu-id="d706d-186">表格式清單會更新以反映所做的變更。</span><span class="sxs-lookup"><span data-stu-id="d706d-186">The tabular listing will be updated to reflect the changes.</span></span>

    ![Confirm delete](./media/storsimple-8000-manage-storage-accounts/deletestorageacct2.png)

## <a name="key-rotation-of-storage-accounts"></a><span data-ttu-id="d706d-188">替換儲存體帳戶的金鑰</span><span class="sxs-lookup"><span data-stu-id="d706d-188">Key rotation of storage accounts</span></span>

<span data-ttu-id="d706d-189">基於安全性理由，通常是在資料中心內才需要替換金鑰。</span><span class="sxs-lookup"><span data-stu-id="d706d-189">For security reasons, key rotation is often a requirement in data centers.</span></span> <span data-ttu-id="d706d-190">每個 Microsoft Azure 訂用帳戶可以有一或多個相關聯的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d706d-190">Each Microsoft Azure subscription can have one or more associated storage accounts.</span></span> <span data-ttu-id="d706d-191">訂用帳戶與每個儲存體帳戶的存取金鑰可以控制這些帳戶的存取權。</span><span class="sxs-lookup"><span data-stu-id="d706d-191">The access to these accounts is controlled by the subscription and access keys for each storage account.</span></span> 

<span data-ttu-id="d706d-192">當您建立儲存體帳戶時，Azure 會產生兩個 512 位元的儲存體存取金鑰，可在存取儲存體帳戶時用於驗證。</span><span class="sxs-lookup"><span data-stu-id="d706d-192">When you create a storage account, Microsoft Azure generates two 512-bit storage access keys that are used for authentication when the storage account is accessed.</span></span> <span data-ttu-id="d706d-193">有這兩個儲存體存取金鑰，您不需要中斷儲存體服務或對該服務的存取，就能重新產生金鑰。</span><span class="sxs-lookup"><span data-stu-id="d706d-193">Having two storage access keys allows you to regenerate the keys with no interruption to your storage service or access to that service.</span></span> <span data-ttu-id="d706d-194">目前使用中的金鑰是「主要」金鑰，而備份金鑰則稱為「次要」金鑰。</span><span class="sxs-lookup"><span data-stu-id="d706d-194">The key that is currently in use is the *primary* key and the backup key is referred to as the *secondary* key.</span></span> <span data-ttu-id="d706d-195">當 Microsoft Azure StorSimple 裝置存取您的雲端儲存體服務提供者時必須提供這些兩個機碼之一。</span><span class="sxs-lookup"><span data-stu-id="d706d-195">One of these two keys must be supplied when your Microsoft Azure StorSimple device accesses your cloud storage service provider.</span></span>

## <a name="what-is-key-rotation"></a><span data-ttu-id="d706d-196">什麼是替換金鑰？</span><span class="sxs-lookup"><span data-stu-id="d706d-196">What is key rotation?</span></span>

<span data-ttu-id="d706d-197">一般而言，應用程式只使用其中一個金鑰來存取您的資料。</span><span class="sxs-lookup"><span data-stu-id="d706d-197">Typically, applications use only one of the keys to access your data.</span></span> <span data-ttu-id="d706d-198">經過一段時間之後，您可以讓應用程式切換為使用第二個金鑰。</span><span class="sxs-lookup"><span data-stu-id="d706d-198">After a certain period of time, you can have your applications switch over to using the second key.</span></span> <span data-ttu-id="d706d-199">在您將應用程式切換至次要金鑰之後，可以淘汰第一個金鑰，然後產生新的金鑰。</span><span class="sxs-lookup"><span data-stu-id="d706d-199">After you have switched your applications to the secondary key, you can retire the first key and then generate a new key.</span></span> <span data-ttu-id="d706d-200">這種使用兩個金鑰的方式可讓您的應用程式存取資料，卻不會產生任何停機時間。</span><span class="sxs-lookup"><span data-stu-id="d706d-200">Using the two keys this way allows your applications access to the data without incurring any downtime.</span></span>

<span data-ttu-id="d706d-201">儲存體帳戶金鑰一律以加密的格式儲存在服務中。</span><span class="sxs-lookup"><span data-stu-id="d706d-201">The storage account keys are always stored in the service in an encrypted form.</span></span> <span data-ttu-id="d706d-202">不過，您可以透過 StorSimple 裝置管理員服務來重設。</span><span class="sxs-lookup"><span data-stu-id="d706d-202">However, these can be reset via the StorSimple Device Manager service.</span></span> <span data-ttu-id="d706d-203">服務可為相同訂用帳戶中的所有儲存體帳戶取得主要金鑰與次要金鑰，包括儲存體服務中建立的帳戶以及 StorSimple 裝置管理員服務初次建立時產生的預設儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d706d-203">The service can get the primary key and secondary key for all the storage accounts in the same subscription, including accounts created in the Storage service as well as the default storage accounts generated when the StorSimple Device Manager service service was first created.</span></span> <span data-ttu-id="d706d-204">StorSimple 裝置管理員服務將一律從 Azure 傳統入口網站取得這些金鑰，再以加密的方式儲存。</span><span class="sxs-lookup"><span data-stu-id="d706d-204">The StorSimple Device Manager service will always get these keys from the Azure classic portal and then store them in an encrypted manner.</span></span>

## <a name="rotation-workflow"></a><span data-ttu-id="d706d-205">替換工作流程</span><span class="sxs-lookup"><span data-stu-id="d706d-205">Rotation workflow</span></span>

<span data-ttu-id="d706d-206">Microsoft Azure 系統管理員可以直接存取儲存體帳戶 (透過 Microsoft Azure 儲存體服務) 來重新產生或變更主要金鑰或次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="d706d-206">A Microsoft Azure administrator can regenerate or change the primary or secondary key by directly accessing the storage account (via the Microsoft Azure Storage service).</span></span> <span data-ttu-id="d706d-207">StorSimple 裝置管理員服務不會自動發現這項變更。</span><span class="sxs-lookup"><span data-stu-id="d706d-207">The StorSimple Device Manager service does not see this change automatically.</span></span>

<span data-ttu-id="d706d-208">若要向 StorSimple 裝置管理員服務通知此變更，您需要存取 StorSimple 裝置管理員服務，存取儲存體帳戶，然後同步處理主要金鑰或次要金鑰 (根據何者已變更而定)。</span><span class="sxs-lookup"><span data-stu-id="d706d-208">To inform the StorSimple Device Manager service of the change, you will need to access the StorSimple Device Manager service, access the storage account, and then synchronize the primary or secondary key (depending on which one was changed).</span></span> <span data-ttu-id="d706d-209">服務接著會取得最新的金鑰，將金鑰加密，然後將加密的金鑰傳送給裝置。</span><span class="sxs-lookup"><span data-stu-id="d706d-209">The service then gets the latest key, encrypts the keys, and sends the encrypted key to the device.</span></span>

#### <a name="to-synchronize-keys-for-storage-accounts-in-the-same-subscription-as-the-service"></a><span data-ttu-id="d706d-210">若要同步服務之相同訂用帳戶中的儲存體帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="d706d-210">To synchronize keys for storage accounts in the same subscription as the service</span></span> 
1. <span data-ttu-id="d706d-211">移至您的 StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="d706d-211">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="d706d-212">在 [設定] 區段中，按一下 [儲存體帳戶認證]。</span><span class="sxs-lookup"><span data-stu-id="d706d-212">In the **Configuration** section, click **Storage account credentials**.</span></span>
2. <span data-ttu-id="d706d-213">從儲存體帳戶的表格式清單中，按一下您要修改的項目。</span><span class="sxs-lookup"><span data-stu-id="d706d-213">From the tabular listing of storage accounts, click the one that you want to modify.</span></span> 

    ![同步處理金鑰](./media/storsimple-8000-manage-storage-accounts/syncaccesskey1.png)

3. <span data-ttu-id="d706d-215">按一下 [更多]，然後選取 [同步存取金鑰] 以進行替換。</span><span class="sxs-lookup"><span data-stu-id="d706d-215">Click **...More** and then select **Sync access key to rotate**.</span></span>   

    ![同步處理金鑰](./media/storsimple-8000-manage-storage-accounts/syncaccesskey2.png)

4. <span data-ttu-id="d706d-217">在 StorSimple 裝置管理員服務中，您需要更新先前在 Microsoft Azure 儲存體服務中變更的金鑰。</span><span class="sxs-lookup"><span data-stu-id="d706d-217">In the StorSimple Device Manager service, you need to update the key that was previously changed in the Microsoft Azure Storage service.</span></span> <span data-ttu-id="d706d-218">如果主要存取金鑰有所變更 (已重新產生)，請選取 [主要] 金鑰。</span><span class="sxs-lookup"><span data-stu-id="d706d-218">If the primary access key was changed (regenerated), select **primary** key.</span></span> <span data-ttu-id="d706d-219">如果次要金鑰有所變更，請選取 [次要] 金鑰。</span><span class="sxs-lookup"><span data-stu-id="d706d-219">If the secondary key was changed, select **secondary** key.</span></span> <span data-ttu-id="d706d-220">按一下 [同步處理金鑰]。</span><span class="sxs-lookup"><span data-stu-id="d706d-220">Click **Sync key**.</span></span>
      
      ![同步處理金鑰](./media/storsimple-8000-manage-storage-accounts/syncaccesskey3.png)

<span data-ttu-id="d706d-222">在成功同步金鑰之後，系統將會通知您。</span><span class="sxs-lookup"><span data-stu-id="d706d-222">You will be notified after the key is successfully sycnhronized.</span></span>

#### <a name="to-synchronize-keys-for-storage-accounts-outside-of-the-service-subscription"></a><span data-ttu-id="d706d-223">若要同步處理服務訂用帳戶外的儲存體帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="d706d-223">To synchronize keys for storage accounts outside of the service subscription</span></span>
1. <span data-ttu-id="d706d-224">在 [服務] 頁面上，按一下 [設定] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="d706d-224">On the **Services** page, click the **Configure** tab.</span></span>
2. <span data-ttu-id="d706d-225">按一下 [新增/編輯儲存體帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="d706d-225">Click **Add/Edit Storage Accounts**.</span></span>
3. <span data-ttu-id="d706d-226">在對話方塊中，執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="d706d-226">In the dialog box, do the following:</span></span>
   
   1. <span data-ttu-id="d706d-227">選取您要更新其存取金鑰的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d706d-227">Select the storage account with the access key that you want to update.</span></span>
   2. <span data-ttu-id="d706d-228">您必須更新 StorSimple 裝置管理員服務中的儲存體存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="d706d-228">You will need to update the storage access key in the StorSimple Device Manager service.</span></span> <span data-ttu-id="d706d-229">在此情況下，您可以看到儲存體存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="d706d-229">In this case, you can see the storage access key.</span></span> <span data-ttu-id="d706d-230">在 [儲存體帳戶存取金鑰] 方塊中，輸入新的金鑰。</span><span class="sxs-lookup"><span data-stu-id="d706d-230">Enter the new key in the **Storage Account Access Key** box.</span></span> 
   3. <span data-ttu-id="d706d-231">儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="d706d-231">Save your changes.</span></span> <span data-ttu-id="d706d-232">現在應已更新您的儲存體帳戶存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="d706d-232">Your storage account access key should now be updated.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d706d-233">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d706d-233">Next steps</span></span>
* <span data-ttu-id="d706d-234">深入了解 [StorSimple 安全性](storsimple-8000-security.md)。</span><span class="sxs-lookup"><span data-stu-id="d706d-234">Learn more about [StorSimple security](storsimple-8000-security.md).</span></span>
* <span data-ttu-id="d706d-235">深入了解[使用 StorSimple 裝置管理員服務管理 StorSimple 裝置](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="d706d-235">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

