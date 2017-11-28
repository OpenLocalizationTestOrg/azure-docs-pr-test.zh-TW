---
title: "aaaStorSimple 容錯移轉時，適用於 8000 系列裝置的災害復原 |Microsoft 文件"
description: "深入了解如何透過您的 StorSimple 裝置 toohello toofail 相同的裝置。"
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
ms.date: 06/23/2017
ms.author: alkohli
ms.openlocfilehash: b0b4216c7af6745ff68b85ca3d655691b43b4334
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-your-storsimple-physical-device-toosame-device"></a><span data-ttu-id="d9515-103">容錯移轉您的 StorSimple 實體裝置 toosame 裝置</span><span class="sxs-lookup"><span data-stu-id="d9515-103">Fail over your StorSimple physical device toosame device</span></span>

## <a name="overview"></a><span data-ttu-id="d9515-104">概觀</span><span class="sxs-lookup"><span data-stu-id="d9515-104">Overview</span></span>

<span data-ttu-id="d9515-105">如果沒有損毀，本教學課程的描述 hello 步驟需要的 toofail StorSimple 8000 系列實體裝置 tooitself。</span><span class="sxs-lookup"><span data-stu-id="d9515-105">This tutorial describes hello steps required toofail over a StorSimple 8000 series physical device tooitself if there is a disaster.</span></span> <span data-ttu-id="d9515-106">StorSimple 會使用 hello 裝置容錯移轉功能 toomigrate 資料來源的實體裝置在 hello datacenter tooanother 實體裝置中。</span><span class="sxs-lookup"><span data-stu-id="d9515-106">StorSimple uses hello device failover feature toomigrate data from a source physical device in hello datacenter tooanother physical device.</span></span> <span data-ttu-id="d9515-107">本教學課程中的 hello 指導方針適用於執行軟體版本更新 3 及更新版本的 tooStorSimple 8000 系列實體裝置。</span><span class="sxs-lookup"><span data-stu-id="d9515-107">hello guidance in this tutorial applies tooStorSimple 8000 series physical devices running software versions Update 3 and later.</span></span>

<span data-ttu-id="d9515-108">深入了解裝置容錯移轉和就是從嚴重損毀，使用的 toorecover toolearn 移過[StorSimple 8000 系列裝置的容錯移轉和災害復原](storsimple-8000-device-failover-disaster-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="d9515-108">toolearn more about device failover and how it is used toorecover from a disaster, go too[Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

<span data-ttu-id="d9515-109">toofail 透過實體裝置 tooanother 實體裝置，請跳過[相同容錯移轉 toohello StorSimple 實體裝置](storsimple-8000-device-failover-physical-device.md)。</span><span class="sxs-lookup"><span data-stu-id="d9515-109">toofail over a physical device tooanother physical device, go too[Fail over toohello same StorSimple physical device](storsimple-8000-device-failover-physical-device.md).</span></span> <span data-ttu-id="d9515-110">透過 StorSimple 雲端應用裝置，StorSimple 實體裝置 tooa toofail 移過[容錯移轉 tooa StorSimple 雲端應用裝置](storsimple-8000-device-failover-cloud-appliance.md)。</span><span class="sxs-lookup"><span data-stu-id="d9515-110">toofail over a StorSimple physical device tooa StorSimple Cloud Appliance, go too[Fail over tooa StorSimple Cloud Appliance](storsimple-8000-device-failover-cloud-appliance.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="d9515-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="d9515-111">Prerequisites</span></span>

- <span data-ttu-id="d9515-112">請確定您已檢閱 hello 考量用於裝置容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="d9515-112">Ensure that you have reviewed hello considerations for device failover.</span></span> <span data-ttu-id="d9515-113">如需詳細資訊，請移至太[用於裝置容錯移轉的一般考量](storsimple-8000-device-failover-disaster-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="d9515-113">For more information, go too[Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md).</span></span>


## <a name="steps-toofail-over-toohello-same-device"></a><span data-ttu-id="d9515-114">步驟 toofail toohello 透過相同的裝置</span><span class="sxs-lookup"><span data-stu-id="d9515-114">Steps toofail over toohello same device</span></span>

<span data-ttu-id="d9515-115">執行下列步驟，若要透過 toohello toofail hello 相同的裝置。</span><span class="sxs-lookup"><span data-stu-id="d9515-115">Perform hello following steps if you need toofail over toohello same device.</span></span>

1. <span data-ttu-id="d9515-116">在您的裝置擷取所有 hello 磁碟區的雲端快照。</span><span class="sxs-lookup"><span data-stu-id="d9515-116">Take cloud snapshots of all hello volumes in your device.</span></span> <span data-ttu-id="d9515-117">如需詳細資訊，請移至太[使用 StorSimple 裝置管理員服務 toocreate 備份](storsimple-8000-manage-backup-policies-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="d9515-117">For more information, go too[Use StorSimple Device Manager service toocreate backups](storsimple-8000-manage-backup-policies-u2.md).</span></span>
2. <span data-ttu-id="d9515-118">重設您的裝置 toofactory 預設值。</span><span class="sxs-lookup"><span data-stu-id="d9515-118">Reset your device toofactory defaults.</span></span> <span data-ttu-id="d9515-119">請遵循 hello 詳細中的指示[tooreset StorSimple 裝置 toofactory 預設設定的方式](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings)。</span><span class="sxs-lookup"><span data-stu-id="d9515-119">Follow hello detailed instructions in [how tooreset a StorSimple device toofactory default settings](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>
3. <span data-ttu-id="d9515-120">移 toohello StorSimple 裝置管理員服務，然後選取**裝置**。</span><span class="sxs-lookup"><span data-stu-id="d9515-120">Go toohello StorSimple Device Manager service and then select **Devices**.</span></span> <span data-ttu-id="d9515-121">在 hello**裝置**刀鋒視窗中，hello 舊裝置應顯示為**離線**。</span><span class="sxs-lookup"><span data-stu-id="d9515-121">In hello **Devices** blade, hello old device should show as **Offline**.</span></span>

    ![來源裝置離線](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev2.png)

4. <span data-ttu-id="d9515-123">設定裝置，並再次使用 StorSimple 裝置管理員服務重新註冊裝置。</span><span class="sxs-lookup"><span data-stu-id="d9515-123">Configure your device and register it again with your StorSimple Device Manager service.</span></span> <span data-ttu-id="d9515-124">hello 新註冊的裝置應顯示為**已 tooset 準備註冊**。</span><span class="sxs-lookup"><span data-stu-id="d9515-124">hello newly registered device should show as **Ready tooset up**.</span></span> <span data-ttu-id="d9515-125">hello hello 新裝置的裝置名稱為的 hello 相同 hello 舊裝置但加上數字 tooindicate hello 裝置已重設 toofactory 預設和已註冊一次。</span><span class="sxs-lookup"><span data-stu-id="d9515-125">hello device name for hello new device is hello same as hello old device but appended with a numeral tooindicate that hello device was reset toofactory default and registered again.</span></span>

    ![新註冊的裝置準備好 tooset 向上](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev3.png)
5. <span data-ttu-id="d9515-127">Hello 新裝置，來完成 hello 裝置安裝。</span><span class="sxs-lookup"><span data-stu-id="d9515-127">For hello new device, complete hello device setup.</span></span> <span data-ttu-id="d9515-128">如需詳細資訊，請移至太[步驟 4： 完成基本裝置設定](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup)。</span><span class="sxs-lookup"><span data-stu-id="d9515-128">For more information, go too[Step 4: Complete minimum device setup](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup).</span></span> <span data-ttu-id="d9515-129">在 hello**裝置**刀鋒視窗中，hello 裝置 hello 狀態變更太**線上**。</span><span class="sxs-lookup"><span data-stu-id="d9515-129">On hello **Devices** blade, hello status of hello device changes too**Online**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="d9515-130">**首先，完成 hello 最低設定，或您的 DR 可能會失敗。**</span><span class="sxs-lookup"><span data-stu-id="d9515-130">**Complete hello minimum configuration first, or your DR may fail.**</span></span>

    ![新註冊的裝置狀態為線上](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev7.png)

6. <span data-ttu-id="d9515-132">選取 hello 舊裝置 （離線狀態），然後在 hello 命令列中，按一下**容錯移轉**。</span><span class="sxs-lookup"><span data-stu-id="d9515-132">Select hello old device (status offline) and from hello command bar, click **Fail over**.</span></span> <span data-ttu-id="d9515-133">在 hello**容錯移轉**刀鋒視窗中，選取舊裝置做為 hello 來源並指定 hello 目標裝置 hello 新註冊的裝置。</span><span class="sxs-lookup"><span data-stu-id="d9515-133">In hello **Fail over** blade, select old device as hello source and specify hello target device as hello newly registered device.</span></span>

    ![容錯移轉摘要](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev11.png)

    <span data-ttu-id="d9515-135">如需詳細指示，請參閱太[容錯移轉 tooanother 實體裝置](#fail-over-to-another-physical-device)。</span><span class="sxs-lookup"><span data-stu-id="d9515-135">For detailed instructions, refer too[Fail over tooanother physical device](#fail-over-to-another-physical-device).</span></span>

7. <span data-ttu-id="d9515-136">裝置還原作業會建立您可以監視從 hello**作業**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d9515-136">A device restore job is created that you can monitor from hello **Jobs** blade.</span></span>

8. <span data-ttu-id="d9515-137">Hello 作業已成功完成之後，存取 hello 新裝置，並瀏覽 toohello**磁碟區容器**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d9515-137">After hello job has successfully completed, access hello new device and navigate toohello **Volume containers** blade.</span></span> <span data-ttu-id="d9515-138">請確認所有 hello 磁碟區容器從 hello 舊裝置已都移轉 toohello 新裝置。</span><span class="sxs-lookup"><span data-stu-id="d9515-138">Verify that all hello volume containers from hello old device have migrated toohello new device.</span></span>

   ![移轉磁碟區容器](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev13.png)

9. <span data-ttu-id="d9515-140">Hello 容錯移轉已完成之後，您可以停用並刪除 hello 入口網站中的 hello 舊裝置。</span><span class="sxs-lookup"><span data-stu-id="d9515-140">After hello failover is complete, you can deactivate and delete hello old device from hello portal.</span></span> <span data-ttu-id="d9515-141">選取 hello 舊裝置 （離線），以滑鼠右鍵按一下，然後再選取**停用**。</span><span class="sxs-lookup"><span data-stu-id="d9515-141">Select hello old device (offline), right-click, and then select **Deactivate**.</span></span> <span data-ttu-id="d9515-142">Hello 裝置停用後，會更新 hello 裝置 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="d9515-142">After hello device is deactivated, hello status of hello device is updated.</span></span>

     ![停用來源裝置](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev14.png)

10. <span data-ttu-id="d9515-144">選取 hello 停用裝置，以滑鼠右鍵按一下，然後選取**刪除**。</span><span class="sxs-lookup"><span data-stu-id="d9515-144">Select hello deactivated device, right-click, and then select **Delete**.</span></span> <span data-ttu-id="d9515-145">這會從裝置 hello 清單刪除 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="d9515-145">This deletes hello device from hello list of devices.</span></span>

    ![刪除來源裝置](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev15.png)



## <a name="next-steps"></a><span data-ttu-id="d9515-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d9515-147">Next steps</span></span>

* <span data-ttu-id="d9515-148">在您執行容錯移轉之後，您可能需要過[停用或刪除您的 StorSimple 裝置](storsimple-8000-deactivate-and-delete-device.md)。</span><span class="sxs-lookup"><span data-stu-id="d9515-148">After you have performed a failover, you may need too[deactivate or delete your StorSimple device](storsimple-8000-deactivate-and-delete-device.md).</span></span>
* <span data-ttu-id="d9515-149">如需如何 toouse hello StorSimple 裝置管理員服務，請跳過[使用 hello StorSimple 裝置管理員服務 tooadminister StorSimple 裝置](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="d9515-149">For information about how toouse hello StorSimple Device Manager service, go too[Use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

