---
title: "aaaStorSimple Snapshot Manager 備份原則 |Microsoft 文件"
description: "描述如何 toouse hello StorSimple Snapshot Manager MMC 嵌入式管理單元 toocreate 和管理 hello 控制排定的備份的備份原則。"
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
ms.openlocfilehash: c2ae75a8d0568090add6018da18de73eb56e6590
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toocreate-and-manage-backup-policies"></a><span data-ttu-id="440a2-103">使用 StorSimple Snapshot Manager toocreate 及管理備份原則</span><span class="sxs-lookup"><span data-stu-id="440a2-103">Use StorSimple Snapshot Manager toocreate and manage backup policies</span></span>
## <a name="overview"></a><span data-ttu-id="440a2-104">概觀</span><span class="sxs-lookup"><span data-stu-id="440a2-104">Overview</span></span>
<span data-ttu-id="440a2-105">備份原則會建立在本機或 hello 雲端備份磁碟區資料的排程。</span><span class="sxs-lookup"><span data-stu-id="440a2-105">A backup policy creates a schedule for backing up volume data locally or in hello cloud.</span></span> <span data-ttu-id="440a2-106">建立備份原則時，您也可以指定保留原則。</span><span class="sxs-lookup"><span data-stu-id="440a2-106">When you create a backup policy, you can also specify a retention policy.</span></span> <span data-ttu-id="440a2-107">(您最多可以保留 64 個快照)。如需備份原則的詳細資訊，請參閱 [StorSimple 8000 系列：混合式雲端解決方案](storsimple-overview.md)中的[備份類型](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies)。</span><span class="sxs-lookup"><span data-stu-id="440a2-107">(You can retain a maximum of 64 snapshots.) For more information about backup policies, see [Backup types](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies) in [StorSimple 8000 series: a hybrid cloud solution](storsimple-overview.md).</span></span>

<span data-ttu-id="440a2-108">本教學課程說明如何：</span><span class="sxs-lookup"><span data-stu-id="440a2-108">This tutorial explains how to:</span></span>

* <span data-ttu-id="440a2-109">建立備份原則</span><span class="sxs-lookup"><span data-stu-id="440a2-109">Create a backup policy</span></span>
* <span data-ttu-id="440a2-110">編輯備份原則</span><span class="sxs-lookup"><span data-stu-id="440a2-110">Edit a backup policy</span></span>
* <span data-ttu-id="440a2-111">刪除備份原則</span><span class="sxs-lookup"><span data-stu-id="440a2-111">Delete a backup policy</span></span>

## <a name="create-a-backup-policy"></a><span data-ttu-id="440a2-112">建立備份原則</span><span class="sxs-lookup"><span data-stu-id="440a2-112">Create a backup policy</span></span>
<span data-ttu-id="440a2-113">使用下列程序 toocreate 新的備份原則的 hello。</span><span class="sxs-lookup"><span data-stu-id="440a2-113">Use hello following procedure toocreate a new backup policy.</span></span>

#### <a name="toocreate-a-backup-policy"></a><span data-ttu-id="440a2-114">toocreate 備份原則</span><span class="sxs-lookup"><span data-stu-id="440a2-114">toocreate a backup policy</span></span>
1. <span data-ttu-id="440a2-115">按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="440a2-115">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="440a2-116">在 [hello**範圍**] 窗格中，以滑鼠右鍵按一下**備份原則**，按一下**建立備份原則**。</span><span class="sxs-lookup"><span data-stu-id="440a2-116">In hello **Scope** pane, right-click **Backup Policies**, and click **Create Backup Policy**.</span></span>

    ![建立備份原則](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_BU_policy.png)

    <span data-ttu-id="440a2-118">hello**建立原則** 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="440a2-118">hello **Create a Policy** dialog box appears.</span></span>

    ![建立原則 - 一般索引標籤](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_general.png)
3. <span data-ttu-id="440a2-120">在 hello**一般**索引標籤，完成 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="440a2-120">On hello **General** tab, complete hello following information:</span></span>

   1. <span data-ttu-id="440a2-121">在 [hello**名稱**] 文字方塊中，輸入 hello 原則的名稱。</span><span class="sxs-lookup"><span data-stu-id="440a2-121">In hello **Name** text box, type a name for hello policy.</span></span>
   2. <span data-ttu-id="440a2-122">在 hello**磁碟區群組**文字方塊中，型別 hello hello 與 hello 原則相關聯的磁碟區群組名稱。</span><span class="sxs-lookup"><span data-stu-id="440a2-122">In hello **Volume group** text box, type hello name of hello volume group associated with hello policy.</span></span>
   3. <span data-ttu-id="440a2-123">選取 [本機快照] 或 [雲端快照]。</span><span class="sxs-lookup"><span data-stu-id="440a2-123">Select either **Local Snapshot** or **Cloud Snapshot**.</span></span>
   4. <span data-ttu-id="440a2-124">選取快照集 tooretain hello 的數目。</span><span class="sxs-lookup"><span data-stu-id="440a2-124">Select hello number of snapshots tooretain.</span></span> <span data-ttu-id="440a2-125">如果您選取**所有**，將會保留 64 個快照 (上限 hello)。</span><span class="sxs-lookup"><span data-stu-id="440a2-125">If you select **All**, 64 snapshots will be retained (hello maximum).</span></span>
4. <span data-ttu-id="440a2-126">按一下 hello**排程** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="440a2-126">Click hello **Schedule** tab.</span></span>

    ![建立原則 - 排程索引標籤](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_schedule.png)
5. <span data-ttu-id="440a2-128">在 hello**排程**索引標籤，完成 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="440a2-128">On hello **Schedule** tab, complete hello following information:</span></span>

   1. <span data-ttu-id="440a2-129">按一下 hello**啟用**核取方塊 tooschedule hello 下一次備份。</span><span class="sxs-lookup"><span data-stu-id="440a2-129">Click hello **Enable** check box tooschedule hello next backup.</span></span>
   2. <span data-ttu-id="440a2-130">在 [設定] 之下，選取 [一次]、[每日]、[每週] 或 [每月]。</span><span class="sxs-lookup"><span data-stu-id="440a2-130">Under **Settings**, select **One time**, **Daily**, **Weekly**, or **Monthly**.</span></span>
   3. <span data-ttu-id="440a2-131">在 [hello**啟動**] 文字方塊中，按一下 hello 行事曆圖示，然後選取開始日期。</span><span class="sxs-lookup"><span data-stu-id="440a2-131">In hello **Start** text box, click hello calendar icon and select a start date.</span></span>
   4. <span data-ttu-id="440a2-132">在 [ **進階設定**] 之下，您可以設定選用的重複排程和結束日期。</span><span class="sxs-lookup"><span data-stu-id="440a2-132">Under **Advanced Settings**, you can set optional repeat schedules and an end date.</span></span>
   5. <span data-ttu-id="440a2-133">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="440a2-133">Click **OK**.</span></span>

<span data-ttu-id="440a2-134">下列資訊的 hello 建立備份原則之後，會出現在 hello**結果**窗格：</span><span class="sxs-lookup"><span data-stu-id="440a2-134">After you create a backup policy, hello following information appears in hello **Results** pane:</span></span>

* <span data-ttu-id="440a2-135">**名稱**– hello 備份原則的名稱。</span><span class="sxs-lookup"><span data-stu-id="440a2-135">**Name** – hello name of backup policy.</span></span>
* <span data-ttu-id="440a2-136">**類型**  – 本機快照或雲端快照。</span><span class="sxs-lookup"><span data-stu-id="440a2-136">**Type** – local snapshot or cloud snapshot.</span></span>
* <span data-ttu-id="440a2-137">**磁碟區群組**– hello 與 hello 原則相關聯的磁碟區群組。</span><span class="sxs-lookup"><span data-stu-id="440a2-137">**Volume Group** – hello volume group associated with hello policy.</span></span>
* <span data-ttu-id="440a2-138">**保留**– hello 保留的快照數目; hello 上限為 64。</span><span class="sxs-lookup"><span data-stu-id="440a2-138">**Retention** – hello number of snapshots retained; hello maximum is 64.</span></span>
* <span data-ttu-id="440a2-139">**建立**– 建立此原則的 hello 日期。</span><span class="sxs-lookup"><span data-stu-id="440a2-139">**Created** – hello date that this policy was created.</span></span>
* <span data-ttu-id="440a2-140">**啟用**– hello 原則目前是否生效： **True**表示它是作用中。**False**表示它不是作用中。</span><span class="sxs-lookup"><span data-stu-id="440a2-140">**Enabled** – whether hello policy is currently in effect: **True** indicates that it is in effect; **False** indicates that it is not in effect.</span></span>

## <a name="edit-a-backup-policy"></a><span data-ttu-id="440a2-141">編輯備份原則</span><span class="sxs-lookup"><span data-stu-id="440a2-141">Edit a backup policy</span></span>
<span data-ttu-id="440a2-142">使用下列程序 tooedit 現有的備份原則的 hello。</span><span class="sxs-lookup"><span data-stu-id="440a2-142">Use hello following procedure tooedit an existing backup policy.</span></span>

#### <a name="tooedit-a-backup-policy"></a><span data-ttu-id="440a2-143">tooedit 備份原則</span><span class="sxs-lookup"><span data-stu-id="440a2-143">tooedit a backup policy</span></span>
1. <span data-ttu-id="440a2-144">按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="440a2-144">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="440a2-145">在 [hello**範圍**] 窗格中，按一下 hello**備份原則**節點。</span><span class="sxs-lookup"><span data-stu-id="440a2-145">In hello **Scope** pane, click hello **Backup Policies** node.</span></span> <span data-ttu-id="440a2-146">所有的 hello 備份原則會出現在 hello**結果**窗格。</span><span class="sxs-lookup"><span data-stu-id="440a2-146">All hello backup policies appear in hello **Results** pane.</span></span>
3. <span data-ttu-id="440a2-147">以滑鼠右鍵按一下您想 tooedit，然後再按一下 hello 原則**編輯**。</span><span class="sxs-lookup"><span data-stu-id="440a2-147">Right-click hello policy that you want tooedit, and then click **Edit**.</span></span>

    ![編輯備份原則](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Edit_BU_policy.png)
4. <span data-ttu-id="440a2-149">當 hello**建立原則**視窗出現時，請輸入您的變更，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="440a2-149">When hello **Create a Policy** window appears, enter your changes, and then click **OK**.</span></span>

## <a name="delete-a-backup-policy"></a><span data-ttu-id="440a2-150">刪除備份原則</span><span class="sxs-lookup"><span data-stu-id="440a2-150">Delete a backup policy</span></span>
<span data-ttu-id="440a2-151">使用下列程序 toodelete 備份原則的 hello。</span><span class="sxs-lookup"><span data-stu-id="440a2-151">Use hello following procedure toodelete a backup policy.</span></span>

#### <a name="toodelete-a-backup-policy"></a><span data-ttu-id="440a2-152">toodelete 備份原則</span><span class="sxs-lookup"><span data-stu-id="440a2-152">toodelete a backup policy</span></span>
1. <span data-ttu-id="440a2-153">按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="440a2-153">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="440a2-154">在 [hello**範圍**] 窗格中，按一下 hello**備份原則**節點。</span><span class="sxs-lookup"><span data-stu-id="440a2-154">In hello **Scope** pane, click hello **Backup Policies** node.</span></span> <span data-ttu-id="440a2-155">所有的 hello 備份原則會出現在 hello**結果**窗格。</span><span class="sxs-lookup"><span data-stu-id="440a2-155">All hello backup policies appear in hello **Results** pane.</span></span>
3. <span data-ttu-id="440a2-156">以滑鼠右鍵按一下您想 toodelete，然後再按一下 hello 備份原則**刪除**。</span><span class="sxs-lookup"><span data-stu-id="440a2-156">Right-click hello backup policy that you want toodelete, and then click **Delete**.</span></span>
4. <span data-ttu-id="440a2-157">Hello 確認訊息出現時，按一下**是**。</span><span class="sxs-lookup"><span data-stu-id="440a2-157">When hello confirmation message appears, click **Yes**.</span></span>

    ![確認刪除備份原則](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Delete_BU_policy.png)

## <a name="next-steps"></a><span data-ttu-id="440a2-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="440a2-159">Next steps</span></span>
* <span data-ttu-id="440a2-160">了解如何太[使用您的 StorSimple 解決方案的 StorSimple Snapshot Manager tooadminister](storsimple-snapshot-manager-admin.md)。</span><span class="sxs-lookup"><span data-stu-id="440a2-160">Learn how too[use StorSimple Snapshot Manager tooadminister your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="440a2-161">了解如何太[使用 StorSimple Snapshot Manager tooview 及管理備份工作](storsimple-snapshot-manager-manage-backup-jobs.md)。</span><span class="sxs-lookup"><span data-stu-id="440a2-161">Learn how too[use StorSimple Snapshot Manager tooview and manage backup jobs](storsimple-snapshot-manager-manage-backup-jobs.md).</span></span>
