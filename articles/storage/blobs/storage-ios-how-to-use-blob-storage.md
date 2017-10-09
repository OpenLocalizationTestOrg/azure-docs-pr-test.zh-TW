---
title: "aaaHow toouse 從 iOS 的 Azure Blob 儲存體 |Microsoft 文件"
description: "使用 Azure Blob 儲存體 （物件儲存體） 的 hello 雲端中儲存非結構化的資料。"
services: storage
documentationcenter: ios
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: df188021-86fc-4d31-a810-1b0e7bcd814b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: objective-c
ms.topic: article
ms.date: 05/11/2017
ms.author: michaelhauss
ms.openlocfilehash: cc08b76b682537a9a51e970c76bd76c7c06a4ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-ios"></a><span data-ttu-id="22146-103">如何 toouse iOS 從 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="22146-103">How toouse Blob storage from iOS</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="22146-104">概觀</span><span class="sxs-lookup"><span data-stu-id="22146-104">Overview</span></span>
<span data-ttu-id="22146-105">這篇文章將示範如何使用 Microsoft Azure Blob 儲存體 tooperform 常見案例。</span><span class="sxs-lookup"><span data-stu-id="22146-105">This article will show you how tooperform common scenarios using Microsoft Azure Blob storage.</span></span> <span data-ttu-id="22146-106">hello 範例以 OBJECTIVE-C 所撰寫並使用 hello[適用於 iOS 的 Azure 儲存體用戶端程式庫](https://github.com/Azure/azure-storage-ios)。</span><span class="sxs-lookup"><span data-stu-id="22146-106">hello samples are written in Objective-C and use hello [Azure Storage Client Library for iOS](https://github.com/Azure/azure-storage-ios).</span></span> <span data-ttu-id="22146-107">hello 涵蓋案例包括**上載**，**列出**，**下載**，和**刪除**blob。</span><span class="sxs-lookup"><span data-stu-id="22146-107">hello scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="22146-108">如需有關 blob 的詳細資訊，請參閱 hello[接下來的步驟](#next-steps)> 一節。</span><span class="sxs-lookup"><span data-stu-id="22146-108">For more information on blobs, see hello [Next Steps](#next-steps) section.</span></span> <span data-ttu-id="22146-109">您也可以下載 hello[範例應用程式](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample)tooquickly 看到 hello iOS 應用程式中的使用 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="22146-109">You can also download hello [sample app](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) tooquickly see hello use of Azure Storage in an iOS application.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="import-hello-azure-storage-ios-library-into-your-application"></a><span data-ttu-id="22146-110">Hello Azure 儲存體 iOS 的程式庫匯入您的應用程式</span><span class="sxs-lookup"><span data-stu-id="22146-110">Import hello Azure Storage iOS library into your application</span></span>
<span data-ttu-id="22146-111">Hello Azure 儲存體 iOS 的程式庫匯入您的應用程式使用 hello [Azure 儲存體 CocoaPod](https://cocoapods.org/pods/AZSClient)或匯入 hello **Framework**檔案。</span><span class="sxs-lookup"><span data-stu-id="22146-111">You can import hello Azure Storage iOS library into your application either by using hello [Azure Storage CocoaPod](https://cocoapods.org/pods/AZSClient) or by importing hello **Framework** file.</span></span> <span data-ttu-id="22146-112">CocoaPod 為建議的方式，因為它會讓整合 hello 庫較為簡單，不過匯入從 hello 架構檔案是較不干擾現有專案的 hello。</span><span class="sxs-lookup"><span data-stu-id="22146-112">CocoaPod is hello recommended way as it makes integrating hello library easier, however importing from hello framework file is less intrusive for your existing project.</span></span>

<span data-ttu-id="22146-113">toouse 此程式庫，您需要遵循的 hello:</span><span class="sxs-lookup"><span data-stu-id="22146-113">toouse this library, you need hello following:</span></span>
- <span data-ttu-id="22146-114">iOS 8+</span><span class="sxs-lookup"><span data-stu-id="22146-114">iOS 8+</span></span>
- <span data-ttu-id="22146-115">Xcode 7+</span><span class="sxs-lookup"><span data-stu-id="22146-115">Xcode 7+</span></span>

## <a name="cocoapod"></a><span data-ttu-id="22146-116">CocoaPod</span><span class="sxs-lookup"><span data-stu-id="22146-116">CocoaPod</span></span>
1. <span data-ttu-id="22146-117">如果您沒有這樣做，[安裝 CocoaPods](https://guides.cocoapods.org/using/getting-started.html#toc_3)上開啟終端機視窗，然後執行下列命令的 hello 電腦</span><span class="sxs-lookup"><span data-stu-id="22146-117">If you haven't done so already, [Install CocoaPods](https://guides.cocoapods.org/using/getting-started.html#toc_3) on your computer by opening a terminal window and running hello following command</span></span>
    
    ```shell   
    sudo gem install cocoapods
    ```

2. <span data-ttu-id="22146-118">接下來，在 hello 專案目錄中 （hello 目錄包含.xcodeproj 檔案），建立新的檔案，稱為_Podfile_（沒有副檔名）。</span><span class="sxs-lookup"><span data-stu-id="22146-118">Next, in hello project directory (hello directory containing your .xcodeproj file), create a new file called _Podfile_(no file extension).</span></span> <span data-ttu-id="22146-119">新增下列 too_Podfile_ hello 和儲存。</span><span class="sxs-lookup"><span data-stu-id="22146-119">Add hello following too_Podfile_ and save.</span></span>

    ```ruby
    platform :ios, '8.0'

    target 'TargetName' do
      pod 'AZSClient'
    end
    ```

3. <span data-ttu-id="22146-120">在 hello 終端機視窗，瀏覽 toohello 專案目錄並執行下列命令的 hello</span><span class="sxs-lookup"><span data-stu-id="22146-120">In hello terminal window, navigate toohello project directory and run hello following command</span></span>

    ```shell    
    pod install
    ```

4. <span data-ttu-id="22146-121">如果您已在 Xcode 中開啟 .xcodeproj，請將它關閉。</span><span class="sxs-lookup"><span data-stu-id="22146-121">If your .xcodeproj is open in Xcode, close it.</span></span> <span data-ttu-id="22146-122">專案目錄開啟 hello 新建立的專案檔中將有 hello.xcworkspace 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="22146-122">In your project directory open hello newly created project file which will have hello .xcworkspace extension.</span></span> <span data-ttu-id="22146-123">這是您將從現在在運作的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="22146-123">This is hello file you'll work from for now on.</span></span>

## <a name="framework"></a><span data-ttu-id="22146-124">Framework</span><span class="sxs-lookup"><span data-stu-id="22146-124">Framework</span></span>
<span data-ttu-id="22146-125">hello toouse hello 程式庫手動是 toobuild hello 架構，另一種方式：</span><span class="sxs-lookup"><span data-stu-id="22146-125">hello other way toouse hello library is toobuild hello framework manually:</span></span>

1. <span data-ttu-id="22146-126">第一個、 下載或複製 hello [azure 儲存體 ios 儲存機制](https://github.com/azure/azure-storage-ios)。</span><span class="sxs-lookup"><span data-stu-id="22146-126">First, download or clone hello [azure-storage-ios repo](https://github.com/azure/azure-storage-ios).</span></span>
2. <span data-ttu-id="22146-127">移至 *azure-storage-ios* -> *Lib* -> *Azure 儲存體用戶端程式庫*，然後在 Xcode 中開啟 `AZSClient.xcodeproj`。</span><span class="sxs-lookup"><span data-stu-id="22146-127">Go into *azure-storage-ios* -> *Lib* -> *Azure Storage Client Library*, and open `AZSClient.xcodeproj` in Xcode.</span></span>
3. <span data-ttu-id="22146-128">在 hello 左上方的 Xcode 變更 hello active 配置從 「 Azure 儲存體用戶端程式庫 」 太 < Framework >。</span><span class="sxs-lookup"><span data-stu-id="22146-128">At hello top-left of Xcode, change hello active scheme from "Azure Storage Client Library" too"Framework".</span></span>
4. <span data-ttu-id="22146-129">建置 hello 專案 （⌘ + B）。</span><span class="sxs-lookup"><span data-stu-id="22146-129">Build hello project (⌘+B).</span></span> <span data-ttu-id="22146-130">這會在您的桌面上建立 `AZSClient.framework` 檔案。</span><span class="sxs-lookup"><span data-stu-id="22146-130">This will create an `AZSClient.framework` file on your Desktop.</span></span>

<span data-ttu-id="22146-131">您接著可以 hello 架構檔案匯入您的應用程式執行 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="22146-131">You can then import hello framework file into your application by doing hello following:</span></span>

1. <span data-ttu-id="22146-132">建立新的專案，或在 Xcode 中開啟現有的專案。</span><span class="sxs-lookup"><span data-stu-id="22146-132">Create a new project or open up your existing project in Xcode.</span></span>
2. <span data-ttu-id="22146-133">拖放 hello`AZSClient.framework`到您的 Xcode 專案導覽器。</span><span class="sxs-lookup"><span data-stu-id="22146-133">Drag and drop hello `AZSClient.framework` into your Xcode project navigator.</span></span>
3. <span data-ttu-id="22146-134">選取 [必要時複製項目]，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="22146-134">Select *Copy items if needed*, and click on *Finish*.</span></span>
4. <span data-ttu-id="22146-135">Hello 左側導覽中的專案上按一下，然後按一下 hello*一般*在 hello hello 專案編輯器頂端的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="22146-135">Click on your project in hello left-hand navigation and click hello *General* tab at hello top of hello project editor.</span></span>
5. <span data-ttu-id="22146-136">在 [hello*連結架構和程式庫*區段中，按一下 hello 新增] 按鈕 （+）。</span><span class="sxs-lookup"><span data-stu-id="22146-136">Under hello *Linked Frameworks and Libraries* section, click hello Add button (+).</span></span>
6. <span data-ttu-id="22146-137">在 [hello] 清單中已經提供的程式庫，搜尋`libxml2.2.tbd`並將它加入 tooyour 專案。</span><span class="sxs-lookup"><span data-stu-id="22146-137">In hello list of libraries already provided, search for `libxml2.2.tbd` and add it tooyour project.</span></span>

## <a name="import-hello-library"></a><span data-ttu-id="22146-138">匯入 hello 程式庫</span><span class="sxs-lookup"><span data-stu-id="22146-138">Import hello Library</span></span> 
```objc
// Include hello following import statement toouse blob APIs.
#import <AZSClient/AZSClient.h>
```

<span data-ttu-id="22146-139">如果您使用 Swift 時，您將需要 toocreate 橋接標頭，並那里匯入 < AZSClient/AZSClient.h >:</span><span class="sxs-lookup"><span data-stu-id="22146-139">If you are using Swift, you will need toocreate a bridging header and import <AZSClient/AZSClient.h> there:</span></span>

1. <span data-ttu-id="22146-140">建立標頭檔`Bridging-Header.h`，並加入 hello 上方匯入陳述式。</span><span class="sxs-lookup"><span data-stu-id="22146-140">Create a header file `Bridging-Header.h`, and add hello above import statement.</span></span>
2. <span data-ttu-id="22146-141">移 toohello*組建設定*索引標籤，並搜尋*OBJECTIVE-C 橋接標頭*。</span><span class="sxs-lookup"><span data-stu-id="22146-141">Go toohello *Build Settings* tab, and search for *Objective-C Bridging Header*.</span></span>
3. <span data-ttu-id="22146-142">Hello 欄位上按兩下*OBJECTIVE-C 橋接標頭*將 hello 路徑 tooyour 標頭檔：`ProjectName/Bridging-Header.h`</span><span class="sxs-lookup"><span data-stu-id="22146-142">Double-click on hello field of *Objective-C Bridging Header* and add hello path tooyour header file: `ProjectName/Bridging-Header.h`</span></span>
4. <span data-ttu-id="22146-143">Hello 橋接標頭的組建 hello 專案 （⌘ + B） tooverify Xcode 已收取。</span><span class="sxs-lookup"><span data-stu-id="22146-143">Build hello project (⌘+B) tooverify that hello bridging header was picked up by Xcode.</span></span>
5. <span data-ttu-id="22146-144">開始使用 hello 程式庫直接在任何 Swift 檔案中，不需要匯入陳述式。</span><span class="sxs-lookup"><span data-stu-id="22146-144">Start using hello library directly in any Swift file, there is no need for import statements.</span></span>

[!INCLUDE [storage-mobile-authentication-guidance](../../../includes/storage-mobile-authentication-guidance.md)]

## <a name="asynchronous-operations"></a><span data-ttu-id="22146-145">非同步作業</span><span class="sxs-lookup"><span data-stu-id="22146-145">Asynchronous Operations</span></span>
> [!NOTE]
> <span data-ttu-id="22146-146">執行對 hello 服務提出之要求的所有方法都是非同步作業。</span><span class="sxs-lookup"><span data-stu-id="22146-146">All methods that perform a request against hello service are asynchronous operations.</span></span> <span data-ttu-id="22146-147">在 hello 程式碼範例中，您會發現這些方法已完成處理常式。</span><span class="sxs-lookup"><span data-stu-id="22146-147">In hello code samples, you'll find that these methods have a completion handler.</span></span> <span data-ttu-id="22146-148">Hello 完成處理常式內部的程式碼會執行**之後**hello 要求完成。</span><span class="sxs-lookup"><span data-stu-id="22146-148">Code inside hello completion handler will run **after** hello request is completed.</span></span> <span data-ttu-id="22146-149">程式碼會執行 hello 完成處理常式之後**時**hello 要求所針對。</span><span class="sxs-lookup"><span data-stu-id="22146-149">Code after hello completion handler will run **while** hello request is being made.</span></span>
> 
> 

## <a name="create-a-container"></a><span data-ttu-id="22146-150">建立容器</span><span class="sxs-lookup"><span data-stu-id="22146-150">Create a container</span></span>
<span data-ttu-id="22146-151">儲存體 Blob 中的每個 Blob 必須位於一個容器中。</span><span class="sxs-lookup"><span data-stu-id="22146-151">Every blob in Azure Storage must reside in a container.</span></span> <span data-ttu-id="22146-152">hello 下列範例顯示如何 toocreate 容器使用時，呼叫*newcontainer*，在儲存體帳戶，如果不存在。</span><span class="sxs-lookup"><span data-stu-id="22146-152">hello following example shows how toocreate a container, called *newcontainer*, in your Storage account if it doesn't already exist.</span></span> <span data-ttu-id="22146-153">選擇您的容器的名稱，留意 hello 命名上面所述的規則。</span><span class="sxs-lookup"><span data-stu-id="22146-153">When choosing a name for your container, be mindful of hello naming rules mentioned above.</span></span>

```objc
-(void)createContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"newcontainer"];

    // Create container in your Storage account if hello container doesn't already exist
    [blobContainer createContainerIfNotExistsWithCompletionHandler:^(NSError *error, BOOL exists) {
        if (error){
            NSLog(@"Error in creating container.");
        }
    }];
}
```

<span data-ttu-id="22146-154">您可以確認其運作藉由查看 hello [Microsoft Azure 儲存體總管](http://storageexplorer.com)並確認*newcontainer* hello 容器使用的儲存體帳戶清單中。</span><span class="sxs-lookup"><span data-stu-id="22146-154">You can confirm that this works by looking at hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) and verifying that *newcontainer* is in hello list of containers for your Storage account.</span></span>

## <a name="set-container-permissions"></a><span data-ttu-id="22146-155">設定容器權限</span><span class="sxs-lookup"><span data-stu-id="22146-155">Set Container Permissions</span></span>
<span data-ttu-id="22146-156">依預設會針對 [私人]  存取設定容器的權限。</span><span class="sxs-lookup"><span data-stu-id="22146-156">A container's permissions are configured for **Private** access by default.</span></span> <span data-ttu-id="22146-157">不過，容器會提供幾個不同的容器存取選項：</span><span class="sxs-lookup"><span data-stu-id="22146-157">However, containers provide a few different options for container access:</span></span>

* <span data-ttu-id="22146-158">**私用**: hello 帳戶擁有者可以讀取容器和 blob 資料。</span><span class="sxs-lookup"><span data-stu-id="22146-158">**Private**: Container and blob data can be read by hello account owner only.</span></span>
* <span data-ttu-id="22146-159">**Blob**：您可以透過匿名要求讀取此容器內的 Blob 資料，但您無法使用容器資料。</span><span class="sxs-lookup"><span data-stu-id="22146-159">**Blob**: Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="22146-160">用戶端無法列舉 hello 透過匿名要求的容器中的 blob。</span><span class="sxs-lookup"><span data-stu-id="22146-160">Clients cannot enumerate blobs within hello container via anonymous request.</span></span>
* <span data-ttu-id="22146-161">**容器**：可以透過匿名要求讀取容器和 Blob 資料。</span><span class="sxs-lookup"><span data-stu-id="22146-161">**Container**: Container and blob data can be read via anonymous request.</span></span> <span data-ttu-id="22146-162">用戶端透過匿名要求，hello 容器內的 blob，但無法列舉 hello 儲存體帳戶中的容器。</span><span class="sxs-lookup"><span data-stu-id="22146-162">Clients can enumerate blobs within hello container via anonymous request, but cannot enumerate containers within hello storage account.</span></span>

<span data-ttu-id="22146-163">hello 下列範例會示範如何與容器的 toocreate**容器**存取允許 hello 網際網路上的所有使用者公開的唯讀存取權限：</span><span class="sxs-lookup"><span data-stu-id="22146-163">hello following example shows you how toocreate a container with **Container** access permissions, which will allow public, read-only access for all users on hello Internet:</span></span>

```objc
-(void)createContainerWithPublicAccess{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Create container in your Storage account if hello container doesn't already exist
    [blobContainer createContainerIfNotExistsWithAccessType:AZSContainerPublicAccessTypeContainer requestOptions:nil operationContext:nil completionHandler:^(NSError *error, BOOL exists){
        if (error){
            NSLog(@"Error in creating container.");
        }
    }];
}
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="22146-164">將 Blob 上傳至容器</span><span class="sxs-lookup"><span data-stu-id="22146-164">Upload a blob into a container</span></span>
<span data-ttu-id="22146-165">Hello 中所述[Blob 服務概念](#blob-service-concepts) 區段中，Blob 儲存體提供三種不同的 blob： 區塊 blob、 附加 blob 和分頁 blob。</span><span class="sxs-lookup"><span data-stu-id="22146-165">As mentioned in hello [Blob service concepts](#blob-service-concepts) section, Blob Storage offers three different types of blobs: block blobs, append blobs, and page blobs.</span></span> <span data-ttu-id="22146-166">hello Azure 儲存體 iOS 的程式庫支援所有的三種類型的 blob。</span><span class="sxs-lookup"><span data-stu-id="22146-166">hello Azure Storage iOS library supports all three types of blobs.</span></span> <span data-ttu-id="22146-167">在大部分情況下，區塊 blob 是建議的型別 toouse hello。</span><span class="sxs-lookup"><span data-stu-id="22146-167">In most cases, block blob is hello recommended type toouse.</span></span>

<span data-ttu-id="22146-168">hello 下列範例會顯示從 NSString tooupload 區塊 blob 的方式。</span><span class="sxs-lookup"><span data-stu-id="22146-168">hello following example shows how tooupload a block blob from an NSString.</span></span> <span data-ttu-id="22146-169">如果此容器中已經有名稱相同的 hello 的 blob，此 blob 的 hello 內容會被覆寫。</span><span class="sxs-lookup"><span data-stu-id="22146-169">If a blob with hello same name already exists in this container, hello contents of this blob will be overwritten.</span></span>

```objc
-(void)uploadBlobToContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    [blobContainer createContainerIfNotExistsWithAccessType:AZSContainerPublicAccessTypeContainer requestOptions:nil operationContext:nil completionHandler:^(NSError *error, BOOL exists)
        {
            if (error){
                NSLog(@"Error in creating container.");
            }
            else{
                // Create a local blob object
                AZSCloudBlockBlob *blockBlob = [blobContainer blockBlobReferenceFromName:@"sampleblob"];

                // Upload blob tooStorage
                [blockBlob uploadFromText:@"This text will be uploaded tooBlob Storage." completionHandler:^(NSError *error) {
                    if (error){
                        NSLog(@"Error in creating blob.");
                    }
                }];
            }
        }];
}
```

<span data-ttu-id="22146-170">您可以確認其運作藉由查看 hello [Microsoft Azure 儲存體總管](http://storageexplorer.com)及驗證 hello 程序*containerpublic*，包含 hello blob *sampleblob*.</span><span class="sxs-lookup"><span data-stu-id="22146-170">You can confirm that this works by looking at hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) and verifying that hello container, *containerpublic*, contains hello blob, *sampleblob*.</span></span> <span data-ttu-id="22146-171">在此範例中，我們會使用公用容器，因此您也可以驗證，此應用程式的工作移 toohello blob URI:</span><span class="sxs-lookup"><span data-stu-id="22146-171">In this sample, we used a public container so you can also verify that this application worked by going toohello blobs URI:</span></span>

    https://nameofyourstorageaccount.blob.core.windows.net/containerpublic/sampleblob

<span data-ttu-id="22146-172">此外 toouploading NSString 從區塊 blob，類似的方法有 NSData、 NSInputStream 或本機檔案。</span><span class="sxs-lookup"><span data-stu-id="22146-172">In addition toouploading a block blob from an NSString, similar methods exist for NSData, NSInputStream, or a local file.</span></span>

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="22146-173">列出容器中的 hello blob</span><span class="sxs-lookup"><span data-stu-id="22146-173">List hello blobs in a container</span></span>
<span data-ttu-id="22146-174">下列範例會示範如何 toolist 所有 blob 容器中的 hello。</span><span class="sxs-lookup"><span data-stu-id="22146-174">hello following example shows how toolist all blobs in a container.</span></span> <span data-ttu-id="22146-175">當執行這項作業，請留意 hello 下列參數：</span><span class="sxs-lookup"><span data-stu-id="22146-175">When performing this operation, be mindful of hello following parameters:</span></span>     

* <span data-ttu-id="22146-176">**continuationToken** -hello 接續 token 代表 hello 列出作業應該在此處開始。</span><span class="sxs-lookup"><span data-stu-id="22146-176">**continuationToken** - hello continuation token represents where hello listing operation should start.</span></span> <span data-ttu-id="22146-177">如果未不提供任何 token，則它會列出從 hello 開頭的 blob。</span><span class="sxs-lookup"><span data-stu-id="22146-177">If no token is provided, it will list blobs from hello beginning.</span></span> <span data-ttu-id="22146-178">可以列出任何數目的 blob，從零向上 tooa 設定最大值。</span><span class="sxs-lookup"><span data-stu-id="22146-178">Any number of blobs can be listed, from zero up tooa set maximum.</span></span> <span data-ttu-id="22146-179">即使這個方法會傳回零個結果，如果`results.continuationToken`不是 nil，可能有 hello 服務上未列出的多個 blob。</span><span class="sxs-lookup"><span data-stu-id="22146-179">Even if this method returns zero results, if `results.continuationToken` is not nil, there may be more blobs on hello service that have not been listed.</span></span>
* <span data-ttu-id="22146-180">**前置詞**-您可以指定 blob 清單的 hello 前置詞 toouse。</span><span class="sxs-lookup"><span data-stu-id="22146-180">**prefix** - You can specify hello prefix toouse for blob listing.</span></span> <span data-ttu-id="22146-181">只有開頭為此前置詞的 Blob 才會列出。</span><span class="sxs-lookup"><span data-stu-id="22146-181">Only blobs that begin with this prefix will be listed.</span></span>
* <span data-ttu-id="22146-182">**useFlatBlobListing** -hello 中所述[命名和參考容器和 blob](#naming-and-referencing-containers-and-blobs)  區段中，雖然 hello Blob 服務是一般儲存體配置，您可以建立虛擬階層所命名的 blob 路徑資訊。</span><span class="sxs-lookup"><span data-stu-id="22146-182">**useFlatBlobListing** - As mentioned in hello [Naming and referencing containers and blobs](#naming-and-referencing-containers-and-blobs) section, although hello Blob service is a flat storage scheme, you can create a virtual hierarchy by naming blobs with path information.</span></span> <span data-ttu-id="22146-183">不過目前不支援非一般列出。</span><span class="sxs-lookup"><span data-stu-id="22146-183">However, non-flat listing is currently not supported.</span></span> <span data-ttu-id="22146-184">不久後將有此功能。</span><span class="sxs-lookup"><span data-stu-id="22146-184">This feature is coming soon.</span></span> <span data-ttu-id="22146-185">目前，此值應為 **YES**。</span><span class="sxs-lookup"><span data-stu-id="22146-185">For now, this value should be **YES**.</span></span>
* <span data-ttu-id="22146-186">**blobListingDetails** -列出 blob 時，您可以指定哪些項目 tooinclude</span><span class="sxs-lookup"><span data-stu-id="22146-186">**blobListingDetails** - You can specify which items tooinclude when listing blobs</span></span>
  * <span data-ttu-id="22146-187">_AZSBlobListingDetailsNone_：僅列出已認可的 Blob，且不傳回 Blob 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="22146-187">_AZSBlobListingDetailsNone_: List only committed blobs, and do not return blob metadata.</span></span>
  * <span data-ttu-id="22146-188">_AZSBlobListingDetailsSnapshots_︰列出已認可的 Blob 和 Blob 快照。</span><span class="sxs-lookup"><span data-stu-id="22146-188">_AZSBlobListingDetailsSnapshots_: List committed blobs and blob snapshots.</span></span>
  * <span data-ttu-id="22146-189">_AZSBlobListingDetailsMetadata_: hello 清單中傳回擷取每一個 blob 的 blob 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="22146-189">_AZSBlobListingDetailsMetadata_: Retrieve blob metadata for each blob returned in hello listing.</span></span>
  * <span data-ttu-id="22146-190">_AZSBlobListingDetailsUncommittedBlobs_︰列出已認可和未認可的 Blob。</span><span class="sxs-lookup"><span data-stu-id="22146-190">_AZSBlobListingDetailsUncommittedBlobs_: List committed and uncommitted blobs.</span></span>
  * <span data-ttu-id="22146-191">_AZSBlobListingDetailsCopy_： 包含複製 hello 清單中的屬性。</span><span class="sxs-lookup"><span data-stu-id="22146-191">_AZSBlobListingDetailsCopy_: Include copy properties in hello listing.</span></span>
  * <span data-ttu-id="22146-192">_AZSBlobListingDetailsAll_：列出所有可用的已認可 Blob、未認可的 Blob 和快照，並傳回這些 Blob 的所有中繼資料和複製狀態。</span><span class="sxs-lookup"><span data-stu-id="22146-192">_AZSBlobListingDetailsAll_: List all available committed blobs, uncommitted blobs, and snapshots, and return all metadata and copy status for those blobs.</span></span>
* <span data-ttu-id="22146-193">**maxResults** -hello 結果 tooreturn 這項作業的最大數目。</span><span class="sxs-lookup"><span data-stu-id="22146-193">**maxResults** - hello maximum number of results tooreturn for this operation.</span></span> <span data-ttu-id="22146-194">使用-1 toonot 設定的限制。</span><span class="sxs-lookup"><span data-stu-id="22146-194">Use -1 toonot set a limit.</span></span>
* <span data-ttu-id="22146-195">**completionHandler** -hello 區塊的程式碼 tooexecute hello 的 hello 列出作業的結果。</span><span class="sxs-lookup"><span data-stu-id="22146-195">**completionHandler** - hello block of code tooexecute with hello results of hello listing operation.</span></span>

<span data-ttu-id="22146-196">在此範例中，協助程式方法是使用的 toorecursively 呼叫 hello 清單 blob 方法每次會傳回接續 token。</span><span class="sxs-lookup"><span data-stu-id="22146-196">In this example, a helper method is used toorecursively call hello list blobs method every time a continuation token is returned.</span></span>

```objc
-(void)listBlobsInContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    //List all blobs in container
    [self listBlobsInContainerHelper:blobContainer continuationToken:nil prefix:nil blobListingDetails:AZSBlobListingDetailsAll maxResults:-1 completionHandler:^(NSError *error) {
        if (error != nil){
            NSLog(@"Error in creating container.");
        }
    }];
}

//List blobs helper method
-(void)listBlobsInContainerHelper:(AZSCloudBlobContainer *)container continuationToken:(AZSContinuationToken *)continuationToken prefix:(NSString *)prefix blobListingDetails:(AZSBlobListingDetails)blobListingDetails maxResults:(NSUInteger)maxResults completionHandler:(void (^)(NSError *))completionHandler
{
    [container listBlobsSegmentedWithContinuationToken:continuationToken prefix:prefix useFlatBlobListing:YES blobListingDetails:blobListingDetails maxResults:maxResults completionHandler:^(NSError *error, AZSBlobResultSegment *results) {
        if (error)
        {
            completionHandler(error);
        }
        else
        {
            for (int i = 0; i < results.blobs.count; i++) {
                NSLog(@"%@",[(AZSCloudBlockBlob *)results.blobs[i] blobName]);
            }
            if (results.continuationToken)
            {
                [self listBlobsInContainerHelper:container continuationToken:results.continuationToken prefix:prefix blobListingDetails:blobListingDetails maxResults:maxResults completionHandler:completionHandler];
            }
            else
            {
                completionHandler(nil);
            }
        }
    }];
}
```

## <a name="download-a-blob"></a><span data-ttu-id="22146-197">下載 Blob</span><span class="sxs-lookup"><span data-stu-id="22146-197">Download a blob</span></span>
<span data-ttu-id="22146-198">下列範例會示範如何 hello toodownload blob tooa NSString 物件。</span><span class="sxs-lookup"><span data-stu-id="22146-198">hello following example shows how toodownload a blob tooa NSString object.</span></span>

```objc
-(void)downloadBlobToString{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Create a local blob object
    AZSCloudBlockBlob *blockBlob = [blobContainer blockBlobReferenceFromName:@"sampleblob"];

    // Download blob
    [blockBlob downloadToTextWithCompletionHandler:^(NSError *error, NSString *text) {
        if (error) {
            NSLog(@"Error in downloading blob");
        }
        else{
            NSLog(@"%@",text);
        }
    }];
}
```

## <a name="delete-a-blob"></a><span data-ttu-id="22146-199">刪除 Blob</span><span class="sxs-lookup"><span data-stu-id="22146-199">Delete a blob</span></span>
<span data-ttu-id="22146-200">下列範例會示範如何 hello toodelete blob。</span><span class="sxs-lookup"><span data-stu-id="22146-200">hello following example shows how toodelete a blob.</span></span>

```objc
-(void)deleteBlob{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Create a local blob object
    AZSCloudBlockBlob *blockBlob = [blobContainer blockBlobReferenceFromName:@"sampleblob1"];

    // Delete blob
    [blockBlob deleteWithCompletionHandler:^(NSError *error) {
        if (error) {
            NSLog(@"Error in deleting blob.");
        }
    }];
}
```

## <a name="delete-a-blob-container"></a><span data-ttu-id="22146-201">刪除 Blob 容器</span><span class="sxs-lookup"><span data-stu-id="22146-201">Delete a blob container</span></span>
<span data-ttu-id="22146-202">下列範例會示範如何 hello toodelete 容器。</span><span class="sxs-lookup"><span data-stu-id="22146-202">hello following example shows how toodelete a container.</span></span>

```objc
-(void)deleteContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Delete container
    [blobContainer deleteContainerIfExistsWithCompletionHandler:^(NSError *error, BOOL success) {
        if(error){
            NSLog(@"Error in deleting container");
        }
    }];
}
```

## <a name="next-steps"></a><span data-ttu-id="22146-203">後續步驟</span><span class="sxs-lookup"><span data-stu-id="22146-203">Next steps</span></span>
<span data-ttu-id="22146-204">既然您已經學會如何 toouse Blob 儲存體從 iOS，請遵循這些連結 toolearn 更多關於 hello iOS 的程式庫及 hello 儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="22146-204">Now that you've learned how toouse Blob Storage from iOS, follow these links toolearn more about hello iOS library and hello Storage service.</span></span>

* [<span data-ttu-id="22146-205">Azure Storage Client Library for iOS</span><span class="sxs-lookup"><span data-stu-id="22146-205">Azure Storage Client Library for iOS</span></span>](https://github.com/azure/azure-storage-ios)
* [<span data-ttu-id="22146-206">Azure 儲存體 iOS 參考文件</span><span class="sxs-lookup"><span data-stu-id="22146-206">Azure Storage iOS Reference Documentation</span></span>](http://azure.github.io/azure-storage-ios/)
* [<span data-ttu-id="22146-207">Azure 儲存體服務 REST API</span><span class="sxs-lookup"><span data-stu-id="22146-207">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="22146-208">Azure 儲存體團隊部落格</span><span class="sxs-lookup"><span data-stu-id="22146-208">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage)

<span data-ttu-id="22146-209">如果您有此文件庫有關的問題，則可以免費 toopost tooour [MSDN Azure 論壇](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata)或[堆疊溢位](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files)。</span><span class="sxs-lookup"><span data-stu-id="22146-209">If you have questions regarding this library, feel free toopost tooour [MSDN Azure forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) or [Stack Overflow](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).</span></span>
<span data-ttu-id="22146-210">如果您有 Azure 儲存體的功能建議，請張貼太[Azure 儲存體的意見反應](https://feedback.azure.com/forums/217298-storage/)。</span><span class="sxs-lookup"><span data-stu-id="22146-210">If you have feature suggestions for Azure Storage, please post too[Azure Storage Feedback](https://feedback.azure.com/forums/217298-storage/).</span></span>

