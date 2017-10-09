---
title: "在 Azure 儲存體 blob 的唯讀快照集 aaaCreate |Microsoft 文件"
description: "深入了解如何 toocreate blob tooback 在給定的時間內的 blob 資料的快照集。 了解快照集的計費方式以及 toouse 它們 toominimize 容量費用。"
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 3710705d-e127-4b01-8d0f-29853fb06d0d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/11/2017
ms.author: marsma
ms.openlocfilehash: 9e7af611e885d83df69d3329217f261b3f3f333e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-blob-snapshot"></a>建立 Blob 快照集

快照集是在某個點時間取得的唯讀 Blob 版本。 快照集對於備份 Blob 非常有用。 建立快照集後，您便可加以讀取、複製或刪除，但無法加以修改。

Blob 的快照集是相同 tooits 基底 blob，除非該 hello blob URI 已**DateTime**值附加 toohello blob URI tooindicate hello 時間在哪一個 hello 拍攝快照。 例如，如果分頁 blob URI 是`http://storagesample.core.blob.windows.net/mydrives/myvhd`，也很類似 hello 快照集 URI`http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`。

> [!NOTE]
> 所有快照集共用 hello 基底 blob 的 URI。 hello 只有 hello 基底 blob 與 hello 快照之間的差異為附加的 hello **DateTime**值。
>

Blob 可包含任意數目的快照集。 系統會保存快照集，直到您將它們明確刪除為止。 快照集必須有其基底 Blob 才能存在。 您可以列舉與 hello 基底 blob tootrack 相關聯的 hello 快照目前的快照集。

當您建立 blob 的快照集時，hello blob 的系統屬性會以 hello 複製的 toohello 快照集相同的值。 hello 基底 blob 的中繼資料也是快照集，請複製的 toohello，除非您指定不同的中繼資料的快照集時建立它的 hello。

任何與 hello 基底 blob 相關聯的租用不會影響 hello 快照集。 您無法取得快照集上的租用。

VHD 檔案是使用的 toostore hello 目前資訊和 VM 磁碟的狀態。 您可以從中斷連接磁碟 hello VM 內或關閉 hello VM，然後再採取其 VHD 檔案的快照集。 您可以使用該快照集檔案稍後 tooretrieve hello VHD 檔案中該時間點的時間，並重新建立 hello VM。

如果 hello 儲存體帳戶已啟用儲存體服務加密 (SSE) 中的 hello blob 所在，則採取該 blob 的任何快照集將會加密在靜止。

## <a name="create-a-snapshot"></a>建立快照集
hello 下列程式碼範例示範如何使用快照集 toocreate hello[適用於.NET 的 Azure 儲存體用戶端程式庫](https://www.nuget.org/packages/WindowsAzure.Storage/)。 在建立時，這個範例會指定 hello 快照集的其他中繼資料。

```csharp
private static async Task CreateBlockBlobSnapshot(CloudBlobContainer container)
{
    // Create a new block blob in hello container.
    CloudBlockBlob baseBlob = container.GetBlockBlobReference("sample-base-blob.txt");

    // Add blob metadata.
    baseBlob.Metadata.Add("ApproxBlobCreatedDate", DateTime.UtcNow.ToString());

    try
    {
        // Upload hello blob toocreate it, with its metadata.
        await baseBlob.UploadTextAsync(string.Format("Base blob: {0}", baseBlob.Uri.ToString()));

        // Sleep 5 seconds.
        System.Threading.Thread.Sleep(5000);

        // Create a snapshot of hello base blob.
        // Specify metadata at hello time that hello snapshot is created toospecify unique metadata for hello snapshot.
        // If no metadata is specified when hello snapshot is created, hello base blob's metadata is copied toohello snapshot.
        Dictionary<string, string> metadata = new Dictionary<string, string>();
        metadata.Add("ApproxSnapshotCreatedDate", DateTime.UtcNow.ToString());
        await baseBlob.CreateSnapshotAsync(metadata, null, null, null);
    }
    catch (StorageException e)
    {
        Console.WriteLine(e.Message);
        Console.ReadLine();
        throw;
    }
}
```

## <a name="copy-snapshots"></a>複製快照集
涉及 Blob 和快照集的複製作業會遵循下列規則：

* 您可以將快照集複製到其基底 Blob 之上。 透過升級 hello 基底 blob 的快照集 toohello 位置，您可以還原舊版的 blob。 hello 快照集會保留，但會覆寫基底 blob 的 hello hello 快照集的可寫入副本。
* 您可以複製快照集 tooa 目的地 blob，使用不同的名稱。 可寫入的 blob，而不是快照集 hello 產生的目的地 blob。
* 當複製來源 blob 時，任何 hello 來源 blob 的快照集不會複製的 toohello 目的地。 當複本覆寫目的地 blob 時，任何與 hello 原始目的地 blob 相關聯的快照集維持不變。
* 當您建立區塊 blob 的快照集時，hello blob 之認可的區塊清單會同時複製的 toohello 快照集。 系統不會複製任何未認可的區塊。

## <a name="specify-an-access-condition"></a>指定存取條件
當您呼叫[CreateSnapshotAsync][dotnet_CreateSnapshotAsync]，您可以指定存取條件，使得 hello 快照集才會建立符合條件。 toospecify 存取條件，使用 hello [AccessCondition] [ dotnet_AccessCondition]參數。 如果不符合條件、 沒有建立 hello 快照集，和 hello Blob 服務會傳回狀態碼，指定 hello [HTTPStatusCode][dotnet_HTTPStatusCode]。PreconditionFailed。

## <a name="delete-snapshots"></a>刪除快照集
您無法刪除具有快照集的 blob，除非 hello 快照集也會一併刪除。 您可以個別刪除快照集或指定刪除 hello 來源 blob 時，會刪除所有快照集。 如果您嘗試 toodelete 仍具有快照集的 blob 時，會發生錯誤。

hello 下列程式碼範例顯示如何 toodelete blob 和在.NET 中，其快照集位置`blockBlob`是類型的物件[CloudBlockBlob][dotnet_CloudBlockBlob]:

```csharp
await blockBlob.DeleteIfExistsAsync(DeleteSnapshotsOption.IncludeSnapshots, null, null, null);
```

## <a name="snapshots-with-azure-premium-storage"></a>快照集與 Azure 進階儲存體
當使用進階儲存體中的快照集，套用下列規則的 hello:

* hello 的每個 premium 儲存體帳戶中的分頁 blob 的快照集數目上限為 100。 如果超出該限制，hello 快照集 Blob 作業會傳回錯誤碼 409 (`SnapshotCountExceeded`)。
* 您可以每 10 分鐘擷取一次進階儲存體帳戶中分頁 Blob 的快照集。 如果超出該比率，hello 快照集 Blob 作業會傳回錯誤碼 409 (`SnapshotOperationRateExceeded`)。
* tooread 快照集，您可以使用 hello 複製 Blob 作業 toocopy 快照 tooanother 分頁 blob hello 帳戶中。 hello hello 複製作業的目的地 blob 必須沒有任何現有的快照集。 如果 hello 目的地 blob 具有快照集，則 hello 複製 Blob 作業會傳回錯誤碼 409 (`SnapshotsPresent`)。

## <a name="return-hello-absolute-uri-tooa-snapshot"></a>傳回 hello 絕對 URI tooa 快照集
這個 C# 程式碼範例會建立快照集，並寫出 hello hello 主要位置的絕對 URI。

```csharp
//Create hello blob service client object.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";

CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();

//Get a reference tooa blob.
CloudBlockBlob blob = container.GetBlockBlobReference("sampleblob.txt");
blob.UploadText("This is a blob.");

//Create a snapshot of hello blob and write out its primary URI.
CloudBlockBlob blobSnapshot = blob.CreateSnapshot();
Console.WriteLine(blobSnapshot.SnapshotQualifiedStorageUri.PrimaryUri);
```

## <a name="understand-how-snapshots-accrue-charges"></a>了解快照集產生費用的方式
建立快照集，這是 blob 的唯讀複本，可能會導致其他資料儲存體費用 tooyour 帳戶。 在設計您的應用程式時，很重要 toobe 知道如何這些可能會產生費用，讓成本降至最低。

### <a name="important-billing-considerations"></a>重要的計費考量
下列清單中的 hello 包括重點 tooconsider 時建立快照集。

* 無論是在 hello blob 或 hello 快照中，儲存體帳戶就會產生唯一的區塊或頁面的費用。 您的帳戶不會造成額外的費用，除非您更新為基礎的 hello blob 與 blob 相關聯的快照集。 更新 hello 基底 blob 之後，它會偏離其快照集。 當發生這種情況時，您必須支付 hello 唯一區塊或頁面中的每個 blob 或快照集。
* 當您取代區塊 Blob 內的某個區塊時，後續即會將該區塊視為唯一區塊進行收費。 這是 true，即使 hello 區塊都具有相同的區塊識別碼和 hello 相同的 hello 資料，因為它有 hello 快照集。 Hello 區塊認可後同樣地，其值與值的任何快照集的對應項目，您將支付其資料。 hello 同樣適用於網頁中使用相同的資料會更新分頁 blob。
* 取代區塊 blob 呼叫 hello [UploadFromFile][dotnet_UploadFromFile]， [UploadText][dotnet_UploadText]， [UploadFromStream] [ dotnet_UploadFromStream]，或[UploadFromByteArray] [ dotnet_UploadFromByteArray]方法會取代 hello blob 中的所有區塊。 如果您有與該 blob 相關聯的快照集，在 hello 基底 blob 和快照集的所有區塊現在都分離，，您將支付這兩個 blob 中的所有 hello 區塊。 即使 hello 基底 blob 和 hello 快照中的 hello 資料都會保持一致，也是如此。
* hello Azure Blob 服務沒有表示 toodetermine 是否兩個區塊包含相同的資料。 上傳且認可的每個區塊仍會視為唯一，即使它已在相同的資料和 hello hello 相同區塊識別碼。 產生唯一的區塊的費用，因為它是重要 tooconsider 更新 blob 具有快照集產生額外的唯一區塊及額外費用。

### <a name="minimize-cost-with-snapshot-management"></a>透過管理快照集將成本降到最低

我們建議您小心管理您的快照集 tooavoid 額外費用。 您可以依照 toohelp 降至最低 hello 成本 hello 儲存體，您的快照集的這些最佳作法：

* 刪除並重新建立與 blob 相關聯每當您更新 hello blob，即使您正在使用相同的資料，除非您的應用程式設計為需要維護快照集的快照集。 藉由刪除並重新建立 hello blob 的快照集，您可以確保，hello blob 和快照集不會分流。
* 如果您要維護 blob 的快照集，避免呼叫[UploadFromFile][dotnet_UploadFromFile]， [UploadText][dotnet_UploadText]， [UploadFromStream][dotnet_UploadFromStream]，或[UploadFromByteArray] [ dotnet_UploadFromByteArray] tooupdate hello blob。 這些方法會取代所有 hello blob，導致您的基底 blob 和其快照集 toodiverge 大幅中的 hello 區塊。 相反地，更新 hello 最少的可能值的區塊使用 hello [PutBlock] [ dotnet_PutBlock]和[PutBlockList] [ dotnet_PutBlockList]方法。

### <a name="snapshot-billing-scenarios"></a>快照集計費案例
hello 下列案例示範區塊 blob 和其快照集如何產生費用。

**案例 1**

在案例 1 中，hello 基底 blob 不後已更新 hello 快照，如此會僅針對唯一區塊 1、 2 和 3 產生費用。

![Azure 儲存體資源](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-1.png)

**案例 2**

在案例 2 中，hello 基底 blob 已更新，但 hello 快照中不包含。 區塊 3 已更新，而且即使它包含 hello 相同的資料及 hello 相同的識別碼，就不 hello 與 hello 快照集中的區塊 3 相同。 如此一來，hello 帳戶支付四個區塊。

![Azure 儲存體資源](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-2.png)

**案例 3**

案例 3，hello 基底 blob 已更新，但 hello 快照中不包含。 區塊 3 已取代為區塊 4 hello 基底 blob，但 hello 快照集仍反映區塊 3。 如此一來，hello 帳戶支付四個區塊。

![Azure 儲存體資源](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-3.png)

**案例 4**

在案例 4 中，hello 基底 blob 已更新完成，未包含任何原始區塊。 如此一來，所有的八個唯一區塊的計費 hello 帳戶。 如果您使用 update 方法，例如，可能會發生這個狀況[UploadFromFile][dotnet_UploadFromFile]， [UploadText][dotnet_UploadText]， [UploadFromStream][dotnet_UploadFromStream]，或[UploadFromByteArray][dotnet_UploadFromByteArray]，因為這些方法會取代所有 hello blob 的內容。

![Azure 儲存體資源](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-4.png)

## <a name="next-steps"></a>後續步驟

* 您可以在[使用增量快照備份 Azure 非受控磁碟](storage-incremental-snapshots.md)中，找到使用虛擬機器 (VM) 磁碟快照集的詳細資訊

* 如需使用 Blob 儲存體的其他程式碼範例，請參閱 [Azure 程式碼範例](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob)。 您可以下載範例應用程式和執行它，或瀏覽 hello GitHub 上的程式碼。

[dotnet_AccessCondition]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.accesscondition.aspx
[dotnet_CloudBlockBlob]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.aspx
[dotnet_CreateSnapshotAsync]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.createsnapshotasync.aspx
[dotnet_HTTPStatusCode]: https://msdn.microsoft.com/library/system.net.httpstatuscode(v=vs.110).aspx
[dotnet_PutBlockList]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.putblocklist.aspx
[dotnet_PutBlock]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.putblock.aspx
[dotnet_UploadFromByteArray]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadfrombytearray.aspx
[dotnet_UploadFromFile]: https://msdn.microsoft.com/library/azure/mt705654.aspx
[dotnet_UploadFromStream]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadfromstream.aspx
[dotnet_UploadText]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadtext.aspx