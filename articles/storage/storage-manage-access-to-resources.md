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
# <a name="manage-anonymous-read-access-toocontainers-and-blobs"></a>管理匿名讀取權限 toocontainers 和 blob
您可以啟用匿名、 公用讀取權限 tooa 容器和其在 Azure Blob 儲存體的 blob。 如此一來，您可以授與唯讀存取 toothese 資源共用您的帳戶金鑰，而不需要共用的存取簽章 (SAS)。

公用讀取權限是最佳的案例中，您特定 blob tooalways 可供匿名讀取權限。 對於更深入的控管需求，您可以建立共用存取簽章。 共用的存取簽章可讓您 tooprovide 限制存取特定的時間內使用不同的權限。 如需建立共用存取簽章的詳細資訊，請參閱[在 Azure 儲存體中使用共用存取簽章 (SAS)](storage-dotnet-shared-access-signature-part-1.md)。

## <a name="grant-anonymous-users-permissions-toocontainers-and-blobs"></a>授與匿名使用者的權限 toocontainers 和 blob
根據預設，容器和內部任何 blob 能存取只能由 hello hello 儲存體帳戶的擁有者。 toogive 匿名使用者的讀取權限 tooa 容器和其 blob，您可以設定 hello 容器的權限 tooallow 公用存取。 匿名使用者可以讀取可公開存取容器中的 blob，而不需驗證 hello 要求。

您可以設定容器具有下列權限的 hello:

* **沒有公開讀取權限：** hello 容器和其 blob 可以只由存取 hello 儲存體帳戶擁有者。 這是所有的新容器的 hello 預設。
* **僅對 blob 具有公開讀取：** hello 容器中的 Blob 可以讀取的匿名要求，但沒有可用容器資料。 匿名用戶端無法列舉 hello hello 容器內的 blob。
* **完整的公用讀取權限：**可以透過匿名要求讀取所有容器和 Blob 資料。 用戶端可以匿名要求，列舉 hello 容器中的 blob，但無法列舉 hello 儲存體帳戶中的容器。

您可以使用下列 tooset 容器權限的 hello:

* [Azure 入口網站](https://portal.azure.com)
* [Azure PowerShell](storage-powershell-guide-full.md#how-to-manage-azure-blobs)
* [Azure CLI 2.0](storage-azure-cli.md#create-and-manage-blobs)
* 以程式設計方式，利用其中一個 hello 儲存體用戶端程式庫或 hello REST API

### <a name="set-container-permissions-in-hello-azure-portal"></a>在 hello Azure 入口網站中設定容器的權限
在 hello tooset 容器權限[Azure 入口網站](https://portal.azure.com)，請遵循下列步驟：

1. 開啟您**儲存體帳戶**hello 入口網站中的刀鋒視窗。 您可以尋找儲存體帳戶選取**儲存體帳戶**hello 主要入口網站功能表刀鋒視窗中。
1. 在下**BLOB 服務**hello 功能表 刀鋒視窗中，選取**容器**。
1. 以滑鼠右鍵按一下 hello 容器資料列或選取 hello 省略 tooopen hello 容器的**操作功能表**。
1. 選取**存取原則**hello 內容功能表中。
1. 選取**存取類型**hello 從下拉功能表。

    ![編輯容器中繼資料對話方塊](./media/storage-manage-access-to-resources/storage-manage-access-to-resources-0.png)

### <a name="set-container-permissions-with-net"></a>使用 .NET 設定容器權限
tooset for.NET，使用 C# 和 hello 儲存體用戶端程式庫容器的權限第一次擷取 hello 容器的現有權限呼叫 hello **GetPermissions**方法。 然後組 hello **PublicAccess**屬性 hello **BlobContainerPermissions** hello 所傳回的物件**GetPermissions**方法。 最後，呼叫 hello **SetPermissions**方法 hello 與更新權限。

下列範例中的 hello 設定 hello 容器的權限 toofull 公用讀取權限。 tooset 權限 toopublic 「 讀取 」 存取 blob，設定 hello **PublicAccess**屬性太**BlobContainerPublicAccessType.Blob**。 tooremove 所有匿名使用者，權限設定太 hello 屬性**BlobContainerPublicAccessType.Off**。

```csharp
public static void SetPublicContainerPermissions(CloudBlobContainer container)
{
    BlobContainerPermissions permissions = container.GetPermissions();
    permissions.PublicAccess = BlobContainerPublicAccessType.Container;
    container.SetPermissions(permissions);
}
```

## <a name="access-containers-and-blobs-anonymously"></a>匿名存取容器與 Blob
匿名存取容器與 Blob 的用戶端可使用不需要認證的建構函式。 hello 遵循範例顯示一些不同方式 tooreference Blob 服務資源以匿名方式。

### <a name="create-an-anonymous-client-object"></a>建立匿名用戶端物件
您可以藉由提供 hello Blob 服務端點 hello 帳戶建立新的服務用戶端物件來匿名存取。 不過，您也必須知道 hello 供匿名存取該帳戶中的容器名稱。

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

### <a name="reference-a-container-anonymously"></a>匿名參考容器
如果您擁有 hello URL tooa 容器以匿名方式可用，您可以使用它 tooreference hello 容器直接。

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

### <a name="reference-a-blob-anonymously"></a>匿名參考 Blob
如果您有可供匿名存取的 hello URL tooa blob，您可以參考直接使用該 URL 的 hello blob:

```csharp
public static void DownloadBlobAnonymously()
{
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(@"https://storagesample.blob.core.windows.net/sample-container/logfile.txt"));
    blob.DownloadToFile(@"C:\Temp\logfile.txt", System.IO.FileMode.Create);
}
```

## <a name="features-available-tooanonymous-users"></a>功能可用 tooanonymous 使用者
hello 下表顯示容器的 ACL 設定 tooallow 公用存取時，可能會由匿名使用者呼叫哪些作業。

| REST 作業 | 具有完整公開讀取權限 | 僅對 Blob 有公開讀取權限 |
| --- | --- | --- |
| 列出容器 |只有擁有者 |只有擁有者 |
| 建立容器 |只有擁有者 |只有擁有者 |
| 取得容器屬性 |全部 |只有擁有者 |
| 取得容器中繼資料 |全部 |只有擁有者 |
| 設定容器中繼資料 |只有擁有者 |只有擁有者 |
| 取得容器 ACL |只有擁有者 |只有擁有者 |
| 設定容器 ACL |只有擁有者 |只有擁有者 |
| 刪除容器 |只有擁有者 |只有擁有者 |
| 列出 Blob |全部 |只有擁有者 |
| 放置 Blob |只有擁有者 |只有擁有者 |
| 取得 Blob |全部 |全部 |
| 取得 Blob 屬性 |全部 |全部 |
| 設定 Blob 屬性 |只有擁有者 |只有擁有者 |
| 取得 Blob 中繼資料 |全部 |全部 |
| 設定 Blob 中繼資料 |只有擁有者 |只有擁有者 |
| 放置區塊 |只有擁有者 |只有擁有者 |
| 取得區塊清單 (僅限認可區塊) |全部 |全部 |
| 取得區塊清單 (僅限未認可的區塊或所有區塊) |只有擁有者 |只有擁有者 |
| 放置區塊清單 |只有擁有者 |只有擁有者 |
| 刪除 Blob |只有擁有者 |只有擁有者 |
| 複製 Blob |只有擁有者 |只有擁有者 |
| 快照 Blob |只有擁有者 |只有擁有者 |
| 租用 Blob |只有擁有者 |只有擁有者 |
| 放置頁面 |只有擁有者 |只有擁有者 |
| 取得頁面範圍 |全部 |全部 |
| 附加 Blob |只有擁有者 |只有擁有者 |

## <a name="next-steps"></a>後續步驟

* [Hello Azure 儲存體服務的驗證](https://msdn.microsoft.com/library/azure/dd179428.aspx)
* [使用共用存取簽章 (SAS)](storage-dotnet-shared-access-signature-part-1.md)
* [使用共用存取簽章來委派存取權](https://msdn.microsoft.com/library/azure/ee395415.aspx)
