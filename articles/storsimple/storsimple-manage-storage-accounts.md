---
title: "管理 StorSimple 儲存體帳戶 | Microsoft Docs"
description: "說明如何使用 StorSimple Manager 的 [設定] 頁面來加入、編輯、刪除或替換儲存體帳戶的安全性金鑰。"
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 93207c40-e0eb-489e-8724-59fb94907081
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/29/2016
ms.author: v-sharos
ms.openlocfilehash: 68b767c9c93f2daff476a21029b9813f347590b5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-your-storage-account"></a><span data-ttu-id="48abc-103">使用 StorSimple Manager 服務管理儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="48abc-103">Use the StorSimple Manager service to manage your storage account</span></span>
## <a name="overview"></a><span data-ttu-id="48abc-104">概觀</span><span class="sxs-lookup"><span data-stu-id="48abc-104">Overview</span></span>
<span data-ttu-id="48abc-105">[設定]  頁面會顯示所有可在 StorSimple Manager 服務中建立的全域服務參數。</span><span class="sxs-lookup"><span data-stu-id="48abc-105">The **Configure** page presents all the global service parameters that can be created in the StorSimple Manager service.</span></span> <span data-ttu-id="48abc-106">這些參數可以套用到與該服務連線的所有裝置，還包括：</span><span class="sxs-lookup"><span data-stu-id="48abc-106">These parameters can be applied to all the devices connected to the service, and include:</span></span>

* <span data-ttu-id="48abc-107">儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="48abc-107">Storage accounts</span></span> 
* <span data-ttu-id="48abc-108">頻寬範本</span><span class="sxs-lookup"><span data-stu-id="48abc-108">Bandwidth templates</span></span> 
* <span data-ttu-id="48abc-109">存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="48abc-109">Access control records</span></span> 

<span data-ttu-id="48abc-110">本教學課程說明如何使用 [設定]  頁面來新增、 編輯或刪除儲存體帳戶或替換儲存體帳戶的安全性金鑰。</span><span class="sxs-lookup"><span data-stu-id="48abc-110">This tutorial explains how you can use the **Configure** page to add, edit, or delete storage accounts, or rotate the security keys for a storage account.</span></span>

 ![[設定] 頁面](./media/storsimple-manage-storage-accounts/HCS_ConfigureService.png)  

<span data-ttu-id="48abc-112">儲存體帳戶包含的認證可供裝置用來存取雲端服務提供者的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="48abc-112">Storage accounts contain the credentials that the device uses to access your storage account with your cloud service provider.</span></span> <span data-ttu-id="48abc-113">對於 Microsoft Azure 儲存體帳戶，像是帳戶名稱與主要存取金鑰就屬於這些認證。</span><span class="sxs-lookup"><span data-stu-id="48abc-113">For Microsoft Azure storage accounts, these are credentials such as the account name and the primary access key.</span></span> 

<span data-ttu-id="48abc-114">在 [設定]  頁面上，為訂用帳戶計費而建立的所有儲存體帳戶都會以表格顯示，其中包含下列資訊：</span><span class="sxs-lookup"><span data-stu-id="48abc-114">On the **Configure** page, all storage accounts that are created for the billing subscription are displayed in a tabular format containing the following information:</span></span>

* <span data-ttu-id="48abc-115">**名稱** – 帳戶建立時獲指派的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="48abc-115">**Name** – The unique name assigned to the account when it was created.</span></span>
* <span data-ttu-id="48abc-116">**啟用 SSL** – 是否已啟用 SSL 並透過安全通道進行裝置對雲端的通訊。</span><span class="sxs-lookup"><span data-stu-id="48abc-116">**SSL enabled** – Whether the SSL is enabled and device-to-cloud communication is over the secure channel.</span></span>
* <span data-ttu-id="48abc-117">**使用者** – 使用該儲存體帳戶的的磁碟區數目。</span><span class="sxs-lookup"><span data-stu-id="48abc-117">**Used by** – The number of volumes using the storage account.</span></span>

<span data-ttu-id="48abc-118">最常見可在 [設定]  頁面上執行與儲存體帳戶相關的工作如下：</span><span class="sxs-lookup"><span data-stu-id="48abc-118">The most common tasks related to storage accounts that can be performed on the **Configure** page are:</span></span>

* <span data-ttu-id="48abc-119">新增儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="48abc-119">Add a storage account</span></span> 
* <span data-ttu-id="48abc-120">編輯儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="48abc-120">Edit a storage account</span></span> 
* <span data-ttu-id="48abc-121">刪除儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="48abc-121">Delete a storage account</span></span> 
* <span data-ttu-id="48abc-122">替換儲存體帳戶的金鑰</span><span class="sxs-lookup"><span data-stu-id="48abc-122">Key rotation of storage accounts</span></span> 

## <a name="types-of-storage-accounts"></a><span data-ttu-id="48abc-123">儲存體帳戶類型</span><span class="sxs-lookup"><span data-stu-id="48abc-123">Types of storage accounts</span></span>
<span data-ttu-id="48abc-124">有三種儲存體帳戶類型能與 StorSimple 裝置搭配使用。</span><span class="sxs-lookup"><span data-stu-id="48abc-124">There are three types of storage accounts that can be used with your StorSimple device.</span></span>

* <span data-ttu-id="48abc-125">**自動產生的儲存體帳戶** – 正如其名，這類型的儲存體帳戶是在初次建立服務時自動產生。</span><span class="sxs-lookup"><span data-stu-id="48abc-125">**Auto-generated storage accounts** – As the name suggests, this type of storage account is automatically generated when the service is first created.</span></span> <span data-ttu-id="48abc-126">若要深入了解如何建立此儲存體帳戶，請參閱[部署您的內部部署 StorSimple 裝置](storsimple-deployment-walkthrough.md)中的[步驟 1：建立新的服務](storsimple-deployment-walkthrough-u1.md#step-1-create-a-new-service)。</span><span class="sxs-lookup"><span data-stu-id="48abc-126">To learn more about how this storage account is created, see [Step 1: Create a new service](storsimple-deployment-walkthrough-u1.md#step-1-create-a-new-service) in [Deploy your on-premises StorSimple device](storsimple-deployment-walkthrough.md).</span></span> 
* <span data-ttu-id="48abc-127">**服務訂用帳戶中的儲存體帳戶** – 這些是與相同服務訂用帳戶相關聯的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="48abc-127">**Storage accounts in the service subscription** – These are the Azure storage accounts that are associated with the same subscription as that of the service.</span></span> <span data-ttu-id="48abc-128">若要深入了解如何建立這些儲存體帳戶，請參閱 [關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="48abc-128">To learn more about how these storage accounts are created, see [About Azure Storage Accounts](../storage/common/storage-create-storage-account.md).</span></span> 
* <span data-ttu-id="48abc-129">**服務訂用帳戶外的儲存體帳戶** – 這些是與服務毫無關聯的 Azure 儲存體帳戶，而且可能在服務建立之前便已存在 。</span><span class="sxs-lookup"><span data-stu-id="48abc-129">**Storage accounts outside of the service subscription** – These are the Azure storage accounts that are not associated with your service and likely existed before the service was created.</span></span>

## <a name="add-a-storage-account"></a><span data-ttu-id="48abc-130">新增儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="48abc-130">Add a storage account</span></span>
<span data-ttu-id="48abc-131">您可以提供唯一的易記名稱以及與儲存體帳戶(搭配指定的雲端服務提供者) 連結的存取認證來新增儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="48abc-131">You can add a storage account by providing a unique friendly name and access credentials that are linked to the storage account (with the specified cloud service provider).</span></span> <span data-ttu-id="48abc-132">您也能選擇啟用安全通訊端層 (SSL) 模式，建立裝置與雲端之間網路通訊的安全通道。</span><span class="sxs-lookup"><span data-stu-id="48abc-132">You also have the option of enabling the secure sockets layer (SSL) mode to create a secure channel for network communication between your device and the cloud.</span></span>

<span data-ttu-id="48abc-133">您可以為指定的雲端服務提供者建立多個帳戶。</span><span class="sxs-lookup"><span data-stu-id="48abc-133">You can create multiple accounts for a given cloud service provider.</span></span> <span data-ttu-id="48abc-134">不過，請注意，建立儲存體帳戶之後，您無法變更雲端服務提供者。</span><span class="sxs-lookup"><span data-stu-id="48abc-134">Be aware, however, that after a storage account is created, you cannot change the cloud service provider.</span></span>

<span data-ttu-id="48abc-135">儲存體帳戶在儲存時，服務會嘗試與您的雲端服務提供者通訊。</span><span class="sxs-lookup"><span data-stu-id="48abc-135">While the storage account is being saved, the service attempts to communicate with your cloud service provider.</span></span> <span data-ttu-id="48abc-136">此時會驗證您提供的認證與存取資料。</span><span class="sxs-lookup"><span data-stu-id="48abc-136">The credentials and the access material that you supplied will be authenticated at this time.</span></span> <span data-ttu-id="48abc-137">只有當驗證成功時，才會建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="48abc-137">A storage account is created only if the authentication succeeds.</span></span> <span data-ttu-id="48abc-138">如果驗證失敗，則會顯示適當的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="48abc-138">If the authentication fails, then an appropriate error message will be displayed.</span></span>

<span data-ttu-id="48abc-139">在 Azure 入口網站中建立的 Resource Manager 儲存體帳戶也支援 StorSimple。</span><span class="sxs-lookup"><span data-stu-id="48abc-139">Resource Manager storage accounts created in Azure portal are also supported with StorSimple.</span></span> <span data-ttu-id="48abc-140">嘗試建立磁碟區容器時，下拉式清單中將不會顯示 Resource Manager 儲存體帳戶供選取，只會顯示在 Azure 傳統入口網站中建立的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="48abc-140">The Resource Manager storage accounts will not show up in the drop-down list for selection when trying to create a volume container, only the storage accounts created in the Azure classic portal will be displayed.</span></span> <span data-ttu-id="48abc-141">Resource Manager 儲存體帳戶必須使用如下所述的新增儲存體帳戶的程序來新增。</span><span class="sxs-lookup"><span data-stu-id="48abc-141">Resource Manager storage accounts will need to be added using the procedure to add a storage account described below.</span></span>

> [!NOTE]
> <span data-ttu-id="48abc-142">新增儲存體帳戶的程序將因為使用的軟體版本而有所不同。</span><span class="sxs-lookup"><span data-stu-id="48abc-142">The procedure for adding a storage account differs based on the StorSimple software version you are using.</span></span> <span data-ttu-id="48abc-143">請務必依照您 StorSimple 版本適用的程序執行。</span><span class="sxs-lookup"><span data-stu-id="48abc-143">Be sure to follow the correct procedure for your StorSimple version.</span></span>
> 
> 

[!INCLUDE [add-a-storage-account-update1](../../includes/storsimple-configure-new-storage-account-u1.md)]

[!INCLUDE [add-a-storage-account](../../includes/storsimple-configure-new-storage-account.md)]

## <a name="edit-a-storage-account"></a><span data-ttu-id="48abc-144">編輯儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="48abc-144">Edit a storage account</span></span>
<span data-ttu-id="48abc-145">您可以編輯磁碟區容器所使用的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="48abc-145">You can edit a storage account that is used by a volume container.</span></span> <span data-ttu-id="48abc-146">如果您編輯的儲存體帳戶目前正在使用中，唯一可修改的欄位就是儲存體帳戶的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="48abc-146">If you edit a storage account that is currently in use, the only field available to modify is the access key for the storage account.</span></span> <span data-ttu-id="48abc-147">您可以提供新的儲存體存取金鑰，並儲存更新的設定。</span><span class="sxs-lookup"><span data-stu-id="48abc-147">You can supply the new storage access key and save the updated settings.</span></span>

#### <a name="to-edit-a-storage-account"></a><span data-ttu-id="48abc-148">若要編輯儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="48abc-148">To edit a storage account</span></span>
1. <span data-ttu-id="48abc-149">在服務登陸頁面上，選取您的服務，連按兩下該服務名稱，然後按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="48abc-149">On the service landing page, select your service, double-click the service name, and then click **Configure**.</span></span>
2. <span data-ttu-id="48abc-150">按一下 [新增/編輯儲存體帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="48abc-150">Click **Add/Edit Storage Accounts**.</span></span>
3. <span data-ttu-id="48abc-151">在 [新增/編輯儲存體帳戶]  對話方塊中：</span><span class="sxs-lookup"><span data-stu-id="48abc-151">In the **Add/Edit Storage Accounts** dialog box:</span></span>
   
   1. <span data-ttu-id="48abc-152">在 [儲存體帳戶] 下拉式清單中，選擇您想要修改的現有帳戶。</span><span class="sxs-lookup"><span data-stu-id="48abc-152">In the drop-down list of **Storage Accounts**, choose an existing account that you would like to modify.</span></span> <span data-ttu-id="48abc-153">這也包含服務初次建立時自動產生的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="48abc-153">This could also include the storage accounts that were automatically generated when the service was first created.</span></span>
   2. <span data-ttu-id="48abc-154">如有必要，您可以修改 [啟用 SSL 模式]  選項。</span><span class="sxs-lookup"><span data-stu-id="48abc-154">If necessary, you can modify the **Enable SSL Mode** selection.</span></span>
   3. <span data-ttu-id="48abc-155">您可以選擇替換儲存體帳戶存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="48abc-155">You can choose to rotate your storage account access keys.</span></span> <span data-ttu-id="48abc-156">如需如何執行金鑰替換的詳細資訊，請參閱 [替換儲存體帳戶的金鑰](#key-rotation-of-storage-accounts) 。</span><span class="sxs-lookup"><span data-stu-id="48abc-156">See [Key rotation of storage accounts](#key-rotation-of-storage-accounts) for more information about how to perform key rotation.</span></span>
   4. <span data-ttu-id="48abc-157">按一下核取圖示 ![核取圖示](./media/storsimple-manage-storage-accounts/HCS_CheckIcon.png) 以儲存設定。</span><span class="sxs-lookup"><span data-stu-id="48abc-157">Click the check icon ![check icon](./media/storsimple-manage-storage-accounts/HCS_CheckIcon.png) to save the settings.</span></span> <span data-ttu-id="48abc-158">[設定]  頁面上的設定隨即更新。</span><span class="sxs-lookup"><span data-stu-id="48abc-158">The settings will be updated on the **Configure** page.</span></span> <span data-ttu-id="48abc-159">按一下 [儲存]  以儲存剛更新的設定。</span><span class="sxs-lookup"><span data-stu-id="48abc-159">Click **Save** to save the newly updated settings.</span></span>
      
      ![編輯儲存體帳戶](./media/storsimple-manage-storage-accounts/HCs_AddEditStorageAccount.png)

## <a name="delete-a-storage-account"></a><span data-ttu-id="48abc-161">刪除儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="48abc-161">Delete a storage account</span></span>
> [!IMPORTANT]
> <span data-ttu-id="48abc-162">只有在其未由磁碟區容器使用時，您才可以刪除儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="48abc-162">You can delete a storage account only if it is not used by a volume container.</span></span> <span data-ttu-id="48abc-163">如果磁碟區容器正在使用儲存體帳戶，請先刪除磁碟區容器，然後再刪除相關聯的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="48abc-163">If a storage account is being used by a volume container, first delete the volume container and then delete the associated storage account.</span></span>
> 
> 

#### <a name="to-delete-a-storage-account"></a><span data-ttu-id="48abc-164">若要刪除儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="48abc-164">To delete a storage account</span></span>
1. <span data-ttu-id="48abc-165">在 StorSimple Manager 服務登陸頁面上，選取您的服務，連按兩下該服務名稱，然後按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="48abc-165">On the StorSimple Manager service landing page, select your service, double-click the service name, and then click **Configure**.</span></span>
2. <span data-ttu-id="48abc-166">在儲存體帳戶的表格式清單中，將滑鼠停留在您想要刪除的帳戶上方。</span><span class="sxs-lookup"><span data-stu-id="48abc-166">In the tabular list of storage accounts, hover over the account that you wish to delete.</span></span>
3. <span data-ttu-id="48abc-167">刪除圖示 (**x**) 會出現在該儲存體帳戶資料行的最右邊。</span><span class="sxs-lookup"><span data-stu-id="48abc-167">A delete icon (**x**) will appear in the extreme right column for that storage account.</span></span> <span data-ttu-id="48abc-168">按一下 [x]  圖示，以刪除認證。</span><span class="sxs-lookup"><span data-stu-id="48abc-168">Click the **x** icon to delete the credentials.</span></span>
4. <span data-ttu-id="48abc-169">當系統提示您確認時，按一下 [是]  繼續進行刪除。</span><span class="sxs-lookup"><span data-stu-id="48abc-169">When prompted for confirmation, click **Yes** to continue with the deletion.</span></span> <span data-ttu-id="48abc-170">表格式清單會更新以反映所做的變更。</span><span class="sxs-lookup"><span data-stu-id="48abc-170">The tabular listing will be updated to reflect the changes.</span></span>

## <a name="key-rotation-of-storage-accounts"></a><span data-ttu-id="48abc-171">替換儲存體帳戶的金鑰</span><span class="sxs-lookup"><span data-stu-id="48abc-171">Key rotation of storage accounts</span></span>
<span data-ttu-id="48abc-172">基於安全性理由，通常是在資料中心內才需要替換金鑰。</span><span class="sxs-lookup"><span data-stu-id="48abc-172">For security reasons, key rotation is often a requirement in data centers.</span></span> 

> [!NOTE]
> <span data-ttu-id="48abc-173">下面的金鑰輪替資訊和程序僅適用於 Microsoft Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="48abc-173">The following key rotation information and the rotation procedure apply to Microsoft Azure storage accounts only.</span></span> <span data-ttu-id="48abc-174">若您使用的是其他雲端服務提供者，可以透過該提供者的儀表板管理儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="48abc-174">If you are using another cloud service provider, you can manage storage account keys through that provider's dashboard.</span></span>
> 
> 

<span data-ttu-id="48abc-175">每個 Microsoft Azure 訂用帳戶可以有一或多個相關聯的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="48abc-175">Each Microsoft Azure subscription can have one or more associated storage accounts.</span></span> <span data-ttu-id="48abc-176">訂用帳戶與每個儲存體帳戶的存取金鑰可以控制這些帳戶的存取權。</span><span class="sxs-lookup"><span data-stu-id="48abc-176">The access to these accounts is controlled by the subscription and access keys for each storage account.</span></span> 

<span data-ttu-id="48abc-177">當您建立儲存體帳戶時，Azure 會產生兩個 512 位元的儲存體存取金鑰，可在存取儲存體帳戶時用於驗證。</span><span class="sxs-lookup"><span data-stu-id="48abc-177">When you create a storage account, Microsoft Azure generates two 512-bit storage access keys that are used for authentication when the storage account is accessed.</span></span> <span data-ttu-id="48abc-178">有這兩個儲存體存取金鑰，您不需要中斷儲存體服務或對該服務的存取，就能重新產生金鑰。</span><span class="sxs-lookup"><span data-stu-id="48abc-178">Having two storage access keys allows you to regenerate the keys with no interruption to your storage service or access to that service.</span></span> <span data-ttu-id="48abc-179">目前使用中的金鑰是「主要」金鑰，而備份金鑰則稱為「次要」金鑰。</span><span class="sxs-lookup"><span data-stu-id="48abc-179">The key that is currently in use is the *primary* key and the backup key is referred to as the *secondary* key.</span></span> <span data-ttu-id="48abc-180">當 Microsoft Azure StorSimple 裝置存取您的雲端儲存體服務提供者時必須提供這些兩個機碼之一。</span><span class="sxs-lookup"><span data-stu-id="48abc-180">One of these two keys must be supplied when your Microsoft Azure StorSimple device accesses your cloud storage service provider.</span></span>

## <a name="what-is-key-rotation"></a><span data-ttu-id="48abc-181">什麼是替換金鑰？</span><span class="sxs-lookup"><span data-stu-id="48abc-181">What is key rotation?</span></span>
<span data-ttu-id="48abc-182">一般而言，應用程式只使用其中一個金鑰來存取您的資料。</span><span class="sxs-lookup"><span data-stu-id="48abc-182">Typically, applications use only one of the keys to access your data.</span></span> <span data-ttu-id="48abc-183">經過一段時間之後，您可以讓應用程式切換為使用第二個金鑰。</span><span class="sxs-lookup"><span data-stu-id="48abc-183">After a certain period of time, you can have your applications switch over to using the second key.</span></span> <span data-ttu-id="48abc-184">在您將應用程式切換至次要金鑰之後，可以淘汰第一個金鑰，然後產生新的金鑰。</span><span class="sxs-lookup"><span data-stu-id="48abc-184">After you have switched your applications to the secondary key, you can retire the first key and then generate a new key.</span></span> <span data-ttu-id="48abc-185">這種使用兩個金鑰的方式可讓您的應用程式存取資料，卻不會產生任何停機時間。</span><span class="sxs-lookup"><span data-stu-id="48abc-185">Using the two keys this way allows your applications access to the data without incurring any downtime.</span></span>

<span data-ttu-id="48abc-186">儲存體帳戶金鑰一律以加密的格式儲存在服務中。</span><span class="sxs-lookup"><span data-stu-id="48abc-186">The storage account keys are always stored in the service in an encrypted form.</span></span> <span data-ttu-id="48abc-187">不過，您可以透過 StorSimple Manager 服務來重設。</span><span class="sxs-lookup"><span data-stu-id="48abc-187">However, these can be reset via the StorSimple Manager service.</span></span> <span data-ttu-id="48abc-188">服務可為相同訂用帳戶中的所有儲存體帳戶取得主要金鑰與次要金鑰，包括儲存體服務中建立的帳戶以及 StorSimple Manager 服務初次建立時產生的預設儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="48abc-188">The service can get the primary key and secondary key for all the storage accounts in the same subscription, including accounts created in the Storage service as well as the default storage accounts generated when the StorSimple Manager service service was first created.</span></span> <span data-ttu-id="48abc-189">StorSimple Manager 服務將一律從 Azure 傳統入口網站取得這些金鑰，再以加密的方式儲存。</span><span class="sxs-lookup"><span data-stu-id="48abc-189">The StorSimple Manager service service will always get these keys from the Azure classic portal and then store them in an encrypted manner.</span></span>

## <a name="rotation-workflow"></a><span data-ttu-id="48abc-190">替換工作流程</span><span class="sxs-lookup"><span data-stu-id="48abc-190">Rotation workflow</span></span>
<span data-ttu-id="48abc-191">Microsoft Azure 系統管理員可以直接存取儲存體帳戶 (透過 Microsoft Azure 儲存體服務) 來重新產生或變更主要金鑰或次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="48abc-191">A Microsoft Azure administrator can regenerate or change the primary or secondary key by directly accessing the storage account (via the Microsoft Azure Storage service).</span></span> <span data-ttu-id="48abc-192">StorSimple Manager 服務不會自動發現這項變更。</span><span class="sxs-lookup"><span data-stu-id="48abc-192">The StorSimple Manager service does not see this change automatically.</span></span>

<span data-ttu-id="48abc-193">若要通知 StorSimple Manager 服務所做的變更，您需要存取 StorSimple Manager 服務，存取儲存體帳戶，然後同步處理主要或次要金鑰 (根據哪一個有變更而定)。</span><span class="sxs-lookup"><span data-stu-id="48abc-193">To inform the StorSimple Manager service of the change, you will need to access the StorSimple Manager service, access the storage account, and then synchronize the primary or secondary key (depending on which one was changed).</span></span> <span data-ttu-id="48abc-194">服務接著會取得最新的金鑰，將金鑰加密，然後將加密的金鑰傳送給裝置。</span><span class="sxs-lookup"><span data-stu-id="48abc-194">The service then gets the latest key, encrypts the keys, and sends the encrypted key to the device.</span></span>

#### <a name="to-synchronize-keys-for-storage-accounts-in-the-same-subscription-as-the-service-azure-only"></a><span data-ttu-id="48abc-195">若要同步服務 (僅限 Azure only) 之訂用帳戶中的儲存體帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="48abc-195">To synchronize keys for storage accounts in the same subscription as the service (Azure only)</span></span>
1. <span data-ttu-id="48abc-196">在 [服務] 頁面上，按一下 [設定] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="48abc-196">On the **Services** page, click the **Configure** tab.</span></span>
2. <span data-ttu-id="48abc-197">按一下 [新增/編輯儲存體帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="48abc-197">Click **Add/Edit Storage Accounts**.</span></span>
3. <span data-ttu-id="48abc-198">在對話方塊中，執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="48abc-198">In the dialog box, do the following:</span></span>
   
   1. <span data-ttu-id="48abc-199">選取您要同步處理其金鑰的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="48abc-199">Select the storage account with the key that you want to synchronize.</span></span> <span data-ttu-id="48abc-200">儲存體帳戶金鑰是以加密的狀態顯示。</span><span class="sxs-lookup"><span data-stu-id="48abc-200">The storage account keys are encrypted when they are displayed.</span></span>
   2. <span data-ttu-id="48abc-201">在 StorSimple Manager 服務中，您需要更新先前在 Microsoft Azure 儲存體服務中變更的金鑰。</span><span class="sxs-lookup"><span data-stu-id="48abc-201">In the StorSimple Manager service, you need to update the key that was previously changed in the Microsoft Azure Storage service.</span></span> <span data-ttu-id="48abc-202">如果主要存取金鑰有所變更 (已重新產生)，按一下 [同步處理主要金鑰] 。</span><span class="sxs-lookup"><span data-stu-id="48abc-202">If the primary access key was changed (regenerated), click **synchronize primary key**.</span></span> <span data-ttu-id="48abc-203">如果次要金鑰有所變更，按一下 [同步處理次要金鑰] 。</span><span class="sxs-lookup"><span data-stu-id="48abc-203">If the secondary key was changed, click **synchronize secondary key**.</span></span>
      
      ![同步處理金鑰](./media/storsimple-manage-storage-accounts/HCS_KeyRotationStorageAccountSameSubscriptionAsService.png)

#### <a name="to-synchronize-keys-for-storage-accounts-outside-of-the-service-subscription"></a><span data-ttu-id="48abc-205">若要同步處理服務訂用帳戶外的儲存體帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="48abc-205">To synchronize keys for storage accounts outside of the service subscription</span></span>
1. <span data-ttu-id="48abc-206">在 [服務] 頁面上，按一下 [設定] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="48abc-206">On the **Services** page, click the **Configure** tab.</span></span>
2. <span data-ttu-id="48abc-207">按一下 [新增/編輯儲存體帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="48abc-207">Click **Add/Edit Storage Accounts**.</span></span>
3. <span data-ttu-id="48abc-208">在對話方塊中，執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="48abc-208">In the dialog box, do the following:</span></span>
   
   1. <span data-ttu-id="48abc-209">選取您要更新其存取金鑰的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="48abc-209">Select the storage account with the access key that you want to update.</span></span>
   2. <span data-ttu-id="48abc-210">您必須更新 StorSimple Manager 服務中的儲存體存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="48abc-210">You will need to update the storage access key in the StorSimple Manager service.</span></span> <span data-ttu-id="48abc-211">在此情況下，您可以看到儲存體存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="48abc-211">In this case, you can see the storage access key.</span></span> <span data-ttu-id="48abc-212">在 [ **儲存體帳戶存取金鑰**] 方塊中，輸入新的金鑰。</span><span class="sxs-lookup"><span data-stu-id="48abc-212">Enter the new key in the **Storage Account Access Key**y box.</span></span> 
   3. <span data-ttu-id="48abc-213">儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="48abc-213">Save your changes.</span></span> <span data-ttu-id="48abc-214">現在應已更新您的儲存體帳戶存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="48abc-214">Your storage account access key should now be updated.</span></span>

## <a name="next-steps"></a><span data-ttu-id="48abc-215">後續步驟</span><span class="sxs-lookup"><span data-stu-id="48abc-215">Next steps</span></span>
* <span data-ttu-id="48abc-216">深入了解 [StorSimple 安全性](storsimple-security.md)。</span><span class="sxs-lookup"><span data-stu-id="48abc-216">Learn more about [StorSimple security](storsimple-security.md).</span></span>
* <span data-ttu-id="48abc-217">深入了解 [使用 StorSimple Manager 服務管理 StorSimple 裝置](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="48abc-217">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

