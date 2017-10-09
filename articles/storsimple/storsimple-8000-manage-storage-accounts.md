---
title: "您的 StorSimple 儲存體帳戶認證的 Microsoft Azure StorSimple 8000 系列裝置的 aaaManage |Microsoft 文件"
description: "說明如何使用 hello StorSimple 裝置管理員 設定頁面 tooadd、 編輯、 刪除或旋轉 hello 安全性金鑰的儲存體帳戶。"
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
ms.openlocfilehash: 132ee46509b39db4d1b97b0f1077800a253e8da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-your-storage-account-credentials"></a><span data-ttu-id="553ad-103">使用 hello StorSimple 裝置管理員服務 toomanage 儲存體帳戶認證</span><span class="sxs-lookup"><span data-stu-id="553ad-103">Use hello StorSimple Device Manager service toomanage your storage account credentials</span></span>

## <a name="overview"></a><span data-ttu-id="553ad-104">概觀</span><span class="sxs-lookup"><span data-stu-id="553ad-104">Overview</span></span>

<span data-ttu-id="553ad-105">hello**組態**hello StorSimple 裝置管理員服務刀鋒視窗中的區段會顯示所有可由 hello StorSimple 裝置管理員服務的 hello 全域服務參數。</span><span class="sxs-lookup"><span data-stu-id="553ad-105">hello **Configuration** section in hello StorSimple Device Manager service blade presents all hello global service parameters that can be created in hello StorSimple Device Manager service.</span></span> <span data-ttu-id="553ad-106">這些參數可以是裝置連線 toohello 服務，並包含套用的 tooall hello:</span><span class="sxs-lookup"><span data-stu-id="553ad-106">These parameters can be applied tooall hello devices connected toohello service, and include:</span></span>

* <span data-ttu-id="553ad-107">儲存體帳戶認證</span><span class="sxs-lookup"><span data-stu-id="553ad-107">Storage account credentials</span></span>
* <span data-ttu-id="553ad-108">頻寬範本</span><span class="sxs-lookup"><span data-stu-id="553ad-108">Bandwidth templates</span></span> 
* <span data-ttu-id="553ad-109">存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="553ad-109">Access control records</span></span> 

<span data-ttu-id="553ad-110">本教學課程說明 tooadd，編輯或刪除儲存體帳戶認證，或旋轉 hello 儲存體帳戶的安全性金鑰的方式。</span><span class="sxs-lookup"><span data-stu-id="553ad-110">This tutorial explains how tooadd, edit, or delete storage account credentials, or rotate hello security keys for a storage account.</span></span>

 ![儲存體帳戶認證的清單](./media/storsimple-8000-manage-storage-accounts/createnewstorageacct6.png)  

<span data-ttu-id="553ad-112">儲存體帳戶包含 hello hello StorSimple 裝置會使用 tooaccess 與您的雲端服務提供者的儲存體帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="553ad-112">Storage accounts contain hello credentials that hello StorSimple device uses tooaccess your storage account with your cloud service provider.</span></span> <span data-ttu-id="553ad-113">Microsoft Azure 儲存體帳戶，這些是認證，例如 hello 帳戶名稱和 hello 主要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="553ad-113">For Microsoft Azure storage accounts, these are credentials such as hello account name and hello primary access key.</span></span> 

<span data-ttu-id="553ad-114">在 hello**儲存體帳戶認證**刀鋒視窗中，建立 hello 計費訂用帳戶的帳戶會包含下列資訊的 hello 以表格格式顯示所有存放裝置：</span><span class="sxs-lookup"><span data-stu-id="553ad-114">On hello **Storage account credentials** blade, all storage accounts that are created for hello billing subscription are displayed in a tabular format containing hello following information:</span></span>

* <span data-ttu-id="553ad-115">**名稱**– hello 指派唯一名稱 toohello 帳戶建立時。</span><span class="sxs-lookup"><span data-stu-id="553ad-115">**Name** – hello unique name assigned toohello account when it was created.</span></span>
* <span data-ttu-id="553ad-116">**啟用 SSL** – 是否 hello 啟用 SSL，所以裝置到雲端的通訊都會透過 hello 安全通道。</span><span class="sxs-lookup"><span data-stu-id="553ad-116">**SSL enabled** – Whether hello SSL is enabled and device-to-cloud communication is over hello secure channel.</span></span>
* <span data-ttu-id="553ad-117">**使用**– hello 使用 hello 儲存體帳戶的磁碟區數目。</span><span class="sxs-lookup"><span data-stu-id="553ad-117">**Used by** – hello number of volumes using hello storage account.</span></span>

<span data-ttu-id="553ad-118">您可以執行的 hello 最常見的工作相關的 toostorage 帳戶是：</span><span class="sxs-lookup"><span data-stu-id="553ad-118">hello most common tasks related toostorage accounts that can be performed are:</span></span>

* <span data-ttu-id="553ad-119">新增儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="553ad-119">Add a storage account</span></span> 
* <span data-ttu-id="553ad-120">編輯儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="553ad-120">Edit a storage account</span></span> 
* <span data-ttu-id="553ad-121">刪除儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="553ad-121">Delete a storage account</span></span> 
* <span data-ttu-id="553ad-122">替換儲存體帳戶的金鑰</span><span class="sxs-lookup"><span data-stu-id="553ad-122">Key rotation of storage accounts</span></span> 

## <a name="types-of-storage-accounts"></a><span data-ttu-id="553ad-123">儲存體帳戶類型</span><span class="sxs-lookup"><span data-stu-id="553ad-123">Types of storage accounts</span></span>

<span data-ttu-id="553ad-124">有三種儲存體帳戶類型能與 StorSimple 裝置搭配使用。</span><span class="sxs-lookup"><span data-stu-id="553ad-124">There are three types of storage accounts that can be used with your StorSimple device.</span></span>

* <span data-ttu-id="553ad-125">**自動產生的儲存體帳戶**– 第一次建立 hello 服務時，就 hello 名所示，自動產生這種類型的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="553ad-125">**Auto-generated storage accounts** – As hello name suggests, this type of storage account is automatically generated when hello service is first created.</span></span> <span data-ttu-id="553ad-126">toolearn 深入了解如何建立這個儲存體帳戶，請參閱[步驟 1： 建立新的服務](storsimple-8000-deployment-walkthrough-u2.md#step-1-create-a-new-service)中[部署在內部部署 StorSimple 裝置](storsimple-8000-deployment-walkthrough-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="553ad-126">toolearn more about how this storage account is created, see [Step 1: Create a new service](storsimple-8000-deployment-walkthrough-u2.md#step-1-create-a-new-service) in [Deploy your on-premises StorSimple device](storsimple-8000-deployment-walkthrough-u2.md).</span></span> 
* <span data-ttu-id="553ad-127">**Hello 服務訂用帳戶中的儲存體帳戶**– 這些是 hello hello 與相關聯的 Azure 儲存體帳戶相同的訂用帳戶 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="553ad-127">**Storage accounts in hello service subscription** – These are hello Azure storage accounts that are associated with hello same subscription as that of hello service.</span></span> <span data-ttu-id="553ad-128">toolearn 深入了解如何建立儲存體帳戶，請參閱[關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="553ad-128">toolearn more about how these storage accounts are created, see [About Azure Storage Accounts](../storage/common/storage-create-storage-account.md).</span></span> 
* <span data-ttu-id="553ad-129">**Hello 服務訂用帳戶以外的儲存體帳戶**-這些是與您的服務沒有關聯的 hello Azure 儲存體帳戶，並可能存在於之前 hello 服務已建立。</span><span class="sxs-lookup"><span data-stu-id="553ad-129">**Storage accounts outside of hello service subscription** – These are hello Azure storage accounts that are not associated with your service and likely existed before hello service was created.</span></span>

## <a name="add-a-storage-account"></a><span data-ttu-id="553ad-130">新增儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="553ad-130">Add a storage account</span></span>

<span data-ttu-id="553ad-131">您可以新增儲存體帳戶提供唯一的易記名稱和存取認證連結 toohello 儲存體帳戶 （與 hello 指定的雲端服務提供者）。</span><span class="sxs-lookup"><span data-stu-id="553ad-131">You can add a storage account by providing a unique friendly name and access credentials that are linked toohello storage account (with hello specified cloud service provider).</span></span> <span data-ttu-id="553ad-132">您也可以啟用您的裝置與 hello 雲端之間的網路通訊的安全通道 hello 安全通訊端層 (SSL) 模式 toocreate hello 選項。</span><span class="sxs-lookup"><span data-stu-id="553ad-132">You also have hello option of enabling hello secure sockets layer (SSL) mode toocreate a secure channel for network communication between your device and hello cloud.</span></span>

<span data-ttu-id="553ad-133">您可以為指定的雲端服務提供者建立多個帳戶。</span><span class="sxs-lookup"><span data-stu-id="553ad-133">You can create multiple accounts for a given cloud service provider.</span></span> <span data-ttu-id="553ad-134">不過，請注意，建立儲存體帳戶之後，您無法變更 hello 雲端服務提供者。</span><span class="sxs-lookup"><span data-stu-id="553ad-134">Be aware, however, that after a storage account is created, you cannot change hello cloud service provider.</span></span>

<span data-ttu-id="553ad-135">正在儲存 hello 儲存體帳戶，而 hello 服務會嘗試 toocommunicate 與您的雲端服務提供者。</span><span class="sxs-lookup"><span data-stu-id="553ad-135">While hello storage account is being saved, hello service attempts toocommunicate with your cloud service provider.</span></span> <span data-ttu-id="553ad-136">在這個階段，將會驗證 hello 認證和您所提供的 hello 存取資料。</span><span class="sxs-lookup"><span data-stu-id="553ad-136">hello credentials and hello access material that you supplied will be authenticated at this time.</span></span> <span data-ttu-id="553ad-137">只有在 hello 驗證成功時，會建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="553ad-137">A storage account is created only if hello authentication succeeds.</span></span> <span data-ttu-id="553ad-138">如果 hello 驗證失敗，將顯示適當的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="553ad-138">If hello authentication fails, then an appropriate error message will be displayed.</span></span>

<span data-ttu-id="553ad-139">使用下列程序 tooadd Azure 儲存體帳戶認證的 hello:</span><span class="sxs-lookup"><span data-stu-id="553ad-139">Use hello following procedures tooadd Azure storage account credentials:</span></span>

* <span data-ttu-id="553ad-140">儲存體帳戶認證具有 tooadd hello 相同 Azure 訂用帳戶 hello 裝置管理員服務</span><span class="sxs-lookup"><span data-stu-id="553ad-140">tooadd a storage account credential that has hello same Azure subscription as hello Device Manager service</span></span>
* <span data-ttu-id="553ad-141">tooadd 超出 hello 裝置管理員服務訂用帳戶的 Azure 儲存體帳戶認證</span><span class="sxs-lookup"><span data-stu-id="553ad-141">tooadd an Azure storage account credential that is outside of hello Device Manager service subscription</span></span>

[!INCLUDE [add-a-storage-account-update2](../../includes/storsimple-8000-configure-new-storage-account-u2.md)]

#### <a name="tooadd-an-azure-storage-account-credential-outside-of-hello-storsimple-device-manager-service-subscription"></a><span data-ttu-id="553ad-142">tooadd hello StorSimple 裝置管理員服務訂用帳戶以外的 Azure 儲存體帳戶認證</span><span class="sxs-lookup"><span data-stu-id="553ad-142">tooadd an Azure storage account credential outside of hello StorSimple Device Manager service subscription</span></span>

1. <span data-ttu-id="553ad-143">瀏覽 tooyour StorSimple 裝置管理員服務，選取，然後按兩下。</span><span class="sxs-lookup"><span data-stu-id="553ad-143">Navigate tooyour StorSimple Device Manager service, select and double-click it.</span></span> <span data-ttu-id="553ad-144">這會開啟 hello**概觀**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="553ad-144">This opens hello **Overview** blade.</span></span>
2. <span data-ttu-id="553ad-145">選取**儲存體帳戶認證**內 hello**組態**> 一節。</span><span class="sxs-lookup"><span data-stu-id="553ad-145">Select **Storage account credentials** within hello **Configuration** section.</span></span> <span data-ttu-id="553ad-146">這樣就會列出任何現有儲存體帳戶的認證與 hello StorSimple 裝置管理員服務相關聯。</span><span class="sxs-lookup"><span data-stu-id="553ad-146">This lists any existing storage account credentials associated with hello StorSimple Device Manager service.</span></span>
3. <span data-ttu-id="553ad-147">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="553ad-147">Click **Add**.</span></span>
4. <span data-ttu-id="553ad-148">在 hello**新增儲存體帳戶認證**刀鋒視窗中，請勿遵循 hello:</span><span class="sxs-lookup"><span data-stu-id="553ad-148">In hello **Add a storage account credential** blade, do hello following:</span></span>
   
    1. <span data-ttu-id="553ad-149">在 [訂用帳戶] 中，選取 [其他]。</span><span class="sxs-lookup"><span data-stu-id="553ad-149">For **Subscription**, select **Other**.</span></span>
   
    2. <span data-ttu-id="553ad-150">提供您的 Azure 儲存體帳戶認證 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="553ad-150">Provide hello name of your Azure storage account credential.</span></span>
   
    3. <span data-ttu-id="553ad-151">在 [hello**儲存體帳戶存取金鑰**] 文字方塊中，提供 hello 您的 Azure 儲存體帳戶認證的主要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="553ad-151">In hello **Storage account access key** text box, supply hello primary Access Key for your Azure storage account credential.</span></span> <span data-ttu-id="553ad-152">tooget 此索引鍵，移 toohello Azure 儲存體服務，選取您的儲存體帳戶認證，然後按一下**管理的帳戶金鑰**。</span><span class="sxs-lookup"><span data-stu-id="553ad-152">tooget this key, go toohello Azure Storage service, select your storage account credential, and click **Manage account keys**.</span></span> <span data-ttu-id="553ad-153">您現在可以複製 hello 主要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="553ad-153">You can now copy hello primary access key.</span></span>
   
    4. <span data-ttu-id="553ad-154">tooenable SSL，按一下 hello**啟用**按鈕 toocreate StorSimple 裝置管理員服務和 hello 雲端之間的網路通訊的安全通道。</span><span class="sxs-lookup"><span data-stu-id="553ad-154">tooenable SSL, click hello **Enable** button toocreate a secure channel for network communication between your StorSimple Device Manager service and hello cloud.</span></span> <span data-ttu-id="553ad-155">按一下 hello**停用**按鈕只有當您在私人雲端內操作。</span><span class="sxs-lookup"><span data-stu-id="553ad-155">Click hello **Disable** button only if you are operating within a private cloud.</span></span>
   
    5. <span data-ttu-id="553ad-156">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="553ad-156">Click **Add**.</span></span> <span data-ttu-id="553ad-157">已成功建立 hello 儲存體帳戶認證之後，您會收到通知。</span><span class="sxs-lookup"><span data-stu-id="553ad-157">You are notified after hello storage account credential is successfully created.</span></span>

5. <span data-ttu-id="553ad-158">底下的 hello StorSimple 設定裝置管理員服務刀鋒視窗上會顯示 hello 新建立的儲存體帳戶認證**儲存體帳戶認證**。</span><span class="sxs-lookup"><span data-stu-id="553ad-158">hello newly created storage account credential is displayed on hello StorSimple Configure Device Manager service blade under **Storage account credentials**.</span></span>
   


## <a name="edit-a-storage-account"></a><span data-ttu-id="553ad-159">編輯儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="553ad-159">Edit a storage account</span></span>

<span data-ttu-id="553ad-160">您可以編輯磁碟區容器所使用的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="553ad-160">You can edit a storage account that is used by a volume container.</span></span> <span data-ttu-id="553ad-161">如果您編輯目前正在使用的儲存體帳戶，hello 欄位可用 toomodify 是 hello hello 儲存體帳戶的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="553ad-161">If you edit a storage account that is currently in use, hello only field available toomodify is hello access key for hello storage account.</span></span> <span data-ttu-id="553ad-162">您可以提供 hello 新儲存體存取金鑰，並儲存更新的 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="553ad-162">You can supply hello new storage access key and save hello updated settings.</span></span>

#### <a name="tooedit-a-storage-account"></a><span data-ttu-id="553ad-163">tooedit 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="553ad-163">tooedit a storage account</span></span>

1. <span data-ttu-id="553ad-164">移 tooyour StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="553ad-164">Go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="553ad-165">在 hello**組態**區段中，按一下**儲存體帳戶認證**。</span><span class="sxs-lookup"><span data-stu-id="553ad-165">In hello **Configuration** section, click **Storage account credentials**.</span></span>

    ![儲存體帳戶認證](./media/storsimple-8000-manage-storage-accounts/editstorageacct1.png)

2. <span data-ttu-id="553ad-167">在 hello**儲存體帳戶認證**刀鋒視窗中的，從儲存體帳戶認證，選取 hello 清單，然後按一下您想 tooedit hello。</span><span class="sxs-lookup"><span data-stu-id="553ad-167">In hello **Storage account credentials** blade, from hello list of storage account credentials, select and click hello one you wish tooedit.</span></span> 

3. <span data-ttu-id="553ad-168">您可以修改 hello**啟用 SSL**選取項目。</span><span class="sxs-lookup"><span data-stu-id="553ad-168">You can modify hello **Enable SSL** selection.</span></span> <span data-ttu-id="553ad-169">您也可以按一下**更...** ，然後選取 **同步存取金鑰 toorotate**儲存體帳戶存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="553ad-169">You can also click **More...** and then select **Sync access key toorotate** your storage account access keys.</span></span> <span data-ttu-id="553ad-170">跳過[金鑰輪替的儲存體帳戶](#key-rotation-of-storage-accounts)如需有關如何 tooperform 金鑰輪替。</span><span class="sxs-lookup"><span data-stu-id="553ad-170">Go too[Key rotation of storage accounts](#key-rotation-of-storage-accounts) for more information on how tooperform key rotation.</span></span> <span data-ttu-id="553ad-171">您已修改 hello 設定之後，請按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="553ad-171">After you have modified hello settings, click **Save**.</span></span> 

    ![儲存編輯好的儲存體帳戶認證](./media/storsimple-8000-manage-storage-accounts/editstorageacct3.png)

4. <span data-ttu-id="553ad-173">系統提示您進行確認時，按一下 [是] 。</span><span class="sxs-lookup"><span data-stu-id="553ad-173">When prompted for confirmation, click **Yes**.</span></span> 

    ![確認修改](./media/storsimple-8000-manage-storage-accounts/editstorageacct4.png)

<span data-ttu-id="553ad-175">將更新 hello 設定，並將它儲存為儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="553ad-175">hello settings will be updated and saved for your storage account.</span></span> 

## <a name="delete-a-storage-account"></a><span data-ttu-id="553ad-176">刪除儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="553ad-176">Delete a storage account</span></span>

> [!IMPORTANT]
> <span data-ttu-id="553ad-177">只有在其未由磁碟區容器使用時，您才可以刪除儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="553ad-177">You can delete a storage account only if it is not used by a volume container.</span></span> <span data-ttu-id="553ad-178">如果磁碟區容器正在使用的儲存體帳戶，請先刪除 hello 磁碟區容器，然後再刪除相關聯的 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="553ad-178">If a storage account is being used by a volume container, first delete hello volume container and then delete hello associated storage account.</span></span>

#### <a name="toodelete-a-storage-account"></a><span data-ttu-id="553ad-179">toodelete 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="553ad-179">toodelete a storage account</span></span>

1. <span data-ttu-id="553ad-180">移 tooyour StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="553ad-180">Go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="553ad-181">在 hello**組態**區段中，按一下**儲存體帳戶認證**。</span><span class="sxs-lookup"><span data-stu-id="553ad-181">In hello **Configuration** section, click **Storage account credentials**.</span></span>

2. <span data-ttu-id="553ad-182">在 hello 表格式清單中的儲存體帳戶，請將滑鼠停留在您想 toodelete hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="553ad-182">In hello tabular list of storage accounts, hover over hello account that you wish toodelete.</span></span> <span data-ttu-id="553ad-183">Tooinvoke hello 操作功能表上按一下滑鼠右鍵，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="553ad-183">Right-click tooinvoke hello context menu and click **Delete**.</span></span>

    ![刪除儲存體帳戶認證](./media/storsimple-8000-manage-storage-accounts/deletestorageacct1.png)

3. <span data-ttu-id="553ad-185">當提示確認，請按一下**是**toocontinue 與 hello 刪除。</span><span class="sxs-lookup"><span data-stu-id="553ad-185">When prompted for confirmation, click **Yes** toocontinue with hello deletion.</span></span> <span data-ttu-id="553ad-186">hello 表格式清單將會更新的 tooreflect hello 的變更。</span><span class="sxs-lookup"><span data-stu-id="553ad-186">hello tabular listing will be updated tooreflect hello changes.</span></span>

    ![Confirm delete](./media/storsimple-8000-manage-storage-accounts/deletestorageacct2.png)

## <a name="key-rotation-of-storage-accounts"></a><span data-ttu-id="553ad-188">替換儲存體帳戶的金鑰</span><span class="sxs-lookup"><span data-stu-id="553ad-188">Key rotation of storage accounts</span></span>

<span data-ttu-id="553ad-189">基於安全性理由，通常是在資料中心內才需要替換金鑰。</span><span class="sxs-lookup"><span data-stu-id="553ad-189">For security reasons, key rotation is often a requirement in data centers.</span></span> <span data-ttu-id="553ad-190">每個 Microsoft Azure 訂用帳戶可以有一或多個相關聯的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="553ad-190">Each Microsoft Azure subscription can have one or more associated storage accounts.</span></span> <span data-ttu-id="553ad-191">hello 存取 toothese 帳戶受到 hello 訂用帳戶和每個儲存體帳戶存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="553ad-191">hello access toothese accounts is controlled by hello subscription and access keys for each storage account.</span></span> 

<span data-ttu-id="553ad-192">當您建立儲存體帳戶時，Microsoft Azure 會產生兩個存取 hello 儲存體帳戶時，可用於驗證的 512 位元儲存體存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="553ad-192">When you create a storage account, Microsoft Azure generates two 512-bit storage access keys that are used for authentication when hello storage account is accessed.</span></span> <span data-ttu-id="553ad-193">必須要有兩個儲存體存取金鑰可讓您使用不中斷 tooyour 儲存體服務或存取 toothat 服務 tooregenerate hello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="553ad-193">Having two storage access keys allows you tooregenerate hello keys with no interruption tooyour storage service or access toothat service.</span></span> <span data-ttu-id="553ad-194">hello 目前正在使用的索引鍵為 hello*主要*索引鍵和 hello 備份金鑰是參照的 tooas hello*次要*索引鍵。</span><span class="sxs-lookup"><span data-stu-id="553ad-194">hello key that is currently in use is hello *primary* key and hello backup key is referred tooas hello *secondary* key.</span></span> <span data-ttu-id="553ad-195">當 Microsoft Azure StorSimple 裝置存取您的雲端儲存體服務提供者時必須提供這些兩個機碼之一。</span><span class="sxs-lookup"><span data-stu-id="553ad-195">One of these two keys must be supplied when your Microsoft Azure StorSimple device accesses your cloud storage service provider.</span></span>

## <a name="what-is-key-rotation"></a><span data-ttu-id="553ad-196">什麼是替換金鑰？</span><span class="sxs-lookup"><span data-stu-id="553ad-196">What is key rotation?</span></span>

<span data-ttu-id="553ad-197">一般而言，應用程式使用其中一個 hello 金鑰 tooaccess 您的資料。</span><span class="sxs-lookup"><span data-stu-id="553ad-197">Typically, applications use only one of hello keys tooaccess your data.</span></span> <span data-ttu-id="553ad-198">在一段時間之後, 您可以讓應用程式切換 toousing hello 第二個索引鍵。</span><span class="sxs-lookup"><span data-stu-id="553ad-198">After a certain period of time, you can have your applications switch over toousing hello second key.</span></span> <span data-ttu-id="553ad-199">切換應用程式 toohello 的次要金鑰之後，您可以淘汰 hello 第一個索引鍵，並再產生新的金鑰。</span><span class="sxs-lookup"><span data-stu-id="553ad-199">After you have switched your applications toohello secondary key, you can retire hello first key and then generate a new key.</span></span> <span data-ttu-id="553ad-200">使用 hello 兩個索引鍵，如此一來，可以讓應用程式存取 toohello 資料而不會產生任何停機時間。</span><span class="sxs-lookup"><span data-stu-id="553ad-200">Using hello two keys this way allows your applications access toohello data without incurring any downtime.</span></span>

<span data-ttu-id="553ad-201">hello 儲存體帳戶金鑰一律儲存在 hello 服務，以加密格式。</span><span class="sxs-lookup"><span data-stu-id="553ad-201">hello storage account keys are always stored in hello service in an encrypted form.</span></span> <span data-ttu-id="553ad-202">不過，這些可以重設透過 hello StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="553ad-202">However, these can be reset via hello StorSimple Device Manager service.</span></span> <span data-ttu-id="553ad-203">hello 服務可以取得 hello 主索引鍵和次要索引鍵的所有 hello 的 hello 相同訂用帳戶，包括 hello 儲存體服務，以及 hello 預設儲存體帳戶中建立的帳戶產生的儲存體帳戶時 hello StorSimple 裝置管理員第一次建立服務的服務。</span><span class="sxs-lookup"><span data-stu-id="553ad-203">hello service can get hello primary key and secondary key for all hello storage accounts in hello same subscription, including accounts created in hello Storage service as well as hello default storage accounts generated when hello StorSimple Device Manager service service was first created.</span></span> <span data-ttu-id="553ad-204">hello StorSimple 裝置管理員服務將一律從 hello Azure 傳統入口網站取得這些金鑰，然後以加密方式儲存。</span><span class="sxs-lookup"><span data-stu-id="553ad-204">hello StorSimple Device Manager service will always get these keys from hello Azure classic portal and then store them in an encrypted manner.</span></span>

## <a name="rotation-workflow"></a><span data-ttu-id="553ad-205">替換工作流程</span><span class="sxs-lookup"><span data-stu-id="553ad-205">Rotation workflow</span></span>

<span data-ttu-id="553ad-206">Microsoft Azure 系統管理員可以重新產生，或藉由直接存取 hello （透過 hello Microsoft Azure 儲存體服務) 的儲存體帳戶變更 hello 主要或次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="553ad-206">A Microsoft Azure administrator can regenerate or change hello primary or secondary key by directly accessing hello storage account (via hello Microsoft Azure Storage service).</span></span> <span data-ttu-id="553ad-207">hello StorSimple 裝置 Manager 服務不會自動看到這項變更。</span><span class="sxs-lookup"><span data-stu-id="553ad-207">hello StorSimple Device Manager service does not see this change automatically.</span></span>

<span data-ttu-id="553ad-208">tooinform hello StorSimple 裝置管理員 hello 變更的服務，您將需要 tooaccess hello StorSimple 裝置管理員服務存取 hello 儲存體帳戶，然後再同步處理 hello 主要或次要金鑰 （視何者有所變更）。</span><span class="sxs-lookup"><span data-stu-id="553ad-208">tooinform hello StorSimple Device Manager service of hello change, you will need tooaccess hello StorSimple Device Manager service, access hello storage account, and then synchronize hello primary or secondary key (depending on which one was changed).</span></span> <span data-ttu-id="553ad-209">hello 服務然後取得 hello 最新的金鑰，加密 hello 金鑰，並傳送嗨加密金鑰 toohello 的裝置。</span><span class="sxs-lookup"><span data-stu-id="553ad-209">hello service then gets hello latest key, encrypts hello keys, and sends hello encrypted key toohello device.</span></span>

#### <a name="toosynchronize-keys-for-storage-accounts-in-hello-same-subscription-as-hello-service"></a><span data-ttu-id="553ad-210">儲存體帳戶的 toosynchronize 金鑰 hello hello 服務相同訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="553ad-210">toosynchronize keys for storage accounts in hello same subscription as hello service</span></span> 
1. <span data-ttu-id="553ad-211">移 tooyour StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="553ad-211">Go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="553ad-212">在 hello**組態**區段中，按一下**儲存體帳戶認證**。</span><span class="sxs-lookup"><span data-stu-id="553ad-212">In hello **Configuration** section, click **Storage account credentials**.</span></span>
2. <span data-ttu-id="553ad-213">從 hello 表格清單中的儲存體帳戶，按一下 hello 其中一個要 toomodify。</span><span class="sxs-lookup"><span data-stu-id="553ad-213">From hello tabular listing of storage accounts, click hello one that you want toomodify.</span></span> 

    ![同步處理金鑰](./media/storsimple-8000-manage-storage-accounts/syncaccesskey1.png)

3. <span data-ttu-id="553ad-215">按一下**...多個**，然後選取 **同步存取金鑰 toorotate**。</span><span class="sxs-lookup"><span data-stu-id="553ad-215">Click **...More** and then select **Sync access key toorotate**.</span></span>   

    ![同步處理金鑰](./media/storsimple-8000-manage-storage-accounts/syncaccesskey2.png)

4. <span data-ttu-id="553ad-217">在 hello StorSimple 裝置管理員服務，您會需要 tooupdate hello 金鑰先前已在 hello Microsoft Azure 儲存體服務中變更。</span><span class="sxs-lookup"><span data-stu-id="553ad-217">In hello StorSimple Device Manager service, you need tooupdate hello key that was previously changed in hello Microsoft Azure Storage service.</span></span> <span data-ttu-id="553ad-218">如果 hello 主要存取金鑰已變更 （重新產生），選取**主要**索引鍵。</span><span class="sxs-lookup"><span data-stu-id="553ad-218">If hello primary access key was changed (regenerated), select **primary** key.</span></span> <span data-ttu-id="553ad-219">如果 hello 次要索引鍵已變更，請選取**次要**索引鍵。</span><span class="sxs-lookup"><span data-stu-id="553ad-219">If hello secondary key was changed, select **secondary** key.</span></span> <span data-ttu-id="553ad-220">按一下 [同步處理金鑰]。</span><span class="sxs-lookup"><span data-stu-id="553ad-220">Click **Sync key**.</span></span>
      
      ![同步處理金鑰](./media/storsimple-8000-manage-storage-accounts/syncaccesskey3.png)

<span data-ttu-id="553ad-222">Hello 金鑰已順利 sycnhronized 之後，系統會通知您。</span><span class="sxs-lookup"><span data-stu-id="553ad-222">You will be notified after hello key is successfully sycnhronized.</span></span>

#### <a name="toosynchronize-keys-for-storage-accounts-outside-of-hello-service-subscription"></a><span data-ttu-id="553ad-223">toosynchronize hello 服務訂用帳戶以外的儲存體帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="553ad-223">toosynchronize keys for storage accounts outside of hello service subscription</span></span>
1. <span data-ttu-id="553ad-224">在 [hello**服務**頁面上，按一下 hello**設定**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="553ad-224">On hello **Services** page, click hello **Configure** tab.</span></span>
2. <span data-ttu-id="553ad-225">按一下 [新增/編輯儲存體帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="553ad-225">Click **Add/Edit Storage Accounts**.</span></span>
3. <span data-ttu-id="553ad-226">在 [hello] 對話方塊中，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="553ad-226">In hello dialog box, do hello following:</span></span>
   
   1. <span data-ttu-id="553ad-227">選取 hello 儲存體帳戶與 hello 便捷鍵的 tooupdate。</span><span class="sxs-lookup"><span data-stu-id="553ad-227">Select hello storage account with hello access key that you want tooupdate.</span></span>
   2. <span data-ttu-id="553ad-228">您必須在 StorSimple 裝置管理員服務 hello tooupdate hello 儲存體存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="553ad-228">You will need tooupdate hello storage access key in hello StorSimple Device Manager service.</span></span> <span data-ttu-id="553ad-229">在此情況下，您可以看到 hello 儲存體存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="553ad-229">In this case, you can see hello storage access key.</span></span> <span data-ttu-id="553ad-230">輸入 hello 新金鑰在 hello**儲存體帳戶存取金鑰**方塊。</span><span class="sxs-lookup"><span data-stu-id="553ad-230">Enter hello new key in hello **Storage Account Access Key** box.</span></span> 
   3. <span data-ttu-id="553ad-231">儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="553ad-231">Save your changes.</span></span> <span data-ttu-id="553ad-232">現在應已更新您的儲存體帳戶存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="553ad-232">Your storage account access key should now be updated.</span></span>

## <a name="next-steps"></a><span data-ttu-id="553ad-233">後續步驟</span><span class="sxs-lookup"><span data-stu-id="553ad-233">Next steps</span></span>
* <span data-ttu-id="553ad-234">深入了解 [StorSimple 安全性](storsimple-8000-security.md)。</span><span class="sxs-lookup"><span data-stu-id="553ad-234">Learn more about [StorSimple security](storsimple-8000-security.md).</span></span>
* <span data-ttu-id="553ad-235">深入了解[使用您的 StorSimple 裝置 hello StorSimple 裝置管理員服務 tooadminister](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="553ad-235">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

