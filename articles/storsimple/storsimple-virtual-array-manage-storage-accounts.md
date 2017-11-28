---
title: "管理 StorSimple Virtual Array 儲存體帳戶認證 | Microsoft Docs"
description: "針對與 StorSimple Virtual Array 相關聯的儲存體帳戶認證，說明如何使用 StorSimple 裝置管理員的 [設定] 頁面來新增、編輯、刪除或替換安全性金鑰。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 234bf8bb-d5fe-40be-9d25-721d7482bc3b
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.openlocfilehash: a4ce2d329d0e1399cffaf886adf2b95e34b9cd7b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-storsimple-device-manager-to-manage-storage-account-credentials-for-storsimple-virtual-array"></a><span data-ttu-id="cdd36-103">使用 StorSimple 裝置管理員來管理 StorSimple Virtual Array 的儲存體帳戶認證</span><span class="sxs-lookup"><span data-stu-id="cdd36-103">Use StorSimple Device Manager to manage storage account credentials for StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="cdd36-104">概觀</span><span class="sxs-lookup"><span data-stu-id="cdd36-104">Overview</span></span>
<span data-ttu-id="cdd36-105">在 StorSimple Virtual Array 的 StorSimple 裝置管理員服務刀鋒視窗中，[設定] 區段會顯示可在 StorSimple Manager 服務中建立的全域服務參數。</span><span class="sxs-lookup"><span data-stu-id="cdd36-105">The **Configuration** section of the StorSimple Device Manager service blade of your StorSimple Virtual Array presents the global service parameters that can be created in the StorSimple Manager service.</span></span> <span data-ttu-id="cdd36-106">這些參數可以套用到與該服務連線的所有裝置，還包括：</span><span class="sxs-lookup"><span data-stu-id="cdd36-106">These parameters can be applied to all the devices connected to the service, and include:</span></span>

* <span data-ttu-id="cdd36-107">儲存體帳戶認證</span><span class="sxs-lookup"><span data-stu-id="cdd36-107">Storage account credentials</span></span>
* <span data-ttu-id="cdd36-108">存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="cdd36-108">Access control records</span></span>
  
  ![裝置管理員服務儀表板](./media/storsimple-virtual-array-manage-storage-accounts/ova-storageaccts-dashboard.png)  

<span data-ttu-id="cdd36-110">本教學課程說明如何新增、編輯或刪除 StorSimple Virtual Array 的儲存體帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="cdd36-110">This tutorial explains how you can add, edit, or delete storage account credentials for your StorSimple Virtual Array.</span></span> <span data-ttu-id="cdd36-111">本教學課程中的資訊僅適用於 StorSimple Virtual Array。</span><span class="sxs-lookup"><span data-stu-id="cdd36-111">The information in this tutorial only applies to the StorSimple Virtual Array.</span></span> <span data-ttu-id="cdd36-112">如需如何在 8000 系列中管理儲存體帳戶的相關資訊，請參閱[使用 StorSimple Manager 服務來管理儲存體帳戶](storsimple-manage-storage-accounts.md)。</span><span class="sxs-lookup"><span data-stu-id="cdd36-112">For information on how to manage storage accounts in 8000 series, see [Use the StorSimple Manager service to manage your storage account](storsimple-manage-storage-accounts.md).</span></span>

<span data-ttu-id="cdd36-113">儲存體帳戶認證包含的認證可供裝置用來存取您在雲端服務提供者中的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="cdd36-113">Storage account credentials contain the credentials that the device uses to access your storage account with your cloud service provider.</span></span> <span data-ttu-id="cdd36-114">對於 Microsoft Azure 儲存體帳戶，像是帳戶名稱與主要存取金鑰就屬於這些認證。</span><span class="sxs-lookup"><span data-stu-id="cdd36-114">For Microsoft Azure storage accounts, these are credentials such as the account name and the primary access key.</span></span>

<span data-ttu-id="cdd36-115">在 [儲存體帳戶認證] 刀鋒視窗上，為訂用帳戶計費而建立的所有儲存體帳戶認證都會以表格顯示，其中包含下列資訊：</span><span class="sxs-lookup"><span data-stu-id="cdd36-115">On the **Storage account credentials** blade, all storage account credentials that are created for the billing subscription are displayed in a tabular format containing the following information:</span></span>

* <span data-ttu-id="cdd36-116">**名稱** – 帳戶建立時獲指派的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="cdd36-116">**Name** – The unique name assigned to the account when it was created.</span></span>
* <span data-ttu-id="cdd36-117">**啟用 SSL** – 是否已啟用 SSL 並透過安全通道進行裝置對雲端的通訊。</span><span class="sxs-lookup"><span data-stu-id="cdd36-117">**SSL enabled** – Whether the SSL is enabled and device-to-cloud communication is over the secure channel.</span></span>
  
  ![[設定] 區段](./media/storsimple-virtual-array-manage-storage-accounts/ova-storageaccountcredentials-blade.png)

<span data-ttu-id="cdd36-119">在 [儲存體帳戶認證] 刀鋒視窗上，最常見可執行的儲存體帳戶認證相關工作如下︰</span><span class="sxs-lookup"><span data-stu-id="cdd36-119">The most common tasks related to storage account credentials that can be performed on the **Storage account credentials** blade are:</span></span>

* <span data-ttu-id="cdd36-120">新增儲存體帳戶認證</span><span class="sxs-lookup"><span data-stu-id="cdd36-120">Add a storage account credential</span></span>
* <span data-ttu-id="cdd36-121">編輯儲存體帳戶認證</span><span class="sxs-lookup"><span data-stu-id="cdd36-121">Edit a storage account credential</span></span>
* <span data-ttu-id="cdd36-122">刪除儲存體帳戶認證</span><span class="sxs-lookup"><span data-stu-id="cdd36-122">Delete a storage account credential</span></span>

## <a name="types-of-storage-account-credentials"></a><span data-ttu-id="cdd36-123">儲存體帳戶認證的類型</span><span class="sxs-lookup"><span data-stu-id="cdd36-123">Types of storage account credentials</span></span>
<span data-ttu-id="cdd36-124">有三種儲存體帳戶認證類型可以與 StorSimple 裝置搭配使用。</span><span class="sxs-lookup"><span data-stu-id="cdd36-124">There are three types of storage account credentials that can be used with your StorSimple device.</span></span>

* <span data-ttu-id="cdd36-125">**自動產生的儲存體帳戶認證** – 正如其名，初次建立服務時會自動產生這種儲存體帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="cdd36-125">**Auto-generated storage account credentials** – As the name suggests, this type of storage account credential is automatically generated when the service is first created.</span></span> <span data-ttu-id="cdd36-126">若要深入了解如何建立此儲存體帳戶認證，請參閱[建立新的服務](storsimple-virtual-array-manage-service.md#create-a-service)。</span><span class="sxs-lookup"><span data-stu-id="cdd36-126">To learn more about how this storage account credential is created, see [Create a new service](storsimple-virtual-array-manage-service.md#create-a-service).</span></span>
* <span data-ttu-id="cdd36-127">**服務訂用帳戶中的儲存體帳戶認證** – 這些是與相同服務訂用帳戶相關聯的 Azure 儲存體帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="cdd36-127">**storage account credentials in the service subscription** – These are the Azure storage account credentials that are associated with the same subscription as that of the service.</span></span> <span data-ttu-id="cdd36-128">若要深入了解如何建立這些儲存體帳戶認證，請參閱[關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="cdd36-128">To learn more about how these storage account credentials are created, see [About Azure Storage Accounts](../storage/common/storage-create-storage-account.md).</span></span>
* <span data-ttu-id="cdd36-129">**服務訂用帳戶外的儲存體帳戶認證** – 這些是與服務毫無關聯的 Azure 儲存體帳戶認證，可能在服務建立之前就存在。</span><span class="sxs-lookup"><span data-stu-id="cdd36-129">**storage account credentials outside of the service subscription** – These are the Azure storage account credentials that are not associated with your service and likely existed before the service was created.</span></span>

## <a name="add-a-storage-account-credential"></a><span data-ttu-id="cdd36-130">新增儲存體帳戶認證</span><span class="sxs-lookup"><span data-stu-id="cdd36-130">Add a storage account credential</span></span>
<span data-ttu-id="cdd36-131">您可以提供唯一的易記名稱和連結至儲存體帳戶的存取認證，將儲存體帳戶認證新增至 StorSimple 裝置管理員服務設定。</span><span class="sxs-lookup"><span data-stu-id="cdd36-131">You can add a storage account credential to your StorSimple Device Manager service configuration by providing a unique friendly name and access credentials that are linked to the storage account.</span></span> <span data-ttu-id="cdd36-132">您也能選擇啟用安全通訊端層 (SSL) 模式，建立裝置與雲端之間網路通訊的安全通道。</span><span class="sxs-lookup"><span data-stu-id="cdd36-132">You also have the option of enabling the secure sockets layer (SSL) mode to create a secure channel for network communication between your device and the cloud.</span></span>

<span data-ttu-id="cdd36-133">您可以為指定的雲端服務提供者建立多個帳戶。</span><span class="sxs-lookup"><span data-stu-id="cdd36-133">You can create multiple accounts for a given cloud service provider.</span></span> <span data-ttu-id="cdd36-134">當儲存體帳戶正在儲存時，服務會嘗試與您的雲端服務提供者通訊。</span><span class="sxs-lookup"><span data-stu-id="cdd36-134">While the storage account credential is being saved, the service attempts to communicate with your cloud service provider.</span></span> <span data-ttu-id="cdd36-135">此時會驗證您提供的認證與存取資料。</span><span class="sxs-lookup"><span data-stu-id="cdd36-135">The credentials and the access material that you supplied are authenticated at this time.</span></span> <span data-ttu-id="cdd36-136">只有當驗證成功時，才會建立儲存體帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="cdd36-136">A storage account credential is created only if the authentication succeeds.</span></span> <span data-ttu-id="cdd36-137">如果驗證失敗，則會顯示適當的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="cdd36-137">If the authentication fails, then an appropriate error message is displayed.</span></span>

<span data-ttu-id="cdd36-138">使用下列程序來新增 Azure 儲存體帳戶認證︰</span><span class="sxs-lookup"><span data-stu-id="cdd36-138">Use the following procedures to add Azure storage account credentials:</span></span>

* <span data-ttu-id="cdd36-139">若要新增儲存體帳戶認證，而且其 Azure 訂用帳戶與裝置管理員服務相同</span><span class="sxs-lookup"><span data-stu-id="cdd36-139">To add a storage account credential that has the same Azure subscription as the Device Manager service</span></span>
* <span data-ttu-id="cdd36-140">若要新增裝置管理員服務訂用帳戶外的 Azure 儲存體帳戶認證</span><span class="sxs-lookup"><span data-stu-id="cdd36-140">To add an Azure storage account credential that is outside of the Device Manager service subscription</span></span>

#### <a name="to-add-a-storage-account-credential-that-has-the-same-azure-subscription-as-the-device-manager-service"></a><span data-ttu-id="cdd36-141">若要新增儲存體帳戶認證，而且其 Azure 訂用帳戶與裝置管理員服務相同</span><span class="sxs-lookup"><span data-stu-id="cdd36-141">To add a storage account credential that has the same Azure subscription as the Device Manager service</span></span>

1. <span data-ttu-id="cdd36-142">瀏覽至您的裝置管理員服務，選取它並按兩下。</span><span class="sxs-lookup"><span data-stu-id="cdd36-142">Navigate to your Device Manager service, select and double-click it.</span></span> <span data-ttu-id="cdd36-143">這會開啟 [概觀] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="cdd36-143">This opens the **Overview** blade.</span></span>
2. <span data-ttu-id="cdd36-144">在 [設定] 區段內選取 [儲存體帳戶認證]。</span><span class="sxs-lookup"><span data-stu-id="cdd36-144">Select **Storage account credentials** within the **Configuration** section.</span></span>
3. <span data-ttu-id="cdd36-145">按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="cdd36-145">Click **Add**.</span></span>
4. <span data-ttu-id="cdd36-146">在 [加入儲存體帳戶] 刀鋒視窗中，執行下列動作︰</span><span class="sxs-lookup"><span data-stu-id="cdd36-146">In the **Add a storage account** blade, do the following:</span></span>
   
    1. <span data-ttu-id="cdd36-147">在 [訂用帳戶] 中，選取 [目前]。</span><span class="sxs-lookup"><span data-stu-id="cdd36-147">For **Subscription**, select **Current**.</span></span>
    2. <span data-ttu-id="cdd36-148">提供您 Azure 儲存體帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="cdd36-148">Provide the name of your Azure storage account.</span></span>
    3. <span data-ttu-id="cdd36-149">選取 [啟用]，為 StorSimple 裝置與雲端之間的網路通訊建立安全通道。</span><span class="sxs-lookup"><span data-stu-id="cdd36-149">Select **Enable** to create a secure channel for network communication between your StorSimple device and the cloud.</span></span> <span data-ttu-id="cdd36-150">只有當您在私人雲端內操作時，才選取 [停用]。</span><span class="sxs-lookup"><span data-stu-id="cdd36-150">Select **Disable** only if you are operating within a private cloud.</span></span>
    4. <span data-ttu-id="cdd36-151">按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="cdd36-151">Click **Add**.</span></span> <span data-ttu-id="cdd36-152">成功建立儲存體帳戶之後會通知您。</span><span class="sxs-lookup"><span data-stu-id="cdd36-152">You are notified after the storage account is successfully created.</span></span><br></br>
   
        ![新增現有儲存體帳戶認證](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-storageacct.png)

#### <a name="to-add-an-azure-storage-account-credential-that-is-outside-of-the-device-manager-service-subscription"></a><span data-ttu-id="cdd36-154">若要新增裝置管理員服務訂用帳戶外的 Azure 儲存體帳戶認證</span><span class="sxs-lookup"><span data-stu-id="cdd36-154">To add an Azure storage account credential that is outside of the Device Manager service subscription</span></span>

1. <span data-ttu-id="cdd36-155">瀏覽至您的裝置管理員服務，選取它並按兩下。</span><span class="sxs-lookup"><span data-stu-id="cdd36-155">Navigate to your Device Manager service, select and double-click it.</span></span> <span data-ttu-id="cdd36-156">這會開啟 [概觀] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="cdd36-156">This opens the **Overview** blade.</span></span>
2. <span data-ttu-id="cdd36-157">在 [設定] 區段內選取 [儲存體帳戶認證]。</span><span class="sxs-lookup"><span data-stu-id="cdd36-157">Select **Storage account credentials** within the **Configuration** section.</span></span> <span data-ttu-id="cdd36-158">這樣會列出與 StorSimple 裝置管理員服務相關聯的任何現有儲存體帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="cdd36-158">This lists any existing storage account credentials associated with the StorSimple Device Manager service.</span></span>
3. <span data-ttu-id="cdd36-159">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="cdd36-159">Click **Add**.</span></span>
4. <span data-ttu-id="cdd36-160">在 [加入儲存體帳戶] 刀鋒視窗中，執行下列動作︰</span><span class="sxs-lookup"><span data-stu-id="cdd36-160">In the **Add a storage account** blade, do the following:</span></span>
   
    1. <span data-ttu-id="cdd36-161">在 [訂用帳戶] 中，選取 [其他]。</span><span class="sxs-lookup"><span data-stu-id="cdd36-161">For **Subscription**, select **Other**.</span></span>
   
    2. <span data-ttu-id="cdd36-162">提供 Azure 儲存體帳戶認證的名稱。</span><span class="sxs-lookup"><span data-stu-id="cdd36-162">Provide the name of your Azure storage account credential.</span></span>
   
    3. <span data-ttu-id="cdd36-163">在 [儲存體帳戶存取金鑰]文字方塊中，提供 Azure 儲存體帳戶認證的主要「存取金鑰」。</span><span class="sxs-lookup"><span data-stu-id="cdd36-163">In the **Storage account access key** text box, supply the primary Access Key for your Azure storage account credential.</span></span> <span data-ttu-id="cdd36-164">若要取得此金鑰，請移至 Azure 儲存體服務，選取您的儲存體帳戶認證，然後按一下 [管理帳戶金鑰]。</span><span class="sxs-lookup"><span data-stu-id="cdd36-164">To get this key, go to the Azure Storage service, select your storage account credential, and click **Manage account keys**.</span></span> <span data-ttu-id="cdd36-165">現在，您可以複製主要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="cdd36-165">You can now copy the primary access key.</span></span>
   
    4. <span data-ttu-id="cdd36-166">若要啟用 SSL，請按一下 [啟用] 按鈕，為 StorSimple 裝置管理員服務與雲端之間的網路通訊建立安全通道。</span><span class="sxs-lookup"><span data-stu-id="cdd36-166">To enable SSL, click the **Enable** button to create a secure channel for network communication between your StorSimple Device Manager service and the cloud.</span></span> <span data-ttu-id="cdd36-167">只有當您在私人雲端內操作時，才按一下 [停用] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cdd36-167">Click the **Disable** button only if you are operating within a private cloud.</span></span>
   
    5. <span data-ttu-id="cdd36-168">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="cdd36-168">Click **Add**.</span></span> <span data-ttu-id="cdd36-169">成功建立儲存體帳戶認證之後會通知您。</span><span class="sxs-lookup"><span data-stu-id="cdd36-169">You are notified after the storage account credential is successfully created.</span></span>

5. <span data-ttu-id="cdd36-170">新建立的儲存體帳戶認證會顯示在 [StorSimple 設定裝置管理員服務] 刀鋒視窗的 [儲存體帳戶認證] 下方。</span><span class="sxs-lookup"><span data-stu-id="cdd36-170">The newly created storage account credential is displayed on the StorSimple Configure Device Manager service blade under **Storage account credentials**.</span></span>
   
    ![新增裝置管理員服務訂用帳戶外的 Azure 儲存體帳戶認證](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-outside-storageacct.png)

## <a name="edit-a-storage-account-credential"></a><span data-ttu-id="cdd36-172">編輯儲存體帳戶認證</span><span class="sxs-lookup"><span data-stu-id="cdd36-172">Edit a storage account credential</span></span>
<span data-ttu-id="cdd36-173">您可以編輯裝置所使用的儲存體帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="cdd36-173">You can edit a storage account credential used by your device.</span></span> <span data-ttu-id="cdd36-174">如果您編輯的儲存體帳戶認證目前正在使用中，您就只能修改該儲存體帳戶認證的存取金鑰和 SSL 模式欄位。</span><span class="sxs-lookup"><span data-stu-id="cdd36-174">If you edit a storage account credential that is currently in use, the fields available to modify are the access key and the SSL mode for the storage account credential.</span></span> <span data-ttu-id="cdd36-175">您可以提供新的儲存體存取金鑰，或是修改 [啟用 SSL 模式]  的選取項目，並儲存已更新的設定。</span><span class="sxs-lookup"><span data-stu-id="cdd36-175">You can supply the new storage access key or modify the **Enable SSL mode** selection and save the updated settings.</span></span>

#### <a name="to-edit-a-storage-account-credential"></a><span data-ttu-id="cdd36-176">若要編輯儲存體帳戶認證</span><span class="sxs-lookup"><span data-stu-id="cdd36-176">To edit a storage account credential</span></span>
1. <span data-ttu-id="cdd36-177">瀏覽至您的裝置管理員服務，選取它並按兩下。</span><span class="sxs-lookup"><span data-stu-id="cdd36-177">Navigate to your Device Manager service, select and double-click it.</span></span> <span data-ttu-id="cdd36-178">這會開啟 [概觀] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="cdd36-178">This opens the **Overview** blade.</span></span>
2. <span data-ttu-id="cdd36-179">在 [設定] 區段內選取 [儲存體帳戶認證]。</span><span class="sxs-lookup"><span data-stu-id="cdd36-179">Select **Storage account credentials** within the **Configuration** section.</span></span> <span data-ttu-id="cdd36-180">這樣會列出與 StorSimple 裝置管理員服務相關聯的任何現有儲存體帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="cdd36-180">This lists any existing storage account credentials associated with the StorSimple Device Manager service.</span></span>
3. <span data-ttu-id="cdd36-181">在儲存體帳戶認證的表格式清單中，選取並按兩下您想要修改的帳戶。</span><span class="sxs-lookup"><span data-stu-id="cdd36-181">In the tabular list of storage account credentials, select and double-click the account that you want to modify.</span></span>
4. <span data-ttu-id="cdd36-182">在儲存體帳戶認證的 [屬性] 刀鋒視窗中，執行下列動作︰</span><span class="sxs-lookup"><span data-stu-id="cdd36-182">In the storage account credential **Properties** blade, do the following:</span></span>
   
   1. <span data-ttu-id="cdd36-183">如有必要，您可以修改 [啟用 SSL] 模式選項。</span><span class="sxs-lookup"><span data-stu-id="cdd36-183">If necessary, you can modify the **Enable SSL** mode selection.</span></span>
   2. <span data-ttu-id="cdd36-184">您可以選擇重新產生儲存體帳戶認證的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="cdd36-184">You can choose to regenerate your storage account credential access keys.</span></span> <span data-ttu-id="cdd36-185">如需詳細資訊，請參閱[重新產生儲存體帳戶金鑰](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys)。</span><span class="sxs-lookup"><span data-stu-id="cdd36-185">For more information, see [Regenerate the storage account keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span> <span data-ttu-id="cdd36-186">提供新的儲存體帳戶認證金鑰。</span><span class="sxs-lookup"><span data-stu-id="cdd36-186">Supply the new storage account credential key.</span></span> <span data-ttu-id="cdd36-187">而每個 Azure 儲存體帳戶，都有主要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="cdd36-187">For an Azure storage account, this is the primary access key.</span></span>
   3. <span data-ttu-id="cdd36-188">按一下 [屬性] 刀鋒視窗頂端的 [儲存] 以儲存設定。</span><span class="sxs-lookup"><span data-stu-id="cdd36-188">Click **Save** at the top of the **Properties** blade to save the settings.</span></span> <span data-ttu-id="cdd36-189">[儲存體帳戶認證] 刀鋒視窗上會更新設定。</span><span class="sxs-lookup"><span data-stu-id="cdd36-189">The settings are updated on the **Storage account credentials** blade.</span></span>
      
      ![編輯儲存體帳戶認證](./media/storsimple-virtual-array-manage-storage-accounts/ova-edit-storageacct.png)

## <a name="delete-a-storage-account-credential"></a><span data-ttu-id="cdd36-191">刪除儲存體帳戶認證</span><span class="sxs-lookup"><span data-stu-id="cdd36-191">Delete a storage account credential</span></span>
> [!IMPORTANT]
> <span data-ttu-id="cdd36-192">您只能刪除非使用中的儲存體帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="cdd36-192">You can delete a storage account credential only if it is not in use.</span></span> <span data-ttu-id="cdd36-193">如果您要刪除的儲存體帳戶認證正在使用中，系統會通知您。</span><span class="sxs-lookup"><span data-stu-id="cdd36-193">If a storage account credential is in use, you are notified.</span></span>
> 
> 

#### <a name="to-delete-a-storage-account-credential"></a><span data-ttu-id="cdd36-194">若要刪除儲存體帳戶認證</span><span class="sxs-lookup"><span data-stu-id="cdd36-194">To delete a storage account credential</span></span>
1. <span data-ttu-id="cdd36-195">瀏覽至您的裝置管理員服務，選取它並按兩下。</span><span class="sxs-lookup"><span data-stu-id="cdd36-195">Navigate to your Device Manager service, select and double-click it.</span></span> <span data-ttu-id="cdd36-196">這會開啟 [概觀] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="cdd36-196">This opens the **Overview** blade.</span></span>
2. <span data-ttu-id="cdd36-197">在 [設定] 區段內選取 [儲存體帳戶認證]。</span><span class="sxs-lookup"><span data-stu-id="cdd36-197">Select **Storage account credentials** within the **Configuration** section.</span></span> <span data-ttu-id="cdd36-198">這樣會列出與 StorSimple 裝置管理員服務相關聯的任何現有儲存體帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="cdd36-198">This lists any existing storage account credentials associated with the StorSimple Device Manager service.</span></span>
3. <span data-ttu-id="cdd36-199">在儲存體帳戶認證的表格式清單中，選取並按兩下您想要刪除的帳戶。</span><span class="sxs-lookup"><span data-stu-id="cdd36-199">In the tabular list of storage account credentials, select and double-click the account that you want to delete.</span></span>
4. <span data-ttu-id="cdd36-200">在儲存體帳戶認證的 [屬性] 刀鋒視窗中，執行下列動作︰</span><span class="sxs-lookup"><span data-stu-id="cdd36-200">In the storage account credential **Properties** blade, do the following:</span></span>
   
   1. <span data-ttu-id="cdd36-201">按一下 [刪除]  來刪除認證。</span><span class="sxs-lookup"><span data-stu-id="cdd36-201">Click **Delete** to delete the credentials.</span></span>
   2. <span data-ttu-id="cdd36-202">當系統提示您確認時，按一下 [是]  繼續進行刪除。</span><span class="sxs-lookup"><span data-stu-id="cdd36-202">When prompted for confirmation, click **Yes** to continue with the deletion.</span></span> <span data-ttu-id="cdd36-203">表格式清單會更新以反映變更。</span><span class="sxs-lookup"><span data-stu-id="cdd36-203">The tabular listing is updated to reflect the changes.</span></span>
      
      ![刪除儲存體帳戶認證](./media/storsimple-virtual-array-manage-storage-accounts/ova-del-storageacct.png)

## <a name="synchronizing-storage-account-credential-keys"></a><span data-ttu-id="cdd36-205">同步處理儲存體帳戶認證金鑰</span><span class="sxs-lookup"><span data-stu-id="cdd36-205">Synchronizing storage account credential keys</span></span>
<span data-ttu-id="cdd36-206">基於安全性理由，通常是在資料中心內才需要替換金鑰。</span><span class="sxs-lookup"><span data-stu-id="cdd36-206">For security reasons, key rotation is often a requirement in data centers.</span></span> <span data-ttu-id="cdd36-207">Microsoft Azure 系統管理員可以直接存取儲存體帳戶認證 (透過 Microsoft Azure 儲存體服務)，以重新產生或變更主要金鑰或次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="cdd36-207">A Microsoft Azure administrator can regenerate or change the primary or secondary key by directly accessing the storage account credential (via the Microsoft Azure Storage service).</span></span> <span data-ttu-id="cdd36-208">StorSimple 裝置管理員服務不會自動發現這項變更。</span><span class="sxs-lookup"><span data-stu-id="cdd36-208">The StorSimple Device Manager service does not see this change automatically.</span></span>

<span data-ttu-id="cdd36-209">若要向 StorSimple 裝置管理員服務通知此變更，您需要存取 StorSimple 裝置管理員服務，存取儲存體帳戶認證，然後同步處理主要金鑰或次要金鑰 (根據何者已變更而定)。</span><span class="sxs-lookup"><span data-stu-id="cdd36-209">To inform the StorSimple Device Manager service of the change, you need to access the StorSimple Device Manager service, access the storage account credential, and then synchronize the primary or secondary key (depending on which one was changed).</span></span> <span data-ttu-id="cdd36-210">服務接著會取得最新的金鑰，將金鑰加密，然後將加密的金鑰傳送給裝置。</span><span class="sxs-lookup"><span data-stu-id="cdd36-210">The service then gets the latest key, encrypts the keys, and sends the encrypted key to the device.</span></span>

#### <a name="to-synchronize-keys-for-storage-account-credentials-in-the-same-subscription-as-the-service-azure-only"></a><span data-ttu-id="cdd36-211">若要在相同的服務訂用帳戶中同步處理儲存體帳戶認證的金鑰 (僅限 Azure)</span><span class="sxs-lookup"><span data-stu-id="cdd36-211">To synchronize keys for storage account credentials in the same subscription as the service (Azure only)</span></span>
1. <span data-ttu-id="cdd36-212">在服務登陸刀鋒視窗上，選取您的服務，按兩下服務名稱，然後在 [設定] 區段中按一下 [儲存體帳戶認證]。</span><span class="sxs-lookup"><span data-stu-id="cdd36-212">On the service landing blade, select your service, double-click the service name, and then in the **Configuration** section, click **Storage account credentials**.</span></span>
2. <span data-ttu-id="cdd36-213">在 [儲存體帳戶認證] 刀鋒視窗的儲存體帳戶認證清單中，選取您想要同步處理金鑰的儲存體帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="cdd36-213">On the **Storage account credentials** blade, in the list of Storage account credentials, select the storage account credential whose keys that you want to synchronize.</span></span>
3. <span data-ttu-id="cdd36-214">在所選儲存體帳戶認證的 [屬性] 刀鋒視窗中，執行下列動作︰</span><span class="sxs-lookup"><span data-stu-id="cdd36-214">In the **Properties** blade for the selected storage account credential, do the following:</span></span>
   
    1. <span data-ttu-id="cdd36-215">按一下 [更多]，然後按一下 [同步存取金鑰]。</span><span class="sxs-lookup"><span data-stu-id="cdd36-215">Click **More**, and then click **Sync access key**.</span></span>
   
    2. <span data-ttu-id="cdd36-216">當系統提示您確認時，按一下 [同步金鑰] 完成同步處理。</span><span class="sxs-lookup"><span data-stu-id="cdd36-216">When prompted for confirmation, click **Sync key** to complete the synchronization.</span></span>
    
4. <span data-ttu-id="cdd36-217">在 StorSimple 裝置管理員服務中，您需要更新先前在 Microsoft Azure 儲存體服務中變更的金鑰。</span><span class="sxs-lookup"><span data-stu-id="cdd36-217">In the StorSimple Device Manager service, you need to update the key that was previously changed in the Microsoft Azure Storage service.</span></span> <span data-ttu-id="cdd36-218">在 [同步儲存體帳戶金鑰] 刀鋒視窗中，如果主要存取金鑰已變更 (重新產生)，請按一下 [主要]，然後按一下 [同步金鑰]。</span><span class="sxs-lookup"><span data-stu-id="cdd36-218">In the **Synchronize storage account key** blade, if the primary access key was changed (regenerated), click Primary, and then click **Sync Key**.</span></span> <span data-ttu-id="cdd36-219">如果次要金鑰已變更，請按一下 [次要]，然後按一下 [同步金鑰]。</span><span class="sxs-lookup"><span data-stu-id="cdd36-219">If the secondary key was changed, click **Secondary**, and then click **Sync Key**.</span></span>
   
    ![同步存取金鑰](./media/storsimple-virtual-array-manage-storage-accounts/ova-sync-acess-key.png)

## <a name="next-steps"></a><span data-ttu-id="cdd36-221">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cdd36-221">Next steps</span></span>
* <span data-ttu-id="cdd36-222">了解如何 [管理 StorSimple Virtual Array](storsimple-ova-web-ui-admin.md)。</span><span class="sxs-lookup"><span data-stu-id="cdd36-222">Learn how to [administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

