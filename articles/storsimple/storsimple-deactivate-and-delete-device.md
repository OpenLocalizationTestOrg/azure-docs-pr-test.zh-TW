---
title: "停用及刪除 StorSimple 裝置 | Microsoft Docs"
description: "描述如何停用然後刪除 StorSimple 裝置，將其從服務中移除。"
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
ms.openlocfilehash: c000a642aa088ac80cc7077453b87e9a47f96900
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deactivate-and-delete-a-storsimple-8000-series-device-via-storsimple-manager-service"></a><span data-ttu-id="30454-103">透過 StorSimple Manager 服務來停用及刪除 StorSimple 8000 系列裝置</span><span class="sxs-lookup"><span data-stu-id="30454-103">Deactivate and delete a StorSimple 8000 series device via StorSimple Manager service</span></span>
## <a name="overview"></a><span data-ttu-id="30454-104">概觀</span><span class="sxs-lookup"><span data-stu-id="30454-104">Overview</span></span>
<span data-ttu-id="30454-105">您可能會想讓某個 StorSimple 裝置停止提供服務 (舉例來說，當您在替換或升級裝置時，或是當您不再使用 StorSimple 時)。</span><span class="sxs-lookup"><span data-stu-id="30454-105">You may wish to take a StorSimple device out of service (for example, if you are replacing or upgrading your device or if you are no longer using StorSimple).</span></span> <span data-ttu-id="30454-106">如果是如此，您將必須在刪除該裝置之前，先停用該裝置。</span><span class="sxs-lookup"><span data-stu-id="30454-106">If this is the case, you will need to deactivate the device before you can delete it.</span></span> <span data-ttu-id="30454-107">停用會切斷裝置與相對應 StorSimple Manager 服務之間的連接。</span><span class="sxs-lookup"><span data-stu-id="30454-107">Deactivating severs the connection between the device and the corresponding StorSimple Manager service.</span></span> <span data-ttu-id="30454-108">本教學課程說明如何藉由停用並刪除 StorSimple 裝置，來將該裝置從服務中移除。</span><span class="sxs-lookup"><span data-stu-id="30454-108">This tutorial explains how to remove a StorSimple device from service by first deactivating it and then deleting it.</span></span> 

<span data-ttu-id="30454-109">當您停用裝置時，將無法再存取以本機方式儲存在裝置上的任何資料。</span><span class="sxs-lookup"><span data-stu-id="30454-109">When you deactivate a device, any data that was stored locally on the device will no longer be accessible.</span></span> <span data-ttu-id="30454-110">只有儲存於雲端之裝置的相關聯資料可以復原。</span><span class="sxs-lookup"><span data-stu-id="30454-110">Only the data associated with the device that was stored in the cloud can be recovered.</span></span>  

> [!WARNING]
> <span data-ttu-id="30454-111">停用是永久性的作業，而且無法復原。</span><span class="sxs-lookup"><span data-stu-id="30454-111">Deactivation is a PERMANENT operation and cannot be undone.</span></span> <span data-ttu-id="30454-112">停用的服務無法向 StorSimple Manager 服務登錄，除非先重設為預設的原廠設定。</span><span class="sxs-lookup"><span data-stu-id="30454-112">A deactivated device cannot be registered with the StorSimple Manager service unless it is first reset to the default factory settings.</span></span> 
> 
> <span data-ttu-id="30454-113">原廠重設程序會刪除以本機方式儲存在裝置上的所有資料。</span><span class="sxs-lookup"><span data-stu-id="30454-113">The factory reset process deletes all the data that was stored locally on your device.</span></span> <span data-ttu-id="30454-114">因此，在您停用裝置之前，您必須擷取所有資料的雲端快照集。</span><span class="sxs-lookup"><span data-stu-id="30454-114">Therefore, it is essential that you take a cloud snapshot of all your data before you deactivate a device.</span></span> <span data-ttu-id="30454-115">這樣可讓您在稍後的階段中復原所有的資料。</span><span class="sxs-lookup"><span data-stu-id="30454-115">This will allow you to recover all the data at a later stage.</span></span>
> 
> 

<span data-ttu-id="30454-116">本教學課程說明如何：</span><span class="sxs-lookup"><span data-stu-id="30454-116">This tutorial explains how to:</span></span>

* <span data-ttu-id="30454-117">停用裝置並刪除資料</span><span class="sxs-lookup"><span data-stu-id="30454-117">Deactivate a device and delete the data</span></span>
* <span data-ttu-id="30454-118">停用裝置並保留資料</span><span class="sxs-lookup"><span data-stu-id="30454-118">Deactivate a device and retain the data</span></span>

<span data-ttu-id="30454-119">它也會說明如何針對 StorSimple 虛擬裝置來進行停用及刪除作業。</span><span class="sxs-lookup"><span data-stu-id="30454-119">It also explains how deactivation and deletion works on a StorSimple virtual device.</span></span>

> [!NOTE]
> <span data-ttu-id="30454-120">在您停用 StorSimple 實體或虛擬裝置之前，請務必停止或刪除相依於該裝置的用戶端和主機。</span><span class="sxs-lookup"><span data-stu-id="30454-120">Before you deactivate a StorSimple physical or virtual device, make sure to stop or delete clients and hosts that depend on that device.</span></span>
> 
> 

## <a name="deactivate-and-delete-data"></a><span data-ttu-id="30454-121">停用及刪除資料</span><span class="sxs-lookup"><span data-stu-id="30454-121">Deactivate and delete data</span></span>
<span data-ttu-id="30454-122">如果您想要完全刪除裝置，且不要保留裝置中的資料，請完成下列步驟。</span><span class="sxs-lookup"><span data-stu-id="30454-122">If you are interested in deleting the device completely and do not want to retain the data on the device, then complete the following steps.</span></span>

#### <a name="to-deactivate-the-device-and-delete-the-data"></a><span data-ttu-id="30454-123">如何停用裝置並刪除資料</span><span class="sxs-lookup"><span data-stu-id="30454-123">To deactivate the device and delete the data</span></span>
1. <span data-ttu-id="30454-124">在停用裝置之前，您必須刪除和裝置相關聯的所有磁碟區容器 (和磁碟區)。</span><span class="sxs-lookup"><span data-stu-id="30454-124">Prior to deactivating a device, you must delete all the volume containers (and the volumes) associated with the device.</span></span> <span data-ttu-id="30454-125">但您在刪除磁碟區容器之前，必須先刪除相關聯的備份。</span><span class="sxs-lookup"><span data-stu-id="30454-125">You can delete volume containers only after you have deleted the associated backups.</span></span>
2. <span data-ttu-id="30454-126">請依照下列步驟來停用裝置：</span><span class="sxs-lookup"><span data-stu-id="30454-126">Deactivate the device as follows:</span></span>
   
   1. <span data-ttu-id="30454-127">在 StorSimple Manager 服務**裝置**頁面上，選取您想要停用的裝置，並在頁面底部按一下 [停用]。</span><span class="sxs-lookup"><span data-stu-id="30454-127">On the StorSimple Manager service **Devices** page, select the device that you wish to deactivate and, at the bottom of the page, click **Deactivate**.</span></span>
   2. <span data-ttu-id="30454-128">確認訊息隨即出現。</span><span class="sxs-lookup"><span data-stu-id="30454-128">A confirmation message will appear.</span></span> <span data-ttu-id="30454-129">按一下 [是]  以繼續。</span><span class="sxs-lookup"><span data-stu-id="30454-129">Click **Yes** to continue.</span></span> <span data-ttu-id="30454-130">停用程序將會啟動，並需要幾分鐘才能完成。</span><span class="sxs-lookup"><span data-stu-id="30454-130">The deactivate process will start and take a few minutes to complete.</span></span>
3. <span data-ttu-id="30454-131">停用之後，您就可以完全刪除裝置。</span><span class="sxs-lookup"><span data-stu-id="30454-131">After deactivation, you can delete the device completely.</span></span> <span data-ttu-id="30454-132">刪除裝置會將其從與服務連接的裝置清單移除。</span><span class="sxs-lookup"><span data-stu-id="30454-132">Deleting a device removes it from the list of devices connected to the service.</span></span> <span data-ttu-id="30454-133">服務將不再管理已刪除的裝置。</span><span class="sxs-lookup"><span data-stu-id="30454-133">The service can then no longer manage the deleted device.</span></span> <span data-ttu-id="30454-134">請使用下列步驟來刪除裝置：</span><span class="sxs-lookup"><span data-stu-id="30454-134">Use the following steps to delete the device:</span></span>
   
   1. <span data-ttu-id="30454-135">在 StorSimple Manager 服務上 **裝置** 頁面上，選取您想要刪除的已停用裝置。</span><span class="sxs-lookup"><span data-stu-id="30454-135">On the StorSimple Manager service **Devices** page, select a deactivated device that you wish to delete.</span></span>
   2. <span data-ttu-id="30454-136">按一下頁面底部的 [ **刪除**]。</span><span class="sxs-lookup"><span data-stu-id="30454-136">On the bottom on the page, click **Delete**.</span></span>
   3. <span data-ttu-id="30454-137">系統將提示您進行確認。</span><span class="sxs-lookup"><span data-stu-id="30454-137">You will be prompted for confirmation.</span></span> <span data-ttu-id="30454-138">按一下 [是]  以繼續。</span><span class="sxs-lookup"><span data-stu-id="30454-138">Click **Yes** to continue.</span></span>
      
      <span data-ttu-id="30454-139">刪除裝置可能需要數分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="30454-139">It may take a few minutes for the device to be deleted.</span></span>

## <a name="deactivate-and-retain-data"></a><span data-ttu-id="30454-140">停用並保留資料</span><span class="sxs-lookup"><span data-stu-id="30454-140">Deactivate and retain data</span></span>
<span data-ttu-id="30454-141">如果您想要刪除裝置，但要保留資料，請完成下列步驟。</span><span class="sxs-lookup"><span data-stu-id="30454-141">If you are interested in deleting the device but want to retain the data, then complete the following steps.</span></span>

#### <a name="to-deactivate-a-device-and-retain-the-data"></a><span data-ttu-id="30454-142">如何停用裝置並保留資料</span><span class="sxs-lookup"><span data-stu-id="30454-142">To deactivate a device and retain the data</span></span>
1. <span data-ttu-id="30454-143">停用裝置。</span><span class="sxs-lookup"><span data-stu-id="30454-143">Deactivate the device.</span></span> <span data-ttu-id="30454-144">裝置的所有磁碟區容器及快照集都會保留。</span><span class="sxs-lookup"><span data-stu-id="30454-144">All the volume containers and the snapshots of the device will remain.</span></span>
   
   1. <span data-ttu-id="30454-145">在 StorSimple Manager 服務**裝置**頁面上，選取您想要停用的裝置，並在頁面底部按一下 [停用]。</span><span class="sxs-lookup"><span data-stu-id="30454-145">On the StorSimple Manager service **Devices** page, select the device that you wish to deactivate and, at the bottom of the page, click **Deactivate**.</span></span>
   2. <span data-ttu-id="30454-146">確認訊息隨即出現。</span><span class="sxs-lookup"><span data-stu-id="30454-146">A confirmation message will appear.</span></span> <span data-ttu-id="30454-147">按一下 [是]  以繼續。</span><span class="sxs-lookup"><span data-stu-id="30454-147">Click **Yes** to continue.</span></span> <span data-ttu-id="30454-148">停用程序將會啟動，並需要幾分鐘才能完成。</span><span class="sxs-lookup"><span data-stu-id="30454-148">The deactivate process will start and take a few minutes to complete.</span></span>
2. <span data-ttu-id="30454-149">您現在可以容錯移轉磁碟區容器和相關聯的快照集。</span><span class="sxs-lookup"><span data-stu-id="30454-149">You can now fail over the volume containers and the associated snapshots.</span></span> <span data-ttu-id="30454-150">關於程序，請移至 [StorSimple 裝置的容錯移轉和災害復原](storsimple-device-failover-disaster-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="30454-150">For procedures, go to [Failover and disaster recovery for your StorSimple device](storsimple-device-failover-disaster-recovery.md).</span></span>
3. <span data-ttu-id="30454-151">停用和容錯移轉之後，您就可以完全刪除裝置。</span><span class="sxs-lookup"><span data-stu-id="30454-151">After deactivation and failover, you can delete the device completely.</span></span> <span data-ttu-id="30454-152">刪除裝置會將其從與服務連接的裝置清單移除。</span><span class="sxs-lookup"><span data-stu-id="30454-152">Deleting a device removes it from the list of devices connected to the service.</span></span> <span data-ttu-id="30454-153">服務將不再管理已刪除的裝置。</span><span class="sxs-lookup"><span data-stu-id="30454-153">The service can then no longer manage the deleted device.</span></span> <span data-ttu-id="30454-154">請完成下列步驟來刪除裝置：</span><span class="sxs-lookup"><span data-stu-id="30454-154">Complete the following steps to delete the device:</span></span>
   
   1. <span data-ttu-id="30454-155">在 StorSimple Manager 服務上 **裝置** 頁面上，選取您想要刪除的已停用裝置。</span><span class="sxs-lookup"><span data-stu-id="30454-155">On the StorSimple Manager service **Devices** page, select a deactivated device that you wish to delete.</span></span>
   2. <span data-ttu-id="30454-156">按一下頁面底部的 [ **刪除**]。</span><span class="sxs-lookup"><span data-stu-id="30454-156">On the bottom on the page, click **Delete**.</span></span>
   3. <span data-ttu-id="30454-157">系統將提示您進行確認。</span><span class="sxs-lookup"><span data-stu-id="30454-157">You will be prompted for confirmation.</span></span> <span data-ttu-id="30454-158">按一下 [是]  以繼續。</span><span class="sxs-lookup"><span data-stu-id="30454-158">Click **Yes** to continue.</span></span>
      
      <span data-ttu-id="30454-159">刪除裝置可能需要數分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="30454-159">It may take a few minutes for the device to be deleted.</span></span>

## <a name="deactivate-and-delete-a-virtual-device"></a><span data-ttu-id="30454-160">停用並刪除虛擬裝置</span><span class="sxs-lookup"><span data-stu-id="30454-160">Deactivate and delete a virtual device</span></span>
<span data-ttu-id="30454-161">對於 StorSimple 虛擬裝置來說，停用將會讓虛擬機器取消配置。</span><span class="sxs-lookup"><span data-stu-id="30454-161">For a StorSimple virtual device, deactivation deallocates the virtual machine.</span></span> <span data-ttu-id="30454-162">然後您就可以刪除虛擬機器，以及刪除在佈建該虛擬機器時所建立的資源。</span><span class="sxs-lookup"><span data-stu-id="30454-162">You can then delete the virtual machine and the resources created when it was provisioned.</span></span> <span data-ttu-id="30454-163">停用虛擬裝置之後，就無法將它還原為先前的狀態。</span><span class="sxs-lookup"><span data-stu-id="30454-163">After the virtual device is deactivated, it cannot be restored to its previous state.</span></span> 

<span data-ttu-id="30454-164">停用會導致下列動作發生：</span><span class="sxs-lookup"><span data-stu-id="30454-164">Deactivation results in the following actions:</span></span>

* <span data-ttu-id="30454-165">StorSimple 虛擬裝置會移除。</span><span class="sxs-lookup"><span data-stu-id="30454-165">The StorSimple virtual device is removed.</span></span>
* <span data-ttu-id="30454-166">為虛擬裝置建立的 OSDisk 和資料磁碟會移除。</span><span class="sxs-lookup"><span data-stu-id="30454-166">The OSDisk and Data Disks created for the StorSimple virtual device are removed.</span></span>
* <span data-ttu-id="30454-167">在佈建期間建立的託管服務和虛擬網路會保留。</span><span class="sxs-lookup"><span data-stu-id="30454-167">The Hosted Service and Virtual Network that were created during provisioning are retained.</span></span> <span data-ttu-id="30454-168">如果您不使用這些項目，就應該手動加以刪除。</span><span class="sxs-lookup"><span data-stu-id="30454-168">If you are not using these entities, you should delete them manually.</span></span>
* <span data-ttu-id="30454-169">StorSimple 虛擬裝置所建立的雲端快照集會保留。</span><span class="sxs-lookup"><span data-stu-id="30454-169">Cloud snapshots created by the StorSimple virtual device are retained.</span></span>

## <a name="next-steps"></a><span data-ttu-id="30454-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="30454-170">Next steps</span></span>
* <span data-ttu-id="30454-171">若要將已停用的裝置還原為原廠預設值，請移至 [將裝置重設為原廠預設設定](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings)。</span><span class="sxs-lookup"><span data-stu-id="30454-171">To restore the deactivated device to factory defaults, go to [Reset the device to factory default settings](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>
* <span data-ttu-id="30454-172">如需技術協助， [請連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md)。</span><span class="sxs-lookup"><span data-stu-id="30454-172">For technical assistance, [contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
* <span data-ttu-id="30454-173">若要了解如何使用 StorSimple Manager，請移至 [使用 StorSimple Manager 服務管理 StorSimple 裝置](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="30454-173">To learn more about how to use the StorSimple Manager service, go to [Use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span> 

