---
title: "aaaService 網狀架構的備份和還原 |Microsoft 文件"
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
ms.openlocfilehash: e502b59c84999c3fe825167383f00a5ebd70c9b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-and-restore-reliable-services-and-reliable-actors"></a><span data-ttu-id="ba8ac-103">備份與還原 Reliable Services 和 Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="ba8ac-103">Back up and restore Reliable Services and Reliable Actors</span></span>
<span data-ttu-id="ba8ac-104">Azure Service Fabric 這項高可用性平台可將 hello 狀態複寫到多個節點 toomaintain 這項高可用性。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-104">Azure Service Fabric is a high-availability platform that replicates hello state across multiple nodes toomaintain this high availability.</span></span>  <span data-ttu-id="ba8ac-105">因此，即使 hello 叢集中的一個節點失敗，hello 服務繼續 toobe 可用。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-105">Thus, even if one node in hello cluster fails, hello services continue toobe available.</span></span> <span data-ttu-id="ba8ac-106">這個 hello 平台所提供的內建備援可能足以用於部分，而在某些情況下最好 hello 服務 tooback 資料備份 （tooan 外部存放區）。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-106">While this in-built redundancy provided by hello platform may be sufficient for some, in certain cases it is desirable for hello service tooback up data (tooan external store).</span></span>

> [!NOTE]
> <span data-ttu-id="ba8ac-107">它是關鍵 toobackup 並還原資料 （與它如預期般運作的測試），您可以從 資料遺失狀況復原。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-107">It is critical toobackup and restore your data (and test that it works as expected) so you can recover from data loss scenarios.</span></span>
> 
> 

<span data-ttu-id="ba8ac-108">例如，服務可能會想 tooback 順序 tooprotect 從 hello 下列案例中的資料：</span><span class="sxs-lookup"><span data-stu-id="ba8ac-108">For example, a service may want tooback up data in order tooprotect from hello following scenarios:</span></span>

- <span data-ttu-id="ba8ac-109">中的 hello 永久遺失整個 Service Fabric 叢集 hello 事件。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-109">In hello event of hello permanent loss of an entire Service Fabric cluster.</span></span>
- <span data-ttu-id="ba8ac-110">大部分的服務資料分割的 hello 複本永久遺失</span><span class="sxs-lookup"><span data-stu-id="ba8ac-110">Permanent loss of a majority of hello replicas of a service partition</span></span>
- <span data-ttu-id="ba8ac-111">讓 hello 狀態不小心取得刪除或損毀的系統管理錯誤。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-111">Administrative errors whereby hello state accidentally gets deleted or corrupted.</span></span> <span data-ttu-id="ba8ac-112">例如，如果此情形具有足夠的權限的系統管理員會錯誤地刪除 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-112">For example, this may happen if an administrator with sufficient privilege erroneously deletes hello service.</span></span>
- <span data-ttu-id="ba8ac-113">Hello 服務中導致資料損毀的錯誤。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-113">Bugs in hello service that cause data corruption.</span></span> <span data-ttu-id="ba8ac-114">比方說，這可能會發生寫入錯誤資料 tooa 可靠集合的服務程式碼升級啟動時。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-114">For example, this may happen when a service code upgrade starts writing faulty data tooa Reliable Collection.</span></span> <span data-ttu-id="ba8ac-115">在這種情況下，同時 hello 程式碼和 hello 資料可能會有 toobe 還原 tooan 先前狀態。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-115">In such a case, both hello code and hello data may have toobe reverted tooan earlier state.</span></span>
- <span data-ttu-id="ba8ac-116">離線資料處理。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-116">Offline data processing.</span></span> <span data-ttu-id="ba8ac-117">可能很方便 toohave 離線處理的商業智慧，分別從 hello 服務所產生的 hello 資料的資料。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-117">It might be convenient toohave offline processing of data for business intelligence that happens separately from hello service that generates hello data.</span></span>

<span data-ttu-id="ba8ac-118">hello 備份/還原功能可讓您建置 hello 可靠的服務應用程式開發介面 toocreate 備份和還原備份的服務。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-118">hello Backup/Restore feature allows services built on hello Reliable Services API toocreate and restore backups.</span></span> <span data-ttu-id="ba8ac-119">hello 備份 hello 平台所提供的 Api 允許的服務資料分割的狀態，而不需要封鎖讀取或寫入作業的備份。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-119">hello backup APIs provided by hello platform allow backup(s) of a service partition's state, without blocking read or write operations.</span></span> <span data-ttu-id="ba8ac-120">hello Api 可讓服務資料分割狀態 toobe 從所選的備份還原的還原。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-120">hello restore APIs allow a service partition's state toobe restored from a chosen backup.</span></span>

## <a name="types-of-backup"></a><span data-ttu-id="ba8ac-121">備份類型</span><span class="sxs-lookup"><span data-stu-id="ba8ac-121">Types of Backup</span></span>
<span data-ttu-id="ba8ac-122">有兩個備份選項︰完整和增量。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-122">There are two backup options: Full and Incremental.</span></span>
<span data-ttu-id="ba8ac-123">完整備份會包含所有 hello 所需資料 toorecreate hello hello 複本狀態的備份： 檢查點和所有記錄檔記錄。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-123">A full backup is a backup that contains all hello data required toorecreate hello state of hello replica: checkpoints and all log records.</span></span>
<span data-ttu-id="ba8ac-124">因為 hello 檢查點和 hello 記錄檔，可以單獨使用時還原完整備份。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-124">Since it has hello checkpoints and hello log, a full backup can be restored by itself.</span></span>

<span data-ttu-id="ba8ac-125">大型 hello 檢查點時，就會發生 hello 發生問題的完整備份。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-125">hello problem with full backups arises when hello checkpoints are large.</span></span>
<span data-ttu-id="ba8ac-126">例如，具有 16 GB 的狀態的複本會有加總大約 too16 GB 的檢查點。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-126">For example, a replica that has 16 GB of state will have checkpoints that add up approximately too16 GB.</span></span>
<span data-ttu-id="ba8ac-127">如果我們有五分鐘的復原點目標，hello 複本就會需要 toobe 備份每隔五分鐘。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-127">If we have a Recovery Point Objective of five minutes, hello replica needs toobe backed up every five minutes.</span></span>
<span data-ttu-id="ba8ac-128">它會備份每次需要 toocopy 16 GB 的檢查點以外的地方 too50 MB (可設定使用`CheckpointThresholdInMB`) 的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-128">Each time it backs up it needs toocopy 16 GB of checkpoints in addition too50 MB (configurable using `CheckpointThresholdInMB`) worth of logs.</span></span>

![完整備份範例。](media/service-fabric-reliable-services-backup-restore/FullBackupExample.PNG)

<span data-ttu-id="ba8ac-130">hello 方案 toothis 問題是增量備份，其中備份僅包含 hello 變更記錄檔記錄 hello 上次備份之後。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-130">hello solution toothis problem is incremental backups, where backup only contains hello changed log records since hello last backup.</span></span>

![增量備份範例。](media/service-fabric-reliable-services-backup-restore/IncrementalBackupExample.PNG)

<span data-ttu-id="ba8ac-132">由於增量備份是只能變更 hello （不包括 hello 檢查點） 的上次備份之後，它們通常 toobe 更快，但也無法還原在他們自己。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-132">Since incremental backups are only changes since hello last backup (does not include hello checkpoints), they tend toobe faster but they cannot be restored on their own.</span></span>
<span data-ttu-id="ba8ac-133">toorestore 增量備份，則需要 hello 整個備份鏈結。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-133">toorestore an incremental backup, hello entire backup chain is required.</span></span>
<span data-ttu-id="ba8ac-134">備份鏈結是一連串的備份，開始為完整備份，而接著是數個連續的增量備份。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-134">A backup chain is a chain of backups starting with a full backup and followed by a number of contiguous incremental backups.</span></span>

## <a name="backup-reliable-services"></a><span data-ttu-id="ba8ac-135">備份 Reliable Services</span><span class="sxs-lookup"><span data-stu-id="ba8ac-135">Backup Reliable Services</span></span>
<span data-ttu-id="ba8ac-136">hello 服務作者可完全控制當 toomake 備份和儲存備份。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-136">hello service author has full control of when toomake backups and where backups will be stored.</span></span>

<span data-ttu-id="ba8ac-137">toostart 備份，hello 服務需要 tooinvoke hello 繼承成員函式`BackupAsync`。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-137">toostart a backup, hello service needs tooinvoke hello inherited member function `BackupAsync`.</span></span>  
<span data-ttu-id="ba8ac-138">只能從主要複本進行備份，而且會要求寫入狀態 toobe 授與。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-138">Backups can be made only from primary replicas, and they require write status toobe granted.</span></span>

<span data-ttu-id="ba8ac-139">如下所示`BackupAsync`接受`BackupDescription`物件，可以在其中一個指定完整或增量備份，以及回呼函式，`Func<< BackupInfo, CancellationToken, Task<bool>>>`時在本機建立 hello 備份資料夾，並準備 toobe 移出 toosome 叫用外部儲存體。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-139">As shown below, `BackupAsync` takes in a `BackupDescription` object, where one can specify a full or incremental backup, as well as a callback function, `Func<< BackupInfo, CancellationToken, Task<bool>>>` that is invoked when hello backup folder has been created locally and is ready toobe moved out toosome external storage.</span></span>

```csharp

BackupDescription myBackupDescription = new BackupDescription(backupOption.Incremental,this.BackupCallbackAsync);

await this.BackupAsync(myBackupDescription);

```

<span data-ttu-id="ba8ac-140">增量備份會失敗並出現要求 tootake `FabricMissingFullBackupException`。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-140">Request tootake an incremental backup can fail with `FabricMissingFullBackupException`.</span></span> <span data-ttu-id="ba8ac-141">這個例外狀況表示發生了一個 hello 下列事項：</span><span class="sxs-lookup"><span data-stu-id="ba8ac-141">This exception indicates that one of hello following things is happening:</span></span>

- <span data-ttu-id="ba8ac-142">hello 複本已永遠不會花費的完整備份，因為它已經變成主要，</span><span class="sxs-lookup"><span data-stu-id="ba8ac-142">hello replica has never taken a full backup since it has become primary,</span></span>
- <span data-ttu-id="ba8ac-143">某些 hello 記錄檔記錄，因為 hello 最後一個備份已被截斷或</span><span class="sxs-lookup"><span data-stu-id="ba8ac-143">some of hello log records since hello last backup has been truncated or</span></span>
- <span data-ttu-id="ba8ac-144">複本傳送嗨`MaxAccumulatedBackupLogSizeInMB`限制。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-144">replica passed hello `MaxAccumulatedBackupLogSizeInMB` limit.</span></span>

<span data-ttu-id="ba8ac-145">使用者提升的設定所能 toodo 增量備份的 hello 可能性`MinLogSizeInMB`或`TruncationThresholdFactor`。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-145">Users can increase hello likelihood of being able toodo incremental backups by configuring `MinLogSizeInMB` or `TruncationThresholdFactor`.</span></span>
<span data-ttu-id="ba8ac-146">請注意，增加這些值會增加每個複本磁碟使用量的 hello。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-146">Note that increasing these values increases hello per replica disk usage.</span></span>
<span data-ttu-id="ba8ac-147">如需詳細資訊，請參閱 [Reliable Services 組態](service-fabric-reliable-services-configuration.md)</span><span class="sxs-lookup"><span data-stu-id="ba8ac-147">For more information, see [Reliable Services Configuration](service-fabric-reliable-services-configuration.md)</span></span>

<span data-ttu-id="ba8ac-148">`BackupInfo`提供有關 hello 備份，包括 hello hello 資料夾 hello 執行階段與 hello 備份儲存位置的資訊 (`BackupInfo.Directory`)。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-148">`BackupInfo` provides information regarding hello backup, including hello location of hello folder where hello runtime saved hello backup (`BackupInfo.Directory`).</span></span> <span data-ttu-id="ba8ac-149">hello 回呼函式可以移動 hello `BackupInfo.Directory` tooan 外部存放區或另一個位置。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-149">hello callback function can move hello `BackupInfo.Directory` tooan external store or another location.</span></span>  <span data-ttu-id="ba8ac-150">此函式也會傳回的布林值，指出是否可以 toosuccessfully 移動 hello 備份資料夾 tooits 目標位置。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-150">This function also returns a bool that indicates whether it was able toosuccessfully move hello backup folder tooits target location.</span></span>

<span data-ttu-id="ba8ac-151">hello 下列程式碼示範如何 hello`BackupCallbackAsync`方法可以是使用的 tooupload hello 備份 tooAzure 儲存體：</span><span class="sxs-lookup"><span data-stu-id="ba8ac-151">hello following code demonstrates how hello `BackupCallbackAsync` method can be used tooupload hello backup tooAzure Storage:</span></span>

```csharp
private async Task<bool> BackupCallbackAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
{
    var backupId = Guid.NewGuid();

    await externalBackupStore.UploadBackupFolderAsync(backupInfo.Directory, backupId, cancellationToken);

    return true;
}
```

<span data-ttu-id="ba8ac-152">在 hello 前面範例中，`ExternalBackupStore`是 hello 範例類別，是使用 Azure Blob 儲存體，使用的 toointerface 和`UploadBackupFolderAsync`是壓縮 hello 資料夾並將它放在 hello Azure Blob 存放區中的 hello 方法。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-152">In hello preceeding example, `ExternalBackupStore` is hello sample class that is used toointerface with Azure Blob storage, and `UploadBackupFolderAsync` is hello method that compresses hello folder and places it in hello Azure Blob store.</span></span>

<span data-ttu-id="ba8ac-153">請注意：</span><span class="sxs-lookup"><span data-stu-id="ba8ac-153">Note that:</span></span>

  - <span data-ttu-id="ba8ac-154">在任何指定時間每個複本只能有一項進行中的備份作業。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-154">There can be only one backup operation in-flight per replica at any given time.</span></span> <span data-ttu-id="ba8ac-155">多個`BackupAsync`一次呼叫會擲回`FabricBackupInProgressException`toolimit 傳遞備份 tooone。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-155">More than one `BackupAsync` call at a time will throw `FabricBackupInProgressException` toolimit inflight backups tooone.</span></span>
  - <span data-ttu-id="ba8ac-156">如果備份正在進行時，複本會容錯移轉，hello 備份可能尚未完成。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-156">If a replica fails over while a backup is in progress, hello backup may not have been completed.</span></span> <span data-ttu-id="ba8ac-157">因此，一旦 hello 容錯移轉完成時，它是 hello 服務責任 toorestart hello 備份叫用`BackupAsync`視。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-157">Thus, once hello failover finishes, it is hello service's responsibility toorestart hello backup by invoking `BackupAsync` as necessary.</span></span>

## <a name="restore-reliable-services"></a><span data-ttu-id="ba8ac-158">還原 Reliable Services</span><span class="sxs-lookup"><span data-stu-id="ba8ac-158">Restore Reliable Services</span></span>
<span data-ttu-id="ba8ac-159">一般情況下，hello 情況下，您可能需要 tooperform 還原作業可分成下列其中一種：</span><span class="sxs-lookup"><span data-stu-id="ba8ac-159">In general, hello cases when you might need tooperform a restore operation fall into one of these categories:</span></span>

  - <span data-ttu-id="ba8ac-160">hello 服務資料分割的資料遺失。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-160">hello service partition lost data.</span></span> <span data-ttu-id="ba8ac-161">例如，hello 三分之二以上複本 （包括 hello 主要複本） 的資料分割的磁碟損毀或抹除。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-161">For example, hello disk for two out of three replicas for a partition (including hello primary replica) gets corrupted or wiped.</span></span> <span data-ttu-id="ba8ac-162">hello 新主要複本可能需要從備份 toorestore 資料。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-162">hello new primary may need toorestore data from a backup.</span></span>
  - <span data-ttu-id="ba8ac-163">hello 整個服務將會遺失。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-163">hello entire service is lost.</span></span> <span data-ttu-id="ba8ac-164">例如，系統管理員移除 hello 整個服務，因此 hello 服務與 hello 資料需要 toobe 還原。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-164">For example, an administrator removes hello entire service and thus hello service and hello data need toobe restored.</span></span>
  - <span data-ttu-id="ba8ac-165">hello 服務複寫損毀的應用程式資料 （例如，由於應用程式錯誤）。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-165">hello service replicated corrupt application data (e.g., because of an application bug).</span></span> <span data-ttu-id="ba8ac-166">在此情況下，hello 服務 toobe 升級或還原的 tooremove hello 原因 hello 損毀或未損毀的資料有 toobe 還原。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-166">In this case, hello service has toobe upgraded or reverted tooremove hello cause of hello corruption, and non-corrupt data has toobe restored.</span></span>

<span data-ttu-id="ba8ac-167">雖然有許多種，我們會提供有關使用的部分範例`RestoreAsync`toorecover 從上述案例 hello。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-167">While many approaches are possible, we offer some examples on using `RestoreAsync` toorecover from hello above scenarios.</span></span>

## <a name="partition-data-loss-in-reliable-services"></a><span data-ttu-id="ba8ac-168">Reliable Services 中的分割區資料遺失</span><span class="sxs-lookup"><span data-stu-id="ba8ac-168">Partition data loss in Reliable Services</span></span>
<span data-ttu-id="ba8ac-169">在此情況下，hello 執行階段會自動偵測 hello 資料遺失，並叫用 hello`OnDataLossAsync`應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-169">In this case, hello runtime would automatically detect hello data loss and invoke hello `OnDataLossAsync` API.</span></span>

<span data-ttu-id="ba8ac-170">hello 服務作者必須遵循 toorecover tooperform hello:</span><span class="sxs-lookup"><span data-stu-id="ba8ac-170">hello service author needs tooperform hello following toorecover:</span></span>

  - <span data-ttu-id="ba8ac-171">覆寫 hello 虛擬基底類別方法`OnDataLossAsync`。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-171">Override hello virtual base class method `OnDataLossAsync`.</span></span>
  - <span data-ttu-id="ba8ac-172">包含 hello 服務備份 hello 外部位置中找到 hello 最新備份。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-172">Find hello latest backup in hello external location that contains hello service's backups.</span></span>
  - <span data-ttu-id="ba8ac-173">下載 hello 最新的備份 （並解壓縮 hello 備份到備份資料夾的 hello，如果壓縮）。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-173">Download hello latest backup (and uncompress hello backup into hello backup folder if it was compressed).</span></span>
  - <span data-ttu-id="ba8ac-174">hello`OnDataLossAsync`方法提供`RestoreContext`。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-174">hello `OnDataLossAsync` method provides a `RestoreContext`.</span></span> <span data-ttu-id="ba8ac-175">呼叫 hello`RestoreAsync`上提供的 hello API `RestoreContext`。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-175">Call hello `RestoreAsync` API on hello provided `RestoreContext`.</span></span>
  - <span data-ttu-id="ba8ac-176">如果 hello 還原作業成功，則傳回 true。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-176">Return true if hello restoration was a success.</span></span>

<span data-ttu-id="ba8ac-177">下列是範例實作的 hello`OnDataLossAsync`方法：</span><span class="sxs-lookup"><span data-stu-id="ba8ac-177">Following is an example implementation of hello `OnDataLossAsync` method:</span></span>

```csharp
protected override async Task<bool> OnDataLossAsync(RestoreContext restoreCtx, CancellationToken cancellationToken)
{
    var backupFolder = await this.externalBackupStore.DownloadLastBackupAsync(cancellationToken);

    var restoreDescription = new RestoreDescription(backupFolder);

    await restoreCtx.RestoreAsync(restoreDescription);

    return true;
}
```

<span data-ttu-id="ba8ac-178">`RestoreDescription`傳入 toohello`RestoreContext.RestoreAsync`呼叫中包含一個名為成員`BackupFolderPath`。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-178">`RestoreDescription` passed in toohello `RestoreContext.RestoreAsync` call contains a member called `BackupFolderPath`.</span></span>
<span data-ttu-id="ba8ac-179">當還原完整備份，這`BackupFolderPath`應該設定 toohello 包含完整備份的 hello 資料夾的本機路徑。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-179">When restoring a single full backup, this `BackupFolderPath` should be set toohello local path of hello folder that contains your full backup.</span></span>
<span data-ttu-id="ba8ac-180">還原完整備份和增量備份時，一些時`BackupFolderPath`應該設定 toohello hello 資料夾不只是包含 hello 完整備份，但也所有 hello 增量備份的本機路徑。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-180">When restoring a full backup and a number of incremental backups, `BackupFolderPath` should be set toohello local path of hello folder that not only contains hello full backup, but also all hello incremental backups.</span></span>
<span data-ttu-id="ba8ac-181">`RestoreAsync`呼叫可能會擲回`FabricMissingFullBackupException`如果 hello`BackupFolderPath`提供不包含完整備份。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-181">`RestoreAsync` call can throw `FabricMissingFullBackupException` if hello `BackupFolderPath` provided does not contain a full backup.</span></span>
<span data-ttu-id="ba8ac-182">如果 `BackupFolderPath` 的增量備份包含中斷的鏈結，它也可能會擲回 `ArgumentException`。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-182">It can also throw `ArgumentException` if `BackupFolderPath` has a broken chain of incremental backups.</span></span>
<span data-ttu-id="ba8ac-183">比方說，如果它包含 hello 完整備份，第一次累加 hello 和 hello 第三個增量備份，但沒有 hello 第二個增量備份。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-183">For example, if it contains hello full backup, hello first incremental and hello third incremental backup but no hello second incremental backup.</span></span>

> [!NOTE]
> <span data-ttu-id="ba8ac-184">根據預設設定 tooSafe hello RestorePolicy。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-184">hello RestorePolicy is set tooSafe by default.</span></span>  <span data-ttu-id="ba8ac-185">這表示該 hello`RestoreAsync`如果它偵測到該 hello 備份資料夾包含早於或等於 toohello 狀態包含在這個複本的狀態，將會失敗並 ArgumentException 的 API。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-185">This means that hello `RestoreAsync` API will fail with ArgumentException if it detects that hello backup folder contains a state that is older than or equal toohello state contained in this replica.</span></span>  <span data-ttu-id="ba8ac-186">`RestorePolicy.Force`可以是使用的 tooskip 這項安全檢查。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-186">`RestorePolicy.Force` can be used tooskip this safety check.</span></span> <span data-ttu-id="ba8ac-187">這會指定為屬於 `RestoreDescription`。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-187">This is specified as part of `RestoreDescription`.</span></span>
> 

## <a name="deleted-or-lost-service"></a><span data-ttu-id="ba8ac-188">已刪除或遺失的服務</span><span class="sxs-lookup"><span data-stu-id="ba8ac-188">Deleted or lost service</span></span>
<span data-ttu-id="ba8ac-189">如果移除服務，您必須先重新建立 hello 服務之前可以還原 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-189">If a service is removed, you must first re-create hello service before hello data can be restored.</span></span>  <span data-ttu-id="ba8ac-190">它是以相同的設定，例如，資料分割配置，因此，hello 資料可以順暢地還原的 hello 重要 toocreate hello 服務。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-190">It is important toocreate hello service with hello same configuration, e.g., partitioning scheme, so that hello data can be restored seamlessly.</span></span>  <span data-ttu-id="ba8ac-191">一旦 hello 服務已啟動，hello API toorestore 資料 (`OnDataLossAsync`上方) 具有 toobe 叫用此服務的每個分割區。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-191">Once hello service is up, hello API toorestore data (`OnDataLossAsync` above) has toobe invoked on every partition of this service.</span></span> <span data-ttu-id="ba8ac-192">達到此動作的其中一種方式，是使用每個分割區上的 `[FabricClient.TestManagementClient.StartPartitionDataLossAsync](https://msdn.microsoft.com/library/mt693569.aspx)`。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-192">One way of achieving this is by using `[FabricClient.TestManagementClient.StartPartitionDataLossAsync](https://msdn.microsoft.com/library/mt693569.aspx)` on every partition.</span></span>  

<span data-ttu-id="ba8ac-193">從這一點，實作是 hello 與 hello 上述案例相同。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-193">From this point, implementation is hello same as hello above scenario.</span></span> <span data-ttu-id="ba8ac-194">每個資料分割需要 toorestore hello 最新相關備份 hello 外部存放區。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-194">Each partition needs toorestore hello latest relevant backup from hello external store.</span></span> <span data-ttu-id="ba8ac-195">必須注意的是該 hello 資料分割識別碼可能立即變更，因為 hello 執行階段以動態方式建立資料分割識別碼。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-195">One caveat is that hello partition ID may have now changed, since hello runtime creates partition IDs dynamically.</span></span> <span data-ttu-id="ba8ac-196">因此，hello 服務必須 toostore hello 適當的分割區資訊和服務名稱 tooidentify hello 正確最新備份 toorestore 從每個資料分割。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-196">Thus, hello service needs toostore hello appropriate partition information and service name tooidentify hello correct latest backup toorestore from for each partition.</span></span>

> [!NOTE]
> <span data-ttu-id="ba8ac-197">建議您不要 toouse`FabricClient.ServiceManager.InvokeDataLossAsync`上每個資料分割 toorestore hello 整個服務，因為，可能會損毀您的叢集狀態。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-197">It is not recommended toouse `FabricClient.ServiceManager.InvokeDataLossAsync` on each partition toorestore hello entire service, since that may corrupt your cluster state.</span></span>
> 

## <a name="replication-of-corrupt-application-data"></a><span data-ttu-id="ba8ac-198">損毀之應用程式資料的複寫</span><span class="sxs-lookup"><span data-stu-id="ba8ac-198">Replication of corrupt application data</span></span>
<span data-ttu-id="ba8ac-199">如果新部署的 hello 應用程式升級有 bug，導致資料損毀。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-199">If hello newly deployed application upgrade has a bug, that may cause corruption of data.</span></span> <span data-ttu-id="ba8ac-200">例如，應用程式升級可能啟動 tooupdate 每個電話號碼的記錄中具有無效的區碼可靠字典。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-200">For example, an application upgrade may start tooupdate every phone number record in a Reliable Dictionary with an invalid area code.</span></span>  <span data-ttu-id="ba8ac-201">在此情況下，由於 Service Fabric 並不知道 hello 資料會儲存 hello 本質，將複寫 hello 無效電話號碼。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-201">In this case, hello invalid phone numbers will be replicated since Service Fabric is not aware of hello nature of hello data that is being stored.</span></span>

<span data-ttu-id="ba8ac-202">hello 首先 toodo 偵測這類嚴重的錯誤會導致資料損毀之後是 toofreeze hello 服務 hello 應用程式層級，而且如果可能，升級 toohello 版本沒有 hello bug 的 hello 應用程式程式碼。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-202">hello first thing toodo after you detect such an egregious bug that causes data corruption is toofreeze hello service at hello application level and, if possible, upgrade toohello version of hello application code that does not have hello bug.</span></span>  <span data-ttu-id="ba8ac-203">不過，即使修正 hello 服務程式碼後，hello 資料仍可能已損毀，因此資料可能需要還原 toobe。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-203">However, even after hello service code is fixed, hello data may still be corrupt and thus data may need toobe restored.</span></span>  <span data-ttu-id="ba8ac-204">在這種情況下，它可能無法足夠 toorestore hello 最新備份，因為 hello 最新備份也可能已損毀。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-204">In such cases, it may not be sufficient toorestore hello latest backup, since hello latest backups may also be corrupt.</span></span>  <span data-ttu-id="ba8ac-205">因此，您必須 toofind hello 最後一次備份之前 hello 資料損毀。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-205">Thus, you have toofind hello last backup that was made before hello data got corrupted.</span></span>

<span data-ttu-id="ba8ac-206">如果您不確定哪一個備份已損毀，您無法部署新的 Service Fabric 叢集，並還原受影響的資料分割，如同上述 「 刪除或遺失的服務 」 的 hello hello 備份案例。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-206">If you are not sure which backups are corrupt, you could deploy a new Service Fabric cluster and restore hello backups of affected partitions just like hello above "Deleted or lost service" scenario.</span></span>  <span data-ttu-id="ba8ac-207">對於每個資料分割，開始使用至少從 hello 最近 toohello 還原 hello 備份。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-207">For each partition, start restoring hello backups from hello most recent toohello least.</span></span> <span data-ttu-id="ba8ac-208">一旦您找到並沒有 hello 損毀的備份，移動/delete 的這個資料分割是較新 （比該備份） 的所有備份。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-208">Once you find a backup that does not have hello corruption, move/delete all backups of this partition that were more recent (than that backup).</span></span> <span data-ttu-id="ba8ac-209">針對每個資料分割重複此程序。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-209">Repeat this process for each partition.</span></span> <span data-ttu-id="ba8ac-210">現在，當`OnDataLossAsync`稱為 hello 生產叢集中的 hello 磁碟分割，hello 最後一個備份位於 hello 外部存放區才能 hello 上述程序的其中一個選取的 hello。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-210">Now, when `OnDataLossAsync` is called on hello partition in hello production cluster, hello last backup found in hello external store will be hello one picked by hello above process.</span></span>

<span data-ttu-id="ba8ac-211">Hello hello 「 已刪除或遺失的服務 」 中的步驟，可以是區段 hello 下列程式碼已損毀 hello 狀態之前，請使用 hello 服務 toohello 狀態 toorestore hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-211">Now, hello steps in hello "Deleted or lost service" section can be used toorestore hello state of hello service toohello state before hello buggy code corrupted hello state.</span></span>

<span data-ttu-id="ba8ac-212">請注意：</span><span class="sxs-lookup"><span data-stu-id="ba8ac-212">Note that:</span></span>

  - <span data-ttu-id="ba8ac-213">還原時，有機會讓的 hello 備份正在還原比 hello hello 磁碟分割狀態之前 hello 資料已遺失。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-213">When you restore, there is a chance that hello backup being restored is older than hello state of hello partition before hello data was lost.</span></span> <span data-ttu-id="ba8ac-214">因為這個緣故，您應該還原只能作為最後的手段 toorecover 最多資料越好。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-214">Because of this, you should restore only as a last resort toorecover as much data as possible.</span></span>
  - <span data-ttu-id="ba8ac-215">hello 代表 hello 備份資料夾路徑的字串和 hello hello 備份資料夾內檔案的路徑可能會大於 255 個字元，取決於 hello FabricDataRoot 路徑和應用程式類型名稱的長度。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-215">hello string that represents hello backup folder path and hello paths of files inside hello backup folder can be greater than 255 characters, depending on hello FabricDataRoot path and Application Type name's length.</span></span> <span data-ttu-id="ba8ac-216">這會造成某些.NET 方法，例如`Directory.Move`，toothrow hello`PathTooLongException`例外狀況。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-216">This can cause some .NET methods, like `Directory.Move`, toothrow hello `PathTooLongException` exception.</span></span> <span data-ttu-id="ba8ac-217">解決方法之一是 toodirectly 呼叫 kernel32 Api，像是`CopyFile`。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-217">One workaround is toodirectly call kernel32 APIs, like `CopyFile`.</span></span>

## <a name="backup-and-restore-reliable-actors"></a><span data-ttu-id="ba8ac-218">備份與還原 Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="ba8ac-218">Backup and restore Reliable Actors</span></span>


<span data-ttu-id="ba8ac-219">Reliable Actors 架構以 Reliable Services 為基礎。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-219">Reliable Actors Framework is built on top of Reliable Services.</span></span> <span data-ttu-id="ba8ac-220">hello ActorService 裝載 hello actor(s) 是可設定狀態的可靠服務。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-220">hello ActorService which hosts hello actor(s) is a stateful reliable service.</span></span> <span data-ttu-id="ba8ac-221">因此，所有 hello 備份和還原功能可在可靠的服務也是可用 tooReliable 執行者 （除非是狀態服務提供者特定的行為）。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-221">Hence, all hello backup and restore functionality available in Reliable Services is also available tooReliable Actors (except behaviors that are state provider specific).</span></span> <span data-ttu-id="ba8ac-222">因為是依個別分割區進行備份，將會備份該分割區中所有動作項目的狀態 (還原也一樣依個別分割區進行)。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-222">Since backups will be taken on a per-partition basis, states for all actors in that partition will be backed up (and restoration is similar and will happen on a per-partition basis).</span></span> <span data-ttu-id="ba8ac-223">tooperform 備份/還原、 hello 服務擁有者應該建立自訂動作項目服務類別衍生自 ActorService 類別並再執行備份/還原類似 tooReliable 上面所述在上一節中的服務。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-223">tooperform backup/restore, hello service owner should create a custom actor service class that derives from ActorService class and then do backup/restore similar tooReliable Services as described above in previous sections.</span></span>

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

<span data-ttu-id="ba8ac-224">當您建立自訂動作項目服務類別時，您需要 tooregister，以及註冊 hello 動作項目時。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-224">When you create a custom actor service class, you need tooregister that as well when registering hello actor.</span></span>

```csharp
ActorRuntime.RegisterActorAsync<MyActor>(
   (context, typeInfo) => new MyCustomActorService(context, typeInfo)).GetAwaiter().GetResult();
```

<span data-ttu-id="ba8ac-225">hello Reliable Actors 的預設狀態提供者是`KvsActorStateProvider`。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-225">hello default state provider for Reliable Actors is `KvsActorStateProvider`.</span></span> <span data-ttu-id="ba8ac-226">`KvsActorStateProvider` 依預設不啟用增量備份。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-226">Incremental backup is not enabled by default for `KvsActorStateProvider`.</span></span> <span data-ttu-id="ba8ac-227">您可以藉由建立啟用增量備份`KvsActorStateProvider`hello 與適當的設定在其建構函式，然後再將它傳遞 tooActorService 建構函式在下列程式碼片段所示：</span><span class="sxs-lookup"><span data-stu-id="ba8ac-227">You can enable incremental backup by creating `KvsActorStateProvider` with hello appropriate setting in its constructor and then passing it tooActorService constructor as shown in following code snippet:</span></span>

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

<span data-ttu-id="ba8ac-228">在啟用增量備份之後，進行增量備份可能會失敗並 FabricMissingFullBackupException 下列原因之一，而且您必須在執行增量備份之前 tootake 完整備份：</span><span class="sxs-lookup"><span data-stu-id="ba8ac-228">After incremental backup has been enabled, taking an incremental backup can fail with FabricMissingFullBackupException for one of following reasons and you will need tootake a full backup before taking incremental backup(s):</span></span>

  - <span data-ttu-id="ba8ac-229">因為它會變成主要 hello 複本已經從未使用過的完整備份。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-229">hello replica has never taken a full backup since it became primary.</span></span>
  - <span data-ttu-id="ba8ac-230">所以最後一個備份，已截斷 hello 記錄檔記錄的某些項目。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-230">Some of hello log records were truncated since last backup was taken.</span></span>

<span data-ttu-id="ba8ac-231">啟用增量備份時，`KvsActorStateProvider`不會使用循環緩衝區 toomanage 其記錄檔記錄，並定期會截斷。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-231">When incremental backup is enabled, `KvsActorStateProvider` does not use circular buffer toomanage its log records and periodically truncates it.</span></span> <span data-ttu-id="ba8ac-232">如果沒有備份是使用者一段 45 分鐘內，hello 系統會自動截斷 hello 記錄檔記錄。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-232">If no backup is taken by user for a period of 45 minutes, hello system automatically truncates hello log records.</span></span> <span data-ttu-id="ba8ac-233">此間隔可以設定藉由指定`logTrunctationIntervalInMinutes`中`KvsActorStateProvider`建構函式 (類似 toowhen 啟用累加備份)。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-233">This interval can be configured by specifying `logTrunctationIntervalInMinutes` in `KvsActorStateProvider` constructor (similar toowhen enabling incremental backup).</span></span> <span data-ttu-id="ba8ac-234">如果主要複本需要 toobuild 另一個複本傳送所有資料，也可能會取得截斷 hello 記錄。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-234">hello log records may also get truncated if primary replica need toobuild another replica by sending all its data.</span></span>

<span data-ttu-id="ba8ac-235">當執行還原備份鏈結，類似 tooReliable 服務，從 hello BackupFolderPath 應該包含具有一個包含完整備份和其他項目包含增量備份的子目錄的子目錄的子目錄。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-235">When doing restore from a backup chain, similar tooReliable Services, hello BackupFolderPath should contain subdirectories with one subdirectory containing full backup and others subdirectories containing incremental backup(s).</span></span> <span data-ttu-id="ba8ac-236">hello 還原 API 將會擲回 FabricException 適當錯誤訊息 hello 備份鏈結驗證失敗時。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-236">hello restore API will throw FabricException with appropriate error message if hello backup chain validation fails.</span></span> 

> [!NOTE]
> <span data-ttu-id="ba8ac-237">`KvsActorStateProvider`目前會忽略 hello 選項 RestorePolicy.Safe。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-237">`KvsActorStateProvider` currently ignores hello option RestorePolicy.Safe.</span></span> <span data-ttu-id="ba8ac-238">即將推出的版本已規劃支援這項功能。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-238">Support for this feature is planned in an upcoming release.</span></span>
> 

## <a name="testing-backup-and-restore"></a><span data-ttu-id="ba8ac-239">測試備份和還原</span><span class="sxs-lookup"><span data-stu-id="ba8ac-239">Testing Backup and Restore</span></span>
<span data-ttu-id="ba8ac-240">重要 tooensure 重要資料會進行備份，並可從還原它。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-240">It is important tooensure that critical data is being backed up, and can be restored from.</span></span> <span data-ttu-id="ba8ac-241">這可藉由叫用 hello`Start-ServiceFabricPartitionDataLoss`中可能會促使中特定資料分割 tootest 資料遺失，是否 hello 資料備份和還原功能，針對您的服務是否正常運作的 PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-241">This can be done by invoking hello `Start-ServiceFabricPartitionDataLoss` cmdlet in PowerShell that can induce data loss in a particular partition tootest whether hello data backup and restore functionality for your service is working as expected.</span></span>  <span data-ttu-id="ba8ac-242">它也是可能 tooprogrammatically 叫用資料遺失，並從該事件，以及還原。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-242">It is also possible tooprogrammatically invoke data loss and restore from that event as well.</span></span>

> [!NOTE]
> <span data-ttu-id="ba8ac-243">您可以尋找範例的實作備份和還原 hello GitHub 上的 Web 參考應用程式中的功能。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-243">You can find a sample implementation of backup and restore functionality in hello Web Reference App on GitHub.</span></span> <span data-ttu-id="ba8ac-244">請查看 hello`Inventory.Service`服務以取得更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-244">Please look at hello `Inventory.Service` service for more details.</span></span>
> 
> 

## <a name="under-hello-hood-more-details-on-backup-and-restore"></a><span data-ttu-id="ba8ac-245">Hello 幕後： 對備份和還原的更多詳細資料</span><span class="sxs-lookup"><span data-stu-id="ba8ac-245">Under hello hood: more details on backup and restore</span></span>
<span data-ttu-id="ba8ac-246">以下是備份與還原的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-246">Here's some more details on backup and restore.</span></span>

### <a name="backup"></a><span data-ttu-id="ba8ac-247">備份</span><span class="sxs-lookup"><span data-stu-id="ba8ac-247">Backup</span></span>
<span data-ttu-id="ba8ac-248">hello 可靠狀態管理員提供 hello 能力 toocreate 一致的備份而不會封鎖任何讀取或寫入作業。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-248">hello Reliable State Manager provides hello ability toocreate consistent backups without blocking any read or write operations.</span></span> <span data-ttu-id="ba8ac-249">toodo 因此，它會運用檢查點和記錄檔的持續性機制。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-249">toodo so, it utilizes a checkpoint and log persistence mechanism.</span></span>  <span data-ttu-id="ba8ac-250">hello 可靠狀態管理員會在 hello 交易記錄檔中特定點 toorelieve 壓力模糊 （輕量型） 的檢查點，並改善復原時間。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-250">hello Reliable State Manager takes fuzzy (lightweight) checkpoints at certain points toorelieve pressure from hello transactional log and improve recovery times.</span></span>  <span data-ttu-id="ba8ac-251">當`BackupAsync`呼叫時，hello 可靠狀態管理員會指示所有可靠物件 toocopy 其最新檢查點檔案 tooa 本機備份資料夾。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-251">When `BackupAsync` is called, hello Reliable State Manager instructs all Reliable objects toocopy their latest checkpoint files tooa local backup folder.</span></span>  <span data-ttu-id="ba8ac-252">然後，hello 可靠狀態管理員會複製所有的記錄檔記錄，到 hello 備份資料夾從 hello 「 啟動指標 」 toohello 最新記錄檔記錄。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-252">Then, hello Reliable State Manager copies all log records, starting from hello "start pointer" toohello latest log record into hello backup folder.</span></span>  <span data-ttu-id="ba8ac-253">由於 hello 備份中包含所有 hello 記錄檔記錄總 toohello 最新的記錄檔記錄，而且 hello 可靠狀態管理員會保留預先寫入記錄，可保證 hello 可靠狀態管理員的所有交易，都都會認可 (`CommitAsync`已傳回已成功） 會包含在 hello 備份。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-253">Since all hello log records up toohello latest log record are included in hello backup and hello Reliable State Manager preserves write-ahead logging, hello Reliable State Manager guarantees that all transactions that are committed (`CommitAsync` has returned successfully) are included in hello backup.</span></span>

<span data-ttu-id="ba8ac-254">認可之後的任何交易`BackupAsync`已呼叫可能或可能不在 hello 備份。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-254">Any transaction that commits after `BackupAsync` has been called may or may not be in hello backup.</span></span>  <span data-ttu-id="ba8ac-255">一旦 hello 本機備份資料夾已經填入 hello 平台 （亦即，本機備份完成時由 hello 執行階段），會叫用 hello 服務備份回呼。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-255">Once hello local backup folder has been populated by hello platform (i.e., local backup is completed by hello runtime), hello service's backup callback is invoked.</span></span>  <span data-ttu-id="ba8ac-256">此回呼會負責移動例如 Azure 儲存體的 hello 備份資料夾 tooan 外部位置。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-256">This callback is responsible for moving hello backup folder tooan external location such as Azure Storage.</span></span>

### <a name="restore"></a><span data-ttu-id="ba8ac-257">還原</span><span class="sxs-lookup"><span data-stu-id="ba8ac-257">Restore</span></span>
<span data-ttu-id="ba8ac-258">hello 可靠狀態管理員提供從備份使用 hello hello 能力 toorestore`RestoreAsync`應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-258">hello Reliable State Manager provides hello ability toorestore from a backup by using hello `RestoreAsync` API.</span></span>  
<span data-ttu-id="ba8ac-259">hello`RestoreAsync`方法`RestoreContext`可以只在 hello 呼叫`OnDataLossAsync`方法。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-259">hello `RestoreAsync` method on `RestoreContext` can be called only inside hello `OnDataLossAsync` method.</span></span>
<span data-ttu-id="ba8ac-260">hello 傳回 bool`OnDataLossAsync`指出 hello 服務是否已還原其狀態從外部來源。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-260">hello bool returned by `OnDataLossAsync` indicates whether hello service restored its state from an external source.</span></span>
<span data-ttu-id="ba8ac-261">如果 hello`OnDataLossAsync`傳回 true，表示服務的網狀架構將會重建所有其他的主要複本。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-261">If hello `OnDataLossAsync` returns true, Service Fabric will rebuild all other replicas from this primary.</span></span> <span data-ttu-id="ba8ac-262">Service Fabric 可確保複本將會接收`OnDataLossAsync`呼叫第一個轉換 toohello 主要角色，但不會被授與讀取狀態或寫入狀態。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-262">Service Fabric ensures that replicas that will receive `OnDataLossAsync` call first transition toohello primary role but are not granted read status or write status.</span></span>
<span data-ttu-id="ba8ac-263">這暗示對於 StatefulService 實施者而言，將不會呼叫 `RunAsync`，直到 `OnDataLossAsync` 成功完成為止。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-263">This implies that for StatefulService implementers, `RunAsync` will not be called until `OnDataLossAsync` finishes successfully.</span></span>
<span data-ttu-id="ba8ac-264">然後， `OnDataLossAsync` hello 新主要複本上將會叫用。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-264">Then, `OnDataLossAsync` will be invoked on hello new primary.</span></span>
<span data-ttu-id="ba8ac-265">服務已成功 （藉由傳回 true 或 false） 完成此應用程式開發介面，然後再完成 hello 相關重新設定，hello API 會保持呼叫一次。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-265">Until a service completes this API successfully (by returning true or false) and finishes hello relevant reconfiguration, hello API will keep being called one at a time.</span></span>

<span data-ttu-id="ba8ac-266">`RestoreAsync`先卸除 hello 呼叫它的主要複本中所有現有的狀態。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-266">`RestoreAsync` first drops all existing state in hello primary replica that it was called on.</span></span>  
<span data-ttu-id="ba8ac-267">然後 hello 可靠狀態管理員會建立所有 hello 可靠物件存在於 hello 備份資料夾中。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-267">Then hello Reliable State Manager creates all hello Reliable objects that exist in hello backup folder.</span></span>  
<span data-ttu-id="ba8ac-268">接下來，hello 可靠物件會指示 toorestore 從其 hello 備份資料夾中的檢查點。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-268">Next, hello Reliable objects are instructed toorestore from their checkpoints in hello backup folder.</span></span>  
<span data-ttu-id="ba8ac-269">最後，hello 可靠狀態管理員復原自己的狀態從 hello hello 備份資料夾中的記錄檔記錄，並執行復原。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-269">Finally, hello Reliable State Manager recovers its own state from hello log records in hello backup folder and performs recovery.</span></span>  
<span data-ttu-id="ba8ac-270">Hello 復原程序的一部分，從 hello 起始點 」 開始 hello 備份資料夾中已認可的記錄檔記錄的作業是在重新執行的 toohello 可靠的物件。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-270">As part of hello recovery process, operations starting from hello "starting point" that have commit log records in hello backup folder are replayed toohello Reliable objects.</span></span>  
<span data-ttu-id="ba8ac-271">這個步驟可確保該 hello 復原的狀態不一致。</span><span class="sxs-lookup"><span data-stu-id="ba8ac-271">This step ensures that hello recovered state is consistent.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba8ac-272">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ba8ac-272">Next steps</span></span>
  - [<span data-ttu-id="ba8ac-273">可靠的集合</span><span class="sxs-lookup"><span data-stu-id="ba8ac-273">Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
  - [<span data-ttu-id="ba8ac-274">Reliable Services 快速入門</span><span class="sxs-lookup"><span data-stu-id="ba8ac-274">Reliable Services quick start</span></span>](service-fabric-reliable-services-quick-start.md)
  - [<span data-ttu-id="ba8ac-275">Reliable Services 通知</span><span class="sxs-lookup"><span data-stu-id="ba8ac-275">Reliable Services notifications</span></span>](service-fabric-reliable-services-notifications.md)
  - [<span data-ttu-id="ba8ac-276">Reliable Services 組態</span><span class="sxs-lookup"><span data-stu-id="ba8ac-276">Reliable Services configuration</span></span>](service-fabric-reliable-services-configuration.md)
  - [<span data-ttu-id="ba8ac-277">可靠的集合的開發人員參考資料</span><span class="sxs-lookup"><span data-stu-id="ba8ac-277">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

