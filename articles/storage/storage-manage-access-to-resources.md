---
title: "aaaEnable 公開讀取權限為容器和 blob 在 Azure Blob 儲存體 |Microsoft 文件"
description: "深入了解如何 toomake 容器和 blob 供匿名存取，以及如何 tooaccess 它們以程式設計的方式。"
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: a2cffee6-3224-4f2a-8183-66ca23b2d2d7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: marsma
ms.openlocfilehash: 0675b5dc4d32a3a0a34376ae4c049542b07ba03a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-anonymous-read-access-toocontainers-and-blobs"></a><span data-ttu-id="c77eb-103">管理匿名讀取權限 toocontainers 和 blob</span><span class="sxs-lookup"><span data-stu-id="c77eb-103">Manage anonymous read access toocontainers and blobs</span></span>
<span data-ttu-id="c77eb-104">您可以啟用匿名、 公用讀取權限 tooa 容器和其在 Azure Blob 儲存體的 blob。</span><span class="sxs-lookup"><span data-stu-id="c77eb-104">You can enable anonymous, public read access tooa container and its blobs in Azure Blob storage.</span></span> <span data-ttu-id="c77eb-105">如此一來，您可以授與唯讀存取 toothese 資源共用您的帳戶金鑰，而不需要共用的存取簽章 (SAS)。</span><span class="sxs-lookup"><span data-stu-id="c77eb-105">By doing so, you can grant read-only access toothese resources without sharing your account key, and without requiring a shared access signature (SAS).</span></span>

<span data-ttu-id="c77eb-106">公用讀取權限是最佳的案例中，您特定 blob tooalways 可供匿名讀取權限。</span><span class="sxs-lookup"><span data-stu-id="c77eb-106">Public read access is best for scenarios where you want certain blobs tooalways be available for anonymous read access.</span></span> <span data-ttu-id="c77eb-107">對於更深入的控管需求，您可以建立共用存取簽章。</span><span class="sxs-lookup"><span data-stu-id="c77eb-107">For more fine-grained control, you can create a shared access signature.</span></span> <span data-ttu-id="c77eb-108">共用的存取簽章可讓您 tooprovide 限制存取特定的時間內使用不同的權限。</span><span class="sxs-lookup"><span data-stu-id="c77eb-108">Shared access signatures enable you tooprovide restricted access using different permissions, for a specific time period.</span></span> <span data-ttu-id="c77eb-109">如需建立共用存取簽章的詳細資訊，請參閱[在 Azure 儲存體中使用共用存取簽章 (SAS)](storage-dotnet-shared-access-signature-part-1.md)。</span><span class="sxs-lookup"><span data-stu-id="c77eb-109">For more information about creating shared access signatures, see [Using shared access signatures (SAS) in Azure Storage](storage-dotnet-shared-access-signature-part-1.md).</span></span>

## <a name="grant-anonymous-users-permissions-toocontainers-and-blobs"></a><span data-ttu-id="c77eb-110">授與匿名使用者的權限 toocontainers 和 blob</span><span class="sxs-lookup"><span data-stu-id="c77eb-110">Grant anonymous users permissions toocontainers and blobs</span></span>
<span data-ttu-id="c77eb-111">根據預設，容器和內部任何 blob 能存取只能由 hello hello 儲存體帳戶的擁有者。</span><span class="sxs-lookup"><span data-stu-id="c77eb-111">By default, a container and any blobs within it may be accessed only by hello owner of hello storage account.</span></span> <span data-ttu-id="c77eb-112">toogive 匿名使用者的讀取權限 tooa 容器和其 blob，您可以設定 hello 容器的權限 tooallow 公用存取。</span><span class="sxs-lookup"><span data-stu-id="c77eb-112">toogive anonymous users read permissions tooa container and its blobs, you can set hello container permissions tooallow public access.</span></span> <span data-ttu-id="c77eb-113">匿名使用者可以讀取可公開存取容器中的 blob，而不需驗證 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="c77eb-113">Anonymous users can read blobs within a publicly accessible container without authenticating hello request.</span></span>

<span data-ttu-id="c77eb-114">您可以設定容器具有下列權限的 hello:</span><span class="sxs-lookup"><span data-stu-id="c77eb-114">You can configure a container with hello following permissions:</span></span>

* <span data-ttu-id="c77eb-115">**沒有公開讀取權限：** hello 容器和其 blob 可以只由存取 hello 儲存體帳戶擁有者。</span><span class="sxs-lookup"><span data-stu-id="c77eb-115">**No public read access:** hello container and its blobs can be accessed only by hello storage account owner.</span></span> <span data-ttu-id="c77eb-116">這是所有的新容器的 hello 預設。</span><span class="sxs-lookup"><span data-stu-id="c77eb-116">This is hello default for all new containers.</span></span>
* <span data-ttu-id="c77eb-117">**僅對 blob 具有公開讀取：** hello 容器中的 Blob 可以讀取的匿名要求，但沒有可用容器資料。</span><span class="sxs-lookup"><span data-stu-id="c77eb-117">**Public read access for blobs only:** Blobs within hello container can be read by anonymous request, but container data is not available.</span></span> <span data-ttu-id="c77eb-118">匿名用戶端無法列舉 hello hello 容器內的 blob。</span><span class="sxs-lookup"><span data-stu-id="c77eb-118">Anonymous clients cannot enumerate hello blobs within hello container.</span></span>
* <span data-ttu-id="c77eb-119">**完整的公用讀取權限：**可以透過匿名要求讀取所有容器和 Blob 資料。</span><span class="sxs-lookup"><span data-stu-id="c77eb-119">**Full public read access:** All container and blob data can be read by anonymous request.</span></span> <span data-ttu-id="c77eb-120">用戶端可以匿名要求，列舉 hello 容器中的 blob，但無法列舉 hello 儲存體帳戶中的容器。</span><span class="sxs-lookup"><span data-stu-id="c77eb-120">Clients can enumerate blobs within hello container by anonymous request, but cannot enumerate containers within hello storage account.</span></span>

<span data-ttu-id="c77eb-121">您可以使用下列 tooset 容器權限的 hello:</span><span class="sxs-lookup"><span data-stu-id="c77eb-121">You can use hello following tooset container permissions:</span></span>

* [<span data-ttu-id="c77eb-122">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="c77eb-122">Azure portal</span></span>](https://portal.azure.com)
* [<span data-ttu-id="c77eb-123">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c77eb-123">Azure PowerShell</span></span>](storage-powershell-guide-full.md#how-to-manage-azure-blobs)
* [<span data-ttu-id="c77eb-124">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c77eb-124">Azure CLI 2.0</span></span>](storage-azure-cli.md#create-and-manage-blobs)
* <span data-ttu-id="c77eb-125">以程式設計方式，利用其中一個 hello 儲存體用戶端程式庫或 hello REST API</span><span class="sxs-lookup"><span data-stu-id="c77eb-125">Programmatically, by using one of hello storage client libraries or hello REST API</span></span>

### <a name="set-container-permissions-in-hello-azure-portal"></a><span data-ttu-id="c77eb-126">在 hello Azure 入口網站中設定容器的權限</span><span class="sxs-lookup"><span data-stu-id="c77eb-126">Set container permissions in hello Azure portal</span></span>
<span data-ttu-id="c77eb-127">在 hello tooset 容器權限[Azure 入口網站](https://portal.azure.com)，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="c77eb-127">tooset container permissions in hello [Azure portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="c77eb-128">開啟您**儲存體帳戶**hello 入口網站中的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="c77eb-128">Open your **Storage account** blade in hello portal.</span></span> <span data-ttu-id="c77eb-129">您可以尋找儲存體帳戶選取**儲存體帳戶**hello 主要入口網站功能表刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="c77eb-129">You can find your storage account by selecting **Storage accounts** in hello main portal menu blade.</span></span>
1. <span data-ttu-id="c77eb-130">在下**BLOB 服務**hello 功能表 刀鋒視窗中，選取**容器**。</span><span class="sxs-lookup"><span data-stu-id="c77eb-130">Under **BLOB SERVICE** on hello menu blade, select **Containers**.</span></span>
1. <span data-ttu-id="c77eb-131">以滑鼠右鍵按一下 hello 容器資料列或選取 hello 省略 tooopen hello 容器的**操作功能表**。</span><span class="sxs-lookup"><span data-stu-id="c77eb-131">Right-click on hello container row or select hello ellipsis tooopen hello container's **Context menu**.</span></span>
1. <span data-ttu-id="c77eb-132">選取**存取原則**hello 內容功能表中。</span><span class="sxs-lookup"><span data-stu-id="c77eb-132">Select **Access policy** in hello context menu.</span></span>
1. <span data-ttu-id="c77eb-133">選取**存取類型**hello 從下拉功能表。</span><span class="sxs-lookup"><span data-stu-id="c77eb-133">Select an **Access type** from hello drop down menu.</span></span>

    ![編輯容器中繼資料對話方塊](./media/storage-manage-access-to-resources/storage-manage-access-to-resources-0.png)

### <a name="set-container-permissions-with-net"></a><span data-ttu-id="c77eb-135">使用 .NET 設定容器權限</span><span class="sxs-lookup"><span data-stu-id="c77eb-135">Set container permissions with .NET</span></span>
<span data-ttu-id="c77eb-136">tooset for.NET，使用 C# 和 hello 儲存體用戶端程式庫容器的權限第一次擷取 hello 容器的現有權限呼叫 hello **GetPermissions**方法。</span><span class="sxs-lookup"><span data-stu-id="c77eb-136">tooset permissions for a container using C# and hello Storage Client Library for .NET, first retrieve hello container's existing permissions by calling hello **GetPermissions** method.</span></span> <span data-ttu-id="c77eb-137">然後組 hello **PublicAccess**屬性 hello **BlobContainerPermissions** hello 所傳回的物件**GetPermissions**方法。</span><span class="sxs-lookup"><span data-stu-id="c77eb-137">Then set hello **PublicAccess** property for hello **BlobContainerPermissions** object that is returned by hello **GetPermissions** method.</span></span> <span data-ttu-id="c77eb-138">最後，呼叫 hello **SetPermissions**方法 hello 與更新權限。</span><span class="sxs-lookup"><span data-stu-id="c77eb-138">Finally, call hello **SetPermissions** method with hello updated permissions.</span></span>

<span data-ttu-id="c77eb-139">下列範例中的 hello 設定 hello 容器的權限 toofull 公用讀取權限。</span><span class="sxs-lookup"><span data-stu-id="c77eb-139">hello following example sets hello container's permissions toofull public read access.</span></span> <span data-ttu-id="c77eb-140">tooset 權限 toopublic 「 讀取 」 存取 blob，設定 hello **PublicAccess**屬性太**BlobContainerPublicAccessType.Blob**。</span><span class="sxs-lookup"><span data-stu-id="c77eb-140">tooset permissions toopublic read access for blobs only, set hello **PublicAccess** property too**BlobContainerPublicAccessType.Blob**.</span></span> <span data-ttu-id="c77eb-141">tooremove 所有匿名使用者，權限設定太 hello 屬性**BlobContainerPublicAccessType.Off**。</span><span class="sxs-lookup"><span data-stu-id="c77eb-141">tooremove all permissions for anonymous users, set hello property too**BlobContainerPublicAccessType.Off**.</span></span>

```csharp
public static void SetPublicContainerPermissions(CloudBlobContainer container)
{
    BlobContainerPermissions permissions = container.GetPermissions();
    permissions.PublicAccess = BlobContainerPublicAccessType.Container;
    container.SetPermissions(permissions);
}
```

## <a name="access-containers-and-blobs-anonymously"></a><span data-ttu-id="c77eb-142">匿名存取容器與 Blob</span><span class="sxs-lookup"><span data-stu-id="c77eb-142">Access containers and blobs anonymously</span></span>
<span data-ttu-id="c77eb-143">匿名存取容器與 Blob 的用戶端可使用不需要認證的建構函式。</span><span class="sxs-lookup"><span data-stu-id="c77eb-143">A client that accesses containers and blobs anonymously can use constructors that do not require credentials.</span></span> <span data-ttu-id="c77eb-144">hello 遵循範例顯示一些不同方式 tooreference Blob 服務資源以匿名方式。</span><span class="sxs-lookup"><span data-stu-id="c77eb-144">hello following examples show a few different ways tooreference Blob service resources anonymously.</span></span>

### <a name="create-an-anonymous-client-object"></a><span data-ttu-id="c77eb-145">建立匿名用戶端物件</span><span class="sxs-lookup"><span data-stu-id="c77eb-145">Create an anonymous client object</span></span>
<span data-ttu-id="c77eb-146">您可以藉由提供 hello Blob 服務端點 hello 帳戶建立新的服務用戶端物件來匿名存取。</span><span class="sxs-lookup"><span data-stu-id="c77eb-146">You can create a new service client object for anonymous access by providing hello Blob service endpoint for hello account.</span></span> <span data-ttu-id="c77eb-147">不過，您也必須知道 hello 供匿名存取該帳戶中的容器名稱。</span><span class="sxs-lookup"><span data-stu-id="c77eb-147">However, you must also know hello name of a container in that account that's available for anonymous access.</span></span>

```csharp
public static void CreateAnonymousBlobClient()
{
    // Create hello client object using hello Blob service endpoint.
    CloudBlobClient blobClient = new CloudBlobClient(new Uri(@"https://storagesample.blob.core.windows.net"));

    // Get a reference tooa container that's available for anonymous access.
    CloudBlobContainer container = blobClient.GetContainerReference("sample-container");

    // Read hello container's properties. Note this is only possible when hello container supports full public read access.
    container.FetchAttributes();
    Console.WriteLine(container.Properties.LastModified);
    Console.WriteLine(container.Properties.ETag);
}
```

### <a name="reference-a-container-anonymously"></a><span data-ttu-id="c77eb-148">匿名參考容器</span><span class="sxs-lookup"><span data-stu-id="c77eb-148">Reference a container anonymously</span></span>
<span data-ttu-id="c77eb-149">如果您擁有 hello URL tooa 容器以匿名方式可用，您可以使用它 tooreference hello 容器直接。</span><span class="sxs-lookup"><span data-stu-id="c77eb-149">If you have hello URL tooa container that is anonymously available, you can use it tooreference hello container directly.</span></span>

```csharp
public static void ListBlobsAnonymously()
{
    // Get a reference tooa container that's available for anonymous access.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(@"https://storagesample.blob.core.windows.net/sample-container"));

    // List blobs in hello container.
    foreach (IListBlobItem blobItem in container.ListBlobs())
    {
        Console.WriteLine(blobItem.Uri);
    }
}
```

### <a name="reference-a-blob-anonymously"></a><span data-ttu-id="c77eb-150">匿名參考 Blob</span><span class="sxs-lookup"><span data-stu-id="c77eb-150">Reference a blob anonymously</span></span>
<span data-ttu-id="c77eb-151">如果您有可供匿名存取的 hello URL tooa blob，您可以參考直接使用該 URL 的 hello blob:</span><span class="sxs-lookup"><span data-stu-id="c77eb-151">If you have hello URL tooa blob that is available for anonymous access, you can reference hello blob directly using that URL:</span></span>

```csharp
public static void DownloadBlobAnonymously()
{
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(@"https://storagesample.blob.core.windows.net/sample-container/logfile.txt"));
    blob.DownloadToFile(@"C:\Temp\logfile.txt", System.IO.FileMode.Create);
}
```

## <a name="features-available-tooanonymous-users"></a><span data-ttu-id="c77eb-152">功能可用 tooanonymous 使用者</span><span class="sxs-lookup"><span data-stu-id="c77eb-152">Features available tooanonymous users</span></span>
<span data-ttu-id="c77eb-153">hello 下表顯示容器的 ACL 設定 tooallow 公用存取時，可能會由匿名使用者呼叫哪些作業。</span><span class="sxs-lookup"><span data-stu-id="c77eb-153">hello following table shows which operations may be called by anonymous users when a container's ACL is set tooallow public access.</span></span>

| <span data-ttu-id="c77eb-154">REST 作業</span><span class="sxs-lookup"><span data-stu-id="c77eb-154">REST Operation</span></span> | <span data-ttu-id="c77eb-155">具有完整公開讀取權限</span><span class="sxs-lookup"><span data-stu-id="c77eb-155">Permission with full public read access</span></span> | <span data-ttu-id="c77eb-156">僅對 Blob 有公開讀取權限</span><span class="sxs-lookup"><span data-stu-id="c77eb-156">Permission with public read access for blobs only</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c77eb-157">列出容器</span><span class="sxs-lookup"><span data-stu-id="c77eb-157">List Containers</span></span> |<span data-ttu-id="c77eb-158">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="c77eb-158">Owner only</span></span> |<span data-ttu-id="c77eb-159">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="c77eb-159">Owner only</span></span> |
| <span data-ttu-id="c77eb-160">建立容器</span><span class="sxs-lookup"><span data-stu-id="c77eb-160">Create Container</span></span> |<span data-ttu-id="c77eb-161">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="c77eb-161">Owner only</span></span> |<span data-ttu-id="c77eb-162">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="c77eb-162">Owner only</span></span> |
| <span data-ttu-id="c77eb-163">取得容器屬性</span><span class="sxs-lookup"><span data-stu-id="c77eb-163">Get Container Properties</span></span> |<span data-ttu-id="c77eb-164">全部</span><span class="sxs-lookup"><span data-stu-id="c77eb-164">All</span></span> |<span data-ttu-id="c77eb-165">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="c77eb-165">Owner only</span></span> |
| <span data-ttu-id="c77eb-166">取得容器中繼資料</span><span class="sxs-lookup"><span data-stu-id="c77eb-166">Get Container Metadata</span></span> |<span data-ttu-id="c77eb-167">全部</span><span class="sxs-lookup"><span data-stu-id="c77eb-167">All</span></span> |<span data-ttu-id="c77eb-168">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="c77eb-168">Owner only</span></span> |
| <span data-ttu-id="c77eb-169">設定容器中繼資料</span><span class="sxs-lookup"><span data-stu-id="c77eb-169">Set Container Metadata</span></span> |<span data-ttu-id="c77eb-170">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="c77eb-170">Owner only</span></span> |<span data-ttu-id="c77eb-171">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="c77eb-171">Owner only</span></span> |
| <span data-ttu-id="c77eb-172">取得容器 ACL</span><span class="sxs-lookup"><span data-stu-id="c77eb-172">Get Container ACL</span></span> |<span data-ttu-id="c77eb-173">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="c77eb-173">Owner only</span></span> |<span data-ttu-id="c77eb-174">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="c77eb-174">Owner only</span></span> |
| <span data-ttu-id="c77eb-175">設定容器 ACL</span><span class="sxs-lookup"><span data-stu-id="c77eb-175">Set Container ACL</span></span> |<span data-ttu-id="c77eb-176">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="c77eb-176">Owner only</span></span> |<span data-ttu-id="c77eb-177">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="c77eb-177">Owner only</span></span> |
| <span data-ttu-id="c77eb-178">刪除容器</span><span class="sxs-lookup"><span data-stu-id="c77eb-178">Delete Container</span></span> |<span data-ttu-id="c77eb-179">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="c77eb-179">Owner only</span></span> |<span data-ttu-id="c77eb-180">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="c77eb-180">Owner only</span></span> |
| <span data-ttu-id="c77eb-181">列出 Blob</span><span class="sxs-lookup"><span data-stu-id="c77eb-181">List Blobs</span></span> |<span data-ttu-id="c77eb-182">全部</span><span class="sxs-lookup"><span data-stu-id="c77eb-182">All</span></span> |<span data-ttu-id="c77eb-183">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="c77eb-183">Owner only</span></span> |
| <span data-ttu-id="c77eb-184">放置 Blob</span><span class="sxs-lookup"><span data-stu-id="c77eb-184">Put Blob</span></span> |<span data-ttu-id="c77eb-185">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="c77eb-185">Owner only</span></span> |<span data-ttu-id="c77eb-186">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="c77eb-186">Owner only</span></span> |
| <span data-ttu-id="c77eb-187">取得 Blob</span><span class="sxs-lookup"><span data-stu-id="c77eb-187">Get Blob</span></span> |<span data-ttu-id="c77eb-188">全部</span><span class="sxs-lookup"><span data-stu-id="c77eb-188">All</span></span> |<span data-ttu-id="c77eb-189">全部</span><span class="sxs-lookup"><span data-stu-id="c77eb-189">All</span></span> |
| <span data-ttu-id="c77eb-190">取得 Blob 屬性</span><span class="sxs-lookup"><span data-stu-id="c77eb-190">Get Blob Properties</span></span> |<span data-ttu-id="c77eb-191">全部</span><span class="sxs-lookup"><span data-stu-id="c77eb-191">All</span></span> |<span data-ttu-id="c77eb-192">全部</span><span class="sxs-lookup"><span data-stu-id="c77eb-192">All</span></span> |
| <span data-ttu-id="c77eb-193">設定 Blob 屬性</span><span class="sxs-lookup"><span data-stu-id="c77eb-193">Set Blob Properties</span></span> |<span data-ttu-id="c77eb-194">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="c77eb-194">Owner only</span></span> |<span data-ttu-id="c77eb-195">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="c77eb-195">Owner only</span></span> |
| <span data-ttu-id="c77eb-196">取得 Blob 中繼資料</span><span class="sxs-lookup"><span data-stu-id="c77eb-196">Get Blob Metadata</span></span> |<span data-ttu-id="c77eb-197">全部</span><span class="sxs-lookup"><span data-stu-id="c77eb-197">All</span></span> |<span data-ttu-id="c77eb-198">全部</span><span class="sxs-lookup"><span data-stu-id="c77eb-198">All</span></span> |
| <span data-ttu-id="c77eb-199">設定 Blob 中繼資料</span><span class="sxs-lookup"><span data-stu-id="c77eb-199">Set Blob Metadata</span></span> |<span data-ttu-id="c77eb-200">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="c77eb-200">Owner only</span></span> |<span data-ttu-id="c77eb-201">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="c77eb-201">Owner only</span></span> |
| <span data-ttu-id="c77eb-202">放置區塊</span><span class="sxs-lookup"><span data-stu-id="c77eb-202">Put Block</span></span> |<span data-ttu-id="c77eb-203">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="c77eb-203">Owner only</span></span> |<span data-ttu-id="c77eb-204">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="c77eb-204">Owner only</span></span> |
| <span data-ttu-id="c77eb-205">取得區塊清單 (僅限認可區塊)</span><span class="sxs-lookup"><span data-stu-id="c77eb-205">Get Block List (committed blocks only)</span></span> |<span data-ttu-id="c77eb-206">全部</span><span class="sxs-lookup"><span data-stu-id="c77eb-206">All</span></span> |<span data-ttu-id="c77eb-207">全部</span><span class="sxs-lookup"><span data-stu-id="c77eb-207">All</span></span> |
| <span data-ttu-id="c77eb-208">取得區塊清單 (僅限未認可的區塊或所有區塊)</span><span class="sxs-lookup"><span data-stu-id="c77eb-208">Get Block List (uncommitted blocks only or all blocks)</span></span> |<span data-ttu-id="c77eb-209">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="c77eb-209">Owner only</span></span> |<span data-ttu-id="c77eb-210">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="c77eb-210">Owner only</span></span> |
| <span data-ttu-id="c77eb-211">放置區塊清單</span><span class="sxs-lookup"><span data-stu-id="c77eb-211">Put Block List</span></span> |<span data-ttu-id="c77eb-212">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="c77eb-212">Owner only</span></span> |<span data-ttu-id="c77eb-213">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="c77eb-213">Owner only</span></span> |
| <span data-ttu-id="c77eb-214">刪除 Blob</span><span class="sxs-lookup"><span data-stu-id="c77eb-214">Delete Blob</span></span> |<span data-ttu-id="c77eb-215">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="c77eb-215">Owner only</span></span> |<span data-ttu-id="c77eb-216">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="c77eb-216">Owner only</span></span> |
| <span data-ttu-id="c77eb-217">複製 Blob</span><span class="sxs-lookup"><span data-stu-id="c77eb-217">Copy Blob</span></span> |<span data-ttu-id="c77eb-218">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="c77eb-218">Owner only</span></span> |<span data-ttu-id="c77eb-219">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="c77eb-219">Owner only</span></span> |
| <span data-ttu-id="c77eb-220">快照 Blob</span><span class="sxs-lookup"><span data-stu-id="c77eb-220">Snapshot Blob</span></span> |<span data-ttu-id="c77eb-221">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="c77eb-221">Owner only</span></span> |<span data-ttu-id="c77eb-222">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="c77eb-222">Owner only</span></span> |
| <span data-ttu-id="c77eb-223">租用 Blob</span><span class="sxs-lookup"><span data-stu-id="c77eb-223">Lease Blob</span></span> |<span data-ttu-id="c77eb-224">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="c77eb-224">Owner only</span></span> |<span data-ttu-id="c77eb-225">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="c77eb-225">Owner only</span></span> |
| <span data-ttu-id="c77eb-226">放置頁面</span><span class="sxs-lookup"><span data-stu-id="c77eb-226">Put Page</span></span> |<span data-ttu-id="c77eb-227">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="c77eb-227">Owner only</span></span> |<span data-ttu-id="c77eb-228">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="c77eb-228">Owner only</span></span> |
| <span data-ttu-id="c77eb-229">取得頁面範圍</span><span class="sxs-lookup"><span data-stu-id="c77eb-229">Get Page Ranges</span></span> |<span data-ttu-id="c77eb-230">全部</span><span class="sxs-lookup"><span data-stu-id="c77eb-230">All</span></span> |<span data-ttu-id="c77eb-231">全部</span><span class="sxs-lookup"><span data-stu-id="c77eb-231">All</span></span> |
| <span data-ttu-id="c77eb-232">附加 Blob</span><span class="sxs-lookup"><span data-stu-id="c77eb-232">Append Blob</span></span> |<span data-ttu-id="c77eb-233">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="c77eb-233">Owner only</span></span> |<span data-ttu-id="c77eb-234">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="c77eb-234">Owner only</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c77eb-235">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c77eb-235">Next steps</span></span>

* [<span data-ttu-id="c77eb-236">Hello Azure 儲存體服務的驗證</span><span class="sxs-lookup"><span data-stu-id="c77eb-236">Authentication for hello Azure Storage Services</span></span>](https://msdn.microsoft.com/library/azure/dd179428.aspx)
* [<span data-ttu-id="c77eb-237">使用共用存取簽章 (SAS)</span><span class="sxs-lookup"><span data-stu-id="c77eb-237">Using Shared Access Signatures (SAS)</span></span>](storage-dotnet-shared-access-signature-part-1.md)
* [<span data-ttu-id="c77eb-238">使用共用存取簽章來委派存取權</span><span class="sxs-lookup"><span data-stu-id="c77eb-238">Delegating Access with a Shared Access Signature</span></span>](https://msdn.microsoft.com/library/azure/ee395415.aspx)
