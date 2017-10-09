---
title: "aaaStorSimple 容錯移轉，災害復原 tooa StorSimple 8000 系列實體裝置 |Microsoft 文件"
description: "深入了解如何 toofail 透過 StorSimple 8000 系列實體裝置 tooanother 實體裝置。"
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
ms.openlocfilehash: 29d2576a96c446ff5ffcd98dcd0f5a07f1ab08ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-tooa-storsimple-8000-series-physical-device"></a><span data-ttu-id="b6c58-103">容錯移轉 tooa StorSimple 8000 系列實體裝置</span><span class="sxs-lookup"><span data-stu-id="b6c58-103">Fail over tooa StorSimple 8000 series physical device</span></span>

## <a name="overview"></a><span data-ttu-id="b6c58-104">概觀</span><span class="sxs-lookup"><span data-stu-id="b6c58-104">Overview</span></span>

<span data-ttu-id="b6c58-105">如果沒有損毀，本教學課程的描述 hello 步驟需要的 toofail StorSimple 8000 系列實體裝置 tooanother StorSimple 實體裝置。</span><span class="sxs-lookup"><span data-stu-id="b6c58-105">This tutorial describes hello steps required toofail over a StorSimple 8000 series physical device tooanother StorSimple physical device if there is a disaster.</span></span> <span data-ttu-id="b6c58-106">StorSimple 會使用 hello 裝置容錯移轉功能 toomigrate 資料來源的實體裝置在 hello datacenter tooanother 實體裝置中。</span><span class="sxs-lookup"><span data-stu-id="b6c58-106">StorSimple uses hello device failover feature toomigrate data from a source physical device in hello datacenter tooanother physical device.</span></span> <span data-ttu-id="b6c58-107">本教學課程中的 hello 指導方針適用於執行軟體版本更新 3 及更新版本的 tooStorSimple 8000 系列實體裝置。</span><span class="sxs-lookup"><span data-stu-id="b6c58-107">hello guidance in this tutorial applies tooStorSimple 8000 series physical devices running software versions Update 3 and later.</span></span>

<span data-ttu-id="b6c58-108">深入了解裝置容錯移轉和就是從嚴重損毀，使用的 toorecover toolearn 移過[StorSimple 8000 系列裝置的容錯移轉和災害復原](storsimple-8000-device-failover-disaster-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="b6c58-108">toolearn more about device failover and how it is used toorecover from a disaster, go too[Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

<span data-ttu-id="b6c58-109">透過 StorSimple 雲端應用裝置，StorSimple 實體裝置 tooa toofail 移過[容錯移轉 tooa StorSimple 雲端應用裝置](storsimple-8000-device-failover-cloud-appliance.md)。</span><span class="sxs-lookup"><span data-stu-id="b6c58-109">toofail over a StorSimple physical device tooa StorSimple Cloud Appliance, go too[Fail over tooa StorSimple Cloud Appliance](storsimple-8000-device-failover-cloud-appliance.md).</span></span> <span data-ttu-id="b6c58-110">透過實體裝置 tooitself，toofail 移過[相同容錯移轉 toohello StorSimple 實體裝置](storsimple-8000-device-failover-same-device.md)。</span><span class="sxs-lookup"><span data-stu-id="b6c58-110">toofail over a physical device tooitself, go too[Fail over toohello same StorSimple physical device](storsimple-8000-device-failover-same-device.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="b6c58-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="b6c58-111">Prerequisites</span></span>

- <span data-ttu-id="b6c58-112">請確定您已檢閱 hello 考量用於裝置容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="b6c58-112">Ensure that you have reviewed hello considerations for device failover.</span></span> <span data-ttu-id="b6c58-113">如需詳細資訊，請移至太[用於裝置容錯移轉的一般考量](storsimple-8000-device-failover-disaster-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="b6c58-113">For more information, go too[Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

- <span data-ttu-id="b6c58-114">您必須在 StorSimple 8000 系列實體裝置 hello datacenter 中部署。</span><span class="sxs-lookup"><span data-stu-id="b6c58-114">You must have a StorSimple 8000 series physical device deployed in hello datacenter.</span></span> <span data-ttu-id="b6c58-115">hello 裝置必須執行 Update 3 或更新的軟體版本。</span><span class="sxs-lookup"><span data-stu-id="b6c58-115">hello device must run Update 3 or later software version.</span></span> <span data-ttu-id="b6c58-116">如需詳細資訊，請移至太[部署在內部部署 StorSimple 裝置](storsimple-8000-deployment-walkthrough-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="b6c58-116">For more information, go too[Deploy your on-premises StorSimple device](storsimple-8000-deployment-walkthrough-u2.md).</span></span>


## <a name="steps-toofail-over-tooa-physical-device"></a><span data-ttu-id="b6c58-117">透過 tooa 實體裝置的步驟 toofail</span><span class="sxs-lookup"><span data-stu-id="b6c58-117">Steps toofail over tooa physical device</span></span>

<span data-ttu-id="b6c58-118">執行下列步驟 toorestore hello 裝置 tooa 目標實體裝置。</span><span class="sxs-lookup"><span data-stu-id="b6c58-118">Perform hello following steps toorestore your device tooa target physical device.</span></span>

1. <span data-ttu-id="b6c58-119">請確認您想 toofail 透過 hello 磁碟區容器具有相關聯的雲端快照。</span><span class="sxs-lookup"><span data-stu-id="b6c58-119">Verify that hello volume container you want toofail over has associated cloud snapshots.</span></span> <span data-ttu-id="b6c58-120">如需詳細資訊，請移至太[使用 StorSimple 裝置管理員服務 toocreate 備份](storsimple-8000-manage-backup-policies-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="b6c58-120">For more information, go too[Use StorSimple Device Manager service toocreate backups](storsimple-8000-manage-backup-policies-u2.md).</span></span>
2. <span data-ttu-id="b6c58-121">在 tooyour StorSimple 裝置管理員 的 **裝置**。</span><span class="sxs-lookup"><span data-stu-id="b6c58-121">Go tooyour StorSimple Device Manager and then click **Devices**.</span></span> <span data-ttu-id="b6c58-122">在 hello**裝置**刀鋒視窗、 移 toohello 清單與您的服務連接的裝置。</span><span class="sxs-lookup"><span data-stu-id="b6c58-122">In hello **Devices** blade, go toohello list of devices connected with your service.</span></span>
    <span data-ttu-id="b6c58-123">![選取裝置](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev1.png)</span><span class="sxs-lookup"><span data-stu-id="b6c58-123">![Select device](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev1.png)</span></span>
3. <span data-ttu-id="b6c58-124">選取並按一下您的來源裝置。</span><span class="sxs-lookup"><span data-stu-id="b6c58-124">Select and click your source device.</span></span> <span data-ttu-id="b6c58-125">hello 來源裝置沒有您想 toofail 透過的 hello 磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="b6c58-125">hello source device has hello volume containers that you want toofail over.</span></span> <span data-ttu-id="b6c58-126">跳過**設定 > 磁碟區容器**。</span><span class="sxs-lookup"><span data-stu-id="b6c58-126">Go too**Settings > Volume Containers**.</span></span>
4. <span data-ttu-id="b6c58-127">選取您想要 toofail tooanother 裝置上的磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="b6c58-127">Select a volume container that you would like toofail over tooanother device.</span></span> <span data-ttu-id="b6c58-128">按一下 hello 磁碟區容器 toodisplay hello 清單內這個容器的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b6c58-128">Click hello volume container toodisplay hello list of volumes within this container.</span></span> <span data-ttu-id="b6c58-129">選取磁碟區，按一下滑鼠右鍵，然後按一下**離線**tootake hello 磁碟區離線。</span><span class="sxs-lookup"><span data-stu-id="b6c58-129">Select a volume, right-click, and click **Take Offline** tootake hello volume offline.</span></span> <span data-ttu-id="b6c58-130">Hello 磁碟區容器中的所有 hello 磁碟區都重複此程序。</span><span class="sxs-lookup"><span data-stu-id="b6c58-130">Repeat this process for all hello volumes in hello volume container.</span></span>
5. <span data-ttu-id="b6c58-131">Hello 重複上一個步驟的所有 hello 磁碟區容器想 toofail tooanother 裝置上。</span><span class="sxs-lookup"><span data-stu-id="b6c58-131">Repeat hello previous step for all hello volume containers you would like toofail over tooanother device.</span></span>
6. <span data-ttu-id="b6c58-132">返回 toohello**裝置**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b6c58-132">Go back toohello **Devices** blade.</span></span> <span data-ttu-id="b6c58-133">在 hello 命令列中，按一下**容錯移轉**。</span><span class="sxs-lookup"><span data-stu-id="b6c58-133">From hello command bar, click **Fail over**.</span></span>
    <span data-ttu-id="b6c58-134">按一下 [容錯移轉]![](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev2.png)</span><span class="sxs-lookup"><span data-stu-id="b6c58-134">![Click fail over](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev2.png)</span></span>
    
7. <span data-ttu-id="b6c58-135">在 hello**容錯移轉**刀鋒視窗中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="b6c58-135">In hello **Fail over** blade, perform hello following steps:</span></span>
   
   1. <span data-ttu-id="b6c58-136">按一下 [來源]。</span><span class="sxs-lookup"><span data-stu-id="b6c58-136">Click **Source**.</span></span> <span data-ttu-id="b6c58-137">會顯示 hello 與雲端快照集的相關聯的磁碟區的磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="b6c58-137">hello volume containers with volumes associated with cloud snapshots are displayed.</span></span> <span data-ttu-id="b6c58-138">只顯示 hello 容器是可進行容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="b6c58-138">Only hello containers displayed are eligible for failover.</span></span> <span data-ttu-id="b6c58-139">Hello 清單中的磁碟區容器，選取您希望透過 toofail hello 磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="b6c58-139">In hello list of volume containers, select hello volume containers you would like toofail over.</span></span> <span data-ttu-id="b6c58-140">**只有 hello 與相關聯的雲端快照集磁碟區容器，並且顯示離線的磁碟區。**</span><span class="sxs-lookup"><span data-stu-id="b6c58-140">**Only hello volume containers with associated cloud snapshots and offline volumes are displayed.**</span></span>

       ![選取來源](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev5.png)
   2. <span data-ttu-id="b6c58-142">按一下 [目標]。</span><span class="sxs-lookup"><span data-stu-id="b6c58-142">Click **Target**.</span></span> <span data-ttu-id="b6c58-143">Hello hello 先前步驟中選取的磁碟區容器，請從可用裝置 hello 下拉式清單中選取的目標裝置。</span><span class="sxs-lookup"><span data-stu-id="b6c58-143">For hello volume containers selected in hello previous step, select a target device from hello drop-down list of available devices.</span></span> <span data-ttu-id="b6c58-144">只有 hello 裝置具有足夠的容量 tooaccommodate 來源磁碟區容器會顯示在 [hello] 清單。</span><span class="sxs-lookup"><span data-stu-id="b6c58-144">Only hello devices that have sufficient capacity tooaccommodate source volume containers are displayed in hello list.</span></span>

        ![選取目標](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev6.png)

   3. <span data-ttu-id="b6c58-146">最後，檢閱下的所有 hello 容錯移轉設定**摘要**。</span><span class="sxs-lookup"><span data-stu-id="b6c58-146">Finally, review all hello failover settings under **Summary**.</span></span> <span data-ttu-id="b6c58-147">您已檢閱 hello 設定之後，選取 [hello] 核取方塊，指出選取的磁碟區容器中的 hello 磁碟區會離線。</span><span class="sxs-lookup"><span data-stu-id="b6c58-147">After you have reviewed hello settings, select hello checkbox indicating that hello volumes in selected volume containers are offline.</span></span> <span data-ttu-id="b6c58-148">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="b6c58-148">Click **OK**.</span></span>

       ![檢閱容錯移轉設定](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev8.png)
  
8. <span data-ttu-id="b6c58-150">StorSimple 會建立容錯移轉作業。</span><span class="sxs-lookup"><span data-stu-id="b6c58-150">StorSimple creates a failover job.</span></span> <span data-ttu-id="b6c58-151">按一下 hello 工作通知 toomonitor hello 容錯移轉工作透過 hello**作業**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b6c58-151">Click hello job notification toomonitor hello failover job via hello **Jobs** blade.</span></span>

    <span data-ttu-id="b6c58-152">如果您容錯移轉的 hello 磁碟區容器有本機磁碟區，您會看到每個本機磁碟區 （不適用於分層磁碟區） hello 容器中的個別還原作業。</span><span class="sxs-lookup"><span data-stu-id="b6c58-152">If hello volume container that you failed over has local volumes, then you see individual restore jobs for each local volume (not for tiered volumes) in hello container.</span></span> <span data-ttu-id="b6c58-153">這些還原作業可能需要一段時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="b6c58-153">These restore jobs may take quite some time toocomplete.</span></span> <span data-ttu-id="b6c58-154">它很可能稍早完成該 hello 容錯移轉工作。</span><span class="sxs-lookup"><span data-stu-id="b6c58-154">It is likely that hello failover job may complete earlier.</span></span> <span data-ttu-id="b6c58-155">只 hello 還原作業完成之後，這些磁碟區會有本機保證。</span><span class="sxs-lookup"><span data-stu-id="b6c58-155">These volumes will have local guarantees only after hello restore jobs are complete.</span></span>

    ![監視容錯移轉作業](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

9. <span data-ttu-id="b6c58-157">Hello 容錯移轉完成之後，請繼續 toohello**裝置**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b6c58-157">After hello failover is completed, go toohello **Devices** blade.</span></span>
   
   1. <span data-ttu-id="b6c58-158">選取 hello 裝置已用來作為 hello hello 容錯移轉程序的目標裝置。</span><span class="sxs-lookup"><span data-stu-id="b6c58-158">Select hello device that was used as hello target device for hello failover process.</span></span>

       ![選取裝置](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

   2. <span data-ttu-id="b6c58-160">移 toohello**磁碟區容器**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b6c58-160">Go toohello **Volume Containers** blade.</span></span> <span data-ttu-id="b6c58-161">應該會列出所有 hello 磁碟區容器以及舊裝置 hello 中的 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b6c58-161">All hello volume containers, along with hello volumes from hello old device, should be listed.</span></span>

       ![檢視目標磁碟區容器](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev16.png)


## <a name="next-steps"></a><span data-ttu-id="b6c58-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b6c58-163">Next steps</span></span>

* <span data-ttu-id="b6c58-164">在您執行容錯移轉之後，您可能需要過[停用或刪除您的 StorSimple 裝置](storsimple-8000-deactivate-and-delete-device.md)。</span><span class="sxs-lookup"><span data-stu-id="b6c58-164">After you have performed a failover, you may need too[deactivate or delete your StorSimple device](storsimple-8000-deactivate-and-delete-device.md).</span></span>
* <span data-ttu-id="b6c58-165">如需如何 toouse hello StorSimple 裝置管理員服務，請跳過[使用 hello StorSimple 裝置管理員服務 tooadminister StorSimple 裝置](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="b6c58-165">For information about how toouse hello StorSimple Device Manager service, go too[Use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

