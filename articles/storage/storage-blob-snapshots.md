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
# <a name="create-a-blob-snapshot"></a><span data-ttu-id="af5f3-104">建立 Blob 快照集</span><span class="sxs-lookup"><span data-stu-id="af5f3-104">Create a blob snapshot</span></span>

<span data-ttu-id="af5f3-105">快照集是在某個點時間取得的唯讀 Blob 版本。</span><span class="sxs-lookup"><span data-stu-id="af5f3-105">A snapshot is a read-only version of a blob that's taken at a point in time.</span></span> <span data-ttu-id="af5f3-106">快照集對於備份 Blob 非常有用。</span><span class="sxs-lookup"><span data-stu-id="af5f3-106">Snapshots are useful for backing up blobs.</span></span> <span data-ttu-id="af5f3-107">建立快照集後，您便可加以讀取、複製或刪除，但無法加以修改。</span><span class="sxs-lookup"><span data-stu-id="af5f3-107">After you create a snapshot, you can read, copy, or delete it, but you cannot modify it.</span></span>

<span data-ttu-id="af5f3-108">Blob 的快照集是相同 tooits 基底 blob，除非該 hello blob URI 已**DateTime**值附加 toohello blob URI tooindicate hello 時間在哪一個 hello 拍攝快照。</span><span class="sxs-lookup"><span data-stu-id="af5f3-108">A snapshot of a blob is identical tooits base blob, except that hello blob URI has a **DateTime** value appended toohello blob URI tooindicate hello time at which hello snapshot was taken.</span></span> <span data-ttu-id="af5f3-109">例如，如果分頁 blob URI 是`http://storagesample.core.blob.windows.net/mydrives/myvhd`，也很類似 hello 快照集 URI`http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`。</span><span class="sxs-lookup"><span data-stu-id="af5f3-109">For example, if a page blob URI is `http://storagesample.core.blob.windows.net/mydrives/myvhd`, hello snapshot URI is similar too`http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`.</span></span>

> [!NOTE]
> <span data-ttu-id="af5f3-110">所有快照集共用 hello 基底 blob 的 URI。</span><span class="sxs-lookup"><span data-stu-id="af5f3-110">All snapshots share hello base blob's URI.</span></span> <span data-ttu-id="af5f3-111">hello 只有 hello 基底 blob 與 hello 快照之間的差異為附加的 hello **DateTime**值。</span><span class="sxs-lookup"><span data-stu-id="af5f3-111">hello only distinction between hello base blob and hello snapshot is hello appended **DateTime** value.</span></span>
>

<span data-ttu-id="af5f3-112">Blob 可包含任意數目的快照集。</span><span class="sxs-lookup"><span data-stu-id="af5f3-112">A blob can have any number of snapshots.</span></span> <span data-ttu-id="af5f3-113">系統會保存快照集，直到您將它們明確刪除為止。</span><span class="sxs-lookup"><span data-stu-id="af5f3-113">Snapshots persist until they are explicitly deleted.</span></span> <span data-ttu-id="af5f3-114">快照集必須有其基底 Blob 才能存在。</span><span class="sxs-lookup"><span data-stu-id="af5f3-114">A snapshot cannot outlive its base blob.</span></span> <span data-ttu-id="af5f3-115">您可以列舉與 hello 基底 blob tootrack 相關聯的 hello 快照目前的快照集。</span><span class="sxs-lookup"><span data-stu-id="af5f3-115">You can enumerate hello snapshots associated with hello base blob tootrack your current snapshots.</span></span>

<span data-ttu-id="af5f3-116">當您建立 blob 的快照集時，hello blob 的系統屬性會以 hello 複製的 toohello 快照集相同的值。</span><span class="sxs-lookup"><span data-stu-id="af5f3-116">When you create a snapshot of a blob, hello blob's system properties are copied toohello snapshot with hello same values.</span></span> <span data-ttu-id="af5f3-117">hello 基底 blob 的中繼資料也是快照集，請複製的 toohello，除非您指定不同的中繼資料的快照集時建立它的 hello。</span><span class="sxs-lookup"><span data-stu-id="af5f3-117">hello base blob's metadata is also copied toohello snapshot, unless you specify separate metadata for hello snapshot when you create it.</span></span>

<span data-ttu-id="af5f3-118">任何與 hello 基底 blob 相關聯的租用不會影響 hello 快照集。</span><span class="sxs-lookup"><span data-stu-id="af5f3-118">Any leases associated with hello base blob do not affect hello snapshot.</span></span> <span data-ttu-id="af5f3-119">您無法取得快照集上的租用。</span><span class="sxs-lookup"><span data-stu-id="af5f3-119">You cannot acquire a lease on a snapshot.</span></span>

<span data-ttu-id="af5f3-120">VHD 檔案是使用的 toostore hello 目前資訊和 VM 磁碟的狀態。</span><span class="sxs-lookup"><span data-stu-id="af5f3-120">A VHD file is used toostore hello current information and status for a VM disk.</span></span> <span data-ttu-id="af5f3-121">您可以從中斷連接磁碟 hello VM 內或關閉 hello VM，然後再採取其 VHD 檔案的快照集。</span><span class="sxs-lookup"><span data-stu-id="af5f3-121">You can detach a disk from within hello VM or shut down hello VM, and then take a snapshot of its VHD file.</span></span> <span data-ttu-id="af5f3-122">您可以使用該快照集檔案稍後 tooretrieve hello VHD 檔案中該時間點的時間，並重新建立 hello VM。</span><span class="sxs-lookup"><span data-stu-id="af5f3-122">You can use that snapshot file later tooretrieve hello VHD file at that point in time and recreate hello VM.</span></span>

<span data-ttu-id="af5f3-123">如果 hello 儲存體帳戶已啟用儲存體服務加密 (SSE) 中的 hello blob 所在，則採取該 blob 的任何快照集將會加密在靜止。</span><span class="sxs-lookup"><span data-stu-id="af5f3-123">If Storage Service Encryption (SSE) is enabled for hello storage account in which hello blob resides, then any snapshots taken of that blob will be encrypted at rest.</span></span>

## <a name="create-a-snapshot"></a><span data-ttu-id="af5f3-124">建立快照集</span><span class="sxs-lookup"><span data-stu-id="af5f3-124">Create a snapshot</span></span>
<span data-ttu-id="af5f3-125">hello 下列程式碼範例示範如何使用快照集 toocreate hello[適用於.NET 的 Azure 儲存體用戶端程式庫](https://www.nuget.org/packages/WindowsAzure.Storage/)。</span><span class="sxs-lookup"><span data-stu-id="af5f3-125">hello following code example shows how toocreate a snapshot by using hello [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span> <span data-ttu-id="af5f3-126">在建立時，這個範例會指定 hello 快照集的其他中繼資料。</span><span class="sxs-lookup"><span data-stu-id="af5f3-126">This example specifies additional metadata for hello snapshot when it is created.</span></span>

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

## <a name="copy-snapshots"></a><span data-ttu-id="af5f3-127">複製快照集</span><span class="sxs-lookup"><span data-stu-id="af5f3-127">Copy snapshots</span></span>
<span data-ttu-id="af5f3-128">涉及 Blob 和快照集的複製作業會遵循下列規則：</span><span class="sxs-lookup"><span data-stu-id="af5f3-128">Copy operations involving blobs and snapshots follow these rules:</span></span>

* <span data-ttu-id="af5f3-129">您可以將快照集複製到其基底 Blob 之上。</span><span class="sxs-lookup"><span data-stu-id="af5f3-129">You can copy a snapshot over its base blob.</span></span> <span data-ttu-id="af5f3-130">透過升級 hello 基底 blob 的快照集 toohello 位置，您可以還原舊版的 blob。</span><span class="sxs-lookup"><span data-stu-id="af5f3-130">By promoting a snapshot toohello position of hello base blob, you can restore an earlier version of a blob.</span></span> <span data-ttu-id="af5f3-131">hello 快照集會保留，但會覆寫基底 blob 的 hello hello 快照集的可寫入副本。</span><span class="sxs-lookup"><span data-stu-id="af5f3-131">hello snapshot remains, but hello base blob is overwritten with a writable copy of hello snapshot.</span></span>
* <span data-ttu-id="af5f3-132">您可以複製快照集 tooa 目的地 blob，使用不同的名稱。</span><span class="sxs-lookup"><span data-stu-id="af5f3-132">You can copy a snapshot tooa destination blob with a different name.</span></span> <span data-ttu-id="af5f3-133">可寫入的 blob，而不是快照集 hello 產生的目的地 blob。</span><span class="sxs-lookup"><span data-stu-id="af5f3-133">hello resulting destination blob is a writable blob and not a snapshot.</span></span>
* <span data-ttu-id="af5f3-134">當複製來源 blob 時，任何 hello 來源 blob 的快照集不會複製的 toohello 目的地。</span><span class="sxs-lookup"><span data-stu-id="af5f3-134">When a source blob is copied, any snapshots of hello source blob are not copied toohello destination.</span></span> <span data-ttu-id="af5f3-135">當複本覆寫目的地 blob 時，任何與 hello 原始目的地 blob 相關聯的快照集維持不變。</span><span class="sxs-lookup"><span data-stu-id="af5f3-135">When a destination blob is overwritten with a copy, any snapshots associated with hello original destination blob remain intact.</span></span>
* <span data-ttu-id="af5f3-136">當您建立區塊 blob 的快照集時，hello blob 之認可的區塊清單會同時複製的 toohello 快照集。</span><span class="sxs-lookup"><span data-stu-id="af5f3-136">When you create a snapshot of a block blob, hello blob's committed block list is also copied toohello snapshot.</span></span> <span data-ttu-id="af5f3-137">系統不會複製任何未認可的區塊。</span><span class="sxs-lookup"><span data-stu-id="af5f3-137">Any uncommitted blocks are not copied.</span></span>

## <a name="specify-an-access-condition"></a><span data-ttu-id="af5f3-138">指定存取條件</span><span class="sxs-lookup"><span data-stu-id="af5f3-138">Specify an access condition</span></span>
<span data-ttu-id="af5f3-139">當您呼叫[CreateSnapshotAsync][dotnet_CreateSnapshotAsync]，您可以指定存取條件，使得 hello 快照集才會建立符合條件。</span><span class="sxs-lookup"><span data-stu-id="af5f3-139">When you call [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], you can specify an access condition so that hello snapshot is created only if a condition is met.</span></span> <span data-ttu-id="af5f3-140">toospecify 存取條件，使用 hello [AccessCondition] [ dotnet_AccessCondition]參數。</span><span class="sxs-lookup"><span data-stu-id="af5f3-140">toospecify an access condition, use hello [AccessCondition][dotnet_AccessCondition] parameter.</span></span> <span data-ttu-id="af5f3-141">如果不符合條件、 沒有建立 hello 快照集，和 hello Blob 服務會傳回狀態碼，指定 hello [HTTPStatusCode][dotnet_HTTPStatusCode]。PreconditionFailed。</span><span class="sxs-lookup"><span data-stu-id="af5f3-141">If hello specified condition is not met, hello snapshot is not created, and hello Blob service returns status code [HTTPStatusCode][dotnet_HTTPStatusCode].PreconditionFailed.</span></span>

## <a name="delete-snapshots"></a><span data-ttu-id="af5f3-142">刪除快照集</span><span class="sxs-lookup"><span data-stu-id="af5f3-142">Delete snapshots</span></span>
<span data-ttu-id="af5f3-143">您無法刪除具有快照集的 blob，除非 hello 快照集也會一併刪除。</span><span class="sxs-lookup"><span data-stu-id="af5f3-143">You can't delete a blob with snapshots unless hello snapshots are also deleted.</span></span> <span data-ttu-id="af5f3-144">您可以個別刪除快照集或指定刪除 hello 來源 blob 時，會刪除所有快照集。</span><span class="sxs-lookup"><span data-stu-id="af5f3-144">You can delete a snapshot individually, or specify that all snapshots be deleted when hello source blob is deleted.</span></span> <span data-ttu-id="af5f3-145">如果您嘗試 toodelete 仍具有快照集的 blob 時，會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="af5f3-145">If you attempt toodelete a blob that still has snapshots, an error results.</span></span>

<span data-ttu-id="af5f3-146">hello 下列程式碼範例顯示如何 toodelete blob 和在.NET 中，其快照集位置`blockBlob`是類型的物件[CloudBlockBlob][dotnet_CloudBlockBlob]:</span><span class="sxs-lookup"><span data-stu-id="af5f3-146">hello following code example shows how toodelete a blob and its snapshots in .NET, where `blockBlob` is an object of type [CloudBlockBlob][dotnet_CloudBlockBlob]:</span></span>

```csharp
await blockBlob.DeleteIfExistsAsync(DeleteSnapshotsOption.IncludeSnapshots, null, null, null);
```

## <a name="snapshots-with-azure-premium-storage"></a><span data-ttu-id="af5f3-147">快照集與 Azure 進階儲存體</span><span class="sxs-lookup"><span data-stu-id="af5f3-147">Snapshots with Azure Premium Storage</span></span>
<span data-ttu-id="af5f3-148">當使用進階儲存體中的快照集，套用下列規則的 hello:</span><span class="sxs-lookup"><span data-stu-id="af5f3-148">When using snapshots with Premium Storage, hello following rules apply:</span></span>

* <span data-ttu-id="af5f3-149">hello 的每個 premium 儲存體帳戶中的分頁 blob 的快照集數目上限為 100。</span><span class="sxs-lookup"><span data-stu-id="af5f3-149">hello maximum number of snapshots per page blob in a premium storage account is 100.</span></span> <span data-ttu-id="af5f3-150">如果超出該限制，hello 快照集 Blob 作業會傳回錯誤碼 409 (`SnapshotCountExceeded`)。</span><span class="sxs-lookup"><span data-stu-id="af5f3-150">If that limit is exceeded, hello Snapshot Blob operation returns error code 409 (`SnapshotCountExceeded`).</span></span>
* <span data-ttu-id="af5f3-151">您可以每 10 分鐘擷取一次進階儲存體帳戶中分頁 Blob 的快照集。</span><span class="sxs-lookup"><span data-stu-id="af5f3-151">You can take a snapshot of a page blob in a premium storage account once every 10 minutes.</span></span> <span data-ttu-id="af5f3-152">如果超出該比率，hello 快照集 Blob 作業會傳回錯誤碼 409 (`SnapshotOperationRateExceeded`)。</span><span class="sxs-lookup"><span data-stu-id="af5f3-152">If that rate is exceeded, hello Snapshot Blob operation returns error code 409 (`SnapshotOperationRateExceeded`).</span></span>
* <span data-ttu-id="af5f3-153">tooread 快照集，您可以使用 hello 複製 Blob 作業 toocopy 快照 tooanother 分頁 blob hello 帳戶中。</span><span class="sxs-lookup"><span data-stu-id="af5f3-153">tooread a snapshot, you can use hello Copy Blob operation toocopy a snapshot tooanother page blob in hello account.</span></span> <span data-ttu-id="af5f3-154">hello hello 複製作業的目的地 blob 必須沒有任何現有的快照集。</span><span class="sxs-lookup"><span data-stu-id="af5f3-154">hello destination blob for hello copy operation must not have any existing snapshots.</span></span> <span data-ttu-id="af5f3-155">如果 hello 目的地 blob 具有快照集，則 hello 複製 Blob 作業會傳回錯誤碼 409 (`SnapshotsPresent`)。</span><span class="sxs-lookup"><span data-stu-id="af5f3-155">If hello destination blob does have snapshots, then hello Copy Blob operation returns error code 409 (`SnapshotsPresent`).</span></span>

## <a name="return-hello-absolute-uri-tooa-snapshot"></a><span data-ttu-id="af5f3-156">傳回 hello 絕對 URI tooa 快照集</span><span class="sxs-lookup"><span data-stu-id="af5f3-156">Return hello absolute URI tooa snapshot</span></span>
<span data-ttu-id="af5f3-157">這個 C# 程式碼範例會建立快照集，並寫出 hello hello 主要位置的絕對 URI。</span><span class="sxs-lookup"><span data-stu-id="af5f3-157">This C# code example creates a snapshot and writes out hello absolute URI for hello primary location.</span></span>

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

## <a name="understand-how-snapshots-accrue-charges"></a><span data-ttu-id="af5f3-158">了解快照集產生費用的方式</span><span class="sxs-lookup"><span data-stu-id="af5f3-158">Understand how snapshots accrue charges</span></span>
<span data-ttu-id="af5f3-159">建立快照集，這是 blob 的唯讀複本，可能會導致其他資料儲存體費用 tooyour 帳戶。</span><span class="sxs-lookup"><span data-stu-id="af5f3-159">Creating a snapshot, which is a read-only copy of a blob, can result in additional data storage charges tooyour account.</span></span> <span data-ttu-id="af5f3-160">在設計您的應用程式時，很重要 toobe 知道如何這些可能會產生費用，讓成本降至最低。</span><span class="sxs-lookup"><span data-stu-id="af5f3-160">When designing your application, it is important toobe aware of how these charges might accrue so that you can minimize costs.</span></span>

### <a name="important-billing-considerations"></a><span data-ttu-id="af5f3-161">重要的計費考量</span><span class="sxs-lookup"><span data-stu-id="af5f3-161">Important billing considerations</span></span>
<span data-ttu-id="af5f3-162">下列清單中的 hello 包括重點 tooconsider 時建立快照集。</span><span class="sxs-lookup"><span data-stu-id="af5f3-162">hello following list includes key points tooconsider when creating a snapshot.</span></span>

* <span data-ttu-id="af5f3-163">無論是在 hello blob 或 hello 快照中，儲存體帳戶就會產生唯一的區塊或頁面的費用。</span><span class="sxs-lookup"><span data-stu-id="af5f3-163">Your storage account incurs charges for unique blocks or pages, whether they are in hello blob or in hello snapshot.</span></span> <span data-ttu-id="af5f3-164">您的帳戶不會造成額外的費用，除非您更新為基礎的 hello blob 與 blob 相關聯的快照集。</span><span class="sxs-lookup"><span data-stu-id="af5f3-164">Your account does not incur additional charges for snapshots associated with a blob until you update hello blob on which they are based.</span></span> <span data-ttu-id="af5f3-165">更新 hello 基底 blob 之後，它會偏離其快照集。</span><span class="sxs-lookup"><span data-stu-id="af5f3-165">After you update hello base blob, it diverges from its snapshots.</span></span> <span data-ttu-id="af5f3-166">當發生這種情況時，您必須支付 hello 唯一區塊或頁面中的每個 blob 或快照集。</span><span class="sxs-lookup"><span data-stu-id="af5f3-166">When this happens, you are charged for hello unique blocks or pages in each blob or snapshot.</span></span>
* <span data-ttu-id="af5f3-167">當您取代區塊 Blob 內的某個區塊時，後續即會將該區塊視為唯一區塊進行收費。</span><span class="sxs-lookup"><span data-stu-id="af5f3-167">When you replace a block within a block blob, that block is subsequently charged as a unique block.</span></span> <span data-ttu-id="af5f3-168">這是 true，即使 hello 區塊都具有相同的區塊識別碼和 hello 相同的 hello 資料，因為它有 hello 快照集。</span><span class="sxs-lookup"><span data-stu-id="af5f3-168">This is true even if hello block has hello same block ID and hello same data as it has in hello snapshot.</span></span> <span data-ttu-id="af5f3-169">Hello 區塊認可後同樣地，其值與值的任何快照集的對應項目，您將支付其資料。</span><span class="sxs-lookup"><span data-stu-id="af5f3-169">After hello block is committed again, it diverges from its counterpart in any snapshot, and you will be charged for its data.</span></span> <span data-ttu-id="af5f3-170">hello 同樣適用於網頁中使用相同的資料會更新分頁 blob。</span><span class="sxs-lookup"><span data-stu-id="af5f3-170">hello same holds true for a page in a page blob that's updated with identical data.</span></span>
* <span data-ttu-id="af5f3-171">取代區塊 blob 呼叫 hello [UploadFromFile][dotnet_UploadFromFile]， [UploadText][dotnet_UploadText]， [UploadFromStream] [ dotnet_UploadFromStream]，或[UploadFromByteArray] [ dotnet_UploadFromByteArray]方法會取代 hello blob 中的所有區塊。</span><span class="sxs-lookup"><span data-stu-id="af5f3-171">Replacing a block blob by calling hello [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray] method replaces all blocks in hello blob.</span></span> <span data-ttu-id="af5f3-172">如果您有與該 blob 相關聯的快照集，在 hello 基底 blob 和快照集的所有區塊現在都分離，，您將支付這兩個 blob 中的所有 hello 區塊。</span><span class="sxs-lookup"><span data-stu-id="af5f3-172">If you have a snapshot associated with that blob, all blocks in hello base blob and snapshot now diverge, and you will be charged for all hello blocks in both blobs.</span></span> <span data-ttu-id="af5f3-173">即使 hello 基底 blob 和 hello 快照中的 hello 資料都會保持一致，也是如此。</span><span class="sxs-lookup"><span data-stu-id="af5f3-173">This is true even if hello data in hello base blob and hello snapshot remain identical.</span></span>
* <span data-ttu-id="af5f3-174">hello Azure Blob 服務沒有表示 toodetermine 是否兩個區塊包含相同的資料。</span><span class="sxs-lookup"><span data-stu-id="af5f3-174">hello Azure Blob service does not have a means toodetermine whether two blocks contain identical data.</span></span> <span data-ttu-id="af5f3-175">上傳且認可的每個區塊仍會視為唯一，即使它已在相同的資料和 hello hello 相同區塊識別碼。</span><span class="sxs-lookup"><span data-stu-id="af5f3-175">Each block that is uploaded and committed is treated as unique, even if it has hello same data and hello same block ID.</span></span> <span data-ttu-id="af5f3-176">產生唯一的區塊的費用，因為它是重要 tooconsider 更新 blob 具有快照集產生額外的唯一區塊及額外費用。</span><span class="sxs-lookup"><span data-stu-id="af5f3-176">Because charges accrue for unique blocks, it's important tooconsider that updating a blob that has a snapshot results in additional unique blocks and additional charges.</span></span>

### <a name="minimize-cost-with-snapshot-management"></a><span data-ttu-id="af5f3-177">透過管理快照集將成本降到最低</span><span class="sxs-lookup"><span data-stu-id="af5f3-177">Minimize cost with snapshot management</span></span>

<span data-ttu-id="af5f3-178">我們建議您小心管理您的快照集 tooavoid 額外費用。</span><span class="sxs-lookup"><span data-stu-id="af5f3-178">We recommend managing your snapshots carefully tooavoid extra charges.</span></span> <span data-ttu-id="af5f3-179">您可以依照 toohelp 降至最低 hello 成本 hello 儲存體，您的快照集的這些最佳作法：</span><span class="sxs-lookup"><span data-stu-id="af5f3-179">You can follow these best practices toohelp minimize hello costs incurred by hello storage of your snapshots:</span></span>

* <span data-ttu-id="af5f3-180">刪除並重新建立與 blob 相關聯每當您更新 hello blob，即使您正在使用相同的資料，除非您的應用程式設計為需要維護快照集的快照集。</span><span class="sxs-lookup"><span data-stu-id="af5f3-180">Delete and re-create snapshots associated with a blob whenever you update hello blob, even if you are updating with identical data, unless your application design requires that you maintain snapshots.</span></span> <span data-ttu-id="af5f3-181">藉由刪除並重新建立 hello blob 的快照集，您可以確保，hello blob 和快照集不會分流。</span><span class="sxs-lookup"><span data-stu-id="af5f3-181">By deleting and re-creating hello blob's snapshots, you can ensure that hello blob and snapshots do not diverge.</span></span>
* <span data-ttu-id="af5f3-182">如果您要維護 blob 的快照集，避免呼叫[UploadFromFile][dotnet_UploadFromFile]， [UploadText][dotnet_UploadText]， [UploadFromStream][dotnet_UploadFromStream]，或[UploadFromByteArray] [ dotnet_UploadFromByteArray] tooupdate hello blob。</span><span class="sxs-lookup"><span data-stu-id="af5f3-182">If you are maintaining snapshots for a blob, avoid calling [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray] tooupdate hello blob.</span></span> <span data-ttu-id="af5f3-183">這些方法會取代所有 hello blob，導致您的基底 blob 和其快照集 toodiverge 大幅中的 hello 區塊。</span><span class="sxs-lookup"><span data-stu-id="af5f3-183">These methods replace all of hello blocks in hello blob, causing your base blob and its snapshots toodiverge significantly.</span></span> <span data-ttu-id="af5f3-184">相反地，更新 hello 最少的可能值的區塊使用 hello [PutBlock] [ dotnet_PutBlock]和[PutBlockList] [ dotnet_PutBlockList]方法。</span><span class="sxs-lookup"><span data-stu-id="af5f3-184">Instead, update hello fewest possible number of blocks by using hello [PutBlock][dotnet_PutBlock] and [PutBlockList][dotnet_PutBlockList] methods.</span></span>

### <a name="snapshot-billing-scenarios"></a><span data-ttu-id="af5f3-185">快照集計費案例</span><span class="sxs-lookup"><span data-stu-id="af5f3-185">Snapshot billing scenarios</span></span>
<span data-ttu-id="af5f3-186">hello 下列案例示範區塊 blob 和其快照集如何產生費用。</span><span class="sxs-lookup"><span data-stu-id="af5f3-186">hello following scenarios demonstrate how charges accrue for a block blob and its snapshots.</span></span>

<span data-ttu-id="af5f3-187">**案例 1**</span><span class="sxs-lookup"><span data-stu-id="af5f3-187">**Scenario 1**</span></span>

<span data-ttu-id="af5f3-188">在案例 1 中，hello 基底 blob 不後已更新 hello 快照，如此會僅針對唯一區塊 1、 2 和 3 產生費用。</span><span class="sxs-lookup"><span data-stu-id="af5f3-188">In scenario 1, hello base blob has not been updated after hello snapshot was taken, so charges are incurred only for unique blocks 1, 2, and 3.</span></span>

![Azure 儲存體資源](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-1.png)

<span data-ttu-id="af5f3-190">**案例 2**</span><span class="sxs-lookup"><span data-stu-id="af5f3-190">**Scenario 2**</span></span>

<span data-ttu-id="af5f3-191">在案例 2 中，hello 基底 blob 已更新，但 hello 快照中不包含。</span><span class="sxs-lookup"><span data-stu-id="af5f3-191">In scenario 2, hello base blob has been updated, but hello snapshot has not.</span></span> <span data-ttu-id="af5f3-192">區塊 3 已更新，而且即使它包含 hello 相同的資料及 hello 相同的識別碼，就不 hello 與 hello 快照集中的區塊 3 相同。</span><span class="sxs-lookup"><span data-stu-id="af5f3-192">Block 3 was updated, and even though it contains hello same data and hello same ID, it is not hello same as block 3 in hello snapshot.</span></span> <span data-ttu-id="af5f3-193">如此一來，hello 帳戶支付四個區塊。</span><span class="sxs-lookup"><span data-stu-id="af5f3-193">As a result, hello account is charged for four blocks.</span></span>

![Azure 儲存體資源](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-2.png)

<span data-ttu-id="af5f3-195">**案例 3**</span><span class="sxs-lookup"><span data-stu-id="af5f3-195">**Scenario 3**</span></span>

<span data-ttu-id="af5f3-196">案例 3，hello 基底 blob 已更新，但 hello 快照中不包含。</span><span class="sxs-lookup"><span data-stu-id="af5f3-196">In scenario 3, hello base blob has been updated, but hello snapshot has not.</span></span> <span data-ttu-id="af5f3-197">區塊 3 已取代為區塊 4 hello 基底 blob，但 hello 快照集仍反映區塊 3。</span><span class="sxs-lookup"><span data-stu-id="af5f3-197">Block 3 was replaced with block 4 in hello base blob, but hello snapshot still reflects block 3.</span></span> <span data-ttu-id="af5f3-198">如此一來，hello 帳戶支付四個區塊。</span><span class="sxs-lookup"><span data-stu-id="af5f3-198">As a result, hello account is charged for four blocks.</span></span>

![Azure 儲存體資源](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-3.png)

<span data-ttu-id="af5f3-200">**案例 4**</span><span class="sxs-lookup"><span data-stu-id="af5f3-200">**Scenario 4**</span></span>

<span data-ttu-id="af5f3-201">在案例 4 中，hello 基底 blob 已更新完成，未包含任何原始區塊。</span><span class="sxs-lookup"><span data-stu-id="af5f3-201">In scenario 4, hello base blob has been completely updated and contains none of its original blocks.</span></span> <span data-ttu-id="af5f3-202">如此一來，所有的八個唯一區塊的計費 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="af5f3-202">As a result, hello account is charged for all eight unique blocks.</span></span> <span data-ttu-id="af5f3-203">如果您使用 update 方法，例如，可能會發生這個狀況[UploadFromFile][dotnet_UploadFromFile]， [UploadText][dotnet_UploadText]， [UploadFromStream][dotnet_UploadFromStream]，或[UploadFromByteArray][dotnet_UploadFromByteArray]，因為這些方法會取代所有 hello blob 的內容。</span><span class="sxs-lookup"><span data-stu-id="af5f3-203">This scenario can occur if you are using an update method such as [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray], because these methods replace all of hello contents of a blob.</span></span>

![Azure 儲存體資源](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-4.png)

## <a name="next-steps"></a><span data-ttu-id="af5f3-205">後續步驟</span><span class="sxs-lookup"><span data-stu-id="af5f3-205">Next steps</span></span>

* <span data-ttu-id="af5f3-206">您可以在[使用增量快照備份 Azure 非受控磁碟](storage-incremental-snapshots.md)中，找到使用虛擬機器 (VM) 磁碟快照集的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="af5f3-206">You can find more information about working with virtual machine (VM) disk snapshots in [Back up Azure unmanaged VM disks with incremental snapshots](storage-incremental-snapshots.md)</span></span>

* <span data-ttu-id="af5f3-207">如需使用 Blob 儲存體的其他程式碼範例，請參閱 [Azure 程式碼範例](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob)。</span><span class="sxs-lookup"><span data-stu-id="af5f3-207">For additional code examples using Blob storage, see [Azure Code Samples](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob).</span></span> <span data-ttu-id="af5f3-208">您可以下載範例應用程式和執行它，或瀏覽 hello GitHub 上的程式碼。</span><span class="sxs-lookup"><span data-stu-id="af5f3-208">You can download a sample application and run it, or browse hello code on GitHub.</span></span>

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