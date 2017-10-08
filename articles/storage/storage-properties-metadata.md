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
# <a name="set-and-retrieve-properties-and-metadata"></a>設定並擷取屬性和中繼資料

物件在 Azure 儲存體支援系統屬性和使用者定義的中繼資料，此外 toohello 它們包含的資料。 本文將告訴您管理的系統屬性和使用者定義中繼資料的 hello[適用於.NET 的 Azure 儲存體用戶端程式庫](https://www.nuget.org/packages/WindowsAzure.Storage/)。

* **系統屬性**：系統屬性存在於每個儲存體資源上。 其中有些系統屬性可以讀取或設定，有些則是唯讀的。 Hello 幕後有些系統屬性會對應 toocertain 標準 HTTP 標頭。 hello Azure 儲存體用戶端程式庫會維護這些項。

* **使用者定義的中繼資料**： 使用者定義的中繼資料是您指定的名稱 / 值組的 hello 表單中的指定資源的中繼資料。 您可以使用儲存體資源的中繼資料 toostore 額外的值。 這些額外的中繼資料值對於您自己的目的而言，並不會影響 hello 資源的行為方式。

擷取儲存體資源的屬性和中繼資料值是一個兩步驟程序。 您可以讀取這些值之前，您必須明確地擷取它們所呼叫的 hello **FetchAttributes**方法。

> [!IMPORTANT]
> 除非您呼叫其中一個 hello 儲存體資源的屬性和中繼資料值未填入**FetchAttributes**方法。
>
> 如果任何名稱/值組包含非 ASCII 字元，您會收到 `400 Bad Request`。 中繼資料名稱/值組都是有效的 HTTP 標頭，因此必須遵守 tooall 控管 HTTP 標頭的限制。 因此，如果名稱和值包含非 ASCII 字元，建議您使用 URL 編碼或 Base64 編碼。
>

## <a name="setting-and-retrieving-properties"></a>設定與擷取屬性
tooretrieve 屬性值，呼叫 hello **FetchAttributes**方法上您 blob 或容器 toopopulate hello 屬性，然後讀取 hello 值。

tooset 屬性物件上的指定 hello 屬性值，然後呼叫 hello **SetProperties**方法。

hello 下列程式碼範例會建立容器，然後再將其屬性值 tooa 主控台視窗的部分。

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

## <a name="setting-and-retrieving-metadata"></a>設定與擷取中繼資料
您可以針對 Blob 或容器資源，將中繼資料指定為一個或多個名稱/值組。 tooset 中繼資料，將名稱 / 值組 toohello**中繼資料**hello 資源上的集合，然後呼叫 hello **SetMetadata**方法 toosave hello 值 toohello 服務。

> [!NOTE]
> hello 中繼資料名稱必須符合 toohello C# 識別碼的命名慣例。
>
>

hello 下列程式碼範例會設定中繼資料在容器上。 一個值會設定使用 hello 集合**新增**方法。 hello 其他值會設定使用隱含索引鍵/值的語法。 兩者都有效。

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

tooretrieve 中繼資料，呼叫 hello **FetchAttributes**方法在您的 blob 或容器 toopopulate hello**中繼資料**集合，然後讀取 hello 值 hello 下面範例所示。

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

## <a name="next-steps"></a>後續步驟
* [適用於 .NET 的 Azure 儲存體用戶端程式庫參考資料](/dotnet/api/?term=Microsoft.WindowsAzure.Storage)
* [適用於 .NET NuGet 套件的 Azure 儲存體用戶端程式庫](https://www.nuget.org/packages/WindowsAzure.Storage/)
