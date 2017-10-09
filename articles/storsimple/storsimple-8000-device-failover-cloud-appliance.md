---
title: "aaaStorSimple 容錯移轉，災害復原 tooa StorSimple 雲端應用裝置 |Microsoft 文件"
description: "了解如何透過您的 StorSimple 8000 系列實體裝置 tooa toofail 雲端應用裝置。"
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
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: e8a0bca057024358e3a557fe85a42ddefea36cff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-tooyour-storsimple-cloud-appliance"></a><span data-ttu-id="208d7-103">容錯移轉 tooyour StorSimple 雲端應用裝置</span><span class="sxs-lookup"><span data-stu-id="208d7-103">Fail over tooyour StorSimple Cloud Appliance</span></span>

## <a name="overview"></a><span data-ttu-id="208d7-104">概觀</span><span class="sxs-lookup"><span data-stu-id="208d7-104">Overview</span></span>

<span data-ttu-id="208d7-105">如果沒有損毀，本教學課程的描述 hello 步驟需要的 toofail StorSimple 8000 系列實體裝置 tooa StorSimple 雲端應用裝置。</span><span class="sxs-lookup"><span data-stu-id="208d7-105">This tutorial describes hello steps required toofail over a StorSimple 8000 series physical device tooa StorSimple Cloud Appliance if there is a disaster.</span></span> <span data-ttu-id="208d7-106">StorSimple 會使用 hello 裝置容錯移轉功能 toomigrate 資料來源的實體裝置在 hello datacenter tooa 雲端應用裝置在 Azure 中執行。</span><span class="sxs-lookup"><span data-stu-id="208d7-106">StorSimple uses hello device failover feature toomigrate data from a source physical device in hello datacenter tooa cloud appliance running in Azure.</span></span> <span data-ttu-id="208d7-107">本教學課程中的 hello 指導方針適用於 tooStorSimple 8000 系列實體裝置和執行軟體版本更新 3 及更新版本的雲端應用裝置。</span><span class="sxs-lookup"><span data-stu-id="208d7-107">hello guidance in this tutorial applies tooStorSimple 8000 series physical devices and cloud appliances running software versions Update 3 and later.</span></span>

<span data-ttu-id="208d7-108">深入了解裝置容錯移轉和就是從嚴重損毀，使用的 toorecover toolearn 移過[StorSimple 8000 系列裝置的容錯移轉和災害復原](storsimple-8000-device-failover-disaster-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="208d7-108">toolearn more about device failover and how it is used toorecover from a disaster, go too[Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

<span data-ttu-id="208d7-109">透過 StorSimple 實體裝置 tooanother 實體裝置，toofail 移過[容錯移轉 tooa StorSimple 實體裝置](storsimple-8000-device-failover-physical-device.md)。</span><span class="sxs-lookup"><span data-stu-id="208d7-109">toofail over a StorSimple physical device tooanother physical device, go too[Fail over tooa StorSimple physical device](storsimple-8000-device-failover-physical-device.md).</span></span> <span data-ttu-id="208d7-110">透過裝置 tooitself，toofail 移過[相同容錯移轉 toohello StorSimple 實體裝置](storsimple-8000-device-failover-same-device.md)。</span><span class="sxs-lookup"><span data-stu-id="208d7-110">toofail over a device tooitself, go too[Fail over toohello same StorSimple physical device](storsimple-8000-device-failover-same-device.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="208d7-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="208d7-111">Prerequisites</span></span>

- <span data-ttu-id="208d7-112">請確定您已檢閱 hello 考量用於裝置容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="208d7-112">Ensure that you have reviewed hello considerations for device failover.</span></span> <span data-ttu-id="208d7-113">如需詳細資訊，請移至太[用於裝置容錯移轉的一般考量](storsimple-8000-device-failover-disaster-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="208d7-113">For more information, go too[Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

- <span data-ttu-id="208d7-114">執行此程序之前，您必須已建立並設定 StorSimple 雲端設備。</span><span class="sxs-lookup"><span data-stu-id="208d7-114">You must have a StorSimple Cloud Appliance created and configured before running this procedure.</span></span> <span data-ttu-id="208d7-115">如果執行更新 3 的軟體版本或更新版本中，請考慮使用 8020 雲端應用裝置 hello DR。</span><span class="sxs-lookup"><span data-stu-id="208d7-115">If running   Update 3 software version or later, consider using an 8020 cloud appliance for hello DR.</span></span> <span data-ttu-id="208d7-116">hello 8020 模型具有 64 TB，並使用進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="208d7-116">hello 8020 model has 64 TB and uses Premium Storage.</span></span> <span data-ttu-id="208d7-117">如需詳細資訊，請移至太[部署和管理 StorSimple 雲端應用裝置](storsimple-8000-cloud-appliance-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="208d7-117">For more information, go too[Deploy and manage a StorSimple Cloud Appliance](storsimple-8000-cloud-appliance-u2.md).</span></span>

## <a name="steps-toofail-over-tooa-cloud-appliance"></a><span data-ttu-id="208d7-118">步驟 toofail 透過 tooa 雲端應用裝置</span><span class="sxs-lookup"><span data-stu-id="208d7-118">Steps toofail over tooa cloud appliance</span></span>

<span data-ttu-id="208d7-119">執行下列步驟 toorestore hello 裝置 tooa 目標 StorSimple 雲端應用裝置 hello。</span><span class="sxs-lookup"><span data-stu-id="208d7-119">Perform hello following steps toorestore hello device tooa target StorSimple Cloud Appliance.</span></span>

1.  <span data-ttu-id="208d7-120">請確認您想 toofail 透過 hello 磁碟區容器具有相關聯的雲端快照。</span><span class="sxs-lookup"><span data-stu-id="208d7-120">Verify that hello volume container you want toofail over has associated cloud snapshots.</span></span> <span data-ttu-id="208d7-121">如需詳細資訊，請移至太[使用 StorSimple 裝置管理員服務 toocreate 備份](storsimple-8000-manage-backup-policies-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="208d7-121">For more information, go too[Use StorSimple Device Manager service toocreate backups](storsimple-8000-manage-backup-policies-u2.md).</span></span>
2. <span data-ttu-id="208d7-122">移 tooyour StorSimple 裝置管理員服務，然後按一下**裝置**。</span><span class="sxs-lookup"><span data-stu-id="208d7-122">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="208d7-123">在 hello**裝置**刀鋒視窗、 移 toohello 清單與您的服務連接的裝置。</span><span class="sxs-lookup"><span data-stu-id="208d7-123">In hello **Devices** blade, go toohello list of devices connected with your service.</span></span>
    <span data-ttu-id="208d7-124">![選取裝置](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)</span><span class="sxs-lookup"><span data-stu-id="208d7-124">![Select device](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)</span></span>
3. <span data-ttu-id="208d7-125">選取並按一下您的來源裝置。</span><span class="sxs-lookup"><span data-stu-id="208d7-125">Select and click your source device.</span></span> <span data-ttu-id="208d7-126">hello 來源裝置沒有您想 toofail 透過的 hello 磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="208d7-126">hello source device has hello volume containers that you want toofail over.</span></span> <span data-ttu-id="208d7-127">跳過**設定 > 磁碟區容器**。</span><span class="sxs-lookup"><span data-stu-id="208d7-127">Go too**Settings > Volume Containers**.</span></span>

    ![選取裝置](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev2.png)
    
4. <span data-ttu-id="208d7-129">選取您想要 toofail tooanother 裝置上的磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="208d7-129">Select a volume container that you would like toofail over tooanother device.</span></span> <span data-ttu-id="208d7-130">按一下 hello 磁碟區容器 toodisplay hello 清單內這個容器的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="208d7-130">Click hello volume container toodisplay hello list of volumes within this container.</span></span> <span data-ttu-id="208d7-131">選取磁碟區，按一下滑鼠右鍵，然後按一下**離線**tootake hello 磁碟區離線。</span><span class="sxs-lookup"><span data-stu-id="208d7-131">Select a volume, right-click, and click **Take Offline** tootake hello volume offline.</span></span>

    ![選取裝置](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev5.png)

5. <span data-ttu-id="208d7-133">Hello 磁碟區容器中的所有 hello 磁碟區都重複此程序。</span><span class="sxs-lookup"><span data-stu-id="208d7-133">Repeat this process for all hello volumes in hello volume container.</span></span>

     ![選取裝置](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev7.png)

6. <span data-ttu-id="208d7-135">Hello 重複上一個步驟的所有 hello 磁碟區容器想 toofail tooanother 裝置上。</span><span class="sxs-lookup"><span data-stu-id="208d7-135">Repeat hello previous step for all hello volume containers you would like toofail over tooanother device.</span></span>

7. <span data-ttu-id="208d7-136">返回 toohello**裝置**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="208d7-136">Go back toohello **Devices** blade.</span></span> <span data-ttu-id="208d7-137">在 hello 命令列中，按一下**容錯移轉**。</span><span class="sxs-lookup"><span data-stu-id="208d7-137">From hello command bar, click **Fail over**.</span></span>

    ![按一下 [容錯移轉]](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev8.png)
8. <span data-ttu-id="208d7-139">在 hello**容錯移轉**刀鋒視窗中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="208d7-139">In hello **Fail over** blade, perform hello following steps:</span></span>
   
    1. <span data-ttu-id="208d7-140">按一下 [來源]。</span><span class="sxs-lookup"><span data-stu-id="208d7-140">Click **Source**.</span></span> <span data-ttu-id="208d7-141">透過選取 hello 磁碟區容器 toofail。</span><span class="sxs-lookup"><span data-stu-id="208d7-141">Select hello volume containers toofail over.</span></span> <span data-ttu-id="208d7-142">**只有 hello 與相關聯的雲端快照集磁碟區容器，並且顯示離線的磁碟區。**</span><span class="sxs-lookup"><span data-stu-id="208d7-142">**Only hello volume containers with associated cloud snapshots and offline volumes are displayed.**</span></span>
        <span data-ttu-id="208d7-143">![選取來源](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png)</span><span class="sxs-lookup"><span data-stu-id="208d7-143">![Select source](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png)</span></span>
    2. <span data-ttu-id="208d7-144">按一下 [目標]。</span><span class="sxs-lookup"><span data-stu-id="208d7-144">Click **Target**.</span></span> <span data-ttu-id="208d7-145">從可用的裝置 hello 下拉式清單中選取目標雲端應用裝置。</span><span class="sxs-lookup"><span data-stu-id="208d7-145">Select a target cloud appliance from hello dropdown list of available devices.</span></span> <span data-ttu-id="208d7-146">**只有 hello 裝置具有足夠的容量 tooaccommodate 來源磁碟區容器會顯示在 [hello] 清單。**</span><span class="sxs-lookup"><span data-stu-id="208d7-146">**Only hello devices that have sufficient capacity tooaccommodate source volume containers are displayed in hello list.**</span></span>

        ![選取目標](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev12.png)

    3. <span data-ttu-id="208d7-148">檢閱下方的 hello 容錯移轉設定**摘要**並選取 [hello] 核取方塊，指出選取的磁碟區容器中的 hello 磁碟區會離線。</span><span class="sxs-lookup"><span data-stu-id="208d7-148">Review hello failover settings under **Summary** and select hello checkbox indicating that hello volumes in selected volume containers are offline.</span></span> 

        ![檢閱容錯移轉設定](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev13.png)

9. <span data-ttu-id="208d7-150">已建立容錯移轉作業。</span><span class="sxs-lookup"><span data-stu-id="208d7-150">A failover job is created.</span></span> <span data-ttu-id="208d7-151">toomonitor hello 容錯移轉作業中，按一下 hello 工作通知。</span><span class="sxs-lookup"><span data-stu-id="208d7-151">toomonitor hello failover job, click hello job notification.</span></span>

    ![監視容錯移轉作業](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

10. <span data-ttu-id="208d7-153">Hello 容錯移轉完成之後，請回到 toohello**裝置**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="208d7-153">After hello failover is completed, go back toohello **Devices** blade.</span></span>

    1. <span data-ttu-id="208d7-154">選取已作為 hello 目標 hello 容錯移轉的 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="208d7-154">Select hello device that was used as hello target for hello failover.</span></span>

       ![選取裝置](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

    2. <span data-ttu-id="208d7-156">按一下 [磁碟區容器]。</span><span class="sxs-lookup"><span data-stu-id="208d7-156">Click **Volume Containers**.</span></span> <span data-ttu-id="208d7-157">應該會列出所有 hello 磁碟區容器以及舊裝置 hello 中的 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="208d7-157">All hello volume containers, along with hello volumes from hello old device, should be listed.</span></span>

       <span data-ttu-id="208d7-158">如果 hello 容錯移轉的磁碟區容器具有本機固定磁碟區，這些磁碟區無法透過與分層磁碟區。</span><span class="sxs-lookup"><span data-stu-id="208d7-158">If hello volume container that you failed over has locally pinned volumes, those volumes are failed over as tiered volumes.</span></span> <span data-ttu-id="208d7-159">StorSimple 雲端設備不支援已固定在本機的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="208d7-159">Locally pinned volumes are not supported on a StorSimple Cloud Appliance.</span></span>

       ![檢視目標磁碟區容器](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev17.png)


## <a name="next-steps"></a><span data-ttu-id="208d7-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="208d7-161">Next steps</span></span>

* <span data-ttu-id="208d7-162">在您執行容錯移轉之後，您可能需要過[停用或刪除您的 StorSimple 裝置](storsimple-8000-deactivate-and-delete-device.md)。</span><span class="sxs-lookup"><span data-stu-id="208d7-162">After you have performed a failover, you may need too[deactivate or delete your StorSimple device](storsimple-8000-deactivate-and-delete-device.md).</span></span>

* <span data-ttu-id="208d7-163">如需如何 toouse hello StorSimple 裝置管理員服務，請跳過[使用 hello StorSimple 裝置管理員服務 tooadminister StorSimple 裝置](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="208d7-163">For information about how toouse hello StorSimple Device Manager service, go too[Use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

