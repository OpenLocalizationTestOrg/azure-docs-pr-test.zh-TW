---
title: "aaaSet 並擷取物件屬性和中繼資料在 Azure 儲存體 |Microsoft 文件"
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
ms.openlocfilehash: 44f9243183014845964f337b476a6b0069dc0902
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-and-retrieve-properties-and-metadata"></a><span data-ttu-id="c371b-103">設定並擷取屬性和中繼資料</span><span class="sxs-lookup"><span data-stu-id="c371b-103">Set and retrieve properties and metadata</span></span>

<span data-ttu-id="c371b-104">物件在 Azure 儲存體支援系統屬性和使用者定義的中繼資料，此外 toohello 它們包含的資料。</span><span class="sxs-lookup"><span data-stu-id="c371b-104">Objects in Azure Storage support system properties and user-defined metadata, in addition toohello data they contain.</span></span> <span data-ttu-id="c371b-105">本文將告訴您管理的系統屬性和使用者定義中繼資料的 hello[適用於.NET 的 Azure 儲存體用戶端程式庫](https://www.nuget.org/packages/WindowsAzure.Storage/)。</span><span class="sxs-lookup"><span data-stu-id="c371b-105">This article discusses managing system properties and user-defined metadata with hello [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span>

* <span data-ttu-id="c371b-106">**系統屬性**：系統屬性存在於每個儲存體資源上。</span><span class="sxs-lookup"><span data-stu-id="c371b-106">**System properties**: System properties exist on each storage resource.</span></span> <span data-ttu-id="c371b-107">其中有些系統屬性可以讀取或設定，有些則是唯讀的。</span><span class="sxs-lookup"><span data-stu-id="c371b-107">Some of them can be read or set, while others are read-only.</span></span> <span data-ttu-id="c371b-108">Hello 幕後有些系統屬性會對應 toocertain 標準 HTTP 標頭。</span><span class="sxs-lookup"><span data-stu-id="c371b-108">Under hello covers, some system properties correspond toocertain standard HTTP headers.</span></span> <span data-ttu-id="c371b-109">hello Azure 儲存體用戶端程式庫會維護這些項。</span><span class="sxs-lookup"><span data-stu-id="c371b-109">hello Azure storage client library maintains these for you.</span></span>

* <span data-ttu-id="c371b-110">**使用者定義的中繼資料**： 使用者定義的中繼資料是您指定的名稱 / 值組的 hello 表單中的指定資源的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="c371b-110">**User-defined metadata**: User-defined metadata is metadata that you specify on a given resource in hello form of a name-value pair.</span></span> <span data-ttu-id="c371b-111">您可以使用儲存體資源的中繼資料 toostore 額外的值。</span><span class="sxs-lookup"><span data-stu-id="c371b-111">You can use metadata toostore additional values with a storage resource.</span></span> <span data-ttu-id="c371b-112">這些額外的中繼資料值對於您自己的目的而言，並不會影響 hello 資源的行為方式。</span><span class="sxs-lookup"><span data-stu-id="c371b-112">These additional metadata values are for your own purposes only, and do not affect how hello resource behaves.</span></span>

<span data-ttu-id="c371b-113">擷取儲存體資源的屬性和中繼資料值是一個兩步驟程序。</span><span class="sxs-lookup"><span data-stu-id="c371b-113">Retrieving property and metadata values for a storage resource is a two-step process.</span></span> <span data-ttu-id="c371b-114">您可以讀取這些值之前，您必須明確地擷取它們所呼叫的 hello **FetchAttributes**方法。</span><span class="sxs-lookup"><span data-stu-id="c371b-114">Before you can read these values, you must explicitly fetch them by calling hello **FetchAttributes** method.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c371b-115">除非您呼叫其中一個 hello 儲存體資源的屬性和中繼資料值未填入**FetchAttributes**方法。</span><span class="sxs-lookup"><span data-stu-id="c371b-115">Property and metadata values for a storage resource are not populated unless you call one of hello **FetchAttributes** methods.</span></span>
>
> <span data-ttu-id="c371b-116">如果任何名稱/值組包含非 ASCII 字元，您會收到 `400 Bad Request`。</span><span class="sxs-lookup"><span data-stu-id="c371b-116">You will receive a `400 Bad Request` if any name/value pairs contain non-ASCII characters.</span></span> <span data-ttu-id="c371b-117">中繼資料名稱/值組都是有效的 HTTP 標頭，因此必須遵守 tooall 控管 HTTP 標頭的限制。</span><span class="sxs-lookup"><span data-stu-id="c371b-117">Metadata name/value pairs are valid HTTP headers, and so must adhere tooall restrictions governing HTTP headers.</span></span> <span data-ttu-id="c371b-118">因此，如果名稱和值包含非 ASCII 字元，建議您使用 URL 編碼或 Base64 編碼。</span><span class="sxs-lookup"><span data-stu-id="c371b-118">It is therefore recommended that you use URL encoding or Base64 encoding for names and values containing non-ASCII characters.</span></span>
>

## <a name="setting-and-retrieving-properties"></a><span data-ttu-id="c371b-119">設定與擷取屬性</span><span class="sxs-lookup"><span data-stu-id="c371b-119">Setting and retrieving properties</span></span>
<span data-ttu-id="c371b-120">tooretrieve 屬性值，呼叫 hello **FetchAttributes**方法上您 blob 或容器 toopopulate hello 屬性，然後讀取 hello 值。</span><span class="sxs-lookup"><span data-stu-id="c371b-120">tooretrieve property values, call hello **FetchAttributes** method on your blob or container toopopulate hello properties, then read hello values.</span></span>

<span data-ttu-id="c371b-121">tooset 屬性物件上的指定 hello 屬性值，然後呼叫 hello **SetProperties**方法。</span><span class="sxs-lookup"><span data-stu-id="c371b-121">tooset properties on an object, specify hello property value, then call hello **SetProperties** method.</span></span>

<span data-ttu-id="c371b-122">hello 下列程式碼範例會建立容器，然後再將其屬性值 tooa 主控台視窗的部分。</span><span class="sxs-lookup"><span data-stu-id="c371b-122">hello following code example creates a container, then writes some of its property values tooa console window.</span></span>

```csharp
//Parse hello connection string for hello storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

//Create hello service client object for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create hello container if it does not already exist.
container.CreateIfNotExists();

// Fetch container properties and write out their values.
container.FetchAttributes();
Console.WriteLine("Properties for container {0}", container.StorageUri.PrimaryUri.ToString());
Console.WriteLine("LastModifiedUTC: {0}", container.Properties.LastModified.ToString());
Console.WriteLine("ETag: {0}", container.Properties.ETag);
Console.WriteLine();
```

## <a name="setting-and-retrieving-metadata"></a><span data-ttu-id="c371b-123">設定與擷取中繼資料</span><span class="sxs-lookup"><span data-stu-id="c371b-123">Setting and retrieving metadata</span></span>
<span data-ttu-id="c371b-124">您可以針對 Blob 或容器資源，將中繼資料指定為一個或多個名稱/值組。</span><span class="sxs-lookup"><span data-stu-id="c371b-124">You can specify metadata as one or more name-value pairs on a blob or container resource.</span></span> <span data-ttu-id="c371b-125">tooset 中繼資料，將名稱 / 值組 toohello**中繼資料**hello 資源上的集合，然後呼叫 hello **SetMetadata**方法 toosave hello 值 toohello 服務。</span><span class="sxs-lookup"><span data-stu-id="c371b-125">tooset metadata, add name-value pairs toohello **Metadata** collection on hello resource, then call hello **SetMetadata** method toosave hello values toohello service.</span></span>

> [!NOTE]
> <span data-ttu-id="c371b-126">hello 中繼資料名稱必須符合 toohello C# 識別碼的命名慣例。</span><span class="sxs-lookup"><span data-stu-id="c371b-126">hello name of your metadata must conform toohello naming conventions for C# identifiers.</span></span>
>
>

<span data-ttu-id="c371b-127">hello 下列程式碼範例會設定中繼資料在容器上。</span><span class="sxs-lookup"><span data-stu-id="c371b-127">hello following code example sets metadata on a container.</span></span> <span data-ttu-id="c371b-128">一個值會設定使用 hello 集合**新增**方法。</span><span class="sxs-lookup"><span data-stu-id="c371b-128">One value is set using hello collection's **Add** method.</span></span> <span data-ttu-id="c371b-129">hello 其他值會設定使用隱含索引鍵/值的語法。</span><span class="sxs-lookup"><span data-stu-id="c371b-129">hello other value is set using implicit key/value syntax.</span></span> <span data-ttu-id="c371b-130">兩者都有效。</span><span class="sxs-lookup"><span data-stu-id="c371b-130">Both are valid.</span></span>

```csharp
public static void AddContainerMetadata(CloudBlobContainer container)
{
    //Add some metadata toohello container.
    container.Metadata.Add("docType", "textDocuments");
    container.Metadata["category"] = "guidance";

    //Set hello container's metadata.
    container.SetMetadata();
}
```

<span data-ttu-id="c371b-131">tooretrieve 中繼資料，呼叫 hello **FetchAttributes**方法在您的 blob 或容器 toopopulate hello**中繼資料**集合，然後讀取 hello 值 hello 下面範例所示。</span><span class="sxs-lookup"><span data-stu-id="c371b-131">tooretrieve metadata, call hello **FetchAttributes** method on your blob or container toopopulate hello **Metadata** collection, then read hello values, as shown in hello example below.</span></span>

```csharp
public static void ListContainerMetadata(CloudBlobContainer container)
{
    //Fetch container attributes in order toopopulate hello container's properties and metadata.
    container.FetchAttributes();

    //Enumerate hello container's metadata.
    Console.WriteLine("Container metadata:");
    foreach (var metadataItem in container.Metadata)
    {
        Console.WriteLine("\tKey: {0}", metadataItem.Key);
        Console.WriteLine("\tValue: {0}", metadataItem.Value);
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="c371b-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c371b-132">Next steps</span></span>
* [<span data-ttu-id="c371b-133">適用於 .NET 的 Azure 儲存體用戶端程式庫參考資料</span><span class="sxs-lookup"><span data-stu-id="c371b-133">Azure Storage Client Library for .NET reference</span></span>](/dotnet/api/?term=Microsoft.WindowsAzure.Storage)
* [<span data-ttu-id="c371b-134">適用於 .NET NuGet 套件的 Azure 儲存體用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="c371b-134">Azure Storage Client Library for .NET NuGet package</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
