---
title: "StorSimple 容錯移轉、災害復原至 StorSimple 雲端設備| Microsoft Docs"
description: "了解如何將您的 StorSimple 8000 系列實體裝置容錯移轉至雲端設備。"
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
ms.openlocfilehash: ec8bebf2854e84a37e84b45564e80fc20b63d8d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="fail-over-to-your-storsimple-cloud-appliance"></a><span data-ttu-id="b111a-103">容錯移轉至您的 StorSimple 雲端設備</span><span class="sxs-lookup"><span data-stu-id="b111a-103">Fail over to your StorSimple Cloud Appliance</span></span>

## <a name="overview"></a><span data-ttu-id="b111a-104">概觀</span><span class="sxs-lookup"><span data-stu-id="b111a-104">Overview</span></span>

<span data-ttu-id="b111a-105">本教學課程說明當發生災害時，將 StorSimple 8000 系列實體裝置容錯移轉至 StorSimple 雲端設備所需要的步驟。</span><span class="sxs-lookup"><span data-stu-id="b111a-105">This tutorial describes the steps required to fail over a StorSimple 8000 series physical device to a StorSimple Cloud Appliance if there is a disaster.</span></span> <span data-ttu-id="b111a-106">StorSimple 會使用裝置容錯移轉功能，將資料從資料中心的實體裝置來源移轉至 Azure 中執行的雲端設備。</span><span class="sxs-lookup"><span data-stu-id="b111a-106">StorSimple uses the device failover feature to migrate data from a source physical device in the datacenter to a cloud appliance running in Azure.</span></span> <span data-ttu-id="b111a-107">本教學課程中的指導方針適用於 StorSimple 8000 系列實體裝置和執行軟體版本為 Update 3 和更新版本的雲端設備。</span><span class="sxs-lookup"><span data-stu-id="b111a-107">The guidance in this tutorial applies to StorSimple 8000 series physical devices and cloud appliances running software versions Update 3 and later.</span></span>

<span data-ttu-id="b111a-108">若要深入了解裝置容錯移轉，以及如何用於從災害中復原，請移至 [ StorSimple 8000 系列裝置的容錯移轉與災害復原](storsimple-8000-device-failover-disaster-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="b111a-108">To learn more about device failover and how it is used to recover from a disaster, go to [Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

<span data-ttu-id="b111a-109">若要將 StorSimple 實體裝置容錯移轉至另一個實體裝置，請移至[容錯移轉至 StorSimple 實體裝置](storsimple-8000-device-failover-physical-device.md)。</span><span class="sxs-lookup"><span data-stu-id="b111a-109">To fail over a StorSimple physical device to another physical device, go to [Fail over to a StorSimple physical device](storsimple-8000-device-failover-physical-device.md).</span></span> <span data-ttu-id="b111a-110">若要將裝置容錯移轉至本身的裝置，請移至[容錯移轉至相同的 StorSimple 實體裝置](storsimple-8000-device-failover-same-device.md)。</span><span class="sxs-lookup"><span data-stu-id="b111a-110">To fail over a device to itself, go to [Fail over to the same StorSimple physical device](storsimple-8000-device-failover-same-device.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b111a-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="b111a-111">Prerequisites</span></span>

- <span data-ttu-id="b111a-112">請確定您已檢閱裝置容錯移轉的注意事項。</span><span class="sxs-lookup"><span data-stu-id="b111a-112">Ensure that you have reviewed the considerations for device failover.</span></span> <span data-ttu-id="b111a-113">如需詳細資訊，請移至[裝置容錯移轉的一般注意事項](storsimple-8000-device-failover-disaster-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="b111a-113">For more information, go to [Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

- <span data-ttu-id="b111a-114">執行此程序之前，您必須已建立並設定 StorSimple 雲端設備。</span><span class="sxs-lookup"><span data-stu-id="b111a-114">You must have a StorSimple Cloud Appliance created and configured before running this procedure.</span></span> <span data-ttu-id="b111a-115">如果執行的是 Update 3 的軟體版本或更新版本，請考慮針對 DR 使用 8020 雲端設備。</span><span class="sxs-lookup"><span data-stu-id="b111a-115">If running   Update 3 software version or later, consider using an 8020 cloud appliance for the DR.</span></span> <span data-ttu-id="b111a-116">8020 型號具有 64 TB 容量，且使用的是進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="b111a-116">The 8020 model has 64 TB and uses Premium Storage.</span></span> <span data-ttu-id="b111a-117">如需詳細資訊，請移至[部署和管理 StorSimple 雲端設備](storsimple-8000-cloud-appliance-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="b111a-117">For more information, go to [Deploy and manage a StorSimple Cloud Appliance](storsimple-8000-cloud-appliance-u2.md).</span></span>

## <a name="steps-to-fail-over-to-a-cloud-appliance"></a><span data-ttu-id="b111a-118">容錯移轉至雲端設備的步驟</span><span class="sxs-lookup"><span data-stu-id="b111a-118">Steps to fail over to a cloud appliance</span></span>

<span data-ttu-id="b111a-119">請執行下列步驟以將裝置還原至目標 StorSimple 雲端設備。</span><span class="sxs-lookup"><span data-stu-id="b111a-119">Perform the following steps to restore the device to a target StorSimple Cloud Appliance.</span></span>

1.  <span data-ttu-id="b111a-120">確認您要容錯移轉的磁碟區容器是否具有相關聯的雲端快照。</span><span class="sxs-lookup"><span data-stu-id="b111a-120">Verify that the volume container you want to fail over has associated cloud snapshots.</span></span> <span data-ttu-id="b111a-121">如需詳細資訊，請移至[使用 StorSimple 裝置管理員服務建立備份](storsimple-8000-manage-backup-policies-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="b111a-121">For more information, go to [Use StorSimple Device Manager service to create backups](storsimple-8000-manage-backup-policies-u2.md).</span></span>
2. <span data-ttu-id="b111a-122">移至 StorSimple 裝置管理員服務，然後按一下 [裝置]。</span><span class="sxs-lookup"><span data-stu-id="b111a-122">Go to your StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="b111a-123">在 [裝置] 刀鋒視窗中，移至與您的服務連接的裝置清單。</span><span class="sxs-lookup"><span data-stu-id="b111a-123">In the **Devices** blade, go to the list of devices connected with your service.</span></span>
    <span data-ttu-id="b111a-124">![選取裝置](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)</span><span class="sxs-lookup"><span data-stu-id="b111a-124">![Select device](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)</span></span>
3. <span data-ttu-id="b111a-125">選取並按一下您的來源裝置。</span><span class="sxs-lookup"><span data-stu-id="b111a-125">Select and click your source device.</span></span> <span data-ttu-id="b111a-126">來源裝置具有您想要容錯移轉的磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="b111a-126">The source device has the volume containers that you want to fail over.</span></span> <span data-ttu-id="b111a-127">移至 [設定] > [磁碟區容器]。</span><span class="sxs-lookup"><span data-stu-id="b111a-127">Go to **Settings > Volume Containers**.</span></span>

    ![選取裝置](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev2.png)
    
4. <span data-ttu-id="b111a-129">選取您要容錯移轉至另一個裝置的磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="b111a-129">Select a volume container that you would like to fail over to another device.</span></span> <span data-ttu-id="b111a-130">按一下磁碟區容器，以顯示此容器內的磁碟區清單。</span><span class="sxs-lookup"><span data-stu-id="b111a-130">Click the volume container to display the list of volumes within this container.</span></span> <span data-ttu-id="b111a-131">選取磁碟區，按一下滑鼠右鍵，然後按一下 [離線]，讓磁碟區離線。</span><span class="sxs-lookup"><span data-stu-id="b111a-131">Select a volume, right-click, and click **Take Offline** to take the volume offline.</span></span>

    ![選取裝置](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev5.png)

5. <span data-ttu-id="b111a-133">針對磁碟區容器中的所有磁碟區，重複執行這個程序。</span><span class="sxs-lookup"><span data-stu-id="b111a-133">Repeat this process for all the volumes in the volume container.</span></span>

     ![選取裝置](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev7.png)

6. <span data-ttu-id="b111a-135">針對您要容錯移轉至另一個裝置的所有磁碟區容器，重複執行前一個步驟。</span><span class="sxs-lookup"><span data-stu-id="b111a-135">Repeat the previous step for all the volume containers you would like to fail over to another device.</span></span>

7. <span data-ttu-id="b111a-136">返回 [裝置] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b111a-136">Go back to the **Devices** blade.</span></span> <span data-ttu-id="b111a-137">從命令列中，按一下 [容錯移轉]。</span><span class="sxs-lookup"><span data-stu-id="b111a-137">From the command bar, click **Fail over**.</span></span>

    ![按一下 [容錯移轉]](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev8.png)
8. <span data-ttu-id="b111a-139">在 [容錯移轉] 刀鋒視窗中，執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="b111a-139">In the **Fail over** blade, perform the following steps:</span></span>
   
    1. <span data-ttu-id="b111a-140">按一下 [來源]。</span><span class="sxs-lookup"><span data-stu-id="b111a-140">Click **Source**.</span></span> <span data-ttu-id="b111a-141">選取要容錯移轉的磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="b111a-141">Select the volume containers to fail over.</span></span> <span data-ttu-id="b111a-142">**只會顯示與雲端快照集和離線磁碟區相關聯的磁碟區容器。**</span><span class="sxs-lookup"><span data-stu-id="b111a-142">**Only the volume containers with associated cloud snapshots and offline volumes are displayed.**</span></span>
        <span data-ttu-id="b111a-143">![選取來源](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png)</span><span class="sxs-lookup"><span data-stu-id="b111a-143">![Select source](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png)</span></span>
    2. <span data-ttu-id="b111a-144">按一下 [目標]。</span><span class="sxs-lookup"><span data-stu-id="b111a-144">Click **Target**.</span></span> <span data-ttu-id="b111a-145">從可用裝置的下拉式清單中，選取目標雲端設備。</span><span class="sxs-lookup"><span data-stu-id="b111a-145">Select a target cloud appliance from the dropdown list of available devices.</span></span> <span data-ttu-id="b111a-146">**清單中只會顯示擁有足夠容量容納來源磁碟區容器的裝置。**</span><span class="sxs-lookup"><span data-stu-id="b111a-146">**Only the devices that have sufficient capacity to accommodate source volume containers are displayed in the list.**</span></span>

        ![選取目標](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev12.png)

    3. <span data-ttu-id="b111a-148">檢閱 [摘要] 的容錯移轉設定，並選取核取方塊，代表選取的磁碟區容器內的磁碟區已離線。</span><span class="sxs-lookup"><span data-stu-id="b111a-148">Review the failover settings under **Summary** and select the checkbox indicating that the volumes in selected volume containers are offline.</span></span> 

        ![檢閱容錯移轉設定](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev13.png)

9. <span data-ttu-id="b111a-150">已建立容錯移轉作業。</span><span class="sxs-lookup"><span data-stu-id="b111a-150">A failover job is created.</span></span> <span data-ttu-id="b111a-151">若要監視容錯移轉作業，請按一下 [作業通知]。</span><span class="sxs-lookup"><span data-stu-id="b111a-151">To monitor the failover job, click the job notification.</span></span>

    ![監視容錯移轉作業](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

10. <span data-ttu-id="b111a-153">完成容錯移轉後，返回 [裝置] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b111a-153">After the failover is completed, go back to the **Devices** blade.</span></span>

    1. <span data-ttu-id="b111a-154">為容錯移轉選取要用來做為目標的裝置。</span><span class="sxs-lookup"><span data-stu-id="b111a-154">Select the device that was used as the target for the failover.</span></span>

       ![選取裝置](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

    2. <span data-ttu-id="b111a-156">按一下 [磁碟區容器]。</span><span class="sxs-lookup"><span data-stu-id="b111a-156">Click **Volume Containers**.</span></span> <span data-ttu-id="b111a-157">此時應會列出所有磁碟區容器以及舊裝置中的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b111a-157">All the volume containers, along with the volumes from the old device, should be listed.</span></span>

       <span data-ttu-id="b111a-158">如果您容錯移轉的磁碟區容器含有固定在本機的磁碟區，這些磁碟區會容錯移轉成為分層磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b111a-158">If the volume container that you failed over has locally pinned volumes, those volumes are failed over as tiered volumes.</span></span> <span data-ttu-id="b111a-159">StorSimple 雲端設備不支援已固定在本機的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b111a-159">Locally pinned volumes are not supported on a StorSimple Cloud Appliance.</span></span>

       ![檢視目標磁碟區容器](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev17.png)


## <a name="next-steps"></a><span data-ttu-id="b111a-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b111a-161">Next steps</span></span>

* <span data-ttu-id="b111a-162">執行容錯移轉之後，您可能需要 [停用或刪除 StorSimple 裝置](storsimple-8000-deactivate-and-delete-device.md)。</span><span class="sxs-lookup"><span data-stu-id="b111a-162">After you have performed a failover, you may need to [deactivate or delete your StorSimple device](storsimple-8000-deactivate-and-delete-device.md).</span></span>

* <span data-ttu-id="b111a-163">如需如何使用 StorSimple 裝置管理員服務的相關資訊，請移至[使用 StorSimple 裝置管理員服務管理 StorSimple 裝置](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="b111a-163">For information about how to use the StorSimple Device Manager service, go to [Use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

