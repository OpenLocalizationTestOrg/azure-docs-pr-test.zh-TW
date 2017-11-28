---
title: "Service Fabric 備份與還原 | Microsoft Docs"
description: "Service Fabric 備份與還原的概念文件"
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: subramar,jessebenson
ms.assetid: 91ea6ca4-cc2a-4155-9823-dcbd0b996349
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: mcoskun
ms.openlocfilehash: 4242962e7e03053ef25f198a0b2f6c8012e693eb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="back-up-and-restore-reliable-services-and-reliable-actors"></a><span data-ttu-id="0e9cc-103">備份與還原 Reliable Services 和 Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="0e9cc-103">Back up and restore Reliable Services and Reliable Actors</span></span>
<span data-ttu-id="0e9cc-104">Azure Service Fabric 是高可用性平台，跨多個節點之間複寫狀態以維護這個高可用性。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-104">Azure Service Fabric is a high-availability platform that replicates the state across multiple nodes to maintain this high availability.</span></span>  <span data-ttu-id="0e9cc-105">因此，即使叢集中的一個節點失敗，服務可以繼續。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-105">Thus, even if one node in the cluster fails, the services continue to be available.</span></span> <span data-ttu-id="0e9cc-106">雖然這個由平台提供的內建備援對於一些特定情況可能已經足夠，但是服務最好能夠備份資料 (到外部存放區)。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-106">While this in-built redundancy provided by the platform may be sufficient for some, in certain cases it is desirable for the service to back up data (to an external store).</span></span>

> [!NOTE]
> <span data-ttu-id="0e9cc-107">請務必備份和還原您的資料 (以及測試它是否運作正常)，以便您從資料遺失情況下進行復原。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-107">It is critical to backup and restore your data (and test that it works as expected) so you can recover from data loss scenarios.</span></span>
> 
> 

<span data-ttu-id="0e9cc-108">例如，服務需要備份資料以在下列情節中提供保護：</span><span class="sxs-lookup"><span data-stu-id="0e9cc-108">For example, a service may want to back up data in order to protect from the following scenarios:</span></span>

- <span data-ttu-id="0e9cc-109">發生整個 Service Fabric 叢集永久遺失的情況。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-109">In the event of the permanent loss of an entire Service Fabric cluster.</span></span>
- <span data-ttu-id="0e9cc-110">永久遺失多數的服務分割區複本</span><span class="sxs-lookup"><span data-stu-id="0e9cc-110">Permanent loss of a majority of the replicas of a service partition</span></span>
- <span data-ttu-id="0e9cc-111">不小心刪除或損毀狀態的系統管理錯誤。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-111">Administrative errors whereby the state accidentally gets deleted or corrupted.</span></span> <span data-ttu-id="0e9cc-112">例如，這可能會在具備足夠權限的系統管理員錯誤地刪除服務時發生。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-112">For example, this may happen if an administrator with sufficient privilege erroneously deletes the service.</span></span>
- <span data-ttu-id="0e9cc-113">服務中造成資料損毀的錯誤。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-113">Bugs in the service that cause data corruption.</span></span> <span data-ttu-id="0e9cc-114">例如，當服務程式碼升級而開始將錯誤資料寫入「可靠的集合」時，就可能發生此情況。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-114">For example, this may happen when a service code upgrade starts writing faulty data to a Reliable Collection.</span></span> <span data-ttu-id="0e9cc-115">在這種情況下，可能必須將程式碼和資料還原成先前的狀態。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-115">In such a case, both the code and the data may have to be reverted to an earlier state.</span></span>
- <span data-ttu-id="0e9cc-116">離線資料處理。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-116">Offline data processing.</span></span> <span data-ttu-id="0e9cc-117">對於獨立於服務來產生資料的商業智慧，離線處理資料相當方便。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-117">It might be convenient to have offline processing of data for business intelligence that happens separately from the service that generates the data.</span></span>

<span data-ttu-id="0e9cc-118">備份/還原功能可以讓在 Reliable Services API 上建置的服務建立及還原備份。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-118">The Backup/Restore feature allows services built on the Reliable Services API to create and restore backups.</span></span> <span data-ttu-id="0e9cc-119">平台提供的備份 API 可以備份服務分割區狀態，而不會封鎖讀取或寫入作業。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-119">The backup APIs provided by the platform allow backup(s) of a service partition's state, without blocking read or write operations.</span></span> <span data-ttu-id="0e9cc-120">還原 API 可以從所選的備份還原服務分割區的狀態。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-120">The restore APIs allow a service partition's state to be restored from a chosen backup.</span></span>

## <a name="types-of-backup"></a><span data-ttu-id="0e9cc-121">備份類型</span><span class="sxs-lookup"><span data-stu-id="0e9cc-121">Types of Backup</span></span>
<span data-ttu-id="0e9cc-122">有兩個備份選項︰完整和增量。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-122">There are two backup options: Full and Incremental.</span></span>
<span data-ttu-id="0e9cc-123">完整備份是包含重新建立複本狀態所需的所有資料的備份︰檢查點和所有記錄檔記錄。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-123">A full backup is a backup that contains all the data required to recreate the state of the replica: checkpoints and all log records.</span></span>
<span data-ttu-id="0e9cc-124">因為它有檢查點和記錄檔，所以可以自行還原完整備份。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-124">Since it has the checkpoints and the log, a full backup can be restored by itself.</span></span>

<span data-ttu-id="0e9cc-125">檢查點太大時，會發生完整備份問題。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-125">The problem with full backups arises when the checkpoints are large.</span></span>
<span data-ttu-id="0e9cc-126">例如，具有 16 GB 狀態的複本，其檢查點大約會增加為 16 GB。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-126">For example, a replica that has 16 GB of state will have checkpoints that add up approximately to 16 GB.</span></span>
<span data-ttu-id="0e9cc-127">如果復原點目標為五分鐘，則需要每五分鐘備份複本一次。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-127">If we have a Recovery Point Objective of five minutes, the replica needs to be backed up every five minutes.</span></span>
<span data-ttu-id="0e9cc-128">每次備份時，除了 50 MB (可使用 `CheckpointThresholdInMB` 設定) 的記錄之外，還需要複製 16 GB 的檢查點。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-128">Each time it backs up it needs to copy 16 GB of checkpoints in addition to 50 MB (configurable using `CheckpointThresholdInMB`) worth of logs.</span></span>

![完整備份範例。](media/service-fabric-reliable-services-backup-restore/FullBackupExample.PNG)

<span data-ttu-id="0e9cc-130">此問題的解決方案是增量備份，其中備份只會包含上次備份後的變更記錄資料列。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-130">The solution to this problem is incremental backups, where backup only contains the changed log records since the last backup.</span></span>

![增量備份範例。](media/service-fabric-reliable-services-backup-restore/IncrementalBackupExample.PNG)

<span data-ttu-id="0e9cc-132">因為增量備份只是上次備份後的變更 (不包含檢查點)，所以它們通常會比較快，但無法自行進行還原。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-132">Since incremental backups are only changes since the last backup (does not include the checkpoints), they tend to be faster but they cannot be restored on their own.</span></span>
<span data-ttu-id="0e9cc-133">若要還原增量備份，需要整個備份鏈結。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-133">To restore an incremental backup, the entire backup chain is required.</span></span>
<span data-ttu-id="0e9cc-134">備份鏈結是一連串的備份，開始為完整備份，而接著是數個連續的增量備份。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-134">A backup chain is a chain of backups starting with a full backup and followed by a number of contiguous incremental backups.</span></span>

## <a name="backup-reliable-services"></a><span data-ttu-id="0e9cc-135">備份 Reliable Services</span><span class="sxs-lookup"><span data-stu-id="0e9cc-135">Backup Reliable Services</span></span>
<span data-ttu-id="0e9cc-136">服務作者對於進行備份的時機與儲存備份的位置具有完整的控制權。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-136">The service author has full control of when to make backups and where backups will be stored.</span></span>

<span data-ttu-id="0e9cc-137">若要開始備份，服務必須叫用繼承的成員函式 `BackupAsync`。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-137">To start a backup, the service needs to invoke the inherited member function `BackupAsync`.</span></span>  
<span data-ttu-id="0e9cc-138">備份只能從主要複本進行，且需要授與它們寫入狀態。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-138">Backups can be made only from primary replicas, and they require write status to be granted.</span></span>

<span data-ttu-id="0e9cc-139">如下所示，`BackupAsync` 接受 `BackupDescription` 物件，使用者可以在其中指定完整或增量備份，以及指定在本機建立備份資料夾並準備好移出到一些外部儲存體時，所要叫用的回呼函式 `Func<< BackupInfo, CancellationToken, Task<bool>>>`。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-139">As shown below, `BackupAsync` takes in a `BackupDescription` object, where one can specify a full or incremental backup, as well as a callback function, `Func<< BackupInfo, CancellationToken, Task<bool>>>` that is invoked when the backup folder has been created locally and is ready to be moved out to some external storage.</span></span>

```csharp

BackupDescription myBackupDescription = new BackupDescription(backupOption.Incremental,this.BackupCallbackAsync);

await this.BackupAsync(myBackupDescription);

```

<span data-ttu-id="0e9cc-140">要採取增量備份的要求可能會失敗，並出現 `FabricMissingFullBackupException`。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-140">Request to take an incremental backup can fail with `FabricMissingFullBackupException`.</span></span> <span data-ttu-id="0e9cc-141">這個例外狀況表示發生了下列其中一個事項：</span><span class="sxs-lookup"><span data-stu-id="0e9cc-141">This exception indicates that one of the following things is happening:</span></span>

- <span data-ttu-id="0e9cc-142">複本在變成主要複本之後從未執行完整備份、</span><span class="sxs-lookup"><span data-stu-id="0e9cc-142">the replica has never taken a full backup since it has become primary,</span></span>
- <span data-ttu-id="0e9cc-143">自上次備份被截斷之後記錄了部分記錄檔，或</span><span class="sxs-lookup"><span data-stu-id="0e9cc-143">some of the log records since the last backup has been truncated or</span></span>
- <span data-ttu-id="0e9cc-144">傳遞 `MaxAccumulatedBackupLogSizeInMB` 限制的複本。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-144">replica passed the `MaxAccumulatedBackupLogSizeInMB` limit.</span></span>

<span data-ttu-id="0e9cc-145">使用者可以透過設定 `MinLogSizeInMB` 或 `TruncationThresholdFactor` 來提高能夠進行增量備份的可能性。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-145">Users can increase the likelihood of being able to do incremental backups by configuring `MinLogSizeInMB` or `TruncationThresholdFactor`.</span></span>
<span data-ttu-id="0e9cc-146">請注意，提高這些值將會增加每個複本磁碟的使用量。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-146">Note that increasing these values increases the per replica disk usage.</span></span>
<span data-ttu-id="0e9cc-147">如需詳細資訊，請參閱 [Reliable Services 組態](service-fabric-reliable-services-configuration.md)</span><span class="sxs-lookup"><span data-stu-id="0e9cc-147">For more information, see [Reliable Services Configuration](service-fabric-reliable-services-configuration.md)</span></span>

<span data-ttu-id="0e9cc-148">`BackupInfo` 提供備份的相關資訊，包括執行階段儲存備份所在的資料夾位置 (`BackupInfo.Directory`)。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-148">`BackupInfo` provides information regarding the backup, including the location of the folder where the runtime saved the backup (`BackupInfo.Directory`).</span></span> <span data-ttu-id="0e9cc-149">回呼函式可以將 `BackupInfo.Directory` 移到外部存放區或另一個位置。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-149">The callback function can move the `BackupInfo.Directory` to an external store or another location.</span></span>  <span data-ttu-id="0e9cc-150">此函式也會傳回 Bool，指出是否能夠順利將備份資料夾移動至目標位置。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-150">This function also returns a bool that indicates whether it was able to successfully move the backup folder to its target location.</span></span>

<span data-ttu-id="0e9cc-151">下列程式碼示範如何使用 `BackupCallbackAsync` 方法將備份上傳至 Azure 儲存體：</span><span class="sxs-lookup"><span data-stu-id="0e9cc-151">The following code demonstrates how the `BackupCallbackAsync` method can be used to upload the backup to Azure Storage:</span></span>

```csharp
private async Task<bool> BackupCallbackAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
{
    var backupId = Guid.NewGuid();

    await externalBackupStore.UploadBackupFolderAsync(backupInfo.Directory, backupId, cancellationToken);

    return true;
}
```

<span data-ttu-id="0e9cc-152">在上述範例中，`ExternalBackupStore` 是用來與 Azure Blob 儲存體介接的範例類別，而 `UploadBackupFolderAsync` 是壓縮資料夾並將它放在 Azure Blob 存放區的方法。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-152">In the preceeding example, `ExternalBackupStore` is the sample class that is used to interface with Azure Blob storage, and `UploadBackupFolderAsync` is the method that compresses the folder and places it in the Azure Blob store.</span></span>

<span data-ttu-id="0e9cc-153">請注意：</span><span class="sxs-lookup"><span data-stu-id="0e9cc-153">Note that:</span></span>

  - <span data-ttu-id="0e9cc-154">在任何指定時間每個複本只能有一項進行中的備份作業。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-154">There can be only one backup operation in-flight per replica at any given time.</span></span> <span data-ttu-id="0e9cc-155">一次多個 `BackupAsync` 呼叫會擲回 `FabricBackupInProgressException`，將傳遞備份限制為一個。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-155">More than one `BackupAsync` call at a time will throw `FabricBackupInProgressException` to limit inflight backups to one.</span></span>
  - <span data-ttu-id="0e9cc-156">如果當備份進行中時有複本容錯移轉，備份可能未完成。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-156">If a replica fails over while a backup is in progress, the backup may not have been completed.</span></span> <span data-ttu-id="0e9cc-157">因此，容錯移轉完成之後，服務必須負責視需要叫用 `BackupAsync` 以重新啟動備份。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-157">Thus, once the failover finishes, it is the service's responsibility to restart the backup by invoking `BackupAsync` as necessary.</span></span>

## <a name="restore-reliable-services"></a><span data-ttu-id="0e9cc-158">還原 Reliable Services</span><span class="sxs-lookup"><span data-stu-id="0e9cc-158">Restore Reliable Services</span></span>
<span data-ttu-id="0e9cc-159">一般而言，您可能需要執行還原作業的情況屬於下列其中一種：</span><span class="sxs-lookup"><span data-stu-id="0e9cc-159">In general, the cases when you might need to perform a restore operation fall into one of these categories:</span></span>

  - <span data-ttu-id="0e9cc-160">服務資料分割遺失資料。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-160">The service partition lost data.</span></span> <span data-ttu-id="0e9cc-161">例如，分割區的三分之二複本 (包括主要複本) 的磁碟損毀或抹除。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-161">For example, the disk for two out of three replicas for a partition (including the primary replica) gets corrupted or wiped.</span></span> <span data-ttu-id="0e9cc-162">新的主要複本可能需要從備份還原資料。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-162">The new primary may need to restore data from a backup.</span></span>
  - <span data-ttu-id="0e9cc-163">整個服務遺失。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-163">The entire service is lost.</span></span> <span data-ttu-id="0e9cc-164">例如，系統管理員移除整個服務，因此服務和資料需要還原。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-164">For example, an administrator removes the entire service and thus the service and the data need to be restored.</span></span>
  - <span data-ttu-id="0e9cc-165">服務會複寫損毀的應用程式資料 (例如，因為應用程式錯誤)。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-165">The service replicated corrupt application data (e.g., because of an application bug).</span></span> <span data-ttu-id="0e9cc-166">在此情況下，服務必須升級或還原以移除損毀的原因，且必須還原未損毀的資料。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-166">In this case, the service has to be upgraded or reverted to remove the cause of the corruption, and non-corrupt data has to be restored.</span></span>

<span data-ttu-id="0e9cc-167">雖然有許多種可行的方法，我們會提供一些範例，說明使用 `RestoreAsync` 從上述案例進行復原。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-167">While many approaches are possible, we offer some examples on using `RestoreAsync` to recover from the above scenarios.</span></span>

## <a name="partition-data-loss-in-reliable-services"></a><span data-ttu-id="0e9cc-168">Reliable Services 中的分割區資料遺失</span><span class="sxs-lookup"><span data-stu-id="0e9cc-168">Partition data loss in Reliable Services</span></span>
<span data-ttu-id="0e9cc-169">在此情況下，執行階段會自動偵測資料遺失，並且叫用 `OnDataLossAsync` API。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-169">In this case, the runtime would automatically detect the data loss and invoke the `OnDataLossAsync` API.</span></span>

<span data-ttu-id="0e9cc-170">服務作者必須執行下列動作來復原：</span><span class="sxs-lookup"><span data-stu-id="0e9cc-170">The service author needs to perform the following to recover:</span></span>

  - <span data-ttu-id="0e9cc-171">覆寫虛擬基底類別方法 `OnDataLossAsync`。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-171">Override the virtual base class method `OnDataLossAsync`.</span></span>
  - <span data-ttu-id="0e9cc-172">在包含服務備份的外部位置尋找最新的備份。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-172">Find the latest backup in the external location that contains the service's backups.</span></span>
  - <span data-ttu-id="0e9cc-173">下載最新的備份 (並將已壓縮的備份解壓縮到備份資料夾)。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-173">Download the latest backup (and uncompress the backup into the backup folder if it was compressed).</span></span>
  - <span data-ttu-id="0e9cc-174">`OnDataLossAsync` 方法會提供 `RestoreContext`。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-174">The `OnDataLossAsync` method provides a `RestoreContext`.</span></span> <span data-ttu-id="0e9cc-175">在所提供的 `RestoreContext` 上呼叫 `RestoreAsync` API。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-175">Call the `RestoreAsync` API on the provided `RestoreContext`.</span></span>
  - <span data-ttu-id="0e9cc-176">如果還原成功，則會傳回 true。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-176">Return true if the restoration was a success.</span></span>

<span data-ttu-id="0e9cc-177">以下是 `OnDataLossAsync` 方法的範例實作：</span><span class="sxs-lookup"><span data-stu-id="0e9cc-177">Following is an example implementation of the `OnDataLossAsync` method:</span></span>

```csharp
protected override async Task<bool> OnDataLossAsync(RestoreContext restoreCtx, CancellationToken cancellationToken)
{
    var backupFolder = await this.externalBackupStore.DownloadLastBackupAsync(cancellationToken);

    var restoreDescription = new RestoreDescription(backupFolder);

    await restoreCtx.RestoreAsync(restoreDescription);

    return true;
}
```

<span data-ttu-id="0e9cc-178">傳入 `RestoreContext.RestoreAsync` 呼叫中的 `RestoreDescription` 包含一個名為 `BackupFolderPath` 的成員。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-178">`RestoreDescription` passed in to the `RestoreContext.RestoreAsync` call contains a member called `BackupFolderPath`.</span></span>
<span data-ttu-id="0e9cc-179">還原單一完整備份時，這個 `BackupFolderPath` 應該設定為包含完整備份的資料夾本機路徑。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-179">When restoring a single full backup, this `BackupFolderPath` should be set to the local path of the folder that contains your full backup.</span></span>
<span data-ttu-id="0e9cc-180">還原一個完整備份和一些增量備份時，`BackupFolderPath` 應該設定為資料夾的本機路徑，這個資料夾不只包含完整備份，也包含所有增量備份。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-180">When restoring a full backup and a number of incremental backups, `BackupFolderPath` should be set to the local path of the folder that not only contains the full backup, but also all the incremental backups.</span></span>
<span data-ttu-id="0e9cc-181">如果提供的 `BackupFolderPath` 不包含完整備份，`RestoreAsync` 呼叫可能會擲回 `FabricMissingFullBackupException`。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-181">`RestoreAsync` call can throw `FabricMissingFullBackupException` if the `BackupFolderPath` provided does not contain a full backup.</span></span>
<span data-ttu-id="0e9cc-182">如果 `BackupFolderPath` 的增量備份包含中斷的鏈結，它也可能會擲回 `ArgumentException`。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-182">It can also throw `ArgumentException` if `BackupFolderPath` has a broken chain of incremental backups.</span></span>
<span data-ttu-id="0e9cc-183">例如，如果它包含完整備份、第一個增量和第三個增量備份，但沒有第二個增量備份。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-183">For example, if it contains the full backup, the first incremental and the third incremental backup but no the second incremental backup.</span></span>

> [!NOTE]
> <span data-ttu-id="0e9cc-184">RestorePolicy 預設設定為 [安全]。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-184">The RestorePolicy is set to Safe by default.</span></span>  <span data-ttu-id="0e9cc-185">這表示如果 `RestoreAsync` API 偵測到備份資料夾包含早於或等於這個複本內含狀態的狀態，則它將會失敗且具有 ArgumentException。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-185">This means that the `RestoreAsync` API will fail with ArgumentException if it detects that the backup folder contains a state that is older than or equal to the state contained in this replica.</span></span>  <span data-ttu-id="0e9cc-186">`RestorePolicy.Force` 可以用來跳過這項安全檢查。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-186">`RestorePolicy.Force` can be used to skip this safety check.</span></span> <span data-ttu-id="0e9cc-187">這會指定為屬於 `RestoreDescription`。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-187">This is specified as part of `RestoreDescription`.</span></span>
> 

## <a name="deleted-or-lost-service"></a><span data-ttu-id="0e9cc-188">已刪除或遺失的服務</span><span class="sxs-lookup"><span data-stu-id="0e9cc-188">Deleted or lost service</span></span>
<span data-ttu-id="0e9cc-189">如果服務已移除，您必須先重新建立該服務，才可以還原資料。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-189">If a service is removed, you must first re-create the service before the data can be restored.</span></span>  <span data-ttu-id="0e9cc-190">請務必以相同的組態建立服務 (例如分割配置)，如此才能順暢地還原資料。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-190">It is important to create the service with the same configuration, e.g., partitioning scheme, so that the data can be restored seamlessly.</span></span>  <span data-ttu-id="0e9cc-191">一旦服務啟動後，就必須在此服務的每個分割區上叫用還原資料的 API (上述的 `OnDataLossAsync`)。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-191">Once the service is up, the API to restore data (`OnDataLossAsync` above) has to be invoked on every partition of this service.</span></span> <span data-ttu-id="0e9cc-192">達到此動作的其中一種方式，是使用每個分割區上的 `[FabricClient.TestManagementClient.StartPartitionDataLossAsync](https://msdn.microsoft.com/library/mt693569.aspx)`。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-192">One way of achieving this is by using `[FabricClient.TestManagementClient.StartPartitionDataLossAsync](https://msdn.microsoft.com/library/mt693569.aspx)` on every partition.</span></span>  

<span data-ttu-id="0e9cc-193">從這裡開始，實作與上述案例相同。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-193">From this point, implementation is the same as the above scenario.</span></span> <span data-ttu-id="0e9cc-194">每個資料分割都需要從外部存放區還原最新的相關備份。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-194">Each partition needs to restore the latest relevant backup from the external store.</span></span> <span data-ttu-id="0e9cc-195">有一點需要注意，分割識別碼現在可能已變更，因為執行階段會以動態方式建立分割識別碼。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-195">One caveat is that the partition ID may have now changed, since the runtime creates partition IDs dynamically.</span></span> <span data-ttu-id="0e9cc-196">因此，服務需要儲存適當的分割資訊和服務名稱，來識別要針對每個分割區還原的正確最新備份。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-196">Thus, the service needs to store the appropriate partition information and service name to identify the correct latest backup to restore from for each partition.</span></span>

> [!NOTE]
> <span data-ttu-id="0e9cc-197">不建議在每個分割區上使用 `FabricClient.ServiceManager.InvokeDataLossAsync` 來還原整個服務，因為可能會損毀您的叢集狀態。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-197">It is not recommended to use `FabricClient.ServiceManager.InvokeDataLossAsync` on each partition to restore the entire service, since that may corrupt your cluster state.</span></span>
> 

## <a name="replication-of-corrupt-application-data"></a><span data-ttu-id="0e9cc-198">損毀之應用程式資料的複寫</span><span class="sxs-lookup"><span data-stu-id="0e9cc-198">Replication of corrupt application data</span></span>
<span data-ttu-id="0e9cc-199">如果新部署的應用程式升級有錯誤，可能會造成資料損毀。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-199">If the newly deployed application upgrade has a bug, that may cause corruption of data.</span></span> <span data-ttu-id="0e9cc-200">例如，應用程式升級可能會開始以無效的區碼更新「可靠的字典」中的每個電話號碼記錄。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-200">For example, an application upgrade may start to update every phone number record in a Reliable Dictionary with an invalid area code.</span></span>  <span data-ttu-id="0e9cc-201">在此情況下，因為 Service Fabric 並不知道要儲存的資料本質，所以會複寫無效的電話號碼。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-201">In this case, the invalid phone numbers will be replicated since Service Fabric is not aware of the nature of the data that is being stored.</span></span>

<span data-ttu-id="0e9cc-202">偵測造成資料損毀的這類嚴重錯誤之後，您要做的第一件事是在應用程式層級凍結服務，並且在可行時升級至沒有錯誤的應用程式程式碼的版本。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-202">The first thing to do after you detect such an egregious bug that causes data corruption is to freeze the service at the application level and, if possible, upgrade to the version of the application code that does not have the bug.</span></span>  <span data-ttu-id="0e9cc-203">不過，即使在修正服務程式碼之後，資料仍可能會損毀並且因此需要還原資料。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-203">However, even after the service code is fixed, the data may still be corrupt and thus data may need to be restored.</span></span>  <span data-ttu-id="0e9cc-204">在這種情況下，還原最新的備份可能還不足夠，因為最新的備份也可能已損毀。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-204">In such cases, it may not be sufficient to restore the latest backup, since the latest backups may also be corrupt.</span></span>  <span data-ttu-id="0e9cc-205">因此，您必須尋找在資料損毀之前所做的最後一個備份。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-205">Thus, you have to find the last backup that was made before the data got corrupted.</span></span>

<span data-ttu-id="0e9cc-206">如果不確定哪些備份正確，您可以部署新的 Service Fabric 叢集，並還原受影響的分割區備份，就像上述「已刪除或遺失的服務」案例一樣。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-206">If you are not sure which backups are corrupt, you could deploy a new Service Fabric cluster and restore the backups of affected partitions just like the above "Deleted or lost service" scenario.</span></span>  <span data-ttu-id="0e9cc-207">針對每個資料分割，開始還原從最新到最舊的備份。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-207">For each partition, start restoring the backups from the most recent to the least.</span></span> <span data-ttu-id="0e9cc-208">一旦您找到沒有損毀的備份，就移動/刪除這個資料分割較新 (相較於備份) 的所有備份。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-208">Once you find a backup that does not have the corruption, move/delete all backups of this partition that were more recent (than that backup).</span></span> <span data-ttu-id="0e9cc-209">針對每個資料分割重複此程序。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-209">Repeat this process for each partition.</span></span> <span data-ttu-id="0e9cc-210">現在，當您在生產叢集中的分割區上呼叫 `OnDataLossAsync` 時，外部存放區中找到的最後一個備份會是上述程序所挑選的備份。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-210">Now, when `OnDataLossAsync` is called on the partition in the production cluster, the last backup found in the external store will be the one picked by the above process.</span></span>

<span data-ttu-id="0e9cc-211">現在，可以使用「已刪除或遺失的服務」中的步驟，將服務的狀態還原至不良程式碼損毀狀態之前的狀態。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-211">Now, the steps in the "Deleted or lost service" section can be used to restore the state of the service to the state before the buggy code corrupted the state.</span></span>

<span data-ttu-id="0e9cc-212">請注意：</span><span class="sxs-lookup"><span data-stu-id="0e9cc-212">Note that:</span></span>

  - <span data-ttu-id="0e9cc-213">當您還原時，還原的備份很有可能是早於資料遺失之前的分割區狀態。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-213">When you restore, there is a chance that the backup being restored is older than the state of the partition before the data was lost.</span></span> <span data-ttu-id="0e9cc-214">因此，您應該只能將還原當成最後手段，盡可能復原最多資料。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-214">Because of this, you should restore only as a last resort to recover as much data as possible.</span></span>
  - <span data-ttu-id="0e9cc-215">根據 FabricDataRoot 路徑和應用程式類型名稱的長度而定，代表備份資料夾路徑與備份資料夾內檔案路徑的字串可以大於 255 個字元。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-215">The string that represents the backup folder path and the paths of files inside the backup folder can be greater than 255 characters, depending on the FabricDataRoot path and Application Type name's length.</span></span> <span data-ttu-id="0e9cc-216">這會造成某些 .NET 方法 (例如 `Directory.Move`) 擲回 `PathTooLongException` 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-216">This can cause some .NET methods, like `Directory.Move`, to throw the `PathTooLongException` exception.</span></span> <span data-ttu-id="0e9cc-217">有個解決方法是直接呼叫 kernel32 API，例如 `CopyFile`。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-217">One workaround is to directly call kernel32 APIs, like `CopyFile`.</span></span>

## <a name="backup-and-restore-reliable-actors"></a><span data-ttu-id="0e9cc-218">備份與還原 Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="0e9cc-218">Backup and restore Reliable Actors</span></span>


<span data-ttu-id="0e9cc-219">Reliable Actors 架構以 Reliable Services 為基礎。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-219">Reliable Actors Framework is built on top of Reliable Services.</span></span> <span data-ttu-id="0e9cc-220">裝載動作項目的 ActorService 是具狀態可靠服務。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-220">The ActorService which hosts the actor(s) is a stateful reliable service.</span></span> <span data-ttu-id="0e9cc-221">因此，Reliable Services 中可用的所有備份和還原功能，也可用於 Reliable Actors (狀態供應器特定的行為除外)。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-221">Hence, all the backup and restore functionality available in Reliable Services is also available to Reliable Actors (except behaviors that are state provider specific).</span></span> <span data-ttu-id="0e9cc-222">因為是依個別分割區進行備份，將會備份該分割區中所有動作項目的狀態 (還原也一樣依個別分割區進行)。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-222">Since backups will be taken on a per-partition basis, states for all actors in that partition will be backed up (and restoration is similar and will happen on a per-partition basis).</span></span> <span data-ttu-id="0e9cc-223">若要執行備份/還原，服務擁有者應該建立一個衍生自 ActorService 類別的自訂動作項目服務類別，然後進行備份/還原，類似於前面幾節所述的 Reliable Services。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-223">To perform backup/restore, the service owner should create a custom actor service class that derives from ActorService class and then do backup/restore similar to Reliable Services as described above in previous sections.</span></span>

```csharp
class MyCustomActorService : ActorService
{
     public MyCustomActorService(StatefulServiceContext context, ActorTypeInformation actorTypeInfo)
            : base(context, actorTypeInfo)
     {                  
     }
    
    //
   // Method overrides and other code.
    //
}
```

<span data-ttu-id="0e9cc-224">當您建立自訂動作項目服務類別時，您也必須在註冊動作項目時註冊該類別。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-224">When you create a custom actor service class, you need to register that as well when registering the actor.</span></span>

```csharp
ActorRuntime.RegisterActorAsync<MyActor>(
   (context, typeInfo) => new MyCustomActorService(context, typeInfo)).GetAwaiter().GetResult();
```

<span data-ttu-id="0e9cc-225">Reliable Actors 的預設狀態供應器是 `KvsActorStateProvider`。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-225">The default state provider for Reliable Actors is `KvsActorStateProvider`.</span></span> <span data-ttu-id="0e9cc-226">`KvsActorStateProvider` 依預設不啟用增量備份。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-226">Incremental backup is not enabled by default for `KvsActorStateProvider`.</span></span> <span data-ttu-id="0e9cc-227">您可以建立 `KvsActorStateProvider` 並於建構函式中指定適當的設定，然後傳給 ActorService 建構函式，以啟用增量備份，如下列程式碼片段所示︰</span><span class="sxs-lookup"><span data-stu-id="0e9cc-227">You can enable incremental backup by creating `KvsActorStateProvider` with the appropriate setting in its constructor and then passing it to ActorService constructor as shown in following code snippet:</span></span>

```csharp
class MyCustomActorService : ActorService
{
     public MyCustomActorService(StatefulServiceContext context, ActorTypeInformation actorTypeInfo)
            : base(context, actorTypeInfo, null, null, new KvsActorStateProvider(true)) // Enable incremental backup
     {                  
     }
    
    //
   // Method overrides and other code.
    //
}
```

<span data-ttu-id="0e9cc-228">啟用增量備份之後，進行增量備份可能會因為下列原因之一而失敗，結果傳回 FabricMissingFullBackupException，您將需要先進行完整備份，再進行增量備份︰</span><span class="sxs-lookup"><span data-stu-id="0e9cc-228">After incremental backup has been enabled, taking an incremental backup can fail with FabricMissingFullBackupException for one of following reasons and you will need to take a full backup before taking incremental backup(s):</span></span>

  - <span data-ttu-id="0e9cc-229">複本自從變成主要以來從未進行完整備份。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-229">The replica has never taken a full backup since it became primary.</span></span>
  - <span data-ttu-id="0e9cc-230">自上次備份以來，某些記錄檔記錄已被截斷。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-230">Some of the log records were truncated since last backup was taken.</span></span>

<span data-ttu-id="0e9cc-231">啟用增量備份時，`KvsActorStateProvider` 不會使用循環緩衝區來管理其記錄資料列，也不會定期截斷。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-231">When incremental backup is enabled, `KvsActorStateProvider` does not use circular buffer to manage its log records and periodically truncates it.</span></span> <span data-ttu-id="0e9cc-232">如果使用者已有 45 分鐘沒有進行備份，系統會自動截斷記錄檔記錄。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-232">If no backup is taken by user for a period of 45 minutes, the system automatically truncates the log records.</span></span> <span data-ttu-id="0e9cc-233">您可以在 `KvsActorStateProvider` 建構函式中指定 `logTrunctationIntervalInMinutes` 來設定此間隔 (類似於啟用增量備份時)。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-233">This interval can be configured by specifying `logTrunctationIntervalInMinutes` in `KvsActorStateProvider` constructor (similar to when enabling incremental backup).</span></span> <span data-ttu-id="0e9cc-234">如果主要複本需要傳送其所有資料來建立另一個複本，也可能會截斷記錄檔記錄。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-234">The log records may also get truncated if primary replica need to build another replica by sending all its data.</span></span>

<span data-ttu-id="0e9cc-235">從備份鏈結還原時，類似於 Reliable Services，BackupFolderPath 應該包含一些子目錄，其中一個子目錄包含完整備份，而其他子目錄包含增量備份。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-235">When doing restore from a backup chain, similar to Reliable Services, the BackupFolderPath should contain subdirectories with one subdirectory containing full backup and others subdirectories containing incremental backup(s).</span></span> <span data-ttu-id="0e9cc-236">如果備份鏈結驗證失敗，還原 API 會擲回 FabricException 並傳回適當的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-236">The restore API will throw FabricException with appropriate error message if the backup chain validation fails.</span></span> 

> [!NOTE]
> <span data-ttu-id="0e9cc-237">`KvsActorStateProvider` 目前會忽略 RestorePolicy.Safe 選項。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-237">`KvsActorStateProvider` currently ignores the option RestorePolicy.Safe.</span></span> <span data-ttu-id="0e9cc-238">即將推出的版本已規劃支援這項功能。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-238">Support for this feature is planned in an upcoming release.</span></span>
> 

## <a name="testing-backup-and-restore"></a><span data-ttu-id="0e9cc-239">測試備份和還原</span><span class="sxs-lookup"><span data-stu-id="0e9cc-239">Testing Backup and Restore</span></span>
<span data-ttu-id="0e9cc-240">請務必確保重要資料正在進行備份，並可進行還原。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-240">It is important to ensure that critical data is being backed up, and can be restored from.</span></span> <span data-ttu-id="0e9cc-241">在 PowerShell 中叫用會引起特定分割區遺失資料的 `Start-ServiceFabricPartitionDataLoss` Cmdlet，以測試您服務的資料備份和還原功能是否如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-241">This can be done by invoking the `Start-ServiceFabricPartitionDataLoss` cmdlet in PowerShell that can induce data loss in a particular partition to test whether the data backup and restore functionality for your service is working as expected.</span></span>  <span data-ttu-id="0e9cc-242">此外，也可能以程式設計方式叫用資料遺失，並從該事件進行還原。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-242">It is also possible to programmatically invoke data loss and restore from that event as well.</span></span>

> [!NOTE]
> <span data-ttu-id="0e9cc-243">您可以在 GitHub 上的 Web 參考應用程式中，找到備份與還原功能的範例實作。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-243">You can find a sample implementation of backup and restore functionality in the Web Reference App on GitHub.</span></span> <span data-ttu-id="0e9cc-244">如需詳細資訊，請查看 `Inventory.Service` 服務。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-244">Please look at the `Inventory.Service` service for more details.</span></span>
> 
> 

## <a name="under-the-hood-more-details-on-backup-and-restore"></a><span data-ttu-id="0e9cc-245">幕後：備份與還原的詳細資料</span><span class="sxs-lookup"><span data-stu-id="0e9cc-245">Under the hood: more details on backup and restore</span></span>
<span data-ttu-id="0e9cc-246">以下是備份與還原的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-246">Here's some more details on backup and restore.</span></span>

### <a name="backup"></a><span data-ttu-id="0e9cc-247">備份</span><span class="sxs-lookup"><span data-stu-id="0e9cc-247">Backup</span></span>
<span data-ttu-id="0e9cc-248">可靠的狀態管理員能夠建立一致的備份，而不會封鎖任何讀取或寫入作業。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-248">The Reliable State Manager provides the ability to create consistent backups without blocking any read or write operations.</span></span> <span data-ttu-id="0e9cc-249">為了達到這個目的，它會利用檢查點和記錄持續性機制。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-249">To do so, it utilizes a checkpoint and log persistence mechanism.</span></span>  <span data-ttu-id="0e9cc-250">可靠的狀態管理員會在特定時間點採用模糊 (輕量型) 檢查點，來減輕交易記錄檔的壓力和改善復原時間。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-250">The Reliable State Manager takes fuzzy (lightweight) checkpoints at certain points to relieve pressure from the transactional log and improve recovery times.</span></span>  <span data-ttu-id="0e9cc-251">呼叫 `BackupAsync` 時，可靠的狀態管理員會指示所有可靠物件，將其最新檢查點檔案複製到本機備份資料夾。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-251">When `BackupAsync` is called, the Reliable State Manager instructs all Reliable objects to copy their latest checkpoint files to a local backup folder.</span></span>  <span data-ttu-id="0e9cc-252">然後，可靠的狀態管理員會從「開始指標」開始，將所有記錄檔記錄複製到備份資料夾中的最新記錄檔記錄。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-252">Then, the Reliable State Manager copies all log records, starting from the "start pointer" to the latest log record into the backup folder.</span></span>  <span data-ttu-id="0e9cc-253">因為記錄到最新記錄資料列的所有記錄資料列都會包含於備份中，而且可靠的狀態管理員會保留預寫記錄，所以，可靠的狀態管理員保證所有已認可的交易 (`CommitAsync` 已順利傳回) 都會包含於備份中。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-253">Since all the log records up to the latest log record are included in the backup and the Reliable State Manager preserves write-ahead logging, the Reliable State Manager guarantees that all transactions that are committed (`CommitAsync` has returned successfully) are included in the backup.</span></span>

<span data-ttu-id="0e9cc-254">呼叫 `BackupAsync` 之後認可的任何交易，不一定會在備份中。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-254">Any transaction that commits after `BackupAsync` has been called may or may not be in the backup.</span></span>  <span data-ttu-id="0e9cc-255">一旦由平台填入本機備份資料夾 (亦即執行階段完成的本機備份) 之後，即會叫用服務的備份回呼。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-255">Once the local backup folder has been populated by the platform (i.e., local backup is completed by the runtime), the service's backup callback is invoked.</span></span>  <span data-ttu-id="0e9cc-256">此回呼會負責將備份資料夾移到外部位置，例如 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-256">This callback is responsible for moving the backup folder to an external location such as Azure Storage.</span></span>

### <a name="restore"></a><span data-ttu-id="0e9cc-257">還原</span><span class="sxs-lookup"><span data-stu-id="0e9cc-257">Restore</span></span>
<span data-ttu-id="0e9cc-258">可靠的狀態管理員能夠利用 `RestoreAsync` API，從備份還原。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-258">The Reliable State Manager provides the ability to restore from a backup by using the `RestoreAsync` API.</span></span>  
<span data-ttu-id="0e9cc-259">僅可在 `OnDataLossAsync` 方法內部呼叫 `RestoreContext` 上的 `RestoreAsync` 方法。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-259">The `RestoreAsync` method on `RestoreContext` can be called only inside the `OnDataLossAsync` method.</span></span>
<span data-ttu-id="0e9cc-260">`OnDataLossAsync` 傳回的 Bool 表示服務是否從外部來源還原其狀態。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-260">The bool returned by `OnDataLossAsync` indicates whether the service restored its state from an external source.</span></span>
<span data-ttu-id="0e9cc-261">如果 `OnDataLossAsync` 傳回 true，Service Fabric 將會從這個主要複本重建所有其他複本。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-261">If the `OnDataLossAsync` returns true, Service Fabric will rebuild all other replicas from this primary.</span></span> <span data-ttu-id="0e9cc-262">Service Fabric 可確保將接收 `OnDataLossAsync` 呼叫的複本會先轉換成主要角色，但不會被授與讀取狀態或寫入狀態。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-262">Service Fabric ensures that replicas that will receive `OnDataLossAsync` call first transition to the primary role but are not granted read status or write status.</span></span>
<span data-ttu-id="0e9cc-263">這暗示對於 StatefulService 實施者而言，將不會呼叫 `RunAsync`，直到 `OnDataLossAsync` 成功完成為止。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-263">This implies that for StatefulService implementers, `RunAsync` will not be called until `OnDataLossAsync` finishes successfully.</span></span>
<span data-ttu-id="0e9cc-264">然後，會在新的主要複本上叫用 `OnDataLossAsync`。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-264">Then, `OnDataLossAsync` will be invoked on the new primary.</span></span>
<span data-ttu-id="0e9cc-265">在服務成功完成此 API (藉由傳回 true 或 false) 並完成相關重新設定之前，將會一次一個地繼續呼叫 API。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-265">Until a service completes this API successfully (by returning true or false) and finishes the relevant reconfiguration, the API will keep being called one at a time.</span></span>

<span data-ttu-id="0e9cc-266">`RestoreAsync` 會在過去曾呼叫的主要複本中先卸除所有現有狀態。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-266">`RestoreAsync` first drops all existing state in the primary replica that it was called on.</span></span>  
<span data-ttu-id="0e9cc-267">然後，可靠的狀態管理員會建立存在於備份資料夾中所有可靠的物件。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-267">Then the Reliable State Manager creates all the Reliable objects that exist in the backup folder.</span></span>  
<span data-ttu-id="0e9cc-268">接下來，可靠的物件會獲得指示從其備份資料夾中的檢查點還原。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-268">Next, the Reliable objects are instructed to restore from their checkpoints in the backup folder.</span></span>  
<span data-ttu-id="0e9cc-269">最後，可靠的狀態管理員會從備份資料夾中的記錄檔記錄復原自己的狀態，並執行復原。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-269">Finally, the Reliable State Manager recovers its own state from the log records in the backup folder and performs recovery.</span></span>  
<span data-ttu-id="0e9cc-270">做為復原程序的一部分，作業是從「開始點」開始，在備份資料夾中認可記錄檔記錄，並對可靠的物件重新執行。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-270">As part of the recovery process, operations starting from the "starting point" that have commit log records in the backup folder are replayed to the Reliable objects.</span></span>  
<span data-ttu-id="0e9cc-271">這個步驟可確保復原的狀態一致。</span><span class="sxs-lookup"><span data-stu-id="0e9cc-271">This step ensures that the recovered state is consistent.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e9cc-272">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0e9cc-272">Next steps</span></span>
  - [<span data-ttu-id="0e9cc-273">可靠的集合</span><span class="sxs-lookup"><span data-stu-id="0e9cc-273">Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
  - [<span data-ttu-id="0e9cc-274">Reliable Services 快速入門</span><span class="sxs-lookup"><span data-stu-id="0e9cc-274">Reliable Services quick start</span></span>](service-fabric-reliable-services-quick-start.md)
  - [<span data-ttu-id="0e9cc-275">Reliable Services 通知</span><span class="sxs-lookup"><span data-stu-id="0e9cc-275">Reliable Services notifications</span></span>](service-fabric-reliable-services-notifications.md)
  - [<span data-ttu-id="0e9cc-276">Reliable Services 組態</span><span class="sxs-lookup"><span data-stu-id="0e9cc-276">Reliable Services configuration</span></span>](service-fabric-reliable-services-configuration.md)
  - [<span data-ttu-id="0e9cc-277">可靠的集合的開發人員參考資料</span><span class="sxs-lookup"><span data-stu-id="0e9cc-277">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

