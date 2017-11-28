---
title: "aaaManage StorSimple 儲存體帳戶 |Microsoft 文件"
description: "說明如何使用 StorSimple Manager 設定頁面 tooadd hello、 編輯、 刪除或旋轉 hello 安全性金鑰的儲存體帳戶。"
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
ms.openlocfilehash: 78f408818ee8532dfaac445200048145547c987c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-your-storage-account"></a><span data-ttu-id="5bad7-103">使用 hello StorSimple Manager 服務 toomanage 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="5bad7-103">Use hello StorSimple Manager service toomanage your storage account</span></span>
## <a name="overview"></a><span data-ttu-id="5bad7-104">概觀</span><span class="sxs-lookup"><span data-stu-id="5bad7-104">Overview</span></span>
<span data-ttu-id="5bad7-105">hello**設定**頁面會顯示所有可由 hello StorSimple Manager 服務的 hello 全域服務參數。</span><span class="sxs-lookup"><span data-stu-id="5bad7-105">hello **Configure** page presents all hello global service parameters that can be created in hello StorSimple Manager service.</span></span> <span data-ttu-id="5bad7-106">這些參數可以是裝置連線 toohello 服務，並包含套用的 tooall hello:</span><span class="sxs-lookup"><span data-stu-id="5bad7-106">These parameters can be applied tooall hello devices connected toohello service, and include:</span></span>

* <span data-ttu-id="5bad7-107">儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="5bad7-107">Storage accounts</span></span> 
* <span data-ttu-id="5bad7-108">頻寬範本</span><span class="sxs-lookup"><span data-stu-id="5bad7-108">Bandwidth templates</span></span> 
* <span data-ttu-id="5bad7-109">存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="5bad7-109">Access control records</span></span> 

<span data-ttu-id="5bad7-110">本教學課程說明如何使用 hello**設定**tooadd、 編輯或刪除儲存體帳戶 頁面上，或旋轉 hello 儲存體帳戶的安全性金鑰。</span><span class="sxs-lookup"><span data-stu-id="5bad7-110">This tutorial explains how you can use hello **Configure** page tooadd, edit, or delete storage accounts, or rotate hello security keys for a storage account.</span></span>

 ![[設定] 頁面](./media/storsimple-manage-storage-accounts/HCS_ConfigureService.png)  

<span data-ttu-id="5bad7-112">儲存體帳戶包含 hello hello 裝置使用 tooaccess 與您的雲端服務提供者的儲存體帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="5bad7-112">Storage accounts contain hello credentials that hello device uses tooaccess your storage account with your cloud service provider.</span></span> <span data-ttu-id="5bad7-113">Microsoft Azure 儲存體帳戶，這些是認證，例如 hello 帳戶名稱和 hello 主要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="5bad7-113">For Microsoft Azure storage accounts, these are credentials such as hello account name and hello primary access key.</span></span> 

<span data-ttu-id="5bad7-114">在 hello**設定**頁面上，建立 hello 計費訂用帳戶的帳戶會包含下列資訊的 hello 以表格格式顯示所有存放裝置：</span><span class="sxs-lookup"><span data-stu-id="5bad7-114">On hello **Configure** page, all storage accounts that are created for hello billing subscription are displayed in a tabular format containing hello following information:</span></span>

* <span data-ttu-id="5bad7-115">**名稱**– hello 指派唯一名稱 toohello 帳戶建立時。</span><span class="sxs-lookup"><span data-stu-id="5bad7-115">**Name** – hello unique name assigned toohello account when it was created.</span></span>
* <span data-ttu-id="5bad7-116">**啟用 SSL** – 是否 hello 啟用 SSL，所以裝置到雲端的通訊都會透過 hello 安全通道。</span><span class="sxs-lookup"><span data-stu-id="5bad7-116">**SSL enabled** – Whether hello SSL is enabled and device-to-cloud communication is over hello secure channel.</span></span>
* <span data-ttu-id="5bad7-117">**使用**– hello 使用 hello 儲存體帳戶的磁碟區數目。</span><span class="sxs-lookup"><span data-stu-id="5bad7-117">**Used by** – hello number of volumes using hello storage account.</span></span>

<span data-ttu-id="5bad7-118">hello 最常見的工作相關 toostorage 帳戶對 hello**設定**頁面：</span><span class="sxs-lookup"><span data-stu-id="5bad7-118">hello most common tasks related toostorage accounts that can be performed on hello **Configure** page are:</span></span>

* <span data-ttu-id="5bad7-119">新增儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="5bad7-119">Add a storage account</span></span> 
* <span data-ttu-id="5bad7-120">編輯儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="5bad7-120">Edit a storage account</span></span> 
* <span data-ttu-id="5bad7-121">刪除儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="5bad7-121">Delete a storage account</span></span> 
* <span data-ttu-id="5bad7-122">替換儲存體帳戶的金鑰</span><span class="sxs-lookup"><span data-stu-id="5bad7-122">Key rotation of storage accounts</span></span> 

## <a name="types-of-storage-accounts"></a><span data-ttu-id="5bad7-123">儲存體帳戶類型</span><span class="sxs-lookup"><span data-stu-id="5bad7-123">Types of storage accounts</span></span>
<span data-ttu-id="5bad7-124">有三種儲存體帳戶類型能與 StorSimple 裝置搭配使用。</span><span class="sxs-lookup"><span data-stu-id="5bad7-124">There are three types of storage accounts that can be used with your StorSimple device.</span></span>

* <span data-ttu-id="5bad7-125">**自動產生的儲存體帳戶**– 第一次建立 hello 服務時，就 hello 名所示，自動產生這種類型的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5bad7-125">**Auto-generated storage accounts** – As hello name suggests, this type of storage account is automatically generated when hello service is first created.</span></span> <span data-ttu-id="5bad7-126">toolearn 深入了解如何建立這個儲存體帳戶，請參閱[步驟 1： 建立新的服務](storsimple-deployment-walkthrough-u1.md#step-1-create-a-new-service)中[部署在內部部署 StorSimple 裝置](storsimple-deployment-walkthrough.md)。</span><span class="sxs-lookup"><span data-stu-id="5bad7-126">toolearn more about how this storage account is created, see [Step 1: Create a new service](storsimple-deployment-walkthrough-u1.md#step-1-create-a-new-service) in [Deploy your on-premises StorSimple device](storsimple-deployment-walkthrough.md).</span></span> 
* <span data-ttu-id="5bad7-127">**Hello 服務訂用帳戶中的儲存體帳戶**– 這些是 hello hello 與相關聯的 Azure 儲存體帳戶相同的訂用帳戶 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="5bad7-127">**Storage accounts in hello service subscription** – These are hello Azure storage accounts that are associated with hello same subscription as that of hello service.</span></span> <span data-ttu-id="5bad7-128">toolearn 深入了解如何建立儲存體帳戶，請參閱[關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="5bad7-128">toolearn more about how these storage accounts are created, see [About Azure Storage Accounts](../storage/common/storage-create-storage-account.md).</span></span> 
* <span data-ttu-id="5bad7-129">**Hello 服務訂用帳戶以外的儲存體帳戶**-這些是與您的服務沒有關聯的 hello Azure 儲存體帳戶，並可能存在於之前 hello 服務已建立。</span><span class="sxs-lookup"><span data-stu-id="5bad7-129">**Storage accounts outside of hello service subscription** – These are hello Azure storage accounts that are not associated with your service and likely existed before hello service was created.</span></span>

## <a name="add-a-storage-account"></a><span data-ttu-id="5bad7-130">新增儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="5bad7-130">Add a storage account</span></span>
<span data-ttu-id="5bad7-131">您可以新增儲存體帳戶提供唯一的易記名稱和存取認證連結 toohello 儲存體帳戶 （與 hello 指定的雲端服務提供者）。</span><span class="sxs-lookup"><span data-stu-id="5bad7-131">You can add a storage account by providing a unique friendly name and access credentials that are linked toohello storage account (with hello specified cloud service provider).</span></span> <span data-ttu-id="5bad7-132">您也可以啟用您的裝置與 hello 雲端之間的網路通訊的安全通道 hello 安全通訊端層 (SSL) 模式 toocreate hello 選項。</span><span class="sxs-lookup"><span data-stu-id="5bad7-132">You also have hello option of enabling hello secure sockets layer (SSL) mode toocreate a secure channel for network communication between your device and hello cloud.</span></span>

<span data-ttu-id="5bad7-133">您可以為指定的雲端服務提供者建立多個帳戶。</span><span class="sxs-lookup"><span data-stu-id="5bad7-133">You can create multiple accounts for a given cloud service provider.</span></span> <span data-ttu-id="5bad7-134">不過，請注意，建立儲存體帳戶之後，您無法變更 hello 雲端服務提供者。</span><span class="sxs-lookup"><span data-stu-id="5bad7-134">Be aware, however, that after a storage account is created, you cannot change hello cloud service provider.</span></span>

<span data-ttu-id="5bad7-135">正在儲存 hello 儲存體帳戶，而 hello 服務會嘗試 toocommunicate 與您的雲端服務提供者。</span><span class="sxs-lookup"><span data-stu-id="5bad7-135">While hello storage account is being saved, hello service attempts toocommunicate with your cloud service provider.</span></span> <span data-ttu-id="5bad7-136">在這個階段，將會驗證 hello 認證和您所提供的 hello 存取資料。</span><span class="sxs-lookup"><span data-stu-id="5bad7-136">hello credentials and hello access material that you supplied will be authenticated at this time.</span></span> <span data-ttu-id="5bad7-137">只有在 hello 驗證成功時，會建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5bad7-137">A storage account is created only if hello authentication succeeds.</span></span> <span data-ttu-id="5bad7-138">如果 hello 驗證失敗，將顯示適當的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="5bad7-138">If hello authentication fails, then an appropriate error message will be displayed.</span></span>

<span data-ttu-id="5bad7-139">在 Azure 入口網站中建立的 Resource Manager 儲存體帳戶也支援 StorSimple。</span><span class="sxs-lookup"><span data-stu-id="5bad7-139">Resource Manager storage accounts created in Azure portal are also supported with StorSimple.</span></span> <span data-ttu-id="5bad7-140">hello 時嘗試 toocreate 磁碟區容器，選取範圍的 hello 下拉式清單中將不會顯示儲存體帳戶的資源管理員只 hello hello Azure 傳統入口網站中建立的帳戶將會顯示儲存體。</span><span class="sxs-lookup"><span data-stu-id="5bad7-140">hello Resource Manager storage accounts will not show up in hello drop-down list for selection when trying toocreate a volume container, only hello storage accounts created in hello Azure classic portal will be displayed.</span></span> <span data-ttu-id="5bad7-141">資源管理員的儲存體帳戶將需要使用 hello 程序 tooadd 如下所述的儲存體帳戶加入 toobe。</span><span class="sxs-lookup"><span data-stu-id="5bad7-141">Resource Manager storage accounts will need toobe added using hello procedure tooadd a storage account described below.</span></span>

> [!NOTE]
> <span data-ttu-id="5bad7-142">新增儲存體帳戶的 hello 程序不同根據您所使用的 hello StorSimple 軟體版本。</span><span class="sxs-lookup"><span data-stu-id="5bad7-142">hello procedure for adding a storage account differs based on hello StorSimple software version you are using.</span></span> <span data-ttu-id="5bad7-143">為確定 toofollow hello 正確的程序適用於您的 StorSimple 版本。</span><span class="sxs-lookup"><span data-stu-id="5bad7-143">Be sure toofollow hello correct procedure for your StorSimple version.</span></span>
> 
> 

[!INCLUDE [add-a-storage-account-update1](../../includes/storsimple-configure-new-storage-account-u1.md)]

[!INCLUDE [add-a-storage-account](../../includes/storsimple-configure-new-storage-account.md)]

## <a name="edit-a-storage-account"></a><span data-ttu-id="5bad7-144">編輯儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="5bad7-144">Edit a storage account</span></span>
<span data-ttu-id="5bad7-145">您可以編輯磁碟區容器所使用的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5bad7-145">You can edit a storage account that is used by a volume container.</span></span> <span data-ttu-id="5bad7-146">如果您編輯目前正在使用的儲存體帳戶，hello 欄位可用 toomodify 是 hello hello 儲存體帳戶的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="5bad7-146">If you edit a storage account that is currently in use, hello only field available toomodify is hello access key for hello storage account.</span></span> <span data-ttu-id="5bad7-147">您可以提供 hello 新儲存體存取金鑰，並儲存更新的 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="5bad7-147">You can supply hello new storage access key and save hello updated settings.</span></span>

#### <a name="tooedit-a-storage-account"></a><span data-ttu-id="5bad7-148">tooedit 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="5bad7-148">tooedit a storage account</span></span>
1. <span data-ttu-id="5bad7-149">在 hello 服務登陸頁面上，選取您的服務、 按兩下 hello 的服務名稱，然後按一下**設定**。</span><span class="sxs-lookup"><span data-stu-id="5bad7-149">On hello service landing page, select your service, double-click hello service name, and then click **Configure**.</span></span>
2. <span data-ttu-id="5bad7-150">按一下 [新增/編輯儲存體帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="5bad7-150">Click **Add/Edit Storage Accounts**.</span></span>
3. <span data-ttu-id="5bad7-151">在 hello**新增/編輯儲存體帳戶**對話方塊：</span><span class="sxs-lookup"><span data-stu-id="5bad7-151">In hello **Add/Edit Storage Accounts** dialog box:</span></span>
   
   1. <span data-ttu-id="5bad7-152">Hello 下拉式清單中**儲存體帳戶**，選擇您想要 toomodify 現有的帳戶。</span><span class="sxs-lookup"><span data-stu-id="5bad7-152">In hello drop-down list of **Storage Accounts**, choose an existing account that you would like toomodify.</span></span> <span data-ttu-id="5bad7-153">這也可能包括 hello hello 服務第一次建立時自動產生的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5bad7-153">This could also include hello storage accounts that were automatically generated when hello service was first created.</span></span>
   2. <span data-ttu-id="5bad7-154">如果有必要，您可以修改 hello**啟用 SSL 模式**選取項目。</span><span class="sxs-lookup"><span data-stu-id="5bad7-154">If necessary, you can modify hello **Enable SSL Mode** selection.</span></span>
   3. <span data-ttu-id="5bad7-155">您可以選擇 toorotate 儲存體帳戶存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="5bad7-155">You can choose toorotate your storage account access keys.</span></span> <span data-ttu-id="5bad7-156">請參閱[金鑰輪替的儲存體帳戶](#key-rotation-of-storage-accounts)如需有關如何 tooperform 金鑰輪替。</span><span class="sxs-lookup"><span data-stu-id="5bad7-156">See [Key rotation of storage accounts](#key-rotation-of-storage-accounts) for more information about how tooperform key rotation.</span></span>
   4. <span data-ttu-id="5bad7-157">按一下核取圖示，hello![核取圖示](./media/storsimple-manage-storage-accounts/HCS_CheckIcon.png)toosave hello 設定。</span><span class="sxs-lookup"><span data-stu-id="5bad7-157">Click hello check icon ![check icon](./media/storsimple-manage-storage-accounts/HCS_CheckIcon.png) toosave hello settings.</span></span> <span data-ttu-id="5bad7-158">hello 設定將更新上 hello**設定**頁面。</span><span class="sxs-lookup"><span data-stu-id="5bad7-158">hello settings will be updated on hello **Configure** page.</span></span> <span data-ttu-id="5bad7-159">按一下**儲存**toosave hello 新更新的設定。</span><span class="sxs-lookup"><span data-stu-id="5bad7-159">Click **Save** toosave hello newly updated settings.</span></span>
      
      ![編輯儲存體帳戶](./media/storsimple-manage-storage-accounts/HCs_AddEditStorageAccount.png)

## <a name="delete-a-storage-account"></a><span data-ttu-id="5bad7-161">刪除儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="5bad7-161">Delete a storage account</span></span>
> [!IMPORTANT]
> <span data-ttu-id="5bad7-162">只有在其未由磁碟區容器使用時，您才可以刪除儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5bad7-162">You can delete a storage account only if it is not used by a volume container.</span></span> <span data-ttu-id="5bad7-163">如果磁碟區容器正在使用的儲存體帳戶，請先刪除 hello 磁碟區容器，然後再刪除相關聯的 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5bad7-163">If a storage account is being used by a volume container, first delete hello volume container and then delete hello associated storage account.</span></span>
> 
> 

#### <a name="toodelete-a-storage-account"></a><span data-ttu-id="5bad7-164">toodelete 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="5bad7-164">toodelete a storage account</span></span>
1. <span data-ttu-id="5bad7-165">在 hello StorSimple Manager 服務登陸頁面上，選取您的服務、 按兩下 hello 的服務名稱，然後按一下**設定**。</span><span class="sxs-lookup"><span data-stu-id="5bad7-165">On hello StorSimple Manager service landing page, select your service, double-click hello service name, and then click **Configure**.</span></span>
2. <span data-ttu-id="5bad7-166">在 hello 表格式清單中的儲存體帳戶，請將滑鼠停留在您想 toodelete hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="5bad7-166">In hello tabular list of storage accounts, hover over hello account that you wish toodelete.</span></span>
3. <span data-ttu-id="5bad7-167">刪除圖示 (**x**) 會出現在 hello 極端右側的欄該儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5bad7-167">A delete icon (**x**) will appear in hello extreme right column for that storage account.</span></span> <span data-ttu-id="5bad7-168">按一下 hello **x**圖示 toodelete hello 認證。</span><span class="sxs-lookup"><span data-stu-id="5bad7-168">Click hello **x** icon toodelete hello credentials.</span></span>
4. <span data-ttu-id="5bad7-169">當提示確認，請按一下**是**toocontinue 與 hello 刪除。</span><span class="sxs-lookup"><span data-stu-id="5bad7-169">When prompted for confirmation, click **Yes** toocontinue with hello deletion.</span></span> <span data-ttu-id="5bad7-170">hello 表格式清單將會更新的 tooreflect hello 的變更。</span><span class="sxs-lookup"><span data-stu-id="5bad7-170">hello tabular listing will be updated tooreflect hello changes.</span></span>

## <a name="key-rotation-of-storage-accounts"></a><span data-ttu-id="5bad7-171">替換儲存體帳戶的金鑰</span><span class="sxs-lookup"><span data-stu-id="5bad7-171">Key rotation of storage accounts</span></span>
<span data-ttu-id="5bad7-172">基於安全性理由，通常是在資料中心內才需要替換金鑰。</span><span class="sxs-lookup"><span data-stu-id="5bad7-172">For security reasons, key rotation is often a requirement in data centers.</span></span> 

> [!NOTE]
> <span data-ttu-id="5bad7-173">hello 更換金鑰資訊與 hello 旋轉的程序適用於僅 tooMicrosoft Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5bad7-173">hello following key rotation information and hello rotation procedure apply tooMicrosoft Azure storage accounts only.</span></span> <span data-ttu-id="5bad7-174">若您使用的是其他雲端服務提供者，可以透過該提供者的儀表板管理儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="5bad7-174">If you are using another cloud service provider, you can manage storage account keys through that provider's dashboard.</span></span>
> 
> 

<span data-ttu-id="5bad7-175">每個 Microsoft Azure 訂用帳戶可以有一或多個相關聯的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5bad7-175">Each Microsoft Azure subscription can have one or more associated storage accounts.</span></span> <span data-ttu-id="5bad7-176">hello 存取 toothese 帳戶受到 hello 訂用帳戶和每個儲存體帳戶存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="5bad7-176">hello access toothese accounts is controlled by hello subscription and access keys for each storage account.</span></span> 

<span data-ttu-id="5bad7-177">當您建立儲存體帳戶時，Microsoft Azure 會產生兩個存取 hello 儲存體帳戶時，可用於驗證的 512 位元儲存體存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="5bad7-177">When you create a storage account, Microsoft Azure generates two 512-bit storage access keys that are used for authentication when hello storage account is accessed.</span></span> <span data-ttu-id="5bad7-178">必須要有兩個儲存體存取金鑰可讓您使用不中斷 tooyour 儲存體服務或存取 toothat 服務 tooregenerate hello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="5bad7-178">Having two storage access keys allows you tooregenerate hello keys with no interruption tooyour storage service or access toothat service.</span></span> <span data-ttu-id="5bad7-179">hello 目前正在使用的索引鍵為 hello*主要*索引鍵和 hello 備份金鑰是參照的 tooas hello*次要*索引鍵。</span><span class="sxs-lookup"><span data-stu-id="5bad7-179">hello key that is currently in use is hello *primary* key and hello backup key is referred tooas hello *secondary* key.</span></span> <span data-ttu-id="5bad7-180">當 Microsoft Azure StorSimple 裝置存取您的雲端儲存體服務提供者時必須提供這些兩個機碼之一。</span><span class="sxs-lookup"><span data-stu-id="5bad7-180">One of these two keys must be supplied when your Microsoft Azure StorSimple device accesses your cloud storage service provider.</span></span>

## <a name="what-is-key-rotation"></a><span data-ttu-id="5bad7-181">什麼是替換金鑰？</span><span class="sxs-lookup"><span data-stu-id="5bad7-181">What is key rotation?</span></span>
<span data-ttu-id="5bad7-182">一般而言，應用程式使用其中一個 hello 金鑰 tooaccess 您的資料。</span><span class="sxs-lookup"><span data-stu-id="5bad7-182">Typically, applications use only one of hello keys tooaccess your data.</span></span> <span data-ttu-id="5bad7-183">在一段時間之後, 您可以讓應用程式切換 toousing hello 第二個索引鍵。</span><span class="sxs-lookup"><span data-stu-id="5bad7-183">After a certain period of time, you can have your applications switch over toousing hello second key.</span></span> <span data-ttu-id="5bad7-184">切換應用程式 toohello 的次要金鑰之後，您可以淘汰 hello 第一個索引鍵，並再產生新的金鑰。</span><span class="sxs-lookup"><span data-stu-id="5bad7-184">After you have switched your applications toohello secondary key, you can retire hello first key and then generate a new key.</span></span> <span data-ttu-id="5bad7-185">使用 hello 兩個索引鍵，如此一來，可以讓應用程式存取 toohello 資料而不會產生任何停機時間。</span><span class="sxs-lookup"><span data-stu-id="5bad7-185">Using hello two keys this way allows your applications access toohello data without incurring any downtime.</span></span>

<span data-ttu-id="5bad7-186">hello 儲存體帳戶金鑰一律儲存在 hello 服務，以加密格式。</span><span class="sxs-lookup"><span data-stu-id="5bad7-186">hello storage account keys are always stored in hello service in an encrypted form.</span></span> <span data-ttu-id="5bad7-187">不過，這些可以重設透過 hello StorSimple Manager 服務。</span><span class="sxs-lookup"><span data-stu-id="5bad7-187">However, these can be reset via hello StorSimple Manager service.</span></span> <span data-ttu-id="5bad7-188">hello 服務可以取得 hello 主索引鍵和次要索引鍵的所有 hello 的 hello 相同訂用帳戶，包括 hello 儲存體服務，以及 hello 預設儲存體帳戶中建立的帳戶產生的儲存體帳戶時 hello StorSimple Manager 服務第一次建立服務。</span><span class="sxs-lookup"><span data-stu-id="5bad7-188">hello service can get hello primary key and secondary key for all hello storage accounts in hello same subscription, including accounts created in hello Storage service as well as hello default storage accounts generated when hello StorSimple Manager service service was first created.</span></span> <span data-ttu-id="5bad7-189">hello StorSimple Manager 服務將一律從 hello Azure 傳統入口網站取得這些金鑰，然後以加密方式儲存。</span><span class="sxs-lookup"><span data-stu-id="5bad7-189">hello StorSimple Manager service service will always get these keys from hello Azure classic portal and then store them in an encrypted manner.</span></span>

## <a name="rotation-workflow"></a><span data-ttu-id="5bad7-190">替換工作流程</span><span class="sxs-lookup"><span data-stu-id="5bad7-190">Rotation workflow</span></span>
<span data-ttu-id="5bad7-191">Microsoft Azure 系統管理員可以重新產生，或藉由直接存取 hello （透過 hello Microsoft Azure 儲存體服務) 的儲存體帳戶變更 hello 主要或次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="5bad7-191">A Microsoft Azure administrator can regenerate or change hello primary or secondary key by directly accessing hello storage account (via hello Microsoft Azure Storage service).</span></span> <span data-ttu-id="5bad7-192">hello StorSimple Manager 服務不會自動看到這項變更。</span><span class="sxs-lookup"><span data-stu-id="5bad7-192">hello StorSimple Manager service does not see this change automatically.</span></span>

<span data-ttu-id="5bad7-193">tooinform hello StorSimple Manager 服務的 hello 變更，您將需要 tooaccess hello StorSimple Manager 服務存取 hello 儲存體帳戶，然後再同步處理 hello 主要或次要金鑰 （視何者有所變更）。</span><span class="sxs-lookup"><span data-stu-id="5bad7-193">tooinform hello StorSimple Manager service of hello change, you will need tooaccess hello StorSimple Manager service, access hello storage account, and then synchronize hello primary or secondary key (depending on which one was changed).</span></span> <span data-ttu-id="5bad7-194">hello 服務然後取得 hello 最新的金鑰，加密 hello 金鑰，並傳送嗨加密金鑰 toohello 的裝置。</span><span class="sxs-lookup"><span data-stu-id="5bad7-194">hello service then gets hello latest key, encrypts hello keys, and sends hello encrypted key toohello device.</span></span>

#### <a name="toosynchronize-keys-for-storage-accounts-in-hello-same-subscription-as-hello-service-azure-only"></a><span data-ttu-id="5bad7-195">儲存體帳戶的 toosynchronize 金鑰 hello hello 服務 (僅限 Azure) 相同訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="5bad7-195">toosynchronize keys for storage accounts in hello same subscription as hello service (Azure only)</span></span>
1. <span data-ttu-id="5bad7-196">在 [hello**服務**頁面上，按一下 hello**設定**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="5bad7-196">On hello **Services** page, click hello **Configure** tab.</span></span>
2. <span data-ttu-id="5bad7-197">按一下 [新增/編輯儲存體帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="5bad7-197">Click **Add/Edit Storage Accounts**.</span></span>
3. <span data-ttu-id="5bad7-198">在 [hello] 對話方塊中，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="5bad7-198">In hello dialog box, do hello following:</span></span>
   
   1. <span data-ttu-id="5bad7-199">選取 hello 儲存體帳戶與 hello 索引鍵的 toosynchronize。</span><span class="sxs-lookup"><span data-stu-id="5bad7-199">Select hello storage account with hello key that you want toosynchronize.</span></span> <span data-ttu-id="5bad7-200">在顯示時，會加密 hello 儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="5bad7-200">hello storage account keys are encrypted when they are displayed.</span></span>
   2. <span data-ttu-id="5bad7-201">在 hello StorSimple Manager 服務，您會需要 tooupdate hello 金鑰先前已在 hello Microsoft Azure 儲存體服務中變更。</span><span class="sxs-lookup"><span data-stu-id="5bad7-201">In hello StorSimple Manager service, you need tooupdate hello key that was previously changed in hello Microsoft Azure Storage service.</span></span> <span data-ttu-id="5bad7-202">如果 hello 主要存取金鑰已變更 （重新產生），按一下**同步處理主要金鑰**。</span><span class="sxs-lookup"><span data-stu-id="5bad7-202">If hello primary access key was changed (regenerated), click **synchronize primary key**.</span></span> <span data-ttu-id="5bad7-203">如果 hello 次要索引鍵已變更，請按一下**同步處理次要金鑰**。</span><span class="sxs-lookup"><span data-stu-id="5bad7-203">If hello secondary key was changed, click **synchronize secondary key**.</span></span>
      
      ![同步處理金鑰](./media/storsimple-manage-storage-accounts/HCS_KeyRotationStorageAccountSameSubscriptionAsService.png)

#### <a name="toosynchronize-keys-for-storage-accounts-outside-of-hello-service-subscription"></a><span data-ttu-id="5bad7-205">toosynchronize hello 服務訂用帳戶以外的儲存體帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="5bad7-205">toosynchronize keys for storage accounts outside of hello service subscription</span></span>
1. <span data-ttu-id="5bad7-206">在 [hello**服務**頁面上，按一下 hello**設定**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="5bad7-206">On hello **Services** page, click hello **Configure** tab.</span></span>
2. <span data-ttu-id="5bad7-207">按一下 [新增/編輯儲存體帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="5bad7-207">Click **Add/Edit Storage Accounts**.</span></span>
3. <span data-ttu-id="5bad7-208">在 [hello] 對話方塊中，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="5bad7-208">In hello dialog box, do hello following:</span></span>
   
   1. <span data-ttu-id="5bad7-209">選取 hello 儲存體帳戶與 hello 便捷鍵的 tooupdate。</span><span class="sxs-lookup"><span data-stu-id="5bad7-209">Select hello storage account with hello access key that you want tooupdate.</span></span>
   2. <span data-ttu-id="5bad7-210">您必須在 StorSimple Manager 服務的 hello tooupdate hello 儲存體存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="5bad7-210">You will need tooupdate hello storage access key in hello StorSimple Manager service.</span></span> <span data-ttu-id="5bad7-211">在此情況下，您可以看到 hello 儲存體存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="5bad7-211">In this case, you can see hello storage access key.</span></span> <span data-ttu-id="5bad7-212">輸入 hello 新金鑰在 hello**儲存體帳戶存取金鑰**y 方塊。</span><span class="sxs-lookup"><span data-stu-id="5bad7-212">Enter hello new key in hello **Storage Account Access Key**y box.</span></span> 
   3. <span data-ttu-id="5bad7-213">儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="5bad7-213">Save your changes.</span></span> <span data-ttu-id="5bad7-214">現在應已更新您的儲存體帳戶存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="5bad7-214">Your storage account access key should now be updated.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5bad7-215">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5bad7-215">Next steps</span></span>
* <span data-ttu-id="5bad7-216">深入了解 [StorSimple 安全性](storsimple-security.md)。</span><span class="sxs-lookup"><span data-stu-id="5bad7-216">Learn more about [StorSimple security](storsimple-security.md).</span></span>
* <span data-ttu-id="5bad7-217">深入了解[使用您的 StorSimple 裝置 hello StorSimple Manager 服務 tooadminister](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="5bad7-217">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

