---
title: "aaaManage StorSimple Virtual Array 共用 |Microsoft 文件"
description: "描述 hello StorSimple 裝置管理員，並說明如何 toouse 它在您的 StorSimple Virtual Array toomanage 共用。"
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: 0a799c83-fde5-4f3f-af0e-67535d1882b6
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: 9b57d7ec7c0b7de5a22e1b816daa8852d0f32a48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-shares-on-hello-storsimple-virtual-array"></a><span data-ttu-id="71b89-103">在 hello StorSimple Virtual Array 上使用 hello StorSimple 裝置管理員服務 toomanage 共用</span><span class="sxs-lookup"><span data-stu-id="71b89-103">Use hello StorSimple Device Manager service toomanage shares on hello StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="71b89-104">概觀</span><span class="sxs-lookup"><span data-stu-id="71b89-104">Overview</span></span>

<span data-ttu-id="71b89-105">本教學課程將說明 toouse hello StorSimple 裝置管理員服務 toocreate 並管理您的 StorSimple Virtual Array 上的共用。</span><span class="sxs-lookup"><span data-stu-id="71b89-105">This tutorial explains how toouse hello StorSimple Device Manager service toocreate and manage shares on your StorSimple Virtual Array.</span></span>

<span data-ttu-id="71b89-106">hello StorSimple 裝置管理員服務是 hello Azure 入口網站，可讓您從單一 web 介面來管理您的 StorSimple 解決方案中的延伸模組。</span><span class="sxs-lookup"><span data-stu-id="71b89-106">hello StorSimple Device Manager service is an extension in hello Azure portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="71b89-107">在加法 toomanaging 共用和磁碟區中，您可以使用 hello StorSimple 裝置管理員服務 tooview 和管理裝置、 檢視警示、 管理備份原則，以及管理 hello 備份類別目錄。</span><span class="sxs-lookup"><span data-stu-id="71b89-107">In addition toomanaging shares and volumes, you can use hello StorSimple Device Manager service tooview and manage devices, view alerts, manage backup policies, and manage hello backup catalog.</span></span>

## <a name="share-types"></a><span data-ttu-id="71b89-108">共用類型</span><span class="sxs-lookup"><span data-stu-id="71b89-108">Share Types</span></span>

<span data-ttu-id="71b89-109">StorSimple 共用可以是︰</span><span class="sxs-lookup"><span data-stu-id="71b89-109">StorSimple shares can be:</span></span>

* <span data-ttu-id="71b89-110">**固定在本機**： 一直 hello 陣列上這些共用中的資料，並不 spill toohello 雲端。</span><span class="sxs-lookup"><span data-stu-id="71b89-110">**Locally pinned**: Data in these shares stays on hello array at all times and does not spill toohello cloud.</span></span>
* <span data-ttu-id="71b89-111">**分層**： 這些共用中的資料可以 spill toohello 雲端。</span><span class="sxs-lookup"><span data-stu-id="71b89-111">**Tiered**: Data in these shares can spill toohello cloud.</span></span> <span data-ttu-id="71b89-112">當您建立階層式的共用時，大約 10%的 hello 空間 hello 本機層上佈建和 90%的 hello 空間 hello 雲端中佈建。</span><span class="sxs-lookup"><span data-stu-id="71b89-112">When you create a tiered share, approximately 10 % of hello space is provisioned on hello local tier and 90 % of hello space is provisioned in hello cloud.</span></span> <span data-ttu-id="71b89-113">例如，如果您佈建 1 TB 共用、 100 GB，也可以位於 hello 本機空間和 900GB 會用在 hello 雲端時 hello 資料層。</span><span class="sxs-lookup"><span data-stu-id="71b89-113">For example, if you provisioned a 1 TB share, 100 GB would reside in hello local space and 900 GB would be used in hello cloud when hello data tiers.</span></span> <span data-ttu-id="71b89-114">這會表示，如果您在 hello 裝置上執行所有 hello 的本機空間不足，無法佈建階層式的共用 （因為 hello 10%上需要有本機 hello 層將無法使用）。</span><span class="sxs-lookup"><span data-stu-id="71b89-114">This in turn implies that if you run out of all hello local space on hello device, you cannot provision a tiered share (because hello 10 % required on hello local tier will not be available).</span></span>

### <a name="provisioned-capacity"></a><span data-ttu-id="71b89-115">佈建的容量</span><span class="sxs-lookup"><span data-stu-id="71b89-115">Provisioned capacity</span></span>

<span data-ttu-id="71b89-116">請參閱下表針對每個共用類型的最大佈建的容量 toohello。</span><span class="sxs-lookup"><span data-stu-id="71b89-116">Refer toohello following table for maximum provisioned capacity for each share type.</span></span>

| <span data-ttu-id="71b89-117">**限制識別碼**</span><span class="sxs-lookup"><span data-stu-id="71b89-117">**Limit identifier**</span></span> | <span data-ttu-id="71b89-118">**限制**</span><span class="sxs-lookup"><span data-stu-id="71b89-118">**Limit**</span></span> |
| --- | --- |
| <span data-ttu-id="71b89-119">分層共用的大小下限</span><span class="sxs-lookup"><span data-stu-id="71b89-119">Minimum size of a tiered share</span></span> |<span data-ttu-id="71b89-120">500 GB</span><span class="sxs-lookup"><span data-stu-id="71b89-120">500 GB</span></span> |
| <span data-ttu-id="71b89-121">分層共用的大小上限</span><span class="sxs-lookup"><span data-stu-id="71b89-121">Maximum size of a tiered share</span></span> |<span data-ttu-id="71b89-122">20 TB</span><span class="sxs-lookup"><span data-stu-id="71b89-122">20 TB</span></span> |
| <span data-ttu-id="71b89-123">固定在本機的共用的大小下限</span><span class="sxs-lookup"><span data-stu-id="71b89-123">Minimum size of a locally pinned share</span></span> |<span data-ttu-id="71b89-124">50 GB</span><span class="sxs-lookup"><span data-stu-id="71b89-124">50 GB</span></span> |
| <span data-ttu-id="71b89-125">固定在本機的共用的大小上限</span><span class="sxs-lookup"><span data-stu-id="71b89-125">Maximum size of a locally pinned share</span></span> |<span data-ttu-id="71b89-126">2 TB</span><span class="sxs-lookup"><span data-stu-id="71b89-126">2 TB</span></span> |

## <a name="hello-shares-blade"></a><span data-ttu-id="71b89-127">hello 共用刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="71b89-127">hello Shares blade</span></span>

<span data-ttu-id="71b89-128">hello**共用**您 StorSimple 服務摘要 刀鋒視窗的功能表顯示 hello 存放裝置共用指定的 StorSimple 陣列上，並可讓您 toomanage 它們。</span><span class="sxs-lookup"><span data-stu-id="71b89-128">hello **Shares** menu on your StorSimple service summary blade displays hello list of storage shares on a given StorSimple array and allows you toomanage them.</span></span>

![[共用] 刀鋒視窗](./media/storsimple-virtual-array-manage-shares/shares-blade.png)

<span data-ttu-id="71b89-130">共用包含一系列屬性：</span><span class="sxs-lookup"><span data-stu-id="71b89-130">A share consists of a series of attributes:</span></span>

* <span data-ttu-id="71b89-131">**共用名稱**-必須是唯一的且有助於識別 hello 共用的描述性名稱。</span><span class="sxs-lookup"><span data-stu-id="71b89-131">**Share Name** – A descriptive name that must be unique and helps identify hello share.</span></span>
* <span data-ttu-id="71b89-132">**狀態** – 可為連線或離線。</span><span class="sxs-lookup"><span data-stu-id="71b89-132">**Status** – Can be online or offline.</span></span> <span data-ttu-id="71b89-133">如果共用離線，hello 共用的使用者不會無法 tooaccess 它。</span><span class="sxs-lookup"><span data-stu-id="71b89-133">If a share is offline, users of hello share will not be able tooaccess it.</span></span>
* <span data-ttu-id="71b89-134">**型別**– 指出是否 hello 共用**分層**(hello 預設) 或**固定在本機**。</span><span class="sxs-lookup"><span data-stu-id="71b89-134">**Type** – Indicates whether hello share is **Tiered** (hello default) or **Locally pinned**.</span></span>
* <span data-ttu-id="71b89-135">**容量**– 指定 hello 做為比較的 toohello 可以儲存在 hello 共用的資料量總計的資料數量。</span><span class="sxs-lookup"><span data-stu-id="71b89-135">**Capacity** – specifies hello amount of data used as compared toohello total amount of data that can be stored on hello share.</span></span>
* <span data-ttu-id="71b89-136">**描述**– 選擇性的設定，可協助說明 hello 共用。</span><span class="sxs-lookup"><span data-stu-id="71b89-136">**Description** – An optional setting that helps describe hello share.</span></span>
* <span data-ttu-id="71b89-137">**權限**-hello NTFS 權限 toohello 共用可以透過 Windows 檔案總管 進行管理。</span><span class="sxs-lookup"><span data-stu-id="71b89-137">**Permissions** - hello NTFS permissions toohello share that can be managed through Windows Explorer.</span></span>
* <span data-ttu-id="71b89-138">**備份**– 以防的 hello StorSimple Virtual Array，所有共用會自動都啟用備份。</span><span class="sxs-lookup"><span data-stu-id="71b89-138">**Backup** – In case of hello StorSimple Virtual Array, all shares are automatically enabled for backup.</span></span>

![共用的詳細資料](./media/storsimple-virtual-array-manage-shares/share-details.png)

<span data-ttu-id="71b89-140">使用 hello 指示在本教學課程 tooperform hello，下列工作：</span><span class="sxs-lookup"><span data-stu-id="71b89-140">Use hello instructions in this tutorial tooperform hello following tasks:</span></span>

* <span data-ttu-id="71b89-141">新增共用</span><span class="sxs-lookup"><span data-stu-id="71b89-141">Add a share</span></span>
* <span data-ttu-id="71b89-142">修改共用</span><span class="sxs-lookup"><span data-stu-id="71b89-142">Modify a share</span></span>
* <span data-ttu-id="71b89-143">讓共用離線</span><span class="sxs-lookup"><span data-stu-id="71b89-143">Take a share offline</span></span>
* <span data-ttu-id="71b89-144">刪除共用</span><span class="sxs-lookup"><span data-stu-id="71b89-144">Delete a share</span></span>

## <a name="add-a-share"></a><span data-ttu-id="71b89-145">新增共用</span><span class="sxs-lookup"><span data-stu-id="71b89-145">Add a share</span></span>

1. <span data-ttu-id="71b89-146">從 hello StorSimple 服務摘要刀鋒視窗中，按一下  **+ 新增共用**hello 命令列。</span><span class="sxs-lookup"><span data-stu-id="71b89-146">From hello StorSimple service summary blade, click **+ Add share** from hello command bar.</span></span> <span data-ttu-id="71b89-147">這會開啟 hello**新增共用**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="71b89-147">This opens up hello **Add share** blade.</span></span>

    ![新增共用](./media/storsimple-virtual-array-manage-shares/add-share.png)

2. <span data-ttu-id="71b89-149">在 hello**新增共用**刀鋒視窗中，請勿遵循 hello:</span><span class="sxs-lookup"><span data-stu-id="71b89-149">In hello **Add share** blade, do hello following:</span></span>
   
    1. <span data-ttu-id="71b89-150">在 hello**共用名稱**欄位中，輸入您共用的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="71b89-150">In hello **Share name** field, enter a unique name for your share.</span></span> <span data-ttu-id="71b89-151">hello 名稱必須是包含 3 too127 個字元的字串。</span><span class="sxs-lookup"><span data-stu-id="71b89-151">hello name must be a string that contains 3 too127 characters.</span></span>

    2. <span data-ttu-id="71b89-152">選擇性**描述**hello 共用。</span><span class="sxs-lookup"><span data-stu-id="71b89-152">An optional **Description** for hello share.</span></span> <span data-ttu-id="71b89-153">hello 描述可協助識別 hello 共用擁有者。</span><span class="sxs-lookup"><span data-stu-id="71b89-153">hello description will help identify hello share owners.</span></span>

    3. <span data-ttu-id="71b89-154">在 hello**類型**下拉式清單中，指定是否 toocreate**分層**或**固定在本機**共用。</span><span class="sxs-lookup"><span data-stu-id="71b89-154">In hello **Type** dropdown list, specify whether toocreate a **Tiered** or **Locally pinned** share.</span></span> <span data-ttu-id="71b89-155">對於需要本機保證、低延遲，以及高效能的工作負載，請選取 [固定在本機的共用] 。</span><span class="sxs-lookup"><span data-stu-id="71b89-155">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned share**.</span></span> <span data-ttu-id="71b89-156">對於所有其他資料，請選取 [階層式] 共用。</span><span class="sxs-lookup"><span data-stu-id="71b89-156">For all other data, select **Tiered** share.</span></span>

    4. <span data-ttu-id="71b89-157">在 hello**容量**欄位中，指定 hello 共用的 hello 大小。</span><span class="sxs-lookup"><span data-stu-id="71b89-157">In hello **Capacity** field, specify hello size of hello share.</span></span> <span data-ttu-id="71b89-158">階層式共用必須介於 500 GB 和 20 TB 之間，而固定在本機的共用必須介於 50 GB 和 2 TB 之間。</span><span class="sxs-lookup"><span data-stu-id="71b89-158">A tiered share must be between 500 GB and 20 TB and a locally pinned share must be between 50 GB and 2 TB.</span></span>

    5. <span data-ttu-id="71b89-159">在 hello**設為預設的完整權限**欄位中，指派 toohello hello 權限的使用者或正在存取此共用的 hello 群組。</span><span class="sxs-lookup"><span data-stu-id="71b89-159">In hello **Set default full permissions to** field, assign hello permissions toohello user, or hello group that is accessing this share.</span></span> <span data-ttu-id="71b89-160">指定 hello hello 使用者或群組的名稱 hello 使用者在 _john@contoso.com_ 格式。</span><span class="sxs-lookup"><span data-stu-id="71b89-160">Specify hello name of hello user or hello user group in _john@contoso.com_ format.</span></span> <span data-ttu-id="71b89-161">我們建議您使用使用者群組 （而非單一使用者） tooallow 系統管理員權限 tooaccess 這些共用。</span><span class="sxs-lookup"><span data-stu-id="71b89-161">We recommend that you use a user group (instead of a single user) tooallow admin privileges tooaccess these shares.</span></span> <span data-ttu-id="71b89-162">您已指派 hello 權限之後，您可以使用檔案總管 toomodify 這些權限。</span><span class="sxs-lookup"><span data-stu-id="71b89-162">After you have assigned hello permissions here, you can then use File Explorer toomodify these permissions.</span></span>
3. <span data-ttu-id="71b89-163">共用設定完成之後，按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="71b89-163">When you've finished configuring your share, click **Create**.</span></span> <span data-ttu-id="71b89-164">將指定的 hello 與建立的共用設定，您會看到通知。</span><span class="sxs-lookup"><span data-stu-id="71b89-164">A share will be created with hello specified settings and you will see a notification.</span></span> <span data-ttu-id="71b89-165">根據預設，備份將會啟用 hello 共用。</span><span class="sxs-lookup"><span data-stu-id="71b89-165">By default, backup will be enabled for hello share.</span></span>
4. <span data-ttu-id="71b89-166">hello 共用的 tooconfirm 已成功建立，請移 toohello**共用**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="71b89-166">tooconfirm that hello share was successfully created, go toohello **Shares** blade.</span></span> <span data-ttu-id="71b89-167">您應該會看到共用列出 hello。</span><span class="sxs-lookup"><span data-stu-id="71b89-167">You should see hello share listed.</span></span>
   
    ![共用建立成功](./media/storsimple-virtual-array-manage-shares/share-success.png)

## <a name="modify-a-share"></a><span data-ttu-id="71b89-169">修改共用</span><span class="sxs-lookup"><span data-stu-id="71b89-169">Modify a share</span></span>

<span data-ttu-id="71b89-170">當您需要 toochange hello 描述 hello 共用時，請修改共用。</span><span class="sxs-lookup"><span data-stu-id="71b89-170">Modify a share when you need toochange hello description of hello share.</span></span> <span data-ttu-id="71b89-171">建立 hello 共用之後，就可以修改其他的共用屬性。</span><span class="sxs-lookup"><span data-stu-id="71b89-171">No other share properties can be modified once hello share is created.</span></span>

#### <a name="toomodify-a-share"></a><span data-ttu-id="71b89-172">toomodify 共用</span><span class="sxs-lookup"><span data-stu-id="71b89-172">toomodify a share</span></span>

1. <span data-ttu-id="71b89-173">從 hello**共用**設定 hello StorSimple 服務摘要 刀鋒視窗上，選取 hello 的 hello toomodify 希望您的共用所在的虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="71b89-173">From hello **Shares** setting on hello StorSimple service summary blade, select hello virtual array on which hello share you wish you toomodify resides.</span></span>
2. <span data-ttu-id="71b89-174">**選取**hello 共用 tooview hello 目前描述，並加以修改。</span><span class="sxs-lookup"><span data-stu-id="71b89-174">**Select** hello share tooview hello current description and modify it.</span></span>
3. <span data-ttu-id="71b89-175">儲存您的變更，依序按一下 hello**儲存**命令列。</span><span class="sxs-lookup"><span data-stu-id="71b89-175">Save your changes by clicking hello **Save** command bar.</span></span> <span data-ttu-id="71b89-176">將會套用您指定的設定，您會看到通知。</span><span class="sxs-lookup"><span data-stu-id="71b89-176">Your specified settings will be applied and you will see a notification.</span></span>
   
    ![ <span data-ttu-id="71b89-177">編輯共用</span><span class="sxs-lookup"><span data-stu-id="71b89-177">Edit share</span></span>](./media/storsimple-virtual-array-manage-shares/share-edit.png)

## <a name="take-a-share-offline"></a><span data-ttu-id="71b89-178">讓共用離線</span><span class="sxs-lookup"><span data-stu-id="71b89-178">Take a share offline</span></span>

<span data-ttu-id="71b89-179">您可能需要 tootake 的共用離線，當您計劃 toomodify 它或刪除它。</span><span class="sxs-lookup"><span data-stu-id="71b89-179">You may need tootake a share offline when you are planning toomodify it or delete it.</span></span> <span data-ttu-id="71b89-180">當共用已離線時，即無法進行讀寫存取。</span><span class="sxs-lookup"><span data-stu-id="71b89-180">When a share is offline, it is not available for read-write access.</span></span> <span data-ttu-id="71b89-181">您將需要 tootake hello 共用離線 hello 裝置以及 hello 主機上。</span><span class="sxs-lookup"><span data-stu-id="71b89-181">You will need tootake hello share offline on hello host as well as on hello device.</span></span>

#### <a name="tootake-a-share-offline"></a><span data-ttu-id="71b89-182">tootake 的共用離線</span><span class="sxs-lookup"><span data-stu-id="71b89-182">tootake a share offline</span></span>

1. <span data-ttu-id="71b89-183">請確定有問題該 hello 共用不是使用中，再將其離線。</span><span class="sxs-lookup"><span data-stu-id="71b89-183">Make sure that hello share in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="71b89-184">藉由執行下列步驟的 hello hello 陣列離線採用 hello 共用：</span><span class="sxs-lookup"><span data-stu-id="71b89-184">Take hello share on hello array offline by performing hello following steps:</span></span>
   
    1. <span data-ttu-id="71b89-185">從 hello**共用**設定 hello StorSimple 服務摘要 刀鋒視窗上，選取 hello 的 hello tootake 離線希望您的共用所在的虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="71b89-185">From hello **Shares** setting on hello StorSimple service summary blade, select hello virtual array on which hello share you wish you tootake offline resides.</span></span>

    2. <span data-ttu-id="71b89-186">**選取**hello 共用，然後按一下**...** （或者以滑鼠右鍵按一下此資料列中），然後從 hello 內容功能表中，選取**離線**。</span><span class="sxs-lookup"><span data-stu-id="71b89-186">**Select** hello share and Click **...** (alternately right-click in this row) and from hello context menu, select **Take offline**.</span></span>
     
        ![離線共用](./media/storsimple-virtual-array-manage-shares/shares-offline.png)

    3. <span data-ttu-id="71b89-188">檢閱在 hello hello 資訊**離線**刀鋒視窗，並確認您接受 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="71b89-188">Review hello information in hello **Take offline** blade and confirm your acceptance of hello operation.</span></span> <span data-ttu-id="71b89-189">按一下**離線**tootake hello 共用離線。</span><span class="sxs-lookup"><span data-stu-id="71b89-189">Click **Take offline** tootake hello share offline.</span></span> <span data-ttu-id="71b89-190">您會看到 hello 作業正在進行中的通知。</span><span class="sxs-lookup"><span data-stu-id="71b89-190">You will see a notification of hello operation in progress.</span></span>

    4. <span data-ttu-id="71b89-191">hello 共用的 tooconfirm 已成功取得離線，請移 toohello**共用**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="71b89-191">tooconfirm that hello share was successfully taken offline, go toohello **Shares** blade.</span></span> <span data-ttu-id="71b89-192">您應該會看到 hello hello 共用為離線狀態。</span><span class="sxs-lookup"><span data-stu-id="71b89-192">You should see hello status of hello share as offline.</span></span>

## <a name="delete-a-share"></a><span data-ttu-id="71b89-193">刪除共用</span><span class="sxs-lookup"><span data-stu-id="71b89-193">Delete a share</span></span>

> [!IMPORTANT]
> <span data-ttu-id="71b89-194">只有已離線的共用才能刪除。</span><span class="sxs-lookup"><span data-stu-id="71b89-194">You can delete a share only if it is offline.</span></span>


<span data-ttu-id="71b89-195">完成下列步驟 toodelete 共用 hello。</span><span class="sxs-lookup"><span data-stu-id="71b89-195">Complete hello following steps toodelete a share.</span></span>

#### <a name="toodelete-a-share"></a><span data-ttu-id="71b89-196">toodelete 共用</span><span class="sxs-lookup"><span data-stu-id="71b89-196">toodelete a share</span></span>

1. <span data-ttu-id="71b89-197">從 hello**共用**設定 hello StorSimple 服務摘要 刀鋒視窗上，選取 hello 您想在哪一個 hello 共用 toodelete 所在的虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="71b89-197">From hello **Shares** setting on hello StorSimple service summary blade, select hello virtual array on which hello share you wish toodelete resides.</span></span>
2. <span data-ttu-id="71b89-198">**選取**hello 共用，然後按一下**...** （或者以滑鼠右鍵按一下此資料列中），然後從 hello 內容功能表中，選取**刪除**。</span><span class="sxs-lookup"><span data-stu-id="71b89-198">**Select** hello share and Click **...** (alternately right-click in this row) and from hello context menu, select **Delete**.</span></span>
   
    ![刪除共用](./media/storsimple-virtual-array-manage-shares/share-delete.png)
3. <span data-ttu-id="71b89-200">檢查 hello 狀態要 toodelete hello 共用。</span><span class="sxs-lookup"><span data-stu-id="71b89-200">Check hello status of hello share you want toodelete.</span></span> <span data-ttu-id="71b89-201">如果您想要 toodelete hello 共用未離線，先使其離線。</span><span class="sxs-lookup"><span data-stu-id="71b89-201">If hello share you want toodelete is not offline, take it offline first.</span></span> <span data-ttu-id="71b89-202">中的 hello 步驟[離線工作共用](#take-a-share-offline)。</span><span class="sxs-lookup"><span data-stu-id="71b89-202">Follow hello steps in [Take a share offline](#take-a-share-offline).</span></span>
4. <span data-ttu-id="71b89-203">當系統提示您確認在 hello**刪除**刀鋒視窗中，接受 hello 確認，然後按一下 **刪除**。</span><span class="sxs-lookup"><span data-stu-id="71b89-203">When prompted for confirmation in hello **Delete** blade, accept hello confirmation and click **Delete**.</span></span> <span data-ttu-id="71b89-204">hello 共用現在將會刪除與 hello**共用**刀鋒視窗會顯示 hello 虛擬陣列中的共用 hello 更新清單。</span><span class="sxs-lookup"><span data-stu-id="71b89-204">hello share will now be deleted and hello **Shares** blade shows hello updated list of shares within hello virtual array.</span></span>

## <a name="next-steps"></a><span data-ttu-id="71b89-205">後續步驟</span><span class="sxs-lookup"><span data-stu-id="71b89-205">Next steps</span></span>
<span data-ttu-id="71b89-206">了解如何太[複製 StorSimple 共用](storsimple-virtual-array-clone.md)。</span><span class="sxs-lookup"><span data-stu-id="71b89-206">Learn how too[clone a StorSimple share](storsimple-virtual-array-clone.md).</span></span>

