---
title: "在 Azure 儲存體中設定和擷取物件屬性與中繼資料 | Microsoft Docs"
description: "將物件的自訂中繼資料儲存在Azure 儲存體中，並設定和擷取系統屬性。"
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 036f9006-273e-400b-844b-3329045e9e1f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: marsma
ms.openlocfilehash: 6af66607478c58874f00bcf017a35abfc37888df
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="set-and-retrieve-properties-and-metadata"></a><span data-ttu-id="77910-103">設定並擷取屬性和中繼資料</span><span class="sxs-lookup"><span data-stu-id="77910-103">Set and retrieve properties and metadata</span></span>

<span data-ttu-id="77910-104">除了所包含之資料外，在 Azure 儲存體支援系統屬性和使用者定義中繼資料中的物件。</span><span class="sxs-lookup"><span data-stu-id="77910-104">Objects in Azure Storage support system properties and user-defined metadata, in addition to the data they contain.</span></span> <span data-ttu-id="77910-105">本文討論如何使用[適用於 .NET 的 Azure 儲存體用戶端程式庫](https://www.nuget.org/packages/WindowsAzure.Storage/)來管理系統屬性和使用者定義的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="77910-105">This article discusses managing system properties and user-defined metadata with the [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span>

* <span data-ttu-id="77910-106">**系統屬性**：系統屬性存在於每個儲存體資源上。</span><span class="sxs-lookup"><span data-stu-id="77910-106">**System properties**: System properties exist on each storage resource.</span></span> <span data-ttu-id="77910-107">其中有些系統屬性可以讀取或設定，有些則是唯讀的。</span><span class="sxs-lookup"><span data-stu-id="77910-107">Some of them can be read or set, while others are read-only.</span></span> <span data-ttu-id="77910-108">實際上，有些系統屬性會對應至特定的標準 HTTP 標頭。</span><span class="sxs-lookup"><span data-stu-id="77910-108">Under the covers, some system properties correspond to certain standard HTTP headers.</span></span> <span data-ttu-id="77910-109">Azure 儲存體用戶端程式庫會為您維護這些 HTTP 標頭。</span><span class="sxs-lookup"><span data-stu-id="77910-109">The Azure storage client library maintains these for you.</span></span>

* <span data-ttu-id="77910-110">**使用者定義的中繼資料**：使用者定義的中繼資料是您針對給定的資源，以名稱/值組的形式指定的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="77910-110">**User-defined metadata**: User-defined metadata is metadata that you specify on a given resource in the form of a name-value pair.</span></span> <span data-ttu-id="77910-111">您可以使用中繼資料來儲存儲存體資源的額外值。</span><span class="sxs-lookup"><span data-stu-id="77910-111">You can use metadata to store additional values with a storage resource.</span></span> <span data-ttu-id="77910-112">這些額外的中繼資料值僅供您自己使用，並不會影響資源的運作方式。</span><span class="sxs-lookup"><span data-stu-id="77910-112">These additional metadata values are for your own purposes only, and do not affect how the resource behaves.</span></span>

<span data-ttu-id="77910-113">擷取儲存體資源的屬性和中繼資料值是一個兩步驟程序。</span><span class="sxs-lookup"><span data-stu-id="77910-113">Retrieving property and metadata values for a storage resource is a two-step process.</span></span> <span data-ttu-id="77910-114">您必須先呼叫 **FetchAttributes** 方法明確地擷取這些值，才能開始讀取這些值。</span><span class="sxs-lookup"><span data-stu-id="77910-114">Before you can read these values, you must explicitly fetch them by calling the **FetchAttributes** method.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="77910-115">除非您呼叫其中一個 **FetchAttributes** 方法，否則無法填入儲存體資源的屬性和中繼資料值。</span><span class="sxs-lookup"><span data-stu-id="77910-115">Property and metadata values for a storage resource are not populated unless you call one of the **FetchAttributes** methods.</span></span>
>
> <span data-ttu-id="77910-116">如果任何名稱/值組包含非 ASCII 字元，您會收到 `400 Bad Request`。</span><span class="sxs-lookup"><span data-stu-id="77910-116">You will receive a `400 Bad Request` if any name/value pairs contain non-ASCII characters.</span></span> <span data-ttu-id="77910-117">中繼資料名稱/值組是有效的 HTTP 標頭，所以必須遵守控管 HTTP 標頭的所有限制。</span><span class="sxs-lookup"><span data-stu-id="77910-117">Metadata name/value pairs are valid HTTP headers, and so must adhere to all restrictions governing HTTP headers.</span></span> <span data-ttu-id="77910-118">因此，如果名稱和值包含非 ASCII 字元，建議您使用 URL 編碼或 Base64 編碼。</span><span class="sxs-lookup"><span data-stu-id="77910-118">It is therefore recommended that you use URL encoding or Base64 encoding for names and values containing non-ASCII characters.</span></span>
>

## <a name="setting-and-retrieving-properties"></a><span data-ttu-id="77910-119">設定與擷取屬性</span><span class="sxs-lookup"><span data-stu-id="77910-119">Setting and retrieving properties</span></span>
<span data-ttu-id="77910-120">若要擷取屬性值，請呼叫 Blob 或容器上的 **FetchAttributes** 方法，以填入屬性，然後讀取這些值。</span><span class="sxs-lookup"><span data-stu-id="77910-120">To retrieve property values, call the **FetchAttributes** method on your blob or container to populate the properties, then read the values.</span></span>

<span data-ttu-id="77910-121">若要設定物件的屬性，請指定屬性值，然後呼叫 **SetProperties** 方法。</span><span class="sxs-lookup"><span data-stu-id="77910-121">To set properties on an object, specify the property value, then call the **SetProperties** method.</span></span>

<span data-ttu-id="77910-122">下列程式碼範例會建立一個容器，然後將其部分屬性值寫入主控台視窗。</span><span class="sxs-lookup"><span data-stu-id="77910-122">The following code example creates a container, then writes some of its property values to a console window.</span></span>

```csharp
//Parse the connection string for the storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

//Create the service client object for credentialed access to the Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference to a container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create the container if it does not already exist.
container.CreateIfNotExists();

// Fetch container properties and write out their values.
container.FetchAttributes();
Console.WriteLine("Properties for container {0}", container.StorageUri.PrimaryUri.ToString());
Console.WriteLine("LastModifiedUTC: {0}", container.Properties.LastModified.ToString());
Console.WriteLine("ETag: {0}", container.Properties.ETag);
Console.WriteLine();
```

## <a name="setting-and-retrieving-metadata"></a><span data-ttu-id="77910-123">設定與擷取中繼資料</span><span class="sxs-lookup"><span data-stu-id="77910-123">Setting and retrieving metadata</span></span>
<span data-ttu-id="77910-124">您可以針對 Blob 或容器資源，將中繼資料指定為一個或多個名稱/值組。</span><span class="sxs-lookup"><span data-stu-id="77910-124">You can specify metadata as one or more name-value pairs on a blob or container resource.</span></span> <span data-ttu-id="77910-125">若要設定中繼資料，將名稱/值組加入至資源的**中繼資料**集合，然後呼叫 **SetMetadata** 方法，將這些值儲存至服務。</span><span class="sxs-lookup"><span data-stu-id="77910-125">To set metadata, add name-value pairs to the **Metadata** collection on the resource, then call the **SetMetadata** method to save the values to the service.</span></span>

> [!NOTE]
> <span data-ttu-id="77910-126">您的中繼資料名稱必須符合 C# 識別碼的命名慣例。</span><span class="sxs-lookup"><span data-stu-id="77910-126">The name of your metadata must conform to the naming conventions for C# identifiers.</span></span>
>
>

<span data-ttu-id="77910-127">下列程式碼範例會在容器上設定中繼資料。</span><span class="sxs-lookup"><span data-stu-id="77910-127">The following code example sets metadata on a container.</span></span> <span data-ttu-id="77910-128">其中一個值是使用集合的 **Add** 方法設定。</span><span class="sxs-lookup"><span data-stu-id="77910-128">One value is set using the collection's **Add** method.</span></span> <span data-ttu-id="77910-129">其他值是使用隱含的索引鍵/值語法來設定。</span><span class="sxs-lookup"><span data-stu-id="77910-129">The other value is set using implicit key/value syntax.</span></span> <span data-ttu-id="77910-130">兩者都有效。</span><span class="sxs-lookup"><span data-stu-id="77910-130">Both are valid.</span></span>

```csharp
public static void AddContainerMetadata(CloudBlobContainer container)
{
    //Add some metadata to the container.
    container.Metadata.Add("docType", "textDocuments");
    container.Metadata["category"] = "guidance";

    //Set the container's metadata.
    container.SetMetadata();
}
```

<span data-ttu-id="77910-131">若要擷取 Blob 或容器的中繼資料，請呼叫 **FetchAttributes** 方法以填入 **Metadata** 集合，然後讀取這些值，如以下範例所示。</span><span class="sxs-lookup"><span data-stu-id="77910-131">To retrieve metadata, call the **FetchAttributes** method on your blob or container to populate the **Metadata** collection, then read the values, as shown in the example below.</span></span>

```csharp
public static void ListContainerMetadata(CloudBlobContainer container)
{
    //Fetch container attributes in order to populate the container's properties and metadata.
    container.FetchAttributes();

    //Enumerate the container's metadata.
    Console.WriteLine("Container metadata:");
    foreach (var metadataItem in container.Metadata)
    {
        Console.WriteLine("\tKey: {0}", metadataItem.Key);
        Console.WriteLine("\tValue: {0}", metadataItem.Value);
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="77910-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="77910-132">Next steps</span></span>
* [<span data-ttu-id="77910-133">適用於 .NET 的 Azure 儲存體用戶端程式庫參考資料</span><span class="sxs-lookup"><span data-stu-id="77910-133">Azure Storage Client Library for .NET reference</span></span>](/dotnet/api/?term=Microsoft.WindowsAzure.Storage)
* [<span data-ttu-id="77910-134">適用於 .NET NuGet 套件的 Azure 儲存體用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="77910-134">Azure Storage Client Library for .NET NuGet package</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
