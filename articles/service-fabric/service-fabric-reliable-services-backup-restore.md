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
# <a name="back-up-and-restore-reliable-services-and-reliable-actors"></a>備份與還原 Reliable Services 和 Reliable Actors
Azure Service Fabric 這項高可用性平台可將 hello 狀態複寫到多個節點 toomaintain 這項高可用性。  因此，即使 hello 叢集中的一個節點失敗，hello 服務繼續 toobe 可用。 這個 hello 平台所提供的內建備援可能足以用於部分，而在某些情況下最好 hello 服務 tooback 資料備份 （tooan 外部存放區）。

> [!NOTE]
> 它是關鍵 toobackup 並還原資料 （與它如預期般運作的測試），您可以從 資料遺失狀況復原。
> 
> 

例如，服務可能會想 tooback 順序 tooprotect 從 hello 下列案例中的資料：

- 中的 hello 永久遺失整個 Service Fabric 叢集 hello 事件。
- 大部分的服務資料分割的 hello 複本永久遺失
- 讓 hello 狀態不小心取得刪除或損毀的系統管理錯誤。 例如，如果此情形具有足夠的權限的系統管理員會錯誤地刪除 hello 服務。
- Hello 服務中導致資料損毀的錯誤。 比方說，這可能會發生寫入錯誤資料 tooa 可靠集合的服務程式碼升級啟動時。 在這種情況下，同時 hello 程式碼和 hello 資料可能會有 toobe 還原 tooan 先前狀態。
- 離線資料處理。 可能很方便 toohave 離線處理的商業智慧，分別從 hello 服務所產生的 hello 資料的資料。

hello 備份/還原功能可讓您建置 hello 可靠的服務應用程式開發介面 toocreate 備份和還原備份的服務。 hello 備份 hello 平台所提供的 Api 允許的服務資料分割的狀態，而不需要封鎖讀取或寫入作業的備份。 hello Api 可讓服務資料分割狀態 toobe 從所選的備份還原的還原。

## <a name="types-of-backup"></a>備份類型
有兩個備份選項︰完整和增量。
完整備份會包含所有 hello 所需資料 toorecreate hello hello 複本狀態的備份： 檢查點和所有記錄檔記錄。
因為 hello 檢查點和 hello 記錄檔，可以單獨使用時還原完整備份。

大型 hello 檢查點時，就會發生 hello 發生問題的完整備份。
例如，具有 16 GB 的狀態的複本會有加總大約 too16 GB 的檢查點。
如果我們有五分鐘的復原點目標，hello 複本就會需要 toobe 備份每隔五分鐘。
它會備份每次需要 toocopy 16 GB 的檢查點以外的地方 too50 MB (可設定使用`CheckpointThresholdInMB`) 的記錄檔。

![完整備份範例。](media/service-fabric-reliable-services-backup-restore/FullBackupExample.PNG)

hello 方案 toothis 問題是增量備份，其中備份僅包含 hello 變更記錄檔記錄 hello 上次備份之後。

![增量備份範例。](media/service-fabric-reliable-services-backup-restore/IncrementalBackupExample.PNG)

由於增量備份是只能變更 hello （不包括 hello 檢查點） 的上次備份之後，它們通常 toobe 更快，但也無法還原在他們自己。
toorestore 增量備份，則需要 hello 整個備份鏈結。
備份鏈結是一連串的備份，開始為完整備份，而接著是數個連續的增量備份。

## <a name="backup-reliable-services"></a>備份 Reliable Services
hello 服務作者可完全控制當 toomake 備份和儲存備份。

toostart 備份，hello 服務需要 tooinvoke hello 繼承成員函式`BackupAsync`。  
只能從主要複本進行備份，而且會要求寫入狀態 toobe 授與。

如下所示`BackupAsync`接受`BackupDescription`物件，可以在其中一個指定完整或增量備份，以及回呼函式，`Func<< BackupInfo, CancellationToken, Task<bool>>>`時在本機建立 hello 備份資料夾，並準備 toobe 移出 toosome 叫用外部儲存體。

```csharp

BackupDescription myBackupDescription = new BackupDescription(backupOption.Incremental,this.BackupCallbackAsync);

await this.BackupAsync(myBackupDescription);

```

增量備份會失敗並出現要求 tootake `FabricMissingFullBackupException`。 這個例外狀況表示發生了一個 hello 下列事項：

- hello 複本已永遠不會花費的完整備份，因為它已經變成主要，
- 某些 hello 記錄檔記錄，因為 hello 最後一個備份已被截斷或
- 複本傳送嗨`MaxAccumulatedBackupLogSizeInMB`限制。

使用者提升的設定所能 toodo 增量備份的 hello 可能性`MinLogSizeInMB`或`TruncationThresholdFactor`。
請注意，增加這些值會增加每個複本磁碟使用量的 hello。
如需詳細資訊，請參閱 [Reliable Services 組態](service-fabric-reliable-services-configuration.md)

`BackupInfo`提供有關 hello 備份，包括 hello hello 資料夾 hello 執行階段與 hello 備份儲存位置的資訊 (`BackupInfo.Directory`)。 hello 回呼函式可以移動 hello `BackupInfo.Directory` tooan 外部存放區或另一個位置。  此函式也會傳回的布林值，指出是否可以 toosuccessfully 移動 hello 備份資料夾 tooits 目標位置。

hello 下列程式碼示範如何 hello`BackupCallbackAsync`方法可以是使用的 tooupload hello 備份 tooAzure 儲存體：

```csharp
private async Task<bool> BackupCallbackAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
{
    var backupId = Guid.NewGuid();

    await externalBackupStore.UploadBackupFolderAsync(backupInfo.Directory, backupId, cancellationToken);

    return true;
}
```

在 hello 前面範例中，`ExternalBackupStore`是 hello 範例類別，是使用 Azure Blob 儲存體，使用的 toointerface 和`UploadBackupFolderAsync`是壓縮 hello 資料夾並將它放在 hello Azure Blob 存放區中的 hello 方法。

請注意：

  - 在任何指定時間每個複本只能有一項進行中的備份作業。 多個`BackupAsync`一次呼叫會擲回`FabricBackupInProgressException`toolimit 傳遞備份 tooone。
  - 如果備份正在進行時，複本會容錯移轉，hello 備份可能尚未完成。 因此，一旦 hello 容錯移轉完成時，它是 hello 服務責任 toorestart hello 備份叫用`BackupAsync`視。

## <a name="restore-reliable-services"></a>還原 Reliable Services
一般情況下，hello 情況下，您可能需要 tooperform 還原作業可分成下列其中一種：

  - hello 服務資料分割的資料遺失。 例如，hello 三分之二以上複本 （包括 hello 主要複本） 的資料分割的磁碟損毀或抹除。 hello 新主要複本可能需要從備份 toorestore 資料。
  - hello 整個服務將會遺失。 例如，系統管理員移除 hello 整個服務，因此 hello 服務與 hello 資料需要 toobe 還原。
  - hello 服務複寫損毀的應用程式資料 （例如，由於應用程式錯誤）。 在此情況下，hello 服務 toobe 升級或還原的 tooremove hello 原因 hello 損毀或未損毀的資料有 toobe 還原。

雖然有許多種，我們會提供有關使用的部分範例`RestoreAsync`toorecover 從上述案例 hello。

## <a name="partition-data-loss-in-reliable-services"></a>Reliable Services 中的分割區資料遺失
在此情況下，hello 執行階段會自動偵測 hello 資料遺失，並叫用 hello`OnDataLossAsync`應用程式開發介面。

hello 服務作者必須遵循 toorecover tooperform hello:

  - 覆寫 hello 虛擬基底類別方法`OnDataLossAsync`。
  - 包含 hello 服務備份 hello 外部位置中找到 hello 最新備份。
  - 下載 hello 最新的備份 （並解壓縮 hello 備份到備份資料夾的 hello，如果壓縮）。
  - hello`OnDataLossAsync`方法提供`RestoreContext`。 呼叫 hello`RestoreAsync`上提供的 hello API `RestoreContext`。
  - 如果 hello 還原作業成功，則傳回 true。

下列是範例實作的 hello`OnDataLossAsync`方法：

```csharp
protected override async Task<bool> OnDataLossAsync(RestoreContext restoreCtx, CancellationToken cancellationToken)
{
    var backupFolder = await this.externalBackupStore.DownloadLastBackupAsync(cancellationToken);

    var restoreDescription = new RestoreDescription(backupFolder);

    await restoreCtx.RestoreAsync(restoreDescription);

    return true;
}
```

`RestoreDescription`傳入 toohello`RestoreContext.RestoreAsync`呼叫中包含一個名為成員`BackupFolderPath`。
當還原完整備份，這`BackupFolderPath`應該設定 toohello 包含完整備份的 hello 資料夾的本機路徑。
還原完整備份和增量備份時，一些時`BackupFolderPath`應該設定 toohello hello 資料夾不只是包含 hello 完整備份，但也所有 hello 增量備份的本機路徑。
`RestoreAsync`呼叫可能會擲回`FabricMissingFullBackupException`如果 hello`BackupFolderPath`提供不包含完整備份。
如果 `BackupFolderPath` 的增量備份包含中斷的鏈結，它也可能會擲回 `ArgumentException`。
比方說，如果它包含 hello 完整備份，第一次累加 hello 和 hello 第三個增量備份，但沒有 hello 第二個增量備份。

> [!NOTE]
> 根據預設設定 tooSafe hello RestorePolicy。  這表示該 hello`RestoreAsync`如果它偵測到該 hello 備份資料夾包含早於或等於 toohello 狀態包含在這個複本的狀態，將會失敗並 ArgumentException 的 API。  `RestorePolicy.Force`可以是使用的 tooskip 這項安全檢查。 這會指定為屬於 `RestoreDescription`。
> 

## <a name="deleted-or-lost-service"></a>已刪除或遺失的服務
如果移除服務，您必須先重新建立 hello 服務之前可以還原 hello 資料。  它是以相同的設定，例如，資料分割配置，因此，hello 資料可以順暢地還原的 hello 重要 toocreate hello 服務。  一旦 hello 服務已啟動，hello API toorestore 資料 (`OnDataLossAsync`上方) 具有 toobe 叫用此服務的每個分割區。 達到此動作的其中一種方式，是使用每個分割區上的 `[FabricClient.TestManagementClient.StartPartitionDataLossAsync](https://msdn.microsoft.com/library/mt693569.aspx)`。  

從這一點，實作是 hello 與 hello 上述案例相同。 每個資料分割需要 toorestore hello 最新相關備份 hello 外部存放區。 必須注意的是該 hello 資料分割識別碼可能立即變更，因為 hello 執行階段以動態方式建立資料分割識別碼。 因此，hello 服務必須 toostore hello 適當的分割區資訊和服務名稱 tooidentify hello 正確最新備份 toorestore 從每個資料分割。

> [!NOTE]
> 建議您不要 toouse`FabricClient.ServiceManager.InvokeDataLossAsync`上每個資料分割 toorestore hello 整個服務，因為，可能會損毀您的叢集狀態。
> 

## <a name="replication-of-corrupt-application-data"></a>損毀之應用程式資料的複寫
如果新部署的 hello 應用程式升級有 bug，導致資料損毀。 例如，應用程式升級可能啟動 tooupdate 每個電話號碼的記錄中具有無效的區碼可靠字典。  在此情況下，由於 Service Fabric 並不知道 hello 資料會儲存 hello 本質，將複寫 hello 無效電話號碼。

hello 首先 toodo 偵測這類嚴重的錯誤會導致資料損毀之後是 toofreeze hello 服務 hello 應用程式層級，而且如果可能，升級 toohello 版本沒有 hello bug 的 hello 應用程式程式碼。  不過，即使修正 hello 服務程式碼後，hello 資料仍可能已損毀，因此資料可能需要還原 toobe。  在這種情況下，它可能無法足夠 toorestore hello 最新備份，因為 hello 最新備份也可能已損毀。  因此，您必須 toofind hello 最後一次備份之前 hello 資料損毀。

如果您不確定哪一個備份已損毀，您無法部署新的 Service Fabric 叢集，並還原受影響的資料分割，如同上述 「 刪除或遺失的服務 」 的 hello hello 備份案例。  對於每個資料分割，開始使用至少從 hello 最近 toohello 還原 hello 備份。 一旦您找到並沒有 hello 損毀的備份，移動/delete 的這個資料分割是較新 （比該備份） 的所有備份。 針對每個資料分割重複此程序。 現在，當`OnDataLossAsync`稱為 hello 生產叢集中的 hello 磁碟分割，hello 最後一個備份位於 hello 外部存放區才能 hello 上述程序的其中一個選取的 hello。

Hello hello 「 已刪除或遺失的服務 」 中的步驟，可以是區段 hello 下列程式碼已損毀 hello 狀態之前，請使用 hello 服務 toohello 狀態 toorestore hello 狀態。

請注意：

  - 還原時，有機會讓的 hello 備份正在還原比 hello hello 磁碟分割狀態之前 hello 資料已遺失。 因為這個緣故，您應該還原只能作為最後的手段 toorecover 最多資料越好。
  - hello 代表 hello 備份資料夾路徑的字串和 hello hello 備份資料夾內檔案的路徑可能會大於 255 個字元，取決於 hello FabricDataRoot 路徑和應用程式類型名稱的長度。 這會造成某些.NET 方法，例如`Directory.Move`，toothrow hello`PathTooLongException`例外狀況。 解決方法之一是 toodirectly 呼叫 kernel32 Api，像是`CopyFile`。

## <a name="backup-and-restore-reliable-actors"></a>備份與還原 Reliable Actors


Reliable Actors 架構以 Reliable Services 為基礎。 hello ActorService 裝載 hello actor(s) 是可設定狀態的可靠服務。 因此，所有 hello 備份和還原功能可在可靠的服務也是可用 tooReliable 執行者 （除非是狀態服務提供者特定的行為）。 因為是依個別分割區進行備份，將會備份該分割區中所有動作項目的狀態 (還原也一樣依個別分割區進行)。 tooperform 備份/還原、 hello 服務擁有者應該建立自訂動作項目服務類別衍生自 ActorService 類別並再執行備份/還原類似 tooReliable 上面所述在上一節中的服務。

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

當您建立自訂動作項目服務類別時，您需要 tooregister，以及註冊 hello 動作項目時。

```csharp
ActorRuntime.RegisterActorAsync<MyActor>(
   (context, typeInfo) => new MyCustomActorService(context, typeInfo)).GetAwaiter().GetResult();
```

hello Reliable Actors 的預設狀態提供者是`KvsActorStateProvider`。 `KvsActorStateProvider` 依預設不啟用增量備份。 您可以藉由建立啟用增量備份`KvsActorStateProvider`hello 與適當的設定在其建構函式，然後再將它傳遞 tooActorService 建構函式在下列程式碼片段所示：

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

在啟用增量備份之後，進行增量備份可能會失敗並 FabricMissingFullBackupException 下列原因之一，而且您必須在執行增量備份之前 tootake 完整備份：

  - 因為它會變成主要 hello 複本已經從未使用過的完整備份。
  - 所以最後一個備份，已截斷 hello 記錄檔記錄的某些項目。

啟用增量備份時，`KvsActorStateProvider`不會使用循環緩衝區 toomanage 其記錄檔記錄，並定期會截斷。 如果沒有備份是使用者一段 45 分鐘內，hello 系統會自動截斷 hello 記錄檔記錄。 此間隔可以設定藉由指定`logTrunctationIntervalInMinutes`中`KvsActorStateProvider`建構函式 (類似 toowhen 啟用累加備份)。 如果主要複本需要 toobuild 另一個複本傳送所有資料，也可能會取得截斷 hello 記錄。

當執行還原備份鏈結，類似 tooReliable 服務，從 hello BackupFolderPath 應該包含具有一個包含完整備份和其他項目包含增量備份的子目錄的子目錄的子目錄。 hello 還原 API 將會擲回 FabricException 適當錯誤訊息 hello 備份鏈結驗證失敗時。 

> [!NOTE]
> `KvsActorStateProvider`目前會忽略 hello 選項 RestorePolicy.Safe。 即將推出的版本已規劃支援這項功能。
> 

## <a name="testing-backup-and-restore"></a>測試備份和還原
重要 tooensure 重要資料會進行備份，並可從還原它。 這可藉由叫用 hello`Start-ServiceFabricPartitionDataLoss`中可能會促使中特定資料分割 tootest 資料遺失，是否 hello 資料備份和還原功能，針對您的服務是否正常運作的 PowerShell cmdlet。  它也是可能 tooprogrammatically 叫用資料遺失，並從該事件，以及還原。

> [!NOTE]
> 您可以尋找範例的實作備份和還原 hello GitHub 上的 Web 參考應用程式中的功能。 請查看 hello`Inventory.Service`服務以取得更多詳細資料。
> 
> 

## <a name="under-hello-hood-more-details-on-backup-and-restore"></a>Hello 幕後： 對備份和還原的更多詳細資料
以下是備份與還原的詳細資料。

### <a name="backup"></a>備份
hello 可靠狀態管理員提供 hello 能力 toocreate 一致的備份而不會封鎖任何讀取或寫入作業。 toodo 因此，它會運用檢查點和記錄檔的持續性機制。  hello 可靠狀態管理員會在 hello 交易記錄檔中特定點 toorelieve 壓力模糊 （輕量型） 的檢查點，並改善復原時間。  當`BackupAsync`呼叫時，hello 可靠狀態管理員會指示所有可靠物件 toocopy 其最新檢查點檔案 tooa 本機備份資料夾。  然後，hello 可靠狀態管理員會複製所有的記錄檔記錄，到 hello 備份資料夾從 hello 「 啟動指標 」 toohello 最新記錄檔記錄。  由於 hello 備份中包含所有 hello 記錄檔記錄總 toohello 最新的記錄檔記錄，而且 hello 可靠狀態管理員會保留預先寫入記錄，可保證 hello 可靠狀態管理員的所有交易，都都會認可 (`CommitAsync`已傳回已成功） 會包含在 hello 備份。

認可之後的任何交易`BackupAsync`已呼叫可能或可能不在 hello 備份。  一旦 hello 本機備份資料夾已經填入 hello 平台 （亦即，本機備份完成時由 hello 執行階段），會叫用 hello 服務備份回呼。  此回呼會負責移動例如 Azure 儲存體的 hello 備份資料夾 tooan 外部位置。

### <a name="restore"></a>還原
hello 可靠狀態管理員提供從備份使用 hello hello 能力 toorestore`RestoreAsync`應用程式開發介面。  
hello`RestoreAsync`方法`RestoreContext`可以只在 hello 呼叫`OnDataLossAsync`方法。
hello 傳回 bool`OnDataLossAsync`指出 hello 服務是否已還原其狀態從外部來源。
如果 hello`OnDataLossAsync`傳回 true，表示服務的網狀架構將會重建所有其他的主要複本。 Service Fabric 可確保複本將會接收`OnDataLossAsync`呼叫第一個轉換 toohello 主要角色，但不會被授與讀取狀態或寫入狀態。
這暗示對於 StatefulService 實施者而言，將不會呼叫 `RunAsync`，直到 `OnDataLossAsync` 成功完成為止。
然後， `OnDataLossAsync` hello 新主要複本上將會叫用。
服務已成功 （藉由傳回 true 或 false） 完成此應用程式開發介面，然後再完成 hello 相關重新設定，hello API 會保持呼叫一次。

`RestoreAsync`先卸除 hello 呼叫它的主要複本中所有現有的狀態。  
然後 hello 可靠狀態管理員會建立所有 hello 可靠物件存在於 hello 備份資料夾中。  
接下來，hello 可靠物件會指示 toorestore 從其 hello 備份資料夾中的檢查點。  
最後，hello 可靠狀態管理員復原自己的狀態從 hello hello 備份資料夾中的記錄檔記錄，並執行復原。  
Hello 復原程序的一部分，從 hello 起始點 」 開始 hello 備份資料夾中已認可的記錄檔記錄的作業是在重新執行的 toohello 可靠的物件。  
這個步驟可確保該 hello 復原的狀態不一致。

## <a name="next-steps"></a>後續步驟
  - [可靠的集合](service-fabric-work-with-reliable-collections.md)
  - [Reliable Services 快速入門](service-fabric-reliable-services-quick-start.md)
  - [Reliable Services 通知](service-fabric-reliable-services-notifications.md)
  - [Reliable Services 組態](service-fabric-reliable-services-configuration.md)
  - [可靠的集合的開發人員參考資料](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

