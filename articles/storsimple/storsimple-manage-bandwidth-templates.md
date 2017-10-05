---
title: "管理您的 StorSimple 頻寬範本 | Microsoft Docs"
description: "描述如何管理可讓您控制頻寬耗用量的 StorSimple 頻寬範本。"
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
ms.openlocfilehash: df3ae8bf775370432b3648459a7c942afe69fb17
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-storsimple-bandwidth-templates"></a><span data-ttu-id="5325d-103">使用 StorSimple Manager 服務管理 StorSimple 頻寬範本</span><span class="sxs-lookup"><span data-stu-id="5325d-103">Use the StorSimple Manager service to manage StorSimple bandwidth templates</span></span>
## <a name="overview"></a><span data-ttu-id="5325d-104">Overview</span><span class="sxs-lookup"><span data-stu-id="5325d-104">Overview</span></span>
<span data-ttu-id="5325d-105">頻寬範本可讓您設定多個日期時間排程的網路頻寬使用量，以將 StorSimple 裝置的資料分層至雲端。</span><span class="sxs-lookup"><span data-stu-id="5325d-105">Bandwidth templates allow you to configure network bandwidth usage across multiple time-of-day schedules to tier the data from the StorSimple device to the cloud.</span></span>

<span data-ttu-id="5325d-106">利用頻寬節流排程，您可以：</span><span class="sxs-lookup"><span data-stu-id="5325d-106">With bandwidth throttling schedules you can:</span></span>

* <span data-ttu-id="5325d-107">根據工作負載網路使用情況，指定自訂的頻寬排程。</span><span class="sxs-lookup"><span data-stu-id="5325d-107">Specify customized bandwidth schedules depending on the workload network usages.</span></span>
* <span data-ttu-id="5325d-108">集中管理，並且以簡單且順暢的方式跨多個裝置重複使用排程。</span><span class="sxs-lookup"><span data-stu-id="5325d-108">Centralize management and reuse the schedules across multiple devices in an easy and seamless manner.</span></span>

> [!NOTE]
> <span data-ttu-id="5325d-109">這項功能只可供 StorSimple 實體裝置使用，不能用於虛擬裝置。</span><span class="sxs-lookup"><span data-stu-id="5325d-109">This feature is available only for StorSimple physical devices and not for virtual devices.</span></span>
> 
> 

<span data-ttu-id="5325d-110">服務的所有頻寬範本會以表格格式顯示，並包含下列資訊：</span><span class="sxs-lookup"><span data-stu-id="5325d-110">All the bandwidth templates for your service are displayed in a tabular format, and contain the following information:</span></span>

* <span data-ttu-id="5325d-111">**名稱** – 在建立頻寬範本時，指派給頻寬範本的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="5325d-111">**Name** – A unique name assigned to the bandwidth template when it was created.</span></span>
* <span data-ttu-id="5325d-112">**排程** – 包含在給定頻寬範本中的排程數目。</span><span class="sxs-lookup"><span data-stu-id="5325d-112">**Schedule** – The number of schedules contained in a given bandwidth template.</span></span>
* <span data-ttu-id="5325d-113">**使用者** – 使用頻寬範本的磁碟區數目。</span><span class="sxs-lookup"><span data-stu-id="5325d-113">**Used by** – The number of volumes using the bandwidth templates.</span></span>

<span data-ttu-id="5325d-114">您使用 Azure 傳統入口網站中的 StorSimple Manager 服務 [設定]  頁面管理頻寬範本。</span><span class="sxs-lookup"><span data-stu-id="5325d-114">You use the StorSimple Manager service **Configure** page in the Azure classic portal to manage bandwidth templates.</span></span>

<span data-ttu-id="5325d-115">您也可以在下方找到協助設定頻寬範本的其他資訊：</span><span class="sxs-lookup"><span data-stu-id="5325d-115">You can also find additional information to help configure bandwidth templates in:</span></span>

* <span data-ttu-id="5325d-116">頻寬範本的相關問與答</span><span class="sxs-lookup"><span data-stu-id="5325d-116">Questions and answers about bandwidth templates</span></span>
* <span data-ttu-id="5325d-117">頻寬範本的最佳作法</span><span class="sxs-lookup"><span data-stu-id="5325d-117">Best practices for bandwidth templates</span></span>

## <a name="add-a-bandwidth-template"></a><span data-ttu-id="5325d-118">新增頻寬範本</span><span class="sxs-lookup"><span data-stu-id="5325d-118">Add a bandwidth template</span></span>
<span data-ttu-id="5325d-119">執行下列步驟來建立新的頻寬範本。</span><span class="sxs-lookup"><span data-stu-id="5325d-119">Perform the following steps to create a new bandwidth template.</span></span>

#### <a name="to-add-a-bandwidth-template"></a><span data-ttu-id="5325d-120">新增頻寬範本</span><span class="sxs-lookup"><span data-stu-id="5325d-120">To add a bandwidth template</span></span>
1. <span data-ttu-id="5325d-121">在 StorSimple Manager 服務的 [設定] 頁面上，按一下 [加入/編輯頻寬範本]。</span><span class="sxs-lookup"><span data-stu-id="5325d-121">On the StorSimple Manager service **Configure** page, click **add/edit bandwidth template**.</span></span>
2. <span data-ttu-id="5325d-122">在 [ **新增/編輯頻寬範本** ] 對話方塊中：</span><span class="sxs-lookup"><span data-stu-id="5325d-122">In the **Add/Edit Bandwidth Template** dialog box:</span></span>
   
   1. <span data-ttu-id="5325d-123">從 [範本] 下拉式清單中，選取 [建立新的] 以新增頻寬範本。</span><span class="sxs-lookup"><span data-stu-id="5325d-123">From the **Template** drop-down list, select **Create new** to add a new bandwidth template.</span></span>
   2. <span data-ttu-id="5325d-124">為頻寬範本指定唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="5325d-124">Specify a unique name for your bandwidth template.</span></span>
3. <span data-ttu-id="5325d-125">定義 **頻寬排程**。</span><span class="sxs-lookup"><span data-stu-id="5325d-125">Define a **Bandwidth Schedule**.</span></span> <span data-ttu-id="5325d-126">建立排程：</span><span class="sxs-lookup"><span data-stu-id="5325d-126">To create a schedule:</span></span>
   
   1. <span data-ttu-id="5325d-127">從下拉式清單中，選擇排程要設定為該週的哪幾天。</span><span class="sxs-lookup"><span data-stu-id="5325d-127">From the drop-down list, choose the days of the week the schedule is configured for.</span></span> <span data-ttu-id="5325d-128">您可以選取位於清單中個別天之前的核取方塊，以選取多天。</span><span class="sxs-lookup"><span data-stu-id="5325d-128">You can select multiple days by selecting the check boxes located before the respective days in the list.</span></span>
   2. <span data-ttu-id="5325d-129">如果排程會強制執行全天，請選取 [ **整天** ] 選項。</span><span class="sxs-lookup"><span data-stu-id="5325d-129">Select the **All Day** option if the schedule is enforced for the entire day.</span></span> <span data-ttu-id="5325d-130">核取此選項時，您無法再指定 [開始時間] 或 [結束時間]。</span><span class="sxs-lookup"><span data-stu-id="5325d-130">When this option is checked, you can no longer specify a **Start Time** or an **End Time**.</span></span> <span data-ttu-id="5325d-131">排程執行時間從 12:00 AM 到 11:59 PM。</span><span class="sxs-lookup"><span data-stu-id="5325d-131">The schedule runs from 12:00 AM to 11:59 PM.</span></span>
   3. <span data-ttu-id="5325d-132">從下拉式清單中，選取 [ **開始時間**]。</span><span class="sxs-lookup"><span data-stu-id="5325d-132">From the drop-down list, select a **Start Time**.</span></span> <span data-ttu-id="5325d-133">這就是排程開始的時間。</span><span class="sxs-lookup"><span data-stu-id="5325d-133">This is when the schedule will begin.</span></span>
   4. <span data-ttu-id="5325d-134">從下拉式清單中，選取 [ **結束時間**]。</span><span class="sxs-lookup"><span data-stu-id="5325d-134">From the drop-down list, select an **End Time**.</span></span> <span data-ttu-id="5325d-135">這就是排程結束的時間。</span><span class="sxs-lookup"><span data-stu-id="5325d-135">This is when the schedule will stop.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="5325d-136">不允許重疊的排程。</span><span class="sxs-lookup"><span data-stu-id="5325d-136">Overlapping schedules are not allowed.</span></span> <span data-ttu-id="5325d-137">如果開始和結束時間會產生重疊排程，您會看到錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="5325d-137">If the start and end times will result in an overlapping schedule, you will see an error message to that effect.</span></span>
      > 
      > 
   5. <span data-ttu-id="5325d-138">指定 **頻寬速率**。</span><span class="sxs-lookup"><span data-stu-id="5325d-138">Specify the **Bandwidth Rate**.</span></span> <span data-ttu-id="5325d-139">這是以 MB / 秒 (Mbps) 為單位的頻寬，由包含雲端之作業中 (上傳與下載) 的 StorSimple 裝置所使用。</span><span class="sxs-lookup"><span data-stu-id="5325d-139">This is the bandwidth in Megabits per second (Mbps) used by your StorSimple device in operations involving the cloud (both uploads and downloads).</span></span> <span data-ttu-id="5325d-140">提供一個介於 1 到 1000 之間的數目給此欄位。</span><span class="sxs-lookup"><span data-stu-id="5325d-140">Supply a number between 1 and 1,000 for this field.</span></span>
   6. <span data-ttu-id="5325d-141">按一下核取圖示 ![核取圖示](./media/storsimple-manage-bandwidth-templates/HCS_CheckIcon.png)。</span><span class="sxs-lookup"><span data-stu-id="5325d-141">Click the check icon ![Check icon](./media/storsimple-manage-bandwidth-templates/HCS_CheckIcon.png).</span></span> <span data-ttu-id="5325d-142">您已建立的範本會新增至服務 **設定** 頁面上的頻寬範本清單。</span><span class="sxs-lookup"><span data-stu-id="5325d-142">The template that you have created will be added to the list of bandwidth templates on the service **Configure** page.</span></span>
      
      ![建立新的頻寬範本](./media/storsimple-manage-bandwidth-templates/HCS_CreateNewBT1.png)
4. <span data-ttu-id="5325d-144">在頁面底部按一下 [儲存]，然後在收到確認提示時按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="5325d-144">Click **Save** at the bottom of the page and then click **Yes** when prompted for confirmation.</span></span> <span data-ttu-id="5325d-145">這樣會儲存您所做的組態變更。</span><span class="sxs-lookup"><span data-stu-id="5325d-145">This will save the configuration changes that you have made.</span></span>

## <a name="edit-a-bandwidth-template"></a><span data-ttu-id="5325d-146">編輯頻寬範本</span><span class="sxs-lookup"><span data-stu-id="5325d-146">Edit a bandwidth template</span></span>
<span data-ttu-id="5325d-147">執行下列步驟來編輯頻寬範本。</span><span class="sxs-lookup"><span data-stu-id="5325d-147">Perform the following steps to edit a bandwidth template.</span></span>

### <a name="to-edit-a-bandwidth-template"></a><span data-ttu-id="5325d-148">編輯頻寬範本</span><span class="sxs-lookup"><span data-stu-id="5325d-148">To edit a bandwidth template</span></span>
1. <span data-ttu-id="5325d-149">按一下 [ **新增/編輯頻寬範本**]。</span><span class="sxs-lookup"><span data-stu-id="5325d-149">Click **add/edit bandwidth template**.</span></span>
2. <span data-ttu-id="5325d-150">在 [ **新增/編輯頻寬範本** ] 對話方塊中：</span><span class="sxs-lookup"><span data-stu-id="5325d-150">In the **Add/Edit Bandwidth Template** dialog box:</span></span>
   
   1. <span data-ttu-id="5325d-151">從 [ **範本** ] 下拉式清單中，選擇您想要修改的現有頻寬範本。</span><span class="sxs-lookup"><span data-stu-id="5325d-151">From the **Template** drop-down list, choose an existing bandwidth template that you want to modify.</span></span>
   2. <span data-ttu-id="5325d-152">完成您的變更。</span><span class="sxs-lookup"><span data-stu-id="5325d-152">Complete your changes.</span></span> <span data-ttu-id="5325d-153">(您可以修改任何現有的設定。)</span><span class="sxs-lookup"><span data-stu-id="5325d-153">(You can modify any of the existing settings.)</span></span>
   3. <span data-ttu-id="5325d-154">按一下核取圖示 </span><span class="sxs-lookup"><span data-stu-id="5325d-154">Click the check icon</span></span> ![核取圖示](./media/storsimple-manage-bandwidth-templates/HCS_CheckIcon.png)<span data-ttu-id="5325d-156">。</span><span class="sxs-lookup"><span data-stu-id="5325d-156">.</span></span> <span data-ttu-id="5325d-157">在服務設定頁面上，您會在頻寬範本清單中看到已修改的範本。</span><span class="sxs-lookup"><span data-stu-id="5325d-157">You will see the modified template in the list of bandwidth templates on the service Configure page.</span></span>
3. <span data-ttu-id="5325d-158">若要儲存變更，請按一下頁面底部的 [ **儲存** ]。</span><span class="sxs-lookup"><span data-stu-id="5325d-158">To save your changes, click **Save** at the bottom of the page.</span></span> <span data-ttu-id="5325d-159">在頁面底部按一下 [ **是** ]。</span><span class="sxs-lookup"><span data-stu-id="5325d-159">Click **Yes** when prompted for confirmation.</span></span>

> [!NOTE]
> <span data-ttu-id="5325d-160">如果已編輯的排程和您要修改的頻寬範本中現有的排程重疊，您就不能儲存變更。</span><span class="sxs-lookup"><span data-stu-id="5325d-160">You will not be allowed to save your changes if the edited schedule overlaps with an existing schedule in the bandwidth template that you are modifying.</span></span>
> 
> 

## <a name="delete-a-bandwidth-template"></a><span data-ttu-id="5325d-161">刪除頻寬範本</span><span class="sxs-lookup"><span data-stu-id="5325d-161">Delete a bandwidth template</span></span>
<span data-ttu-id="5325d-162">執行下列步驟來刪除頻寬範本。</span><span class="sxs-lookup"><span data-stu-id="5325d-162">Perform the following steps to delete a bandwidth template.</span></span>

#### <a name="to-delete-a-bandwidth-template"></a><span data-ttu-id="5325d-163">刪除頻寬範本</span><span class="sxs-lookup"><span data-stu-id="5325d-163">To delete a bandwidth template</span></span>
1. <span data-ttu-id="5325d-164">在服務的頻寬範本表格式清單中，選取您想要刪除的範本。</span><span class="sxs-lookup"><span data-stu-id="5325d-164">In the tabular list of the bandwidth templates for your service, select the template that you wish to delete.</span></span> <span data-ttu-id="5325d-165">刪除圖示 (**x**) 會出現在已選取範本的最右邊。</span><span class="sxs-lookup"><span data-stu-id="5325d-165">A delete icon (**x**) will appear to the extreme right of the selected template.</span></span> <span data-ttu-id="5325d-166">按一下 **x** 圖示以刪除範本。</span><span class="sxs-lookup"><span data-stu-id="5325d-166">Click the **x** icon to delete the template.</span></span>
2. <span data-ttu-id="5325d-167">系統將提示您進行確認。</span><span class="sxs-lookup"><span data-stu-id="5325d-167">You will be prompted for confirmation.</span></span> <span data-ttu-id="5325d-168">按一下 [ **確定** ] 以繼續進行。</span><span class="sxs-lookup"><span data-stu-id="5325d-168">Click **OK** to proceed.</span></span>

<span data-ttu-id="5325d-169">如果有任何磁碟區正在使用範本，您就無法將它刪除。</span><span class="sxs-lookup"><span data-stu-id="5325d-169">If the template is in use by any volume(s), you will not be allowed to delete it.</span></span> <span data-ttu-id="5325d-170">您會看到錯誤訊息，指出此範本正在使用中。</span><span class="sxs-lookup"><span data-stu-id="5325d-170">You will see an error message indicating that the template is in use.</span></span> <span data-ttu-id="5325d-171">錯誤訊息對話方塊會隨即出現，建議您移除範本的所有參考。</span><span class="sxs-lookup"><span data-stu-id="5325d-171">An error message dialog box will appear advising you that all the references to the template should be removed.</span></span>

<span data-ttu-id="5325d-172">您可以藉由存取 [ **磁碟區容器** ] 頁面和修改使用此範本的磁碟區容器，以刪除該範本的所有參考，讓它們使用另一個範本，或使用自訂或無限制頻寬設定。</span><span class="sxs-lookup"><span data-stu-id="5325d-172">You can delete all the references to the template by accessing the **Volume Containers** page and modifying the volume containers that use this template so that they use another template or use a custom or unlimited bandwidth setting.</span></span> <span data-ttu-id="5325d-173">移除所有參考時，您就可以刪除範本。</span><span class="sxs-lookup"><span data-stu-id="5325d-173">When all the references have been removed, you can delete the template.</span></span>

## <a name="use-a-default-bandwidth-template"></a><span data-ttu-id="5325d-174">使用預設頻寬範本</span><span class="sxs-lookup"><span data-stu-id="5325d-174">Use a default bandwidth template</span></span>
<span data-ttu-id="5325d-175">預設的頻寬範本可由磁碟區容器提供及使用，根據預設，可在存取雲端時強制執行頻寬控制。</span><span class="sxs-lookup"><span data-stu-id="5325d-175">A default bandwidth template is provided and is used by volume containers by default to enforce bandwidth controls when accessing the cloud.</span></span> <span data-ttu-id="5325d-176">預設範本也可讓建立自己範本的使用者當做準備參考。</span><span class="sxs-lookup"><span data-stu-id="5325d-176">The default template also serves as a ready reference for users who create their own templates.</span></span> <span data-ttu-id="5325d-177">這個預設範本的詳細資料如下：</span><span class="sxs-lookup"><span data-stu-id="5325d-177">The details of this default template are:</span></span>

* <span data-ttu-id="5325d-178">**名稱** – 不限制夜間和週末</span><span class="sxs-lookup"><span data-stu-id="5325d-178">**Name** – Unlimited nights and weekends</span></span>
* <span data-ttu-id="5325d-179">**排程** – 從星期一至星期五的單一排程，在 8 AM 和 5 PM 的裝置時間之間套用 1 Mbps 的頻寬速率。</span><span class="sxs-lookup"><span data-stu-id="5325d-179">**Schedule** – A single schedule from Monday to Friday that applies a bandwidth rate of 1 Mbps between 8 AM and 5 PM device time.</span></span> <span data-ttu-id="5325d-180">一週中的其餘部分之頻寬設定為無限制。</span><span class="sxs-lookup"><span data-stu-id="5325d-180">The bandwidth is set to Unlimited for the remainder of the week.</span></span>

<span data-ttu-id="5325d-181">預設範本可供編輯。</span><span class="sxs-lookup"><span data-stu-id="5325d-181">The default template can be edited.</span></span> <span data-ttu-id="5325d-182">追蹤此範本 (包括編輯的版本) 的使用方式。</span><span class="sxs-lookup"><span data-stu-id="5325d-182">The usage of this template (including edited versions) is tracked.</span></span>

## <a name="create-an-all-day-bandwidth-template-that-starts-at-a-specified-time"></a><span data-ttu-id="5325d-183">建立在指定時間啟動的全天頻寬範本</span><span class="sxs-lookup"><span data-stu-id="5325d-183">Create an all-day bandwidth template that starts at a specified time</span></span>
<span data-ttu-id="5325d-184">請遵循此程序來建立可在指定時間啟動並執行全天的排程。</span><span class="sxs-lookup"><span data-stu-id="5325d-184">Follow this procedure to create a schedule that starts at a specified time and runs all day.</span></span> <span data-ttu-id="5325d-185">在此範例中，排程從早上 9 AM 開始，並執行到隔天早上的 9 AM。</span><span class="sxs-lookup"><span data-stu-id="5325d-185">In the example, the schedule starts at 9 AM in the morning and runs until 9 AM the next morning.</span></span> <span data-ttu-id="5325d-186">請務必注意，給定排程的開始和結束時間都必須包含在相同的 24 小時排程，且不能跨越多天。</span><span class="sxs-lookup"><span data-stu-id="5325d-186">It's important to note that the start and end times for a given schedule must both be contained on the same 24 hour schedule and cannot span multiple days.</span></span> <span data-ttu-id="5325d-187">如果您必須設定跨越多天的頻寬範本，您必須使用多個排程 (如範例所示)。</span><span class="sxs-lookup"><span data-stu-id="5325d-187">If you need to set up bandwidth templates that span multiple days, you will need to use multiple schedules (as shown in the example).</span></span>

#### <a name="to-create-an-all-day-bandwidth-template"></a><span data-ttu-id="5325d-188">建立全天頻寬範本</span><span class="sxs-lookup"><span data-stu-id="5325d-188">To create an all-day bandwidth template</span></span>
1. <span data-ttu-id="5325d-189">建立從 9 AM 開始並執行到午夜的排程。</span><span class="sxs-lookup"><span data-stu-id="5325d-189">Create a schedule that starts at 9 AM in the morning and runs until midnight.</span></span>
2. <span data-ttu-id="5325d-190">新增另一個排程。</span><span class="sxs-lookup"><span data-stu-id="5325d-190">Add another schedule.</span></span> <span data-ttu-id="5325d-191">設定第二個排程從午夜執行到早上 9 AM。</span><span class="sxs-lookup"><span data-stu-id="5325d-191">Configure the second schedule to run from midnight until 9 AM in the morning.</span></span>
3. <span data-ttu-id="5325d-192">儲存頻寬範本</span><span class="sxs-lookup"><span data-stu-id="5325d-192">Save the bandwidth template.</span></span>

<span data-ttu-id="5325d-193">複合排程會從您選擇的時間開始並且全天執行。</span><span class="sxs-lookup"><span data-stu-id="5325d-193">The composite schedule will then start at a time of your choosing and run all-day.</span></span>

## <a name="questions-and-answers-about-bandwidth-templates"></a><span data-ttu-id="5325d-194">頻寬範本的相關問與答</span><span class="sxs-lookup"><span data-stu-id="5325d-194">Questions and answers about bandwidth templates</span></span>
<span data-ttu-id="5325d-195">**問：**</span><span class="sxs-lookup"><span data-stu-id="5325d-195">**Q**.</span></span> <span data-ttu-id="5325d-196">當您在排程之間時，頻寬控制會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="5325d-196">What happens to bandwidth controls when you are in between the schedules?</span></span> <span data-ttu-id="5325d-197">(一個排程已結束而另一個排程尚未開始)。</span><span class="sxs-lookup"><span data-stu-id="5325d-197">(A schedule has ended and another one has not started yet.)</span></span>

<span data-ttu-id="5325d-198">**答：**</span><span class="sxs-lookup"><span data-stu-id="5325d-198">**A**.</span></span> <span data-ttu-id="5325d-199">在這種情況下，不會採用任何頻寬控制。</span><span class="sxs-lookup"><span data-stu-id="5325d-199">In such cases, no bandwidth controls will be employed.</span></span> <span data-ttu-id="5325d-200">這表示將資料分層至雲端時，裝置可以使用無限制的頻寬。</span><span class="sxs-lookup"><span data-stu-id="5325d-200">This means that the device can use unlimited bandwidth when tiering data to the cloud.</span></span>

<span data-ttu-id="5325d-201">**問：**</span><span class="sxs-lookup"><span data-stu-id="5325d-201">**Q**.</span></span> <span data-ttu-id="5325d-202">您是否可以修改離線裝置上的頻寬範本？</span><span class="sxs-lookup"><span data-stu-id="5325d-202">Can you modify bandwidth templates on an offline device?</span></span>

<span data-ttu-id="5325d-203">**答：**</span><span class="sxs-lookup"><span data-stu-id="5325d-203">**A**.</span></span> <span data-ttu-id="5325d-204">如果對應的裝置已離線，您無法修改磁碟區容器上的頻寬範本。</span><span class="sxs-lookup"><span data-stu-id="5325d-204">You will not be able to modify bandwidth templates on volumes containers if the corresponding device is offline.</span></span>

<span data-ttu-id="5325d-205">**問：**</span><span class="sxs-lookup"><span data-stu-id="5325d-205">**Q**.</span></span> <span data-ttu-id="5325d-206">您是否可以在相關聯的磁碟區離線時，編輯和磁碟區容器相關聯的頻寬範本？</span><span class="sxs-lookup"><span data-stu-id="5325d-206">Can you edit a bandwidth template associated with a volume container when the associated volumes are offline?</span></span>

<span data-ttu-id="5325d-207">**答：**</span><span class="sxs-lookup"><span data-stu-id="5325d-207">**A**.</span></span> <span data-ttu-id="5325d-208">您可以修改和磁碟區已離線之磁碟區容器相關聯的頻寬範本。</span><span class="sxs-lookup"><span data-stu-id="5325d-208">You can modify a bandwidth template associated with a volume container whose volumes are offline.</span></span> <span data-ttu-id="5325d-209">請注意，當磁碟區離線時，沒有資料會從裝置分層至雲端。</span><span class="sxs-lookup"><span data-stu-id="5325d-209">Note that when volumes are offline, no data will be tiered from the device to the cloud.</span></span>

<span data-ttu-id="5325d-210">**問：**</span><span class="sxs-lookup"><span data-stu-id="5325d-210">**Q**.</span></span> <span data-ttu-id="5325d-211">您是否可以刪除預設範本？</span><span class="sxs-lookup"><span data-stu-id="5325d-211">Can you delete a default template?</span></span>

<span data-ttu-id="5325d-212">**答：**</span><span class="sxs-lookup"><span data-stu-id="5325d-212">**A**.</span></span> <span data-ttu-id="5325d-213">雖然您可以刪除預設範本，但這並不是個好主意。</span><span class="sxs-lookup"><span data-stu-id="5325d-213">Although you can delete a default template, it is not a good idea to do so.</span></span> <span data-ttu-id="5325d-214">已追蹤此預設範本 (包括已編輯版本) 的使用方式。</span><span class="sxs-lookup"><span data-stu-id="5325d-214">The usage of a default template, including edited versions, is tracked.</span></span> <span data-ttu-id="5325d-215">追蹤資料已進行分析，並在時間過程中用來改善預設範本。</span><span class="sxs-lookup"><span data-stu-id="5325d-215">The tracking data is analyzed and over the course of time, is used to improve the default template.</span></span>

<span data-ttu-id="5325d-216">**問：**</span><span class="sxs-lookup"><span data-stu-id="5325d-216">**Q**.</span></span> <span data-ttu-id="5325d-217">如何判斷頻寬範本必須修改？</span><span class="sxs-lookup"><span data-stu-id="5325d-217">How do you determine that your bandwidth templates need to be modified?</span></span>

<span data-ttu-id="5325d-218">**答：**</span><span class="sxs-lookup"><span data-stu-id="5325d-218">**A**.</span></span> <span data-ttu-id="5325d-219">您必須修改頻寬範本的其中一個徵兆是您會開始看到網路變慢，或在一天中多次停擺。</span><span class="sxs-lookup"><span data-stu-id="5325d-219">One of the signs that you need to modify the bandwidth templates is when you start seeing the network slow down or choke multiple times in a day.</span></span> <span data-ttu-id="5325d-220">如果發生這種情況，請查看 I/O 效能及網路輸送量圖表來監視儲存體和使用方式的網路。</span><span class="sxs-lookup"><span data-stu-id="5325d-220">If this happens, monitor the storage and usage network by looking at the I/O Performance and Network Throughput charts.</span></span>

<span data-ttu-id="5325d-221">從網路輸送量資料，找出發生網路瓶頸的日期時間與磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="5325d-221">From the network throughput data, identify the time of day and the volume containers in which the network bottleneck occurs.</span></span> <span data-ttu-id="5325d-222">如果在資料分層至雲端時發生這種情況 (可由裝置至雲端的所有磁碟區容器之 I/O 效能取得此資訊)，您必須修改和磁碟區容器相關聯的頻寬範本。</span><span class="sxs-lookup"><span data-stu-id="5325d-222">If this happens when data is being tiered to the cloud (get this information from I/O performance for all volume containers for device to cloud), then you will need to modify the bandwidth templates associated with your volume containers.</span></span>

<span data-ttu-id="5325d-223">開始使用已修改的範本之後，您必須再次監視網路是否有顯著的延遲。</span><span class="sxs-lookup"><span data-stu-id="5325d-223">After the modified templates are in use, you will need to monitor the network again for significant latencies.</span></span> <span data-ttu-id="5325d-224">如果仍然存在延遲，您必須返回頻寬範本。</span><span class="sxs-lookup"><span data-stu-id="5325d-224">If these still exist, then you will need to revisit your bandwidth templates.</span></span>

<span data-ttu-id="5325d-225">**問：**</span><span class="sxs-lookup"><span data-stu-id="5325d-225">**Q**.</span></span> <span data-ttu-id="5325d-226">要是裝置上多個磁碟區容器的排程重疊，但是每個排程都套用不同的限制會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="5325d-226">What happens if multiple volume containers on my device have schedules that overlap but different limits apply to each?</span></span>

<span data-ttu-id="5325d-227">**答：**</span><span class="sxs-lookup"><span data-stu-id="5325d-227">**A**.</span></span> <span data-ttu-id="5325d-228">假設您的裝置有 3 個磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="5325d-228">Let's assume that you have a device with 3 volume containers.</span></span> <span data-ttu-id="5325d-229">與這些容器相關聯的排程完全重疊。</span><span class="sxs-lookup"><span data-stu-id="5325d-229">The schedules associated with these containers completely overlap.</span></span> <span data-ttu-id="5325d-230">針對每個容器，分別使用 5、10 和 15 Mbps 的頻寬限制。</span><span class="sxs-lookup"><span data-stu-id="5325d-230">For each of these containers, the bandwidth limits used are 5, 10, and 15 Mbps respectively.</span></span> <span data-ttu-id="5325d-231">當所有容器都同時出現 I/O 時，可能會套用 3 個頻寬限制中的最小值：5 Mbps，因為在此情況下，這些傳出 I/O 要求會共用相同的佇列。</span><span class="sxs-lookup"><span data-stu-id="5325d-231">When I/Os are occurring on all of these containers at the same time, the minimum of the 3 bandwidth limits may be applied: in this case, 5 Mbps as these outgoing I/O requests share the same queue.</span></span>

## <a name="best-practices-for-bandwidth-templates"></a><span data-ttu-id="5325d-232">頻寬範本的最佳作法</span><span class="sxs-lookup"><span data-stu-id="5325d-232">Best practices for bandwidth templates</span></span>
<span data-ttu-id="5325d-233">請遵循 StorSimple 裝置的最佳作法：</span><span class="sxs-lookup"><span data-stu-id="5325d-233">Follow these best practices for your StorSimple device:</span></span>

* <span data-ttu-id="5325d-234">在裝置上設定頻寬範本，以根據裝置在一天中的不同時間，啟用網路傳輸量的變數節流。</span><span class="sxs-lookup"><span data-stu-id="5325d-234">Configure bandwidth templates on your device to enable variable throttling of the network throughput by the device at different times of the day.</span></span> <span data-ttu-id="5325d-235">這些頻寬範本和備份排程搭配使用時，可以在離峰時段期間有效利用雲端作業的其他網路頻寬。</span><span class="sxs-lookup"><span data-stu-id="5325d-235">These bandwidth templates when used with backup schedules can effectively leverage additional network bandwidth for cloud operations during off-peak hours.</span></span>
* <span data-ttu-id="5325d-236">根據部署的大小和所需的復原時間目標 (RTO)，計算特定部署所需的實際頻寬。</span><span class="sxs-lookup"><span data-stu-id="5325d-236">Calculate the actual bandwidth required for a particular deployment based on the size of the deployment and the required recovery time objective (RTO).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5325d-237">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5325d-237">Next steps</span></span>
<span data-ttu-id="5325d-238">深入了解 [使用 StorSimple Manager 服務管理 StorSimple 裝置](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="5325d-238">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

