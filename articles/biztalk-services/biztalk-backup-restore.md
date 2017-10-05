---
title: "在 BizTalk 服務中建立和還原備份 | Microsoft Docs"
description: "BizTalk 服務包含備份與還原功能。 了解如何建立和還原備份，以及判斷該備份什麼。 MABS，WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 59f91173-4683-48df-abd5-41262bfce6df
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: c55d1ab124441c42101b4ad60924a9ea28231408
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="biztalk-services-backup-and-restore"></a><span data-ttu-id="19e49-105">BizTalk 服務：備份與還原</span><span class="sxs-lookup"><span data-stu-id="19e49-105">BizTalk Services: Backup and Restore</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="19e49-106">Azure BizTalk 服務包含備份與還原功能。</span><span class="sxs-lookup"><span data-stu-id="19e49-106">Azure BizTalk Services includes Backup and Restore capabilities.</span></span> <span data-ttu-id="19e49-107">本主題說明如何使用 Azure 傳統入口網站來備份和還原 BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="19e49-107">This topic describes how to backup and restore BizTalk Services using the Azure classic portal.</span></span>

<span data-ttu-id="19e49-108">您也可以使用 [BizTalk 服務 REST API](http://go.microsoft.com/fwlink/p/?LinkID=325584)來備份 BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="19e49-108">You can also back up BizTalk Services using the [BizTalk Services REST API](http://go.microsoft.com/fwlink/p/?LinkID=325584).</span></span> 

> [!NOTE]
> <span data-ttu-id="19e49-109">混合式連接無法備份，與版本無關。</span><span class="sxs-lookup"><span data-stu-id="19e49-109">Hybrid Connections are NOT backed up, regardless of the Edition.</span></span> <span data-ttu-id="19e49-110">您必須重新建立混合式連接。</span><span class="sxs-lookup"><span data-stu-id="19e49-110">You must recreate your hybrid connections.</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="19e49-111">開始之前</span><span class="sxs-lookup"><span data-stu-id="19e49-111">Before you Begin</span></span>
* <span data-ttu-id="19e49-112">備份與還原可能不適用於部分版本。</span><span class="sxs-lookup"><span data-stu-id="19e49-112">Backup and Restore may not be available for all editions.</span></span> <span data-ttu-id="19e49-113">請參閱「 [BizTalk 服務：版本圖表](biztalk-editions-feature-chart.md)」(英文)。</span><span class="sxs-lookup"><span data-stu-id="19e49-113">See [BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span></span>
* <span data-ttu-id="19e49-114">使用 Azure 傳統入口網站可建立隨選備份或排定備份。</span><span class="sxs-lookup"><span data-stu-id="19e49-114">Using the Azure classic portal, you can create an On Demand backup or create a scheduled backup.</span></span> 
* <span data-ttu-id="19e49-115">備份內容可以還原至相同的 BizTalk 服務，或還原至新的 BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="19e49-115">Backup content can be restored to the same BizTalk Service or to a new BizTalk Service.</span></span> <span data-ttu-id="19e49-116">若要使用相同名稱來還原 BizTalk 服務，必須刪除現有的 BizTalk 服務，且名稱必須可用。</span><span class="sxs-lookup"><span data-stu-id="19e49-116">To restore the BizTalk Service using the same name, the existing BizTalk Service must be deleted and the name must be available.</span></span> <span data-ttu-id="19e49-117">刪除 BizTalk 服務之後，可能需要較長的時間，才能使用相同的名稱。</span><span class="sxs-lookup"><span data-stu-id="19e49-117">After you delete a BizTalk Service, it can take longer time than wanted for the same name to be available.</span></span> <span data-ttu-id="19e49-118">如果無法等待相同的名稱可用，請還原至新的 BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="19e49-118">If you cannot wait for the same name to be available, then restore to a new BizTalk Service.</span></span>
* <span data-ttu-id="19e49-119">BizTalk 服務可以還原至相同版本或更高的版本。</span><span class="sxs-lookup"><span data-stu-id="19e49-119">BizTalk Services can be restored to the same edition or a higher edition.</span></span> <span data-ttu-id="19e49-120">從建立備份之後，不支援將 BizTalk 服務還原至較低版本。</span><span class="sxs-lookup"><span data-stu-id="19e49-120">Restoring BizTalk Services to a lower edition, from when the backup was taken, is not supported.</span></span>
  
    <span data-ttu-id="19e49-121">例如，使用基本版本的備份可以還原至高級版本。</span><span class="sxs-lookup"><span data-stu-id="19e49-121">For example, a backup using the Basic Edition can be restored to the Premium Edition.</span></span> <span data-ttu-id="19e49-122">使用高級版本的備份不能還原至標準版本。</span><span class="sxs-lookup"><span data-stu-id="19e49-122">A backup using the Premium Edition cannot be restored to the Standard Edition.</span></span>
* <span data-ttu-id="19e49-123">EDI 控制編號會備份以維持控制編號的連貫性。</span><span class="sxs-lookup"><span data-stu-id="19e49-123">The EDI Control numbers are backed up to maintain continuity of the control numbers.</span></span> <span data-ttu-id="19e49-124">如果在上次備份之後處理訊息，則還原此備份內容會產生重複的控制編號。</span><span class="sxs-lookup"><span data-stu-id="19e49-124">If messages are processed after the last backup, restoring this backup content can cause duplicate control numbers.</span></span>
* <span data-ttu-id="19e49-125">如果批次中有作用中的訊息，請在執行備份前 **先** 處理批次。</span><span class="sxs-lookup"><span data-stu-id="19e49-125">If a batch has active messages, process the batch **before** running a backup.</span></span> <span data-ttu-id="19e49-126">無論是建立隨選備份或排定備份，都不會儲存批次中的訊息。</span><span class="sxs-lookup"><span data-stu-id="19e49-126">When creating a backup (as needed or scheduled), messages in batches are never stored.</span></span> 
  
    <span data-ttu-id="19e49-127">**建立備份時，如果批次中有作用中的訊息，則不會備份這些訊息，且這些訊息將會遺失。**</span><span class="sxs-lookup"><span data-stu-id="19e49-127">**If a backup is taken with active messages in a batch, these messages are not backed up and are therefore lost.**</span></span>
* <span data-ttu-id="19e49-128">選用：在 BizTalk 服務入口網站中，停止任何管理作業。</span><span class="sxs-lookup"><span data-stu-id="19e49-128">Optional: In the BizTalk Services Portal, stop any management operations.</span></span>

## <a name="create-a-backup"></a><span data-ttu-id="19e49-129">建立備份</span><span class="sxs-lookup"><span data-stu-id="19e49-129">Create a backup</span></span>
<span data-ttu-id="19e49-130">您隨時都可以建立備份，完全決由掌控。</span><span class="sxs-lookup"><span data-stu-id="19e49-130">A backup can be taken at any time and is completely controlled by you.</span></span> <span data-ttu-id="19e49-131">本節列出使用 Azure 傳統入口網站建立備份的步驟，內容包括：</span><span class="sxs-lookup"><span data-stu-id="19e49-131">This section lists the steps to create backups using the Azure classic portal, including:</span></span>

[<span data-ttu-id="19e49-132">隨選備份</span><span class="sxs-lookup"><span data-stu-id="19e49-132">On Demand backup</span></span>](#backupnow)

[<span data-ttu-id="19e49-133">排定備份</span><span class="sxs-lookup"><span data-stu-id="19e49-133">Schedule a backup</span></span>](#backupschedule)

#### <span data-ttu-id="19e49-134"><a name="backupnow"></a>隨選備份</span><span class="sxs-lookup"><span data-stu-id="19e49-134"><a name="backupnow"></a>On Demand backup</span></span>
1. <span data-ttu-id="19e49-135">在 Azure 傳統入口網站上，選取 [BizTalk 服務] ，然後選取要備份的 BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="19e49-135">In the Azure classic portal, select **BizTalk Services**, and then select the BizTalk Service you want to backup.</span></span>
2. <span data-ttu-id="19e49-136">在 [儀表板] 索引標籤中，選取頁面底部的 [備份]。</span><span class="sxs-lookup"><span data-stu-id="19e49-136">In the **Dashboard** tab, select **Back up** at the bottom of the page.</span></span>
3. <span data-ttu-id="19e49-137">輸入備份名稱。</span><span class="sxs-lookup"><span data-stu-id="19e49-137">Enter a backup name.</span></span> <span data-ttu-id="19e49-138">例如，輸入 *myBizTalkService*BU*Date*。</span><span class="sxs-lookup"><span data-stu-id="19e49-138">For example, enter *myBizTalkService*BU*Date*.</span></span>
4. <span data-ttu-id="19e49-139">選擇 Blob 儲存體帳戶，然後選取勾選記號開始備份。</span><span class="sxs-lookup"><span data-stu-id="19e49-139">Choose a blob storage account and select the checkmark to start the backup.</span></span>

<span data-ttu-id="19e49-140">備份完成時，儲存體帳戶內會以您輸入的備份名稱建立一個容器。</span><span class="sxs-lookup"><span data-stu-id="19e49-140">Once the backup completes, a container with the backup name you enter is created in the storage account.</span></span> <span data-ttu-id="19e49-141">此容器包含 BizTalk 服務備份組態。</span><span class="sxs-lookup"><span data-stu-id="19e49-141">This container contains your BizTalk Service backup configuration.</span></span>

#### <span data-ttu-id="19e49-142"><a name="backupschedule"></a>排定備份</span><span class="sxs-lookup"><span data-stu-id="19e49-142"><a name="backupschedule"></a>Schedule a backup</span></span>
1. <span data-ttu-id="19e49-143">在 Azure 傳統入口網站上，選取 [BizTalk 服務]，選取您要排定備份的 BizTalk 服務名稱，然後選取 [設定] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="19e49-143">In the Azure classic portal, select **BizTalk Services**, select the BizTalk Service name you want to schedule the backup, and then select the **Configure** tab.</span></span>
2. <span data-ttu-id="19e49-144">將 [備份狀態] 設為 [自動]。</span><span class="sxs-lookup"><span data-stu-id="19e49-144">Set the **Backup Status** to **Automatic**.</span></span> 
3. <span data-ttu-id="19e49-145">選取要儲存備份的 [儲存體帳戶]，輸入建立備份的 [頻率] 以及備份的保留時間 ([保留天數])：</span><span class="sxs-lookup"><span data-stu-id="19e49-145">Select the **Storage Account** to store the backup, enter the **Frequency** to create the backups, and how long to keep the backups (**Retention Days**):</span></span>
   
    ![][AutomaticBU]
   
    <span data-ttu-id="19e49-146">**注意事項**</span><span class="sxs-lookup"><span data-stu-id="19e49-146">**Notes**</span></span>     
   
   * <span data-ttu-id="19e49-147">[保留天數] 中的保留週期必須大於備份頻率。</span><span class="sxs-lookup"><span data-stu-id="19e49-147">In **Retention Days**, the retention period must be greater than the backup frequency.</span></span>
   * <span data-ttu-id="19e49-148">選取 [永遠保留至少一個備份] ，以確保即使超過保留週期也有備份可用。</span><span class="sxs-lookup"><span data-stu-id="19e49-148">Select **Always keep at least one backup**, even if it is past the retention period.</span></span>
4. <span data-ttu-id="19e49-149">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="19e49-149">Select **Save**.</span></span>

<span data-ttu-id="19e49-150">排定的備份工作執行時，會在您輸入的儲存體帳戶中建立容器 (以儲存備份資料)。</span><span class="sxs-lookup"><span data-stu-id="19e49-150">When a scheduled backup job runs, it creates a container (to store backup data) in the storage account you entered.</span></span> <span data-ttu-id="19e49-151">容器名稱的命名方式為 *BizTalk Service Name-date-time*。</span><span class="sxs-lookup"><span data-stu-id="19e49-151">The name of the container is named *BizTalk Service Name-date-time*.</span></span> 

<span data-ttu-id="19e49-152">如果 BizTalk 服務儀表板顯示 [ **失敗** ] 狀態：</span><span class="sxs-lookup"><span data-stu-id="19e49-152">If the BizTalk Service dashboard shows a **Failed** status:</span></span>

![上次排定的備份狀態][BackupStatus] 

<span data-ttu-id="19e49-154">該連結可開啟 [管理服務作業記錄] 以協助進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="19e49-154">The link opens the Management Services Operation Logs to help troubleshoot.</span></span> <span data-ttu-id="19e49-155">請參閱 [BizTalk 服務：使用作業記錄進行疑難排解](http://go.microsoft.com/fwlink/p/?LinkId=391211)。</span><span class="sxs-lookup"><span data-stu-id="19e49-155">See [BizTalk Services: Troubleshoot using operation logs](http://go.microsoft.com/fwlink/p/?LinkId=391211).</span></span>

## <a name="restore"></a><span data-ttu-id="19e49-156">Restore</span><span class="sxs-lookup"><span data-stu-id="19e49-156">Restore</span></span>
<span data-ttu-id="19e49-157">您可以從 Azure 傳統入口網站或從 [還原 BizTalk 服務 REST API](http://go.microsoft.com/fwlink/p/?LinkID=325582)來還原備份。</span><span class="sxs-lookup"><span data-stu-id="19e49-157">You can restore backups from the Azure classic portal or from the [Restore BizTalk Service REST API](http://go.microsoft.com/fwlink/p/?LinkID=325582).</span></span> <span data-ttu-id="19e49-158">本節列出使用傳統入口網站進行還原的步驟。</span><span class="sxs-lookup"><span data-stu-id="19e49-158">This section lists the steps to restore using the classic portal.</span></span>

#### <a name="before-restoring-a-backup"></a><span data-ttu-id="19e49-159">還原備份之前</span><span class="sxs-lookup"><span data-stu-id="19e49-159">Before restoring a backup</span></span>
* <span data-ttu-id="19e49-160">還原 BizTalk 服務時可以輸入新的追蹤、封存和監視儲存區。</span><span class="sxs-lookup"><span data-stu-id="19e49-160">New tracking, archiving, and monitoring stores can be entered while restoring a BizTalk Service.</span></span>
* <span data-ttu-id="19e49-161">將還原相同的 EDI Runtime 資料。</span><span class="sxs-lookup"><span data-stu-id="19e49-161">The same EDI Runtime data is restored.</span></span> <span data-ttu-id="19e49-162">EDI Runtime 備份中儲存控制編號。</span><span class="sxs-lookup"><span data-stu-id="19e49-162">The EDI Runtime backup stores the control numbers.</span></span> <span data-ttu-id="19e49-163">還原的控制編號從備份時間開始按順序編排。</span><span class="sxs-lookup"><span data-stu-id="19e49-163">The restored control numbers are in sequence from the time of the backup.</span></span> <span data-ttu-id="19e49-164">如果在上次備份之後處理訊息，則還原此備份內容會產生重複的控制編號。</span><span class="sxs-lookup"><span data-stu-id="19e49-164">If messages are processed after the last backup, restoring this backup content can cause duplicate control numbers.</span></span>

#### <a name="restore-a-backup"></a><span data-ttu-id="19e49-165">還原備份</span><span class="sxs-lookup"><span data-stu-id="19e49-165">Restore a backup</span></span>
1. <span data-ttu-id="19e49-166">在 Azure 傳統入口網站中，選取 [新增] > [應用程式服務] > [BizTalk 服務] > [還原]：</span><span class="sxs-lookup"><span data-stu-id="19e49-166">In the Azure classic portal, select **New** > **App Services** > **BizTalk Service** > **Restore**:</span></span>
   
    ![還原備份][Restore]
2. <span data-ttu-id="19e49-168">在 [ **備份 URL**] 中，選取資料夾圖示並展開儲存 BizTalk 服務設定備份的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="19e49-168">In **Backup URL**, select the folder icon and expand the Azure storage account that stores the BizTalk Service configuration backup.</span></span> <span data-ttu-id="19e49-169">展開容器，然後在右窗格中，選取對應的 .txt 備份檔案。</span><span class="sxs-lookup"><span data-stu-id="19e49-169">Expand the container and in the right pane, select the corresponding back up .txt file.</span></span> 
   <br/><br/>
   <span data-ttu-id="19e49-170">選取 [開啟] 。</span><span class="sxs-lookup"><span data-stu-id="19e49-170">Select **Open**.</span></span>
3. <span data-ttu-id="19e49-171">在 [還原 BizTalk 服務] 頁面上，輸入一個 **BizTalk 服務名稱**，然後驗證要還原的 BizTalk 服務的**網域 URL**、**版本**和**區域**。</span><span class="sxs-lookup"><span data-stu-id="19e49-171">On the **Restore BizTalk Service** page, enter a **BizTalk Service Name** and verify the **Domain URL**, **Edition**, and **Region** for the restored BizTalk Service.</span></span> <span data-ttu-id="19e49-172">**建立新的 SQL 資料庫執行個體** ：</span><span class="sxs-lookup"><span data-stu-id="19e49-172">**Create a new SQL database instance** for the tracking database:</span></span>
   
    ![][RestoreBizTalkService]
   
    <span data-ttu-id="19e49-173">選取下一個箭頭。</span><span class="sxs-lookup"><span data-stu-id="19e49-173">Select the next arrow.</span></span>
4. <span data-ttu-id="19e49-174">驗證 SQL 資料庫的名稱，輸入將建立 SQL 資料庫的實體伺服器，以及該伺服器的使用者名稱/密碼。</span><span class="sxs-lookup"><span data-stu-id="19e49-174">Verify the name of the SQL database, enter the physical server where the SQL database will be created, and a username/password for that server.</span></span>

    <span data-ttu-id="19e49-175">如果您要設定 SQL 資料庫版本、大小和其他屬性，請選取 [設定進階資料庫設定]。</span><span class="sxs-lookup"><span data-stu-id="19e49-175">If you want to configure the SQL database edition, size, and other properties, select  **Configure Advanced Database Settings**.</span></span> 

    <span data-ttu-id="19e49-176">選取下一個箭頭。</span><span class="sxs-lookup"><span data-stu-id="19e49-176">Select the next arrow.</span></span>

1. <span data-ttu-id="19e49-177">為 BizTalk 服務建立新的儲存體帳戶或輸入現有的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="19e49-177">Create a new storage account or enter an existing storage account for the BizTalk Service.</span></span>
2. <span data-ttu-id="19e49-178">選取勾選記號以啟動還原。</span><span class="sxs-lookup"><span data-stu-id="19e49-178">Select the checkmark to start the restore.</span></span>

<span data-ttu-id="19e49-179">順利完成還原時，在 Azure 傳統入口網站的 BizTalk 伺服器頁面上，新的 BizTalk 服務將以暫止狀態列出。</span><span class="sxs-lookup"><span data-stu-id="19e49-179">Once the restoration successfully completes, a new BizTalk Service is listed in a suspended state on the BizTalk Services page in the Azure classic portal.</span></span>

### <span data-ttu-id="19e49-180"><a name="postrestore"></a>還原備份之後</span><span class="sxs-lookup"><span data-stu-id="19e49-180"><a name="postrestore"></a>After restoring a backup</span></span>
<span data-ttu-id="19e49-181">BizTalk 服務永遠還原成 **暫止** 狀態。</span><span class="sxs-lookup"><span data-stu-id="19e49-181">The BizTalk Service is always restored in a **Suspended** state.</span></span> <span data-ttu-id="19e49-182">在此狀態下，您可以在新環境開始運作前進行任何設定變更，包括：</span><span class="sxs-lookup"><span data-stu-id="19e49-182">In this state, you can make any configuration changes before the new environment is functional, including:</span></span>

* <span data-ttu-id="19e49-183">若您使用 Azure BizTalk 服務 SDK 來建立 BizTalk 服務應用程式，您可能需要在這些應用程式中更新存取控制 (ACS) 認證，才能使用還原後的環境。</span><span class="sxs-lookup"><span data-stu-id="19e49-183">If you created BizTalk Service applications using the Azure BizTalk Services SDK, you may need to to update the Access Control (ACS) credentials in those applications to work with the restored environment.</span></span>
* <span data-ttu-id="19e49-184">您可以還原 BizTalk 服務來複寫現有的 BizTalk 服務環境。</span><span class="sxs-lookup"><span data-stu-id="19e49-184">You restore a BizTalk Service to replicate an existing BizTalk Service environment.</span></span> <span data-ttu-id="19e49-185">在此情況下，如果在原始 BizTalk 服務入口網站中有設定的協議使用 FTP 來源資料夾，則您可能需要在剛還原的環境中更新協議，以使用其他 FTP 來源資料夾。</span><span class="sxs-lookup"><span data-stu-id="19e49-185">In this situation, if there are agreements configured in the original BizTalk Services portal that use a source FTP folder, you may need to update the agreements in the newly restored environment to use a different source FTP folder.</span></span> <span data-ttu-id="19e49-186">否則，可能會有兩個不同的協議都嘗試提取相同的訊息。</span><span class="sxs-lookup"><span data-stu-id="19e49-186">Otherwise, there may be two different agreements trying to pull the same message.</span></span>
* <span data-ttu-id="19e49-187">如果您已進行還原而產生多個 BizTalk 服務環境，則在使用 Visual Studio 應用程式、PowerShell Cmdlet、REST API 或交易夥伴管理 OM API 時，請確定目標環境正確。</span><span class="sxs-lookup"><span data-stu-id="19e49-187">If you restored to have multiple BizTalk Service environments, make sure you target the correct environment in the Visual Studio applications, PowerShell cmdlets, REST APIs, or Trading Partner Management OM APIs.</span></span>
* <span data-ttu-id="19e49-188">在剛還原的 BizTalk 服務環境上，建議設定自動備份。</span><span class="sxs-lookup"><span data-stu-id="19e49-188">It's a good practice to configure automated backups on the newly restored BizTalk Service environment.</span></span>

<span data-ttu-id="19e49-189">若要在 Azure 傳統入口網站上啟動 BizTalk 服務，請選取已還原的 BizTalk 服務，然後在工作列中選取 [繼續]  。</span><span class="sxs-lookup"><span data-stu-id="19e49-189">To start the BizTalk Service in the Azure classic portal, select the restored BizTalk Service and select **Resume** in the task bar.</span></span> 

## <a name="what-gets-backed-up"></a><span data-ttu-id="19e49-190">備份什麼項目</span><span class="sxs-lookup"><span data-stu-id="19e49-190">What gets backed up</span></span>
<span data-ttu-id="19e49-191">建立備份時會備份下列項目：</span><span class="sxs-lookup"><span data-stu-id="19e49-191">When a backup is created, the following items are backed up:</span></span>

<table border="1"> 
<tr bgcolor="FAF9F9">
<th> </th>
<TH><span data-ttu-id="19e49-192">備份的項目</span><span class="sxs-lookup"><span data-stu-id="19e49-192">Items backed up</span></span></TH> 
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="19e49-193">
 <strong>Azure BizTalk 服務入口網站</strong></span><span class="sxs-lookup"><span data-stu-id="19e49-193">
 <strong>Azure BizTalk Services Portal</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="19e49-194">組態和執行階段</span><span class="sxs-lookup"><span data-stu-id="19e49-194">Configuration and Runtime</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="19e49-195">夥伴和設定檔詳細資料</span><span class="sxs-lookup"><span data-stu-id="19e49-195">Partner and profile details</span></span></li>
<li><span data-ttu-id="19e49-196">夥伴協議</span><span class="sxs-lookup"><span data-stu-id="19e49-196">Partner Agreements</span></span></li>
<li><span data-ttu-id="19e49-197">已部署的自訂組件</span><span class="sxs-lookup"><span data-stu-id="19e49-197">Custom assemblies deployed</span></span></li>
<li><span data-ttu-id="19e49-198">已部署的橋接器</span><span class="sxs-lookup"><span data-stu-id="19e49-198">Bridges deployed</span></span></li>
<li><span data-ttu-id="19e49-199">憑證</span><span class="sxs-lookup"><span data-stu-id="19e49-199">Certificates</span></span></li>
<li><span data-ttu-id="19e49-200">已部署的轉換</span><span class="sxs-lookup"><span data-stu-id="19e49-200">Transforms deployed</span></span></li>
<li><span data-ttu-id="19e49-201">管線</span><span class="sxs-lookup"><span data-stu-id="19e49-201">Pipelines</span></span></li>
<li><span data-ttu-id="19e49-202">BizTalk 服務入口網站中建立和儲存的範本</span><span class="sxs-lookup"><span data-stu-id="19e49-202">Templates created and saved in the BizTalk Services Portal</span></span></li>
<li><span data-ttu-id="19e49-203">X12 ST01 和 GS01 對應</span><span class="sxs-lookup"><span data-stu-id="19e49-203">X12 ST01 and GS01 mappings</span></span></li>
<li><span data-ttu-id="19e49-204">控制編號 (EDI)</span><span class="sxs-lookup"><span data-stu-id="19e49-204">Control numbers (EDI)</span></span></li>
<li><span data-ttu-id="19e49-205">AS2 訊息 MIC 值</span><span class="sxs-lookup"><span data-stu-id="19e49-205">AS2 Message MIC values</span></span></li>
</ul>
</td>
</tr> 

<tr>
<td colspan="2"><span data-ttu-id="19e49-206">
 <strong>Azure BizTalk 服務</strong></span><span class="sxs-lookup"><span data-stu-id="19e49-206">
 <strong>Azure BizTalk Service</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="19e49-207">SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="19e49-207">SSL Certificate</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="19e49-208">SSL 憑證資料</span><span class="sxs-lookup"><span data-stu-id="19e49-208">SSL Certificate Data</span></span></li>
<li><span data-ttu-id="19e49-209">SSL 憑證密碼</span><span class="sxs-lookup"><span data-stu-id="19e49-209">SSL Certificate Password</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td><span data-ttu-id="19e49-210">BizTalk 服務設定</span><span class="sxs-lookup"><span data-stu-id="19e49-210">BizTalk Service Settings</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="19e49-211">調整單位計數</span><span class="sxs-lookup"><span data-stu-id="19e49-211">Scale unit count</span></span></li>
<li><span data-ttu-id="19e49-212">版本</span><span class="sxs-lookup"><span data-stu-id="19e49-212">Edition</span></span></li>
<li><span data-ttu-id="19e49-213">產品版本</span><span class="sxs-lookup"><span data-stu-id="19e49-213">Product Version</span></span></li>
<li><span data-ttu-id="19e49-214">區域/資料中心</span><span class="sxs-lookup"><span data-stu-id="19e49-214">Region/Datacenter</span></span></li>
<li><span data-ttu-id="19e49-215">存取控制服務 (ACS) 命名空間和金鑰</span><span class="sxs-lookup"><span data-stu-id="19e49-215">Access Control Service (ACS) namespace and key</span></span></li>
<li><span data-ttu-id="19e49-216">追蹤資料庫連接字串</span><span class="sxs-lookup"><span data-stu-id="19e49-216">Tracking database connection string</span></span></li>
<li><span data-ttu-id="19e49-217">封存儲存體帳戶連接字串</span><span class="sxs-lookup"><span data-stu-id="19e49-217">Archiving Storage account connection string</span></span></li>
<li><span data-ttu-id="19e49-218">監視儲存體帳戶連接字串</span><span class="sxs-lookup"><span data-stu-id="19e49-218">Monitoring storage account connection string</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="19e49-219">
 <strong>其他項目</strong></span><span class="sxs-lookup"><span data-stu-id="19e49-219">
 <strong>Additional Items</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="19e49-220">追蹤資料庫</span><span class="sxs-lookup"><span data-stu-id="19e49-220">Tracking Database</span></span></td> 
<td><span data-ttu-id="19e49-221">建立 BizTalk 服務時需要輸入追蹤資料庫詳細資料，包括 Azure SQL Database 伺服器和追蹤資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="19e49-221">When the BizTalk Service is created, the Tracking Database details are entered, including the Azure SQL Database Server and the Tracking Database name.</span></span> <span data-ttu-id="19e49-222">不會自動備份追蹤資料庫。</span><span class="sxs-lookup"><span data-stu-id="19e49-222">The Tracking Database is not automatically backed up.</span></span>
<br/><br/><span data-ttu-id="19e49-223">
<strong>重要</strong></span><span class="sxs-lookup"><span data-stu-id="19e49-223">
<strong>Important</strong></span></span><br/>
<span data-ttu-id="19e49-224">如果刪除了追蹤資料庫，且需要復原資料庫，先前的備份必須存在。</span><span class="sxs-lookup"><span data-stu-id="19e49-224">If the Tracking Database is deleted and the database needs recovered, a previous backup must exist.</span></span> <span data-ttu-id="19e49-225">如果備份不存在，則無法復原追蹤資料庫及其資料。</span><span class="sxs-lookup"><span data-stu-id="19e49-225">If a backup does not exist, the Tracking Database and its data are not recoverable.</span></span> <span data-ttu-id="19e49-226">在此情況下，請以相同的資料庫名稱建立新的追蹤資料庫。</span><span class="sxs-lookup"><span data-stu-id="19e49-226">In this situation, create a new Tracking Database with the same database name.</span></span> <span data-ttu-id="19e49-227">建議採用地理複寫。</span><span class="sxs-lookup"><span data-stu-id="19e49-227">Geo-Replication is recommended.</span></span></td>
</tr> 
</table>

## <a name="next"></a><span data-ttu-id="19e49-228">下一步</span><span class="sxs-lookup"><span data-stu-id="19e49-228">Next</span></span>
<span data-ttu-id="19e49-229">若要在 Azure 傳統入口網站中建立 Azure BizTalk 服務，請移至 [BizTalk 服務：使用 Azure 傳統入口網站進行佈建](http://go.microsoft.com/fwlink/p/?LinkID=302280)。</span><span class="sxs-lookup"><span data-stu-id="19e49-229">To create Azure BizTalk Services in the Azure classic portal, go to [BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280).</span></span> <span data-ttu-id="19e49-230">若要開始建立應用程式，請移至 [Azure BizTalk 服務](http://go.microsoft.com/fwlink/p/?LinkID=235197)(英文)。</span><span class="sxs-lookup"><span data-stu-id="19e49-230">To start creating applications, go to [Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span></span>

## <a name="see-also"></a><span data-ttu-id="19e49-231">另請參閱</span><span class="sxs-lookup"><span data-stu-id="19e49-231">See Also</span></span>
* [<span data-ttu-id="19e49-232">備份 BizTalk 服務</span><span class="sxs-lookup"><span data-stu-id="19e49-232">Backup BizTalk Service</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [<span data-ttu-id="19e49-233">從備份還原 BizTalk 服務</span><span class="sxs-lookup"><span data-stu-id="19e49-233">Restore BizTalk Service from Backup</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [<span data-ttu-id="19e49-234">BizTalk 服務：開發人員、基本、標準和高級版本圖表</span><span class="sxs-lookup"><span data-stu-id="19e49-234">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [<span data-ttu-id="19e49-235">BizTalk 服務：使用 Azure 傳統入口網站進行佈建</span><span class="sxs-lookup"><span data-stu-id="19e49-235">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [<span data-ttu-id="19e49-236">BizTalk 服務：佈建狀態圖</span><span class="sxs-lookup"><span data-stu-id="19e49-236">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [<span data-ttu-id="19e49-237">BizTalk 服務：儀表板、監視和調整索引標籤</span><span class="sxs-lookup"><span data-stu-id="19e49-237">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [<span data-ttu-id="19e49-238">BizTalk 服務：節流</span><span class="sxs-lookup"><span data-stu-id="19e49-238">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [<span data-ttu-id="19e49-239">BizTalk 服務：簽發者名稱和簽發者金鑰</span><span class="sxs-lookup"><span data-stu-id="19e49-239">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [<span data-ttu-id="19e49-240">如何開始使用 Azure BizTalk 服務 SDK</span><span class="sxs-lookup"><span data-stu-id="19e49-240">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[BackupStatus]: ./media/biztalk-backup-restore/status-last-backup.png
[Restore]: ./media/biztalk-backup-restore/restore-ui.png
[AutomaticBU]: ./media/biztalk-backup-restore/AutomaticBU.png
[RestoreBizTalkService]: ./media/biztalk-backup-restore/RestoreBizTalkServiceWindow.png

