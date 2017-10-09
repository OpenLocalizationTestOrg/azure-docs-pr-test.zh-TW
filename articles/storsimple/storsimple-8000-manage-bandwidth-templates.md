---
title: "StorSimple 8000 系列的 aaaManage 頻寬範本 |Microsoft 文件"
description: "描述如何 toomanage StorSimple 頻寬範本，可讓您 toocontrol 頻寬耗用量。"
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
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: ebcd1824d7bb9e4c235194c04edbfe8001a3e794
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-storsimple-bandwidth-templates"></a><span data-ttu-id="5693f-103">使用 hello StorSimple 裝置管理員服務 toomanage StorSimple 頻寬範本</span><span class="sxs-lookup"><span data-stu-id="5693f-103">Use hello StorSimple Device Manager service toomanage StorSimple bandwidth templates</span></span>

## <a name="overview"></a><span data-ttu-id="5693f-104">概觀</span><span class="sxs-lookup"><span data-stu-id="5693f-104">Overview</span></span>

<span data-ttu-id="5693f-105">頻寬範本可讓您 tooconfigure 網路頻寬使用跨多個日期時間排程 tootier hello 資料從 hello StorSimple 裝置 toohello 雲端。</span><span class="sxs-lookup"><span data-stu-id="5693f-105">Bandwidth templates allow you tooconfigure network bandwidth usage across multiple time-of-day schedules tootier hello data from hello StorSimple device toohello cloud.</span></span>

<span data-ttu-id="5693f-106">利用頻寬節流排程，您可以：</span><span class="sxs-lookup"><span data-stu-id="5693f-106">With bandwidth throttling schedules you can:</span></span>

* <span data-ttu-id="5693f-107">指定自訂的頻寬排程視 hello 工作負載的網路使用方式而定。</span><span class="sxs-lookup"><span data-stu-id="5693f-107">Specify customized bandwidth schedules depending on hello workload network usages.</span></span>
* <span data-ttu-id="5693f-108">集中管理，並重複跨多個裝置的 hello 排程使用簡便而順暢的方式。</span><span class="sxs-lookup"><span data-stu-id="5693f-108">Centralize management and reuse hello schedules across multiple devices in an easy and seamless manner.</span></span>

> [!NOTE]
> <span data-ttu-id="5693f-109">此功能僅適用於 StorSimple 實體裝置 (8100 和 8600 機型)，而不適用於 StorSimple 雲端設備 (8010 和 8020 機型)。</span><span class="sxs-lookup"><span data-stu-id="5693f-109">This feature is available only for StorSimple physical devices (models 8100 and 8600) and not for StorSimple Cloud Appliances (models 8010 and 8020).</span></span>


## <a name="hello-bandwidth-templates-blade"></a><span data-ttu-id="5693f-110">hello 頻寬範本 刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="5693f-110">hello Bandwidth templates blade</span></span>

<span data-ttu-id="5693f-111">hello**頻寬範本**刀鋒視窗以表格式格式，具有所有 hello 頻寬範本，為您的服務，且包含下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="5693f-111">hello **Bandwidth templates** blade has all hello bandwidth templates for your service in a tabular format, and contains hello following information:</span></span>

* <span data-ttu-id="5693f-112">**名稱**– 指派唯一名稱 toohello 頻寬範本建立時。</span><span class="sxs-lookup"><span data-stu-id="5693f-112">**Name** – A unique name assigned toohello bandwidth template when it was created.</span></span>
* <span data-ttu-id="5693f-113">**排程**– hello 給定的頻寬範本中包含的排程數目。</span><span class="sxs-lookup"><span data-stu-id="5693f-113">**Schedule** – hello number of schedules contained in a given bandwidth template.</span></span>
* <span data-ttu-id="5693f-114">**使用**– hello 使用 hello 頻寬範本的磁碟區數目。</span><span class="sxs-lookup"><span data-stu-id="5693f-114">**Used by** – hello number of volumes using hello bandwidth templates.</span></span>

<span data-ttu-id="5693f-115">您也可以找到其他資訊 toohelp 設定頻寬範本中：</span><span class="sxs-lookup"><span data-stu-id="5693f-115">You can also find additional information toohelp configure bandwidth templates in:</span></span>

* [<span data-ttu-id="5693f-116">頻寬範本的相關問與答</span><span class="sxs-lookup"><span data-stu-id="5693f-116">Questions and answers about bandwidth templates</span></span>](#questions-and-answers-about-bandwidth-templates)
* [<span data-ttu-id="5693f-117">頻寬範本的最佳作法</span><span class="sxs-lookup"><span data-stu-id="5693f-117">Best practices for bandwidth templates</span></span>](#best-practices-for-bandwidth-templates)

## <a name="add-a-bandwidth-template"></a><span data-ttu-id="5693f-118">新增頻寬範本</span><span class="sxs-lookup"><span data-stu-id="5693f-118">Add a bandwidth template</span></span>

<span data-ttu-id="5693f-119">執行下列步驟 toocreate 新的頻寬範本的 hello。</span><span class="sxs-lookup"><span data-stu-id="5693f-119">Perform hello following steps toocreate a new bandwidth template.</span></span>

#### <a name="tooadd-a-bandwidth-template"></a><span data-ttu-id="5693f-120">tooadd 頻寬範本</span><span class="sxs-lookup"><span data-stu-id="5693f-120">tooadd a bandwidth template</span></span>

1. <span data-ttu-id="5693f-121">移 tooyour StorSimple 裝置管理員服務，請按一下**頻寬範本**，然後按一下 **+ 新增頻寬範本**。</span><span class="sxs-lookup"><span data-stu-id="5693f-121">Go tooyour StorSimple Device Manager service, click **Bandwidth templates** and then click **+ Add Bandwidth template**.</span></span>

    ![按一下 [+ 新增頻寬範本]](./media/storsimple-8000-manage-bandwidth-templates/addbwtemp1.png)

2. <span data-ttu-id="5693f-123">在 hello**新增頻寬範本**刀鋒視窗中，執行下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="5693f-123">In hello **Add bandwidth template** blade, do hello following steps:</span></span>
   
    1. <span data-ttu-id="5693f-124">為頻寬範本指定唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="5693f-124">Specify a unique name for your bandwidth template.</span></span>
    2. <span data-ttu-id="5693f-125">定義頻寬排程。</span><span class="sxs-lookup"><span data-stu-id="5693f-125">Define a bandwidth schedule.</span></span> <span data-ttu-id="5693f-126">toocreate 排程：</span><span class="sxs-lookup"><span data-stu-id="5693f-126">toocreate a schedule:</span></span>
   
        1. <span data-ttu-id="5693f-127">從 hello 下拉式清單中，選擇 hello**天**hello 週 hello 的排程設定的。</span><span class="sxs-lookup"><span data-stu-id="5693f-127">From hello drop-down list, choose hello **Days** of hello week hello schedule is configured for.</span></span> <span data-ttu-id="5693f-128">您可以選取多天。</span><span class="sxs-lookup"><span data-stu-id="5693f-128">You can select multiple days.</span></span>        
        
        2. <span data-ttu-id="5693f-129">輸入 [開始時間]，格式為 _hh:mm_。</span><span class="sxs-lookup"><span data-stu-id="5693f-129">Enter a **Start Time** in _hh:mm_ format.</span></span> <span data-ttu-id="5693f-130">這是當 hello 排程就會開始。</span><span class="sxs-lookup"><span data-stu-id="5693f-130">This is when hello schedule will begin.</span></span>

        3. <span data-ttu-id="5693f-131">輸入 [結束時間]，格式為 _hh:mm_。</span><span class="sxs-lookup"><span data-stu-id="5693f-131">Enter an **End Time** in _hh:mm_ format.</span></span> <span data-ttu-id="5693f-132">這是 hello 排程將會停止。</span><span class="sxs-lookup"><span data-stu-id="5693f-132">This is when hello schedule will stop.</span></span>
      
           > [!NOTE]
           > <span data-ttu-id="5693f-133">不允許重疊的排程。</span><span class="sxs-lookup"><span data-stu-id="5693f-133">Overlapping schedules are not allowed.</span></span> <span data-ttu-id="5693f-134">如果 hello 開始和結束時間會產生重疊的排程，您會看到錯誤訊息 toothat 效果。</span><span class="sxs-lookup"><span data-stu-id="5693f-134">If hello start and end times will result in an overlapping schedule, you will see an error message toothat effect.</span></span>

        4. <span data-ttu-id="5693f-135">指定 hello**頻寬速率**。</span><span class="sxs-lookup"><span data-stu-id="5693f-135">Specify hello **Bandwidth Rate**.</span></span> <span data-ttu-id="5693f-136">這是以 mb / 秒 (Mbps 牽涉 hello 雲端 （上傳和下載） 的作業在 StorSimple 裝置所使用) 的 hello 頻寬。</span><span class="sxs-lookup"><span data-stu-id="5693f-136">This is hello bandwidth in Megabits per second (Mbps) used by your StorSimple device in operations involving hello cloud (both uploads and downloads).</span></span> <span data-ttu-id="5693f-137">提供一個介於 1 到 1000 之間的數目給此欄位。</span><span class="sxs-lookup"><span data-stu-id="5693f-137">Supply a number between 1 and 1,000 for this field.</span></span>

            ![定義頻寬排程](./media/storsimple-8000-manage-bandwidth-templates/addbwtemp2.png)
         
            <span data-ttu-id="5693f-139">重複上述步驟 toodefine hello，直到您完成多個排程為範本。</span><span class="sxs-lookup"><span data-stu-id="5693f-139">Repeat hello above steps toodefine multiple schedules for your template until you are done.</span></span>

        5. <span data-ttu-id="5693f-140">按一下**新增**toostart 建立頻寬範本。</span><span class="sxs-lookup"><span data-stu-id="5693f-140">Click **Add** toostart creating a bandwidth template.</span></span> <span data-ttu-id="5693f-141">建立範本的 hello 加入 toohello 頻寬範本清單。</span><span class="sxs-lookup"><span data-stu-id="5693f-141">hello created template is added toohello list of bandwidth templates.</span></span>
      

## <a name="edit-a-bandwidth-template"></a><span data-ttu-id="5693f-142">編輯頻寬範本</span><span class="sxs-lookup"><span data-stu-id="5693f-142">Edit a bandwidth template</span></span>

<span data-ttu-id="5693f-143">執行下列步驟 tooedit 頻寬範本的 hello。</span><span class="sxs-lookup"><span data-stu-id="5693f-143">Perform hello following steps tooedit a bandwidth template.</span></span>

### <a name="tooedit-a-bandwidth-template"></a><span data-ttu-id="5693f-144">tooedit 頻寬範本</span><span class="sxs-lookup"><span data-stu-id="5693f-144">tooedit a bandwidth template</span></span>

1. <span data-ttu-id="5693f-145">移 tooyour StorSimple 裝置管理員服務，然後按一下**頻寬範本**。</span><span class="sxs-lookup"><span data-stu-id="5693f-145">Go tooyour StorSimple Device Manager service and click **Bandwidth templates**.</span></span>
2. <span data-ttu-id="5693f-146">Hello 頻寬範本清單中選取您想 toodelete hello 範本。</span><span class="sxs-lookup"><span data-stu-id="5693f-146">In hello list of bandwidth templates, select hello template you wish toodelete.</span></span> <span data-ttu-id="5693f-147">以滑鼠右鍵按一下，然後從 hello 內容功能表中，選取**刪除**。</span><span class="sxs-lookup"><span data-stu-id="5693f-147">Right-click and from hello context menu, select **Delete**.</span></span>
3. <span data-ttu-id="5693f-148">系統提示您進行確認時，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="5693f-148">When prompted for confirmation, click **OK**.</span></span> <span data-ttu-id="5693f-149">這應該刪除 hello 頻寬範本。</span><span class="sxs-lookup"><span data-stu-id="5693f-149">This should delete hello bandwidth template.</span></span> 
4. <span data-ttu-id="5693f-150">更新 tooreflect hello 刪除頻寬範本 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="5693f-150">hello list of bandwidth templates updates tooreflect hello deletion.</span></span>

> [!NOTE]
> <span data-ttu-id="5693f-151">如果 hello 編輯與您要修改的 hello 頻寬範本中的現有排程的排程重疊，您無法儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="5693f-151">You cannot save your changes if hello edited schedule overlaps with an existing schedule in hello bandwidth template that you are modifying.</span></span>

## <a name="delete-a-bandwidth-template"></a><span data-ttu-id="5693f-152">刪除頻寬範本</span><span class="sxs-lookup"><span data-stu-id="5693f-152">Delete a bandwidth template</span></span>

<span data-ttu-id="5693f-153">執行下列步驟 toodelete 頻寬範本的 hello。</span><span class="sxs-lookup"><span data-stu-id="5693f-153">Perform hello following steps toodelete a bandwidth template.</span></span>

#### <a name="toodelete-a-bandwidth-template"></a><span data-ttu-id="5693f-154">toodelete 頻寬範本</span><span class="sxs-lookup"><span data-stu-id="5693f-154">toodelete a bandwidth template</span></span>

1. <span data-ttu-id="5693f-155">移 tooyour StorSimple 裝置管理員服務，然後按一下**頻寬範本**。</span><span class="sxs-lookup"><span data-stu-id="5693f-155">Go tooyour StorSimple Device Manager service and click **Bandwidth templates**.</span></span>
2. <span data-ttu-id="5693f-156">Hello 頻寬範本清單中選取您想 toodelete hello 範本。</span><span class="sxs-lookup"><span data-stu-id="5693f-156">In hello list of bandwidth templates, select hello template you wish toodelete.</span></span> <span data-ttu-id="5693f-157">以滑鼠右鍵按一下並從 hello 內容功能表中，選取 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="5693f-157">Right-click and from hello context menu, select Delete.</span></span>
3. <span data-ttu-id="5693f-158">系統提示您進行確認時，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="5693f-158">When prompted for confirmation, click **OK**.</span></span> <span data-ttu-id="5693f-159">這應該刪除 hello 頻寬範本。</span><span class="sxs-lookup"><span data-stu-id="5693f-159">This should delete hello bandwidth template.</span></span>
4. <span data-ttu-id="5693f-160">更新 tooreflect hello 刪除頻寬範本 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="5693f-160">hello list of bandwidth templates updates tooreflect hello deletion.</span></span>

<span data-ttu-id="5693f-161">如果任何磁碟區的使用中 hello 範本，您不能 toodelete 它。</span><span class="sxs-lookup"><span data-stu-id="5693f-161">If hello template is in use by any volume(s), you will not be allowed toodelete it.</span></span> <span data-ttu-id="5693f-162">您會看到錯誤訊息，指出正在使用該 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="5693f-162">You will see an error message indicating that hello template is in use.</span></span> <span data-ttu-id="5693f-163">錯誤訊息對話方塊會通知您，應該移除所有 hello 參考 toohello 範本。</span><span class="sxs-lookup"><span data-stu-id="5693f-163">An error message dialog box will appear advising you that all hello references toohello template should be removed.</span></span>

<span data-ttu-id="5693f-164">您可以藉由存取 hello 刪除所有的 hello 參考 toohello 範本**磁碟區容器**頁面上，並修改使用此範本，讓它們使用另一個範本，或使用自訂或無限制頻寬的 hello 磁碟區容器設定。</span><span class="sxs-lookup"><span data-stu-id="5693f-164">You can delete all hello references toohello template by accessing hello **Volume Containers** page and modifying hello volume containers that use this template so that they use another template or use a custom or unlimited bandwidth setting.</span></span> <span data-ttu-id="5693f-165">當所有 hello 參考已都移除之後時，您可以刪除 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="5693f-165">When all hello references have been removed, you can delete hello template.</span></span>

## <a name="use-a-default-bandwidth-template"></a><span data-ttu-id="5693f-166">使用預設頻寬範本</span><span class="sxs-lookup"><span data-stu-id="5693f-166">Use a default bandwidth template</span></span>

<span data-ttu-id="5693f-167">預設頻寬範本提供，並可供磁碟區容器依預設 tooenforce 頻寬控制存取 hello 雲端。</span><span class="sxs-lookup"><span data-stu-id="5693f-167">A default bandwidth template is provided and is used by volume containers by default tooenforce bandwidth controls when accessing hello cloud.</span></span> <span data-ttu-id="5693f-168">hello 預設範本也可做為現成的參考的使用者建立其自己的範本。</span><span class="sxs-lookup"><span data-stu-id="5693f-168">hello default template also serves as a ready reference for users who create their own templates.</span></span> <span data-ttu-id="5693f-169">此預設範本的 hello 詳細資料如下：</span><span class="sxs-lookup"><span data-stu-id="5693f-169">hello details of this default template are:</span></span>

* <span data-ttu-id="5693f-170">**名稱** – 不限制夜間和週末</span><span class="sxs-lookup"><span data-stu-id="5693f-170">**Name** – Unlimited nights and weekends</span></span>
* <span data-ttu-id="5693f-171">**排程**– 從星期一 tooFriday 適用於上午 8 點和下午 5 點裝置時間之間的 1 Mbps 的頻寬速率的單一排程。</span><span class="sxs-lookup"><span data-stu-id="5693f-171">**Schedule** – A single schedule from Monday tooFriday that applies a bandwidth rate of 1 Mbps between 8 AM and 5 PM device time.</span></span> <span data-ttu-id="5693f-172">hello 頻寬設定 tooUnlimited hello 週 hello 其餘部分。</span><span class="sxs-lookup"><span data-stu-id="5693f-172">hello bandwidth is set tooUnlimited for hello remainder of hello week.</span></span>

<span data-ttu-id="5693f-173">可以編輯 hello 預設範本。</span><span class="sxs-lookup"><span data-stu-id="5693f-173">hello default template can be edited.</span></span> <span data-ttu-id="5693f-174">hello 使用量 （包括已編輯的版本） 這個範本會追蹤。</span><span class="sxs-lookup"><span data-stu-id="5693f-174">hello usage of this template (including edited versions) is tracked.</span></span>

## <a name="create-an-all-day-bandwidth-template-that-starts-at-a-specified-time"></a><span data-ttu-id="5693f-175">建立在指定時間啟動的全天頻寬範本</span><span class="sxs-lookup"><span data-stu-id="5693f-175">Create an all-day bandwidth template that starts at a specified time</span></span>

<span data-ttu-id="5693f-176">請遵循此程序 toocreate 在指定時間啟動並執行所有日期的排程。</span><span class="sxs-lookup"><span data-stu-id="5693f-176">Follow this procedure toocreate a schedule that starts at a specified time and runs all day.</span></span> <span data-ttu-id="5693f-177">在 hello 範例中，hello 排程 hello 早上 9 點開始，直到上午 9 點 hello 隔天早上執行。</span><span class="sxs-lookup"><span data-stu-id="5693f-177">In hello example, hello schedule starts at 9 AM in hello morning and runs until 9 AM hello next morning.</span></span> <span data-ttu-id="5693f-178">很重要的 toonote hello 開始，並指定排程的結束時間都必須包含在 hello 相同 24 小時排程，且不能跨越多天。</span><span class="sxs-lookup"><span data-stu-id="5693f-178">It's important toonote that hello start and end times for a given schedule must both be contained on hello same 24 hour schedule and cannot span multiple days.</span></span> <span data-ttu-id="5693f-179">如果您需要 tooset 向上跨多天的頻寬範本，您將需要 toouse 多個排程 （如 hello 範例所示）。</span><span class="sxs-lookup"><span data-stu-id="5693f-179">If you need tooset up bandwidth templates that span multiple days, you will need toouse multiple schedules (as shown in hello example).</span></span>

#### <a name="toocreate-an-all-day-bandwidth-template"></a><span data-ttu-id="5693f-180">toocreate 全天頻寬範本</span><span class="sxs-lookup"><span data-stu-id="5693f-180">toocreate an all-day bandwidth template</span></span>

1. <span data-ttu-id="5693f-181">建立在 hello 早上 9 點啟動並執行到午夜的排程。</span><span class="sxs-lookup"><span data-stu-id="5693f-181">Create a schedule that starts at 9 AM in hello morning and runs until midnight.</span></span>
2. <span data-ttu-id="5693f-182">新增另一個排程。</span><span class="sxs-lookup"><span data-stu-id="5693f-182">Add another schedule.</span></span> <span data-ttu-id="5693f-183">設定從午夜 hello 第二個排程 toorun hello 早上 9 點。</span><span class="sxs-lookup"><span data-stu-id="5693f-183">Configure hello second schedule toorun from midnight until 9 AM in hello morning.</span></span>
3. <span data-ttu-id="5693f-184">儲存 hello 頻寬範本。</span><span class="sxs-lookup"><span data-stu-id="5693f-184">Save hello bandwidth template.</span></span>

<span data-ttu-id="5693f-185">接著在您選擇的時間啟動並全天執行 hello 複合排程。</span><span class="sxs-lookup"><span data-stu-id="5693f-185">hello composite schedule will then start at a time of your choosing and run all-day.</span></span>

## <a name="questions-and-answers-about-bandwidth-templates"></a><span data-ttu-id="5693f-186">頻寬範本的相關問與答</span><span class="sxs-lookup"><span data-stu-id="5693f-186">Questions and answers about bandwidth templates</span></span>

<span data-ttu-id="5693f-187">**問：**</span><span class="sxs-lookup"><span data-stu-id="5693f-187">**Q**.</span></span> <span data-ttu-id="5693f-188">發生什麼事 toobandwidth 控制項 hello 排程之間會？</span><span class="sxs-lookup"><span data-stu-id="5693f-188">What happens toobandwidth controls when you are in between hello schedules?</span></span> <span data-ttu-id="5693f-189">(一個排程已結束而另一個排程尚未開始)。</span><span class="sxs-lookup"><span data-stu-id="5693f-189">(A schedule has ended and another one has not started yet.)</span></span>

<span data-ttu-id="5693f-190">**答：**</span><span class="sxs-lookup"><span data-stu-id="5693f-190">**A**.</span></span> <span data-ttu-id="5693f-191">在這種情況下，不會採用任何頻寬控制。</span><span class="sxs-lookup"><span data-stu-id="5693f-191">In such cases, no bandwidth controls will be employed.</span></span> <span data-ttu-id="5693f-192">這表示該 hello 裝置分層資料 toohello 雲端時，可以使用無限制的頻寬。</span><span class="sxs-lookup"><span data-stu-id="5693f-192">This means that hello device can use unlimited bandwidth when tiering data toohello cloud.</span></span>

<span data-ttu-id="5693f-193">**問：**</span><span class="sxs-lookup"><span data-stu-id="5693f-193">**Q**.</span></span> <span data-ttu-id="5693f-194">您是否可以修改離線裝置上的頻寬範本？</span><span class="sxs-lookup"><span data-stu-id="5693f-194">Can you modify bandwidth templates on an offline device?</span></span>

<span data-ttu-id="5693f-195">**答：**</span><span class="sxs-lookup"><span data-stu-id="5693f-195">**A**.</span></span> <span data-ttu-id="5693f-196">如果 hello 對應的裝置已離線，您將無法能 toomodify 磁碟區容器上的頻寬範本。</span><span class="sxs-lookup"><span data-stu-id="5693f-196">You will not be able toomodify bandwidth templates on volumes containers if hello corresponding device is offline.</span></span>

<span data-ttu-id="5693f-197">**問：**</span><span class="sxs-lookup"><span data-stu-id="5693f-197">**Q**.</span></span> <span data-ttu-id="5693f-198">您可以編輯 hello 相關聯的磁碟區離線時，與磁碟區容器相關聯的頻寬範本嗎？</span><span class="sxs-lookup"><span data-stu-id="5693f-198">Can you edit a bandwidth template associated with a volume container when hello associated volumes are offline?</span></span>

<span data-ttu-id="5693f-199">**答：**</span><span class="sxs-lookup"><span data-stu-id="5693f-199">**A**.</span></span> <span data-ttu-id="5693f-200">您可以修改和磁碟區已離線之磁碟區容器相關聯的頻寬範本。</span><span class="sxs-lookup"><span data-stu-id="5693f-200">You can modify a bandwidth template associated with a volume container whose volumes are offline.</span></span> <span data-ttu-id="5693f-201">請注意，當磁碟區離線，任何資料會分層從 hello 裝置 toohello 雲端。</span><span class="sxs-lookup"><span data-stu-id="5693f-201">Note that when volumes are offline, no data will be tiered from hello device toohello cloud.</span></span>

<span data-ttu-id="5693f-202">**問：**</span><span class="sxs-lookup"><span data-stu-id="5693f-202">**Q**.</span></span> <span data-ttu-id="5693f-203">您是否可以刪除預設範本？</span><span class="sxs-lookup"><span data-stu-id="5693f-203">Can you delete a default template?</span></span>

<span data-ttu-id="5693f-204">**答：**</span><span class="sxs-lookup"><span data-stu-id="5693f-204">**A**.</span></span> <span data-ttu-id="5693f-205">雖然您可以刪除預設範本，但它並不建議 toodo。</span><span class="sxs-lookup"><span data-stu-id="5693f-205">Although you can delete a default template, it is not a good idea toodo so.</span></span> <span data-ttu-id="5693f-206">hello 使用量的預設範本，包括已編輯的版本中，系統會追蹤。</span><span class="sxs-lookup"><span data-stu-id="5693f-206">hello usage of a default template, including edited versions, is tracked.</span></span> <span data-ttu-id="5693f-207">hello 追蹤資料分析，並透過 hello 課程中的時間，是使用的 tooimprove hello 預設範本。</span><span class="sxs-lookup"><span data-stu-id="5693f-207">hello tracking data is analyzed and over hello course of time, is used tooimprove hello default template.</span></span>

<span data-ttu-id="5693f-208">**問：**</span><span class="sxs-lookup"><span data-stu-id="5693f-208">**Q**.</span></span> <span data-ttu-id="5693f-209">如何判斷頻寬範本需要 toobe 修改？</span><span class="sxs-lookup"><span data-stu-id="5693f-209">How do you determine that your bandwidth templates need toobe modified?</span></span>

<span data-ttu-id="5693f-210">**答：**</span><span class="sxs-lookup"><span data-stu-id="5693f-210">**A**.</span></span> <span data-ttu-id="5693f-211">一開始時，您需要 toomodify hello 頻寬範本的徵兆的 hello 看見 hello 網路變慢或在一天多次阻礙。</span><span class="sxs-lookup"><span data-stu-id="5693f-211">One of hello signs that you need toomodify hello bandwidth templates is when you start seeing hello network slow down or choke multiple times in a day.</span></span> <span data-ttu-id="5693f-212">如果發生這種情況，請查看 hello I/O 效能及網路輸送量圖表監視 hello 儲存體和使用網路。</span><span class="sxs-lookup"><span data-stu-id="5693f-212">If this happens, monitor hello storage and usage network by looking at hello I/O Performance and Network Throughput charts.</span></span>

<span data-ttu-id="5693f-213">從 hello 網路輸送量資料中，找出 hello 一天的時間並 hello 中的 hello 網路瓶頸後，就會發生的磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="5693f-213">From hello network throughput data, identify hello time of day and hello volume containers in which hello network bottleneck occurs.</span></span> <span data-ttu-id="5693f-214">如果發生這種情況時資料分層式的 toohello 雲端 （取得這項資訊的所有磁碟區容器從 I/O 效能裝置 toocloud），則需要 toomodify hello 頻寬範本與磁碟區容器相關聯。</span><span class="sxs-lookup"><span data-stu-id="5693f-214">If this happens when data is being tiered toohello cloud (get this information from I/O performance for all volume containers for device toocloud), then you will need toomodify hello bandwidth templates associated with your volume containers.</span></span>

<span data-ttu-id="5693f-215">Hello 修改後範本正在使用中，您必須 toomonitor hello 網路一次無顯著的延遲。</span><span class="sxs-lookup"><span data-stu-id="5693f-215">After hello modified templates are in use, you will need toomonitor hello network again for significant latencies.</span></span> <span data-ttu-id="5693f-216">如果這些狀況仍存在，則您需要 toorevisit 頻寬範本。</span><span class="sxs-lookup"><span data-stu-id="5693f-216">If these still exist, then you will need toorevisit your bandwidth templates.</span></span>

<span data-ttu-id="5693f-217">**問：**</span><span class="sxs-lookup"><span data-stu-id="5693f-217">**Q**.</span></span> <span data-ttu-id="5693f-218">萬一我的裝置上的多個磁碟區容器有重疊的排程，但不同限制套用 tooeach 嗎？</span><span class="sxs-lookup"><span data-stu-id="5693f-218">What happens if multiple volume containers on my device have schedules that overlap but different limits apply tooeach?</span></span>

<span data-ttu-id="5693f-219">**答：**</span><span class="sxs-lookup"><span data-stu-id="5693f-219">**A**.</span></span> <span data-ttu-id="5693f-220">假設您的裝置有 3 個磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="5693f-220">Let's assume that you have a device with 3 volume containers.</span></span> <span data-ttu-id="5693f-221">hello 完全與這些容器相關聯的排程重疊。</span><span class="sxs-lookup"><span data-stu-id="5693f-221">hello schedules associated with these containers completely overlap.</span></span> <span data-ttu-id="5693f-222">針對每個容器，使用 hello 頻寬限制分別 5、 10 和 15 Mbps。</span><span class="sxs-lookup"><span data-stu-id="5693f-222">For each of these containers, hello bandwidth limits used are 5, 10, and 15 Mbps respectively.</span></span> <span data-ttu-id="5693f-223">當 I/O 所發生的所有可能套用相同的時間，hello 最小值為 hello 3 頻寬限制的 hello 在這些容器： 在此情況下，因此這些傳出 I/O 要求共用為 5 Mbps hello 相同的佇列。</span><span class="sxs-lookup"><span data-stu-id="5693f-223">When I/O are occurring on all of these containers at hello same time, hello minimum of hello 3 bandwidth limits may be applied: in this case, 5 Mbps as these outgoing I/O requests share hello same queue.</span></span>

## <a name="best-practices-for-bandwidth-templates"></a><span data-ttu-id="5693f-224">頻寬範本的最佳作法</span><span class="sxs-lookup"><span data-stu-id="5693f-224">Best practices for bandwidth templates</span></span>

<span data-ttu-id="5693f-225">請遵循 StorSimple 裝置的最佳作法：</span><span class="sxs-lookup"><span data-stu-id="5693f-225">Follow these best practices for your StorSimple device:</span></span>

* <span data-ttu-id="5693f-226">設定您裝置 tooenable 變數節流的 hello 網路輸送量 hello 裝置在 hello 每天不同時間的頻寬範本。</span><span class="sxs-lookup"><span data-stu-id="5693f-226">Configure bandwidth templates on your device tooenable variable throttling of hello network throughput by hello device at different times of hello day.</span></span> <span data-ttu-id="5693f-227">這些頻寬範本和備份排程搭配使用時，可以在離峰時段期間有效利用雲端作業的其他網路頻寬。</span><span class="sxs-lookup"><span data-stu-id="5693f-227">These bandwidth templates when used with backup schedules can effectively leverage additional network bandwidth for cloud operations during off-peak hours.</span></span>
* <span data-ttu-id="5693f-228">計算所需的基礎 hello 大小 hello 部署與 hello 所需的復原時間目標 (RTO) 的特定部署的 hello 實際頻寬。</span><span class="sxs-lookup"><span data-stu-id="5693f-228">Calculate hello actual bandwidth required for a particular deployment based on hello size of hello deployment and hello required recovery time objective (RTO).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5693f-229">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5693f-229">Next steps</span></span>

<span data-ttu-id="5693f-230">深入了解[使用您的 StorSimple 裝置 hello StorSimple 裝置管理員服務 tooadminister](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="5693f-230">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

