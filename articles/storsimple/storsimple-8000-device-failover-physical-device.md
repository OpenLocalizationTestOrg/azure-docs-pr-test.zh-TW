---
title: "StorSimple 容錯移轉、災害復原至 StorSimple 8000 系列實體裝置| Microsoft Docs"
description: "了解如何將您的 StorSimple 8000 系列實體裝置容錯移轉至另一個實體裝置。"
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
ms.date: 05/03/2017
ms.author: alkohli
ms.openlocfilehash: f3ac9545a341fc24ca12c9f2547805d6956cd98a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="fail-over-to-a-storsimple-8000-series-physical-device"></a><span data-ttu-id="98cb5-103">容錯移轉至 StorSimple 8000 系列實體裝置</span><span class="sxs-lookup"><span data-stu-id="98cb5-103">Fail over to a StorSimple 8000 series physical device</span></span>

## <a name="overview"></a><span data-ttu-id="98cb5-104">概觀</span><span class="sxs-lookup"><span data-stu-id="98cb5-104">Overview</span></span>

<span data-ttu-id="98cb5-105">本教學課程說明出現災害時，將 StorSimple 8000 系列實體裝置容錯移轉至另一個 StorSimple 實體裝置所需要的步驟。</span><span class="sxs-lookup"><span data-stu-id="98cb5-105">This tutorial describes the steps required to fail over a StorSimple 8000 series physical device to another StorSimple physical device if there is a disaster.</span></span> <span data-ttu-id="98cb5-106">StorSimple 會使用裝置容錯移轉功能，將資料從資料中心的實體裝置來源移轉至另一個實體裝置。</span><span class="sxs-lookup"><span data-stu-id="98cb5-106">StorSimple uses the device failover feature to migrate data from a source physical device in the datacenter to another physical device.</span></span> <span data-ttu-id="98cb5-107">本教學課程中的指導方針適用於執行軟體版本 Update 3 和更新版本的 StorSimple 8000 系列實體裝置。</span><span class="sxs-lookup"><span data-stu-id="98cb5-107">The guidance in this tutorial applies to StorSimple 8000 series physical devices running software versions Update 3 and later.</span></span>

<span data-ttu-id="98cb5-108">若要深入了解裝置容錯移轉，以及如何用於從災害中復原，請移至 [ StorSimple 8000 系列裝置的容錯移轉與災害復原](storsimple-8000-device-failover-disaster-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="98cb5-108">To learn more about device failover and how it is used to recover from a disaster, go to [Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

<span data-ttu-id="98cb5-109">若要將 StorSimple 實體裝置容錯移轉至 StorSimple 雲端設備，請移至[容錯移轉至 StorSimple 雲端設備](storsimple-8000-device-failover-cloud-appliance.md)。</span><span class="sxs-lookup"><span data-stu-id="98cb5-109">To fail over a StorSimple physical device to a StorSimple Cloud Appliance, go to [Fail over to a StorSimple Cloud Appliance](storsimple-8000-device-failover-cloud-appliance.md).</span></span> <span data-ttu-id="98cb5-110">若要將實體裝置容錯移轉至本身的裝置，請移至[容錯移轉至相同的 StorSimple 實體裝置](storsimple-8000-device-failover-same-device.md)。</span><span class="sxs-lookup"><span data-stu-id="98cb5-110">To fail over a physical device to itself, go to [Fail over to the same StorSimple physical device](storsimple-8000-device-failover-same-device.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="98cb5-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="98cb5-111">Prerequisites</span></span>

- <span data-ttu-id="98cb5-112">請確定您已檢閱裝置容錯移轉的注意事項。</span><span class="sxs-lookup"><span data-stu-id="98cb5-112">Ensure that you have reviewed the considerations for device failover.</span></span> <span data-ttu-id="98cb5-113">如需詳細資訊，請移至[裝置容錯移轉的一般注意事項](storsimple-8000-device-failover-disaster-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="98cb5-113">For more information, go to [Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

- <span data-ttu-id="98cb5-114">必須已在資料中心內部署 StorSimple 8000 系列實體裝置。</span><span class="sxs-lookup"><span data-stu-id="98cb5-114">You must have a StorSimple 8000 series physical device deployed in the datacenter.</span></span> <span data-ttu-id="98cb5-115">裝置必須執行 Update 3 或更新的軟體版本。</span><span class="sxs-lookup"><span data-stu-id="98cb5-115">The device must run Update 3 or later software version.</span></span> <span data-ttu-id="98cb5-116">如需詳細資訊，請移至 [部署內部部署 StorSimple 裝置](storsimple-8000-deployment-walkthrough-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="98cb5-116">For more information, go to [Deploy your on-premises StorSimple device](storsimple-8000-deployment-walkthrough-u2.md).</span></span>


## <a name="steps-to-fail-over-to-a-physical-device"></a><span data-ttu-id="98cb5-117">容錯移轉到實體裝置的步驟</span><span class="sxs-lookup"><span data-stu-id="98cb5-117">Steps to fail over to a physical device</span></span>

<span data-ttu-id="98cb5-118">請執行下列步驟以將裝置還原至目標實體裝置。</span><span class="sxs-lookup"><span data-stu-id="98cb5-118">Perform the following steps to restore your device to a target physical device.</span></span>

1. <span data-ttu-id="98cb5-119">確認您要容錯移轉的磁碟區容器是否具有相關聯的雲端快照。</span><span class="sxs-lookup"><span data-stu-id="98cb5-119">Verify that the volume container you want to fail over has associated cloud snapshots.</span></span> <span data-ttu-id="98cb5-120">如需詳細資訊，請移至[使用 StorSimple 裝置管理員服務建立備份](storsimple-8000-manage-backup-policies-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="98cb5-120">For more information, go to [Use StorSimple Device Manager service to create backups](storsimple-8000-manage-backup-policies-u2.md).</span></span>
2. <span data-ttu-id="98cb5-121">移至您的 StorSimple 裝置管理員，然後按一下 [裝置]。</span><span class="sxs-lookup"><span data-stu-id="98cb5-121">Go to your StorSimple Device Manager and then click **Devices**.</span></span> <span data-ttu-id="98cb5-122">在 [裝置] 刀鋒視窗中，移至與您的服務連接的裝置清單。</span><span class="sxs-lookup"><span data-stu-id="98cb5-122">In the **Devices** blade, go to the list of devices connected with your service.</span></span>
    <span data-ttu-id="98cb5-123">![選取裝置](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev1.png)</span><span class="sxs-lookup"><span data-stu-id="98cb5-123">![Select device](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev1.png)</span></span>
3. <span data-ttu-id="98cb5-124">選取並按一下您的來源裝置。</span><span class="sxs-lookup"><span data-stu-id="98cb5-124">Select and click your source device.</span></span> <span data-ttu-id="98cb5-125">來源裝置具有您想要容錯移轉的磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="98cb5-125">The source device has the volume containers that you want to fail over.</span></span> <span data-ttu-id="98cb5-126">移至 [設定] > [磁碟區容器]。</span><span class="sxs-lookup"><span data-stu-id="98cb5-126">Go to **Settings > Volume Containers**.</span></span>
4. <span data-ttu-id="98cb5-127">選取您要容錯移轉至另一個裝置的磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="98cb5-127">Select a volume container that you would like to fail over to another device.</span></span> <span data-ttu-id="98cb5-128">按一下磁碟區容器，以顯示此容器內的磁碟區清單。</span><span class="sxs-lookup"><span data-stu-id="98cb5-128">Click the volume container to display the list of volumes within this container.</span></span> <span data-ttu-id="98cb5-129">選取磁碟區，按一下滑鼠右鍵，然後按一下 [離線]，讓磁碟區離線。</span><span class="sxs-lookup"><span data-stu-id="98cb5-129">Select a volume, right-click, and click **Take Offline** to take the volume offline.</span></span> <span data-ttu-id="98cb5-130">針對磁碟區容器中的所有磁碟區，重複執行這個程序。</span><span class="sxs-lookup"><span data-stu-id="98cb5-130">Repeat this process for all the volumes in the volume container.</span></span>
5. <span data-ttu-id="98cb5-131">針對您要容錯移轉至另一個裝置的所有磁碟區容器，重複執行前一個步驟。</span><span class="sxs-lookup"><span data-stu-id="98cb5-131">Repeat the previous step for all the volume containers you would like to fail over to another device.</span></span>
6. <span data-ttu-id="98cb5-132">返回 [裝置] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="98cb5-132">Go back to the **Devices** blade.</span></span> <span data-ttu-id="98cb5-133">從命令列中，按一下 [容錯移轉]。</span><span class="sxs-lookup"><span data-stu-id="98cb5-133">From the command bar, click **Fail over**.</span></span>
    <span data-ttu-id="98cb5-134">按一下 [容錯移轉]![](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev2.png)</span><span class="sxs-lookup"><span data-stu-id="98cb5-134">![Click fail over](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev2.png)</span></span>
    
7. <span data-ttu-id="98cb5-135">在 [容錯移轉] 刀鋒視窗中，執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="98cb5-135">In the **Fail over** blade, perform the following steps:</span></span>
   
   1. <span data-ttu-id="98cb5-136">按一下 [來源]。</span><span class="sxs-lookup"><span data-stu-id="98cb5-136">Click **Source**.</span></span> <span data-ttu-id="98cb5-137">隨即顯示含有與雲端快照集相關聯之磁碟區的磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="98cb5-137">The volume containers with volumes associated with cloud snapshots are displayed.</span></span> <span data-ttu-id="98cb5-138">只有顯示的容器才可進行容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="98cb5-138">Only the containers displayed are eligible for failover.</span></span> <span data-ttu-id="98cb5-139">在磁碟區容器清單中，選取您要容錯移轉的磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="98cb5-139">In the list of volume containers, select the volume containers you would like to fail over.</span></span> <span data-ttu-id="98cb5-140">**只會顯示與雲端快照集和離線磁碟區相關聯的磁碟區容器。**</span><span class="sxs-lookup"><span data-stu-id="98cb5-140">**Only the volume containers with associated cloud snapshots and offline volumes are displayed.**</span></span>

       ![選取來源](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev5.png)
   2. <span data-ttu-id="98cb5-142">按一下 [目標]。</span><span class="sxs-lookup"><span data-stu-id="98cb5-142">Click **Target**.</span></span> <span data-ttu-id="98cb5-143">從可用裝置的下拉式清單中選取目標裝置，供上一步選取的磁碟區容器使用。</span><span class="sxs-lookup"><span data-stu-id="98cb5-143">For the volume containers selected in the previous step, select a target device from the drop-down list of available devices.</span></span> <span data-ttu-id="98cb5-144">清單中只會顯示擁有足夠容量容納來源磁碟區容器的裝置。</span><span class="sxs-lookup"><span data-stu-id="98cb5-144">Only the devices that have sufficient capacity to accommodate source volume containers are displayed in the list.</span></span>

        ![選取目標](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev6.png)

   3. <span data-ttu-id="98cb5-146">最後，檢閱 [摘要] 下的所有容錯移轉設定。</span><span class="sxs-lookup"><span data-stu-id="98cb5-146">Finally, review all the failover settings under **Summary**.</span></span> <span data-ttu-id="98cb5-147">檢閱設定之後，選取核取方塊，代表所選取磁碟區容器中的磁碟區已離線。</span><span class="sxs-lookup"><span data-stu-id="98cb5-147">After you have reviewed the settings, select the checkbox indicating that the volumes in selected volume containers are offline.</span></span> <span data-ttu-id="98cb5-148">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="98cb5-148">Click **OK**.</span></span>

       ![檢閱容錯移轉設定](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev8.png)
  
8. <span data-ttu-id="98cb5-150">StorSimple 會建立容錯移轉作業。</span><span class="sxs-lookup"><span data-stu-id="98cb5-150">StorSimple creates a failover job.</span></span> <span data-ttu-id="98cb5-151">按一下 [作業通知]，以透過 [作業] 刀鋒視窗監視容錯移轉作業。</span><span class="sxs-lookup"><span data-stu-id="98cb5-151">Click the job notification to monitor the failover job via the **Jobs** blade.</span></span>

    <span data-ttu-id="98cb5-152">如果要容錯移轉的磁碟區容器包含本機磁碟區，則您會看到容器中每個本機磁碟區 (除分層磁碟區外) 的還原作業。</span><span class="sxs-lookup"><span data-stu-id="98cb5-152">If the volume container that you failed over has local volumes, then you see individual restore jobs for each local volume (not for tiered volumes) in the container.</span></span> <span data-ttu-id="98cb5-153">這些還原作業可能需要一段時間才能完成。</span><span class="sxs-lookup"><span data-stu-id="98cb5-153">These restore jobs may take quite some time to complete.</span></span> <span data-ttu-id="98cb5-154">容錯移轉作業可能會較早完成。</span><span class="sxs-lookup"><span data-stu-id="98cb5-154">It is likely that the failover job may complete earlier.</span></span> <span data-ttu-id="98cb5-155">還原作業完成之後這些磁碟區才有本機保證。</span><span class="sxs-lookup"><span data-stu-id="98cb5-155">These volumes will have local guarantees only after the restore jobs are complete.</span></span>

    ![監視容錯移轉作業](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

9. <span data-ttu-id="98cb5-157">完成容錯移轉後，移至 [裝置] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="98cb5-157">After the failover is completed, go to the **Devices** blade.</span></span>
   
   1. <span data-ttu-id="98cb5-158">為容錯移轉程序選取要用來做為目標裝置的裝置。</span><span class="sxs-lookup"><span data-stu-id="98cb5-158">Select the device that was used as the target device for the failover process.</span></span>

       ![選取裝置](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

   2. <span data-ttu-id="98cb5-160">移至 [磁碟區容器] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="98cb5-160">Go to the **Volume Containers** blade.</span></span> <span data-ttu-id="98cb5-161">此時應會列出所有磁碟區容器以及舊裝置中的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="98cb5-161">All the volume containers, along with the volumes from the old device, should be listed.</span></span>

       ![檢視目標磁碟區容器](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev16.png)


## <a name="next-steps"></a><span data-ttu-id="98cb5-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="98cb5-163">Next steps</span></span>

* <span data-ttu-id="98cb5-164">執行容錯移轉之後，您可能需要 [停用或刪除 StorSimple 裝置](storsimple-8000-deactivate-and-delete-device.md)。</span><span class="sxs-lookup"><span data-stu-id="98cb5-164">After you have performed a failover, you may need to [deactivate or delete your StorSimple device](storsimple-8000-deactivate-and-delete-device.md).</span></span>
* <span data-ttu-id="98cb5-165">如需如何使用 StorSimple 裝置管理員服務的相關資訊，請移至[使用 StorSimple 裝置管理員服務管理 StorSimple 裝置](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="98cb5-165">For information about how to use the StorSimple Device Manager service, go to [Use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

