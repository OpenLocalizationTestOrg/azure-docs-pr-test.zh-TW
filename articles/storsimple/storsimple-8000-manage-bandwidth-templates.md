---
title: "管理 StorSimple 8000 系列的頻寬範本 | Microsoft Docs"
description: "描述如何管理可讓您控制頻寬耗用量的 StorSimple 頻寬範本。"
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
ms.openlocfilehash: 50d0a920bef097013feddc828d2c37133b9057b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-manage-storsimple-bandwidth-templates"></a><span data-ttu-id="30cb1-103">使用 StorSimple 裝置管理員服務管理 StorSimple 頻寬範本</span><span class="sxs-lookup"><span data-stu-id="30cb1-103">Use the StorSimple Device Manager service to manage StorSimple bandwidth templates</span></span>

## <a name="overview"></a><span data-ttu-id="30cb1-104">概觀</span><span class="sxs-lookup"><span data-stu-id="30cb1-104">Overview</span></span>

<span data-ttu-id="30cb1-105">頻寬範本可讓您設定多個日期時間排程的網路頻寬使用量，以將 StorSimple 裝置的資料分層至雲端。</span><span class="sxs-lookup"><span data-stu-id="30cb1-105">Bandwidth templates allow you to configure network bandwidth usage across multiple time-of-day schedules to tier the data from the StorSimple device to the cloud.</span></span>

<span data-ttu-id="30cb1-106">利用頻寬節流排程，您可以：</span><span class="sxs-lookup"><span data-stu-id="30cb1-106">With bandwidth throttling schedules you can:</span></span>

* <span data-ttu-id="30cb1-107">根據工作負載網路使用情況，指定自訂的頻寬排程。</span><span class="sxs-lookup"><span data-stu-id="30cb1-107">Specify customized bandwidth schedules depending on the workload network usages.</span></span>
* <span data-ttu-id="30cb1-108">集中管理，並且以簡單且順暢的方式跨多個裝置重複使用排程。</span><span class="sxs-lookup"><span data-stu-id="30cb1-108">Centralize management and reuse the schedules across multiple devices in an easy and seamless manner.</span></span>

> [!NOTE]
> <span data-ttu-id="30cb1-109">此功能僅適用於 StorSimple 實體裝置 (8100 和 8600 機型)，而不適用於 StorSimple 雲端設備 (8010 和 8020 機型)。</span><span class="sxs-lookup"><span data-stu-id="30cb1-109">This feature is available only for StorSimple physical devices (models 8100 and 8600) and not for StorSimple Cloud Appliances (models 8010 and 8020).</span></span>


## <a name="the-bandwidth-templates-blade"></a><span data-ttu-id="30cb1-110">[頻寬範本] 刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="30cb1-110">The Bandwidth templates blade</span></span>

<span data-ttu-id="30cb1-111">[頻寬範本] 刀鋒視窗會以表格格式顯示服務的所有頻寬範本，內含下列資訊：</span><span class="sxs-lookup"><span data-stu-id="30cb1-111">The **Bandwidth templates** blade has all the bandwidth templates for your service in a tabular format, and contains the following information:</span></span>

* <span data-ttu-id="30cb1-112">**名稱** – 在建立頻寬範本時，指派給頻寬範本的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="30cb1-112">**Name** – A unique name assigned to the bandwidth template when it was created.</span></span>
* <span data-ttu-id="30cb1-113">**排程** – 包含在給定頻寬範本中的排程數目。</span><span class="sxs-lookup"><span data-stu-id="30cb1-113">**Schedule** – The number of schedules contained in a given bandwidth template.</span></span>
* <span data-ttu-id="30cb1-114">**使用者** – 使用頻寬範本的磁碟區數目。</span><span class="sxs-lookup"><span data-stu-id="30cb1-114">**Used by** – The number of volumes using the bandwidth templates.</span></span>

<span data-ttu-id="30cb1-115">您也可以在下方找到協助設定頻寬範本的其他資訊：</span><span class="sxs-lookup"><span data-stu-id="30cb1-115">You can also find additional information to help configure bandwidth templates in:</span></span>

* [<span data-ttu-id="30cb1-116">頻寬範本的相關問與答</span><span class="sxs-lookup"><span data-stu-id="30cb1-116">Questions and answers about bandwidth templates</span></span>](#questions-and-answers-about-bandwidth-templates)
* [<span data-ttu-id="30cb1-117">頻寬範本的最佳作法</span><span class="sxs-lookup"><span data-stu-id="30cb1-117">Best practices for bandwidth templates</span></span>](#best-practices-for-bandwidth-templates)

## <a name="add-a-bandwidth-template"></a><span data-ttu-id="30cb1-118">新增頻寬範本</span><span class="sxs-lookup"><span data-stu-id="30cb1-118">Add a bandwidth template</span></span>

<span data-ttu-id="30cb1-119">執行下列步驟來建立新的頻寬範本。</span><span class="sxs-lookup"><span data-stu-id="30cb1-119">Perform the following steps to create a new bandwidth template.</span></span>

#### <a name="to-add-a-bandwidth-template"></a><span data-ttu-id="30cb1-120">新增頻寬範本</span><span class="sxs-lookup"><span data-stu-id="30cb1-120">To add a bandwidth template</span></span>

1. <span data-ttu-id="30cb1-121">移至 StorSimple 裝置管理員服務，按一下 [頻寬範本]，然後按一下 [+ 新增頻寬範本]。</span><span class="sxs-lookup"><span data-stu-id="30cb1-121">Go to your StorSimple Device Manager service, click **Bandwidth templates** and then click **+ Add Bandwidth template**.</span></span>

    ![按一下 [+ 新增頻寬範本]](./media/storsimple-8000-manage-bandwidth-templates/addbwtemp1.png)

2. <span data-ttu-id="30cb1-123">在 [新增頻寬範本] 刀鋒視窗中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="30cb1-123">In the **Add bandwidth template** blade, do the following steps:</span></span>
   
    1. <span data-ttu-id="30cb1-124">為頻寬範本指定唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="30cb1-124">Specify a unique name for your bandwidth template.</span></span>
    2. <span data-ttu-id="30cb1-125">定義頻寬排程。</span><span class="sxs-lookup"><span data-stu-id="30cb1-125">Define a bandwidth schedule.</span></span> <span data-ttu-id="30cb1-126">建立排程：</span><span class="sxs-lookup"><span data-stu-id="30cb1-126">To create a schedule:</span></span>
   
        1. <span data-ttu-id="30cb1-127">從下拉式清單中，選擇排程要設定為該週的哪幾個**日期**。</span><span class="sxs-lookup"><span data-stu-id="30cb1-127">From the drop-down list, choose the **Days** of the week the schedule is configured for.</span></span> <span data-ttu-id="30cb1-128">您可以選取多天。</span><span class="sxs-lookup"><span data-stu-id="30cb1-128">You can select multiple days.</span></span>        
        
        2. <span data-ttu-id="30cb1-129">輸入 [開始時間]，格式為 _hh:mm_。</span><span class="sxs-lookup"><span data-stu-id="30cb1-129">Enter a **Start Time** in _hh:mm_ format.</span></span> <span data-ttu-id="30cb1-130">這就是排程開始的時間。</span><span class="sxs-lookup"><span data-stu-id="30cb1-130">This is when the schedule will begin.</span></span>

        3. <span data-ttu-id="30cb1-131">輸入 [結束時間]，格式為 _hh:mm_。</span><span class="sxs-lookup"><span data-stu-id="30cb1-131">Enter an **End Time** in _hh:mm_ format.</span></span> <span data-ttu-id="30cb1-132">這就是排程結束的時間。</span><span class="sxs-lookup"><span data-stu-id="30cb1-132">This is when the schedule will stop.</span></span>
      
           > [!NOTE]
           > <span data-ttu-id="30cb1-133">不允許重疊的排程。</span><span class="sxs-lookup"><span data-stu-id="30cb1-133">Overlapping schedules are not allowed.</span></span> <span data-ttu-id="30cb1-134">如果開始和結束時間會產生重疊排程，您會看到錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="30cb1-134">If the start and end times will result in an overlapping schedule, you will see an error message to that effect.</span></span>

        4. <span data-ttu-id="30cb1-135">指定 **頻寬速率**。</span><span class="sxs-lookup"><span data-stu-id="30cb1-135">Specify the **Bandwidth Rate**.</span></span> <span data-ttu-id="30cb1-136">這是以 MB / 秒 (Mbps) 為單位的頻寬，由包含雲端之作業中 (上傳與下載) 的 StorSimple 裝置所使用。</span><span class="sxs-lookup"><span data-stu-id="30cb1-136">This is the bandwidth in Megabits per second (Mbps) used by your StorSimple device in operations involving the cloud (both uploads and downloads).</span></span> <span data-ttu-id="30cb1-137">提供一個介於 1 到 1000 之間的數目給此欄位。</span><span class="sxs-lookup"><span data-stu-id="30cb1-137">Supply a number between 1 and 1,000 for this field.</span></span>

            ![定義頻寬排程](./media/storsimple-8000-manage-bandwidth-templates/addbwtemp2.png)
         
            <span data-ttu-id="30cb1-139">重複上述步驟，為範本定義排程，直到完成為止。</span><span class="sxs-lookup"><span data-stu-id="30cb1-139">Repeat the above steps to define multiple schedules for your template until you are done.</span></span>

        5. <span data-ttu-id="30cb1-140">按一下 [新增]，開始建立頻寬範本。</span><span class="sxs-lookup"><span data-stu-id="30cb1-140">Click **Add** to start creating a bandwidth template.</span></span> <span data-ttu-id="30cb1-141">建立的範本會加入頻寬範本的清單。</span><span class="sxs-lookup"><span data-stu-id="30cb1-141">The created template is added to the list of bandwidth templates.</span></span>
      

## <a name="edit-a-bandwidth-template"></a><span data-ttu-id="30cb1-142">編輯頻寬範本</span><span class="sxs-lookup"><span data-stu-id="30cb1-142">Edit a bandwidth template</span></span>

<span data-ttu-id="30cb1-143">執行下列步驟來編輯頻寬範本。</span><span class="sxs-lookup"><span data-stu-id="30cb1-143">Perform the following steps to edit a bandwidth template.</span></span>

### <a name="to-edit-a-bandwidth-template"></a><span data-ttu-id="30cb1-144">編輯頻寬範本</span><span class="sxs-lookup"><span data-stu-id="30cb1-144">To edit a bandwidth template</span></span>

1. <span data-ttu-id="30cb1-145">移至 StorSimple 裝置管理員服務，然後按一下 [頻寬範本]。</span><span class="sxs-lookup"><span data-stu-id="30cb1-145">Go to your StorSimple Device Manager service and click **Bandwidth templates**.</span></span>
2. <span data-ttu-id="30cb1-146">在頻寬範本清單中，選取您想要刪除的範本。</span><span class="sxs-lookup"><span data-stu-id="30cb1-146">In the list of bandwidth templates, select the template you wish to delete.</span></span> <span data-ttu-id="30cb1-147">以滑鼠右鍵按一下，然後從內容功能表中選取 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="30cb1-147">Right-click and from the context menu, select **Delete**.</span></span>
3. <span data-ttu-id="30cb1-148">系統提示您進行確認時，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="30cb1-148">When prompted for confirmation, click **OK**.</span></span> <span data-ttu-id="30cb1-149">如此即會刪除頻寬範本。</span><span class="sxs-lookup"><span data-stu-id="30cb1-149">This should delete the bandwidth template.</span></span> 
4. <span data-ttu-id="30cb1-150">頻寬範本清單會一併更新以反映刪除。</span><span class="sxs-lookup"><span data-stu-id="30cb1-150">The list of bandwidth templates updates to reflect the deletion.</span></span>

> [!NOTE]
> <span data-ttu-id="30cb1-151">如果已編輯的排程和您要修改之頻寬範本中現有的排程重疊，您無法儲存變更。</span><span class="sxs-lookup"><span data-stu-id="30cb1-151">You cannot save your changes if the edited schedule overlaps with an existing schedule in the bandwidth template that you are modifying.</span></span>

## <a name="delete-a-bandwidth-template"></a><span data-ttu-id="30cb1-152">刪除頻寬範本</span><span class="sxs-lookup"><span data-stu-id="30cb1-152">Delete a bandwidth template</span></span>

<span data-ttu-id="30cb1-153">執行下列步驟來刪除頻寬範本。</span><span class="sxs-lookup"><span data-stu-id="30cb1-153">Perform the following steps to delete a bandwidth template.</span></span>

#### <a name="to-delete-a-bandwidth-template"></a><span data-ttu-id="30cb1-154">刪除頻寬範本</span><span class="sxs-lookup"><span data-stu-id="30cb1-154">To delete a bandwidth template</span></span>

1. <span data-ttu-id="30cb1-155">移至 StorSimple 裝置管理員服務，然後按一下 [頻寬範本]。</span><span class="sxs-lookup"><span data-stu-id="30cb1-155">Go to your StorSimple Device Manager service and click **Bandwidth templates**.</span></span>
2. <span data-ttu-id="30cb1-156">在頻寬範本清單中，選取您想要刪除的範本。</span><span class="sxs-lookup"><span data-stu-id="30cb1-156">In the list of bandwidth templates, select the template you wish to delete.</span></span> <span data-ttu-id="30cb1-157">以滑鼠右鍵按一下，然後從操作功能表中選取 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="30cb1-157">Right-click and from the context menu, select Delete.</span></span>
3. <span data-ttu-id="30cb1-158">系統提示您進行確認時，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="30cb1-158">When prompted for confirmation, click **OK**.</span></span> <span data-ttu-id="30cb1-159">如此即會刪除頻寬範本。</span><span class="sxs-lookup"><span data-stu-id="30cb1-159">This should delete the bandwidth template.</span></span>
4. <span data-ttu-id="30cb1-160">頻寬範本清單會一併更新以反映刪除。</span><span class="sxs-lookup"><span data-stu-id="30cb1-160">The list of bandwidth templates updates to reflect the deletion.</span></span>

<span data-ttu-id="30cb1-161">如果有任何磁碟區正在使用範本，您就無法將它刪除。</span><span class="sxs-lookup"><span data-stu-id="30cb1-161">If the template is in use by any volume(s), you will not be allowed to delete it.</span></span> <span data-ttu-id="30cb1-162">您會看到錯誤訊息，指出此範本正在使用中。</span><span class="sxs-lookup"><span data-stu-id="30cb1-162">You will see an error message indicating that the template is in use.</span></span> <span data-ttu-id="30cb1-163">錯誤訊息對話方塊會隨即出現，建議您移除範本的所有參考。</span><span class="sxs-lookup"><span data-stu-id="30cb1-163">An error message dialog box will appear advising you that all the references to the template should be removed.</span></span>

<span data-ttu-id="30cb1-164">您可以藉由存取 [ **磁碟區容器** ] 頁面和修改使用此範本的磁碟區容器，以刪除該範本的所有參考，讓它們使用另一個範本，或使用自訂或無限制頻寬設定。</span><span class="sxs-lookup"><span data-stu-id="30cb1-164">You can delete all the references to the template by accessing the **Volume Containers** page and modifying the volume containers that use this template so that they use another template or use a custom or unlimited bandwidth setting.</span></span> <span data-ttu-id="30cb1-165">移除所有參考時，您就可以刪除範本。</span><span class="sxs-lookup"><span data-stu-id="30cb1-165">When all the references have been removed, you can delete the template.</span></span>

## <a name="use-a-default-bandwidth-template"></a><span data-ttu-id="30cb1-166">使用預設頻寬範本</span><span class="sxs-lookup"><span data-stu-id="30cb1-166">Use a default bandwidth template</span></span>

<span data-ttu-id="30cb1-167">預設的頻寬範本可由磁碟區容器提供及使用，根據預設，可在存取雲端時強制執行頻寬控制。</span><span class="sxs-lookup"><span data-stu-id="30cb1-167">A default bandwidth template is provided and is used by volume containers by default to enforce bandwidth controls when accessing the cloud.</span></span> <span data-ttu-id="30cb1-168">預設範本也可讓建立自己範本的使用者當做準備參考。</span><span class="sxs-lookup"><span data-stu-id="30cb1-168">The default template also serves as a ready reference for users who create their own templates.</span></span> <span data-ttu-id="30cb1-169">這個預設範本的詳細資料如下：</span><span class="sxs-lookup"><span data-stu-id="30cb1-169">The details of this default template are:</span></span>

* <span data-ttu-id="30cb1-170">**名稱** – 不限制夜間和週末</span><span class="sxs-lookup"><span data-stu-id="30cb1-170">**Name** – Unlimited nights and weekends</span></span>
* <span data-ttu-id="30cb1-171">**排程** – 從星期一至星期五的單一排程，在 8 AM 和 5 PM 的裝置時間之間套用 1 Mbps 的頻寬速率。</span><span class="sxs-lookup"><span data-stu-id="30cb1-171">**Schedule** – A single schedule from Monday to Friday that applies a bandwidth rate of 1 Mbps between 8 AM and 5 PM device time.</span></span> <span data-ttu-id="30cb1-172">一週中的其餘部分之頻寬設定為無限制。</span><span class="sxs-lookup"><span data-stu-id="30cb1-172">The bandwidth is set to Unlimited for the remainder of the week.</span></span>

<span data-ttu-id="30cb1-173">預設範本可供編輯。</span><span class="sxs-lookup"><span data-stu-id="30cb1-173">The default template can be edited.</span></span> <span data-ttu-id="30cb1-174">追蹤此範本 (包括編輯的版本) 的使用方式。</span><span class="sxs-lookup"><span data-stu-id="30cb1-174">The usage of this template (including edited versions) is tracked.</span></span>

## <a name="create-an-all-day-bandwidth-template-that-starts-at-a-specified-time"></a><span data-ttu-id="30cb1-175">建立在指定時間啟動的全天頻寬範本</span><span class="sxs-lookup"><span data-stu-id="30cb1-175">Create an all-day bandwidth template that starts at a specified time</span></span>

<span data-ttu-id="30cb1-176">請遵循此程序來建立可在指定時間啟動並執行全天的排程。</span><span class="sxs-lookup"><span data-stu-id="30cb1-176">Follow this procedure to create a schedule that starts at a specified time and runs all day.</span></span> <span data-ttu-id="30cb1-177">在此範例中，排程從早上 9 AM 開始，並執行到隔天早上的 9 AM。</span><span class="sxs-lookup"><span data-stu-id="30cb1-177">In the example, the schedule starts at 9 AM in the morning and runs until 9 AM the next morning.</span></span> <span data-ttu-id="30cb1-178">請務必注意，給定排程的開始和結束時間都必須包含在相同的 24 小時排程，且不能跨越多天。</span><span class="sxs-lookup"><span data-stu-id="30cb1-178">It's important to note that the start and end times for a given schedule must both be contained on the same 24 hour schedule and cannot span multiple days.</span></span> <span data-ttu-id="30cb1-179">如果您必須設定跨越多天的頻寬範本，您必須使用多個排程 (如範例所示)。</span><span class="sxs-lookup"><span data-stu-id="30cb1-179">If you need to set up bandwidth templates that span multiple days, you will need to use multiple schedules (as shown in the example).</span></span>

#### <a name="to-create-an-all-day-bandwidth-template"></a><span data-ttu-id="30cb1-180">建立全天頻寬範本</span><span class="sxs-lookup"><span data-stu-id="30cb1-180">To create an all-day bandwidth template</span></span>

1. <span data-ttu-id="30cb1-181">建立從 9 AM 開始並執行到午夜的排程。</span><span class="sxs-lookup"><span data-stu-id="30cb1-181">Create a schedule that starts at 9 AM in the morning and runs until midnight.</span></span>
2. <span data-ttu-id="30cb1-182">新增另一個排程。</span><span class="sxs-lookup"><span data-stu-id="30cb1-182">Add another schedule.</span></span> <span data-ttu-id="30cb1-183">設定第二個排程從午夜執行到早上 9 AM。</span><span class="sxs-lookup"><span data-stu-id="30cb1-183">Configure the second schedule to run from midnight until 9 AM in the morning.</span></span>
3. <span data-ttu-id="30cb1-184">儲存頻寬範本</span><span class="sxs-lookup"><span data-stu-id="30cb1-184">Save the bandwidth template.</span></span>

<span data-ttu-id="30cb1-185">複合排程會從您選擇的時間開始並且全天執行。</span><span class="sxs-lookup"><span data-stu-id="30cb1-185">The composite schedule will then start at a time of your choosing and run all-day.</span></span>

## <a name="questions-and-answers-about-bandwidth-templates"></a><span data-ttu-id="30cb1-186">頻寬範本的相關問與答</span><span class="sxs-lookup"><span data-stu-id="30cb1-186">Questions and answers about bandwidth templates</span></span>

<span data-ttu-id="30cb1-187">**問：**</span><span class="sxs-lookup"><span data-stu-id="30cb1-187">**Q**.</span></span> <span data-ttu-id="30cb1-188">當您在排程之間時，頻寬控制會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="30cb1-188">What happens to bandwidth controls when you are in between the schedules?</span></span> <span data-ttu-id="30cb1-189">(一個排程已結束而另一個排程尚未開始)。</span><span class="sxs-lookup"><span data-stu-id="30cb1-189">(A schedule has ended and another one has not started yet.)</span></span>

<span data-ttu-id="30cb1-190">**答：**</span><span class="sxs-lookup"><span data-stu-id="30cb1-190">**A**.</span></span> <span data-ttu-id="30cb1-191">在這種情況下，不會採用任何頻寬控制。</span><span class="sxs-lookup"><span data-stu-id="30cb1-191">In such cases, no bandwidth controls will be employed.</span></span> <span data-ttu-id="30cb1-192">這表示將資料分層至雲端時，裝置可以使用無限制的頻寬。</span><span class="sxs-lookup"><span data-stu-id="30cb1-192">This means that the device can use unlimited bandwidth when tiering data to the cloud.</span></span>

<span data-ttu-id="30cb1-193">**問：**</span><span class="sxs-lookup"><span data-stu-id="30cb1-193">**Q**.</span></span> <span data-ttu-id="30cb1-194">您是否可以修改離線裝置上的頻寬範本？</span><span class="sxs-lookup"><span data-stu-id="30cb1-194">Can you modify bandwidth templates on an offline device?</span></span>

<span data-ttu-id="30cb1-195">**答：**</span><span class="sxs-lookup"><span data-stu-id="30cb1-195">**A**.</span></span> <span data-ttu-id="30cb1-196">如果對應的裝置已離線，您無法修改磁碟區容器上的頻寬範本。</span><span class="sxs-lookup"><span data-stu-id="30cb1-196">You will not be able to modify bandwidth templates on volumes containers if the corresponding device is offline.</span></span>

<span data-ttu-id="30cb1-197">**問：**</span><span class="sxs-lookup"><span data-stu-id="30cb1-197">**Q**.</span></span> <span data-ttu-id="30cb1-198">您是否可以在相關聯的磁碟區離線時，編輯和磁碟區容器相關聯的頻寬範本？</span><span class="sxs-lookup"><span data-stu-id="30cb1-198">Can you edit a bandwidth template associated with a volume container when the associated volumes are offline?</span></span>

<span data-ttu-id="30cb1-199">**答：**</span><span class="sxs-lookup"><span data-stu-id="30cb1-199">**A**.</span></span> <span data-ttu-id="30cb1-200">您可以修改和磁碟區已離線之磁碟區容器相關聯的頻寬範本。</span><span class="sxs-lookup"><span data-stu-id="30cb1-200">You can modify a bandwidth template associated with a volume container whose volumes are offline.</span></span> <span data-ttu-id="30cb1-201">請注意，當磁碟區離線時，沒有資料會從裝置分層至雲端。</span><span class="sxs-lookup"><span data-stu-id="30cb1-201">Note that when volumes are offline, no data will be tiered from the device to the cloud.</span></span>

<span data-ttu-id="30cb1-202">**問：**</span><span class="sxs-lookup"><span data-stu-id="30cb1-202">**Q**.</span></span> <span data-ttu-id="30cb1-203">您是否可以刪除預設範本？</span><span class="sxs-lookup"><span data-stu-id="30cb1-203">Can you delete a default template?</span></span>

<span data-ttu-id="30cb1-204">**答：**</span><span class="sxs-lookup"><span data-stu-id="30cb1-204">**A**.</span></span> <span data-ttu-id="30cb1-205">雖然您可以刪除預設範本，但這並不是個好主意。</span><span class="sxs-lookup"><span data-stu-id="30cb1-205">Although you can delete a default template, it is not a good idea to do so.</span></span> <span data-ttu-id="30cb1-206">已追蹤此預設範本 (包括已編輯版本) 的使用方式。</span><span class="sxs-lookup"><span data-stu-id="30cb1-206">The usage of a default template, including edited versions, is tracked.</span></span> <span data-ttu-id="30cb1-207">追蹤資料已進行分析，並在時間過程中用來改善預設範本。</span><span class="sxs-lookup"><span data-stu-id="30cb1-207">The tracking data is analyzed and over the course of time, is used to improve the default template.</span></span>

<span data-ttu-id="30cb1-208">**問：**</span><span class="sxs-lookup"><span data-stu-id="30cb1-208">**Q**.</span></span> <span data-ttu-id="30cb1-209">如何判斷頻寬範本必須修改？</span><span class="sxs-lookup"><span data-stu-id="30cb1-209">How do you determine that your bandwidth templates need to be modified?</span></span>

<span data-ttu-id="30cb1-210">**答：**</span><span class="sxs-lookup"><span data-stu-id="30cb1-210">**A**.</span></span> <span data-ttu-id="30cb1-211">您必須修改頻寬範本的其中一個徵兆是您會開始看到網路變慢，或在一天中多次停擺。</span><span class="sxs-lookup"><span data-stu-id="30cb1-211">One of the signs that you need to modify the bandwidth templates is when you start seeing the network slow down or choke multiple times in a day.</span></span> <span data-ttu-id="30cb1-212">如果發生這種情況，請查看 I/O 效能及網路輸送量圖表來監視儲存體和使用方式的網路。</span><span class="sxs-lookup"><span data-stu-id="30cb1-212">If this happens, monitor the storage and usage network by looking at the I/O Performance and Network Throughput charts.</span></span>

<span data-ttu-id="30cb1-213">從網路輸送量資料，找出發生網路瓶頸的日期時間與磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="30cb1-213">From the network throughput data, identify the time of day and the volume containers in which the network bottleneck occurs.</span></span> <span data-ttu-id="30cb1-214">如果在資料分層至雲端時發生這種情況 (可由裝置至雲端的所有磁碟區容器之 I/O 效能取得此資訊)，您必須修改和磁碟區容器相關聯的頻寬範本。</span><span class="sxs-lookup"><span data-stu-id="30cb1-214">If this happens when data is being tiered to the cloud (get this information from I/O performance for all volume containers for device to cloud), then you will need to modify the bandwidth templates associated with your volume containers.</span></span>

<span data-ttu-id="30cb1-215">開始使用已修改的範本之後，您必須再次監視網路是否有顯著的延遲。</span><span class="sxs-lookup"><span data-stu-id="30cb1-215">After the modified templates are in use, you will need to monitor the network again for significant latencies.</span></span> <span data-ttu-id="30cb1-216">如果仍然存在延遲，您必須返回頻寬範本。</span><span class="sxs-lookup"><span data-stu-id="30cb1-216">If these still exist, then you will need to revisit your bandwidth templates.</span></span>

<span data-ttu-id="30cb1-217">**問：**</span><span class="sxs-lookup"><span data-stu-id="30cb1-217">**Q**.</span></span> <span data-ttu-id="30cb1-218">要是裝置上多個磁碟區容器的排程重疊，但是每個排程都套用不同的限制會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="30cb1-218">What happens if multiple volume containers on my device have schedules that overlap but different limits apply to each?</span></span>

<span data-ttu-id="30cb1-219">**答：**</span><span class="sxs-lookup"><span data-stu-id="30cb1-219">**A**.</span></span> <span data-ttu-id="30cb1-220">假設您的裝置有 3 個磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="30cb1-220">Let's assume that you have a device with 3 volume containers.</span></span> <span data-ttu-id="30cb1-221">與這些容器相關聯的排程完全重疊。</span><span class="sxs-lookup"><span data-stu-id="30cb1-221">The schedules associated with these containers completely overlap.</span></span> <span data-ttu-id="30cb1-222">針對每個容器，分別使用 5、10 和 15 Mbps 的頻寬限制。</span><span class="sxs-lookup"><span data-stu-id="30cb1-222">For each of these containers, the bandwidth limits used are 5, 10, and 15 Mbps respectively.</span></span> <span data-ttu-id="30cb1-223">當所有容器都同時出現 I/O 時，可能會套用 3 個頻寬限制中的最小值：5 Mbps，因為在此情況下，這些傳出 I/O 要求會共用相同的佇列。</span><span class="sxs-lookup"><span data-stu-id="30cb1-223">When I/O are occurring on all of these containers at the same time, the minimum of the 3 bandwidth limits may be applied: in this case, 5 Mbps as these outgoing I/O requests share the same queue.</span></span>

## <a name="best-practices-for-bandwidth-templates"></a><span data-ttu-id="30cb1-224">頻寬範本的最佳作法</span><span class="sxs-lookup"><span data-stu-id="30cb1-224">Best practices for bandwidth templates</span></span>

<span data-ttu-id="30cb1-225">請遵循 StorSimple 裝置的最佳作法：</span><span class="sxs-lookup"><span data-stu-id="30cb1-225">Follow these best practices for your StorSimple device:</span></span>

* <span data-ttu-id="30cb1-226">在裝置上設定頻寬範本，以根據裝置在一天中的不同時間，啟用網路傳輸量的變數節流。</span><span class="sxs-lookup"><span data-stu-id="30cb1-226">Configure bandwidth templates on your device to enable variable throttling of the network throughput by the device at different times of the day.</span></span> <span data-ttu-id="30cb1-227">這些頻寬範本和備份排程搭配使用時，可以在離峰時段期間有效利用雲端作業的其他網路頻寬。</span><span class="sxs-lookup"><span data-stu-id="30cb1-227">These bandwidth templates when used with backup schedules can effectively leverage additional network bandwidth for cloud operations during off-peak hours.</span></span>
* <span data-ttu-id="30cb1-228">根據部署的大小和所需的復原時間目標 (RTO)，計算特定部署所需的實際頻寬。</span><span class="sxs-lookup"><span data-stu-id="30cb1-228">Calculate the actual bandwidth required for a particular deployment based on the size of the deployment and the required recovery time objective (RTO).</span></span>

## <a name="next-steps"></a><span data-ttu-id="30cb1-229">後續步驟</span><span class="sxs-lookup"><span data-stu-id="30cb1-229">Next steps</span></span>

<span data-ttu-id="30cb1-230">深入了解[使用 StorSimple 裝置管理員服務管理 StorSimple 裝置](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="30cb1-230">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

