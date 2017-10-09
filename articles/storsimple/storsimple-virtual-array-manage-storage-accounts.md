---
title: "aaaManage StorSimple Virtual Array 儲存體帳戶認證 |Microsoft 文件"
description: "說明如何使用 hello StorSimple 裝置管理員 設定頁面 tooadd、 編輯、 刪除或旋轉 hello 安全性金鑰 hello StorSimple Virtual Array 相關聯的儲存體帳戶認證。"
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
ms.openlocfilehash: 22a0341eae0b89020065be4dbfaae77999f8be0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-toomanage-storage-account-credentials-for-storsimple-virtual-array"></a><span data-ttu-id="36b23-103">使用 StorSimple 裝置管理員 toomanage StorSimple Virtual Array 的儲存體帳戶認證</span><span class="sxs-lookup"><span data-stu-id="36b23-103">Use StorSimple Device Manager toomanage storage account credentials for StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="36b23-104">概觀</span><span class="sxs-lookup"><span data-stu-id="36b23-104">Overview</span></span>
<span data-ttu-id="36b23-105">hello**組態**hello StorSimple 裝置管理員服務刀鋒視窗，您的 StorSimple Virtual Array 的區段提供可由 hello StorSimple Manager 服務的 hello 全域服務參數。</span><span class="sxs-lookup"><span data-stu-id="36b23-105">hello **Configuration** section of hello StorSimple Device Manager service blade of your StorSimple Virtual Array presents hello global service parameters that can be created in hello StorSimple Manager service.</span></span> <span data-ttu-id="36b23-106">這些參數可以是裝置連線 toohello 服務，並包含套用的 tooall hello:</span><span class="sxs-lookup"><span data-stu-id="36b23-106">These parameters can be applied tooall hello devices connected toohello service, and include:</span></span>

* <span data-ttu-id="36b23-107">儲存體帳戶認證</span><span class="sxs-lookup"><span data-stu-id="36b23-107">Storage account credentials</span></span>
* <span data-ttu-id="36b23-108">存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="36b23-108">Access control records</span></span>
  
  ![裝置管理員服務儀表板](./media/storsimple-virtual-array-manage-storage-accounts/ova-storageaccts-dashboard.png)  

<span data-ttu-id="36b23-110">本教學課程說明如何新增、編輯或刪除 StorSimple Virtual Array 的儲存體帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="36b23-110">This tutorial explains how you can add, edit, or delete storage account credentials for your StorSimple Virtual Array.</span></span> <span data-ttu-id="36b23-111">本教學課程中的 hello 資訊僅適用於 toohello StorSimple Virtual Array。</span><span class="sxs-lookup"><span data-stu-id="36b23-111">hello information in this tutorial only applies toohello StorSimple Virtual Array.</span></span> <span data-ttu-id="36b23-112">如需 toomanage 儲存體帳戶中 8000 系列的如何資訊，請參閱[使用 hello StorSimple Manager 服務 toomanage 儲存體帳戶](storsimple-manage-storage-accounts.md)。</span><span class="sxs-lookup"><span data-stu-id="36b23-112">For information on how toomanage storage accounts in 8000 series, see [Use hello StorSimple Manager service toomanage your storage account](storsimple-manage-storage-accounts.md).</span></span>

<span data-ttu-id="36b23-113">儲存體帳戶認證都包含 hello 裝置 hello 認證使用 tooaccess 儲存體帳戶與您的雲端服務提供者。</span><span class="sxs-lookup"><span data-stu-id="36b23-113">Storage account credentials contain hello credentials that hello device uses tooaccess your storage account with your cloud service provider.</span></span> <span data-ttu-id="36b23-114">Microsoft Azure 儲存體帳戶，這些是認證，例如 hello 帳戶名稱和 hello 主要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="36b23-114">For Microsoft Azure storage accounts, these are credentials such as hello account name and hello primary access key.</span></span>

<span data-ttu-id="36b23-115">在 hello**儲存體帳戶認證**刀鋒視窗中，建立 hello 計費訂用帳戶的認證會包含下列資訊的 hello 以表格格式顯示所有儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="36b23-115">On hello **Storage account credentials** blade, all storage account credentials that are created for hello billing subscription are displayed in a tabular format containing hello following information:</span></span>

* <span data-ttu-id="36b23-116">**名稱**– hello 指派唯一名稱 toohello 帳戶建立時。</span><span class="sxs-lookup"><span data-stu-id="36b23-116">**Name** – hello unique name assigned toohello account when it was created.</span></span>
* <span data-ttu-id="36b23-117">**啟用 SSL** – 是否 hello 啟用 SSL，所以裝置到雲端的通訊都會透過 hello 安全通道。</span><span class="sxs-lookup"><span data-stu-id="36b23-117">**SSL enabled** – Whether hello SSL is enabled and device-to-cloud communication is over hello secure channel.</span></span>
  
  ![[設定] 區段](./media/storsimple-virtual-array-manage-storage-accounts/ova-storageaccountcredentials-blade.png)

<span data-ttu-id="36b23-119">hello 最常見的工作相關 toostorage 帳戶認證，可對 hello**儲存體帳戶認證**刀鋒視窗會：</span><span class="sxs-lookup"><span data-stu-id="36b23-119">hello most common tasks related toostorage account credentials that can be performed on hello **Storage account credentials** blade are:</span></span>

* <span data-ttu-id="36b23-120">新增儲存體帳戶認證</span><span class="sxs-lookup"><span data-stu-id="36b23-120">Add a storage account credential</span></span>
* <span data-ttu-id="36b23-121">編輯儲存體帳戶認證</span><span class="sxs-lookup"><span data-stu-id="36b23-121">Edit a storage account credential</span></span>
* <span data-ttu-id="36b23-122">刪除儲存體帳戶認證</span><span class="sxs-lookup"><span data-stu-id="36b23-122">Delete a storage account credential</span></span>

## <a name="types-of-storage-account-credentials"></a><span data-ttu-id="36b23-123">儲存體帳戶認證的類型</span><span class="sxs-lookup"><span data-stu-id="36b23-123">Types of storage account credentials</span></span>
<span data-ttu-id="36b23-124">有三種儲存體帳戶認證類型可以與 StorSimple 裝置搭配使用。</span><span class="sxs-lookup"><span data-stu-id="36b23-124">There are three types of storage account credentials that can be used with your StorSimple device.</span></span>

* <span data-ttu-id="36b23-125">**自動產生的儲存體帳戶認證**– 第一次建立 hello 服務時，就 hello 名所示，自動產生這種類型的儲存體帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="36b23-125">**Auto-generated storage account credentials** – As hello name suggests, this type of storage account credential is automatically generated when hello service is first created.</span></span> <span data-ttu-id="36b23-126">toolearn 深入了解如何建立這個儲存體帳戶認證，請參閱[建立新的服務](storsimple-virtual-array-manage-service.md#create-a-service)。</span><span class="sxs-lookup"><span data-stu-id="36b23-126">toolearn more about how this storage account credential is created, see [Create a new service](storsimple-virtual-array-manage-service.md#create-a-service).</span></span>
* <span data-ttu-id="36b23-127">**hello 服務訂用帳戶中的儲存體帳戶認證**– 這些是 hello Azure 儲存體帳戶相關聯的認證 hello 相同訂用帳戶的 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="36b23-127">**storage account credentials in hello service subscription** – These are hello Azure storage account credentials that are associated with hello same subscription as that of hello service.</span></span> <span data-ttu-id="36b23-128">toolearn 深入了解如何建立這些儲存體帳戶認證，請參閱[關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="36b23-128">toolearn more about how these storage account credentials are created, see [About Azure Storage Accounts](../storage/common/storage-create-storage-account.md).</span></span>
* <span data-ttu-id="36b23-129">**hello 服務訂用帳戶以外的儲存體帳戶認證**-這些是與您的服務沒有關聯的 hello Azure 儲存體帳戶認證，並可能存在於之前 hello 服務已建立。</span><span class="sxs-lookup"><span data-stu-id="36b23-129">**storage account credentials outside of hello service subscription** – These are hello Azure storage account credentials that are not associated with your service and likely existed before hello service was created.</span></span>

## <a name="add-a-storage-account-credential"></a><span data-ttu-id="36b23-130">新增儲存體帳戶認證</span><span class="sxs-lookup"><span data-stu-id="36b23-130">Add a storage account credential</span></span>
<span data-ttu-id="36b23-131">您可以加入儲存體帳戶認證 tooyour StorSimple 裝置管理員服務組態，藉由提供唯一的易記名稱和存取認證連結 toohello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="36b23-131">You can add a storage account credential tooyour StorSimple Device Manager service configuration by providing a unique friendly name and access credentials that are linked toohello storage account.</span></span> <span data-ttu-id="36b23-132">您也可以啟用您的裝置與 hello 雲端之間的網路通訊的安全通道 hello 安全通訊端層 (SSL) 模式 toocreate hello 選項。</span><span class="sxs-lookup"><span data-stu-id="36b23-132">You also have hello option of enabling hello secure sockets layer (SSL) mode toocreate a secure channel for network communication between your device and hello cloud.</span></span>

<span data-ttu-id="36b23-133">您可以為指定的雲端服務提供者建立多個帳戶。</span><span class="sxs-lookup"><span data-stu-id="36b23-133">You can create multiple accounts for a given cloud service provider.</span></span> <span data-ttu-id="36b23-134">正在儲存 hello 儲存體帳戶認證，而 hello 服務會嘗試 toocommunicate 與您的雲端服務提供者。</span><span class="sxs-lookup"><span data-stu-id="36b23-134">While hello storage account credential is being saved, hello service attempts toocommunicate with your cloud service provider.</span></span> <span data-ttu-id="36b23-135">此時會進行驗證 hello 認證和您所提供的 hello 存取資料。</span><span class="sxs-lookup"><span data-stu-id="36b23-135">hello credentials and hello access material that you supplied are authenticated at this time.</span></span> <span data-ttu-id="36b23-136">只有當 hello 驗證成功時，會建立儲存體帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="36b23-136">A storage account credential is created only if hello authentication succeeds.</span></span> <span data-ttu-id="36b23-137">Hello 驗證失敗時，會顯示適當的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="36b23-137">If hello authentication fails, then an appropriate error message is displayed.</span></span>

<span data-ttu-id="36b23-138">使用下列程序 tooadd Azure 儲存體帳戶認證的 hello:</span><span class="sxs-lookup"><span data-stu-id="36b23-138">Use hello following procedures tooadd Azure storage account credentials:</span></span>

* <span data-ttu-id="36b23-139">儲存體帳戶認證具有 tooadd hello 相同 Azure 訂用帳戶 hello 裝置管理員服務</span><span class="sxs-lookup"><span data-stu-id="36b23-139">tooadd a storage account credential that has hello same Azure subscription as hello Device Manager service</span></span>
* <span data-ttu-id="36b23-140">tooadd 超出 hello 裝置管理員服務訂用帳戶的 Azure 儲存體帳戶認證</span><span class="sxs-lookup"><span data-stu-id="36b23-140">tooadd an Azure storage account credential that is outside of hello Device Manager service subscription</span></span>

#### <a name="tooadd-a-storage-account-credential-that-has-hello-same-azure-subscription-as-hello-device-manager-service"></a><span data-ttu-id="36b23-141">儲存體帳戶認證具有 tooadd hello 相同 Azure 訂用帳戶 hello 裝置管理員服務</span><span class="sxs-lookup"><span data-stu-id="36b23-141">tooadd a storage account credential that has hello same Azure subscription as hello Device Manager service</span></span>

1. <span data-ttu-id="36b23-142">瀏覽 tooyour 裝置管理員服務，選取，然後按兩下。</span><span class="sxs-lookup"><span data-stu-id="36b23-142">Navigate tooyour Device Manager service, select and double-click it.</span></span> <span data-ttu-id="36b23-143">這會開啟 hello**概觀**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="36b23-143">This opens hello **Overview** blade.</span></span>
2. <span data-ttu-id="36b23-144">選取**儲存體帳戶認證**內 hello**組態**> 一節。</span><span class="sxs-lookup"><span data-stu-id="36b23-144">Select **Storage account credentials** within hello **Configuration** section.</span></span>
3. <span data-ttu-id="36b23-145">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="36b23-145">Click **Add**.</span></span>
4. <span data-ttu-id="36b23-146">在 hello**加入儲存體帳戶**刀鋒視窗中，請勿遵循 hello:</span><span class="sxs-lookup"><span data-stu-id="36b23-146">In hello **Add a storage account** blade, do hello following:</span></span>
   
    1. <span data-ttu-id="36b23-147">在 [訂用帳戶] 中，選取 [目前]。</span><span class="sxs-lookup"><span data-stu-id="36b23-147">For **Subscription**, select **Current**.</span></span>
    2. <span data-ttu-id="36b23-148">提供 hello Azure 儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="36b23-148">Provide hello name of your Azure storage account.</span></span>
    3. <span data-ttu-id="36b23-149">選取**啟用**toocreate StorSimple 裝置與 hello 雲端之間的網路通訊的安全通道。</span><span class="sxs-lookup"><span data-stu-id="36b23-149">Select **Enable** toocreate a secure channel for network communication between your StorSimple device and hello cloud.</span></span> <span data-ttu-id="36b23-150">只有當您在私人雲端內操作時，才選取 [停用]。</span><span class="sxs-lookup"><span data-stu-id="36b23-150">Select **Disable** only if you are operating within a private cloud.</span></span>
    4. <span data-ttu-id="36b23-151">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="36b23-151">Click **Add**.</span></span> <span data-ttu-id="36b23-152">已成功建立 hello 儲存體帳戶之後，您會收到通知。</span><span class="sxs-lookup"><span data-stu-id="36b23-152">You are notified after hello storage account is successfully created.</span></span><br></br>
   
        ![新增現有儲存體帳戶認證](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-storageacct.png)

#### <a name="tooadd-an-azure-storage-account-credential-that-is-outside-of-hello-device-manager-service-subscription"></a><span data-ttu-id="36b23-154">tooadd 超出 hello 裝置管理員服務訂用帳戶的 Azure 儲存體帳戶認證</span><span class="sxs-lookup"><span data-stu-id="36b23-154">tooadd an Azure storage account credential that is outside of hello Device Manager service subscription</span></span>

1. <span data-ttu-id="36b23-155">瀏覽 tooyour 裝置管理員服務，選取，然後按兩下。</span><span class="sxs-lookup"><span data-stu-id="36b23-155">Navigate tooyour Device Manager service, select and double-click it.</span></span> <span data-ttu-id="36b23-156">這會開啟 hello**概觀**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="36b23-156">This opens hello **Overview** blade.</span></span>
2. <span data-ttu-id="36b23-157">選取**儲存體帳戶認證**內 hello**組態**> 一節。</span><span class="sxs-lookup"><span data-stu-id="36b23-157">Select **Storage account credentials** within hello **Configuration** section.</span></span> <span data-ttu-id="36b23-158">這樣就會列出任何現有儲存體帳戶的認證與 hello StorSimple 裝置管理員服務相關聯。</span><span class="sxs-lookup"><span data-stu-id="36b23-158">This lists any existing storage account credentials associated with hello StorSimple Device Manager service.</span></span>
3. <span data-ttu-id="36b23-159">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="36b23-159">Click **Add**.</span></span>
4. <span data-ttu-id="36b23-160">在 hello**加入儲存體帳戶**刀鋒視窗中，請勿遵循 hello:</span><span class="sxs-lookup"><span data-stu-id="36b23-160">In hello **Add a storage account** blade, do hello following:</span></span>
   
    1. <span data-ttu-id="36b23-161">在 [訂用帳戶] 中，選取 [其他]。</span><span class="sxs-lookup"><span data-stu-id="36b23-161">For **Subscription**, select **Other**.</span></span>
   
    2. <span data-ttu-id="36b23-162">提供您的 Azure 儲存體帳戶認證 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="36b23-162">Provide hello name of your Azure storage account credential.</span></span>
   
    3. <span data-ttu-id="36b23-163">在 [hello**儲存體帳戶存取金鑰**] 文字方塊中，提供 hello 您的 Azure 儲存體帳戶認證的主要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="36b23-163">In hello **Storage account access key** text box, supply hello primary Access Key for your Azure storage account credential.</span></span> <span data-ttu-id="36b23-164">tooget 此索引鍵，移 toohello Azure 儲存體服務，選取您的儲存體帳戶認證，然後按一下**管理的帳戶金鑰**。</span><span class="sxs-lookup"><span data-stu-id="36b23-164">tooget this key, go toohello Azure Storage service, select your storage account credential, and click **Manage account keys**.</span></span> <span data-ttu-id="36b23-165">您現在可以複製 hello 主要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="36b23-165">You can now copy hello primary access key.</span></span>
   
    4. <span data-ttu-id="36b23-166">tooenable SSL，按一下 hello**啟用**按鈕 toocreate StorSimple 裝置管理員服務和 hello 雲端之間的網路通訊的安全通道。</span><span class="sxs-lookup"><span data-stu-id="36b23-166">tooenable SSL, click hello **Enable** button toocreate a secure channel for network communication between your StorSimple Device Manager service and hello cloud.</span></span> <span data-ttu-id="36b23-167">按一下 hello**停用**按鈕只有當您在私人雲端內操作。</span><span class="sxs-lookup"><span data-stu-id="36b23-167">Click hello **Disable** button only if you are operating within a private cloud.</span></span>
   
    5. <span data-ttu-id="36b23-168">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="36b23-168">Click **Add**.</span></span> <span data-ttu-id="36b23-169">已成功建立 hello 儲存體帳戶認證之後，您會收到通知。</span><span class="sxs-lookup"><span data-stu-id="36b23-169">You are notified after hello storage account credential is successfully created.</span></span>

5. <span data-ttu-id="36b23-170">底下的 hello StorSimple 設定裝置管理員服務刀鋒視窗上會顯示 hello 新建立的儲存體帳戶認證**儲存體帳戶認證**。</span><span class="sxs-lookup"><span data-stu-id="36b23-170">hello newly created storage account credential is displayed on hello StorSimple Configure Device Manager service blade under **Storage account credentials**.</span></span>
   
    ![新增外部 hello 裝置管理員服務訂用帳戶的儲存體帳戶認證](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-outside-storageacct.png)

## <a name="edit-a-storage-account-credential"></a><span data-ttu-id="36b23-172">編輯儲存體帳戶認證</span><span class="sxs-lookup"><span data-stu-id="36b23-172">Edit a storage account credential</span></span>
<span data-ttu-id="36b23-173">您可以編輯裝置所使用的儲存體帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="36b23-173">You can edit a storage account credential used by your device.</span></span> <span data-ttu-id="36b23-174">如果您編輯目前正在使用儲存體帳戶認證，hello 欄位可用 toomodify 而 hello 便捷鍵 hello 儲存體帳戶認證的 hello SSL 模式。</span><span class="sxs-lookup"><span data-stu-id="36b23-174">If you edit a storage account credential that is currently in use, hello fields available toomodify are hello access key and hello SSL mode for hello storage account credential.</span></span> <span data-ttu-id="36b23-175">您可以提供 hello 新儲存體存取金鑰，或修改 hello**啟用 SSL 模式**選取項目並儲存更新的 hello 的設定。</span><span class="sxs-lookup"><span data-stu-id="36b23-175">You can supply hello new storage access key or modify hello **Enable SSL mode** selection and save hello updated settings.</span></span>

#### <a name="tooedit-a-storage-account-credential"></a><span data-ttu-id="36b23-176">tooedit 儲存體帳戶認證</span><span class="sxs-lookup"><span data-stu-id="36b23-176">tooedit a storage account credential</span></span>
1. <span data-ttu-id="36b23-177">瀏覽 tooyour 裝置管理員服務，選取，然後按兩下。</span><span class="sxs-lookup"><span data-stu-id="36b23-177">Navigate tooyour Device Manager service, select and double-click it.</span></span> <span data-ttu-id="36b23-178">這會開啟 hello**概觀**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="36b23-178">This opens hello **Overview** blade.</span></span>
2. <span data-ttu-id="36b23-179">選取**儲存體帳戶認證**內 hello**組態**> 一節。</span><span class="sxs-lookup"><span data-stu-id="36b23-179">Select **Storage account credentials** within hello **Configuration** section.</span></span> <span data-ttu-id="36b23-180">這樣就會列出任何現有儲存體帳戶的認證與 hello StorSimple 裝置管理員服務相關聯。</span><span class="sxs-lookup"><span data-stu-id="36b23-180">This lists any existing storage account credentials associated with hello StorSimple Device Manager service.</span></span>
3. <span data-ttu-id="36b23-181">在 hello 表格式清單中的儲存體帳戶認證，請選取，然後按兩下您想 toomodify hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="36b23-181">In hello tabular list of storage account credentials, select and double-click hello account that you want toomodify.</span></span>
4. <span data-ttu-id="36b23-182">在 hello 儲存體帳戶認證**屬性**刀鋒視窗中，請勿遵循 hello:</span><span class="sxs-lookup"><span data-stu-id="36b23-182">In hello storage account credential **Properties** blade, do hello following:</span></span>
   
   1. <span data-ttu-id="36b23-183">如果有必要，您可以修改 hello**啟用 SSL**模式選取項目。</span><span class="sxs-lookup"><span data-stu-id="36b23-183">If necessary, you can modify hello **Enable SSL** mode selection.</span></span>
   2. <span data-ttu-id="36b23-184">您可以選擇 tooregenerate 儲存體帳戶認證的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="36b23-184">You can choose tooregenerate your storage account credential access keys.</span></span> <span data-ttu-id="36b23-185">如需詳細資訊，請參閱[hello 儲存體帳戶金鑰重新產生](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys)。</span><span class="sxs-lookup"><span data-stu-id="36b23-185">For more information, see [Regenerate hello storage account keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span> <span data-ttu-id="36b23-186">提供 hello 新儲存體帳戶認證金鑰。</span><span class="sxs-lookup"><span data-stu-id="36b23-186">Supply hello new storage account credential key.</span></span> <span data-ttu-id="36b23-187">Azure 儲存體帳戶時，這是 hello 主要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="36b23-187">For an Azure storage account, this is hello primary access key.</span></span>
   3. <span data-ttu-id="36b23-188">按一下**儲存**頂端的 hello hello**屬性**刀鋒視窗 toosave hello 設定。</span><span class="sxs-lookup"><span data-stu-id="36b23-188">Click **Save** at hello top of hello **Properties** blade toosave hello settings.</span></span> <span data-ttu-id="36b23-189">hello 設定會更新在 hello**儲存體帳戶認證**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="36b23-189">hello settings are updated on hello **Storage account credentials** blade.</span></span>
      
      ![編輯儲存體帳戶認證](./media/storsimple-virtual-array-manage-storage-accounts/ova-edit-storageacct.png)

## <a name="delete-a-storage-account-credential"></a><span data-ttu-id="36b23-191">刪除儲存體帳戶認證</span><span class="sxs-lookup"><span data-stu-id="36b23-191">Delete a storage account credential</span></span>
> [!IMPORTANT]
> <span data-ttu-id="36b23-192">您只能刪除非使用中的儲存體帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="36b23-192">You can delete a storage account credential only if it is not in use.</span></span> <span data-ttu-id="36b23-193">如果您要刪除的儲存體帳戶認證正在使用中，系統會通知您。</span><span class="sxs-lookup"><span data-stu-id="36b23-193">If a storage account credential is in use, you are notified.</span></span>
> 
> 

#### <a name="toodelete-a-storage-account-credential"></a><span data-ttu-id="36b23-194">toodelete 儲存體帳戶認證</span><span class="sxs-lookup"><span data-stu-id="36b23-194">toodelete a storage account credential</span></span>
1. <span data-ttu-id="36b23-195">瀏覽 tooyour 裝置管理員服務，選取，然後按兩下。</span><span class="sxs-lookup"><span data-stu-id="36b23-195">Navigate tooyour Device Manager service, select and double-click it.</span></span> <span data-ttu-id="36b23-196">這會開啟 hello**概觀**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="36b23-196">This opens hello **Overview** blade.</span></span>
2. <span data-ttu-id="36b23-197">選取**儲存體帳戶認證**內 hello**組態**> 一節。</span><span class="sxs-lookup"><span data-stu-id="36b23-197">Select **Storage account credentials** within hello **Configuration** section.</span></span> <span data-ttu-id="36b23-198">這樣就會列出任何現有儲存體帳戶的認證與 hello StorSimple 裝置管理員服務相關聯。</span><span class="sxs-lookup"><span data-stu-id="36b23-198">This lists any existing storage account credentials associated with hello StorSimple Device Manager service.</span></span>
3. <span data-ttu-id="36b23-199">在 hello 表格式清單中的儲存體帳戶認證，請選取，然後按兩下您想 toodelete hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="36b23-199">In hello tabular list of storage account credentials, select and double-click hello account that you want toodelete.</span></span>
4. <span data-ttu-id="36b23-200">在 hello 儲存體帳戶認證**屬性**刀鋒視窗中，請勿遵循 hello:</span><span class="sxs-lookup"><span data-stu-id="36b23-200">In hello storage account credential **Properties** blade, do hello following:</span></span>
   
   1. <span data-ttu-id="36b23-201">按一下**刪除**toodelete hello 認證。</span><span class="sxs-lookup"><span data-stu-id="36b23-201">Click **Delete** toodelete hello credentials.</span></span>
   2. <span data-ttu-id="36b23-202">當提示確認，請按一下**是**toocontinue 與 hello 刪除。</span><span class="sxs-lookup"><span data-stu-id="36b23-202">When prompted for confirmation, click **Yes** toocontinue with hello deletion.</span></span> <span data-ttu-id="36b23-203">hello 表格清單已更新的 tooreflect hello 變更。</span><span class="sxs-lookup"><span data-stu-id="36b23-203">hello tabular listing is updated tooreflect hello changes.</span></span>
      
      ![刪除儲存體帳戶認證](./media/storsimple-virtual-array-manage-storage-accounts/ova-del-storageacct.png)

## <a name="synchronizing-storage-account-credential-keys"></a><span data-ttu-id="36b23-205">同步處理儲存體帳戶認證金鑰</span><span class="sxs-lookup"><span data-stu-id="36b23-205">Synchronizing storage account credential keys</span></span>
<span data-ttu-id="36b23-206">基於安全性理由，通常是在資料中心內才需要替換金鑰。</span><span class="sxs-lookup"><span data-stu-id="36b23-206">For security reasons, key rotation is often a requirement in data centers.</span></span> <span data-ttu-id="36b23-207">Microsoft Azure 系統管理員可以重新產生，或直接存取 hello 儲存體帳戶認證 （透過 hello Microsoft Azure 儲存體服務)，以變更 hello 主要或次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="36b23-207">A Microsoft Azure administrator can regenerate or change hello primary or secondary key by directly accessing hello storage account credential (via hello Microsoft Azure Storage service).</span></span> <span data-ttu-id="36b23-208">hello StorSimple 裝置 Manager 服務不會自動看到這項變更。</span><span class="sxs-lookup"><span data-stu-id="36b23-208">hello StorSimple Device Manager service does not see this change automatically.</span></span>

<span data-ttu-id="36b23-209">tooinform hello StorSimple 裝置管理員 hello 變更的服務，您需要 tooaccess hello StorSimple 裝置管理員服務，存取 hello 儲存體帳戶認證，然後再同步處理 hello 主要或次要金鑰 （視何者有所變更）。</span><span class="sxs-lookup"><span data-stu-id="36b23-209">tooinform hello StorSimple Device Manager service of hello change, you need tooaccess hello StorSimple Device Manager service, access hello storage account credential, and then synchronize hello primary or secondary key (depending on which one was changed).</span></span> <span data-ttu-id="36b23-210">hello 服務然後取得 hello 最新的金鑰，加密 hello 金鑰，並傳送嗨加密金鑰 toohello 的裝置。</span><span class="sxs-lookup"><span data-stu-id="36b23-210">hello service then gets hello latest key, encrypts hello keys, and sends hello encrypted key toohello device.</span></span>

#### <a name="toosynchronize-keys-for-storage-account-credentials-in-hello-same-subscription-as-hello-service-azure-only"></a><span data-ttu-id="36b23-211">中的儲存體帳戶認證的 toosynchronize 金鑰 hello hello 服務 (僅限 Azure) 相同訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="36b23-211">toosynchronize keys for storage account credentials in hello same subscription as hello service (Azure only)</span></span>
1. <span data-ttu-id="36b23-212">在 hello 服務登陸刀鋒視窗中，選取您的服務、 按兩下 hello 服務名稱，然後在 hello**組態**區段中，按一下**儲存體帳戶認證**。</span><span class="sxs-lookup"><span data-stu-id="36b23-212">On hello service landing blade, select your service, double-click hello service name, and then in hello **Configuration** section, click **Storage account credentials**.</span></span>
2. <span data-ttu-id="36b23-213">在 hello**儲存體帳戶認證**刀鋒視窗中，在 hello 清單中的儲存體帳戶認證，選取 hello 儲存體帳戶認證的 toosynchronize 之索引鍵。</span><span class="sxs-lookup"><span data-stu-id="36b23-213">On hello **Storage account credentials** blade, in hello list of Storage account credentials, select hello storage account credential whose keys that you want toosynchronize.</span></span>
3. <span data-ttu-id="36b23-214">在 hello**屬性**hello 刀鋒視窗選取儲存體帳戶認證，請勿遵循 hello:</span><span class="sxs-lookup"><span data-stu-id="36b23-214">In hello **Properties** blade for hello selected storage account credential, do hello following:</span></span>
   
    1. <span data-ttu-id="36b23-215">按一下 更多，然後按一下同步存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="36b23-215">Click **More**, and then click **Sync access key**.</span></span>
   
    2. <span data-ttu-id="36b23-216">當提示確認，請按一下**同步處理金鑰**toocomplete hello 同步處理。</span><span class="sxs-lookup"><span data-stu-id="36b23-216">When prompted for confirmation, click **Sync key** toocomplete hello synchronization.</span></span>
    
4. <span data-ttu-id="36b23-217">在 hello StorSimple 裝置管理員服務，您會需要 tooupdate hello 金鑰先前已在 hello Microsoft Azure 儲存體服務中變更。</span><span class="sxs-lookup"><span data-stu-id="36b23-217">In hello StorSimple Device Manager service, you need tooupdate hello key that was previously changed in hello Microsoft Azure Storage service.</span></span> <span data-ttu-id="36b23-218">在 hello**同步處理儲存體帳戶金鑰**刀鋒視窗中，如果 hello 主要存取金鑰已變更 （重新產生），按一下 主要伺服器上，然後再按一下**同步處理金鑰**。</span><span class="sxs-lookup"><span data-stu-id="36b23-218">In hello **Synchronize storage account key** blade, if hello primary access key was changed (regenerated), click Primary, and then click **Sync Key**.</span></span> <span data-ttu-id="36b23-219">如果 hello 次要索引鍵已變更，請按一下**次要**，然後按一下**同步處理金鑰**。</span><span class="sxs-lookup"><span data-stu-id="36b23-219">If hello secondary key was changed, click **Secondary**, and then click **Sync Key**.</span></span>
   
    ![同步存取金鑰](./media/storsimple-virtual-array-manage-storage-accounts/ova-sync-acess-key.png)

## <a name="next-steps"></a><span data-ttu-id="36b23-221">後續步驟</span><span class="sxs-lookup"><span data-stu-id="36b23-221">Next steps</span></span>
* <span data-ttu-id="36b23-222">了解如何太[管理您的 StorSimple Virtual Array](storsimple-ova-web-ui-admin.md)。</span><span class="sxs-lookup"><span data-stu-id="36b23-222">Learn how too[administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

