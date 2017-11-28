---
title: "aaaDeactivate 和刪除 StorSimple 裝置 |Microsoft 文件"
description: "描述如何從服務，方法是先停用後再將其刪除 tooremove StorSimple 裝置。"
services: storsimple
documentationcenter: 
author: SharS
manager: timlt
editor: 
ms.assetid: 155cda38-c5ae-45dc-b7e8-6444494afc9e
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: anbacker
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ed86bcd089aa957128e14b1709c836d938c131a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-8000-series-device-via-storsimple-manager-service"></a><span data-ttu-id="13e61-103">透過 StorSimple Manager 服務來停用及刪除 StorSimple 8000 系列裝置</span><span class="sxs-lookup"><span data-stu-id="13e61-103">Deactivate and delete a StorSimple 8000 series device via StorSimple Manager service</span></span>
## <a name="overview"></a><span data-ttu-id="13e61-104">概觀</span><span class="sxs-lookup"><span data-stu-id="13e61-104">Overview</span></span>
<span data-ttu-id="13e61-105">您可能會想 tootake 汰 StorSimple 裝置 （例如，如果您要取代或升級您的裝置，或您不再需要使用 StorSimple）。</span><span class="sxs-lookup"><span data-stu-id="13e61-105">You may wish tootake a StorSimple device out of service (for example, if you are replacing or upgrading your device or if you are no longer using StorSimple).</span></span> <span data-ttu-id="13e61-106">在 hello 情況下，您將需要 toodeactivate hello 裝置，才能刪除它。</span><span class="sxs-lookup"><span data-stu-id="13e61-106">If this is hello case, you will need toodeactivate hello device before you can delete it.</span></span> <span data-ttu-id="13e61-107">停用伺服器 hello hello 裝置與之間連線 hello 相對應的 StorSimple Manager 服務。</span><span class="sxs-lookup"><span data-stu-id="13e61-107">Deactivating severs hello connection between hello device and hello corresponding StorSimple Manager service.</span></span> <span data-ttu-id="13e61-108">本教學課程說明如何 tooremove StorSimple 裝置的服務，方法是先停用後再將其刪除。</span><span class="sxs-lookup"><span data-stu-id="13e61-108">This tutorial explains how tooremove a StorSimple device from service by first deactivating it and then deleting it.</span></span> 

<span data-ttu-id="13e61-109">當您停用裝置時，任何已儲存在本機 hello 裝置的資料將不再可存取。</span><span class="sxs-lookup"><span data-stu-id="13e61-109">When you deactivate a device, any data that was stored locally on hello device will no longer be accessible.</span></span> <span data-ttu-id="13e61-110">只會 hello 與 hello 裝置 hello 雲端中儲存相關聯的資料可以復原。</span><span class="sxs-lookup"><span data-stu-id="13e61-110">Only hello data associated with hello device that was stored in hello cloud can be recovered.</span></span>  

> [!WARNING]
> <span data-ttu-id="13e61-111">停用是永久性的作業，而且無法復原。</span><span class="sxs-lookup"><span data-stu-id="13e61-111">Deactivation is a PERMANENT operation and cannot be undone.</span></span> <span data-ttu-id="13e61-112">已停用的裝置無法登錄與 hello StorSimple Manager 服務，除非它是第一次重設 toohello 預設原廠設定。</span><span class="sxs-lookup"><span data-stu-id="13e61-112">A deactivated device cannot be registered with hello StorSimple Manager service unless it is first reset toohello default factory settings.</span></span> 
> 
> <span data-ttu-id="13e61-113">hello 原廠重設程序會刪除已儲存在本機裝置的所有 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="13e61-113">hello factory reset process deletes all hello data that was stored locally on your device.</span></span> <span data-ttu-id="13e61-114">因此，在您停用裝置之前，您必須擷取所有資料的雲端快照集。</span><span class="sxs-lookup"><span data-stu-id="13e61-114">Therefore, it is essential that you take a cloud snapshot of all your data before you deactivate a device.</span></span> <span data-ttu-id="13e61-115">這可讓您 toorecover 所有 hello 資料在後續階段。</span><span class="sxs-lookup"><span data-stu-id="13e61-115">This will allow you toorecover all hello data at a later stage.</span></span>
> 
> 

<span data-ttu-id="13e61-116">本教學課程說明如何：</span><span class="sxs-lookup"><span data-stu-id="13e61-116">This tutorial explains how to:</span></span>

* <span data-ttu-id="13e61-117">停用的裝置，並刪除 hello 資料</span><span class="sxs-lookup"><span data-stu-id="13e61-117">Deactivate a device and delete hello data</span></span>
* <span data-ttu-id="13e61-118">停用的裝置並 hello 資料保留</span><span class="sxs-lookup"><span data-stu-id="13e61-118">Deactivate a device and retain hello data</span></span>

<span data-ttu-id="13e61-119">它也會說明如何針對 StorSimple 虛擬裝置來進行停用及刪除作業。</span><span class="sxs-lookup"><span data-stu-id="13e61-119">It also explains how deactivation and deletion works on a StorSimple virtual device.</span></span>

> [!NOTE]
> <span data-ttu-id="13e61-120">您停用 StorSimple 實體或虛擬裝置之前，請確定 toostop 或刪除用戶端和相依於該裝置的主機。</span><span class="sxs-lookup"><span data-stu-id="13e61-120">Before you deactivate a StorSimple physical or virtual device, make sure toostop or delete clients and hosts that depend on that device.</span></span>
> 
> 

## <a name="deactivate-and-delete-data"></a><span data-ttu-id="13e61-121">停用及刪除資料</span><span class="sxs-lookup"><span data-stu-id="13e61-121">Deactivate and delete data</span></span>
<span data-ttu-id="13e61-122">如果您想要完全刪除 hello 裝置並不想 tooretain hello 資料 hello 裝置上的，然後完成下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="13e61-122">If you are interested in deleting hello device completely and do not want tooretain hello data on hello device, then complete hello following steps.</span></span>

#### <a name="toodeactivate-hello-device-and-delete-hello-data"></a><span data-ttu-id="13e61-123">toodeactivate hello 裝置和 delete hello 資料</span><span class="sxs-lookup"><span data-stu-id="13e61-123">toodeactivate hello device and delete hello data</span></span>
1. <span data-ttu-id="13e61-124">先前 toodeactivating 裝置，您必須刪除所有 hello 磁碟區容器 （和 hello 磁碟區） 與 hello 裝置相關聯。</span><span class="sxs-lookup"><span data-stu-id="13e61-124">Prior toodeactivating a device, you must delete all hello volume containers (and hello volumes) associated with hello device.</span></span> <span data-ttu-id="13e61-125">只在您刪除相關聯的 hello 備份之後，您可以刪除磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="13e61-125">You can delete volume containers only after you have deleted hello associated backups.</span></span>
2. <span data-ttu-id="13e61-126">如下所示停用裝置 hello:</span><span class="sxs-lookup"><span data-stu-id="13e61-126">Deactivate hello device as follows:</span></span>
   
   1. <span data-ttu-id="13e61-127">Hello StorSimple Manager 服務在**裝置**頁面上，選取 hello 裝置，您想 toodeactivate 並在 hello hello 頁面底部，按一下 **停用**。</span><span class="sxs-lookup"><span data-stu-id="13e61-127">On hello StorSimple Manager service **Devices** page, select hello device that you wish toodeactivate and, at hello bottom of hello page, click **Deactivate**.</span></span>
   2. <span data-ttu-id="13e61-128">確認訊息隨即出現。</span><span class="sxs-lookup"><span data-stu-id="13e61-128">A confirmation message will appear.</span></span> <span data-ttu-id="13e61-129">按一下**是**toocontinue。</span><span class="sxs-lookup"><span data-stu-id="13e61-129">Click **Yes** toocontinue.</span></span> <span data-ttu-id="13e61-130">hello 停用程序將會啟動，並花幾分鐘的時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="13e61-130">hello deactivate process will start and take a few minutes toocomplete.</span></span>
3. <span data-ttu-id="13e61-131">停用之後，您可以完全刪除 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="13e61-131">After deactivation, you can delete hello device completely.</span></span> <span data-ttu-id="13e61-132">刪除裝置，即會從裝置連接的 toohello 服務的 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="13e61-132">Deleting a device removes it from hello list of devices connected toohello service.</span></span> <span data-ttu-id="13e61-133">hello 服務可以再管理 hello 刪除裝置。</span><span class="sxs-lookup"><span data-stu-id="13e61-133">hello service can then no longer manage hello deleted device.</span></span> <span data-ttu-id="13e61-134">使用下列步驟 toodelete hello 裝置 hello:</span><span class="sxs-lookup"><span data-stu-id="13e61-134">Use hello following steps toodelete hello device:</span></span>
   
   1. <span data-ttu-id="13e61-135">在 hello StorSimple Manager 服務**裝置**頁面上，選取您想 toodelete 停用的裝置。</span><span class="sxs-lookup"><span data-stu-id="13e61-135">On hello StorSimple Manager service **Devices** page, select a deactivated device that you wish toodelete.</span></span>
   2. <span data-ttu-id="13e61-136">在 hello 底部 hello 頁面上，按一下 **刪除**。</span><span class="sxs-lookup"><span data-stu-id="13e61-136">On hello bottom on hello page, click **Delete**.</span></span>
   3. <span data-ttu-id="13e61-137">系統將提示您進行確認。</span><span class="sxs-lookup"><span data-stu-id="13e61-137">You will be prompted for confirmation.</span></span> <span data-ttu-id="13e61-138">按一下**是**toocontinue。</span><span class="sxs-lookup"><span data-stu-id="13e61-138">Click **Yes** toocontinue.</span></span>
      
      <span data-ttu-id="13e61-139">可能需要幾分鐘，讓 hello 裝置 toobe 刪除。</span><span class="sxs-lookup"><span data-stu-id="13e61-139">It may take a few minutes for hello device toobe deleted.</span></span>

## <a name="deactivate-and-retain-data"></a><span data-ttu-id="13e61-140">停用並保留資料</span><span class="sxs-lookup"><span data-stu-id="13e61-140">Deactivate and retain data</span></span>
<span data-ttu-id="13e61-141">如果您有興趣刪除 hello 裝置，但想 tooretain hello 資料，然後完成下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="13e61-141">If you are interested in deleting hello device but want tooretain hello data, then complete hello following steps.</span></span>

#### <a name="toodeactivate-a-device-and-retain-hello-data"></a><span data-ttu-id="13e61-142">toodeactivate 裝置並 hello 資料保留</span><span class="sxs-lookup"><span data-stu-id="13e61-142">toodeactivate a device and retain hello data</span></span>
1. <span data-ttu-id="13e61-143">停用 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="13e61-143">Deactivate hello device.</span></span> <span data-ttu-id="13e61-144">所有 hello 磁碟區容器，但仍會保留的 hello 裝置 hello 快照集。</span><span class="sxs-lookup"><span data-stu-id="13e61-144">All hello volume containers and hello snapshots of hello device will remain.</span></span>
   
   1. <span data-ttu-id="13e61-145">Hello StorSimple Manager 服務在**裝置**頁面上，選取 hello 裝置，您想 toodeactivate 並在 hello hello 頁面底部，按一下 **停用**。</span><span class="sxs-lookup"><span data-stu-id="13e61-145">On hello StorSimple Manager service **Devices** page, select hello device that you wish toodeactivate and, at hello bottom of hello page, click **Deactivate**.</span></span>
   2. <span data-ttu-id="13e61-146">確認訊息隨即出現。</span><span class="sxs-lookup"><span data-stu-id="13e61-146">A confirmation message will appear.</span></span> <span data-ttu-id="13e61-147">按一下**是**toocontinue。</span><span class="sxs-lookup"><span data-stu-id="13e61-147">Click **Yes** toocontinue.</span></span> <span data-ttu-id="13e61-148">hello 停用程序將會啟動，並花幾分鐘的時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="13e61-148">hello deactivate process will start and take a few minutes toocomplete.</span></span>
2. <span data-ttu-id="13e61-149">您現在可以容錯移轉 hello 磁碟區容器和相關聯的 hello 快照集。</span><span class="sxs-lookup"><span data-stu-id="13e61-149">You can now fail over hello volume containers and hello associated snapshots.</span></span> <span data-ttu-id="13e61-150">程序，跳過[StorSimple 裝置的容錯移轉和災害復原](storsimple-device-failover-disaster-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="13e61-150">For procedures, go too[Failover and disaster recovery for your StorSimple device](storsimple-device-failover-disaster-recovery.md).</span></span>
3. <span data-ttu-id="13e61-151">停用和容錯移轉之後, 您可以完全刪除 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="13e61-151">After deactivation and failover, you can delete hello device completely.</span></span> <span data-ttu-id="13e61-152">刪除裝置，即會從裝置連接的 toohello 服務的 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="13e61-152">Deleting a device removes it from hello list of devices connected toohello service.</span></span> <span data-ttu-id="13e61-153">hello 服務可以再管理 hello 刪除裝置。</span><span class="sxs-lookup"><span data-stu-id="13e61-153">hello service can then no longer manage hello deleted device.</span></span> <span data-ttu-id="13e61-154">完成下列步驟 toodelete hello 裝置 hello:</span><span class="sxs-lookup"><span data-stu-id="13e61-154">Complete hello following steps toodelete hello device:</span></span>
   
   1. <span data-ttu-id="13e61-155">在 hello StorSimple Manager 服務**裝置**頁面上，選取您想 toodelete 停用的裝置。</span><span class="sxs-lookup"><span data-stu-id="13e61-155">On hello StorSimple Manager service **Devices** page, select a deactivated device that you wish toodelete.</span></span>
   2. <span data-ttu-id="13e61-156">在 hello 底部 hello 頁面上，按一下 **刪除**。</span><span class="sxs-lookup"><span data-stu-id="13e61-156">On hello bottom on hello page, click **Delete**.</span></span>
   3. <span data-ttu-id="13e61-157">系統將提示您進行確認。</span><span class="sxs-lookup"><span data-stu-id="13e61-157">You will be prompted for confirmation.</span></span> <span data-ttu-id="13e61-158">按一下**是**toocontinue。</span><span class="sxs-lookup"><span data-stu-id="13e61-158">Click **Yes** toocontinue.</span></span>
      
      <span data-ttu-id="13e61-159">可能需要幾分鐘，讓 hello 裝置 toobe 刪除。</span><span class="sxs-lookup"><span data-stu-id="13e61-159">It may take a few minutes for hello device toobe deleted.</span></span>

## <a name="deactivate-and-delete-a-virtual-device"></a><span data-ttu-id="13e61-160">停用並刪除虛擬裝置</span><span class="sxs-lookup"><span data-stu-id="13e61-160">Deactivate and delete a virtual device</span></span>
<span data-ttu-id="13e61-161">StorSimple 虛擬裝置，請停用取消配置 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="13e61-161">For a StorSimple virtual device, deactivation deallocates hello virtual machine.</span></span> <span data-ttu-id="13e61-162">然後您就可以刪除 hello 虛擬機器及其 hello 資源建立時已佈建。</span><span class="sxs-lookup"><span data-stu-id="13e61-162">You can then delete hello virtual machine and hello resources created when it was provisioned.</span></span> <span data-ttu-id="13e61-163">Hello 虛擬裝置停用之後，它不能還原 tooits 先前的狀態。</span><span class="sxs-lookup"><span data-stu-id="13e61-163">After hello virtual device is deactivated, it cannot be restored tooits previous state.</span></span> 

<span data-ttu-id="13e61-164">停用產生 hello 下列動作：</span><span class="sxs-lookup"><span data-stu-id="13e61-164">Deactivation results in hello following actions:</span></span>

* <span data-ttu-id="13e61-165">移除 hello StorSimple 虛擬裝置。</span><span class="sxs-lookup"><span data-stu-id="13e61-165">hello StorSimple virtual device is removed.</span></span>
* <span data-ttu-id="13e61-166">hello OSDisk 和資料磁碟建立 hello StorSimple 虛擬裝置會移除。</span><span class="sxs-lookup"><span data-stu-id="13e61-166">hello OSDisk and Data Disks created for hello StorSimple virtual device are removed.</span></span>
* <span data-ttu-id="13e61-167">hello 裝載服務和已佈建期間建立的虛擬網路會保留。</span><span class="sxs-lookup"><span data-stu-id="13e61-167">hello Hosted Service and Virtual Network that were created during provisioning are retained.</span></span> <span data-ttu-id="13e61-168">如果您不使用這些項目，就應該手動加以刪除。</span><span class="sxs-lookup"><span data-stu-id="13e61-168">If you are not using these entities, you should delete them manually.</span></span>
* <span data-ttu-id="13e61-169">保留的 hello StorSimple 虛擬裝置所建立的雲端快照集。</span><span class="sxs-lookup"><span data-stu-id="13e61-169">Cloud snapshots created by hello StorSimple virtual device are retained.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13e61-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="13e61-170">Next steps</span></span>
* <span data-ttu-id="13e61-171">toorestore hello 停用的裝置 toofactory 預設值、 跳過[hello 裝置 toofactory 預設設定重設](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings)。</span><span class="sxs-lookup"><span data-stu-id="13e61-171">toorestore hello deactivated device toofactory defaults, go too[Reset hello device toofactory default settings](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>
* <span data-ttu-id="13e61-172">如需技術協助， [請連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md)。</span><span class="sxs-lookup"><span data-stu-id="13e61-172">For technical assistance, [contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
* <span data-ttu-id="13e61-173">toolearn 深入了解如何 toouse hello StorSimple Manager 服務移過[使用 hello StorSimple Manager 服務 tooadminister StorSimple 裝置](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="13e61-173">toolearn more about how toouse hello StorSimple Manager service, go too[Use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span> 

