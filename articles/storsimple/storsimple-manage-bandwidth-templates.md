---
title: "aaaManage StorSimple 頻寬範本 |Microsoft 文件"
description: "描述如何 toomanage StorSimple 頻寬範本，可讓您 toocontrol 頻寬耗用量。"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 0027b90e-91a5-437d-9bd0-06b05674aa5f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2016
ms.author: alkohli
ms.openlocfilehash: 3f767e985667121e977106e7a1f8e5a3ad25f022
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-storsimple-bandwidth-templates"></a><span data-ttu-id="18e2d-103">使用 hello StorSimple Manager 服務 toomanage StorSimple 頻寬範本</span><span class="sxs-lookup"><span data-stu-id="18e2d-103">Use hello StorSimple Manager service toomanage StorSimple bandwidth templates</span></span>
## <a name="overview"></a><span data-ttu-id="18e2d-104">概觀</span><span class="sxs-lookup"><span data-stu-id="18e2d-104">Overview</span></span>
<span data-ttu-id="18e2d-105">頻寬範本可讓您 tooconfigure 網路頻寬使用跨多個日期時間排程 tootier hello 資料從 hello StorSimple 裝置 toohello 雲端。</span><span class="sxs-lookup"><span data-stu-id="18e2d-105">Bandwidth templates allow you tooconfigure network bandwidth usage across multiple time-of-day schedules tootier hello data from hello StorSimple device toohello cloud.</span></span>

<span data-ttu-id="18e2d-106">利用頻寬節流排程，您可以：</span><span class="sxs-lookup"><span data-stu-id="18e2d-106">With bandwidth throttling schedules you can:</span></span>

* <span data-ttu-id="18e2d-107">指定自訂的頻寬排程視 hello 工作負載的網路使用方式而定。</span><span class="sxs-lookup"><span data-stu-id="18e2d-107">Specify customized bandwidth schedules depending on hello workload network usages.</span></span>
* <span data-ttu-id="18e2d-108">集中管理，並重複跨多個裝置的 hello 排程使用簡便而順暢的方式。</span><span class="sxs-lookup"><span data-stu-id="18e2d-108">Centralize management and reuse hello schedules across multiple devices in an easy and seamless manner.</span></span>

> [!NOTE]
> <span data-ttu-id="18e2d-109">這項功能只可供 StorSimple 實體裝置使用，不能用於虛擬裝置。</span><span class="sxs-lookup"><span data-stu-id="18e2d-109">This feature is available only for StorSimple physical devices and not for virtual devices.</span></span>
> 
> 

<span data-ttu-id="18e2d-110">所有的 hello 頻寬範本，為您的服務會顯示在以表格式，並包含下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="18e2d-110">All hello bandwidth templates for your service are displayed in a tabular format, and contain hello following information:</span></span>

* <span data-ttu-id="18e2d-111">**名稱**– 指派唯一名稱 toohello 頻寬範本建立時。</span><span class="sxs-lookup"><span data-stu-id="18e2d-111">**Name** – A unique name assigned toohello bandwidth template when it was created.</span></span>
* <span data-ttu-id="18e2d-112">**排程**– hello 給定的頻寬範本中包含的排程數目。</span><span class="sxs-lookup"><span data-stu-id="18e2d-112">**Schedule** – hello number of schedules contained in a given bandwidth template.</span></span>
* <span data-ttu-id="18e2d-113">**使用**– hello 使用 hello 頻寬範本的磁碟區數目。</span><span class="sxs-lookup"><span data-stu-id="18e2d-113">**Used by** – hello number of volumes using hello bandwidth templates.</span></span>

<span data-ttu-id="18e2d-114">使用 hello StorSimple Manager 服務**設定**hello Azure 傳統入口網站 toomanage 頻寬範本中的頁面。</span><span class="sxs-lookup"><span data-stu-id="18e2d-114">You use hello StorSimple Manager service **Configure** page in hello Azure classic portal toomanage bandwidth templates.</span></span>

<span data-ttu-id="18e2d-115">您也可以找到其他資訊 toohelp 設定頻寬範本中：</span><span class="sxs-lookup"><span data-stu-id="18e2d-115">You can also find additional information toohelp configure bandwidth templates in:</span></span>

* <span data-ttu-id="18e2d-116">頻寬範本的相關問與答</span><span class="sxs-lookup"><span data-stu-id="18e2d-116">Questions and answers about bandwidth templates</span></span>
* <span data-ttu-id="18e2d-117">頻寬範本的最佳作法</span><span class="sxs-lookup"><span data-stu-id="18e2d-117">Best practices for bandwidth templates</span></span>

## <a name="add-a-bandwidth-template"></a><span data-ttu-id="18e2d-118">新增頻寬範本</span><span class="sxs-lookup"><span data-stu-id="18e2d-118">Add a bandwidth template</span></span>
<span data-ttu-id="18e2d-119">執行下列步驟 toocreate 新的頻寬範本的 hello。</span><span class="sxs-lookup"><span data-stu-id="18e2d-119">Perform hello following steps toocreate a new bandwidth template.</span></span>

#### <a name="tooadd-a-bandwidth-template"></a><span data-ttu-id="18e2d-120">tooadd 頻寬範本</span><span class="sxs-lookup"><span data-stu-id="18e2d-120">tooadd a bandwidth template</span></span>
1. <span data-ttu-id="18e2d-121">在 hello StorSimple Manager 服務**設定**頁面上，按一下**新增/編輯頻寬範本**。</span><span class="sxs-lookup"><span data-stu-id="18e2d-121">On hello StorSimple Manager service **Configure** page, click **add/edit bandwidth template**.</span></span>
2. <span data-ttu-id="18e2d-122">在 hello**新增/編輯頻寬範本**對話方塊：</span><span class="sxs-lookup"><span data-stu-id="18e2d-122">In hello **Add/Edit Bandwidth Template** dialog box:</span></span>
   
   1. <span data-ttu-id="18e2d-123">從 hello**範本**下拉式清單中，選取**建立新**tooadd 新的頻寬範本。</span><span class="sxs-lookup"><span data-stu-id="18e2d-123">From hello **Template** drop-down list, select **Create new** tooadd a new bandwidth template.</span></span>
   2. <span data-ttu-id="18e2d-124">為頻寬範本指定唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="18e2d-124">Specify a unique name for your bandwidth template.</span></span>
3. <span data-ttu-id="18e2d-125">定義 **頻寬排程**。</span><span class="sxs-lookup"><span data-stu-id="18e2d-125">Define a **Bandwidth Schedule**.</span></span> <span data-ttu-id="18e2d-126">toocreate 排程：</span><span class="sxs-lookup"><span data-stu-id="18e2d-126">toocreate a schedule:</span></span>
   
   1. <span data-ttu-id="18e2d-127">從 hello 下拉式清單中，選擇設定 hello hello 週 hello 排程的天數。</span><span class="sxs-lookup"><span data-stu-id="18e2d-127">From hello drop-down list, choose hello days of hello week hello schedule is configured for.</span></span> <span data-ttu-id="18e2d-128">您可以選取多天 hello hello 清單中的 hello 各日期前面的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="18e2d-128">You can select multiple days by selecting hello check boxes located before hello respective days in hello list.</span></span>
   2. <span data-ttu-id="18e2d-129">選取 hello**全天**hello 排程是否僅限於 hello 整天選項。</span><span class="sxs-lookup"><span data-stu-id="18e2d-129">Select hello **All Day** option if hello schedule is enforced for hello entire day.</span></span> <span data-ttu-id="18e2d-130">核取此選項時，您無法再指定 [開始時間] 或 [結束時間]。</span><span class="sxs-lookup"><span data-stu-id="18e2d-130">When this option is checked, you can no longer specify a **Start Time** or an **End Time**.</span></span> <span data-ttu-id="18e2d-131">hello 排程執行從 12:00 AM too11: 59 PM。</span><span class="sxs-lookup"><span data-stu-id="18e2d-131">hello schedule runs from 12:00 AM too11:59 PM.</span></span>
   3. <span data-ttu-id="18e2d-132">從 hello 下拉式清單中，選取 **開始時間**。</span><span class="sxs-lookup"><span data-stu-id="18e2d-132">From hello drop-down list, select a **Start Time**.</span></span> <span data-ttu-id="18e2d-133">這是當 hello 排程就會開始。</span><span class="sxs-lookup"><span data-stu-id="18e2d-133">This is when hello schedule will begin.</span></span>
   4. <span data-ttu-id="18e2d-134">從 hello 下拉式清單中，選取 **結束時間**。</span><span class="sxs-lookup"><span data-stu-id="18e2d-134">From hello drop-down list, select an **End Time**.</span></span> <span data-ttu-id="18e2d-135">這是 hello 排程將會停止。</span><span class="sxs-lookup"><span data-stu-id="18e2d-135">This is when hello schedule will stop.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="18e2d-136">不允許重疊的排程。</span><span class="sxs-lookup"><span data-stu-id="18e2d-136">Overlapping schedules are not allowed.</span></span> <span data-ttu-id="18e2d-137">如果 hello 開始和結束時間會產生重疊的排程，您會看到錯誤訊息 toothat 效果。</span><span class="sxs-lookup"><span data-stu-id="18e2d-137">If hello start and end times will result in an overlapping schedule, you will see an error message toothat effect.</span></span>
      > 
      > 
   5. <span data-ttu-id="18e2d-138">指定 hello**頻寬速率**。</span><span class="sxs-lookup"><span data-stu-id="18e2d-138">Specify hello **Bandwidth Rate**.</span></span> <span data-ttu-id="18e2d-139">這是以 mb / 秒 (Mbps 牽涉 hello 雲端 （上傳和下載） 的作業在 StorSimple 裝置所使用) 的 hello 頻寬。</span><span class="sxs-lookup"><span data-stu-id="18e2d-139">This is hello bandwidth in Megabits per second (Mbps) used by your StorSimple device in operations involving hello cloud (both uploads and downloads).</span></span> <span data-ttu-id="18e2d-140">提供一個介於 1 到 1000 之間的數目給此欄位。</span><span class="sxs-lookup"><span data-stu-id="18e2d-140">Supply a number between 1 and 1,000 for this field.</span></span>
   6. <span data-ttu-id="18e2d-141">按一下核取圖示，hello![核取圖示](./media/storsimple-manage-bandwidth-templates/HCS_CheckIcon.png)。</span><span class="sxs-lookup"><span data-stu-id="18e2d-141">Click hello check icon ![Check icon](./media/storsimple-manage-bandwidth-templates/HCS_CheckIcon.png).</span></span> <span data-ttu-id="18e2d-142">您已建立的 hello 範本將會新增頻寬範本清單 toohello hello 服務上**設定**頁面。</span><span class="sxs-lookup"><span data-stu-id="18e2d-142">hello template that you have created will be added toohello list of bandwidth templates on hello service **Configure** page.</span></span>
      
      ![建立新的頻寬範本](./media/storsimple-manage-bandwidth-templates/HCS_CreateNewBT1.png)
4. <span data-ttu-id="18e2d-144">按一下**儲存**在 hello hello 頁面，然後按一下底部**是**出現確認提示時。</span><span class="sxs-lookup"><span data-stu-id="18e2d-144">Click **Save** at hello bottom of hello page and then click **Yes** when prompted for confirmation.</span></span> <span data-ttu-id="18e2d-145">這樣會儲存您所做的 hello 組態變更。</span><span class="sxs-lookup"><span data-stu-id="18e2d-145">This will save hello configuration changes that you have made.</span></span>

## <a name="edit-a-bandwidth-template"></a><span data-ttu-id="18e2d-146">編輯頻寬範本</span><span class="sxs-lookup"><span data-stu-id="18e2d-146">Edit a bandwidth template</span></span>
<span data-ttu-id="18e2d-147">執行下列步驟 tooedit 頻寬範本的 hello。</span><span class="sxs-lookup"><span data-stu-id="18e2d-147">Perform hello following steps tooedit a bandwidth template.</span></span>

### <a name="tooedit-a-bandwidth-template"></a><span data-ttu-id="18e2d-148">tooedit 頻寬範本</span><span class="sxs-lookup"><span data-stu-id="18e2d-148">tooedit a bandwidth template</span></span>
1. <span data-ttu-id="18e2d-149">按一下 [ **新增/編輯頻寬範本**]。</span><span class="sxs-lookup"><span data-stu-id="18e2d-149">Click **add/edit bandwidth template**.</span></span>
2. <span data-ttu-id="18e2d-150">在 hello**新增/編輯頻寬範本**對話方塊：</span><span class="sxs-lookup"><span data-stu-id="18e2d-150">In hello **Add/Edit Bandwidth Template** dialog box:</span></span>
   
   1. <span data-ttu-id="18e2d-151">從 hello**範本**下拉式清單中，選擇現有的頻寬範本的 toomodify。</span><span class="sxs-lookup"><span data-stu-id="18e2d-151">From hello **Template** drop-down list, choose an existing bandwidth template that you want toomodify.</span></span>
   2. <span data-ttu-id="18e2d-152">完成您的變更。</span><span class="sxs-lookup"><span data-stu-id="18e2d-152">Complete your changes.</span></span> <span data-ttu-id="18e2d-153">（您可以修改任何 hello 現有設定。）</span><span class="sxs-lookup"><span data-stu-id="18e2d-153">(You can modify any of hello existing settings.)</span></span>
   3. <span data-ttu-id="18e2d-154">按一下 [hello] 核取圖示</span><span class="sxs-lookup"><span data-stu-id="18e2d-154">Click hello check icon</span></span> ![核取圖示](./media/storsimple-manage-bandwidth-templates/HCS_CheckIcon.png)<span data-ttu-id="18e2d-156">.</span><span class="sxs-lookup"><span data-stu-id="18e2d-156">.</span></span> <span data-ttu-id="18e2d-157">Hello 服務設定 頁面上，您會看到在 hello 頻寬範本清單中的 hello 已修改的範本。</span><span class="sxs-lookup"><span data-stu-id="18e2d-157">You will see hello modified template in hello list of bandwidth templates on hello service Configure page.</span></span>
3. <span data-ttu-id="18e2d-158">您的變更，按一下 toosave**儲存**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="18e2d-158">toosave your changes, click **Save** at hello bottom of hello page.</span></span> <span data-ttu-id="18e2d-159">在頁面底部按一下 [ **是** ]。</span><span class="sxs-lookup"><span data-stu-id="18e2d-159">Click **Yes** when prompted for confirmation.</span></span>

> [!NOTE]
> <span data-ttu-id="18e2d-160">您不會允許您的變更，如果與現有的 hello 已編輯的排程重疊排程 hello 頻寬範本中您要修改的 toosave。</span><span class="sxs-lookup"><span data-stu-id="18e2d-160">You will not be allowed toosave your changes if hello edited schedule overlaps with an existing schedule in hello bandwidth template that you are modifying.</span></span>
> 
> 

## <a name="delete-a-bandwidth-template"></a><span data-ttu-id="18e2d-161">刪除頻寬範本</span><span class="sxs-lookup"><span data-stu-id="18e2d-161">Delete a bandwidth template</span></span>
<span data-ttu-id="18e2d-162">執行下列步驟 toodelete 頻寬範本的 hello。</span><span class="sxs-lookup"><span data-stu-id="18e2d-162">Perform hello following steps toodelete a bandwidth template.</span></span>

#### <a name="toodelete-a-bandwidth-template"></a><span data-ttu-id="18e2d-163">toodelete 頻寬範本</span><span class="sxs-lookup"><span data-stu-id="18e2d-163">toodelete a bandwidth template</span></span>
1. <span data-ttu-id="18e2d-164">在您的服務的 hello 頻寬範本表格式清單中 hello，選取您想 toodelete hello 範本。</span><span class="sxs-lookup"><span data-stu-id="18e2d-164">In hello tabular list of hello bandwidth templates for your service, select hello template that you wish toodelete.</span></span> <span data-ttu-id="18e2d-165">刪除圖示 (**x**) 會出現 toohello 最右側的 hello 選取的範本。</span><span class="sxs-lookup"><span data-stu-id="18e2d-165">A delete icon (**x**) will appear toohello extreme right of hello selected template.</span></span> <span data-ttu-id="18e2d-166">按一下 hello **x**圖示 toodelete hello 範本。</span><span class="sxs-lookup"><span data-stu-id="18e2d-166">Click hello **x** icon toodelete hello template.</span></span>
2. <span data-ttu-id="18e2d-167">系統將提示您進行確認。</span><span class="sxs-lookup"><span data-stu-id="18e2d-167">You will be prompted for confirmation.</span></span> <span data-ttu-id="18e2d-168">按一下**確定**tooproceed。</span><span class="sxs-lookup"><span data-stu-id="18e2d-168">Click **OK** tooproceed.</span></span>

<span data-ttu-id="18e2d-169">如果任何磁碟區的使用中 hello 範本，您不能 toodelete 它。</span><span class="sxs-lookup"><span data-stu-id="18e2d-169">If hello template is in use by any volume(s), you will not be allowed toodelete it.</span></span> <span data-ttu-id="18e2d-170">您會看到錯誤訊息，指出正在使用該 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="18e2d-170">You will see an error message indicating that hello template is in use.</span></span> <span data-ttu-id="18e2d-171">錯誤訊息對話方塊會通知您，應該移除所有 hello 參考 toohello 範本。</span><span class="sxs-lookup"><span data-stu-id="18e2d-171">An error message dialog box will appear advising you that all hello references toohello template should be removed.</span></span>

<span data-ttu-id="18e2d-172">您可以藉由存取 hello 刪除所有的 hello 參考 toohello 範本**磁碟區容器**頁面上，並修改使用此範本，讓它們使用另一個範本，或使用自訂或無限制頻寬的 hello 磁碟區容器設定。</span><span class="sxs-lookup"><span data-stu-id="18e2d-172">You can delete all hello references toohello template by accessing hello **Volume Containers** page and modifying hello volume containers that use this template so that they use another template or use a custom or unlimited bandwidth setting.</span></span> <span data-ttu-id="18e2d-173">當所有 hello 參考已都移除之後時，您可以刪除 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="18e2d-173">When all hello references have been removed, you can delete hello template.</span></span>

## <a name="use-a-default-bandwidth-template"></a><span data-ttu-id="18e2d-174">使用預設頻寬範本</span><span class="sxs-lookup"><span data-stu-id="18e2d-174">Use a default bandwidth template</span></span>
<span data-ttu-id="18e2d-175">預設頻寬範本提供，並可供磁碟區容器依預設 tooenforce 頻寬控制存取 hello 雲端。</span><span class="sxs-lookup"><span data-stu-id="18e2d-175">A default bandwidth template is provided and is used by volume containers by default tooenforce bandwidth controls when accessing hello cloud.</span></span> <span data-ttu-id="18e2d-176">hello 預設範本也可做為現成的參考的使用者建立其自己的範本。</span><span class="sxs-lookup"><span data-stu-id="18e2d-176">hello default template also serves as a ready reference for users who create their own templates.</span></span> <span data-ttu-id="18e2d-177">此預設範本的 hello 詳細資料如下：</span><span class="sxs-lookup"><span data-stu-id="18e2d-177">hello details of this default template are:</span></span>

* <span data-ttu-id="18e2d-178">**名稱** – 不限制夜間和週末</span><span class="sxs-lookup"><span data-stu-id="18e2d-178">**Name** – Unlimited nights and weekends</span></span>
* <span data-ttu-id="18e2d-179">**排程**– 從星期一 tooFriday 適用於上午 8 點和下午 5 點裝置時間之間的 1 Mbps 的頻寬速率的單一排程。</span><span class="sxs-lookup"><span data-stu-id="18e2d-179">**Schedule** – A single schedule from Monday tooFriday that applies a bandwidth rate of 1 Mbps between 8 AM and 5 PM device time.</span></span> <span data-ttu-id="18e2d-180">hello 頻寬設定 tooUnlimited hello 週 hello 其餘部分。</span><span class="sxs-lookup"><span data-stu-id="18e2d-180">hello bandwidth is set tooUnlimited for hello remainder of hello week.</span></span>

<span data-ttu-id="18e2d-181">可以編輯 hello 預設範本。</span><span class="sxs-lookup"><span data-stu-id="18e2d-181">hello default template can be edited.</span></span> <span data-ttu-id="18e2d-182">hello 使用量 （包括已編輯的版本） 這個範本會追蹤。</span><span class="sxs-lookup"><span data-stu-id="18e2d-182">hello usage of this template (including edited versions) is tracked.</span></span>

## <a name="create-an-all-day-bandwidth-template-that-starts-at-a-specified-time"></a><span data-ttu-id="18e2d-183">建立在指定時間啟動的全天頻寬範本</span><span class="sxs-lookup"><span data-stu-id="18e2d-183">Create an all-day bandwidth template that starts at a specified time</span></span>
<span data-ttu-id="18e2d-184">請遵循此程序 toocreate 在指定時間啟動並執行所有日期的排程。</span><span class="sxs-lookup"><span data-stu-id="18e2d-184">Follow this procedure toocreate a schedule that starts at a specified time and runs all day.</span></span> <span data-ttu-id="18e2d-185">在 hello 範例中，hello 排程 hello 早上 9 點開始，直到上午 9 點 hello 隔天早上執行。</span><span class="sxs-lookup"><span data-stu-id="18e2d-185">In hello example, hello schedule starts at 9 AM in hello morning and runs until 9 AM hello next morning.</span></span> <span data-ttu-id="18e2d-186">很重要的 toonote hello 開始，並指定排程的結束時間都必須包含在 hello 相同 24 小時排程，且不能跨越多天。</span><span class="sxs-lookup"><span data-stu-id="18e2d-186">It's important toonote that hello start and end times for a given schedule must both be contained on hello same 24 hour schedule and cannot span multiple days.</span></span> <span data-ttu-id="18e2d-187">如果您需要 tooset 向上跨多天的頻寬範本，您將需要 toouse 多個排程 （如 hello 範例所示）。</span><span class="sxs-lookup"><span data-stu-id="18e2d-187">If you need tooset up bandwidth templates that span multiple days, you will need toouse multiple schedules (as shown in hello example).</span></span>

#### <a name="toocreate-an-all-day-bandwidth-template"></a><span data-ttu-id="18e2d-188">toocreate 全天頻寬範本</span><span class="sxs-lookup"><span data-stu-id="18e2d-188">toocreate an all-day bandwidth template</span></span>
1. <span data-ttu-id="18e2d-189">建立在 hello 早上 9 點啟動並執行到午夜的排程。</span><span class="sxs-lookup"><span data-stu-id="18e2d-189">Create a schedule that starts at 9 AM in hello morning and runs until midnight.</span></span>
2. <span data-ttu-id="18e2d-190">新增另一個排程。</span><span class="sxs-lookup"><span data-stu-id="18e2d-190">Add another schedule.</span></span> <span data-ttu-id="18e2d-191">設定從午夜 hello 第二個排程 toorun hello 早上 9 點。</span><span class="sxs-lookup"><span data-stu-id="18e2d-191">Configure hello second schedule toorun from midnight until 9 AM in hello morning.</span></span>
3. <span data-ttu-id="18e2d-192">儲存 hello 頻寬範本。</span><span class="sxs-lookup"><span data-stu-id="18e2d-192">Save hello bandwidth template.</span></span>

<span data-ttu-id="18e2d-193">接著在您選擇的時間啟動並全天執行 hello 複合排程。</span><span class="sxs-lookup"><span data-stu-id="18e2d-193">hello composite schedule will then start at a time of your choosing and run all-day.</span></span>

## <a name="questions-and-answers-about-bandwidth-templates"></a><span data-ttu-id="18e2d-194">頻寬範本的相關問與答</span><span class="sxs-lookup"><span data-stu-id="18e2d-194">Questions and answers about bandwidth templates</span></span>
<span data-ttu-id="18e2d-195">**問：**</span><span class="sxs-lookup"><span data-stu-id="18e2d-195">**Q**.</span></span> <span data-ttu-id="18e2d-196">發生什麼事 toobandwidth 控制項 hello 排程之間會？</span><span class="sxs-lookup"><span data-stu-id="18e2d-196">What happens toobandwidth controls when you are in between hello schedules?</span></span> <span data-ttu-id="18e2d-197">(一個排程已結束而另一個排程尚未開始)。</span><span class="sxs-lookup"><span data-stu-id="18e2d-197">(A schedule has ended and another one has not started yet.)</span></span>

<span data-ttu-id="18e2d-198">**答：**</span><span class="sxs-lookup"><span data-stu-id="18e2d-198">**A**.</span></span> <span data-ttu-id="18e2d-199">在這種情況下，不會採用任何頻寬控制。</span><span class="sxs-lookup"><span data-stu-id="18e2d-199">In such cases, no bandwidth controls will be employed.</span></span> <span data-ttu-id="18e2d-200">這表示該 hello 裝置分層資料 toohello 雲端時，可以使用無限制的頻寬。</span><span class="sxs-lookup"><span data-stu-id="18e2d-200">This means that hello device can use unlimited bandwidth when tiering data toohello cloud.</span></span>

<span data-ttu-id="18e2d-201">**問：**</span><span class="sxs-lookup"><span data-stu-id="18e2d-201">**Q**.</span></span> <span data-ttu-id="18e2d-202">您是否可以修改離線裝置上的頻寬範本？</span><span class="sxs-lookup"><span data-stu-id="18e2d-202">Can you modify bandwidth templates on an offline device?</span></span>

<span data-ttu-id="18e2d-203">**答：**</span><span class="sxs-lookup"><span data-stu-id="18e2d-203">**A**.</span></span> <span data-ttu-id="18e2d-204">如果 hello 對應的裝置已離線，您將無法能 toomodify 磁碟區容器上的頻寬範本。</span><span class="sxs-lookup"><span data-stu-id="18e2d-204">You will not be able toomodify bandwidth templates on volumes containers if hello corresponding device is offline.</span></span>

<span data-ttu-id="18e2d-205">**問：**</span><span class="sxs-lookup"><span data-stu-id="18e2d-205">**Q**.</span></span> <span data-ttu-id="18e2d-206">您可以編輯 hello 相關聯的磁碟區離線時，與磁碟區容器相關聯的頻寬範本嗎？</span><span class="sxs-lookup"><span data-stu-id="18e2d-206">Can you edit a bandwidth template associated with a volume container when hello associated volumes are offline?</span></span>

<span data-ttu-id="18e2d-207">**答：**</span><span class="sxs-lookup"><span data-stu-id="18e2d-207">**A**.</span></span> <span data-ttu-id="18e2d-208">您可以修改和磁碟區已離線之磁碟區容器相關聯的頻寬範本。</span><span class="sxs-lookup"><span data-stu-id="18e2d-208">You can modify a bandwidth template associated with a volume container whose volumes are offline.</span></span> <span data-ttu-id="18e2d-209">請注意，當磁碟區離線，任何資料會分層從 hello 裝置 toohello 雲端。</span><span class="sxs-lookup"><span data-stu-id="18e2d-209">Note that when volumes are offline, no data will be tiered from hello device toohello cloud.</span></span>

<span data-ttu-id="18e2d-210">**問：**</span><span class="sxs-lookup"><span data-stu-id="18e2d-210">**Q**.</span></span> <span data-ttu-id="18e2d-211">您是否可以刪除預設範本？</span><span class="sxs-lookup"><span data-stu-id="18e2d-211">Can you delete a default template?</span></span>

<span data-ttu-id="18e2d-212">**答：**</span><span class="sxs-lookup"><span data-stu-id="18e2d-212">**A**.</span></span> <span data-ttu-id="18e2d-213">雖然您可以刪除預設範本，但它並不建議 toodo。</span><span class="sxs-lookup"><span data-stu-id="18e2d-213">Although you can delete a default template, it is not a good idea toodo so.</span></span> <span data-ttu-id="18e2d-214">hello 使用量的預設範本，包括已編輯的版本中，系統會追蹤。</span><span class="sxs-lookup"><span data-stu-id="18e2d-214">hello usage of a default template, including edited versions, is tracked.</span></span> <span data-ttu-id="18e2d-215">hello 追蹤資料分析，並透過 hello 課程中的時間，是使用的 tooimprove hello 預設範本。</span><span class="sxs-lookup"><span data-stu-id="18e2d-215">hello tracking data is analyzed and over hello course of time, is used tooimprove hello default template.</span></span>

<span data-ttu-id="18e2d-216">**問：**</span><span class="sxs-lookup"><span data-stu-id="18e2d-216">**Q**.</span></span> <span data-ttu-id="18e2d-217">如何判斷頻寬範本需要 toobe 修改？</span><span class="sxs-lookup"><span data-stu-id="18e2d-217">How do you determine that your bandwidth templates need toobe modified?</span></span>

<span data-ttu-id="18e2d-218">**答：**</span><span class="sxs-lookup"><span data-stu-id="18e2d-218">**A**.</span></span> <span data-ttu-id="18e2d-219">一開始時，您需要 toomodify hello 頻寬範本的徵兆的 hello 看見 hello 網路變慢或在一天多次阻礙。</span><span class="sxs-lookup"><span data-stu-id="18e2d-219">One of hello signs that you need toomodify hello bandwidth templates is when you start seeing hello network slow down or choke multiple times in a day.</span></span> <span data-ttu-id="18e2d-220">如果發生這種情況，請查看 hello I/O 效能及網路輸送量圖表監視 hello 儲存體和使用網路。</span><span class="sxs-lookup"><span data-stu-id="18e2d-220">If this happens, monitor hello storage and usage network by looking at hello I/O Performance and Network Throughput charts.</span></span>

<span data-ttu-id="18e2d-221">從 hello 網路輸送量資料中，找出 hello 一天的時間並 hello 中的 hello 網路瓶頸後，就會發生的磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="18e2d-221">From hello network throughput data, identify hello time of day and hello volume containers in which hello network bottleneck occurs.</span></span> <span data-ttu-id="18e2d-222">如果發生這種情況時資料分層式的 toohello 雲端 （取得這項資訊的所有磁碟區容器從 I/O 效能裝置 toocloud），則需要 toomodify hello 頻寬範本與磁碟區容器相關聯。</span><span class="sxs-lookup"><span data-stu-id="18e2d-222">If this happens when data is being tiered toohello cloud (get this information from I/O performance for all volume containers for device toocloud), then you will need toomodify hello bandwidth templates associated with your volume containers.</span></span>

<span data-ttu-id="18e2d-223">Hello 修改後範本正在使用中，您必須 toomonitor hello 網路一次無顯著的延遲。</span><span class="sxs-lookup"><span data-stu-id="18e2d-223">After hello modified templates are in use, you will need toomonitor hello network again for significant latencies.</span></span> <span data-ttu-id="18e2d-224">如果這些狀況仍存在，則您需要 toorevisit 頻寬範本。</span><span class="sxs-lookup"><span data-stu-id="18e2d-224">If these still exist, then you will need toorevisit your bandwidth templates.</span></span>

<span data-ttu-id="18e2d-225">**問：**</span><span class="sxs-lookup"><span data-stu-id="18e2d-225">**Q**.</span></span> <span data-ttu-id="18e2d-226">萬一我的裝置上的多個磁碟區容器有重疊的排程，但不同限制套用 tooeach 嗎？</span><span class="sxs-lookup"><span data-stu-id="18e2d-226">What happens if multiple volume containers on my device have schedules that overlap but different limits apply tooeach?</span></span>

<span data-ttu-id="18e2d-227">**答：**</span><span class="sxs-lookup"><span data-stu-id="18e2d-227">**A**.</span></span> <span data-ttu-id="18e2d-228">假設您的裝置有 3 個磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="18e2d-228">Let's assume that you have a device with 3 volume containers.</span></span> <span data-ttu-id="18e2d-229">hello 完全與這些容器相關聯的排程重疊。</span><span class="sxs-lookup"><span data-stu-id="18e2d-229">hello schedules associated with these containers completely overlap.</span></span> <span data-ttu-id="18e2d-230">針對每個容器，使用 hello 頻寬限制分別 5、 10 和 15 Mbps。</span><span class="sxs-lookup"><span data-stu-id="18e2d-230">For each of these containers, hello bandwidth limits used are 5, 10, and 15 Mbps respectively.</span></span> <span data-ttu-id="18e2d-231">當 I/o 所發生的所有可能套用相同的時間，hello 最小值為 hello 3 頻寬限制的 hello 在這些容器： 在此情況下，因此這些傳出 I/O 要求共用為 5 Mbps hello 相同的佇列。</span><span class="sxs-lookup"><span data-stu-id="18e2d-231">When I/Os are occurring on all of these containers at hello same time, hello minimum of hello 3 bandwidth limits may be applied: in this case, 5 Mbps as these outgoing I/O requests share hello same queue.</span></span>

## <a name="best-practices-for-bandwidth-templates"></a><span data-ttu-id="18e2d-232">頻寬範本的最佳作法</span><span class="sxs-lookup"><span data-stu-id="18e2d-232">Best practices for bandwidth templates</span></span>
<span data-ttu-id="18e2d-233">請遵循 StorSimple 裝置的最佳作法：</span><span class="sxs-lookup"><span data-stu-id="18e2d-233">Follow these best practices for your StorSimple device:</span></span>

* <span data-ttu-id="18e2d-234">設定您裝置 tooenable 變數節流的 hello 網路輸送量 hello 裝置在 hello 每天不同時間的頻寬範本。</span><span class="sxs-lookup"><span data-stu-id="18e2d-234">Configure bandwidth templates on your device tooenable variable throttling of hello network throughput by hello device at different times of hello day.</span></span> <span data-ttu-id="18e2d-235">這些頻寬範本和備份排程搭配使用時，可以在離峰時段期間有效利用雲端作業的其他網路頻寬。</span><span class="sxs-lookup"><span data-stu-id="18e2d-235">These bandwidth templates when used with backup schedules can effectively leverage additional network bandwidth for cloud operations during off-peak hours.</span></span>
* <span data-ttu-id="18e2d-236">計算所需的基礎 hello 大小 hello 部署與 hello 所需的復原時間目標 (RTO) 的特定部署的 hello 實際頻寬。</span><span class="sxs-lookup"><span data-stu-id="18e2d-236">Calculate hello actual bandwidth required for a particular deployment based on hello size of hello deployment and hello required recovery time objective (RTO).</span></span>

## <a name="next-steps"></a><span data-ttu-id="18e2d-237">後續步驟</span><span class="sxs-lookup"><span data-stu-id="18e2d-237">Next steps</span></span>
<span data-ttu-id="18e2d-238">深入了解[使用您的 StorSimple 裝置 hello StorSimple Manager 服務 tooadminister](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="18e2d-238">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

