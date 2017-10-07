---
title: "aaaDeactivate 和刪除 StorSimple 8000 系列裝置 |Microsoft 文件"
description: "描述如何從服務，方法是先停用後再將其刪除 tooremove StorSimple 裝置。"
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: alkohli
ms.openlocfilehash: 841ecd7f0fb5e425bf23e1fe0044faeab2af4b53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-device"></a><span data-ttu-id="27cce-103">停用及刪除 StorSimple 裝置</span><span class="sxs-lookup"><span data-stu-id="27cce-103">Deactivate and delete a StorSimple device</span></span>

## <a name="overview"></a><span data-ttu-id="27cce-104">概觀</span><span class="sxs-lookup"><span data-stu-id="27cce-104">Overview</span></span>

<span data-ttu-id="27cce-105">本文說明如何 toodeactivate 並刪除已連接的 tooa StorSimple 裝置管理員服務的 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="27cce-105">This article describes how toodeactivate and delete a StorSimple device that is connected tooa StorSimple Device Manager service.</span></span> <span data-ttu-id="27cce-106">這篇文章中的 hello 指導方針適用於只有 tooStorSimple 8000 系列裝置包括 hello StorSimple 雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="27cce-106">hello guidance in this article applies only tooStorSimple 8000 series devices including hello StorSimple Cloud Appliances.</span></span> <span data-ttu-id="27cce-107">如果您使用 StorSimple Virtual Array，然後跳過[停用及刪除 StorSimple Virtual Array](storsimple-virtual-array-deactivate-and-delete-device.md)。</span><span class="sxs-lookup"><span data-stu-id="27cce-107">If you are using a StorSimple Virtual Array, then go too[Deactivate and delete a StorSimple Virtual Array](storsimple-virtual-array-deactivate-and-delete-device.md).</span></span>

<span data-ttu-id="27cce-108">停用伺服器 hello hello 裝置與之間連線 hello 相對應的 StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="27cce-108">Deactivation severs hello connection between hello device and hello corresponding StorSimple Device Manager service.</span></span> <span data-ttu-id="27cce-109">您可能會想 tootake 汰 StorSimple 裝置 （例如，如果您要取代或升級您的裝置，或您不再需要使用 StorSimple）。</span><span class="sxs-lookup"><span data-stu-id="27cce-109">You may wish tootake a StorSimple device out of service (for example, if you are replacing or upgrading your device or if you are no longer using StorSimple).</span></span> <span data-ttu-id="27cce-110">如果是這樣，您需要 toodeactivate hello 裝置，才能刪除它。</span><span class="sxs-lookup"><span data-stu-id="27cce-110">If so, you need toodeactivate hello device before you can delete it.</span></span>

<span data-ttu-id="27cce-111">當您停用裝置時，已無法存取任何已儲存在本機 hello 裝置的資料。</span><span class="sxs-lookup"><span data-stu-id="27cce-111">When you deactivate a device, any data that was stored locally on hello device is no longer accessible.</span></span> <span data-ttu-id="27cce-112">只會 hello 與 hello 裝置 hello 雲端中儲存相關聯的資料可以復原。</span><span class="sxs-lookup"><span data-stu-id="27cce-112">Only hello data associated with hello device that was stored in hello cloud can be recovered.</span></span>

> [!WARNING]
> <span data-ttu-id="27cce-113">停用是永久性的作業，而且無法復原。</span><span class="sxs-lookup"><span data-stu-id="27cce-113">Deactivation is a PERMANENT operation and cannot be undone.</span></span> <span data-ttu-id="27cce-114">已停用的裝置無法登錄以 hello StorSimple 裝置管理員服務，除非它是重設 toofactory 預設值。</span><span class="sxs-lookup"><span data-stu-id="27cce-114">A deactivated device cannot be registered with hello StorSimple Device Manager service unless it is reset toofactory defaults.</span></span>
>
> <span data-ttu-id="27cce-115">hello 原廠重設程序會刪除已儲存在本機裝置的所有 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="27cce-115">hello factory reset process deletes all hello data that was stored locally on your device.</span></span> <span data-ttu-id="27cce-116">因此，在您停用裝置之前，您必須擷取所有資料的雲端快照。</span><span class="sxs-lookup"><span data-stu-id="27cce-116">Therefore, you must take a cloud snapshot of all your data before you deactivate a device.</span></span> <span data-ttu-id="27cce-117">此雲端快照可讓您 toorecover 所有 hello 資料在後續階段。</span><span class="sxs-lookup"><span data-stu-id="27cce-117">This cloud snapshot allows you toorecover all hello data at a later stage.</span></span>

<span data-ttu-id="27cce-118">閱讀本教學課程之後，您將能夠：</span><span class="sxs-lookup"><span data-stu-id="27cce-118">After reading this tutorial, you will be able to:</span></span>

* <span data-ttu-id="27cce-119">停用的裝置，並刪除 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="27cce-119">Deactivate a device and delete hello data.</span></span>
* <span data-ttu-id="27cce-120">停用的裝置，並保留 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="27cce-120">Deactivate a device and retain hello data.</span></span>

> [!NOTE]
> <span data-ttu-id="27cce-121">在您停用 StorSimple 實體裝置或雲端設備之前，請停止或刪除相依於該裝置的用戶端和主機。</span><span class="sxs-lookup"><span data-stu-id="27cce-121">Before you deactivate a StorSimple physical device or cloud appliance, stop or delete clients and hosts that depend on that device.</span></span>


## <a name="deactivate-and-delete-data"></a><span data-ttu-id="27cce-122">停用及刪除資料</span><span class="sxs-lookup"><span data-stu-id="27cce-122">Deactivate and delete data</span></span>

<span data-ttu-id="27cce-123">如果您想要完全刪除 hello 裝置並不想 tooretain hello 資料 hello 裝置上的，然後完成下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="27cce-123">If you are interested in deleting hello device completely and do not want tooretain hello data on hello device, then complete hello following steps.</span></span>

#### <a name="toodeactivate-hello-device-and-delete-hello-data"></a><span data-ttu-id="27cce-124">toodeactivate hello 裝置和 delete hello 資料</span><span class="sxs-lookup"><span data-stu-id="27cce-124">toodeactivate hello device and delete hello data</span></span>

1. <span data-ttu-id="27cce-125">停用裝置之前，您必須刪除所有 hello 磁碟區容器 （和 hello 磁碟區） 與 hello 裝置相關聯。</span><span class="sxs-lookup"><span data-stu-id="27cce-125">Before you deactivate a device, you must delete all hello volume containers (and hello volumes) associated with hello device.</span></span> <span data-ttu-id="27cce-126">只在您刪除相關聯的 hello 備份之後，您可以刪除磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="27cce-126">You can delete volume containers only after you have deleted hello associated backups.</span></span>

    > [!NOTE]
    > <span data-ttu-id="27cce-127">您停用 StorSimple 實體裝置或雲端應用裝置之前，請確定從 hello 裝置會實際刪除 hello hello 刪除磁碟區容器中的資料。</span><span class="sxs-lookup"><span data-stu-id="27cce-127">Before you deactivate a StorSimple physical device or cloud appliance, ensure that hello data from hello deleted volume container is actually deleted from hello device.</span></span> <span data-ttu-id="27cce-128">您可以監視 hello 雲端耗用量圖表，以及當您看見 hello 雲端使用量卸除，因為已刪除的 hello 備份，則可繼續 toodeactivate hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="27cce-128">You can monitor hello cloud consumption charts and when you see hello cloud usage drop because of hello backups you have deleted, then you can proceed toodeactivate hello device.</span></span> <span data-ttu-id="27cce-129">如果您停用之前的 hello 裝置此下拉式清單就會發生，hello 資料困在 hello 儲存體帳戶和累算費用。</span><span class="sxs-lookup"><span data-stu-id="27cce-129">If you deactivate hello device before this drop occurs, hello data is stranded in hello storage account and accrues charges.</span></span>

2. <span data-ttu-id="27cce-130">如下所示停用裝置 hello:</span><span class="sxs-lookup"><span data-stu-id="27cce-130">Deactivate hello device as follows:</span></span>
   
   1. <span data-ttu-id="27cce-131">移 tooyour StorSimple 裝置管理員服務，然後按一下**裝置**。</span><span class="sxs-lookup"><span data-stu-id="27cce-131">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="27cce-132">在 hello**裝置**刀鋒視窗中，選取 hello 裝置 toodeactivate、 按一下滑鼠右鍵，然後再按一下您想**停用**。</span><span class="sxs-lookup"><span data-stu-id="27cce-132">In hello **Devices** blade, select hello device that you wish toodeactivate, right-click, and then click **Deactivate**.</span></span>

        ![停用 StorSimple 裝置](./media/storsimple-8000-deactivate-and-delete-device/deactivate1.png)
   2. <span data-ttu-id="27cce-134">在 hello**停用**刀鋒視窗中，輸入 hello 裝置名稱 tooconfirm，然後按一下**停用**。</span><span class="sxs-lookup"><span data-stu-id="27cce-134">In hello **Deactivate** blade, type hello device name tooconfirm and then click **Deactivate**.</span></span> <span data-ttu-id="27cce-135">hello 停用程序會啟動並在幾分鐘的時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="27cce-135">hello deactivate process starts and takes a few minutes toocomplete.</span></span>

        ![停用 StorSimple 裝置](./media/storsimple-8000-deactivate-and-delete-device/deactivate2.png)

3. <span data-ttu-id="27cce-137">停用之後，您可以完全刪除 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="27cce-137">After deactivation, you can delete hello device completely.</span></span> <span data-ttu-id="27cce-138">刪除裝置，即會從裝置連接的 toohello 服務的 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="27cce-138">Deleting a device removes it from hello list of devices connected toohello service.</span></span> <span data-ttu-id="27cce-139">hello 服務可以再管理 hello 刪除裝置。</span><span class="sxs-lookup"><span data-stu-id="27cce-139">hello service can then no longer manage hello deleted device.</span></span> <span data-ttu-id="27cce-140">使用下列步驟 toodelete hello 裝置 hello:</span><span class="sxs-lookup"><span data-stu-id="27cce-140">Use hello following steps toodelete hello device:</span></span>
   
   1. <span data-ttu-id="27cce-141">移 tooyour StorSimple 裝置管理員服務，然後按一下**裝置**。</span><span class="sxs-lookup"><span data-stu-id="27cce-141">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="27cce-142">在 hello**裝置**刀鋒視窗中，選取 hello 停用裝置 toodelete、 按一下滑鼠右鍵，然後再按一下您想**刪除**。</span><span class="sxs-lookup"><span data-stu-id="27cce-142">In hello **Devices** blade, select hello deactivated device that you wish toodelete, right-click, and then click **Delete**.</span></span>

        ![停用 StorSimple 裝置](./media/storsimple-8000-deactivate-and-delete-device/deactivate5.png)
   2. <span data-ttu-id="27cce-144">在 hello**刪除**刀鋒視窗中，輸入 hello 裝置名稱 tooconfirm，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="27cce-144">In hello **Delete** blade, type hello device name tooconfirm and then click **Delete**.</span></span> <span data-ttu-id="27cce-145">hello 可能需要幾分鐘的時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="27cce-145">hello deletion takes a few minutes toocomplete.</span></span>

        ![停用 StorSimple 裝置](./media/storsimple-8000-deactivate-and-delete-device/deactivate6.png)
   3. <span data-ttu-id="27cce-147">已成功完成 hello 刪除之後，您會收到通知。</span><span class="sxs-lookup"><span data-stu-id="27cce-147">After hello deletion is successfully complete, you are notified.</span></span> <span data-ttu-id="27cce-148">hello 裝置清單也會更新 tooreflect hello 刪除。</span><span class="sxs-lookup"><span data-stu-id="27cce-148">hello device list also updates tooreflect hello deletion.</span></span>

## <a name="deactivate-and-retain-data"></a><span data-ttu-id="27cce-149">停用並保留資料</span><span class="sxs-lookup"><span data-stu-id="27cce-149">Deactivate and retain data</span></span>

<span data-ttu-id="27cce-150">如果您有興趣刪除 hello 裝置，但想 tooretain hello 資料，然後完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="27cce-150">If you are interested in deleting hello device but want tooretain hello data, then complete hello following steps:</span></span>

#### <a name="toodeactivate-a-device-and-retain-hello-data"></a><span data-ttu-id="27cce-151">toodeactivate 裝置並 hello 資料保留</span><span class="sxs-lookup"><span data-stu-id="27cce-151">toodeactivate a device and retain hello data</span></span>
1. <span data-ttu-id="27cce-152">停用 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="27cce-152">Deactivate hello device.</span></span> <span data-ttu-id="27cce-153">所有 hello 磁碟區容器和的 hello 裝置 hello 快照集會保留。</span><span class="sxs-lookup"><span data-stu-id="27cce-153">All hello volume containers and hello snapshots of hello device remain.</span></span>
   
   1. <span data-ttu-id="27cce-154">移 tooyour StorSimple 裝置管理員服務，然後按一下**裝置**。</span><span class="sxs-lookup"><span data-stu-id="27cce-154">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="27cce-155">在 hello**裝置**刀鋒視窗中，選取 hello 裝置 toodeactivate、 按一下滑鼠右鍵，然後再按一下您想**停用**。</span><span class="sxs-lookup"><span data-stu-id="27cce-155">In hello **Devices** blade, select hello device that you wish toodeactivate, right-click, and then click **Deactivate**.</span></span>

         ![停用 StorSimple 裝置](./media/storsimple-8000-deactivate-and-delete-device/deactivate1.png)
   2. <span data-ttu-id="27cce-157">在 hello**停用**刀鋒視窗中，輸入 hello 裝置名稱 tooconfirm，然後按一下**停用**。</span><span class="sxs-lookup"><span data-stu-id="27cce-157">In hello **Deactivate** blade, type hello device name tooconfirm and then click **Deactivate**.</span></span> <span data-ttu-id="27cce-158">hello 停用程序會啟動並在幾分鐘的時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="27cce-158">hello deactivate process starts and takes a few minutes toocomplete.</span></span>

         ![停用 StorSimple 裝置](./media/storsimple-8000-deactivate-and-delete-device/deactivate2.png)
2. <span data-ttu-id="27cce-160">您現在可以容錯移轉 hello 磁碟區容器和相關聯的 hello 快照集。</span><span class="sxs-lookup"><span data-stu-id="27cce-160">You can now fail over hello volume containers and hello associated snapshots.</span></span> <span data-ttu-id="27cce-161">程序，跳過[StorSimple 裝置的容錯移轉和災害復原](storsimple-8000-device-failover-disaster-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="27cce-161">For procedures, go too[Failover and disaster recovery for your StorSimple device](storsimple-8000-device-failover-disaster-recovery.md).</span></span>
3. <span data-ttu-id="27cce-162">停用和容錯移轉之後, 您可以完全刪除 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="27cce-162">After deactivation and failover, you can delete hello device completely.</span></span> <span data-ttu-id="27cce-163">刪除裝置，即會從裝置連接的 toohello 服務的 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="27cce-163">Deleting a device removes it from hello list of devices connected toohello service.</span></span> <span data-ttu-id="27cce-164">hello 服務可以再管理 hello 刪除裝置。</span><span class="sxs-lookup"><span data-stu-id="27cce-164">hello service can then no longer manage hello deleted device.</span></span> <span data-ttu-id="27cce-165">完成下列步驟的 hello toodelete hello 裝置：</span><span class="sxs-lookup"><span data-stu-id="27cce-165">toodelete hello device, complete hello following steps:</span></span>
   
   1. <span data-ttu-id="27cce-166">移 tooyour StorSimple 裝置管理員服務，然後按一下**裝置**。</span><span class="sxs-lookup"><span data-stu-id="27cce-166">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="27cce-167">在 hello**裝置**刀鋒視窗中，選取 hello 停用裝置 toodelete、 按一下滑鼠右鍵，然後再按一下您想**刪除**。</span><span class="sxs-lookup"><span data-stu-id="27cce-167">In hello **Devices** blade, select hello deactivated device that you wish toodelete, right-click, and then click **Delete**.</span></span>

       ![停用 StorSimple 裝置](./media/storsimple-8000-deactivate-and-delete-device/deactivate5.png)
   2. <span data-ttu-id="27cce-169">在 hello**刪除**刀鋒視窗中，輸入 hello 裝置名稱 tooconfirm，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="27cce-169">In hello **Delete** blade, type hello device name tooconfirm and then click **Delete**.</span></span> <span data-ttu-id="27cce-170">hello 可能需要幾分鐘的時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="27cce-170">hello deletion takes a few minutes toocomplete.</span></span>

       ![停用 StorSimple 裝置](./media/storsimple-8000-deactivate-and-delete-device/deactivate6.png)
   3. <span data-ttu-id="27cce-172">已成功完成 hello 刪除之後，您會收到通知。</span><span class="sxs-lookup"><span data-stu-id="27cce-172">After hello deletion is successfully complete, you are notified.</span></span> <span data-ttu-id="27cce-173">hello 裝置清單也會更新 tooreflect hello 刪除。</span><span class="sxs-lookup"><span data-stu-id="27cce-173">hello device list also updates tooreflect hello deletion.</span></span>

     
## <a name="deactivate-and-delete-a-cloud-appliance"></a><span data-ttu-id="27cce-174">停用及刪除雲端設備</span><span class="sxs-lookup"><span data-stu-id="27cce-174">Deactivate and delete a cloud appliance</span></span>

<span data-ttu-id="27cce-175">為 StorSimple 雲端應用裝置中，從 hello 入口網站停用取消配置，並刪除 hello 虛擬機器，與 hello 資源建立時已佈建。</span><span class="sxs-lookup"><span data-stu-id="27cce-175">For a StorSimple Cloud Appliance, deactivation from hello portal deallocates and deletes hello virtual machine, and hello resources created when it was provisioned.</span></span> <span data-ttu-id="27cce-176">Hello 雲端應用裝置已停用之後，它不能還原 tooits 先前的狀態。</span><span class="sxs-lookup"><span data-stu-id="27cce-176">After hello cloud appliance is deactivated, it cannot be restored tooits previous state.</span></span>

![停用 StorSimple 雲端設備](./media/storsimple-8000-deactivate-and-delete-device/deactivate7.png)

<span data-ttu-id="27cce-178">停用產生 hello 下列動作：</span><span class="sxs-lookup"><span data-stu-id="27cce-178">Deactivation results in hello following actions:</span></span>

* <span data-ttu-id="27cce-179">hello StorSimple 雲端應用裝置會從 hello 服務移除。</span><span class="sxs-lookup"><span data-stu-id="27cce-179">hello StorSimple Cloud Appliance is removed from hello service.</span></span>
* <span data-ttu-id="27cce-180">刪除 hello hello StorSimple 雲端應用裝置的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="27cce-180">hello virtual machine for hello StorSimple Cloud Appliance is deleted.</span></span>
* <span data-ttu-id="27cce-181">hello OS 磁碟和資料磁碟建立 hello StorSimple 雲端應用裝置會移除。</span><span class="sxs-lookup"><span data-stu-id="27cce-181">hello OS disk and data disks created for hello StorSimple Cloud Appliance are removed.</span></span>
* <span data-ttu-id="27cce-182">保留 hello 裝載服務和已佈建期間建立的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="27cce-182">hello hosted service and Virtual Network that were created during provisioning are retained.</span></span> <span data-ttu-id="27cce-183">如果您不使用這些項目，就應該手動加以刪除。</span><span class="sxs-lookup"><span data-stu-id="27cce-183">If you are not using these entities, you should delete them manually.</span></span>
* <span data-ttu-id="27cce-184">會保留 hello StorSimple 雲端應用裝置所建立的雲端快照。</span><span class="sxs-lookup"><span data-stu-id="27cce-184">Cloud snapshots created by hello StorSimple Cloud Appliance are retained.</span></span>

<span data-ttu-id="27cce-185">Hello 雲端應用裝置已停用之後，您可以從裝置 hello 清單中刪除它。</span><span class="sxs-lookup"><span data-stu-id="27cce-185">After hello cloud appliance is deactivated, you can delete it from hello list of devices.</span></span> <span data-ttu-id="27cce-186">選取 hello 停用裝置，以滑鼠右鍵按一下，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="27cce-186">Select hello deactivated device, right-click, and then click **Delete**.</span></span> <span data-ttu-id="27cce-187">StorSimple 通知您一旦 hello 裝置會刪除與 hello 裝置更新的清單。</span><span class="sxs-lookup"><span data-stu-id="27cce-187">StorSimple notifies you once hello device is deleted and hello list of devices updates.</span></span>

## <a name="next-steps"></a><span data-ttu-id="27cce-188">後續步驟</span><span class="sxs-lookup"><span data-stu-id="27cce-188">Next steps</span></span>

* <span data-ttu-id="27cce-189">toorestore hello 停用的裝置 toofactory 預設值、 跳過[hello 裝置 toofactory 預設設定重設](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings)。</span><span class="sxs-lookup"><span data-stu-id="27cce-189">toorestore hello deactivated device toofactory defaults, go too[Reset hello device toofactory default settings](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>
* <span data-ttu-id="27cce-190">如需技術協助， [請連絡 Microsoft 支援服務](storsimple-8000-contact-microsoft-support.md)。</span><span class="sxs-lookup"><span data-stu-id="27cce-190">For technical assistance, [contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>
* <span data-ttu-id="27cce-191">toolearn 深入了解如何 toouse hello StorSimple 裝置管理員服務移過[使用 hello StorSimple 裝置管理員服務 tooadminister StorSimple 裝置](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="27cce-191">toolearn more about how toouse hello StorSimple Device Manager service, go too[Use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

