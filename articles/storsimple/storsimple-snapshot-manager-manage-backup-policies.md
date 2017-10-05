---
title: "StorSimple Snapshot Manager 備份原則 | Microsoft Docs"
description: "描述如何使用 StorSimple Snapshot Manager MMC 嵌入式管理單元，來建立和管理控制已排定之備份的備份原則。"
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 04415d0b-42f0-4737-8afa-257fb2dbe5d0
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 218c89e403673c16c72da95aa2c1d685bbed5a86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-snapshot-manager-to-create-and-manage-backup-policies"></a><span data-ttu-id="39f3b-103">使用 StorSimple Snapshot Manager 來建立和管理備份原則</span><span class="sxs-lookup"><span data-stu-id="39f3b-103">Use StorSimple Snapshot Manager to create and manage backup policies</span></span>
## <a name="overview"></a><span data-ttu-id="39f3b-104">概觀</span><span class="sxs-lookup"><span data-stu-id="39f3b-104">Overview</span></span>
<span data-ttu-id="39f3b-105">備份原則會建立一個在本機或雲端中備份磁碟區資料的排程。</span><span class="sxs-lookup"><span data-stu-id="39f3b-105">A backup policy creates a schedule for backing up volume data locally or in the cloud.</span></span> <span data-ttu-id="39f3b-106">建立備份原則時，您也可以指定保留原則。</span><span class="sxs-lookup"><span data-stu-id="39f3b-106">When you create a backup policy, you can also specify a retention policy.</span></span> <span data-ttu-id="39f3b-107">(您最多可以保留 64 個快照)。如需備份原則的詳細資訊，請參閱 [StorSimple 8000 系列：混合式雲端解決方案](storsimple-overview.md)中的[備份類型](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies)。</span><span class="sxs-lookup"><span data-stu-id="39f3b-107">(You can retain a maximum of 64 snapshots.) For more information about backup policies, see [Backup types](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies) in [StorSimple 8000 series: a hybrid cloud solution](storsimple-overview.md).</span></span>

<span data-ttu-id="39f3b-108">本教學課程說明如何：</span><span class="sxs-lookup"><span data-stu-id="39f3b-108">This tutorial explains how to:</span></span>

* <span data-ttu-id="39f3b-109">建立備份原則</span><span class="sxs-lookup"><span data-stu-id="39f3b-109">Create a backup policy</span></span>
* <span data-ttu-id="39f3b-110">編輯備份原則</span><span class="sxs-lookup"><span data-stu-id="39f3b-110">Edit a backup policy</span></span>
* <span data-ttu-id="39f3b-111">刪除備份原則</span><span class="sxs-lookup"><span data-stu-id="39f3b-111">Delete a backup policy</span></span>

## <a name="create-a-backup-policy"></a><span data-ttu-id="39f3b-112">建立備份原則</span><span class="sxs-lookup"><span data-stu-id="39f3b-112">Create a backup policy</span></span>
<span data-ttu-id="39f3b-113">請使用下列程序來建立新的備份原則。</span><span class="sxs-lookup"><span data-stu-id="39f3b-113">Use the following procedure to create a new backup policy.</span></span>

#### <a name="to-create-a-backup-policy"></a><span data-ttu-id="39f3b-114">若要建立備份原則</span><span class="sxs-lookup"><span data-stu-id="39f3b-114">To create a backup policy</span></span>
1. <span data-ttu-id="39f3b-115">按一下桌面圖示，以啟動 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="39f3b-115">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="39f3b-116">在 [範圍] 窗格中，以滑鼠右鍵按一下 [備份原則]，然後按一下 [建立備份原則]。</span><span class="sxs-lookup"><span data-stu-id="39f3b-116">In the **Scope** pane, right-click **Backup Policies**, and click **Create Backup Policy**.</span></span>

    ![建立備份原則](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_BU_policy.png)

    <span data-ttu-id="39f3b-118">[ **建立原則** ] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="39f3b-118">The **Create a Policy** dialog box appears.</span></span>

    ![建立原則 - 一般索引標籤](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_general.png)
3. <span data-ttu-id="39f3b-120">在 [ **一般** ] 索引標籤上，完成下列資訊：</span><span class="sxs-lookup"><span data-stu-id="39f3b-120">On the **General** tab, complete the following information:</span></span>

   1. <span data-ttu-id="39f3b-121">在 [ **名稱** ] 文字方塊中，輸入原則的名稱。</span><span class="sxs-lookup"><span data-stu-id="39f3b-121">In the **Name** text box, type a name for the policy.</span></span>
   2. <span data-ttu-id="39f3b-122">在 [磁碟機群組]  文字方塊中，輸入與原則相關聯之磁碟區群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="39f3b-122">In the **Volume group** text box, type the name of the volume group associated with the policy.</span></span>
   3. <span data-ttu-id="39f3b-123">選取 [本機快照] 或 [雲端快照]。</span><span class="sxs-lookup"><span data-stu-id="39f3b-123">Select either **Local Snapshot** or **Cloud Snapshot**.</span></span>
   4. <span data-ttu-id="39f3b-124">選取要保留的快照數目。</span><span class="sxs-lookup"><span data-stu-id="39f3b-124">Select the number of snapshots to retain.</span></span> <span data-ttu-id="39f3b-125">如果選取 [ **全部**]，將保留 64 個快照 (上限)。</span><span class="sxs-lookup"><span data-stu-id="39f3b-125">If you select **All**, 64 snapshots will be retained (the maximum).</span></span>
4. <span data-ttu-id="39f3b-126">按一下 [ **排程** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="39f3b-126">Click the **Schedule** tab.</span></span>

    ![建立原則 - 排程索引標籤](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_schedule.png)
5. <span data-ttu-id="39f3b-128">在 [ **排程** ] 索引標籤上，完成下列資訊：</span><span class="sxs-lookup"><span data-stu-id="39f3b-128">On the **Schedule** tab, complete the following information:</span></span>

   1. <span data-ttu-id="39f3b-129">按一下 [ **啟用** ] 核取方塊，以排程下次備份。</span><span class="sxs-lookup"><span data-stu-id="39f3b-129">Click the **Enable** check box to schedule the next backup.</span></span>
   2. <span data-ttu-id="39f3b-130">在 [設定] 之下，選取 [一次]、[每日]、[每週] 或 [每月]。</span><span class="sxs-lookup"><span data-stu-id="39f3b-130">Under **Settings**, select **One time**, **Daily**, **Weekly**, or **Monthly**.</span></span>
   3. <span data-ttu-id="39f3b-131">在 [ **開始** ] 文字方塊中，按一下日曆圖示，然後選取開始日期。</span><span class="sxs-lookup"><span data-stu-id="39f3b-131">In the **Start** text box, click the calendar icon and select a start date.</span></span>
   4. <span data-ttu-id="39f3b-132">在 [ **進階設定**] 之下，您可以設定選用的重複排程和結束日期。</span><span class="sxs-lookup"><span data-stu-id="39f3b-132">Under **Advanced Settings**, you can set optional repeat schedules and an end date.</span></span>
   5. <span data-ttu-id="39f3b-133">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="39f3b-133">Click **OK**.</span></span>

<span data-ttu-id="39f3b-134">建立備份原則之後，下列資訊會出現在 [ **結果** ] 窗格中：</span><span class="sxs-lookup"><span data-stu-id="39f3b-134">After you create a backup policy, the following information appears in the **Results** pane:</span></span>

* <span data-ttu-id="39f3b-135">**名稱**  – 備份原則的名稱。</span><span class="sxs-lookup"><span data-stu-id="39f3b-135">**Name** – the name of backup policy.</span></span>
* <span data-ttu-id="39f3b-136">**類型**  – 本機快照或雲端快照。</span><span class="sxs-lookup"><span data-stu-id="39f3b-136">**Type** – local snapshot or cloud snapshot.</span></span>
* <span data-ttu-id="39f3b-137">**Volume Group**  – 與原則相關聯的磁碟區群組。</span><span class="sxs-lookup"><span data-stu-id="39f3b-137">**Volume Group** – the volume group associated with the policy.</span></span>
* <span data-ttu-id="39f3b-138">**保留**  – 保留的快照數目；上限為 64。</span><span class="sxs-lookup"><span data-stu-id="39f3b-138">**Retention** – the number of snapshots retained; the maximum is 64.</span></span>
* <span data-ttu-id="39f3b-139">**建立時間**  – 此原則的建立日期。</span><span class="sxs-lookup"><span data-stu-id="39f3b-139">**Created** – the date that this policy was created.</span></span>
* <span data-ttu-id="39f3b-140">[已啟用] – 原則目前是否生效：**True** 表示生效；**False** 表示未生效。</span><span class="sxs-lookup"><span data-stu-id="39f3b-140">**Enabled** – whether the policy is currently in effect: **True** indicates that it is in effect; **False** indicates that it is not in effect.</span></span>

## <a name="edit-a-backup-policy"></a><span data-ttu-id="39f3b-141">編輯備份原則</span><span class="sxs-lookup"><span data-stu-id="39f3b-141">Edit a backup policy</span></span>
<span data-ttu-id="39f3b-142">請使用下列程序來編輯現有的備份原則。</span><span class="sxs-lookup"><span data-stu-id="39f3b-142">Use the following procedure to edit an existing backup policy.</span></span>

#### <a name="to-edit-a-backup-policy"></a><span data-ttu-id="39f3b-143">若要編輯備份原則</span><span class="sxs-lookup"><span data-stu-id="39f3b-143">To edit a backup policy</span></span>
1. <span data-ttu-id="39f3b-144">按一下桌面圖示，以啟動 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="39f3b-144">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="39f3b-145">在 [範圍] 窗格中，按一下 [備份原則] 節點。</span><span class="sxs-lookup"><span data-stu-id="39f3b-145">In the **Scope** pane, click the **Backup Policies** node.</span></span> <span data-ttu-id="39f3b-146">所有備份原則都會出現在 [ **結果** ] 窗格中。</span><span class="sxs-lookup"><span data-stu-id="39f3b-146">All the backup policies appear in the **Results** pane.</span></span>
3. <span data-ttu-id="39f3b-147">以滑鼠右鍵按一下您要編輯的原則，然後按一下 [ **編輯**]。</span><span class="sxs-lookup"><span data-stu-id="39f3b-147">Right-click the policy that you want to edit, and then click **Edit**.</span></span>

    ![編輯備份原則](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Edit_BU_policy.png)
4. <span data-ttu-id="39f3b-149">當 [建立原則] 視窗出現時，輸入您的變更，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="39f3b-149">When the **Create a Policy** window appears, enter your changes, and then click **OK**.</span></span>

## <a name="delete-a-backup-policy"></a><span data-ttu-id="39f3b-150">刪除備份原則</span><span class="sxs-lookup"><span data-stu-id="39f3b-150">Delete a backup policy</span></span>
<span data-ttu-id="39f3b-151">請使用下列程序來刪除備份原則。</span><span class="sxs-lookup"><span data-stu-id="39f3b-151">Use the following procedure to delete a backup policy.</span></span>

#### <a name="to-delete-a-backup-policy"></a><span data-ttu-id="39f3b-152">若要刪除備份原則</span><span class="sxs-lookup"><span data-stu-id="39f3b-152">To delete a backup policy</span></span>
1. <span data-ttu-id="39f3b-153">按一下桌面圖示，以啟動 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="39f3b-153">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="39f3b-154">在 [範圍] 窗格中，按一下 [備份原則] 節點。</span><span class="sxs-lookup"><span data-stu-id="39f3b-154">In the **Scope** pane, click the **Backup Policies** node.</span></span> <span data-ttu-id="39f3b-155">所有備份原則都會出現在 [ **結果** ] 窗格中。</span><span class="sxs-lookup"><span data-stu-id="39f3b-155">All the backup policies appear in the **Results** pane.</span></span>
3. <span data-ttu-id="39f3b-156">以滑鼠右鍵按一下您要刪除的備份原則，然後按一下 [刪除] 。</span><span class="sxs-lookup"><span data-stu-id="39f3b-156">Right-click the backup policy that you want to delete, and then click **Delete**.</span></span>
4. <span data-ttu-id="39f3b-157">確認訊息出現時，按一下 [ **是**]。</span><span class="sxs-lookup"><span data-stu-id="39f3b-157">When the confirmation message appears, click **Yes**.</span></span>

    ![確認刪除備份原則](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Delete_BU_policy.png)

## <a name="next-steps"></a><span data-ttu-id="39f3b-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="39f3b-159">Next steps</span></span>
* <span data-ttu-id="39f3b-160">了解如何 [使用 StorSimple Snapshot Manager 來管理您的 StorSimple 解決方案](storsimple-snapshot-manager-admin.md)。</span><span class="sxs-lookup"><span data-stu-id="39f3b-160">Learn how to [use StorSimple Snapshot Manager to administer your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="39f3b-161">了解如何 [使用 StorSimple Snapshot Manager 來檢視和管理備份工作](storsimple-snapshot-manager-manage-backup-jobs.md)。</span><span class="sxs-lookup"><span data-stu-id="39f3b-161">Learn how to [use StorSimple Snapshot Manager to view and manage backup jobs](storsimple-snapshot-manager-manage-backup-jobs.md).</span></span>
