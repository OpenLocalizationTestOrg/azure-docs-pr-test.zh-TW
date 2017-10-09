---
title: "在 StorSimple Virtual Array aaaManage 磁碟區 |Microsoft 文件"
description: "描述 hello StorSimple 裝置管理員，並說明如何 toouse 它 toomanage StorSimple 虛擬陣列上的磁碟區。"
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: caa6a26b-b7ba-4a05-b092-1a79450225cf
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: 46aa6d7508b3e62f75a3b78ed73302b88320a0f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-service-toomanage-volumes-on-hello-storsimple-virtual-array"></a><span data-ttu-id="6ee78-103">使用 StorSimple 裝置管理員服務 toomanage 磁碟區上 hello StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="6ee78-103">Use StorSimple Device Manager service toomanage volumes on hello StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="6ee78-104">概觀</span><span class="sxs-lookup"><span data-stu-id="6ee78-104">Overview</span></span>

<span data-ttu-id="6ee78-105">本教學課程將說明 toouse hello StorSimple 裝置管理員服務 toocreate 並管理您的 StorSimple 虛擬陣列上的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="6ee78-105">This tutorial explains how toouse hello StorSimple Device Manager service toocreate and manage volumes on your StorSimple Virtual Array.</span></span>

<span data-ttu-id="6ee78-106">hello StorSimple 裝置管理員服務是 hello Azure 入口網站，可讓您從單一 web 介面來管理您的 StorSimple 解決方案中的延伸模組。</span><span class="sxs-lookup"><span data-stu-id="6ee78-106">hello StorSimple Device Manager service is an extension in hello Azure portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="6ee78-107">在加法 toomanaging 共用和磁碟區中，您可以使用 hello StorSimple 裝置管理員服務 tooview 和管理裝置、 檢視警示，以及檢視和管理備份原則與 hello 備份類別目錄。</span><span class="sxs-lookup"><span data-stu-id="6ee78-107">In addition toomanaging shares and volumes, you can use hello StorSimple Device Manager service tooview and manage devices, view alerts, and view and manage backup policies and hello backup catalog.</span></span>

## <a name="volume-types"></a><span data-ttu-id="6ee78-108">磁碟區類型</span><span class="sxs-lookup"><span data-stu-id="6ee78-108">Volume Types</span></span>

<span data-ttu-id="6ee78-109">StorSimple 磁碟區可以是：</span><span class="sxs-lookup"><span data-stu-id="6ee78-109">StorSimple volumes can be:</span></span>

* <span data-ttu-id="6ee78-110">**固定在本機**： 一直 hello 陣列上這些磁碟區中的資料，並不 spill toohello 雲端。</span><span class="sxs-lookup"><span data-stu-id="6ee78-110">**Locally pinned**: Data in these volumes stays on hello array at all times and does not spill toohello cloud.</span></span>
* <span data-ttu-id="6ee78-111">**分層**： 這些磁碟區中的資料可以 spill toohello 雲端。</span><span class="sxs-lookup"><span data-stu-id="6ee78-111">**Tiered**: Data in these volumes can spill toohello cloud.</span></span> <span data-ttu-id="6ee78-112">當您建立階層式磁碟區時，大約 10%的 hello 空間 hello 本機層上佈建和 90%的 hello 空間 hello 雲端中佈建。</span><span class="sxs-lookup"><span data-stu-id="6ee78-112">When you create a tiered volume, approximately 10 % of hello space is provisioned on hello local tier and 90 % of hello space is provisioned in hello cloud.</span></span> <span data-ttu-id="6ee78-113">例如，如果您佈建 1 TB 磁碟區、 100 GB，也可以位於 hello 本機空間和 900GB 會用在 hello 雲端時 hello 資料層。</span><span class="sxs-lookup"><span data-stu-id="6ee78-113">For example, if you provisioned a 1 TB volume, 100 GB would reside in hello local space and 900 GB would be used in hello cloud when hello data tiers.</span></span> <span data-ttu-id="6ee78-114">這會表示，如果您在 hello 裝置上執行所有 hello 的本機空間不足，無法佈建分層磁碟區 （因為 hello 10%上需要有本機 hello 層將無法使用）。</span><span class="sxs-lookup"><span data-stu-id="6ee78-114">This in turn implies that if you run out of all hello local space on hello device, you cannot provision a tiered volume (because hello 10 % required on hello local tier will not be available).</span></span>

### <a name="provisioned-capacity"></a><span data-ttu-id="6ee78-115">佈建的容量</span><span class="sxs-lookup"><span data-stu-id="6ee78-115">Provisioned capacity</span></span>
<span data-ttu-id="6ee78-116">請參閱下表針對每個磁碟區類型的最大佈建的容量 toohello。</span><span class="sxs-lookup"><span data-stu-id="6ee78-116">Refer toohello following table for maximum provisioned capacity for each volume type.</span></span>

| <span data-ttu-id="6ee78-117">**限制識別碼**</span><span class="sxs-lookup"><span data-stu-id="6ee78-117">**Limit identifier**</span></span>                                       | <span data-ttu-id="6ee78-118">**限制**</span><span class="sxs-lookup"><span data-stu-id="6ee78-118">**Limit**</span></span>     |
|------------------------------------------------------------|---------------|
| <span data-ttu-id="6ee78-119">分層磁碟區的大小下限</span><span class="sxs-lookup"><span data-stu-id="6ee78-119">Minimum size of a tiered volume</span></span>                            | <span data-ttu-id="6ee78-120">500 GB</span><span class="sxs-lookup"><span data-stu-id="6ee78-120">500 GB</span></span>        |
| <span data-ttu-id="6ee78-121">分層磁碟區的大小上限</span><span class="sxs-lookup"><span data-stu-id="6ee78-121">Maximum size of a tiered volume</span></span>                            | <span data-ttu-id="6ee78-122">5 TB</span><span class="sxs-lookup"><span data-stu-id="6ee78-122">5 TB</span></span>          |
| <span data-ttu-id="6ee78-123">固定在本機的磁碟區的大小下限</span><span class="sxs-lookup"><span data-stu-id="6ee78-123">Minimum size of a locally pinned volume</span></span>                    | <span data-ttu-id="6ee78-124">50 GB</span><span class="sxs-lookup"><span data-stu-id="6ee78-124">50 GB</span></span>         |
| <span data-ttu-id="6ee78-125">固定在本機的磁碟區的大小上限</span><span class="sxs-lookup"><span data-stu-id="6ee78-125">Maximum size of a locally pinned volume</span></span>                    | <span data-ttu-id="6ee78-126">500 GB</span><span class="sxs-lookup"><span data-stu-id="6ee78-126">500 GB</span></span>        |

## <a name="hello-volumes-blade"></a><span data-ttu-id="6ee78-127">hello 磁碟區 刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="6ee78-127">hello Volumes blade</span></span>
<span data-ttu-id="6ee78-128">hello**磁碟區**您 StorSimple 服務摘要 刀鋒視窗的功能表顯示 hello 存放磁碟區上指定的 StorSimple 陣列，並可讓您 toomanage 它們。</span><span class="sxs-lookup"><span data-stu-id="6ee78-128">hello **Volumes** menu on your StorSimple service summary blade displays hello list of storage volumes on a given StorSimple array and allows you toomanage them.</span></span>

![[磁碟區] 刀鋒視窗](./media/storsimple-virtual-array-manage-volumes/volumes-blade.png)

<span data-ttu-id="6ee78-130">磁碟區是由一系列屬性所組成：</span><span class="sxs-lookup"><span data-stu-id="6ee78-130">A volume consists of a series of attributes:</span></span>

* <span data-ttu-id="6ee78-131">**磁碟區名稱**– 描述性的名稱必須是唯一的可協助識別 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="6ee78-131">**Volume Name** – A descriptive name that must be unique and helps identify hello volume.</span></span>
* <span data-ttu-id="6ee78-132">**狀態** – 可為連線或離線。</span><span class="sxs-lookup"><span data-stu-id="6ee78-132">**Status** – Can be online or offline.</span></span> <span data-ttu-id="6ee78-133">如果磁碟區已離線，就不允許存取 toouse hello 磁碟區的可見 tooinitiators （伺服器）。</span><span class="sxs-lookup"><span data-stu-id="6ee78-133">If a volume is offline, it is not visible tooinitiators (servers) that are allowed access toouse hello volume.</span></span>
* <span data-ttu-id="6ee78-134">**型別**– 指出 hello 磁碟區是否為**分層**(hello 預設) 或**固定在本機**。</span><span class="sxs-lookup"><span data-stu-id="6ee78-134">**Type** – Indicates whether hello volume is **Tiered** (hello default) or **Locally pinned**.</span></span>
* <span data-ttu-id="6ee78-135">**容量**– 指定 hello 做為比較的 toohello 的 hello 啟動器 （伺服器） 來儲存的資料量總計的資料數量。</span><span class="sxs-lookup"><span data-stu-id="6ee78-135">**Capacity** – specifies hello amount of data used as compared toohello total amount of data that can be stored by hello initiator (server).</span></span>
* <span data-ttu-id="6ee78-136">**備份**– 以防 hello StorSimple Virtual Array 的所有磁碟區會自動啟用備份。</span><span class="sxs-lookup"><span data-stu-id="6ee78-136">**Backup** – In case of hello StorSimple Virtual Array, all volumes are automatically enabled for backup.</span></span>
* <span data-ttu-id="6ee78-137">**連線主機**– 指定允許存取 toothis 磁碟區的 hello 啟動器 （伺服器）。</span><span class="sxs-lookup"><span data-stu-id="6ee78-137">**Connected hosts** – Specifies hello initiators (servers) that are allowed access toothis volume.</span></span>

![磁碟區詳細資料](./media/storsimple-virtual-array-manage-volumes/volume-details.png)

<span data-ttu-id="6ee78-139">使用 hello 指示在本教學課程 tooperform hello，下列工作：</span><span class="sxs-lookup"><span data-stu-id="6ee78-139">Use hello instructions in this tutorial tooperform hello following tasks:</span></span>

* <span data-ttu-id="6ee78-140">新增磁碟區</span><span class="sxs-lookup"><span data-stu-id="6ee78-140">Add a volume</span></span>
* <span data-ttu-id="6ee78-141">修改磁碟區</span><span class="sxs-lookup"><span data-stu-id="6ee78-141">Modify a volume</span></span>
* <span data-ttu-id="6ee78-142">使磁碟區離線</span><span class="sxs-lookup"><span data-stu-id="6ee78-142">Take a volume offline</span></span>
* <span data-ttu-id="6ee78-143">刪除磁碟區</span><span class="sxs-lookup"><span data-stu-id="6ee78-143">Delete a volume</span></span>

## <a name="add-a-volume"></a><span data-ttu-id="6ee78-144">新增磁碟區</span><span class="sxs-lookup"><span data-stu-id="6ee78-144">Add a volume</span></span>

1. <span data-ttu-id="6ee78-145">從 hello StorSimple 服務摘要刀鋒視窗中，按一下 **新增磁碟區 +** hello 命令列。</span><span class="sxs-lookup"><span data-stu-id="6ee78-145">From hello StorSimple service summary blade, click **+ Add volume** from hello command bar.</span></span> <span data-ttu-id="6ee78-146">這會開啟 hello**新增磁碟區**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="6ee78-146">This opens up hello **Add volume** blade.</span></span>
   
    ![新增磁碟區](./media/storsimple-virtual-array-manage-volumes/add-volume.png)
2. <span data-ttu-id="6ee78-148">在 hello**新增磁碟區**刀鋒視窗中，請勿遵循 hello:</span><span class="sxs-lookup"><span data-stu-id="6ee78-148">In hello **Add volume** blade, do hello following:</span></span>
   
   * <span data-ttu-id="6ee78-149">在 hello**磁碟區名稱**欄位中，輸入您的磁碟區的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="6ee78-149">In hello **Volume name** field, enter a unique name for your volume.</span></span> <span data-ttu-id="6ee78-150">hello 名稱必須是包含 3 too127 個字元的字串。</span><span class="sxs-lookup"><span data-stu-id="6ee78-150">hello name must be a string that contains 3 too127 characters.</span></span>
   * <span data-ttu-id="6ee78-151">在 hello**類型**下拉式清單中，指定是否 toocreate**分層**或**固定在本機**磁碟區。</span><span class="sxs-lookup"><span data-stu-id="6ee78-151">In hello **Type** dropdown list, specify whether toocreate a **Tiered** or **Locally pinned** volume.</span></span> <span data-ttu-id="6ee78-152">對於需要本機保證、低延遲及更高效能的工作負載，請選取 [固定在本機的磁碟區]。</span><span class="sxs-lookup"><span data-stu-id="6ee78-152">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned volume**.</span></span> <span data-ttu-id="6ee78-153">針對所有其他資料，請選取 [階層式] 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="6ee78-153">For all other data, select **Tiered** volume.</span></span>
   * <span data-ttu-id="6ee78-154">在 hello**容量**欄位中，指定 hello hello 磁碟區的大小。</span><span class="sxs-lookup"><span data-stu-id="6ee78-154">In hello **Capacity** field, specify hello size of hello volume.</span></span> <span data-ttu-id="6ee78-155">階層式磁碟區必須介於 500 GB 和 5 TB 之間，而固定在本機的磁碟區必須介於 50 GB 和 500 GB 之間。</span><span class="sxs-lookup"><span data-stu-id="6ee78-155">A tiered volume must be between 500 GB and 5 TB and a locally pinned volume must be between 50 GB and 500 GB.</span></span>
   * * <span data-ttu-id="6ee78-156">按一下**連線主機**，選取 存取控制記錄 (ACR) 對應 toohello iSCSI 啟動器您想 tooconnect toothis 磁碟區，然後再按一下**選取**。</span><span class="sxs-lookup"><span data-stu-id="6ee78-156">Click **Connected hosts**, select an access control record (ACR) corresponding toohello iSCSI initiator that you want tooconnect toothis volume, and then click **Select**.</span></span>
3. <span data-ttu-id="6ee78-157">tooadd 新連線的主機，按一下**新增**，輸入的名稱 hello 主機和其 iSCSI 合格名稱 (IQN)，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="6ee78-157">tooadd a new connected host, click **Add new**, enter a name for hello host and its iSCSI Qualified Name (IQN), and then click **Add**.</span></span>
   
    ![新增磁碟區](./media/storsimple-virtual-array-manage-volumes/volume-add-acr.png)
4. <span data-ttu-id="6ee78-159">磁碟區設定完成之後，按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="6ee78-159">When you've finished configuring your volume, click **Create**.</span></span> <span data-ttu-id="6ee78-160">將指定的 hello 與建立磁碟區設定，您會看到在 hello 成功建立 hello 相同的通知。</span><span class="sxs-lookup"><span data-stu-id="6ee78-160">A volume will be created with hello specified settings and you will see a notification on hello successful creation of hello same.</span></span> <span data-ttu-id="6ee78-161">依預設會啟用 hello 磁碟區備份。</span><span class="sxs-lookup"><span data-stu-id="6ee78-161">By default backup will be enabled for hello volume.</span></span>
5. <span data-ttu-id="6ee78-162">hello 磁碟區的 tooconfirm 已成功建立，請移 toohello**磁碟區**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="6ee78-162">tooconfirm that hello volume was successfully created, go toohello **Volumes** blade.</span></span> <span data-ttu-id="6ee78-163">您應該會看到列出的 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="6ee78-163">You should see hello volume listed.</span></span>
   
    ![磁碟區建立成功](./media/storsimple-virtual-array-manage-volumes/volume-success.png)

## <a name="modify-a-volume"></a><span data-ttu-id="6ee78-165">修改磁碟區</span><span class="sxs-lookup"><span data-stu-id="6ee78-165">Modify a volume</span></span>

<span data-ttu-id="6ee78-166">當您需要存取 hello 的磁碟區的 toochange hello 主機時，請修改磁碟區。</span><span class="sxs-lookup"><span data-stu-id="6ee78-166">Modify a volume when you need toochange hello hosts that access hello volume.</span></span> <span data-ttu-id="6ee78-167">hello 磁碟區的其他屬性，即無法修改已建立 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="6ee78-167">hello other attributes of a volume cannot be modified once hello volume has been created.</span></span>

#### <a name="toomodify-a-volume"></a><span data-ttu-id="6ee78-168">toomodify 磁碟區</span><span class="sxs-lookup"><span data-stu-id="6ee78-168">toomodify a volume</span></span>

1. <span data-ttu-id="6ee78-169">從 hello**磁碟區**設定 hello StorSimple 服務摘要 刀鋒視窗上，選取 hello 的 hello toomodify 希望您的磁碟區所在的虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="6ee78-169">From hello **Volumes** setting on hello StorSimple service summary blade, select hello virtual array on which hello volume you wish you toomodify resides.</span></span>
2. <span data-ttu-id="6ee78-170">**選取**hello 磁碟區，然後按一下**連線主機**tooview hello 目前連線的主機，並加以修改 tooa 不同的伺服器。</span><span class="sxs-lookup"><span data-stu-id="6ee78-170">**Select** hello volume and click **Connected hosts** tooview hello currently connected host and modify it tooa different server.</span></span>
   
    ![編輯磁碟區](./media/storsimple-virtual-array-manage-volumes/volume-edit-acr.png)
3. <span data-ttu-id="6ee78-172">儲存您的變更，依序按一下 hello**儲存**命令列。</span><span class="sxs-lookup"><span data-stu-id="6ee78-172">Save your changes by clicking hello **Save** command bar.</span></span> <span data-ttu-id="6ee78-173">將會套用您指定的設定，您會看到通知。</span><span class="sxs-lookup"><span data-stu-id="6ee78-173">Your specified settings will be applied and you will see a notification.</span></span>

## <a name="take-a-volume-offline"></a><span data-ttu-id="6ee78-174">使磁碟區離線</span><span class="sxs-lookup"><span data-stu-id="6ee78-174">Take a volume offline</span></span>

<span data-ttu-id="6ee78-175">您可能需要 tootake 磁碟區離線，當您計劃 toomodify 它或刪除它。</span><span class="sxs-lookup"><span data-stu-id="6ee78-175">You may need tootake a volume offline when you are planning toomodify it or delete it.</span></span> <span data-ttu-id="6ee78-176">當磁碟區離線時，即無法進行讀寫存取。</span><span class="sxs-lookup"><span data-stu-id="6ee78-176">When a volume is offline, it is not available for read-write access.</span></span> <span data-ttu-id="6ee78-177">您將需要 tootake hello 磁碟區離線 hello 裝置以及 hello 主機上。</span><span class="sxs-lookup"><span data-stu-id="6ee78-177">You will need tootake hello volume offline on hello host as well as on hello device.</span></span>

#### <a name="tootake-a-volume-offline"></a><span data-ttu-id="6ee78-178">tootake 磁碟區離線</span><span class="sxs-lookup"><span data-stu-id="6ee78-178">tootake a volume offline</span></span>

1. <span data-ttu-id="6ee78-179">請確定有問題的 hello 磁碟區不是使用中，再將其離線。</span><span class="sxs-lookup"><span data-stu-id="6ee78-179">Make sure that hello volume in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="6ee78-180">Hello 主機上的 hello 磁碟區離線讓第一次。</span><span class="sxs-lookup"><span data-stu-id="6ee78-180">Take hello volume offline on hello host first.</span></span> <span data-ttu-id="6ee78-181">這可免除 hello 磁碟區上的資料損毀的任何潛在風險。</span><span class="sxs-lookup"><span data-stu-id="6ee78-181">This eliminates any potential risk of data corruption on hello volume.</span></span> <span data-ttu-id="6ee78-182">如需特定步驟，請參閱主機作業系統的 toohello 指示。</span><span class="sxs-lookup"><span data-stu-id="6ee78-182">For specific steps, refer toohello instructions for your host operating system.</span></span>
3. <span data-ttu-id="6ee78-183">Hello hello 主機上的磁碟區離線後，採用的 hello 陣列離線 hello 磁碟區，藉由執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="6ee78-183">After hello volume on hello host is offline, take hello volume on hello array  offline by performing hello following steps:</span></span>
   
   * <span data-ttu-id="6ee78-184">從 hello**磁碟區**設定 hello StorSimple 服務摘要 刀鋒視窗上，選取 hello 的 hello 您想 tootake 離線的磁碟區所在的虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="6ee78-184">From hello **Volumes** setting on hello StorSimple service summary blade, select hello virtual array on which hello volume you wish you tootake offline resides.</span></span>
   * <span data-ttu-id="6ee78-185">**選取**hello 磁碟區，然後按一下**...** （或者以滑鼠右鍵按一下此資料列中），然後從 hello 內容功能表中，選取**離線**。</span><span class="sxs-lookup"><span data-stu-id="6ee78-185">**Select** hello volume and click **...** (alternately right-click in this row) and from hello context menu, select **Take offline**.</span></span>
     
        ![讓磁碟區離線](./media/storsimple-virtual-array-manage-volumes/volume-offline.png)
   * <span data-ttu-id="6ee78-187">檢閱在 hello hello 資訊**離線**刀鋒視窗，並確認您接受 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="6ee78-187">Review hello information in hello **Take offline** blade and confirm your acceptance of hello operation.</span></span> <span data-ttu-id="6ee78-188">按一下**離線**tootake hello 磁碟區離線。</span><span class="sxs-lookup"><span data-stu-id="6ee78-188">Click **Take offline** tootake hello volume offline.</span></span> <span data-ttu-id="6ee78-189">您會看到 hello 作業正在進行中的通知。</span><span class="sxs-lookup"><span data-stu-id="6ee78-189">You will see a notification of hello operation in progress.</span></span>
   * <span data-ttu-id="6ee78-190">hello 磁碟區已成功地使其離線的 tooconfirm 移 toohello**磁碟區**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="6ee78-190">tooconfirm that hello volume was successfully taken offline, go toohello **Volumes** blade.</span></span> <span data-ttu-id="6ee78-191">您應該會看到 hello hello 磁碟區狀態為離線。</span><span class="sxs-lookup"><span data-stu-id="6ee78-191">You should see hello status of hello volume as offline.</span></span>
     
       ![確認磁碟區離線](./media/storsimple-virtual-array-manage-volumes/volume-offline-confirm.png)

## <a name="delete-a-volume"></a><span data-ttu-id="6ee78-193">刪除磁碟區</span><span class="sxs-lookup"><span data-stu-id="6ee78-193">Delete a volume</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6ee78-194">只有當磁碟區離線時，您才能予以刪除。</span><span class="sxs-lookup"><span data-stu-id="6ee78-194">You can delete a volume only if it is offline.</span></span>
> 
> 

<span data-ttu-id="6ee78-195">完成下列步驟 toodelete 磁碟區的 hello。</span><span class="sxs-lookup"><span data-stu-id="6ee78-195">Complete hello following steps toodelete a volume.</span></span>

#### <a name="toodelete-a-volume"></a><span data-ttu-id="6ee78-196">toodelete 磁碟區</span><span class="sxs-lookup"><span data-stu-id="6ee78-196">toodelete a volume</span></span>

1. <span data-ttu-id="6ee78-197">從 hello**磁碟區**設定 hello StorSimple 服務摘要 刀鋒視窗上，選取 hello 的 hello toodelete 希望您的磁碟區所在的虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="6ee78-197">From hello **Volumes** setting on hello StorSimple service summary blade, select hello virtual array on which hello volume you wish you toodelete resides.</span></span>
2. <span data-ttu-id="6ee78-198">**選取**hello 磁碟區，然後按一下**...** （或者以滑鼠右鍵按一下此資料列中），然後從 hello 內容功能表中，選取**刪除**。</span><span class="sxs-lookup"><span data-stu-id="6ee78-198">**Select** hello volume and click **...** (alternately right-click in this row) and from hello context menu, select **Delete**.</span></span>
   
    ![刪除磁碟區](./media/storsimple-virtual-array-manage-volumes/volume-delete.png)
3. <span data-ttu-id="6ee78-200">檢查 hello 狀態想 toodelete hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="6ee78-200">Check hello status of hello volume you want toodelete.</span></span> <span data-ttu-id="6ee78-201">如果您想要 toodelete hello 磁碟區未離線，使其離線的第一個步驟，下列 hello 步驟[使磁碟區離線](#take-a-volume-offline)。</span><span class="sxs-lookup"><span data-stu-id="6ee78-201">If hello volume you want toodelete is not offline, take it offline first, following hello steps in [Take a volume offline](#take-a-volume-offline).</span></span>
4. <span data-ttu-id="6ee78-202">當系統提示您確認在 hello**刪除**刀鋒視窗中，接受 hello 確認，然後按一下 **刪除**。</span><span class="sxs-lookup"><span data-stu-id="6ee78-202">When prompted for confirmation in hello **Delete** blade, accept hello confirmation and click **Delete**.</span></span> <span data-ttu-id="6ee78-203">hello 磁碟區現在將會刪除與 hello**磁碟區**刀鋒視窗會顯示更新的 hello hello 虛擬陣列中的磁碟區清單。</span><span class="sxs-lookup"><span data-stu-id="6ee78-203">hello volume will now be deleted and hello **Volumes** blade will show hello updated list of volumes within hello virtual array.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ee78-204">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6ee78-204">Next steps</span></span>

<span data-ttu-id="6ee78-205">了解如何太[複製 StorSimple 磁碟區](storsimple-virtual-array-clone.md)。</span><span class="sxs-lookup"><span data-stu-id="6ee78-205">Learn how too[clone a StorSimple volume](storsimple-virtual-array-clone.md).</span></span>

