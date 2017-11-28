---
title: "aaaCreate 和還原 BizTalk 服務中的備份 |Microsoft 文件"
description: "BizTalk 服務包含備份與還原功能。 深入了解如何 toocreate 和還原備份，並決定備份的項目。 MABS，WABS"
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
ms.openlocfilehash: 32356ad870678fa5fd5bbbbf13d9377188f770a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-backup-and-restore"></a><span data-ttu-id="9e7c2-105">BizTalk 服務：備份與還原</span><span class="sxs-lookup"><span data-stu-id="9e7c2-105">BizTalk Services: Backup and Restore</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="9e7c2-106">Azure BizTalk 服務包含備份與還原功能。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-106">Azure BizTalk Services includes Backup and Restore capabilities.</span></span> <span data-ttu-id="9e7c2-107">本主題描述如何使用 toobackup 和還原 BizTalk 服務 hello Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-107">This topic describes how toobackup and restore BizTalk Services using hello Azure classic portal.</span></span>

<span data-ttu-id="9e7c2-108">您也可以備份 BizTalk 服務使用 hello [BizTalk 服務 REST API](http://go.microsoft.com/fwlink/p/?LinkID=325584)。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-108">You can also back up BizTalk Services using hello [BizTalk Services REST API](http://go.microsoft.com/fwlink/p/?LinkID=325584).</span></span> 

> [!NOTE]
> <span data-ttu-id="9e7c2-109">混合式連線無法備份，不論 hello 版本。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-109">Hybrid Connections are NOT backed up, regardless of hello Edition.</span></span> <span data-ttu-id="9e7c2-110">您必須重新建立混合式連接。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-110">You must recreate your hybrid connections.</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="9e7c2-111">開始之前</span><span class="sxs-lookup"><span data-stu-id="9e7c2-111">Before you Begin</span></span>
* <span data-ttu-id="9e7c2-112">備份與還原可能不適用於部分版本。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-112">Backup and Restore may not be available for all editions.</span></span> <span data-ttu-id="9e7c2-113">請參閱「 [BizTalk 服務：版本圖表](biztalk-editions-feature-chart.md)」(英文)。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-113">See [BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span></span>
* <span data-ttu-id="9e7c2-114">使用 hello Azure 傳統入口網站，您可以建立隨選備份，或建立排定的備份。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-114">Using hello Azure classic portal, you can create an On Demand backup or create a scheduled backup.</span></span> 
* <span data-ttu-id="9e7c2-115">備份內容可以是相同的 BizTalk 服務或 tooa 還原的 toohello 新的 BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-115">Backup content can be restored toohello same BizTalk Service or tooa new BizTalk Service.</span></span> <span data-ttu-id="9e7c2-116">toorestore hello BizTalk 服務使用相同的名稱，現有的 BizTalk 服務的 hello，必須先刪除的 hello 和 hello 名稱必須可供使用。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-116">toorestore hello BizTalk Service using hello same name, hello existing BizTalk Service must be deleted and hello name must be available.</span></span> <span data-ttu-id="9e7c2-117">刪除 BizTalk 服務之後，可能需要較長的時間比希望 hello 相同名稱 toobe 可用。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-117">After you delete a BizTalk Service, it can take longer time than wanted for hello same name toobe available.</span></span> <span data-ttu-id="9e7c2-118">如果您無法等候 hello 相同命名 toobe 可用，然後還原 tooa 新的 BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-118">If you cannot wait for hello same name toobe available, then restore tooa new BizTalk Service.</span></span>
* <span data-ttu-id="9e7c2-119">BizTalk 服務可以還原的 toohello 相同版本或更高版本。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-119">BizTalk Services can be restored toohello same edition or a higher edition.</span></span> <span data-ttu-id="9e7c2-120">不支援還原 BizTalk 服務 tooa、 當 hello 備份，從較低版本。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-120">Restoring BizTalk Services tooa lower edition, from when hello backup was taken, is not supported.</span></span>
  
    <span data-ttu-id="9e7c2-121">例如，使用的 hello Basic Edition 可還原備份 toohello Premium Edition。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-121">For example, a backup using hello Basic Edition can be restored toohello Premium Edition.</span></span> <span data-ttu-id="9e7c2-122">使用 Premium 版本不能的 hello 的備份還原 toohello Standard Edition。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-122">A backup using hello Premium Edition cannot be restored toohello Standard Edition.</span></span>
* <span data-ttu-id="9e7c2-123">hello EDI 控制編號會備份 toomaintain 連續性的 hello 控制編號。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-123">hello EDI Control numbers are backed up toomaintain continuity of hello control numbers.</span></span> <span data-ttu-id="9e7c2-124">如果訊息處理 hello 上次備份後，還原此備份的內容可能會導致重複的控制編號。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-124">If messages are processed after hello last backup, restoring this backup content can cause duplicate control numbers.</span></span>
* <span data-ttu-id="9e7c2-125">如果批次具有作用中的訊息，處理 hello 批次**之前**執行備份。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-125">If a batch has active messages, process hello batch **before** running a backup.</span></span> <span data-ttu-id="9e7c2-126">無論是建立隨選備份或排定備份，都不會儲存批次中的訊息。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-126">When creating a backup (as needed or scheduled), messages in batches are never stored.</span></span> 
  
    <span data-ttu-id="9e7c2-127">**建立備份時，如果批次中有作用中的訊息，則不會備份這些訊息，且這些訊息將會遺失。**</span><span class="sxs-lookup"><span data-stu-id="9e7c2-127">**If a backup is taken with active messages in a batch, these messages are not backed up and are therefore lost.**</span></span>
* <span data-ttu-id="9e7c2-128">選擇性： Hello BizTalk 服務入口網站，在停止的任何管理作業。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-128">Optional: In hello BizTalk Services Portal, stop any management operations.</span></span>

## <a name="create-a-backup"></a><span data-ttu-id="9e7c2-129">建立備份</span><span class="sxs-lookup"><span data-stu-id="9e7c2-129">Create a backup</span></span>
<span data-ttu-id="9e7c2-130">您隨時都可以建立備份，完全決由掌控。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-130">A backup can be taken at any time and is completely controlled by you.</span></span> <span data-ttu-id="9e7c2-131">此區段會列出 hello 步驟 toocreate 備份使用 hello Azure 傳統入口網站，包括：</span><span class="sxs-lookup"><span data-stu-id="9e7c2-131">This section lists hello steps toocreate backups using hello Azure classic portal, including:</span></span>

[<span data-ttu-id="9e7c2-132">隨選備份</span><span class="sxs-lookup"><span data-stu-id="9e7c2-132">On Demand backup</span></span>](#backupnow)

[<span data-ttu-id="9e7c2-133">排定備份</span><span class="sxs-lookup"><span data-stu-id="9e7c2-133">Schedule a backup</span></span>](#backupschedule)

#### <span data-ttu-id="9e7c2-134"><a name="backupnow"></a>隨選備份</span><span class="sxs-lookup"><span data-stu-id="9e7c2-134"><a name="backupnow"></a>On Demand backup</span></span>
1. <span data-ttu-id="9e7c2-135">在 hello Azure 傳統入口網站，選取  **BizTalk 服務**，，然後選取 hello 想 toobackup BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-135">In hello Azure classic portal, select **BizTalk Services**, and then select hello BizTalk Service you want toobackup.</span></span>
2. <span data-ttu-id="9e7c2-136">在 hello**儀表板**索引標籤上，選取**Back up** hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-136">In hello **Dashboard** tab, select **Back up** at hello bottom of hello page.</span></span>
3. <span data-ttu-id="9e7c2-137">輸入備份名稱。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-137">Enter a backup name.</span></span> <span data-ttu-id="9e7c2-138">例如，輸入 *myBizTalkService*BU*Date*。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-138">For example, enter *myBizTalkService*BU*Date*.</span></span>
4. <span data-ttu-id="9e7c2-139">選擇 blob 儲存體帳戶和選取 hello 核取記號 toostart hello 備份。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-139">Choose a blob storage account and select hello checkmark toostart hello backup.</span></span>

<span data-ttu-id="9e7c2-140">Hello 備份完成之後，您輸入的 hello 備份名稱的容器會建立 hello 儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-140">Once hello backup completes, a container with hello backup name you enter is created in hello storage account.</span></span> <span data-ttu-id="9e7c2-141">此容器包含 BizTalk 服務備份組態。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-141">This container contains your BizTalk Service backup configuration.</span></span>

#### <span data-ttu-id="9e7c2-142"><a name="backupschedule"></a>排定備份</span><span class="sxs-lookup"><span data-stu-id="9e7c2-142"><a name="backupschedule"></a>Schedule a backup</span></span>
1. <span data-ttu-id="9e7c2-143">在 hello Azure 傳統入口網站，選取  **BizTalk 服務**，選取 hello BizTalk 服務名稱，tooschedule hello 備份，然後再選取 hello**設定** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-143">In hello Azure classic portal, select **BizTalk Services**, select hello BizTalk Service name you want tooschedule hello backup, and then select hello **Configure** tab.</span></span>
2. <span data-ttu-id="9e7c2-144">設定 hello**備份狀態**太**自動**。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-144">Set hello **Backup Status** too**Automatic**.</span></span> 
3. <span data-ttu-id="9e7c2-145">選取 hello**儲存體帳戶**toostore hello 備份中，輸入 hello**頻率**toocreate hello 備份和多久 tookeep hello 備份 (**保留天數**):</span><span class="sxs-lookup"><span data-stu-id="9e7c2-145">Select hello **Storage Account** toostore hello backup, enter hello **Frequency** toocreate hello backups, and how long tookeep hello backups (**Retention Days**):</span></span>
   
    ![][AutomaticBU]
   
    <span data-ttu-id="9e7c2-146">**注意事項**</span><span class="sxs-lookup"><span data-stu-id="9e7c2-146">**Notes**</span></span>     
   
   * <span data-ttu-id="9e7c2-147">在**保留天數**，hello 保留期限必須大於 hello 備份頻率。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-147">In **Retention Days**, hello retention period must be greater than hello backup frequency.</span></span>
   * <span data-ttu-id="9e7c2-148">選取**永遠保留至少一個備份**，即使它已超出 hello 保留期限。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-148">Select **Always keep at least one backup**, even if it is past hello retention period.</span></span>
4. <span data-ttu-id="9e7c2-149">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-149">Select **Save**.</span></span>

<span data-ttu-id="9e7c2-150">已排定的備份工作執行時，它會建立 hello 您輸入的儲存體帳戶中的容器 （toostore 備份資料）。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-150">When a scheduled backup job runs, it creates a container (toostore backup data) in hello storage account you entered.</span></span> <span data-ttu-id="9e7c2-151">hello hello 容器名*BizTalk 服務名稱日期時間*。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-151">hello name of hello container is named *BizTalk Service Name-date-time*.</span></span> 

<span data-ttu-id="9e7c2-152">如果顯示 hello BizTalk 服務儀表板**失敗**狀態：</span><span class="sxs-lookup"><span data-stu-id="9e7c2-152">If hello BizTalk Service dashboard shows a **Failed** status:</span></span>

![上次排定的備份狀態][BackupStatus] 

<span data-ttu-id="9e7c2-154">hello 連結會開啟 hello toohelp 疑難排解管理服務的作業記錄。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-154">hello link opens hello Management Services Operation Logs toohelp troubleshoot.</span></span> <span data-ttu-id="9e7c2-155">請參閱 [BizTalk 服務：使用作業記錄進行疑難排解](http://go.microsoft.com/fwlink/p/?LinkId=391211)。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-155">See [BizTalk Services: Troubleshoot using operation logs](http://go.microsoft.com/fwlink/p/?LinkId=391211).</span></span>

## <a name="restore"></a><span data-ttu-id="9e7c2-156">還原</span><span class="sxs-lookup"><span data-stu-id="9e7c2-156">Restore</span></span>
<span data-ttu-id="9e7c2-157">您可以還原備份，從 Azure 傳統入口網站 hello 或 hello[還原 BizTalk 服務 REST API](http://go.microsoft.com/fwlink/p/?LinkID=325582)。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-157">You can restore backups from hello Azure classic portal or from hello [Restore BizTalk Service REST API](http://go.microsoft.com/fwlink/p/?LinkID=325582).</span></span> <span data-ttu-id="9e7c2-158">此區段會列出 hello 步驟 toorestore 使用 hello 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-158">This section lists hello steps toorestore using hello classic portal.</span></span>

#### <a name="before-restoring-a-backup"></a><span data-ttu-id="9e7c2-159">還原備份之前</span><span class="sxs-lookup"><span data-stu-id="9e7c2-159">Before restoring a backup</span></span>
* <span data-ttu-id="9e7c2-160">還原 BizTalk 服務時可以輸入新的追蹤、封存和監視儲存區。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-160">New tracking, archiving, and monitoring stores can be entered while restoring a BizTalk Service.</span></span>
* <span data-ttu-id="9e7c2-161">hello 還原相同 EDI 執行階段資料。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-161">hello same EDI Runtime data is restored.</span></span> <span data-ttu-id="9e7c2-162">hello EDI 執行階段備份會儲存 hello 控制編號。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-162">hello EDI Runtime backup stores hello control numbers.</span></span> <span data-ttu-id="9e7c2-163">還原的 hello 控制編號是從 hello hello 備份時的順序。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-163">hello restored control numbers are in sequence from hello time of hello backup.</span></span> <span data-ttu-id="9e7c2-164">如果訊息處理 hello 上次備份後，還原此備份的內容可能會導致重複的控制編號。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-164">If messages are processed after hello last backup, restoring this backup content can cause duplicate control numbers.</span></span>

#### <a name="restore-a-backup"></a><span data-ttu-id="9e7c2-165">還原備份</span><span class="sxs-lookup"><span data-stu-id="9e7c2-165">Restore a backup</span></span>
1. <span data-ttu-id="9e7c2-166">在 hello Azure 傳統入口網站，選取 **新增** > **應用程式服務** > **BizTalk 服務** > **還原**:</span><span class="sxs-lookup"><span data-stu-id="9e7c2-166">In hello Azure classic portal, select **New** > **App Services** > **BizTalk Service** > **Restore**:</span></span>
   
    ![還原備份][Restore]
2. <span data-ttu-id="9e7c2-168">在**備份 URL**選取 hello 資料夾圖示，依序展開 存放區 hello BizTalk 服務設定備份的 hello Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-168">In **Backup URL**, select hello folder icon and expand hello Azure storage account that stores hello BizTalk Service configuration backup.</span></span> <span data-ttu-id="9e7c2-169">展開 hello 容器，然後在 hello 右窗格中，選取 hello 對應備份.txt 檔案。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-169">Expand hello container and in hello right pane, select hello corresponding back up .txt file.</span></span> 
   <br/><br/>
   <span data-ttu-id="9e7c2-170">選取 [開啟] 。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-170">Select **Open**.</span></span>
3. <span data-ttu-id="9e7c2-171">在 hello**還原 BizTalk 服務**頁面上，輸入**BizTalk 服務名稱**並確認 hello**網域 URL**， **Edition**，和**區域**的 hello 還原 BizTalk 服務。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-171">On hello **Restore BizTalk Service** page, enter a **BizTalk Service Name** and verify hello **Domain URL**, **Edition**, and **Region** for hello restored BizTalk Service.</span></span> <span data-ttu-id="9e7c2-172">**建立新的 SQL 資料庫執行個體**追蹤資料庫的 hello:</span><span class="sxs-lookup"><span data-stu-id="9e7c2-172">**Create a new SQL database instance** for hello tracking database:</span></span>
   
    ![][RestoreBizTalkService]
   
    <span data-ttu-id="9e7c2-173">選取 hello 下一步 箭號。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-173">Select hello next arrow.</span></span>
4. <span data-ttu-id="9e7c2-174">確認 hello hello SQL 資料庫名稱，輸入該伺服器 hello 實體伺服器 hello SQL 資料庫建立的位置和使用者名稱/密碼。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-174">Verify hello name of hello SQL database, enter hello physical server where hello SQL database will be created, and a username/password for that server.</span></span>

    <span data-ttu-id="9e7c2-175">如果您想 tooconfigure hello SQL 資料庫版本、 大小和其他屬性，選取**設定進階資料庫設定**。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-175">If you want tooconfigure hello SQL database edition, size, and other properties, select  **Configure Advanced Database Settings**.</span></span> 

    <span data-ttu-id="9e7c2-176">選取 hello 下一步 箭號。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-176">Select hello next arrow.</span></span>

1. <span data-ttu-id="9e7c2-177">建立新的儲存體帳戶，或輸入 hello BizTalk 服務現有的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-177">Create a new storage account or enter an existing storage account for hello BizTalk Service.</span></span>
2. <span data-ttu-id="9e7c2-178">選取 hello 核取記號 toostart hello 還原。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-178">Select hello checkmark toostart hello restore.</span></span>

<span data-ttu-id="9e7c2-179">Hello 還原已成功完成之後，新的 BizTalk 服務會列在 hello Azure 傳統入口網站中的 hello BizTalk 服務頁面上的暫止狀態。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-179">Once hello restoration successfully completes, a new BizTalk Service is listed in a suspended state on hello BizTalk Services page in hello Azure classic portal.</span></span>

### <span data-ttu-id="9e7c2-180"><a name="postrestore"></a>還原備份之後</span><span class="sxs-lookup"><span data-stu-id="9e7c2-180"><a name="postrestore"></a>After restoring a backup</span></span>
<span data-ttu-id="9e7c2-181">hello BizTalk 服務系統一定會還原在**Suspended**狀態。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-181">hello BizTalk Service is always restored in a **Suspended** state.</span></span> <span data-ttu-id="9e7c2-182">處於此狀態，您可以進行任何組態變更之前 hello 新環境正常運作，包括：</span><span class="sxs-lookup"><span data-stu-id="9e7c2-182">In this state, you can make any configuration changes before hello new environment is functional, including:</span></span>

* <span data-ttu-id="9e7c2-183">如果您建立 BizTalk 服務使用 hello Azure BizTalk 服務 SDK 的應用程式，您可能需要還原的 hello 環境與這些應用程式 toowork tootooupdate hello 存取控制 (ACS) 認證。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-183">If you created BizTalk Service applications using hello Azure BizTalk Services SDK, you may need tootooupdate hello Access Control (ACS) credentials in those applications toowork with hello restored environment.</span></span>
* <span data-ttu-id="9e7c2-184">您還原 BizTalk 服務 tooreplicate 現有的 BizTalk 服務環境。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-184">You restore a BizTalk Service tooreplicate an existing BizTalk Service environment.</span></span> <span data-ttu-id="9e7c2-185">在此情況下，如果沒有合約 hello 原始 BizTalk 服務入口網站中設定使用 FTP 來源 資料夾中，您可能需要 tooupdate hello 最近還原環境 toouse 不同的來源 FTP 資料夾中的 hello 協議。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-185">In this situation, if there are agreements configured in hello original BizTalk Services portal that use a source FTP folder, you may need tooupdate hello agreements in hello newly restored environment toouse a different source FTP folder.</span></span> <span data-ttu-id="9e7c2-186">否則，可能有兩個不同的協議嘗試 toopull hello 相同的訊息。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-186">Otherwise, there may be two different agreements trying toopull hello same message.</span></span>
* <span data-ttu-id="9e7c2-187">如果您還原 toohave 多個 BizTalk 服務環境，請確定目標 hello Visual Studio 應用程式、 PowerShell 指令程式、 REST Api 或交易夥伴管理 OM Api 中的 hello 正確環境。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-187">If you restored toohave multiple BizTalk Service environments, make sure you target hello correct environment in hello Visual Studio applications, PowerShell cmdlets, REST APIs, or Trading Partner Management OM APIs.</span></span>
* <span data-ttu-id="9e7c2-188">它是很好的作法 tooconfigure 自動化上的備份 hello 最近還原 BizTalk 服務的環境。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-188">It's a good practice tooconfigure automated backups on hello newly restored BizTalk Service environment.</span></span>

<span data-ttu-id="9e7c2-189">toostart hello BizTalk 服務在 hello Azure 傳統入口網站，選取 hello 還原 BizTalk 服務，然後選取**繼續**hello 工作列中。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-189">toostart hello BizTalk Service in hello Azure classic portal, select hello restored BizTalk Service and select **Resume** in hello task bar.</span></span> 

## <a name="what-gets-backed-up"></a><span data-ttu-id="9e7c2-190">備份什麼項目</span><span class="sxs-lookup"><span data-stu-id="9e7c2-190">What gets backed up</span></span>
<span data-ttu-id="9e7c2-191">建立備份時，hello 下列項目會備份：</span><span class="sxs-lookup"><span data-stu-id="9e7c2-191">When a backup is created, hello following items are backed up:</span></span>

<table border="1"> 
<tr bgcolor="FAF9F9">
<th> </th>
<TH><span data-ttu-id="9e7c2-192">備份的項目</span><span class="sxs-lookup"><span data-stu-id="9e7c2-192">Items backed up</span></span></TH> 
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="9e7c2-193">
 <strong>Azure BizTalk 服務入口網站</strong></span><span class="sxs-lookup"><span data-stu-id="9e7c2-193">
 <strong>Azure BizTalk Services Portal</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="9e7c2-194">組態和執行階段</span><span class="sxs-lookup"><span data-stu-id="9e7c2-194">Configuration and Runtime</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="9e7c2-195">夥伴和設定檔詳細資料</span><span class="sxs-lookup"><span data-stu-id="9e7c2-195">Partner and profile details</span></span></li>
<li><span data-ttu-id="9e7c2-196">夥伴協議</span><span class="sxs-lookup"><span data-stu-id="9e7c2-196">Partner Agreements</span></span></li>
<li><span data-ttu-id="9e7c2-197">已部署的自訂組件</span><span class="sxs-lookup"><span data-stu-id="9e7c2-197">Custom assemblies deployed</span></span></li>
<li><span data-ttu-id="9e7c2-198">已部署的橋接器</span><span class="sxs-lookup"><span data-stu-id="9e7c2-198">Bridges deployed</span></span></li>
<li><span data-ttu-id="9e7c2-199">憑證</span><span class="sxs-lookup"><span data-stu-id="9e7c2-199">Certificates</span></span></li>
<li><span data-ttu-id="9e7c2-200">已部署的轉換</span><span class="sxs-lookup"><span data-stu-id="9e7c2-200">Transforms deployed</span></span></li>
<li><span data-ttu-id="9e7c2-201">管線</span><span class="sxs-lookup"><span data-stu-id="9e7c2-201">Pipelines</span></span></li>
<li><span data-ttu-id="9e7c2-202">建立及儲存於 hello BizTalk 服務入口網站的範本</span><span class="sxs-lookup"><span data-stu-id="9e7c2-202">Templates created and saved in hello BizTalk Services Portal</span></span></li>
<li><span data-ttu-id="9e7c2-203">X12 ST01 和 GS01 對應</span><span class="sxs-lookup"><span data-stu-id="9e7c2-203">X12 ST01 and GS01 mappings</span></span></li>
<li><span data-ttu-id="9e7c2-204">控制編號 (EDI)</span><span class="sxs-lookup"><span data-stu-id="9e7c2-204">Control numbers (EDI)</span></span></li>
<li><span data-ttu-id="9e7c2-205">AS2 訊息 MIC 值</span><span class="sxs-lookup"><span data-stu-id="9e7c2-205">AS2 Message MIC values</span></span></li>
</ul>
</td>
</tr> 

<tr>
<td colspan="2"><span data-ttu-id="9e7c2-206">
 <strong>Azure BizTalk 服務</strong></span><span class="sxs-lookup"><span data-stu-id="9e7c2-206">
 <strong>Azure BizTalk Service</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="9e7c2-207">SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="9e7c2-207">SSL Certificate</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="9e7c2-208">SSL 憑證資料</span><span class="sxs-lookup"><span data-stu-id="9e7c2-208">SSL Certificate Data</span></span></li>
<li><span data-ttu-id="9e7c2-209">SSL 憑證密碼</span><span class="sxs-lookup"><span data-stu-id="9e7c2-209">SSL Certificate Password</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td><span data-ttu-id="9e7c2-210">BizTalk 服務設定</span><span class="sxs-lookup"><span data-stu-id="9e7c2-210">BizTalk Service Settings</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="9e7c2-211">調整單位計數</span><span class="sxs-lookup"><span data-stu-id="9e7c2-211">Scale unit count</span></span></li>
<li><span data-ttu-id="9e7c2-212">版本</span><span class="sxs-lookup"><span data-stu-id="9e7c2-212">Edition</span></span></li>
<li><span data-ttu-id="9e7c2-213">產品版本</span><span class="sxs-lookup"><span data-stu-id="9e7c2-213">Product Version</span></span></li>
<li><span data-ttu-id="9e7c2-214">區域/資料中心</span><span class="sxs-lookup"><span data-stu-id="9e7c2-214">Region/Datacenter</span></span></li>
<li><span data-ttu-id="9e7c2-215">存取控制服務 (ACS) 命名空間和金鑰</span><span class="sxs-lookup"><span data-stu-id="9e7c2-215">Access Control Service (ACS) namespace and key</span></span></li>
<li><span data-ttu-id="9e7c2-216">追蹤資料庫連接字串</span><span class="sxs-lookup"><span data-stu-id="9e7c2-216">Tracking database connection string</span></span></li>
<li><span data-ttu-id="9e7c2-217">封存儲存體帳戶連接字串</span><span class="sxs-lookup"><span data-stu-id="9e7c2-217">Archiving Storage account connection string</span></span></li>
<li><span data-ttu-id="9e7c2-218">監視儲存體帳戶連接字串</span><span class="sxs-lookup"><span data-stu-id="9e7c2-218">Monitoring storage account connection string</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="9e7c2-219">
 <strong>其他項目</strong></span><span class="sxs-lookup"><span data-stu-id="9e7c2-219">
 <strong>Additional Items</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="9e7c2-220">追蹤資料庫</span><span class="sxs-lookup"><span data-stu-id="9e7c2-220">Tracking Database</span></span></td> 
<td><span data-ttu-id="9e7c2-221">建立 hello BizTalk 服務時，會輸入 hello 追蹤資料庫的詳細資訊，包括 hello Azure SQL Database 伺服器和 hello 追蹤資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-221">When hello BizTalk Service is created, hello Tracking Database details are entered, including hello Azure SQL Database Server and hello Tracking Database name.</span></span> <span data-ttu-id="9e7c2-222">hello 追蹤資料庫不會自動備份。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-222">hello Tracking Database is not automatically backed up.</span></span>
<br/><br/><span data-ttu-id="9e7c2-223">
<strong>重要</strong></span><span class="sxs-lookup"><span data-stu-id="9e7c2-223">
<strong>Important</strong></span></span><br/>
<span data-ttu-id="9e7c2-224">如果 hello 追蹤資料庫刪除與 hello 復原的資料庫需求，必須存在先前的備份。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-224">If hello Tracking Database is deleted and hello database needs recovered, a previous backup must exist.</span></span> <span data-ttu-id="9e7c2-225">如果備份不存在，便無法復原 hello 追蹤資料庫和其資料。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-225">If a backup does not exist, hello Tracking Database and its data are not recoverable.</span></span> <span data-ttu-id="9e7c2-226">在此情況下，建立新的追蹤資料庫以 hello 相同的資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-226">In this situation, create a new Tracking Database with hello same database name.</span></span> <span data-ttu-id="9e7c2-227">建議採用地理複寫。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-227">Geo-Replication is recommended.</span></span></td>
</tr> 
</table>

## <a name="next"></a><span data-ttu-id="9e7c2-228">下一步</span><span class="sxs-lookup"><span data-stu-id="9e7c2-228">Next</span></span>
<span data-ttu-id="9e7c2-229">toocreate Azure BizTalk 服務中太 hello Azure 傳統入口網站中，移至[BizTalk 服務： 佈建使用 Azure 傳統入口網站](http://go.microsoft.com/fwlink/p/?LinkID=302280)。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-229">toocreate Azure BizTalk Services in hello Azure classic portal, go too[BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280).</span></span> <span data-ttu-id="9e7c2-230">建立應用程式，請跳過 toostart[Azure BizTalk 服務](http://go.microsoft.com/fwlink/p/?LinkID=235197)。</span><span class="sxs-lookup"><span data-stu-id="9e7c2-230">toostart creating applications, go too[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span></span>

## <a name="see-also"></a><span data-ttu-id="9e7c2-231">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9e7c2-231">See Also</span></span>
* [<span data-ttu-id="9e7c2-232">備份 BizTalk 服務</span><span class="sxs-lookup"><span data-stu-id="9e7c2-232">Backup BizTalk Service</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [<span data-ttu-id="9e7c2-233">從備份還原 BizTalk 服務</span><span class="sxs-lookup"><span data-stu-id="9e7c2-233">Restore BizTalk Service from Backup</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [<span data-ttu-id="9e7c2-234">BizTalk 服務：開發人員、基本、標準和高級版本圖表</span><span class="sxs-lookup"><span data-stu-id="9e7c2-234">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [<span data-ttu-id="9e7c2-235">BizTalk 服務：使用 Azure 傳統入口網站進行佈建</span><span class="sxs-lookup"><span data-stu-id="9e7c2-235">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [<span data-ttu-id="9e7c2-236">BizTalk 服務：佈建狀態圖</span><span class="sxs-lookup"><span data-stu-id="9e7c2-236">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [<span data-ttu-id="9e7c2-237">BizTalk 服務：儀表板、監視和調整索引標籤</span><span class="sxs-lookup"><span data-stu-id="9e7c2-237">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [<span data-ttu-id="9e7c2-238">BizTalk 服務：節流</span><span class="sxs-lookup"><span data-stu-id="9e7c2-238">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [<span data-ttu-id="9e7c2-239">BizTalk 服務：簽發者名稱和簽發者金鑰</span><span class="sxs-lookup"><span data-stu-id="9e7c2-239">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [<span data-ttu-id="9e7c2-240">開始使用我要如何 hello Azure BizTalk 服務 SDK</span><span class="sxs-lookup"><span data-stu-id="9e7c2-240">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[BackupStatus]: ./media/biztalk-backup-restore/status-last-backup.png
[Restore]: ./media/biztalk-backup-restore/restore-ui.png
[AutomaticBU]: ./media/biztalk-backup-restore/AutomaticBU.png
[RestoreBizTalkService]: ./media/biztalk-backup-restore/RestoreBizTalkServiceWindow.png

