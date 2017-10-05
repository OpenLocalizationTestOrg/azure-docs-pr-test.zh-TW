---
title: "對 Azure Blob 儲存體中的容器與 Blob 啟用公用讀取權限 | Microsoft Docs"
description: "了解如何讓容器與 Blob 可供匿名存取，以及如何以程式設計方式存取。"
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
ms.openlocfilehash: c7b83667b58649c156a62fa68cebd854c13e2cba
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-anonymous-read-access-to-containers-and-blobs"></a><span data-ttu-id="5e656-103">管理對容器與 Blob 的匿名讀取權限。</span><span class="sxs-lookup"><span data-stu-id="5e656-103">Manage anonymous read access to containers and blobs</span></span>
<span data-ttu-id="5e656-104">您可以對 Azure Blob 儲存體中的容器及其 Blob 啟用匿名與公用讀取權限。</span><span class="sxs-lookup"><span data-stu-id="5e656-104">You can enable anonymous, public read access to a container and its blobs in Azure Blob storage.</span></span> <span data-ttu-id="5e656-105">如此您就可以將這些資源的唯讀存取權限授與他人，而無須共用您的帳戶金鑰，也無須要求共用存取簽章 (SAS)。</span><span class="sxs-lookup"><span data-stu-id="5e656-105">By doing so, you can grant read-only access to these resources without sharing your account key, and without requiring a shared access signature (SAS).</span></span>

<span data-ttu-id="5e656-106">公用讀取權限適用於您想要某些 Blob 永遠可供匿名讀取存取的狀況。</span><span class="sxs-lookup"><span data-stu-id="5e656-106">Public read access is best for scenarios where you want certain blobs to always be available for anonymous read access.</span></span> <span data-ttu-id="5e656-107">對於更深入的控管需求，您可以建立共用存取簽章。</span><span class="sxs-lookup"><span data-stu-id="5e656-107">For more fine-grained control, you can create a shared access signature.</span></span> <span data-ttu-id="5e656-108">共用存取簽章可讓您針對一段特定時間提供不同權限的限制存取。</span><span class="sxs-lookup"><span data-stu-id="5e656-108">Shared access signatures enable you to provide restricted access using different permissions, for a specific time period.</span></span> <span data-ttu-id="5e656-109">如需建立共用存取簽章的詳細資訊，請參閱[在 Azure 儲存體中使用共用存取簽章 (SAS)](storage-dotnet-shared-access-signature-part-1.md)。</span><span class="sxs-lookup"><span data-stu-id="5e656-109">For more information about creating shared access signatures, see [Using shared access signatures (SAS) in Azure Storage](storage-dotnet-shared-access-signature-part-1.md).</span></span>

## <a name="grant-anonymous-users-permissions-to-containers-and-blobs"></a><span data-ttu-id="5e656-110">授與容器和 Blob 的匿名使用者權限</span><span class="sxs-lookup"><span data-stu-id="5e656-110">Grant anonymous users permissions to containers and blobs</span></span>
<span data-ttu-id="5e656-111">根據預設，可能只有儲存體帳戶的擁有者能存取容器及其內部的任何 Blob。</span><span class="sxs-lookup"><span data-stu-id="5e656-111">By default, a container and any blobs within it may be accessed only by the owner of the storage account.</span></span> <span data-ttu-id="5e656-112">若要為匿名使用者授與容器及其 Blob 的讀取權限，您可以設定容器權限以允許公用存取。</span><span class="sxs-lookup"><span data-stu-id="5e656-112">To give anonymous users read permissions to a container and its blobs, you can set the container permissions to allow public access.</span></span> <span data-ttu-id="5e656-113">匿名使用者可以讀取可公開存取之容器內的 Blob，而不需驗證要求。</span><span class="sxs-lookup"><span data-stu-id="5e656-113">Anonymous users can read blobs within a publicly accessible container without authenticating the request.</span></span>

<span data-ttu-id="5e656-114">您可以為容器設定下列權限︰</span><span class="sxs-lookup"><span data-stu-id="5e656-114">You can configure a container with the following permissions:</span></span>

* <span data-ttu-id="5e656-115">**無公用讀取權限︰**只有儲存體帳戶擁有者可以存取容器和其 Blob。</span><span class="sxs-lookup"><span data-stu-id="5e656-115">**No public read access:** The container and its blobs can be accessed only by the storage account owner.</span></span> <span data-ttu-id="5e656-116">這是所有新建容器的預設值。</span><span class="sxs-lookup"><span data-stu-id="5e656-116">This is the default for all new containers.</span></span>
* <span data-ttu-id="5e656-117">**僅對 Blob 有公用讀取權限：**您可以透過匿名要求讀取容器內的 Blob，但您無法使用容器資料。</span><span class="sxs-lookup"><span data-stu-id="5e656-117">**Public read access for blobs only:** Blobs within the container can be read by anonymous request, but container data is not available.</span></span> <span data-ttu-id="5e656-118">匿名用戶端無法列舉容器內的 Blob。</span><span class="sxs-lookup"><span data-stu-id="5e656-118">Anonymous clients cannot enumerate the blobs within the container.</span></span>
* <span data-ttu-id="5e656-119">**完整的公用讀取權限：**可以透過匿名要求讀取所有容器和 Blob 資料。</span><span class="sxs-lookup"><span data-stu-id="5e656-119">**Full public read access:** All container and blob data can be read by anonymous request.</span></span> <span data-ttu-id="5e656-120">用戶端可以透過匿名要求列舉容器內的 Blob，但無法列舉儲存體帳戶內的容器。</span><span class="sxs-lookup"><span data-stu-id="5e656-120">Clients can enumerate blobs within the container by anonymous request, but cannot enumerate containers within the storage account.</span></span>

<span data-ttu-id="5e656-121">您可以使用下列方式設定容器權限：</span><span class="sxs-lookup"><span data-stu-id="5e656-121">You can use the following to set container permissions:</span></span>

* [<span data-ttu-id="5e656-122">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="5e656-122">Azure portal</span></span>](https://portal.azure.com)
* [<span data-ttu-id="5e656-123">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5e656-123">Azure PowerShell</span></span>](storage-powershell-guide-full.md#how-to-manage-azure-blobs)
* [<span data-ttu-id="5e656-124">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5e656-124">Azure CLI 2.0</span></span>](storage-azure-cli.md#create-and-manage-blobs)
* <span data-ttu-id="5e656-125">使用其中一個儲存體用戶端程式庫或 REST API 以程式設計方式設定</span><span class="sxs-lookup"><span data-stu-id="5e656-125">Programmatically, by using one of the storage client libraries or the REST API</span></span>

### <a name="set-container-permissions-in-the-azure-portal"></a><span data-ttu-id="5e656-126">在 Azure 入口網站中設定容器權限</span><span class="sxs-lookup"><span data-stu-id="5e656-126">Set container permissions in the Azure portal</span></span>
<span data-ttu-id="5e656-127">若要在 [Azure 入口網站](https://portal.azure.com)中設定容器權限，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5e656-127">To set container permissions in the [Azure portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="5e656-128">在入口網站中開啟 [儲存體帳戶] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="5e656-128">Open your **Storage account** blade in the portal.</span></span> <span data-ttu-id="5e656-129">您可以在主要入口網站的功能表刀鋒視窗中選取 [儲存體帳戶]，來尋找您的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5e656-129">You can find your storage account by selecting **Storage accounts** in the main portal menu blade.</span></span>
1. <span data-ttu-id="5e656-130">在功能表刀鋒視窗的 [BLOB 服務] 下，選取 [容器]。</span><span class="sxs-lookup"><span data-stu-id="5e656-130">Under **BLOB SERVICE** on the menu blade, select **Containers**.</span></span>
1. <span data-ttu-id="5e656-131">以滑鼠右鍵按一下容器資料列或選取省略符號來開啟容器的**操作功能表**。</span><span class="sxs-lookup"><span data-stu-id="5e656-131">Right-click on the container row or select the ellipsis to open the container's **Context menu**.</span></span>
1. <span data-ttu-id="5e656-132">在操作功能表中選取 [存取原則]。</span><span class="sxs-lookup"><span data-stu-id="5e656-132">Select **Access policy** in the context menu.</span></span>
1. <span data-ttu-id="5e656-133">從下拉式功能表中選取 [存取類型]。</span><span class="sxs-lookup"><span data-stu-id="5e656-133">Select an **Access type** from the drop down menu.</span></span>

    ![編輯容器中繼資料對話方塊](./media/storage-manage-access-to-resources/storage-manage-access-to-resources-0.png)

### <a name="set-container-permissions-with-net"></a><span data-ttu-id="5e656-135">使用 .NET 設定容器權限</span><span class="sxs-lookup"><span data-stu-id="5e656-135">Set container permissions with .NET</span></span>
<span data-ttu-id="5e656-136">若要使用 .NET 的 C# 和儲存體用戶端程式庫來設定容器的權限，請先呼叫 **GetPermissions** 方法來擷取容器的現有權限。</span><span class="sxs-lookup"><span data-stu-id="5e656-136">To set permissions for a container using C# and the Storage Client Library for .NET, first retrieve the container's existing permissions by calling the **GetPermissions** method.</span></span> <span data-ttu-id="5e656-137">接著為由 **GetPermissions** 方法傳回的 **BlobContainerPermissions** 物件設定 **PublicAccess** 屬性。</span><span class="sxs-lookup"><span data-stu-id="5e656-137">Then set the **PublicAccess** property for the **BlobContainerPermissions** object that is returned by the **GetPermissions** method.</span></span> <span data-ttu-id="5e656-138">最後，使用更新的權限呼叫 **SetPermissions** 方法。</span><span class="sxs-lookup"><span data-stu-id="5e656-138">Finally, call the **SetPermissions** method with the updated permissions.</span></span>

<span data-ttu-id="5e656-139">下列範例將容器的權限設為完整公用讀取權限。</span><span class="sxs-lookup"><span data-stu-id="5e656-139">The following example sets the container's permissions to full public read access.</span></span> <span data-ttu-id="5e656-140">若只要將 Blob 的權限設為公用讀取權限，請將 **PublicAccess** 屬性設為 **BlobContainerPublicAccessType.Blob**。</span><span class="sxs-lookup"><span data-stu-id="5e656-140">To set permissions to public read access for blobs only, set the **PublicAccess** property to **BlobContainerPublicAccessType.Blob**.</span></span> <span data-ttu-id="5e656-141">若要移除匿名使用者的所有權限，請將屬性設為 **BlobContainerPublicAccessType.Off**。</span><span class="sxs-lookup"><span data-stu-id="5e656-141">To remove all permissions for anonymous users, set the property to **BlobContainerPublicAccessType.Off**.</span></span>

```csharp
public static void SetPublicContainerPermissions(CloudBlobContainer container)
{
    BlobContainerPermissions permissions = container.GetPermissions();
    permissions.PublicAccess = BlobContainerPublicAccessType.Container;
    container.SetPermissions(permissions);
}
```

## <a name="access-containers-and-blobs-anonymously"></a><span data-ttu-id="5e656-142">匿名存取容器與 Blob</span><span class="sxs-lookup"><span data-stu-id="5e656-142">Access containers and blobs anonymously</span></span>
<span data-ttu-id="5e656-143">匿名存取容器與 Blob 的用戶端可使用不需要認證的建構函式。</span><span class="sxs-lookup"><span data-stu-id="5e656-143">A client that accesses containers and blobs anonymously can use constructors that do not require credentials.</span></span> <span data-ttu-id="5e656-144">以下範例顯示可匿名參考 Blob 服務資源的不同方法。</span><span class="sxs-lookup"><span data-stu-id="5e656-144">The following examples show a few different ways to reference Blob service resources anonymously.</span></span>

### <a name="create-an-anonymous-client-object"></a><span data-ttu-id="5e656-145">建立匿名用戶端物件</span><span class="sxs-lookup"><span data-stu-id="5e656-145">Create an anonymous client object</span></span>
<span data-ttu-id="5e656-146">您可以為帳戶提供 Blob 服務端點，來建立用於匿名存取的新服務用戶端物件。</span><span class="sxs-lookup"><span data-stu-id="5e656-146">You can create a new service client object for anonymous access by providing the Blob service endpoint for the account.</span></span> <span data-ttu-id="5e656-147">不同，您也必須知道可供匿名存取的帳戶中的容器名稱。</span><span class="sxs-lookup"><span data-stu-id="5e656-147">However, you must also know the name of a container in that account that's available for anonymous access.</span></span>

```csharp
public static void CreateAnonymousBlobClient()
{
    // Create the client object using the Blob service endpoint.
    CloudBlobClient blobClient = new CloudBlobClient(new Uri(@"https://storagesample.blob.core.windows.net"));

    // Get a reference to a container that's available for anonymous access.
    CloudBlobContainer container = blobClient.GetContainerReference("sample-container");

    // Read the container's properties. Note this is only possible when the container supports full public read access.
    container.FetchAttributes();
    Console.WriteLine(container.Properties.LastModified);
    Console.WriteLine(container.Properties.ETag);
}
```

### <a name="reference-a-container-anonymously"></a><span data-ttu-id="5e656-148">匿名參考容器</span><span class="sxs-lookup"><span data-stu-id="5e656-148">Reference a container anonymously</span></span>
<span data-ttu-id="5e656-149">如果您有可供匿名使用之容器的 URL，您可以使用該 URL 直接參考容器。</span><span class="sxs-lookup"><span data-stu-id="5e656-149">If you have the URL to a container that is anonymously available, you can use it to reference the container directly.</span></span>

```csharp
public static void ListBlobsAnonymously()
{
    // Get a reference to a container that's available for anonymous access.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(@"https://storagesample.blob.core.windows.net/sample-container"));

    // List blobs in the container.
    foreach (IListBlobItem blobItem in container.ListBlobs())
    {
        Console.WriteLine(blobItem.Uri);
    }
}
```

### <a name="reference-a-blob-anonymously"></a><span data-ttu-id="5e656-150">匿名參考 Blob</span><span class="sxs-lookup"><span data-stu-id="5e656-150">Reference a blob anonymously</span></span>
<span data-ttu-id="5e656-151">如果您有可供匿名存取之 Blob 的 URL，您可以使用該 URL 直接參考 Blob：</span><span class="sxs-lookup"><span data-stu-id="5e656-151">If you have the URL to a blob that is available for anonymous access, you can reference the blob directly using that URL:</span></span>

```csharp
public static void DownloadBlobAnonymously()
{
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(@"https://storagesample.blob.core.windows.net/sample-container/logfile.txt"));
    blob.DownloadToFile(@"C:\Temp\logfile.txt", System.IO.FileMode.Create);
}
```

## <a name="features-available-to-anonymous-users"></a><span data-ttu-id="5e656-152">匿名使用者可使用的功能</span><span class="sxs-lookup"><span data-stu-id="5e656-152">Features available to anonymous users</span></span>
<span data-ttu-id="5e656-153">下表顯示當容器的 ACL 設為允許公用存取時，匿名使用者可能會呼叫哪些作業。</span><span class="sxs-lookup"><span data-stu-id="5e656-153">The following table shows which operations may be called by anonymous users when a container's ACL is set to allow public access.</span></span>

| <span data-ttu-id="5e656-154">REST 作業</span><span class="sxs-lookup"><span data-stu-id="5e656-154">REST Operation</span></span> | <span data-ttu-id="5e656-155">具有完整公開讀取權限</span><span class="sxs-lookup"><span data-stu-id="5e656-155">Permission with full public read access</span></span> | <span data-ttu-id="5e656-156">僅對 Blob 有公開讀取權限</span><span class="sxs-lookup"><span data-stu-id="5e656-156">Permission with public read access for blobs only</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5e656-157">列出容器</span><span class="sxs-lookup"><span data-stu-id="5e656-157">List Containers</span></span> |<span data-ttu-id="5e656-158">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="5e656-158">Owner only</span></span> |<span data-ttu-id="5e656-159">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="5e656-159">Owner only</span></span> |
| <span data-ttu-id="5e656-160">建立容器</span><span class="sxs-lookup"><span data-stu-id="5e656-160">Create Container</span></span> |<span data-ttu-id="5e656-161">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="5e656-161">Owner only</span></span> |<span data-ttu-id="5e656-162">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="5e656-162">Owner only</span></span> |
| <span data-ttu-id="5e656-163">取得容器屬性</span><span class="sxs-lookup"><span data-stu-id="5e656-163">Get Container Properties</span></span> |<span data-ttu-id="5e656-164">全部</span><span class="sxs-lookup"><span data-stu-id="5e656-164">All</span></span> |<span data-ttu-id="5e656-165">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="5e656-165">Owner only</span></span> |
| <span data-ttu-id="5e656-166">取得容器中繼資料</span><span class="sxs-lookup"><span data-stu-id="5e656-166">Get Container Metadata</span></span> |<span data-ttu-id="5e656-167">全部</span><span class="sxs-lookup"><span data-stu-id="5e656-167">All</span></span> |<span data-ttu-id="5e656-168">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="5e656-168">Owner only</span></span> |
| <span data-ttu-id="5e656-169">設定容器中繼資料</span><span class="sxs-lookup"><span data-stu-id="5e656-169">Set Container Metadata</span></span> |<span data-ttu-id="5e656-170">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="5e656-170">Owner only</span></span> |<span data-ttu-id="5e656-171">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="5e656-171">Owner only</span></span> |
| <span data-ttu-id="5e656-172">取得容器 ACL</span><span class="sxs-lookup"><span data-stu-id="5e656-172">Get Container ACL</span></span> |<span data-ttu-id="5e656-173">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="5e656-173">Owner only</span></span> |<span data-ttu-id="5e656-174">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="5e656-174">Owner only</span></span> |
| <span data-ttu-id="5e656-175">設定容器 ACL</span><span class="sxs-lookup"><span data-stu-id="5e656-175">Set Container ACL</span></span> |<span data-ttu-id="5e656-176">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="5e656-176">Owner only</span></span> |<span data-ttu-id="5e656-177">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="5e656-177">Owner only</span></span> |
| <span data-ttu-id="5e656-178">刪除容器</span><span class="sxs-lookup"><span data-stu-id="5e656-178">Delete Container</span></span> |<span data-ttu-id="5e656-179">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="5e656-179">Owner only</span></span> |<span data-ttu-id="5e656-180">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="5e656-180">Owner only</span></span> |
| <span data-ttu-id="5e656-181">列出 Blob</span><span class="sxs-lookup"><span data-stu-id="5e656-181">List Blobs</span></span> |<span data-ttu-id="5e656-182">全部</span><span class="sxs-lookup"><span data-stu-id="5e656-182">All</span></span> |<span data-ttu-id="5e656-183">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="5e656-183">Owner only</span></span> |
| <span data-ttu-id="5e656-184">放置 Blob</span><span class="sxs-lookup"><span data-stu-id="5e656-184">Put Blob</span></span> |<span data-ttu-id="5e656-185">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="5e656-185">Owner only</span></span> |<span data-ttu-id="5e656-186">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="5e656-186">Owner only</span></span> |
| <span data-ttu-id="5e656-187">取得 Blob</span><span class="sxs-lookup"><span data-stu-id="5e656-187">Get Blob</span></span> |<span data-ttu-id="5e656-188">全部</span><span class="sxs-lookup"><span data-stu-id="5e656-188">All</span></span> |<span data-ttu-id="5e656-189">全部</span><span class="sxs-lookup"><span data-stu-id="5e656-189">All</span></span> |
| <span data-ttu-id="5e656-190">取得 Blob 屬性</span><span class="sxs-lookup"><span data-stu-id="5e656-190">Get Blob Properties</span></span> |<span data-ttu-id="5e656-191">全部</span><span class="sxs-lookup"><span data-stu-id="5e656-191">All</span></span> |<span data-ttu-id="5e656-192">全部</span><span class="sxs-lookup"><span data-stu-id="5e656-192">All</span></span> |
| <span data-ttu-id="5e656-193">設定 Blob 屬性</span><span class="sxs-lookup"><span data-stu-id="5e656-193">Set Blob Properties</span></span> |<span data-ttu-id="5e656-194">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="5e656-194">Owner only</span></span> |<span data-ttu-id="5e656-195">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="5e656-195">Owner only</span></span> |
| <span data-ttu-id="5e656-196">取得 Blob 中繼資料</span><span class="sxs-lookup"><span data-stu-id="5e656-196">Get Blob Metadata</span></span> |<span data-ttu-id="5e656-197">全部</span><span class="sxs-lookup"><span data-stu-id="5e656-197">All</span></span> |<span data-ttu-id="5e656-198">全部</span><span class="sxs-lookup"><span data-stu-id="5e656-198">All</span></span> |
| <span data-ttu-id="5e656-199">設定 Blob 中繼資料</span><span class="sxs-lookup"><span data-stu-id="5e656-199">Set Blob Metadata</span></span> |<span data-ttu-id="5e656-200">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="5e656-200">Owner only</span></span> |<span data-ttu-id="5e656-201">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="5e656-201">Owner only</span></span> |
| <span data-ttu-id="5e656-202">放置區塊</span><span class="sxs-lookup"><span data-stu-id="5e656-202">Put Block</span></span> |<span data-ttu-id="5e656-203">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="5e656-203">Owner only</span></span> |<span data-ttu-id="5e656-204">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="5e656-204">Owner only</span></span> |
| <span data-ttu-id="5e656-205">取得區塊清單 (僅限認可區塊)</span><span class="sxs-lookup"><span data-stu-id="5e656-205">Get Block List (committed blocks only)</span></span> |<span data-ttu-id="5e656-206">全部</span><span class="sxs-lookup"><span data-stu-id="5e656-206">All</span></span> |<span data-ttu-id="5e656-207">全部</span><span class="sxs-lookup"><span data-stu-id="5e656-207">All</span></span> |
| <span data-ttu-id="5e656-208">取得區塊清單 (僅限未認可的區塊或所有區塊)</span><span class="sxs-lookup"><span data-stu-id="5e656-208">Get Block List (uncommitted blocks only or all blocks)</span></span> |<span data-ttu-id="5e656-209">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="5e656-209">Owner only</span></span> |<span data-ttu-id="5e656-210">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="5e656-210">Owner only</span></span> |
| <span data-ttu-id="5e656-211">放置區塊清單</span><span class="sxs-lookup"><span data-stu-id="5e656-211">Put Block List</span></span> |<span data-ttu-id="5e656-212">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="5e656-212">Owner only</span></span> |<span data-ttu-id="5e656-213">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="5e656-213">Owner only</span></span> |
| <span data-ttu-id="5e656-214">刪除 Blob</span><span class="sxs-lookup"><span data-stu-id="5e656-214">Delete Blob</span></span> |<span data-ttu-id="5e656-215">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="5e656-215">Owner only</span></span> |<span data-ttu-id="5e656-216">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="5e656-216">Owner only</span></span> |
| <span data-ttu-id="5e656-217">複製 Blob</span><span class="sxs-lookup"><span data-stu-id="5e656-217">Copy Blob</span></span> |<span data-ttu-id="5e656-218">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="5e656-218">Owner only</span></span> |<span data-ttu-id="5e656-219">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="5e656-219">Owner only</span></span> |
| <span data-ttu-id="5e656-220">快照 Blob</span><span class="sxs-lookup"><span data-stu-id="5e656-220">Snapshot Blob</span></span> |<span data-ttu-id="5e656-221">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="5e656-221">Owner only</span></span> |<span data-ttu-id="5e656-222">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="5e656-222">Owner only</span></span> |
| <span data-ttu-id="5e656-223">租用 Blob</span><span class="sxs-lookup"><span data-stu-id="5e656-223">Lease Blob</span></span> |<span data-ttu-id="5e656-224">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="5e656-224">Owner only</span></span> |<span data-ttu-id="5e656-225">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="5e656-225">Owner only</span></span> |
| <span data-ttu-id="5e656-226">放置頁面</span><span class="sxs-lookup"><span data-stu-id="5e656-226">Put Page</span></span> |<span data-ttu-id="5e656-227">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="5e656-227">Owner only</span></span> |<span data-ttu-id="5e656-228">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="5e656-228">Owner only</span></span> |
| <span data-ttu-id="5e656-229">取得頁面範圍</span><span class="sxs-lookup"><span data-stu-id="5e656-229">Get Page Ranges</span></span> |<span data-ttu-id="5e656-230">全部</span><span class="sxs-lookup"><span data-stu-id="5e656-230">All</span></span> |<span data-ttu-id="5e656-231">全部</span><span class="sxs-lookup"><span data-stu-id="5e656-231">All</span></span> |
| <span data-ttu-id="5e656-232">附加 Blob</span><span class="sxs-lookup"><span data-stu-id="5e656-232">Append Blob</span></span> |<span data-ttu-id="5e656-233">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="5e656-233">Owner only</span></span> |<span data-ttu-id="5e656-234">只有擁有者</span><span class="sxs-lookup"><span data-stu-id="5e656-234">Owner only</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5e656-235">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5e656-235">Next steps</span></span>

* [<span data-ttu-id="5e656-236">Azure 儲存體服務的驗證</span><span class="sxs-lookup"><span data-stu-id="5e656-236">Authentication for the Azure Storage Services</span></span>](https://msdn.microsoft.com/library/azure/dd179428.aspx)
* [<span data-ttu-id="5e656-237">使用共用存取簽章 (SAS)</span><span class="sxs-lookup"><span data-stu-id="5e656-237">Using Shared Access Signatures (SAS)</span></span>](storage-dotnet-shared-access-signature-part-1.md)
* [<span data-ttu-id="5e656-238">使用共用存取簽章來委派存取權</span><span class="sxs-lookup"><span data-stu-id="5e656-238">Delegating Access with a Shared Access Signature</span></span>](https://msdn.microsoft.com/library/azure/ee395415.aspx)
