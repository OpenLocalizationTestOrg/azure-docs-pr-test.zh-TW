---
title: "Windows 市集應用程式中的 Azure 儲存體 aaaUse |Microsoft 文件"
description: "了解如何 toocreate Windows 市集應用程式使用 Azure Blob、 佇列、 資料表或檔案的儲存體。"
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 63c4b29d-b2f2-4d7c-b164-a0d38f4d14f6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: ac21b0695c0d77c1d81c1b921718fb929945d45e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-storage-in-windows-store-apps"></a>如何在 Windows 市集應用程式中的 Azure 儲存體 toouse
## <a name="overview"></a>概觀
本指南也說明 tooget 如何開始使用開發 Windows 市集應用程式，可使用的 Azure 儲存體。

## <a name="download-required-tools"></a>下載所需工具
* [Visual Studio](https://www.visualstudio.com/downloads/)可讓您輕鬆 toobuild，偵錯、 當地語系化、 封裝和部署 Windows 市集應用程式。 需要 visual Studio 2012 或更新版本。
* hello [Azure 儲存體用戶端程式庫](https://www.nuget.org/packages/WindowsAzure.Storage)提供 Windows 執行階段類別庫，使用 Azure 儲存體。
* [WCF 資料服務工具為 Windows 市集應用程式](http://www.microsoft.com/download/details.aspx?id=30714)擴充 Visual Studio 中的 Windows 市集應用程式的用戶端的 OData 支援 hello 加入服務參考的經驗。

## <a name="develop-apps"></a>開發應用程式
### <a name="getting-ready"></a>準備就緒
在 Visual Studio 2012 或更新版本中建立新的 Windows 市集應用程式專案：

![store-apps-storage-vs-project][store-apps-storage-vs-project]

接下來，以滑鼠右鍵按一下新增 Azure 儲存體用戶端程式庫的參考 toohello**參考**，然後按一下**加入參考**，然後瀏覽 toohello 儲存體用戶端程式庫的 Windows 執行階段，您下載：

![store-apps-storage-choose-library][store-apps-storage-choose-library]

### <a name="using-hello-library-with-hello-blob-and-queue-services"></a>使用 hello 文件庫以 hello Blob 和佇列服務
此時，您的應用程式已準備好 toocall hello Azure Blob 和佇列服務。 新增下列 hello**使用**陳述式，以便可以直接參考 Azure 儲存體類型：

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
```

接下來，新增按鈕 tooyour 頁面。 新增下列程式碼 tooits hello**按一下**事件，並修改您的事件處理常式方法使用 hello [async 關鍵字](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var blobClient = account.CreateCloudBlobClient();
var container = blobClient.GetContainerReference("container1");
await container.CreateIfNotExistsAsync();
```

此程式碼假設您有兩個字串變數 *accountName* 和 *accountKey*。 它們代表 hello 的儲存體帳戶和 hello 帳戶金鑰與該帳戶相關聯的名稱。

建置並執行 hello 應用程式。 按一下 [hello] 按鈕會檢查容器是否命名*container1*存在於您的帳戶，然後再建立它，如果不是。

### <a name="using-hello-library-with-hello-table-service"></a>Hello 表格服務搭配使用 hello 庫
使用的 toocommunicate 與 hello Azure 表格服務的型別取決於 hello Windows 市集應用程式程式庫的 WCF Data Services。 接下來，加入參考 toohello 需要 WCF 程式庫使用 hello Package Manager Console:

![store-apps-storage-package-manager][store-apps-storage-package-manager]

使用下列命令 toopoint 封裝管理員 toohello 位置在電腦上的 hello:

    Install-Package Microsoft.Data.OData.WindowsStore -Source "C:\Program Files (x86)\Microsoft WCF Data Services\5.0\bin\NuGet"

此命令會自動加入所有必要的參考 tooyour 專案。 若不想讓 toouse hello 封裝管理員主控台，則可以在本機電腦 toohello 清單中的封裝來源加入 hello WCF Data Services NuGet 資料夾中所述，然後新增 hello 參考 hello UI、 透過[管理 NuGet 封裝使用hello 對話方塊](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog)。

當您參考 hello WCF Data Services NuGet 套件時，變更按鈕的中的 hello 程式碼**按一下**事件：

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var tableClient = account.CreateCloudTableClient();
var table = tableClient.GetTableReference("table1");
await table.CreateIfNotExistsAsync();
```

此程式碼會檢查您的帳戶中是否有名為 *table1* 的資料表存在，如果不存在，則會建立該資料表。

您也可以加入參考 tooMicrosoft.WindowsAzure.Storage.Table.dll，它位在相同封裝下載的 hello。 此程式庫包含其他功能，例如反映式序列化和一般查詢。 請注意，此程式庫不支援 JavaScript。

[store-apps-storage-vs-project]: ./media/storage-use-store-apps/store-apps-storage-vs-project.png
[store-apps-storage-choose-library]: ./media/storage-use-store-apps/store-apps-storage-choose-library.png
[store-apps-storage-package-manager]: ./media/storage-use-store-apps/store-apps-storage-package-manager.png
