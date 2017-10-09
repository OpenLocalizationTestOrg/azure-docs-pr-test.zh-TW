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
# <a name="how-toouse-azure-storage-in-windows-store-apps"></a><span data-ttu-id="d3754-103">如何在 Windows 市集應用程式中的 Azure 儲存體 toouse</span><span class="sxs-lookup"><span data-stu-id="d3754-103">How toouse Azure Storage in Windows Store apps</span></span>
## <a name="overview"></a><span data-ttu-id="d3754-104">概觀</span><span class="sxs-lookup"><span data-stu-id="d3754-104">Overview</span></span>
<span data-ttu-id="d3754-105">本指南也說明 tooget 如何開始使用開發 Windows 市集應用程式，可使用的 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="d3754-105">This guide shows how tooget started with developing a Windows Store app that makes use of Azure Storage.</span></span>

## <a name="download-required-tools"></a><span data-ttu-id="d3754-106">下載所需工具</span><span class="sxs-lookup"><span data-stu-id="d3754-106">Download required tools</span></span>
* <span data-ttu-id="d3754-107">[Visual Studio](https://www.visualstudio.com/downloads/)可讓您輕鬆 toobuild，偵錯、 當地語系化、 封裝和部署 Windows 市集應用程式。</span><span class="sxs-lookup"><span data-stu-id="d3754-107">[Visual Studio](https://www.visualstudio.com/downloads/) makes it easy toobuild, debug, localize, package, and deploy Windows Store apps.</span></span> <span data-ttu-id="d3754-108">需要 visual Studio 2012 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="d3754-108">Visual Studio 2012 or later is required.</span></span>
* <span data-ttu-id="d3754-109">hello [Azure 儲存體用戶端程式庫](https://www.nuget.org/packages/WindowsAzure.Storage)提供 Windows 執行階段類別庫，使用 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="d3754-109">hello [Azure Storage Client Library](https://www.nuget.org/packages/WindowsAzure.Storage) provides a Windows Runtime class library for working with Azure Storage.</span></span>
* <span data-ttu-id="d3754-110">[WCF 資料服務工具為 Windows 市集應用程式](http://www.microsoft.com/download/details.aspx?id=30714)擴充 Visual Studio 中的 Windows 市集應用程式的用戶端的 OData 支援 hello 加入服務參考的經驗。</span><span class="sxs-lookup"><span data-stu-id="d3754-110">[WCF Data Services Tools for Windows Store Apps](http://www.microsoft.com/download/details.aspx?id=30714) extends hello Add Service Reference experience with client-side OData support for Windows Store apps in Visual Studio.</span></span>

## <a name="develop-apps"></a><span data-ttu-id="d3754-111">開發應用程式</span><span class="sxs-lookup"><span data-stu-id="d3754-111">Develop apps</span></span>
### <a name="getting-ready"></a><span data-ttu-id="d3754-112">準備就緒</span><span class="sxs-lookup"><span data-stu-id="d3754-112">Getting ready</span></span>
<span data-ttu-id="d3754-113">在 Visual Studio 2012 或更新版本中建立新的 Windows 市集應用程式專案：</span><span class="sxs-lookup"><span data-stu-id="d3754-113">Create a new Windows Store app project in Visual Studio 2012 or later:</span></span>

![store-apps-storage-vs-project][store-apps-storage-vs-project]

<span data-ttu-id="d3754-115">接下來，以滑鼠右鍵按一下新增 Azure 儲存體用戶端程式庫的參考 toohello**參考**，然後按一下**加入參考**，然後瀏覽 toohello 儲存體用戶端程式庫的 Windows 執行階段，您下載：</span><span class="sxs-lookup"><span data-stu-id="d3754-115">Next, add a reference toohello Azure Storage Client Library by right-clicking **References**, clicking **Add Reference**, and then browsing toohello Storage Client Library for Windows Runtime that you downloaded:</span></span>

![store-apps-storage-choose-library][store-apps-storage-choose-library]

### <a name="using-hello-library-with-hello-blob-and-queue-services"></a><span data-ttu-id="d3754-117">使用 hello 文件庫以 hello Blob 和佇列服務</span><span class="sxs-lookup"><span data-stu-id="d3754-117">Using hello library with hello Blob and Queue services</span></span>
<span data-ttu-id="d3754-118">此時，您的應用程式已準備好 toocall hello Azure Blob 和佇列服務。</span><span class="sxs-lookup"><span data-stu-id="d3754-118">At this point, your app is ready toocall hello Azure Blob and Queue services.</span></span> <span data-ttu-id="d3754-119">新增下列 hello**使用**陳述式，以便可以直接參考 Azure 儲存體類型：</span><span class="sxs-lookup"><span data-stu-id="d3754-119">Add hello following **using** statements so that Azure Storage types can be referenced directly:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
```

<span data-ttu-id="d3754-120">接下來，新增按鈕 tooyour 頁面。</span><span class="sxs-lookup"><span data-stu-id="d3754-120">Next, add a button tooyour page.</span></span> <span data-ttu-id="d3754-121">新增下列程式碼 tooits hello**按一下**事件，並修改您的事件處理常式方法使用 hello [async 關鍵字](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):</span><span class="sxs-lookup"><span data-stu-id="d3754-121">Add hello following code tooits **Click** event and modify your event handler method by using hello [async keyword](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):</span></span>

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var blobClient = account.CreateCloudBlobClient();
var container = blobClient.GetContainerReference("container1");
await container.CreateIfNotExistsAsync();
```

<span data-ttu-id="d3754-122">此程式碼假設您有兩個字串變數 *accountName* 和 *accountKey*。</span><span class="sxs-lookup"><span data-stu-id="d3754-122">This code assumes that you have two string variables, *accountName* and *accountKey*.</span></span> <span data-ttu-id="d3754-123">它們代表 hello 的儲存體帳戶和 hello 帳戶金鑰與該帳戶相關聯的名稱。</span><span class="sxs-lookup"><span data-stu-id="d3754-123">They represent hello name of your storage account and hello account key that is associated with that account.</span></span>

<span data-ttu-id="d3754-124">建置並執行 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d3754-124">Build and run hello application.</span></span> <span data-ttu-id="d3754-125">按一下 [hello] 按鈕會檢查容器是否命名*container1*存在於您的帳戶，然後再建立它，如果不是。</span><span class="sxs-lookup"><span data-stu-id="d3754-125">Clicking hello button will check whether a container named *container1* exists in your account and then create it if not.</span></span>

### <a name="using-hello-library-with-hello-table-service"></a><span data-ttu-id="d3754-126">Hello 表格服務搭配使用 hello 庫</span><span class="sxs-lookup"><span data-stu-id="d3754-126">Using hello library with hello Table service</span></span>
<span data-ttu-id="d3754-127">使用的 toocommunicate 與 hello Azure 表格服務的型別取決於 hello Windows 市集應用程式程式庫的 WCF Data Services。</span><span class="sxs-lookup"><span data-stu-id="d3754-127">Types that are used toocommunicate with hello Azure Table service depend on WCF Data Services for hello Windows Store app library.</span></span> <span data-ttu-id="d3754-128">接下來，加入參考 toohello 需要 WCF 程式庫使用 hello Package Manager Console:</span><span class="sxs-lookup"><span data-stu-id="d3754-128">Next, add a reference toohello required WCF libraries by using hello Package Manager Console:</span></span>

![store-apps-storage-package-manager][store-apps-storage-package-manager]

<span data-ttu-id="d3754-130">使用下列命令 toopoint 封裝管理員 toohello 位置在電腦上的 hello:</span><span class="sxs-lookup"><span data-stu-id="d3754-130">Use hello following command toopoint Package Manager toohello location on your machine:</span></span>

    Install-Package Microsoft.Data.OData.WindowsStore -Source "C:\Program Files (x86)\Microsoft WCF Data Services\5.0\bin\NuGet"

<span data-ttu-id="d3754-131">此命令會自動加入所有必要的參考 tooyour 專案。</span><span class="sxs-lookup"><span data-stu-id="d3754-131">This command will automatically add all required references tooyour project.</span></span> <span data-ttu-id="d3754-132">若不想讓 toouse hello 封裝管理員主控台，則可以在本機電腦 toohello 清單中的封裝來源加入 hello WCF Data Services NuGet 資料夾中所述，然後新增 hello 參考 hello UI、 透過[管理 NuGet 封裝使用hello 對話方塊](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog)。</span><span class="sxs-lookup"><span data-stu-id="d3754-132">If you do not want toouse hello Package Manager Console, you can add hello WCF Data Services NuGet folder on your local machine toohello list of package sources and then add hello reference through hello UI, as described in [Managing NuGet Packages Using hello Dialog](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).</span></span>

<span data-ttu-id="d3754-133">當您參考 hello WCF Data Services NuGet 套件時，變更按鈕的中的 hello 程式碼**按一下**事件：</span><span class="sxs-lookup"><span data-stu-id="d3754-133">When you have referenced hello WCF Data Services NuGet package, change hello code in your button's **Click** event:</span></span>

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var tableClient = account.CreateCloudTableClient();
var table = tableClient.GetTableReference("table1");
await table.CreateIfNotExistsAsync();
```

<span data-ttu-id="d3754-134">此程式碼會檢查您的帳戶中是否有名為 *table1* 的資料表存在，如果不存在，則會建立該資料表。</span><span class="sxs-lookup"><span data-stu-id="d3754-134">This code checks whether a table named *table1* exists in your account, and then creates it if not.</span></span>

<span data-ttu-id="d3754-135">您也可以加入參考 tooMicrosoft.WindowsAzure.Storage.Table.dll，它位在相同封裝下載的 hello。</span><span class="sxs-lookup"><span data-stu-id="d3754-135">You can also add a reference tooMicrosoft.WindowsAzure.Storage.Table.dll, which is available in hello same package that you downloaded.</span></span> <span data-ttu-id="d3754-136">此程式庫包含其他功能，例如反映式序列化和一般查詢。</span><span class="sxs-lookup"><span data-stu-id="d3754-136">This library contains additional functionality, such as reflection-based serialization and generic queries.</span></span> <span data-ttu-id="d3754-137">請注意，此程式庫不支援 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="d3754-137">Note that this library does not support JavaScript.</span></span>

[store-apps-storage-vs-project]: ./media/storage-use-store-apps/store-apps-storage-vs-project.png
[store-apps-storage-choose-library]: ./media/storage-use-store-apps/store-apps-storage-choose-library.png
[store-apps-storage-package-manager]: ./media/storage-use-store-apps/store-apps-storage-package-manager.png
