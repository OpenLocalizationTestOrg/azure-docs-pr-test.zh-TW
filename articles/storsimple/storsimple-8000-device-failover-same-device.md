---
title: "8000 系列裝置的 StorSimple 容錯移轉和災害復原 | Microsoft Docs"
description: "了解如何將您的 StorSimple 裝置容錯移轉至相同的裝置。"
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
ms.openlocfilehash: acc8929dc3476e9590e8e4d9526b38b7c0719570
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="fail-over-your-storsimple-physical-device-to-same-device"></a><span data-ttu-id="6c90a-103">將您的 StorSimple 實體裝置容錯移轉至相同的裝置</span><span class="sxs-lookup"><span data-stu-id="6c90a-103">Fail over your StorSimple physical device to same device</span></span>

## <a name="overview"></a><span data-ttu-id="6c90a-104">概觀</span><span class="sxs-lookup"><span data-stu-id="6c90a-104">Overview</span></span>

<span data-ttu-id="6c90a-105">本教學課程說明出現災害時，將 StorSimple 8000 系列實體裝置容錯移轉至本身裝置所需要的步驟。</span><span class="sxs-lookup"><span data-stu-id="6c90a-105">This tutorial describes the steps required to fail over a StorSimple 8000 series physical device to itself if there is a disaster.</span></span> <span data-ttu-id="6c90a-106">StorSimple 會使用裝置容錯移轉功能，將資料從資料中心的實體裝置來源移轉至另一個實體裝置。</span><span class="sxs-lookup"><span data-stu-id="6c90a-106">StorSimple uses the device failover feature to migrate data from a source physical device in the datacenter to another physical device.</span></span> <span data-ttu-id="6c90a-107">本教學課程中的指導方針適用於執行軟體版本 Update 3 和更新版本的 StorSimple 8000 系列實體裝置。</span><span class="sxs-lookup"><span data-stu-id="6c90a-107">The guidance in this tutorial applies to StorSimple 8000 series physical devices running software versions Update 3 and later.</span></span>

<span data-ttu-id="6c90a-108">若要深入了解裝置容錯移轉，以及如何用於從災害中復原，請移至 [ StorSimple 8000 系列裝置的容錯移轉與災害復原](storsimple-8000-device-failover-disaster-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="6c90a-108">To learn more about device failover and how it is used to recover from a disaster, go to [Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

<span data-ttu-id="6c90a-109">若要將實體裝置容錯移轉至另一個實體裝置，請移至[容錯移轉至相同的 StorSimple 實體裝置](storsimple-8000-device-failover-physical-device.md)。</span><span class="sxs-lookup"><span data-stu-id="6c90a-109">To fail over a physical device to another physical device, go to [Fail over to the same StorSimple physical device](storsimple-8000-device-failover-physical-device.md).</span></span> <span data-ttu-id="6c90a-110">若要將 StorSimple 實體裝置容錯移轉至 StorSimple 雲端設備，請移至[容錯移轉至 StorSimple 雲端設備](storsimple-8000-device-failover-cloud-appliance.md)。</span><span class="sxs-lookup"><span data-stu-id="6c90a-110">To fail over a StorSimple physical device to a StorSimple Cloud Appliance, go to [Fail over to a StorSimple Cloud Appliance](storsimple-8000-device-failover-cloud-appliance.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="6c90a-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="6c90a-111">Prerequisites</span></span>

- <span data-ttu-id="6c90a-112">請確定您已檢閱裝置容錯移轉的注意事項。</span><span class="sxs-lookup"><span data-stu-id="6c90a-112">Ensure that you have reviewed the considerations for device failover.</span></span> <span data-ttu-id="6c90a-113">如需詳細資訊，請移至[裝置容錯移轉的一般注意事項](storsimple-8000-device-failover-disaster-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="6c90a-113">For more information, go to [Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md).</span></span>


## <a name="steps-to-fail-over-to-the-same-device"></a><span data-ttu-id="6c90a-114">容錯移轉至相同裝置的步驟</span><span class="sxs-lookup"><span data-stu-id="6c90a-114">Steps to fail over to the same device</span></span>

<span data-ttu-id="6c90a-115">如果您需要容錯移轉至相同的裝置，請執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="6c90a-115">Perform the following steps if you need to fail over to the same device.</span></span>

1. <span data-ttu-id="6c90a-116">建立裝置中所有磁碟區的雲端快照。</span><span class="sxs-lookup"><span data-stu-id="6c90a-116">Take cloud snapshots of all the volumes in your device.</span></span> <span data-ttu-id="6c90a-117">如需詳細資訊，請移至[使用 StorSimple 裝置管理員服務建立備份](storsimple-8000-manage-backup-policies-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="6c90a-117">For more information, go to [Use StorSimple Device Manager service to create backups](storsimple-8000-manage-backup-policies-u2.md).</span></span>
2. <span data-ttu-id="6c90a-118">將裝置重設為原廠預設值。</span><span class="sxs-lookup"><span data-stu-id="6c90a-118">Reset your device to factory defaults.</span></span> <span data-ttu-id="6c90a-119">請依照 [如何將 StorSimple 裝置重設為原廠預設值](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings)中的詳細指示執行。</span><span class="sxs-lookup"><span data-stu-id="6c90a-119">Follow the detailed instructions in [how to reset a StorSimple device to factory default settings](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>
3. <span data-ttu-id="6c90a-120">移至 StorSimple 裝置管理員服務，然後按一下 [裝置]。</span><span class="sxs-lookup"><span data-stu-id="6c90a-120">Go to the StorSimple Device Manager service and then select **Devices**.</span></span> <span data-ttu-id="6c90a-121">在 [裝置] 刀鋒視窗中，舊的裝置應會顯示成 [離線]。</span><span class="sxs-lookup"><span data-stu-id="6c90a-121">In the **Devices** blade, the old device should show as **Offline**.</span></span>

    ![來源裝置離線](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev2.png)

4. <span data-ttu-id="6c90a-123">設定裝置，並再次使用 StorSimple 裝置管理員服務重新註冊裝置。</span><span class="sxs-lookup"><span data-stu-id="6c90a-123">Configure your device and register it again with your StorSimple Device Manager service.</span></span> <span data-ttu-id="6c90a-124">新註冊的裝置應該會顯示成 [準備好進行設定]。</span><span class="sxs-lookup"><span data-stu-id="6c90a-124">The newly registered device should show as **Ready to set up**.</span></span> <span data-ttu-id="6c90a-125">新裝置的裝置名稱與舊裝置的相同，但會加上數字來表示裝置已重設為原廠預設值，並重新註冊。</span><span class="sxs-lookup"><span data-stu-id="6c90a-125">The device name for the new device is the same as the old device but appended with a numeral to indicate that the device was reset to factory default and registered again.</span></span>

    ![新註冊的裝置已準備好進行設定](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev3.png)
5. <span data-ttu-id="6c90a-127">請完成新裝置的裝置設定。</span><span class="sxs-lookup"><span data-stu-id="6c90a-127">For the new device, complete the device setup.</span></span> <span data-ttu-id="6c90a-128">如需詳細資訊，請移至[步驟 4：完成基本裝置設定](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup)。</span><span class="sxs-lookup"><span data-stu-id="6c90a-128">For more information, go to [Step 4: Complete minimum device setup](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup).</span></span> <span data-ttu-id="6c90a-129">在 [裝置] 刀鋒視窗中，裝置的狀態會變更為 [線上]。</span><span class="sxs-lookup"><span data-stu-id="6c90a-129">On the **Devices** blade, the status of the device changes to **Online**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="6c90a-130">**請先完成基本設定，否則您的 DR 可能會失敗。**</span><span class="sxs-lookup"><span data-stu-id="6c90a-130">**Complete the minimum configuration first, or your DR may fail.**</span></span>

    ![新註冊的裝置狀態為線上](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev7.png)

6. <span data-ttu-id="6c90a-132">選取舊裝置 (離線狀態)，然後從命令列按一下 [容錯移轉]。</span><span class="sxs-lookup"><span data-stu-id="6c90a-132">Select the old device (status offline) and from the command bar, click **Fail over**.</span></span> <span data-ttu-id="6c90a-133">在 [容錯移轉] 刀鋒視窗中，選取舊裝置做為來源，並將目標裝置指定為新註冊的裝置。</span><span class="sxs-lookup"><span data-stu-id="6c90a-133">In the **Fail over** blade, select old device as the source and specify the target device as the newly registered device.</span></span>

    ![容錯移轉摘要](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev11.png)

    <span data-ttu-id="6c90a-135">如需詳細指示，請參閱 [容錯移轉到另一個實體裝置](#fail-over-to-another-physical-device)。</span><span class="sxs-lookup"><span data-stu-id="6c90a-135">For detailed instructions, refer to [Fail over to another physical device](#fail-over-to-another-physical-device).</span></span>

7. <span data-ttu-id="6c90a-136">您可以從 [作業] 刀鋒視窗來監視建立的裝置還原作業。</span><span class="sxs-lookup"><span data-stu-id="6c90a-136">A device restore job is created that you can monitor from the **Jobs** blade.</span></span>

8. <span data-ttu-id="6c90a-137">順利完成作業後，請存取新裝置，並瀏覽到 [磁碟區容器] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="6c90a-137">After the job has successfully completed, access the new device and navigate to the **Volume containers** blade.</span></span> <span data-ttu-id="6c90a-138">確認舊裝置的所有磁碟區容器已移轉到新的裝置。</span><span class="sxs-lookup"><span data-stu-id="6c90a-138">Verify that all the volume containers from the old device have migrated to the new device.</span></span>

   ![移轉磁碟區容器](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev13.png)

9. <span data-ttu-id="6c90a-140">完成容錯移轉之後，您可以停用舊裝置，並將其從入口網站中刪除。</span><span class="sxs-lookup"><span data-stu-id="6c90a-140">After the failover is complete, you can deactivate and delete the old device from the portal.</span></span> <span data-ttu-id="6c90a-141">選取舊裝置 (離線)，按一下滑鼠右鍵，然後選取 [停用]。</span><span class="sxs-lookup"><span data-stu-id="6c90a-141">Select the old device (offline), right-click, and then select **Deactivate**.</span></span> <span data-ttu-id="6c90a-142">停用裝置之後，裝置的狀態也會一併更新。</span><span class="sxs-lookup"><span data-stu-id="6c90a-142">After the device is deactivated, the status of the device is updated.</span></span>

     ![停用來源裝置](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev14.png)

10. <span data-ttu-id="6c90a-144">選取停用的裝置，按一下滑鼠右鍵，然後選取 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="6c90a-144">Select the deactivated device, right-click, and then select **Delete**.</span></span> <span data-ttu-id="6c90a-145">如此會將裝置從裝置清單中刪除。</span><span class="sxs-lookup"><span data-stu-id="6c90a-145">This deletes the device from the list of devices.</span></span>

    ![刪除來源裝置](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev15.png)



## <a name="next-steps"></a><span data-ttu-id="6c90a-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6c90a-147">Next steps</span></span>

* <span data-ttu-id="6c90a-148">執行容錯移轉之後，您可能需要 [停用或刪除 StorSimple 裝置](storsimple-8000-deactivate-and-delete-device.md)。</span><span class="sxs-lookup"><span data-stu-id="6c90a-148">After you have performed a failover, you may need to [deactivate or delete your StorSimple device](storsimple-8000-deactivate-and-delete-device.md).</span></span>
* <span data-ttu-id="6c90a-149">如需如何使用 StorSimple 裝置管理員服務的相關資訊，請移至[使用 StorSimple 裝置管理員服務管理 StorSimple 裝置](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="6c90a-149">For information about how to use the StorSimple Device Manager service, go to [Use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

