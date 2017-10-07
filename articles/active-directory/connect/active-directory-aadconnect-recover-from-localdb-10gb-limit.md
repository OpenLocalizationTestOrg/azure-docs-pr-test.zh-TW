---
title: "Azure AD Connect： 如何限制來自 LocalDB 10GB toorecover 問題 |Microsoft 文件"
description: "本主題描述如何 toorecover Azure AD Connect 同步處理服務遇到 LocalDB 10 GB 時限制問題。"
services: active-directory
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 41d081af-ed89-4e17-be34-14f7e80ae358
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: 7b8ce6e19b68837639017bb0315eda4b924d525a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-how-toorecover-from-localdb-10-gb-limit"></a><span data-ttu-id="78dee-103">Azure AD Connect： 如何 toorecover 從 LocalDB 10 GB 的限制</span><span class="sxs-lookup"><span data-stu-id="78dee-103">Azure AD Connect: How toorecover from LocalDB 10-GB limit</span></span>
<span data-ttu-id="78dee-104">Azure AD Connect 需要 SQL Server 資料庫 toostore 識別資料。</span><span class="sxs-lookup"><span data-stu-id="78dee-104">Azure AD Connect requires a SQL Server database toostore identity data.</span></span> <span data-ttu-id="78dee-105">您可以使用 SQL Server 2012 Express LocalDB 安裝 Azure AD Connect 與 hello 預設值，或使用完整的 SQL。</span><span class="sxs-lookup"><span data-stu-id="78dee-105">You can either use hello default SQL Server 2012 Express LocalDB installed with Azure AD Connect or use your own full SQL.</span></span> <span data-ttu-id="78dee-106">SQL Server Express 會實行 10 GB 的大小限制。</span><span class="sxs-lookup"><span data-stu-id="78dee-106">SQL Server Express imposes a 10-GB size limit.</span></span> <span data-ttu-id="78dee-107">使用 LocalDB 且達到這個限制時，Azure AD Connect 同步處理服務無法再啟動或正確同步處理。</span><span class="sxs-lookup"><span data-stu-id="78dee-107">When using LocalDB and this limit is reached, Azure AD Connect Synchronization Service can no longer start or synchronize properly.</span></span> <span data-ttu-id="78dee-108">本文章提供 hello 復原步驟。</span><span class="sxs-lookup"><span data-stu-id="78dee-108">This article provides hello recovery steps.</span></span>

## <a name="symptoms"></a><span data-ttu-id="78dee-109">徵兆</span><span class="sxs-lookup"><span data-stu-id="78dee-109">Symptoms</span></span>
<span data-ttu-id="78dee-110">有兩個常見的徵兆︰</span><span class="sxs-lookup"><span data-stu-id="78dee-110">There are two common symptoms:</span></span>

* <span data-ttu-id="78dee-111">Azure AD Connect 同步處理服務**執行**但無法與 toosynchronize *"停止-資料庫-磁碟-full"*錯誤。</span><span class="sxs-lookup"><span data-stu-id="78dee-111">Azure AD Connect Synchronization Service **is running** but fails toosynchronize with *“stopped-database-disk-full”* error.</span></span>

* <span data-ttu-id="78dee-112">Azure AD Connect 同步處理服務**是無法 toostart**。</span><span class="sxs-lookup"><span data-stu-id="78dee-112">Azure AD Connect Synchronization Service **is unable toostart**.</span></span> <span data-ttu-id="78dee-113">當您嘗試 toostart hello 服務時，它會因 6323 事件和錯誤訊息*"hello 伺服器發生錯誤，因為 SQL Server 已用完磁碟空間。 」*</span><span class="sxs-lookup"><span data-stu-id="78dee-113">When you attempt toostart hello service, it fails with event 6323 and error message *"hello server encountered an error because SQL Server is out of disk space."*</span></span>

## <a name="short-term-recovery-steps"></a><span data-ttu-id="78dee-114">短期復原步驟</span><span class="sxs-lookup"><span data-stu-id="78dee-114">Short-term recovery steps</span></span>
<span data-ttu-id="78dee-115">本節提供所需的 Azure AD Connect 同步處理服務 tooresume 作業 hello 步驟 tooreclaim DB 空間。</span><span class="sxs-lookup"><span data-stu-id="78dee-115">This section provides hello steps tooreclaim DB space required for Azure AD Connect Synchronization Service tooresume operation.</span></span> <span data-ttu-id="78dee-116">hello 步驟包括：</span><span class="sxs-lookup"><span data-stu-id="78dee-116">hello steps include:</span></span>
1. [<span data-ttu-id="78dee-117">判斷 hello 同步處理服務狀態</span><span class="sxs-lookup"><span data-stu-id="78dee-117">Determine hello Synchronization Service status</span></span>](#determine-the-synchronization-service-status)
2. [<span data-ttu-id="78dee-118">壓縮 hello 資料庫</span><span class="sxs-lookup"><span data-stu-id="78dee-118">Shrink hello database</span></span>](#shrink-the-database)
3. [<span data-ttu-id="78dee-119">刪除執行記錄資料</span><span class="sxs-lookup"><span data-stu-id="78dee-119">Delete run history data</span></span>](#delete-run-history-data)
4. [<span data-ttu-id="78dee-120">縮短執行歷程記錄資料的保留期間</span><span class="sxs-lookup"><span data-stu-id="78dee-120">Shorten retention period for run history data</span></span>](#shorten-retention-period-for-run-history-data)

### <a name="determine-hello-synchronization-service-status"></a><span data-ttu-id="78dee-121">判斷 hello 同步處理服務狀態</span><span class="sxs-lookup"><span data-stu-id="78dee-121">Determine hello Synchronization Service status</span></span>
<span data-ttu-id="78dee-122">首先，判斷是否 hello 同步處理服務仍在執行或無法：</span><span class="sxs-lookup"><span data-stu-id="78dee-122">First, determine whether hello Synchronization Service is still running or not:</span></span>

1. <span data-ttu-id="78dee-123">登入 tooyour Azure AD Connect 的伺服器系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="78dee-123">Log in tooyour Azure AD Connect server as administrator.</span></span>

2. <span data-ttu-id="78dee-124">跳過**服務控制管理員**。</span><span class="sxs-lookup"><span data-stu-id="78dee-124">Go too**Service Control Manager**.</span></span>

3. <span data-ttu-id="78dee-125">檢查 hello 狀態**Microsoft Azure AD Sync**。</span><span class="sxs-lookup"><span data-stu-id="78dee-125">Check hello status of **Microsoft Azure AD Sync**.</span></span>


4. <span data-ttu-id="78dee-126">如果它正在執行，不要停止或重新啟動 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="78dee-126">If it is running, do not stop or restart hello service.</span></span> <span data-ttu-id="78dee-127">略過[壓縮 hello 資料庫](#shrink-the-database)步驟並移過[刪除執行記錄資料](#delete-run-history-data)步驟。</span><span class="sxs-lookup"><span data-stu-id="78dee-127">Skip [Shrink hello database](#shrink-the-database) step and go too[Delete run history data](#delete-run-history-data) step.</span></span>

5. <span data-ttu-id="78dee-128">如果未執行，請嘗試 toostart hello 服務。</span><span class="sxs-lookup"><span data-stu-id="78dee-128">If it is not running, try toostart hello service.</span></span> <span data-ttu-id="78dee-129">如果 hello 服務成功啟動，請略過[壓縮 hello 資料庫](#shrink-the-database)步驟並移過[刪除執行記錄資料](#delete-run-history-data)步驟。</span><span class="sxs-lookup"><span data-stu-id="78dee-129">If hello service starts successfully, skip [Shrink hello database](#shrink-the-database) step and go too[Delete run history data](#delete-run-history-data) step.</span></span> <span data-ttu-id="78dee-130">否則，請繼續[壓縮 hello 資料庫](#shrink-the-database)步驟。</span><span class="sxs-lookup"><span data-stu-id="78dee-130">Otherwise, continue with [Shrink hello database](#shrink-the-database) step.</span></span>

### <a name="shrink-hello-database"></a><span data-ttu-id="78dee-131">壓縮 hello 資料庫</span><span class="sxs-lookup"><span data-stu-id="78dee-131">Shrink hello database</span></span>
<span data-ttu-id="78dee-132">使用 hello 壓縮作業 toofree 向上足夠 DB 空間 toostart hello 同步處理服務。</span><span class="sxs-lookup"><span data-stu-id="78dee-132">Use hello Shrink operation toofree up enough DB space toostart hello Synchronization Service.</span></span> <span data-ttu-id="78dee-133">它會釋放資料庫空間 hello 資料庫中移除空白字元。</span><span class="sxs-lookup"><span data-stu-id="78dee-133">It frees up DB space by removing whitespaces in hello database.</span></span> <span data-ttu-id="78dee-134">這個步驟是最佳方式，因為不保證一律可以復原空間。</span><span class="sxs-lookup"><span data-stu-id="78dee-134">This step is best-effort as it is not guaranteed that you can always recover space.</span></span> <span data-ttu-id="78dee-135">進一步了解壓縮作業 toolearn 閱讀此文章[壓縮資料庫](https://msdn.microsoft.com/library/ms189035.aspx)。</span><span class="sxs-lookup"><span data-stu-id="78dee-135">toolearn more about Shrink operation, read this article [Shrink a database](https://msdn.microsoft.com/library/ms189035.aspx).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="78dee-136">如果您可以取得 hello 同步處理服務 toorun，略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="78dee-136">Skip this step if you can get hello Synchronization Service toorun.</span></span> <span data-ttu-id="78dee-137">因為它會導致因為 tooincreased 片段 toopoor 效能不建議 tooshrink hello SQL DB。</span><span class="sxs-lookup"><span data-stu-id="78dee-137">It is not recommended tooshrink hello SQL DB as it can lead toopoor performance due tooincreased fragmentation.</span></span>

<span data-ttu-id="78dee-138">建立 Azure AD Connect 的 hello 資料庫 hello 名稱**ADSync**。</span><span class="sxs-lookup"><span data-stu-id="78dee-138">hello name of hello database created for Azure AD Connect is **ADSync**.</span></span> <span data-ttu-id="78dee-139">tooperform 壓縮作業，您必須登入為 hello sysadmin 或 hello 資料庫的 DBO。</span><span class="sxs-lookup"><span data-stu-id="78dee-139">tooperform a Shrink operation, you must log in either as hello sysadmin or DBO of hello database.</span></span> <span data-ttu-id="78dee-140">Azure AD Connect 在安裝期間，下列帳戶的 hello 被授與系統管理員權限：</span><span class="sxs-lookup"><span data-stu-id="78dee-140">During Azure AD Connect installation, hello following accounts are granted sysadmin rights:</span></span>
* <span data-ttu-id="78dee-141">本機系統管理員</span><span class="sxs-lookup"><span data-stu-id="78dee-141">Local Administrators</span></span>
* <span data-ttu-id="78dee-142">hello 使用者帳戶已使用的 toorun Azure AD Connect 的安裝。</span><span class="sxs-lookup"><span data-stu-id="78dee-142">hello user account that was used toorun Azure AD Connect installation.</span></span>
* <span data-ttu-id="78dee-143">hello 做為 hello 運作的 Azure AD Connect 同步處理服務內容的同步處理服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="78dee-143">hello Sync Service account that is used as hello operating context of Azure AD Connect Synchronization Service.</span></span>
* <span data-ttu-id="78dee-144">本機群組已在安裝期間建立的 ADSyncAdmins hello。</span><span class="sxs-lookup"><span data-stu-id="78dee-144">hello local group ADSyncAdmins that was created during installation.</span></span>

1. <span data-ttu-id="78dee-145">藉由複製 hello 資料庫**ADSync.mdf**和**ADSync_log.ldf**檔案位於`%ProgramFiles%\program files\Microsoft Azure AD Sync\Data`tooa 安全的位置。</span><span class="sxs-lookup"><span data-stu-id="78dee-145">Back up hello database by copying **ADSync.mdf** and **ADSync_log.ldf** files located under `%ProgramFiles%\program files\Microsoft Azure AD Sync\Data` tooa safe location.</span></span>

2. <span data-ttu-id="78dee-146">啟動新的 PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="78dee-146">Start a new PowerShell session.</span></span>

3. <span data-ttu-id="78dee-147">瀏覽 toofolder `%ProgramFiles%\Program Files\Microsoft SQL Server\110\Tools\Binn`。</span><span class="sxs-lookup"><span data-stu-id="78dee-147">Navigate toofolder `%ProgramFiles%\Program Files\Microsoft SQL Server\110\Tools\Binn`.</span></span>

4. <span data-ttu-id="78dee-148">啟動**sqlcmd**公用程式執行 hello 命令`./SQLCMD.EXE -S “(localdb)\.\ADSync” -U <Username> -P <Password>`、 使用 hello 認證的 sysadmin 或 hello 資料庫 DBO。</span><span class="sxs-lookup"><span data-stu-id="78dee-148">Start **sqlcmd** utility by running hello command `./SQLCMD.EXE -S “(localdb)\.\ADSync” -U <Username> -P <Password>`, using hello credential of a sysadmin or hello database DBO.</span></span>

5. <span data-ttu-id="78dee-149">在提示字元中 sqlcmd hello tooshrink hello 資料庫 (1 >)，輸入`DBCC Shrinkdatabase(ADSync,1);`，後面接著`GO`hello 下一行中。</span><span class="sxs-lookup"><span data-stu-id="78dee-149">tooshrink hello database, at hello sqlcmd prompt (1>), enter `DBCC Shrinkdatabase(ADSync,1);`, followed by `GO` in hello next line.</span></span>

6. <span data-ttu-id="78dee-150">如果 hello 作業成功，請再試一次 toostart hello 同步處理服務。</span><span class="sxs-lookup"><span data-stu-id="78dee-150">If hello operation is successful, try toostart hello Synchronization Service again.</span></span> <span data-ttu-id="78dee-151">如果您可以啟動 hello 同步處理服務，請移至太[刪除執行記錄資料](#delete-run-history-data)步驟。</span><span class="sxs-lookup"><span data-stu-id="78dee-151">If you can start hello Synchronization Service, go too[Delete run history data](#delete-run-history-data) step.</span></span> <span data-ttu-id="78dee-152">否則請連絡支援人員。</span><span class="sxs-lookup"><span data-stu-id="78dee-152">If not, contact Support.</span></span>

### <a name="delete-run-history-data"></a><span data-ttu-id="78dee-153">刪除執行記錄資料</span><span class="sxs-lookup"><span data-stu-id="78dee-153">Delete run history data</span></span>
<span data-ttu-id="78dee-154">根據預設，Azure AD Connect 會向上 tooseven 天份的執行歷程記錄資料保留。</span><span class="sxs-lookup"><span data-stu-id="78dee-154">By default, Azure AD Connect retains up tooseven days’ worth of run history data.</span></span> <span data-ttu-id="78dee-155">在此步驟中，我們會刪除 hello 執行歷程記錄資料 tooreclaim DB 空間，讓 Azure AD Connect 同步處理服務可以啟動同步處理一次。</span><span class="sxs-lookup"><span data-stu-id="78dee-155">In this step, we delete hello run history data tooreclaim DB space so that Azure AD Connect Synchronization Service can start syncing again.</span></span>

1.  <span data-ttu-id="78dee-156">啟動**同步處理服務管理員**移 tooSTART → 所同步處理服務。</span><span class="sxs-lookup"><span data-stu-id="78dee-156">Start **Synchronization Service Manager** by going tooSTART → Synchronization Service.</span></span>

2.  <span data-ttu-id="78dee-157">移 toohello**作業** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="78dee-157">Go toohello **Operations** tab.</span></span>

3.  <span data-ttu-id="78dee-158">選取 [動作] 下方的 [清除執行]...</span><span class="sxs-lookup"><span data-stu-id="78dee-158">Under **Actions**, select **Clear Runs**…</span></span>

4.  <span data-ttu-id="78dee-159">您可以選擇 [清除所有執行] 或 [清除之前的執行...]**<date>** 選項。</span><span class="sxs-lookup"><span data-stu-id="78dee-159">You can either choose **Clear all runs** or **Clear runs before… <date>** option.</span></span> <span data-ttu-id="78dee-160">建議您一開始先清除執行超過兩天的歷程記錄資料。</span><span class="sxs-lookup"><span data-stu-id="78dee-160">It is recommended that you start by clearing run history data that are older than two days.</span></span> <span data-ttu-id="78dee-161">如果您繼續 toorun 進入資料庫大小問題，然後選擇 hello**清除所有執行**選項。</span><span class="sxs-lookup"><span data-stu-id="78dee-161">If you continue toorun into DB size issue, then choose hello **Clear all runs** option.</span></span>

### <a name="shorten-retention-period-for-run-history-data"></a><span data-ttu-id="78dee-162">縮短執行歷程記錄資料的保留期間</span><span class="sxs-lookup"><span data-stu-id="78dee-162">Shorten retention period for run history data</span></span>
<span data-ttu-id="78dee-163">這個步驟是 tooreduce hello 可能性的多個同步處理循環之後執行 hello 10 GB 限制的問題。</span><span class="sxs-lookup"><span data-stu-id="78dee-163">This step is tooreduce hello likelihood of running into hello 10-GB limit issue after multiple sync cycles.</span></span>

1. <span data-ttu-id="78dee-164">開啟新的 PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="78dee-164">Open a new PowerShell session.</span></span>

2. <span data-ttu-id="78dee-165">執行`Get-ADSyncScheduler`並記下 hello PurgeRunHistoryInterval 屬性，指定 hello 目前保留期限。</span><span class="sxs-lookup"><span data-stu-id="78dee-165">Run `Get-ADSyncScheduler` and take note of hello PurgeRunHistoryInterval property, which specifies hello current retention period.</span></span>

3. <span data-ttu-id="78dee-166">執行`Set-ADSyncScheduler -PurgeRunHistoryInterval 2.00:00:00`tooset hello 保留週期 tootwo 天數。</span><span class="sxs-lookup"><span data-stu-id="78dee-166">Run `Set-ADSyncScheduler -PurgeRunHistoryInterval 2.00:00:00` tooset hello retention period tootwo days.</span></span> <span data-ttu-id="78dee-167">調整為適當的 hello 保留期限。</span><span class="sxs-lookup"><span data-stu-id="78dee-167">Adjust hello retention period as appropriate.</span></span>

## <a name="long-term-solution--migrate-toofull-sql"></a><span data-ttu-id="78dee-168">長期解決方案 – 移轉 toofull SQL</span><span class="sxs-lookup"><span data-stu-id="78dee-168">Long-term solution – Migrate toofull SQL</span></span>
<span data-ttu-id="78dee-169">一般而言，稍有差異，10 GB 的資料庫大小不再足以讓 Azure AD Connect toosynchronize hello 問題是您在內部部署 Active Directory tooAzure AD。</span><span class="sxs-lookup"><span data-stu-id="78dee-169">In general, hello issue is indicative that 10-GB database size is no longer sufficient for Azure AD Connect toosynchronize your on-premises Active Directory tooAzure AD.</span></span> <span data-ttu-id="78dee-170">建議您先切換 toousing hello 完整版的 SQL server。</span><span class="sxs-lookup"><span data-stu-id="78dee-170">It is recommended that you switch toousing hello full version of SQL server.</span></span> <span data-ttu-id="78dee-171">您無法直接將 hello hello 完整版本的 SQL 資料庫 hello LocalDB 的現有 Azure AD Connect 部署取代。</span><span class="sxs-lookup"><span data-stu-id="78dee-171">You cannot directly replace hello LocalDB of an existing Azure AD Connect deployment with hello database of hello full version of SQL.</span></span> <span data-ttu-id="78dee-172">相反地，您必須部署新的 Azure AD Connect 伺服器 hello 完整版本的 SQL。</span><span class="sxs-lookup"><span data-stu-id="78dee-172">Instead, you must deploy a new Azure AD Connect server with hello full version of SQL.</span></span> <span data-ttu-id="78dee-173">建議您迴旋移轉 hello 新 Azure AD Connect 的伺服器 （搭配 SQL DB) 做為執行的伺服器，下一步 toohello 現有 Azure AD Connect 的伺服器 （含有 LocalDB) 中的部署。</span><span class="sxs-lookup"><span data-stu-id="78dee-173">It is recommended that you do a swing migration where hello new Azure AD Connect server (with SQL DB) is deployed as a staging server, next toohello existing Azure AD Connect server (with LocalDB).</span></span> 
* <span data-ttu-id="78dee-174">如需如何 tooconfigure 遠端的 SQL 搭配 Azure AD Connect，請參閱指示 tooarticle[的 Azure AD Connect 自訂安裝](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-get-started-custom)。</span><span class="sxs-lookup"><span data-stu-id="78dee-174">For instruction on how tooconfigure remote SQL with Azure AD Connect, refer tooarticle [Custom installation of Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-get-started-custom).</span></span>
* <span data-ttu-id="78dee-175">如需 Azure AD Connect 升級迴旋移轉的指示，請參閱 tooarticle [Azure AD Connect： 從先前版本 toohello 最新升級](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-upgrade-previous-version#swing-migration)。</span><span class="sxs-lookup"><span data-stu-id="78dee-175">For instructions on swing migration for Azure AD Connect upgrade, refer tooarticle [Azure AD Connect: Upgrade from a previous version toohello latest](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-upgrade-previous-version#swing-migration).</span></span>

## <a name="next-steps"></a><span data-ttu-id="78dee-176">後續步驟</span><span class="sxs-lookup"><span data-stu-id="78dee-176">Next steps</span></span>
<span data-ttu-id="78dee-177">深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="78dee-177">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
