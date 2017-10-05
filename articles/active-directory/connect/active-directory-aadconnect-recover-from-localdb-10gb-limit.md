---
title: "Azure AD Connect：如何從 LocalDB 10 GB 的限制問題復原 | Microsoft Docs"
description: "本主題說明當遇到 LocalDB 10 GB 限制的問題時，如何復原 Azure AD Connect 同步處理服務。"
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
ms.openlocfilehash: 08e682c51b12d4506019d2f6b68e1eae0798b990
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-how-to-recover-from-localdb-10-gb-limit"></a><span data-ttu-id="a7f08-103">Azure AD Connect：如何從 LocalDB 10-GB 的限制復原</span><span class="sxs-lookup"><span data-stu-id="a7f08-103">Azure AD Connect: How to recover from LocalDB 10-GB limit</span></span>
<span data-ttu-id="a7f08-104">Azure AD Connect 需要 SQL Server 資料庫來儲存身分識別資料。</span><span class="sxs-lookup"><span data-stu-id="a7f08-104">Azure AD Connect requires a SQL Server database to store identity data.</span></span> <span data-ttu-id="a7f08-105">您可以使用 Azure AD Connect 安裝的預設 SQL Server 2012 Express LocalDB 或使用您自己的完整 SQL。</span><span class="sxs-lookup"><span data-stu-id="a7f08-105">You can either use the default SQL Server 2012 Express LocalDB installed with Azure AD Connect or use your own full SQL.</span></span> <span data-ttu-id="a7f08-106">SQL Server Express 會實行 10 GB 的大小限制。</span><span class="sxs-lookup"><span data-stu-id="a7f08-106">SQL Server Express imposes a 10-GB size limit.</span></span> <span data-ttu-id="a7f08-107">使用 LocalDB 且達到這個限制時，Azure AD Connect 同步處理服務無法再啟動或正確同步處理。</span><span class="sxs-lookup"><span data-stu-id="a7f08-107">When using LocalDB and this limit is reached, Azure AD Connect Synchronization Service can no longer start or synchronize properly.</span></span> <span data-ttu-id="a7f08-108">本文提供復原步驟。</span><span class="sxs-lookup"><span data-stu-id="a7f08-108">This article provides the recovery steps.</span></span>

## <a name="symptoms"></a><span data-ttu-id="a7f08-109">徵兆</span><span class="sxs-lookup"><span data-stu-id="a7f08-109">Symptoms</span></span>
<span data-ttu-id="a7f08-110">有兩個常見的徵兆︰</span><span class="sxs-lookup"><span data-stu-id="a7f08-110">There are two common symptoms:</span></span>

* <span data-ttu-id="a7f08-111">Azure AD Connect 同步處理服務**執行**，但無法同步處理並出現 “stopped-database-disk-full” 錯誤。</span><span class="sxs-lookup"><span data-stu-id="a7f08-111">Azure AD Connect Synchronization Service **is running** but fails to synchronize with *“stopped-database-disk-full”* error.</span></span>

* <span data-ttu-id="a7f08-112">Azure AD Connect 同步處理服務**無法啟動**。</span><span class="sxs-lookup"><span data-stu-id="a7f08-112">Azure AD Connect Synchronization Service **is unable to start**.</span></span> <span data-ttu-id="a7f08-113">當您嘗試啟動服務時，它會失敗並出現 6323 事件及「SQL Server 磁碟空間用完，因此伺服器發生錯誤」的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="a7f08-113">When you attempt to start the service, it fails with event 6323 and error message *"The server encountered an error because SQL Server is out of disk space."*</span></span>

## <a name="short-term-recovery-steps"></a><span data-ttu-id="a7f08-114">短期復原步驟</span><span class="sxs-lookup"><span data-stu-id="a7f08-114">Short-term recovery steps</span></span>
<span data-ttu-id="a7f08-115">本節提供的步驟可收回 Azure AD Connect 同步處理服務所需的 DB 空間以繼續作業。</span><span class="sxs-lookup"><span data-stu-id="a7f08-115">This section provides the steps to reclaim DB space required for Azure AD Connect Synchronization Service to resume operation.</span></span> <span data-ttu-id="a7f08-116">步驟包括：</span><span class="sxs-lookup"><span data-stu-id="a7f08-116">The steps include:</span></span>
1. [<span data-ttu-id="a7f08-117">判斷同步處理服務狀態</span><span class="sxs-lookup"><span data-stu-id="a7f08-117">Determine the Synchronization Service status</span></span>](#determine-the-synchronization-service-status)
2. [<span data-ttu-id="a7f08-118">壓縮資料庫</span><span class="sxs-lookup"><span data-stu-id="a7f08-118">Shrink the database</span></span>](#shrink-the-database)
3. [<span data-ttu-id="a7f08-119">刪除執行記錄資料</span><span class="sxs-lookup"><span data-stu-id="a7f08-119">Delete run history data</span></span>](#delete-run-history-data)
4. [<span data-ttu-id="a7f08-120">縮短執行歷程記錄資料的保留期間</span><span class="sxs-lookup"><span data-stu-id="a7f08-120">Shorten retention period for run history data</span></span>](#shorten-retention-period-for-run-history-data)

### <a name="determine-the-synchronization-service-status"></a><span data-ttu-id="a7f08-121">判斷同步處理服務狀態</span><span class="sxs-lookup"><span data-stu-id="a7f08-121">Determine the Synchronization Service status</span></span>
<span data-ttu-id="a7f08-122">首先，判斷同步處理服務是否仍在執行中︰</span><span class="sxs-lookup"><span data-stu-id="a7f08-122">First, determine whether the Synchronization Service is still running or not:</span></span>

1. <span data-ttu-id="a7f08-123">以系統管理員身分登入您的 Azure AD Connect 伺服器。</span><span class="sxs-lookup"><span data-stu-id="a7f08-123">Log in to your Azure AD Connect server as administrator.</span></span>

2. <span data-ttu-id="a7f08-124">移至 [服務控制管理員]。</span><span class="sxs-lookup"><span data-stu-id="a7f08-124">Go to **Service Control Manager**.</span></span>

3. <span data-ttu-id="a7f08-125">檢查 **Microsoft Azure AD Sync** 的狀態。</span><span class="sxs-lookup"><span data-stu-id="a7f08-125">Check the status of **Microsoft Azure AD Sync**.</span></span>


4. <span data-ttu-id="a7f08-126">如果正在執行，請勿停止或重新啟動服務。</span><span class="sxs-lookup"><span data-stu-id="a7f08-126">If it is running, do not stop or restart the service.</span></span> <span data-ttu-id="a7f08-127">略過[壓縮資料庫](#shrink-the-database)步驟並移至[刪除執行記錄資料](#delete-run-history-data)步驟。</span><span class="sxs-lookup"><span data-stu-id="a7f08-127">Skip [Shrink the database](#shrink-the-database) step and go to [Delete run history data](#delete-run-history-data) step.</span></span>

5. <span data-ttu-id="a7f08-128">如果非執行中，請嘗試啟動服務。</span><span class="sxs-lookup"><span data-stu-id="a7f08-128">If it is not running, try to start the service.</span></span> <span data-ttu-id="a7f08-129">如果服務成功啟動，略過[壓縮資料庫](#shrink-the-database)步驟並移至[刪除執行記錄資料](#delete-run-history-data)步驟。</span><span class="sxs-lookup"><span data-stu-id="a7f08-129">If the service starts successfully, skip [Shrink the database](#shrink-the-database) step and go to [Delete run history data](#delete-run-history-data) step.</span></span> <span data-ttu-id="a7f08-130">否則，請以[壓縮資料庫](#shrink-the-database)步驟繼續進行。</span><span class="sxs-lookup"><span data-stu-id="a7f08-130">Otherwise, continue with [Shrink the database](#shrink-the-database) step.</span></span>

### <a name="shrink-the-database"></a><span data-ttu-id="a7f08-131">壓縮資料庫</span><span class="sxs-lookup"><span data-stu-id="a7f08-131">Shrink the database</span></span>
<span data-ttu-id="a7f08-132">請使用壓縮作業釋出足夠的 DB 空間，以啟動同步處理服務。</span><span class="sxs-lookup"><span data-stu-id="a7f08-132">Use the Shrink operation to free up enough DB space to start the Synchronization Service.</span></span> <span data-ttu-id="a7f08-133">它會藉由在資料庫中移除空格來釋放 DB 空間。</span><span class="sxs-lookup"><span data-stu-id="a7f08-133">It frees up DB space by removing whitespaces in the database.</span></span> <span data-ttu-id="a7f08-134">這個步驟是最佳方式，因為不保證一律可以復原空間。</span><span class="sxs-lookup"><span data-stu-id="a7f08-134">This step is best-effort as it is not guaranteed that you can always recover space.</span></span> <span data-ttu-id="a7f08-135">若要深入了解壓縮作業，請閱讀[壓縮資料庫](https://msdn.microsoft.com/library/ms189035.aspx)文章。</span><span class="sxs-lookup"><span data-stu-id="a7f08-135">To learn more about Shrink operation, read this article [Shrink a database](https://msdn.microsoft.com/library/ms189035.aspx).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a7f08-136">如果您可以取得要執行的同步處理服務，請略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="a7f08-136">Skip this step if you can get the Synchronization Service to run.</span></span> <span data-ttu-id="a7f08-137">不建議壓縮 SQL DB，因為它可能會導致因片段增加的效能不佳。</span><span class="sxs-lookup"><span data-stu-id="a7f08-137">It is not recommended to shrink the SQL DB as it can lead to poor performance due to increased fragmentation.</span></span>

<span data-ttu-id="a7f08-138">針對 Azure AD Connect 所建立的資料庫名稱是 **ADSync**。</span><span class="sxs-lookup"><span data-stu-id="a7f08-138">The name of the database created for Azure AD Connect is **ADSync**.</span></span> <span data-ttu-id="a7f08-139">若要執行壓縮作業，您必須以系統管理員或資料庫的 DBO 登入。</span><span class="sxs-lookup"><span data-stu-id="a7f08-139">To perform a Shrink operation, you must log in either as the sysadmin or DBO of the database.</span></span> <span data-ttu-id="a7f08-140">在 Azure AD Connect 安裝期間，會授與系統管理員權限給下列帳戶︰</span><span class="sxs-lookup"><span data-stu-id="a7f08-140">During Azure AD Connect installation, the following accounts are granted sysadmin rights:</span></span>
* <span data-ttu-id="a7f08-141">本機系統管理員</span><span class="sxs-lookup"><span data-stu-id="a7f08-141">Local Administrators</span></span>
* <span data-ttu-id="a7f08-142">用來執行 Azure AD Connect 安裝的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="a7f08-142">The user account that was used to run Azure AD Connect installation.</span></span>
* <span data-ttu-id="a7f08-143">做為 Azure AD Connect 同步處理服務內容之作業系統的同步處理服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="a7f08-143">The Sync Service account that is used as the operating context of Azure AD Connect Synchronization Service.</span></span>
* <span data-ttu-id="a7f08-144">在安裝期間建立的本機群組 ADSyncAdmins。</span><span class="sxs-lookup"><span data-stu-id="a7f08-144">The local group ADSyncAdmins that was created during installation.</span></span>

1. <span data-ttu-id="a7f08-145">藉由將 `%ProgramFiles%\program files\Microsoft Azure AD Sync\Data` 下的 **ADSync.mdf** 和 **ADSync_log.ldf** 檔案複製到安全的位置來備份資料庫。</span><span class="sxs-lookup"><span data-stu-id="a7f08-145">Back up the database by copying **ADSync.mdf** and **ADSync_log.ldf** files located under `%ProgramFiles%\program files\Microsoft Azure AD Sync\Data` to a safe location.</span></span>

2. <span data-ttu-id="a7f08-146">啟動新的 PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="a7f08-146">Start a new PowerShell session.</span></span>

3. <span data-ttu-id="a7f08-147">瀏覽至資料夾 `%ProgramFiles%\Program Files\Microsoft SQL Server\110\Tools\Binn`。</span><span class="sxs-lookup"><span data-stu-id="a7f08-147">Navigate to folder `%ProgramFiles%\Program Files\Microsoft SQL Server\110\Tools\Binn`.</span></span>

4. <span data-ttu-id="a7f08-148">使用系統管理員或資料庫 DBO 的認證，藉由執行 `./SQLCMD.EXE -S “(localdb)\.\ADSync” -U <Username> -P <Password>` 命令來啟動 **sqlcmd** 公用程式。</span><span class="sxs-lookup"><span data-stu-id="a7f08-148">Start **sqlcmd** utility by running the command `./SQLCMD.EXE -S “(localdb)\.\ADSync” -U <Username> -P <Password>`, using the credential of a sysadmin or the database DBO.</span></span>

5. <span data-ttu-id="a7f08-149">若要壓縮資料庫，請在 sqlcmd 提示字元 (1>)，輸入 `DBCC Shrinkdatabase(ADSync,1);`，在下一行後面接著 `GO`。</span><span class="sxs-lookup"><span data-stu-id="a7f08-149">To shrink the database, at the sqlcmd prompt (1>), enter `DBCC Shrinkdatabase(ADSync,1);`, followed by `GO` in the next line.</span></span>

6. <span data-ttu-id="a7f08-150">如果作業成功，請嘗試重新啟動同步處理服務。</span><span class="sxs-lookup"><span data-stu-id="a7f08-150">If the operation is successful, try to start the Synchronization Service again.</span></span> <span data-ttu-id="a7f08-151">如果您可以啟動同步處理服務，請移至[刪除執行記錄資料](#delete-run-history-data)步驟。</span><span class="sxs-lookup"><span data-stu-id="a7f08-151">If you can start the Synchronization Service, go to [Delete run history data](#delete-run-history-data) step.</span></span> <span data-ttu-id="a7f08-152">否則請連絡支援人員。</span><span class="sxs-lookup"><span data-stu-id="a7f08-152">If not, contact Support.</span></span>

### <a name="delete-run-history-data"></a><span data-ttu-id="a7f08-153">刪除執行記錄資料</span><span class="sxs-lookup"><span data-stu-id="a7f08-153">Delete run history data</span></span>
<span data-ttu-id="a7f08-154">根據預設，Azure AD Connect 最多會保留七天的執行歷程記錄資料。</span><span class="sxs-lookup"><span data-stu-id="a7f08-154">By default, Azure AD Connect retains up to seven days’ worth of run history data.</span></span> <span data-ttu-id="a7f08-155">在此步驟中，我們會刪除歷程記錄資料來收回 DB 空間，讓 Azure AD Connect 同步處理服務可以再次啟動同步處理。</span><span class="sxs-lookup"><span data-stu-id="a7f08-155">In this step, we delete the run history data to reclaim DB space so that Azure AD Connect Synchronization Service can start syncing again.</span></span>

1.  <span data-ttu-id="a7f08-156">前往 [開始] → [同步處理服務] 來啟動**同步處理服務管理員**。</span><span class="sxs-lookup"><span data-stu-id="a7f08-156">Start **Synchronization Service Manager** by going to START → Synchronization Service.</span></span>

2.  <span data-ttu-id="a7f08-157">移至 [作業] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a7f08-157">Go to the **Operations** tab.</span></span>

3.  <span data-ttu-id="a7f08-158">選取 [動作] 下方的 [清除執行]...</span><span class="sxs-lookup"><span data-stu-id="a7f08-158">Under **Actions**, select **Clear Runs**…</span></span>

4.  <span data-ttu-id="a7f08-159">您可以選擇 [清除所有執行] 或 [清除之前的執行...]**<date>** 選項。</span><span class="sxs-lookup"><span data-stu-id="a7f08-159">You can either choose **Clear all runs** or **Clear runs before… <date>** option.</span></span> <span data-ttu-id="a7f08-160">建議您一開始先清除執行超過兩天的歷程記錄資料。</span><span class="sxs-lookup"><span data-stu-id="a7f08-160">It is recommended that you start by clearing run history data that are older than two days.</span></span> <span data-ttu-id="a7f08-161">如果您遇到 DB 大小的問題，則選擇 [清除所有執行] 選項。</span><span class="sxs-lookup"><span data-stu-id="a7f08-161">If you continue to run into DB size issue, then choose the **Clear all runs** option.</span></span>

### <a name="shorten-retention-period-for-run-history-data"></a><span data-ttu-id="a7f08-162">縮短執行歷程記錄資料的保留期間</span><span class="sxs-lookup"><span data-stu-id="a7f08-162">Shorten retention period for run history data</span></span>
<span data-ttu-id="a7f08-163">此步驟是要降低在多個同步處理循環之後遇到 10 GB 限制問題的可能性。</span><span class="sxs-lookup"><span data-stu-id="a7f08-163">This step is to reduce the likelihood of running into the 10-GB limit issue after multiple sync cycles.</span></span>

1. <span data-ttu-id="a7f08-164">開啟新的 PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="a7f08-164">Open a new PowerShell session.</span></span>

2. <span data-ttu-id="a7f08-165">執行 `Get-ADSyncScheduler` 並記下 PurgeRunHistoryInterval 屬性，其會指定目前的保留期限。</span><span class="sxs-lookup"><span data-stu-id="a7f08-165">Run `Get-ADSyncScheduler` and take note of the PurgeRunHistoryInterval property, which specifies the current retention period.</span></span>

3. <span data-ttu-id="a7f08-166">執行 `Set-ADSyncScheduler -PurgeRunHistoryInterval 2.00:00:00` 以將保留期限設為兩天。</span><span class="sxs-lookup"><span data-stu-id="a7f08-166">Run `Set-ADSyncScheduler -PurgeRunHistoryInterval 2.00:00:00` to set the retention period to two days.</span></span> <span data-ttu-id="a7f08-167">適當調整保留期限。</span><span class="sxs-lookup"><span data-stu-id="a7f08-167">Adjust the retention period as appropriate.</span></span>

## <a name="long-term-solution--migrate-to-full-sql"></a><span data-ttu-id="a7f08-168">長期解決方案 – 移轉至完整的 SQL</span><span class="sxs-lookup"><span data-stu-id="a7f08-168">Long-term solution – Migrate to full SQL</span></span>
<span data-ttu-id="a7f08-169">一般情況下，問題顯示 10 GB 資料庫大小不足，Azure AD Connect 無法再同步處理您的內部部署 Active Directory 到 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="a7f08-169">In general, the issue is indicative that 10-GB database size is no longer sufficient for Azure AD Connect to synchronize your on-premises Active Directory to Azure AD.</span></span> <span data-ttu-id="a7f08-170">建議您改為使用完整版的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="a7f08-170">It is recommended that you switch to using the full version of SQL server.</span></span> <span data-ttu-id="a7f08-171">您無法直接將現有的 Azure AD Connect 部署取代為完整版的 SQL 資料庫 LocalDB。</span><span class="sxs-lookup"><span data-stu-id="a7f08-171">You cannot directly replace the LocalDB of an existing Azure AD Connect deployment with the database of the full version of SQL.</span></span> <span data-ttu-id="a7f08-172">相反地，您必須部署新的 Azure AD Connect 伺服器與 SQL 的完整版本。</span><span class="sxs-lookup"><span data-stu-id="a7f08-172">Instead, you must deploy a new Azure AD Connect server with the full version of SQL.</span></span> <span data-ttu-id="a7f08-173">建議您將部署新 Azure AD Connect 伺服器 (含 SQL DB) 做為預備伺服器的變換移轉，其位於現有 Azure AD Connect 伺服器 (含 LocalDB) 旁。</span><span class="sxs-lookup"><span data-stu-id="a7f08-173">It is recommended that you do a swing migration where the new Azure AD Connect server (with SQL DB) is deployed as a staging server, next to the existing Azure AD Connect server (with LocalDB).</span></span> 
* <span data-ttu-id="a7f08-174">如需有關如何使用 Azure AD Connect 設定遠端 SQL 的指示，請參閱 [Azure AD Connect 的自訂安裝](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-get-started-custom)文章。</span><span class="sxs-lookup"><span data-stu-id="a7f08-174">For instruction on how to configure remote SQL with Azure AD Connect, refer to article [Custom installation of Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-get-started-custom).</span></span>
* <span data-ttu-id="a7f08-175">如需 Azure AD Connect 升級的變換移轉指示，請參閱 [Azure AD Connect︰從舊版升級至最新版本](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-upgrade-previous-version#swing-migration)文章。</span><span class="sxs-lookup"><span data-stu-id="a7f08-175">For instructions on swing migration for Azure AD Connect upgrade, refer to article [Azure AD Connect: Upgrade from a previous version to the latest](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-upgrade-previous-version#swing-migration).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7f08-176">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a7f08-176">Next steps</span></span>
<span data-ttu-id="a7f08-177">深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="a7f08-177">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
