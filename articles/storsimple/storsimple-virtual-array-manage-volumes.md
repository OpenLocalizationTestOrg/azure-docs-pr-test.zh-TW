---
title: "管理 StorSimple Virtual Array 上的磁碟區 | Microsoft Docs"
description: "描述 StorSimple 裝置管理員，並說明如何使用它來管理 StorSimple Virtual Array 上的磁碟區。"
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
ms.openlocfilehash: a507bf1866952cb79fa6334fed80c88cd207cd0a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-device-manager-service-to-manage-volumes-on-the-storsimple-virtual-array"></a><span data-ttu-id="e74c2-103">使用 StorSimple 裝置管理員服務管理 StorSimple Virtual Array 上的磁碟區</span><span class="sxs-lookup"><span data-stu-id="e74c2-103">Use StorSimple Device Manager service to manage volumes on the StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="e74c2-104">概觀</span><span class="sxs-lookup"><span data-stu-id="e74c2-104">Overview</span></span>

<span data-ttu-id="e74c2-105">本教學課程說明如何使用 StorSimple 裝置管理員服務，在 StorSimple Virtual Array 上建立和管理磁碟區。</span><span class="sxs-lookup"><span data-stu-id="e74c2-105">This tutorial explains how to use the StorSimple Device Manager service to create and manage volumes on your StorSimple Virtual Array.</span></span>

<span data-ttu-id="e74c2-106">StorSimple 裝置管理員服務是 Azure 入口網站中的一項擴充，可讓您從單一 Web 介面來管理 StorSimple 解決方案。</span><span class="sxs-lookup"><span data-stu-id="e74c2-106">The StorSimple Device Manager service is an extension in the Azure portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="e74c2-107">除了管理共用和磁碟區，您還可以使用 StorSimple 裝置管理員服務來檢視和管理裝置、檢視警示、以及檢視和管理備份原則和備份目錄。</span><span class="sxs-lookup"><span data-stu-id="e74c2-107">In addition to managing shares and volumes, you can use the StorSimple Device Manager service to view and manage devices, view alerts, and view and manage backup policies and the backup catalog.</span></span>

## <a name="volume-types"></a><span data-ttu-id="e74c2-108">磁碟區類型</span><span class="sxs-lookup"><span data-stu-id="e74c2-108">Volume Types</span></span>

<span data-ttu-id="e74c2-109">StorSimple 磁碟區可以是：</span><span class="sxs-lookup"><span data-stu-id="e74c2-109">StorSimple volumes can be:</span></span>

* <span data-ttu-id="e74c2-110">**固定在本機**︰這些磁碟區中的資料永遠停留在陣列上，不會流向雲端。</span><span class="sxs-lookup"><span data-stu-id="e74c2-110">**Locally pinned**: Data in these volumes stays on the array at all times and does not spill to the cloud.</span></span>
* <span data-ttu-id="e74c2-111">**階層式**：這些磁碟區中的資料可能流向雲端。</span><span class="sxs-lookup"><span data-stu-id="e74c2-111">**Tiered**: Data in these volumes can spill to the cloud.</span></span> <span data-ttu-id="e74c2-112">當您建立階層式磁碟區時，大約 10 % 的空間會佈建在本機層，而 90 % 的空間會佈建在雲端。</span><span class="sxs-lookup"><span data-stu-id="e74c2-112">When you create a tiered volume, approximately 10 % of the space is provisioned on the local tier and 90 % of the space is provisioned in the cloud.</span></span> <span data-ttu-id="e74c2-113">舉例來說，如果您佈建 1 TB 的磁碟區，當資料使用階層式磁碟區時，其中 100 GB 會位於本機的空間，900 GB 會位於雲端。</span><span class="sxs-lookup"><span data-stu-id="e74c2-113">For example, if you provisioned a 1 TB volume, 100 GB would reside in the local space and 900 GB would be used in the cloud when the data tiers.</span></span> <span data-ttu-id="e74c2-114">這也意味著，如果裝置的可用空間用盡，您就無法佈建階層式磁碟區 (因為本機層上需要的 10% 無法使用)。</span><span class="sxs-lookup"><span data-stu-id="e74c2-114">This in turn implies that if you run out of all the local space on the device, you cannot provision a tiered volume (because the 10 % required on the local tier will not be available).</span></span>

### <a name="provisioned-capacity"></a><span data-ttu-id="e74c2-115">佈建的容量</span><span class="sxs-lookup"><span data-stu-id="e74c2-115">Provisioned capacity</span></span>
<span data-ttu-id="e74c2-116">請參閱下表以了解每個磁碟區類型的最大佈建容量。</span><span class="sxs-lookup"><span data-stu-id="e74c2-116">Refer to the following table for maximum provisioned capacity for each volume type.</span></span>

| <span data-ttu-id="e74c2-117">**限制識別碼**</span><span class="sxs-lookup"><span data-stu-id="e74c2-117">**Limit identifier**</span></span>                                       | <span data-ttu-id="e74c2-118">**限制**</span><span class="sxs-lookup"><span data-stu-id="e74c2-118">**Limit**</span></span>     |
|------------------------------------------------------------|---------------|
| <span data-ttu-id="e74c2-119">分層磁碟區的大小下限</span><span class="sxs-lookup"><span data-stu-id="e74c2-119">Minimum size of a tiered volume</span></span>                            | <span data-ttu-id="e74c2-120">500 GB</span><span class="sxs-lookup"><span data-stu-id="e74c2-120">500 GB</span></span>        |
| <span data-ttu-id="e74c2-121">分層磁碟區的大小上限</span><span class="sxs-lookup"><span data-stu-id="e74c2-121">Maximum size of a tiered volume</span></span>                            | <span data-ttu-id="e74c2-122">5 TB</span><span class="sxs-lookup"><span data-stu-id="e74c2-122">5 TB</span></span>          |
| <span data-ttu-id="e74c2-123">固定在本機的磁碟區的大小下限</span><span class="sxs-lookup"><span data-stu-id="e74c2-123">Minimum size of a locally pinned volume</span></span>                    | <span data-ttu-id="e74c2-124">50 GB</span><span class="sxs-lookup"><span data-stu-id="e74c2-124">50 GB</span></span>         |
| <span data-ttu-id="e74c2-125">固定在本機的磁碟區的大小上限</span><span class="sxs-lookup"><span data-stu-id="e74c2-125">Maximum size of a locally pinned volume</span></span>                    | <span data-ttu-id="e74c2-126">500 GB</span><span class="sxs-lookup"><span data-stu-id="e74c2-126">500 GB</span></span>        |

## <a name="the-volumes-blade"></a><span data-ttu-id="e74c2-127">[磁碟區] 刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="e74c2-127">The Volumes blade</span></span>
<span data-ttu-id="e74c2-128">StorSimple 服務摘要刀鋒視窗的 [磁碟區] 功能表會顯示給定 StorSimple 陣列上的儲存體磁碟區清單，還可讓您管理它們。</span><span class="sxs-lookup"><span data-stu-id="e74c2-128">The **Volumes** menu on your StorSimple service summary blade displays the list of storage volumes on a given StorSimple array and allows you to manage them.</span></span>

![[磁碟區] 刀鋒視窗](./media/storsimple-virtual-array-manage-volumes/volumes-blade.png)

<span data-ttu-id="e74c2-130">磁碟區是由一系列屬性所組成：</span><span class="sxs-lookup"><span data-stu-id="e74c2-130">A volume consists of a series of attributes:</span></span>

* <span data-ttu-id="e74c2-131">**磁碟區名稱** – 必須是唯一且有助於識別磁碟區的描述性名稱。</span><span class="sxs-lookup"><span data-stu-id="e74c2-131">**Volume Name** – A descriptive name that must be unique and helps identify the volume.</span></span>
* <span data-ttu-id="e74c2-132">**狀態** – 可為連線或離線。</span><span class="sxs-lookup"><span data-stu-id="e74c2-132">**Status** – Can be online or offline.</span></span> <span data-ttu-id="e74c2-133">如果是離線的磁碟區，允許存取使用它的啟動器 (伺服器) 會看不到該磁碟區。</span><span class="sxs-lookup"><span data-stu-id="e74c2-133">If a volume is offline, it is not visible to initiators (servers) that are allowed access to use the volume.</span></span>
* <span data-ttu-id="e74c2-134">**類型** – 指出磁碟區為「分層」(預設值) 或「固定在本機」。</span><span class="sxs-lookup"><span data-stu-id="e74c2-134">**Type** – Indicates whether the volume is **Tiered** (the default) or **Locally pinned**.</span></span>
* <span data-ttu-id="e74c2-135">**容量** – 相較於啟動器 (伺服器) 可儲存的資料總量，指定已用的資料量。</span><span class="sxs-lookup"><span data-stu-id="e74c2-135">**Capacity** – specifies the amount of data used as compared to the total amount of data that can be stored by the initiator (server).</span></span>
* <span data-ttu-id="e74c2-136">**備份** – 如果是 StorSimple Virtual Array，所有磁碟區會自動啟用備份。</span><span class="sxs-lookup"><span data-stu-id="e74c2-136">**Backup** – In case of the StorSimple Virtual Array, all volumes are automatically enabled for backup.</span></span>
* <span data-ttu-id="e74c2-137">**連接的主機** – 指定允許存取此磁碟區的啟動器 (伺服器)。</span><span class="sxs-lookup"><span data-stu-id="e74c2-137">**Connected hosts** – Specifies the initiators (servers) that are allowed access to this volume.</span></span>

![磁碟區詳細資料](./media/storsimple-virtual-array-manage-volumes/volume-details.png)

<span data-ttu-id="e74c2-139">使用本教學課程中的指示以執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="e74c2-139">Use the instructions in this tutorial to perform the following tasks:</span></span>

* <span data-ttu-id="e74c2-140">新增磁碟區</span><span class="sxs-lookup"><span data-stu-id="e74c2-140">Add a volume</span></span>
* <span data-ttu-id="e74c2-141">修改磁碟區</span><span class="sxs-lookup"><span data-stu-id="e74c2-141">Modify a volume</span></span>
* <span data-ttu-id="e74c2-142">使磁碟區離線</span><span class="sxs-lookup"><span data-stu-id="e74c2-142">Take a volume offline</span></span>
* <span data-ttu-id="e74c2-143">刪除磁碟區</span><span class="sxs-lookup"><span data-stu-id="e74c2-143">Delete a volume</span></span>

## <a name="add-a-volume"></a><span data-ttu-id="e74c2-144">新增磁碟區</span><span class="sxs-lookup"><span data-stu-id="e74c2-144">Add a volume</span></span>

1. <span data-ttu-id="e74c2-145">從 StorSimple 服務摘要刀鋒視窗中，從命令列按一下 [+ 新增磁碟區]。</span><span class="sxs-lookup"><span data-stu-id="e74c2-145">From the StorSimple service summary blade, click **+ Add volume** from the command bar.</span></span> <span data-ttu-id="e74c2-146">這會開啟 [新增磁碟區] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e74c2-146">This opens up the **Add volume** blade.</span></span>
   
    ![新增磁碟區](./media/storsimple-virtual-array-manage-volumes/add-volume.png)
2. <span data-ttu-id="e74c2-148">在 [新增磁碟區] 刀鋒視窗中，執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="e74c2-148">In the **Add volume** blade, do the following:</span></span>
   
   * <span data-ttu-id="e74c2-149">在 [磁碟區名稱] 欄位中，輸入磁碟區的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="e74c2-149">In the **Volume name** field, enter a unique name for your volume.</span></span> <span data-ttu-id="e74c2-150">該名稱必須為包含 3 至 127 個字元的字串。</span><span class="sxs-lookup"><span data-stu-id="e74c2-150">The name must be a string that contains 3 to 127 characters.</span></span>
   * <span data-ttu-id="e74c2-151">在 [類型] 下拉式清單中，指定要建立 [階層式] 還是 [固定在本機] 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="e74c2-151">In the **Type** dropdown list, specify whether to create a **Tiered** or **Locally pinned** volume.</span></span> <span data-ttu-id="e74c2-152">對於需要本機保證、低延遲及更高效能的工作負載，請選取 [固定在本機的磁碟區]。</span><span class="sxs-lookup"><span data-stu-id="e74c2-152">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned volume**.</span></span> <span data-ttu-id="e74c2-153">針對所有其他資料，請選取 [階層式] 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="e74c2-153">For all other data, select **Tiered** volume.</span></span>
   * <span data-ttu-id="e74c2-154">在 [容量] 欄位中，指定磁碟區大小。</span><span class="sxs-lookup"><span data-stu-id="e74c2-154">In the **Capacity** field, specify the size of the volume.</span></span> <span data-ttu-id="e74c2-155">階層式磁碟區必須介於 500 GB 和 5 TB 之間，而固定在本機的磁碟區必須介於 50 GB 和 500 GB 之間。</span><span class="sxs-lookup"><span data-stu-id="e74c2-155">A tiered volume must be between 500 GB and 5 TB and a locally pinned volume must be between 50 GB and 500 GB.</span></span>
   * * <span data-ttu-id="e74c2-156">按一下 [連接的主機]，選取存取控制記錄 (ACR) (對應於您要連接至此磁碟區的 iSCSI 啟動器，然後按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="e74c2-156">Click **Connected hosts**, select an access control record (ACR) corresponding to the iSCSI initiator that you want to connect to this volume, and then click **Select**.</span></span>
3. <span data-ttu-id="e74c2-157">若要新增連接的主機，請按一下 [新增]，輸入主機的名稱及其 iSCSI 合格名稱 (IQN)，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="e74c2-157">To add a new connected host, click **Add new**, enter a name for the host and its iSCSI Qualified Name (IQN), and then click **Add**.</span></span>
   
    ![新增磁碟區](./media/storsimple-virtual-array-manage-volumes/volume-add-acr.png)
4. <span data-ttu-id="e74c2-159">磁碟區設定完成之後，按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="e74c2-159">When you've finished configuring your volume, click **Create**.</span></span> <span data-ttu-id="e74c2-160">將會使用指定的設定來建立磁碟區，您會看到成功建立磁碟區的通知。</span><span class="sxs-lookup"><span data-stu-id="e74c2-160">A volume will be created with the specified settings and you will see a notification on the successful creation of the same.</span></span> <span data-ttu-id="e74c2-161">根據預設，磁碟區會啟用備份。</span><span class="sxs-lookup"><span data-stu-id="e74c2-161">By default backup will be enabled for the volume.</span></span>
5. <span data-ttu-id="e74c2-162">若要確認已成功建立磁碟區，請移至 [磁碟區] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e74c2-162">To confirm that the volume was successfully created, go to the **Volumes** blade.</span></span> <span data-ttu-id="e74c2-163">您應該會看到此處列出該磁碟區。</span><span class="sxs-lookup"><span data-stu-id="e74c2-163">You should see the volume listed.</span></span>
   
    ![磁碟區建立成功](./media/storsimple-virtual-array-manage-volumes/volume-success.png)

## <a name="modify-a-volume"></a><span data-ttu-id="e74c2-165">修改磁碟區</span><span class="sxs-lookup"><span data-stu-id="e74c2-165">Modify a volume</span></span>

<span data-ttu-id="e74c2-166">當您需要變更存取磁碟區的主機時，請修改磁碟區。</span><span class="sxs-lookup"><span data-stu-id="e74c2-166">Modify a volume when you need to change the hosts that access the volume.</span></span> <span data-ttu-id="e74c2-167">建立磁碟區之後，就無法修改磁碟區的其他屬性。</span><span class="sxs-lookup"><span data-stu-id="e74c2-167">The other attributes of a volume cannot be modified once the volume has been created.</span></span>

#### <a name="to-modify-a-volume"></a><span data-ttu-id="e74c2-168">若要修改磁碟區</span><span class="sxs-lookup"><span data-stu-id="e74c2-168">To modify a volume</span></span>

1. <span data-ttu-id="e74c2-169">從 StorSimple 服務摘要刀鋒視窗的 [磁碟區] 設定中，選取您想要修改的磁碟區所在的虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="e74c2-169">From the **Volumes** setting on the StorSimple service summary blade, select the virtual array on which the volume you wish you to modify resides.</span></span>
2. <span data-ttu-id="e74c2-170">**選取** 磁碟區，然後按一下 [連接的主機]，以檢視目前連接的主機並修改為不同的伺服器。</span><span class="sxs-lookup"><span data-stu-id="e74c2-170">**Select** the volume and click **Connected hosts** to view the currently connected host and modify it to a different server.</span></span>
   
    ![編輯磁碟區](./media/storsimple-virtual-array-manage-volumes/volume-edit-acr.png)
3. <span data-ttu-id="e74c2-172">按一下 [儲存] 命令列以儲存變更。</span><span class="sxs-lookup"><span data-stu-id="e74c2-172">Save your changes by clicking the **Save** command bar.</span></span> <span data-ttu-id="e74c2-173">將會套用您指定的設定，您會看到通知。</span><span class="sxs-lookup"><span data-stu-id="e74c2-173">Your specified settings will be applied and you will see a notification.</span></span>

## <a name="take-a-volume-offline"></a><span data-ttu-id="e74c2-174">使磁碟區離線</span><span class="sxs-lookup"><span data-stu-id="e74c2-174">Take a volume offline</span></span>

<span data-ttu-id="e74c2-175">您想要修改或刪除磁碟區時，可能需要先使其離線。</span><span class="sxs-lookup"><span data-stu-id="e74c2-175">You may need to take a volume offline when you are planning to modify it or delete it.</span></span> <span data-ttu-id="e74c2-176">當磁碟區離線時，即無法進行讀寫存取。</span><span class="sxs-lookup"><span data-stu-id="e74c2-176">When a volume is offline, it is not available for read-write access.</span></span> <span data-ttu-id="e74c2-177">您必須使主機與裝置上的磁碟區同時離線。</span><span class="sxs-lookup"><span data-stu-id="e74c2-177">You will need to take the volume offline on the host as well as on the device.</span></span>

#### <a name="to-take-a-volume-offline"></a><span data-ttu-id="e74c2-178">若要使磁碟區離線</span><span class="sxs-lookup"><span data-stu-id="e74c2-178">To take a volume offline</span></span>

1. <span data-ttu-id="e74c2-179">請確定有問題的磁碟區不在使用中後，再使其離線。</span><span class="sxs-lookup"><span data-stu-id="e74c2-179">Make sure that the volume in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="e74c2-180">先使主機上的磁碟區離線。</span><span class="sxs-lookup"><span data-stu-id="e74c2-180">Take the volume offline on the host first.</span></span> <span data-ttu-id="e74c2-181">這樣做可以排除任何會造成磁碟區上資料損毀的潛在風險。</span><span class="sxs-lookup"><span data-stu-id="e74c2-181">This eliminates any potential risk of data corruption on the volume.</span></span> <span data-ttu-id="e74c2-182">如需特定步驟，請參閱主機作業系統的指示。</span><span class="sxs-lookup"><span data-stu-id="e74c2-182">For specific steps, refer to the instructions for your host operating system.</span></span>
3. <span data-ttu-id="e74c2-183">在主機上的磁碟區離線之後，請執行下列步驟讓陣列上的磁碟區離線：</span><span class="sxs-lookup"><span data-stu-id="e74c2-183">After the volume on the host is offline, take the volume on the array  offline by performing the following steps:</span></span>
   
   * <span data-ttu-id="e74c2-184">從 StorSimple 服務摘要刀鋒視窗的 [磁碟區] 設定中，選取您想要設為離線的磁碟區所在的虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="e74c2-184">From the **Volumes** setting on the StorSimple service summary blade, select the virtual array on which the volume you wish you to take offline resides.</span></span>
   * <span data-ttu-id="e74c2-185">**選取** 磁碟區，從操作功能表中按一下 [...] (或以滑鼠右鍵按一下此資料列)，然後選取 [離線]。</span><span class="sxs-lookup"><span data-stu-id="e74c2-185">**Select** the volume and click **...** (alternately right-click in this row) and from the context menu, select **Take offline**.</span></span>
     
        ![讓磁碟區離線](./media/storsimple-virtual-array-manage-volumes/volume-offline.png)
   * <span data-ttu-id="e74c2-187">檢閱 [離線] 刀鋒視窗中的資訊，並確認您接受此作業。</span><span class="sxs-lookup"><span data-stu-id="e74c2-187">Review the information in the **Take offline** blade and confirm your acceptance of the operation.</span></span> <span data-ttu-id="e74c2-188">按一下 [離線] 讓磁碟區離線。</span><span class="sxs-lookup"><span data-stu-id="e74c2-188">Click **Take offline** to take the volume offline.</span></span> <span data-ttu-id="e74c2-189">您會看到作業進行中的通知。</span><span class="sxs-lookup"><span data-stu-id="e74c2-189">You will see a notification of the operation in progress.</span></span>
   * <span data-ttu-id="e74c2-190">若要確認磁碟區已成功離線，請移至 [磁碟區] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e74c2-190">To confirm that the volume was successfully taken offline, go to the **Volumes** blade.</span></span> <span data-ttu-id="e74c2-191">您應該會看到磁碟區的狀態為離線。</span><span class="sxs-lookup"><span data-stu-id="e74c2-191">You should see the status of the volume as offline.</span></span>
     
       ![確認磁碟區離線](./media/storsimple-virtual-array-manage-volumes/volume-offline-confirm.png)

## <a name="delete-a-volume"></a><span data-ttu-id="e74c2-193">刪除磁碟區</span><span class="sxs-lookup"><span data-stu-id="e74c2-193">Delete a volume</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e74c2-194">只有當磁碟區離線時，您才能予以刪除。</span><span class="sxs-lookup"><span data-stu-id="e74c2-194">You can delete a volume only if it is offline.</span></span>
> 
> 

<span data-ttu-id="e74c2-195">請完成下列步驟來刪除磁碟區。</span><span class="sxs-lookup"><span data-stu-id="e74c2-195">Complete the following steps to delete a volume.</span></span>

#### <a name="to-delete-a-volume"></a><span data-ttu-id="e74c2-196">若要刪除磁碟區</span><span class="sxs-lookup"><span data-stu-id="e74c2-196">To delete a volume</span></span>

1. <span data-ttu-id="e74c2-197">從 StorSimple 服務摘要刀鋒視窗的 [磁碟區] 設定中，選取您想要刪除的磁碟區所在的虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="e74c2-197">From the **Volumes** setting on the StorSimple service summary blade, select the virtual array on which the volume you wish you to delete resides.</span></span>
2. <span data-ttu-id="e74c2-198">**選取** 磁碟區，從操作功能表中按一下 [...] (或以滑鼠右鍵按一下此資料列)，然後選取 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="e74c2-198">**Select** the volume and click **...** (alternately right-click in this row) and from the context menu, select **Delete**.</span></span>
   
    ![刪除磁碟區](./media/storsimple-virtual-array-manage-volumes/volume-delete.png)
3. <span data-ttu-id="e74c2-200">檢查您想要刪除之磁碟區的狀態。</span><span class="sxs-lookup"><span data-stu-id="e74c2-200">Check the status of the volume you want to delete.</span></span> <span data-ttu-id="e74c2-201">如果您想要刪除的磁碟區未離線，請先使其離線，請依照 [使磁碟區離線](#take-a-volume-offline)中的步驟執行。</span><span class="sxs-lookup"><span data-stu-id="e74c2-201">If the volume you want to delete is not offline, take it offline first, following the steps in [Take a volume offline](#take-a-volume-offline).</span></span>
4. <span data-ttu-id="e74c2-202">當 [刪除]**刪除** 刀鋒視窗中提示您確認時，請接受確認並按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="e74c2-202">When prompted for confirmation in the **Delete** blade, accept the confirmation and click **Delete**.</span></span> <span data-ttu-id="e74c2-203">現在將刪除磁碟區，[磁碟區] 刀鋒視窗會顯示虛擬陣列內更新的磁碟區清單。</span><span class="sxs-lookup"><span data-stu-id="e74c2-203">The volume will now be deleted and the **Volumes** blade will show the updated list of volumes within the virtual array.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e74c2-204">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e74c2-204">Next steps</span></span>

<span data-ttu-id="e74c2-205">了解如何 [複製 StorSimple 磁碟區](storsimple-virtual-array-clone.md)。</span><span class="sxs-lookup"><span data-stu-id="e74c2-205">Learn how to [clone a StorSimple volume](storsimple-virtual-array-clone.md).</span></span>

