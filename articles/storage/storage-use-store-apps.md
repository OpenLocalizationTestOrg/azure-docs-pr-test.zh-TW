---
title: "在 Windows 市集應用程式中使用 Azure 儲存體 | Microsoft Docs"
description: "了解如何建立使用 Azure Blob、佇列、資料表或檔案儲存體的 Windows 市集應用程式。"
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
ms.openlocfilehash: 43d38584270fbbbe6fa4e4ff8cef72ca44e14acc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-azure-storage-in-windows-store-apps"></a><span data-ttu-id="4fdf8-103">如何在 Windows 市集應用程式中使用 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="4fdf8-103">How to use Azure Storage in Windows Store apps</span></span>
## <a name="overview"></a><span data-ttu-id="4fdf8-104">Overview</span><span class="sxs-lookup"><span data-stu-id="4fdf8-104">Overview</span></span>
<span data-ttu-id="4fdf8-105">本指南說明如何開始著手開發採用 Azure 儲存體的 Windows 市集應用程式。</span><span class="sxs-lookup"><span data-stu-id="4fdf8-105">This guide shows how to get started with developing a Windows Store app that makes use of Azure Storage.</span></span>

## <a name="download-required-tools"></a><span data-ttu-id="4fdf8-106">下載所需工具</span><span class="sxs-lookup"><span data-stu-id="4fdf8-106">Download required tools</span></span>
* <span data-ttu-id="4fdf8-107">[Visual Studio](https://www.visualstudio.com/downloads/) 可讓您輕鬆地建置、偵錯、當地語系化、封裝及部署 Windows 市集應用程式。</span><span class="sxs-lookup"><span data-stu-id="4fdf8-107">[Visual Studio](https://www.visualstudio.com/downloads/) makes it easy to build, debug, localize, package, and deploy Windows Store apps.</span></span> <span data-ttu-id="4fdf8-108">需要 visual Studio 2012 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="4fdf8-108">Visual Studio 2012 or later is required.</span></span>
* <span data-ttu-id="4fdf8-109">[Azure Storage Client Library (Azure 儲存體用戶端程式庫)](https://www.nuget.org/packages/WindowsAzure.Storage) 提供可處理 Azure 儲存體的 Windows 執行階段類別庫。</span><span class="sxs-lookup"><span data-stu-id="4fdf8-109">The [Azure Storage Client Library](https://www.nuget.org/packages/WindowsAzure.Storage) provides a Windows Runtime class library for working with Azure Storage.</span></span>
* <span data-ttu-id="4fdf8-110">[適用於 Windows 市集應用程式的 WCF 資料服務工具](http://www.microsoft.com/download/details.aspx?id=30714) 利用 Visual Studio 中 Windows 市集應用程式的用戶端 OData 支援，擴充了「加入服務參考」體驗。</span><span class="sxs-lookup"><span data-stu-id="4fdf8-110">[WCF Data Services Tools for Windows Store Apps](http://www.microsoft.com/download/details.aspx?id=30714) extends the Add Service Reference experience with client-side OData support for Windows Store apps in Visual Studio.</span></span>

## <a name="develop-apps"></a><span data-ttu-id="4fdf8-111">開發應用程式</span><span class="sxs-lookup"><span data-stu-id="4fdf8-111">Develop apps</span></span>
### <a name="getting-ready"></a><span data-ttu-id="4fdf8-112">準備就緒</span><span class="sxs-lookup"><span data-stu-id="4fdf8-112">Getting ready</span></span>
<span data-ttu-id="4fdf8-113">在 Visual Studio 2012 或更新版本中建立新的 Windows 市集應用程式專案：</span><span class="sxs-lookup"><span data-stu-id="4fdf8-113">Create a new Windows Store app project in Visual Studio 2012 or later:</span></span>

![store-apps-storage-vs-project][store-apps-storage-vs-project]

<span data-ttu-id="4fdf8-115">接著，加入 Azure 儲存體用戶端程式庫的參考，方法是以滑鼠右鍵按一下 [參考]，然後按一下 [加入參考]，並瀏覽到已下載的適用於 Windows 的儲存體用戶端程式庫執行階段：</span><span class="sxs-lookup"><span data-stu-id="4fdf8-115">Next, add a reference to the Azure Storage Client Library by right-clicking **References**, clicking **Add Reference**, and then browsing to the Storage Client Library for Windows Runtime that you downloaded:</span></span>

![store-apps-storage-choose-library][store-apps-storage-choose-library]

### <a name="using-the-library-with-the-blob-and-queue-services"></a><span data-ttu-id="4fdf8-117">使用搭配 Blob 和佇列服務的程式庫</span><span class="sxs-lookup"><span data-stu-id="4fdf8-117">Using the library with the Blob and Queue services</span></span>
<span data-ttu-id="4fdf8-118">此時您的應用程式已準備好可呼叫 Azure Blob 和佇列服務。</span><span class="sxs-lookup"><span data-stu-id="4fdf8-118">At this point, your app is ready to call the Azure Blob and Queue services.</span></span> <span data-ttu-id="4fdf8-119">新增下列 **using** 陳述式，以方便直接參考 Azure 儲存體類型：</span><span class="sxs-lookup"><span data-stu-id="4fdf8-119">Add the following **using** statements so that Azure Storage types can be referenced directly:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
```

<span data-ttu-id="4fdf8-120">接著，新增頁面按鈕。</span><span class="sxs-lookup"><span data-stu-id="4fdf8-120">Next, add a button to your page.</span></span> <span data-ttu-id="4fdf8-121">將下列程式碼加入其 **Click** 事件，並使用 [async 關鍵字](http://msdn.microsoft.com/library/vstudio/hh156513.aspx)來修改事件處理常式方法：</span><span class="sxs-lookup"><span data-stu-id="4fdf8-121">Add the following code to its **Click** event and modify your event handler method by using the [async keyword](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):</span></span>

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var blobClient = account.CreateCloudBlobClient();
var container = blobClient.GetContainerReference("container1");
await container.CreateIfNotExistsAsync();
```

<span data-ttu-id="4fdf8-122">此程式碼假設您有兩個字串變數 *accountName* 和 *accountKey*。</span><span class="sxs-lookup"><span data-stu-id="4fdf8-122">This code assumes that you have two string variables, *accountName* and *accountKey*.</span></span> <span data-ttu-id="4fdf8-123">它們代表儲存體帳戶和該帳戶相關聯之帳戶金鑰的名稱。</span><span class="sxs-lookup"><span data-stu-id="4fdf8-123">They represent the name of your storage account and the account key that is associated with that account.</span></span>

<span data-ttu-id="4fdf8-124">建置並執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="4fdf8-124">Build and run the application.</span></span> <span data-ttu-id="4fdf8-125">按一下按鈕將會檢查您的帳戶中是否有名為 *container1* 的容器存在，如果沒有的話則建立該容器。</span><span class="sxs-lookup"><span data-stu-id="4fdf8-125">Clicking the button will check whether a container named *container1* exists in your account and then create it if not.</span></span>

### <a name="using-the-library-with-the-table-service"></a><span data-ttu-id="4fdf8-126">使用搭配資料表服務的程式庫</span><span class="sxs-lookup"><span data-stu-id="4fdf8-126">Using the library with the Table service</span></span>
<span data-ttu-id="4fdf8-127">用來與 Azure 資料表服務通訊的類型會視 Windows 市集應用程式程式庫適用的 WCF 資料服務而定。</span><span class="sxs-lookup"><span data-stu-id="4fdf8-127">Types that are used to communicate with the Azure Table service depend on WCF Data Services for the Windows Store app library.</span></span> <span data-ttu-id="4fdf8-128">接著，透過使用 Package Manager Console 加入所需的 WCF 程式庫參考：</span><span class="sxs-lookup"><span data-stu-id="4fdf8-128">Next, add a reference to the required WCF libraries by using the Package Manager Console:</span></span>

![store-apps-storage-package-manager][store-apps-storage-package-manager]

<span data-ttu-id="4fdf8-130">使用下列命令將 [Package Manager] 指向您機器上的位置：</span><span class="sxs-lookup"><span data-stu-id="4fdf8-130">Use the following command to point Package Manager to the location on your machine:</span></span>

    Install-Package Microsoft.Data.OData.WindowsStore -Source "C:\Program Files (x86)\Microsoft WCF Data Services\5.0\bin\NuGet"

<span data-ttu-id="4fdf8-131">此命令會自動將所有所需的參考加入您的專案。</span><span class="sxs-lookup"><span data-stu-id="4fdf8-131">This command will automatically add all required references to your project.</span></span> <span data-ttu-id="4fdf8-132">如果您不想使用 Package Manager Console，您也可以將本機機器上的 WCF 資料服務 NuGet 資料夾加入封裝來源清單，然後透過 UI 加入參考，如 [使用對話方塊管理 NuGet 封裝](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog)中所述。</span><span class="sxs-lookup"><span data-stu-id="4fdf8-132">If you do not want to use the Package Manager Console, you can add the WCF Data Services NuGet folder on your local machine to the list of package sources and then add the reference through the UI, as described in [Managing NuGet Packages Using the Dialog](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).</span></span>

<span data-ttu-id="4fdf8-133">當您參考 WCF 資料服務 NuGet 套件時，請變更按鈕 **Click** 事件中的程式碼：</span><span class="sxs-lookup"><span data-stu-id="4fdf8-133">When you have referenced the WCF Data Services NuGet package, change the code in your button's **Click** event:</span></span>

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var tableClient = account.CreateCloudTableClient();
var table = tableClient.GetTableReference("table1");
await table.CreateIfNotExistsAsync();
```

<span data-ttu-id="4fdf8-134">此程式碼會檢查您的帳戶中是否有名為 *table1* 的資料表存在，如果不存在，則會建立該資料表。</span><span class="sxs-lookup"><span data-stu-id="4fdf8-134">This code checks whether a table named *table1* exists in your account, and then creates it if not.</span></span>

<span data-ttu-id="4fdf8-135">您也可以加入 Microsoft.WindowsAzure.Storage.Table.dll (您可以在下載的相同封裝中找到) 的參考。</span><span class="sxs-lookup"><span data-stu-id="4fdf8-135">You can also add a reference to Microsoft.WindowsAzure.Storage.Table.dll, which is available in the same package that you downloaded.</span></span> <span data-ttu-id="4fdf8-136">此程式庫包含其他功能，例如反映式序列化和一般查詢。</span><span class="sxs-lookup"><span data-stu-id="4fdf8-136">This library contains additional functionality, such as reflection-based serialization and generic queries.</span></span> <span data-ttu-id="4fdf8-137">請注意，此程式庫不支援 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="4fdf8-137">Note that this library does not support JavaScript.</span></span>

[store-apps-storage-vs-project]: ./media/storage-use-store-apps/store-apps-storage-vs-project.png
[store-apps-storage-choose-library]: ./media/storage-use-store-apps/store-apps-storage-choose-library.png
[store-apps-storage-package-manager]: ./media/storage-use-store-apps/store-apps-storage-package-manager.png
