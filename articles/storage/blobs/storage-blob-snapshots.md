---
title: "在 Azure 儲存體中建立 Blob 的唯讀快照集 | Microsoft Docs"
description: "了解如何建立 Blob 的快照集以便在給定的時間點備份 Blob 資料。 了解快照集計費的方式，以及如何使用它們將容量費用降至最低。"
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
ms.openlocfilehash: b1d87cd66457b08bba594bfc7de1e9e4e2dff1e6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-blob-snapshot"></a><span data-ttu-id="d6a7a-104">建立 Blob 快照集</span><span class="sxs-lookup"><span data-stu-id="d6a7a-104">Create a blob snapshot</span></span>

<span data-ttu-id="d6a7a-105">快照集是在某個點時間取得的唯讀 Blob 版本。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-105">A snapshot is a read-only version of a blob that's taken at a point in time.</span></span> <span data-ttu-id="d6a7a-106">快照集對於備份 Blob 非常有用。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-106">Snapshots are useful for backing up blobs.</span></span> <span data-ttu-id="d6a7a-107">建立快照集後，您便可加以讀取、複製或刪除，但無法加以修改。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-107">After you create a snapshot, you can read, copy, or delete it, but you cannot modify it.</span></span>

<span data-ttu-id="d6a7a-108">Blob 的快照集與其基底 Blob 相同，除了 Blob URI 附加了 [日期時間]  值以表示擷取快照當時的時間。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-108">A snapshot of a blob is identical to its base blob, except that the blob URI has a **DateTime** value appended to the blob URI to indicate the time at which the snapshot was taken.</span></span> <span data-ttu-id="d6a7a-109">例如，如果分頁 Blob URI 為 `http://storagesample.core.blob.windows.net/mydrives/myvhd`，則快照集 URI 類似於 `http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-109">For example, if a page blob URI is `http://storagesample.core.blob.windows.net/mydrives/myvhd`, the snapshot URI is similar to `http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`.</span></span>

> [!NOTE]
> <span data-ttu-id="d6a7a-110">所有快照集會共用基底 blob 的 URI。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-110">All snapshots share the base blob's URI.</span></span> <span data-ttu-id="d6a7a-111">基底 blob 與快照集之間的唯一差別在於附加的 **DateTime** 值。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-111">The only distinction between the base blob and the snapshot is the appended **DateTime** value.</span></span>
>

<span data-ttu-id="d6a7a-112">Blob 可包含任意數目的快照集。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-112">A blob can have any number of snapshots.</span></span> <span data-ttu-id="d6a7a-113">系統會保存快照集，直到您將它們明確刪除為止。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-113">Snapshots persist until they are explicitly deleted.</span></span> <span data-ttu-id="d6a7a-114">快照集必須有其基底 Blob 才能存在。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-114">A snapshot cannot outlive its base blob.</span></span> <span data-ttu-id="d6a7a-115">您可以列舉與基底 Blob 相關聯的快照集，以追蹤目前的快照集。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-115">You can enumerate the snapshots associated with the base blob to track your current snapshots.</span></span>

<span data-ttu-id="d6a7a-116">當您建立 Blob 的快照集時，Blob 的系統屬性都會使用相同值複製到快照集中。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-116">When you create a snapshot of a blob, the blob's system properties are copied to the snapshot with the same values.</span></span> <span data-ttu-id="d6a7a-117">基底 blob 的中繼資料也會複製到快照集，除非您在建立快照集時為其指定個別的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-117">The base blob's metadata is also copied to the snapshot, unless you specify separate metadata for the snapshot when you create it.</span></span>

<span data-ttu-id="d6a7a-118">任何與基底 Blob 相關聯的租用不會影響快照集。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-118">Any leases associated with the base blob do not affect the snapshot.</span></span> <span data-ttu-id="d6a7a-119">您無法取得快照集上的租用。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-119">You cannot acquire a lease on a snapshot.</span></span>

<span data-ttu-id="d6a7a-120">VHD 檔案是用來儲存 VM 磁碟目前的資訊和狀態。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-120">A VHD file is used to store the current information and status for a VM disk.</span></span> <span data-ttu-id="d6a7a-121">您可以從 VM 內卸離磁碟或關閉 VM，然後製作其 VHD 檔案的快照集。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-121">You can detach a disk from within the VM or shut down the VM, and then take a snapshot of its VHD file.</span></span> <span data-ttu-id="d6a7a-122">稍後您可以使用快照集檔案來擷取該時間點的 VHD 檔案，並重新建立 VM。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-122">You can use that snapshot file later to retrieve the VHD file at that point in time and recreate the VM.</span></span>

<span data-ttu-id="d6a7a-123">如果 blob 所在的儲存體帳戶啟用儲存體服務加密 (SSE) 時，任何該 blob 製作的快照集將會在待用時加密。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-123">If Storage Service Encryption (SSE) is enabled for the storage account in which the blob resides, then any snapshots taken of that blob will be encrypted at rest.</span></span>

## <a name="create-a-snapshot"></a><span data-ttu-id="d6a7a-124">建立快照集</span><span class="sxs-lookup"><span data-stu-id="d6a7a-124">Create a snapshot</span></span>
<span data-ttu-id="d6a7a-125">下列程式碼範例會示範如何使用 [Azure Storage Client Library for.NET](https://www.nuget.org/packages/WindowsAzure.Storage/) 建立快照集。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-125">The following code example shows how to create a snapshot by using the [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span> <span data-ttu-id="d6a7a-126">此範例會在建立快照集時為其指定其他中繼資料。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-126">This example specifies additional metadata for the snapshot when it is created.</span></span>

```csharp
private static async Task CreateBlockBlobSnapshot(CloudBlobContainer container)
{
    // Create a new block blob in the container.
    CloudBlockBlob baseBlob = container.GetBlockBlobReference("sample-base-blob.txt");

    // Add blob metadata.
    baseBlob.Metadata.Add("ApproxBlobCreatedDate", DateTime.UtcNow.ToString());

    try
    {
        // Upload the blob to create it, with its metadata.
        await baseBlob.UploadTextAsync(string.Format("Base blob: {0}", baseBlob.Uri.ToString()));

        // Sleep 5 seconds.
        System.Threading.Thread.Sleep(5000);

        // Create a snapshot of the base blob.
        // Specify metadata at the time that the snapshot is created to specify unique metadata for the snapshot.
        // If no metadata is specified when the snapshot is created, the base blob's metadata is copied to the snapshot.
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

## <a name="copy-snapshots"></a><span data-ttu-id="d6a7a-127">複製快照集</span><span class="sxs-lookup"><span data-stu-id="d6a7a-127">Copy snapshots</span></span>
<span data-ttu-id="d6a7a-128">涉及 Blob 和快照集的複製作業會遵循下列規則：</span><span class="sxs-lookup"><span data-stu-id="d6a7a-128">Copy operations involving blobs and snapshots follow these rules:</span></span>

* <span data-ttu-id="d6a7a-129">您可以將快照集複製到其基底 Blob 之上。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-129">You can copy a snapshot over its base blob.</span></span> <span data-ttu-id="d6a7a-130">藉由將快照集升級到基底 Blob 的位置，您可以還原舊版的 Blob。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-130">By promoting a snapshot to the position of the base blob, you can restore an earlier version of a blob.</span></span> <span data-ttu-id="d6a7a-131">快照集會被保留，但基底 Blob 會遭到快照集的可寫入複本覆寫。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-131">The snapshot remains, but the base blob is overwritten with a writable copy of the snapshot.</span></span>
* <span data-ttu-id="d6a7a-132">您可以將快照集複製到不同名稱的目的地 Blob。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-132">You can copy a snapshot to a destination blob with a different name.</span></span> <span data-ttu-id="d6a7a-133">所產生的目的地 Blob 會是一個可寫入的 Blob，而不是快照集。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-133">The resulting destination blob is a writable blob and not a snapshot.</span></span>
* <span data-ttu-id="d6a7a-134">複製來源 Blob 時，不會將來源 Blob 的任何快照集複製到目的地。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-134">When a source blob is copied, any snapshots of the source blob are not copied to the destination.</span></span> <span data-ttu-id="d6a7a-135">使用某個複本覆寫目的地 Blob 時，與原始目的地 Blob 相關聯的所有快照集都會保持不變。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-135">When a destination blob is overwritten with a copy, any snapshots associated with the original destination blob remain intact.</span></span>
* <span data-ttu-id="d6a7a-136">當您建立區塊 Blob 的快照集時，該 Blob 的認可區塊清單也會複製到快照集。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-136">When you create a snapshot of a block blob, the blob's committed block list is also copied to the snapshot.</span></span> <span data-ttu-id="d6a7a-137">系統不會複製任何未認可的區塊。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-137">Any uncommitted blocks are not copied.</span></span>

## <a name="specify-an-access-condition"></a><span data-ttu-id="d6a7a-138">指定存取條件</span><span class="sxs-lookup"><span data-stu-id="d6a7a-138">Specify an access condition</span></span>
<span data-ttu-id="d6a7a-139">當您呼叫 [CreateSnapshotAsync][dotnet_CreateSnapshotAsync] 時，您可以指定存取條件，如此一來，只有在符合條件時，才會建立快照集。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-139">When you call [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], you can specify an access condition so that the snapshot is created only if a condition is met.</span></span> <span data-ttu-id="d6a7a-140">若要指定存取條件，請使用 [AccessCondition][dotnet_AccessCondition] 參數。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-140">To specify an access condition, use the [AccessCondition][dotnet_AccessCondition] parameter.</span></span> <span data-ttu-id="d6a7a-141">如果不符合指定的條件，就不會建立快照集，而且 Blob 服務會傳回狀態碼 [HTTPStatusCode][dotnet_HTTPStatusCode].PreconditionFailed。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-141">If the specified condition is not met, the snapshot is not created, and the Blob service returns status code [HTTPStatusCode][dotnet_HTTPStatusCode].PreconditionFailed.</span></span>

## <a name="delete-snapshots"></a><span data-ttu-id="d6a7a-142">刪除快照集</span><span class="sxs-lookup"><span data-stu-id="d6a7a-142">Delete snapshots</span></span>
<span data-ttu-id="d6a7a-143">除非快照集也一併刪除，否則您無法刪除具有快照集的 Blob。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-143">You can't delete a blob with snapshots unless the snapshots are also deleted.</span></span> <span data-ttu-id="d6a7a-144">您可以個別刪除快照集，或指定在刪除來源 Blob 時刪除所有的快照集。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-144">You can delete a snapshot individually, or specify that all snapshots be deleted when the source blob is deleted.</span></span> <span data-ttu-id="d6a7a-145">如果您嘗試刪除仍具有快照集的 Blob，則會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-145">If you attempt to delete a blob that still has snapshots, an error results.</span></span>

<span data-ttu-id="d6a7a-146">下列程式碼範例示範如何在 .NET 中刪除 blob 及其快照集，其中 `blockBlob` 是 [CloudBlockBlob][dotnet_CloudBlockBlob]類型的物件：</span><span class="sxs-lookup"><span data-stu-id="d6a7a-146">The following code example shows how to delete a blob and its snapshots in .NET, where `blockBlob` is an object of type [CloudBlockBlob][dotnet_CloudBlockBlob]:</span></span>

```csharp
await blockBlob.DeleteIfExistsAsync(DeleteSnapshotsOption.IncludeSnapshots, null, null, null);
```

## <a name="snapshots-with-azure-premium-storage"></a><span data-ttu-id="d6a7a-147">快照集與 Azure 進階儲存體</span><span class="sxs-lookup"><span data-stu-id="d6a7a-147">Snapshots with Azure Premium Storage</span></span>
<span data-ttu-id="d6a7a-148">搭配使用快照集與進階儲存體時適用下列規則：</span><span class="sxs-lookup"><span data-stu-id="d6a7a-148">When using snapshots with Premium Storage, the following rules apply:</span></span>

* <span data-ttu-id="d6a7a-149">進階儲存體帳戶中每個分頁 Blob 的快照集數目上限為 100 個。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-149">The maximum number of snapshots per page blob in a premium storage account is 100.</span></span> <span data-ttu-id="d6a7a-150">如果超出該限制，快照集 Blob 作業就會傳回錯誤碼 409 (`SnapshotCountExceeded`)。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-150">If that limit is exceeded, the Snapshot Blob operation returns error code 409 (`SnapshotCountExceeded`).</span></span>
* <span data-ttu-id="d6a7a-151">您可以每 10 分鐘擷取一次進階儲存體帳戶中分頁 Blob 的快照集。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-151">You can take a snapshot of a page blob in a premium storage account once every 10 minutes.</span></span> <span data-ttu-id="d6a7a-152">如果超出該比率，快照集 Blob 作業就會傳回錯誤碼 409 (`SnapshotOperationRateExceeded`)。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-152">If that rate is exceeded, the Snapshot Blob operation returns error code 409 (`SnapshotOperationRateExceeded`).</span></span>
* <span data-ttu-id="d6a7a-153">若要讀取快照集，您可以使用複製 Blob 作業，將快照集複製到帳戶中的其他分頁 Blob。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-153">To read a snapshot, you can use the Copy Blob operation to copy a snapshot to another page blob in the account.</span></span> <span data-ttu-id="d6a7a-154">複製作業的目的地 Blob 不可以包含任何現有的快照集。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-154">The destination blob for the copy operation must not have any existing snapshots.</span></span> <span data-ttu-id="d6a7a-155">如果目的地 Blob 具有快照集，則 Copy Blob 作業會傳回錯誤碼 409 (`SnapshotsPresent`).。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-155">If the destination blob does have snapshots, then the Copy Blob operation returns error code 409 (`SnapshotsPresent`).</span></span>

## <a name="return-the-absolute-uri-to-a-snapshot"></a><span data-ttu-id="d6a7a-156">傳回快照集的絕對 URI</span><span class="sxs-lookup"><span data-stu-id="d6a7a-156">Return the absolute URI to a snapshot</span></span>
<span data-ttu-id="d6a7a-157">這個 C# 程式碼範例會建立快照集，並寫出主要位置的絕對 URI。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-157">This C# code example creates a snapshot and writes out the absolute URI for the primary location.</span></span>

```csharp
//Create the blob service client object.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";

CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference to a container.
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();

//Get a reference to a blob.
CloudBlockBlob blob = container.GetBlockBlobReference("sampleblob.txt");
blob.UploadText("This is a blob.");

//Create a snapshot of the blob and write out its primary URI.
CloudBlockBlob blobSnapshot = blob.CreateSnapshot();
Console.WriteLine(blobSnapshot.SnapshotQualifiedStorageUri.PrimaryUri);
```

## <a name="understand-how-snapshots-accrue-charges"></a><span data-ttu-id="d6a7a-158">了解快照集產生費用的方式</span><span class="sxs-lookup"><span data-stu-id="d6a7a-158">Understand how snapshots accrue charges</span></span>
<span data-ttu-id="d6a7a-159">建立快照集 (即 Blob 的唯讀複本) 可能會為您的帳戶產生額外的資料儲存體費用。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-159">Creating a snapshot, which is a read-only copy of a blob, can result in additional data storage charges to your account.</span></span> <span data-ttu-id="d6a7a-160">設計您的應用程式時，請務必留意產生這些費用的可能方式，以便將成本降至最低。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-160">When designing your application, it is important to be aware of how these charges might accrue so that you can minimize costs.</span></span>

### <a name="important-billing-considerations"></a><span data-ttu-id="d6a7a-161">重要的計費考量</span><span class="sxs-lookup"><span data-stu-id="d6a7a-161">Important billing considerations</span></span>
<span data-ttu-id="d6a7a-162">下列清單包含建立快照集時要考量的重點。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-162">The following list includes key points to consider when creating a snapshot.</span></span>

* <span data-ttu-id="d6a7a-163">無論唯一的區塊或分頁是在 Blob 或快照集中，您的儲存體帳戶都會產生費用。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-163">Your storage account incurs charges for unique blocks or pages, whether they are in the blob or in the snapshot.</span></span> <span data-ttu-id="d6a7a-164">在您更新快照集所依據的 Blob 之前，您的帳戶不會針對與該 Blob 相關聯的快照集產生額外費用。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-164">Your account does not incur additional charges for snapshots associated with a blob until you update the blob on which they are based.</span></span> <span data-ttu-id="d6a7a-165">在您更新基底 blob 之後，它會與其快照集分離。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-165">After you update the base blob, it diverges from its snapshots.</span></span> <span data-ttu-id="d6a7a-166">發生這種情況時，您需支付每個 blob 或快照集中唯一的區塊或頁面。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-166">When this happens, you are charged for the unique blocks or pages in each blob or snapshot.</span></span>
* <span data-ttu-id="d6a7a-167">當您取代區塊 Blob 內的某個區塊時，後續即會將該區塊視為唯一區塊進行收費。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-167">When you replace a block within a block blob, that block is subsequently charged as a unique block.</span></span> <span data-ttu-id="d6a7a-168">即使該區塊的區塊識別碼和資料與其在快照集中擁有的相同，也是如此。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-168">This is true even if the block has the same block ID and the same data as it has in the snapshot.</span></span> <span data-ttu-id="d6a7a-169">再次認可該區塊之後，它就會與其在任何快照集中的對應項目分離，而您將需支付其資料的費用。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-169">After the block is committed again, it diverges from its counterpart in any snapshot, and you will be charged for its data.</span></span> <span data-ttu-id="d6a7a-170">這同樣適用分頁 Blob 中以相同資料更新的頁面。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-170">The same holds true for a page in a page blob that's updated with identical data.</span></span>
* <span data-ttu-id="d6a7a-171">藉由呼叫 [UploadFromFile][dotnet_UploadFromFile]、[UploadText][dotnet_UploadText]、[UploadFromStream][dotnet_UploadFromStream], 或 [UploadFromByteArray][dotnet_UploadFromByteArray] 方法來取代區塊 Blob，會取代該 Blob 中的所有區塊。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-171">Replacing a block blob by calling the [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray] method replaces all blocks in the blob.</span></span> <span data-ttu-id="d6a7a-172">如果您的快照集與該 Blob 相關聯，基底 Blob 和快照集中的所有區塊現在都會分離出來，而您將針對這兩個 Blob 的所有區塊支付費用。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-172">If you have a snapshot associated with that blob, all blocks in the base blob and snapshot now diverge, and you will be charged for all the blocks in both blobs.</span></span> <span data-ttu-id="d6a7a-173">即使基底 Blob 和快照集中的資料保持一致，也是如此。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-173">This is true even if the data in the base blob and the snapshot remain identical.</span></span>
* <span data-ttu-id="d6a7a-174">Azure Blob 服務未提供方法來判斷兩個區塊是否包含相同資料。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-174">The Azure Blob service does not have a means to determine whether two blocks contain identical data.</span></span> <span data-ttu-id="d6a7a-175">已上傳且認可的每個區塊都會被視為唯一，即使它具有相同資料和相同的區塊識別碼也一樣。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-175">Each block that is uploaded and committed is treated as unique, even if it has the same data and the same block ID.</span></span> <span data-ttu-id="d6a7a-176">由於費用是針對唯一區塊而產生，因此請務必注意，更新含有快照集的 Blob 會產生額外的唯一區塊及額外費用。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-176">Because charges accrue for unique blocks, it's important to consider that updating a blob that has a snapshot results in additional unique blocks and additional charges.</span></span>

### <a name="minimize-cost-with-snapshot-management"></a><span data-ttu-id="d6a7a-177">透過管理快照集將成本降到最低</span><span class="sxs-lookup"><span data-stu-id="d6a7a-177">Minimize cost with snapshot management</span></span>

<span data-ttu-id="d6a7a-178">我們建議您謹慎管理快照集，以避免產生額外費用。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-178">We recommend managing your snapshots carefully to avoid extra charges.</span></span> <span data-ttu-id="d6a7a-179">您可以遵循以下最佳做法，協助您將快照集儲存體產生的成本降到最低︰</span><span class="sxs-lookup"><span data-stu-id="d6a7a-179">You can follow these best practices to help minimize the costs incurred by the storage of your snapshots:</span></span>

* <span data-ttu-id="d6a7a-180">每當您更新 Blob 時，刪除並重新建立與該 Blob 相關聯的快照集，除非您的應用程式設計為需要維護快照集，否則即使您正以相同資料進行更新也一樣。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-180">Delete and re-create snapshots associated with a blob whenever you update the blob, even if you are updating with identical data, unless your application design requires that you maintain snapshots.</span></span> <span data-ttu-id="d6a7a-181">藉由刪除並重新建立 Blob 的快照集，讓您可以確保該 Blob 和快照集不會分離開來。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-181">By deleting and re-creating the blob's snapshots, you can ensure that the blob and snapshots do not diverge.</span></span>
* <span data-ttu-id="d6a7a-182">如果您正在維護 Blob 的快照集，請避免呼叫 [UploadFromFile][dotnet_UploadFromFile]、[UploadText][dotnet_UploadText]、[UploadFromStream][dotnet_UploadFromStream], 或 [UploadFromByteArray][dotnet_UploadFromByteArray]來更新 Blob。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-182">If you are maintaining snapshots for a blob, avoid calling [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray] to update the blob.</span></span> <span data-ttu-id="d6a7a-183">這些方法會取代 Blob 中的所有區塊，造成您的基底 Blob 和其快照集明顯分離。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-183">These methods replace all of the blocks in the blob, causing your base blob and its snapshots to diverge significantly.</span></span> <span data-ttu-id="d6a7a-184">請改用 [PutBlock][dotnet_PutBlock] 和 [PutBlockList][dotnet_PutBlockList] 方法，更新區塊的最少可能數目。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-184">Instead, update the fewest possible number of blocks by using the [PutBlock][dotnet_PutBlock] and [PutBlockList][dotnet_PutBlockList] methods.</span></span>

### <a name="snapshot-billing-scenarios"></a><span data-ttu-id="d6a7a-185">快照集計費案例</span><span class="sxs-lookup"><span data-stu-id="d6a7a-185">Snapshot billing scenarios</span></span>
<span data-ttu-id="d6a7a-186">下列案例示範如何針對區塊 Blob 及其快照集產生費用。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-186">The following scenarios demonstrate how charges accrue for a block blob and its snapshots.</span></span>

<span data-ttu-id="d6a7a-187">**案例 1**</span><span class="sxs-lookup"><span data-stu-id="d6a7a-187">**Scenario 1**</span></span>

<span data-ttu-id="d6a7a-188">在案例 1 中，基底 Blob 在擷取快照之後尚未更新，因此只會針對唯一區塊 1、2 和 3 產生費用。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-188">In scenario 1, the base blob has not been updated after the snapshot was taken, so charges are incurred only for unique blocks 1, 2, and 3.</span></span>

![Azure 儲存體資源](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-1.png)

<span data-ttu-id="d6a7a-190">**案例 2**</span><span class="sxs-lookup"><span data-stu-id="d6a7a-190">**Scenario 2**</span></span>

<span data-ttu-id="d6a7a-191">在案例 2 中，基底 Blob 已更新，但快照集並未更新。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-191">In scenario 2, the base blob has been updated, but the snapshot has not.</span></span> <span data-ttu-id="d6a7a-192">區塊 3 已更新，而且即使它包含相同資料及相同的識別碼，它還是與快照集中的區塊 3 不一樣。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-192">Block 3 was updated, and even though it contains the same data and the same ID, it is not the same as block 3 in the snapshot.</span></span> <span data-ttu-id="d6a7a-193">因此，此帳戶必須支付四個區塊的費用。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-193">As a result, the account is charged for four blocks.</span></span>

![Azure 儲存體資源](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-2.png)

<span data-ttu-id="d6a7a-195">**案例 3**</span><span class="sxs-lookup"><span data-stu-id="d6a7a-195">**Scenario 3**</span></span>

<span data-ttu-id="d6a7a-196">在案例 3 中，基底 Blob 已更新，但快照集並未更新。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-196">In scenario 3, the base blob has been updated, but the snapshot has not.</span></span> <span data-ttu-id="d6a7a-197">區塊 3 已使用基底 Blob 中的區塊 4 來取代，但快照集仍然反映區塊 3。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-197">Block 3 was replaced with block 4 in the base blob, but the snapshot still reflects block 3.</span></span> <span data-ttu-id="d6a7a-198">因此，此帳戶必須支付四個區塊的費用。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-198">As a result, the account is charged for four blocks.</span></span>

![Azure 儲存體資源](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-3.png)

<span data-ttu-id="d6a7a-200">**案例 4**</span><span class="sxs-lookup"><span data-stu-id="d6a7a-200">**Scenario 4**</span></span>

<span data-ttu-id="d6a7a-201">在案例 4 中，基底 Blob 已完全更新，且未包含它的任何原始區塊。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-201">In scenario 4, the base blob has been completely updated and contains none of its original blocks.</span></span> <span data-ttu-id="d6a7a-202">因此，此帳戶必須支付所有八個唯一區塊的費用。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-202">As a result, the account is charged for all eight unique blocks.</span></span> <span data-ttu-id="d6a7a-203">如果您使用 [UploadFromFile][dotnet_UploadFromFile]、[UploadText][dotnet_UploadText][UploadFromStream][dotnet_UploadFromStream], 或 [UploadFromByteArray][dotnet_UploadFromByteArray] 等更新方法，就會發生這個案例，因為這些方法會取代 Blob 的所有內容。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-203">This scenario can occur if you are using an update method such as [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray], because these methods replace all of the contents of a blob.</span></span>

![Azure 儲存體資源](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-4.png)

## <a name="next-steps"></a><span data-ttu-id="d6a7a-205">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d6a7a-205">Next steps</span></span>

* <span data-ttu-id="d6a7a-206">您可以在[使用增量快照備份 Azure 非受控磁碟](../../virtual-machines/windows/incremental-snapshots.md)中，找到使用虛擬機器 (VM) 磁碟快照集的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="d6a7a-206">You can find more information about working with virtual machine (VM) disk snapshots in [Back up Azure unmanaged VM disks with incremental snapshots](../../virtual-machines/windows/incremental-snapshots.md)</span></span>

* <span data-ttu-id="d6a7a-207">如需使用 Blob 儲存體的其他程式碼範例，請參閱 [Azure 程式碼範例](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob)。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-207">For additional code examples using Blob storage, see [Azure Code Samples](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob).</span></span> <span data-ttu-id="d6a7a-208">您可以下載範例應用程式並加以執行，或瀏覽 GitHub 上的程式碼。</span><span class="sxs-lookup"><span data-stu-id="d6a7a-208">You can download a sample application and run it, or browse the code on GitHub.</span></span>

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