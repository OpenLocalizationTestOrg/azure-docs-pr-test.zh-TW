---
title: "如何使用 iOS 中的 Azure Blob 儲存體 | Microsoft Docs"
description: "使用 Azure Blob 儲存體 (物件儲存體) 在雲端中儲存非結構化資料。"
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
ms.openlocfilehash: cb2810636c8c23dbd476dc2adf58b17d1887d575
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-blob-storage-from-ios"></a><span data-ttu-id="93735-103">如何使用 iOS 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="93735-103">How to use Blob storage from iOS</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="93735-104">Overview</span><span class="sxs-lookup"><span data-stu-id="93735-104">Overview</span></span>
<span data-ttu-id="93735-105">本文將示範如何使用 Microsoft Azure Blob 儲存體執行一般案例。</span><span class="sxs-lookup"><span data-stu-id="93735-105">This article will show you how to perform common scenarios using Microsoft Azure Blob storage.</span></span> <span data-ttu-id="93735-106">這些範例均以 Objective-C 撰寫，並使用 [Azure Storage Client Library for iOS](https://github.com/Azure/azure-storage-ios)。</span><span class="sxs-lookup"><span data-stu-id="93735-106">The samples are written in Objective-C and use the [Azure Storage Client Library for iOS](https://github.com/Azure/azure-storage-ios).</span></span> <span data-ttu-id="93735-107">所涵蓋的案例包括**上傳**、**列出**、**下載**及**刪除** Blob。</span><span class="sxs-lookup"><span data-stu-id="93735-107">The scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="93735-108">如需 Blob 的詳細資訊，請參閱 [後續步驟](#next-steps) 一節。</span><span class="sxs-lookup"><span data-stu-id="93735-108">For more information on blobs, see the [Next Steps](#next-steps) section.</span></span> <span data-ttu-id="93735-109">您也可以下載 [範例應用程式](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) ，以快速查看在 iOS 應用程式中使用 Azure 儲存體的方法。</span><span class="sxs-lookup"><span data-stu-id="93735-109">You can also download the [sample app](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) to quickly see the use of Azure Storage in an iOS application.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="import-the-azure-storage-ios-library-into-your-application"></a><span data-ttu-id="93735-110">將 Azure 儲存體 iOS 程式庫匯入您的應用程式中</span><span class="sxs-lookup"><span data-stu-id="93735-110">Import the Azure Storage iOS library into your application</span></span>
<span data-ttu-id="93735-111">您可以透過使用 [Azure 儲存體 CocoaPod](https://cocoapods.org/pods/AZSClient) 或匯入 **Framework** 檔，將 Azure 儲存體 iOS 程式庫匯入至您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="93735-111">You can import the Azure Storage iOS library into your application either by using the [Azure Storage CocoaPod](https://cocoapods.org/pods/AZSClient) or by importing the **Framework** file.</span></span> <span data-ttu-id="93735-112">CocoaPod 是建議的方式，因為它讓程式庫整合更容易，不過從架構匯入檔案較不干擾您的現有專案。</span><span class="sxs-lookup"><span data-stu-id="93735-112">CocoaPod is the recommended way as it makes integrating the library easier, however importing from the framework file is less intrusive for your existing project.</span></span>

<span data-ttu-id="93735-113">若要使用此程式庫，您需要：</span><span class="sxs-lookup"><span data-stu-id="93735-113">To use this library, you need the following:</span></span>
- <span data-ttu-id="93735-114">iOS 8+</span><span class="sxs-lookup"><span data-stu-id="93735-114">iOS 8+</span></span>
- <span data-ttu-id="93735-115">Xcode 7+</span><span class="sxs-lookup"><span data-stu-id="93735-115">Xcode 7+</span></span>

## <a name="cocoapod"></a><span data-ttu-id="93735-116">CocoaPod</span><span class="sxs-lookup"><span data-stu-id="93735-116">CocoaPod</span></span>
1. <span data-ttu-id="93735-117">如果您還沒有這麼做，請開啟終端機視窗，並執行下列命令，在電腦上 [安裝 CocoaPods](https://guides.cocoapods.org/using/getting-started.html#toc_3)</span><span class="sxs-lookup"><span data-stu-id="93735-117">If you haven't done so already, [Install CocoaPods](https://guides.cocoapods.org/using/getting-started.html#toc_3) on your computer by opening a terminal window and running the following command</span></span>
    
    ```shell   
    sudo gem install cocoapods
    ```

2. <span data-ttu-id="93735-118">接下來，在專案目錄 (包含您 .xcodeproj 檔案的目錄) 中建立稱為 _Podfile_ 的檔案 (無副檔名)。</span><span class="sxs-lookup"><span data-stu-id="93735-118">Next, in the project directory (the directory containing your .xcodeproj file), create a new file called _Podfile_(no file extension).</span></span> <span data-ttu-id="93735-119">將下列內容加入至 _Podfile_ 並儲存。</span><span class="sxs-lookup"><span data-stu-id="93735-119">Add the following to _Podfile_ and save.</span></span>

    ```ruby
    platform :ios, '8.0'

    target 'TargetName' do
      pod 'AZSClient'
    end
    ```

3. <span data-ttu-id="93735-120">在終端機視窗中，巡覽至專案目錄並執行下列命令</span><span class="sxs-lookup"><span data-stu-id="93735-120">In the terminal window, navigate to the project directory and run the following command</span></span>

    ```shell    
    pod install
    ```

4. <span data-ttu-id="93735-121">如果您已在 Xcode 中開啟 .xcodeproj，請將它關閉。</span><span class="sxs-lookup"><span data-stu-id="93735-121">If your .xcodeproj is open in Xcode, close it.</span></span> <span data-ttu-id="93735-122">在您的專案目錄中開啟新建立的專案檔案 (副檔名為 .xcworkspace)。</span><span class="sxs-lookup"><span data-stu-id="93735-122">In your project directory open the newly created project file which will have the .xcworkspace extension.</span></span> <span data-ttu-id="93735-123">這是您從現在開始會使用的檔案。</span><span class="sxs-lookup"><span data-stu-id="93735-123">This is the file you'll work from for now on.</span></span>

## <a name="framework"></a><span data-ttu-id="93735-124">Framework</span><span class="sxs-lookup"><span data-stu-id="93735-124">Framework</span></span>
<span data-ttu-id="93735-125">程式庫的另一個用法，是手動建立架構︰</span><span class="sxs-lookup"><span data-stu-id="93735-125">The other way to use the library is to build the framework manually:</span></span>

1. <span data-ttu-id="93735-126">首先，請下載或複製 [azure-storage-ios repo](https://github.com/azure/azure-storage-ios)。</span><span class="sxs-lookup"><span data-stu-id="93735-126">First, download or clone the [azure-storage-ios repo](https://github.com/azure/azure-storage-ios).</span></span>
2. <span data-ttu-id="93735-127">移至 *azure-storage-ios* -> *Lib* -> *Azure 儲存體用戶端程式庫*，然後在 Xcode 中開啟 `AZSClient.xcodeproj`。</span><span class="sxs-lookup"><span data-stu-id="93735-127">Go into *azure-storage-ios* -> *Lib* -> *Azure Storage Client Library*, and open `AZSClient.xcodeproj` in Xcode.</span></span>
3. <span data-ttu-id="93735-128">在 Xcode 左上方，將作用中配置從「Azure 儲存體用戶端程式庫」變更為「架構」。</span><span class="sxs-lookup"><span data-stu-id="93735-128">At the top-left of Xcode, change the active scheme from "Azure Storage Client Library" to "Framework".</span></span>
4. <span data-ttu-id="93735-129">建置專案 (⌘ + B)。</span><span class="sxs-lookup"><span data-stu-id="93735-129">Build the project (⌘+B).</span></span> <span data-ttu-id="93735-130">這會在您的桌面上建立 `AZSClient.framework` 檔案。</span><span class="sxs-lookup"><span data-stu-id="93735-130">This will create an `AZSClient.framework` file on your Desktop.</span></span>

<span data-ttu-id="93735-131">您可以透過下列方式，將 Framework 檔案匯入至您的應用程式：</span><span class="sxs-lookup"><span data-stu-id="93735-131">You can then import the framework file into your application by doing the following:</span></span>

1. <span data-ttu-id="93735-132">建立新的專案，或在 Xcode 中開啟現有的專案。</span><span class="sxs-lookup"><span data-stu-id="93735-132">Create a new project or open up your existing project in Xcode.</span></span>
2. <span data-ttu-id="93735-133">將 `AZSClient.framework` 拖曳到您的 Xcode 專案導覽器。</span><span class="sxs-lookup"><span data-stu-id="93735-133">Drag and drop the `AZSClient.framework` into your Xcode project navigator.</span></span>
3. <span data-ttu-id="93735-134">選取 [必要時複製項目]，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="93735-134">Select *Copy items if needed*, and click on *Finish*.</span></span>
4. <span data-ttu-id="93735-135">按一下左側導覽列中的專案，然後按一下專案編輯器頂端的 [一般]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="93735-135">Click on your project in the left-hand navigation and click the *General* tab at the top of the project editor.</span></span>
5. <span data-ttu-id="93735-136">在 [連結的架構和程式庫]  區段下，按一下 [新增] 按鈕 (+)。</span><span class="sxs-lookup"><span data-stu-id="93735-136">Under the *Linked Frameworks and Libraries* section, click the Add button (+).</span></span>
6. <span data-ttu-id="93735-137">在已提供的程式庫清單中搜尋 `libxml2.2.tbd` ，並將它新增至您的專案。</span><span class="sxs-lookup"><span data-stu-id="93735-137">In the list of libraries already provided, search for `libxml2.2.tbd` and add it to your project.</span></span>

## <a name="import-the-library"></a><span data-ttu-id="93735-138">匯入程式庫</span><span class="sxs-lookup"><span data-stu-id="93735-138">Import the Library</span></span> 
```objc
// Include the following import statement to use blob APIs.
#import <AZSClient/AZSClient.h>
```

<span data-ttu-id="93735-139">如果您使用 Swift，必須建立橋接標頭並在標頭匯入 <AZSClient/AZSClient.h>︰</span><span class="sxs-lookup"><span data-stu-id="93735-139">If you are using Swift, you will need to create a bridging header and import <AZSClient/AZSClient.h> there:</span></span>

1. <span data-ttu-id="93735-140">建立標頭檔 `Bridging-Header.h`，並加入上述匯入陳述式。</span><span class="sxs-lookup"><span data-stu-id="93735-140">Create a header file `Bridging-Header.h`, and add the above import statement.</span></span>
2. <span data-ttu-id="93735-141">移至 [建置設定] 索引標籤，搜尋[OBJECTIVE-C 橋接標頭]。</span><span class="sxs-lookup"><span data-stu-id="93735-141">Go to the *Build Settings* tab, and search for *Objective-C Bridging Header*.</span></span>
3. <span data-ttu-id="93735-142">按兩下 [OBJECTIVE-C 橋接標頭] 欄位，並將此路徑加入標頭檔︰`ProjectName/Bridging-Header.h`</span><span class="sxs-lookup"><span data-stu-id="93735-142">Double-click on the field of *Objective-C Bridging Header* and add the path to your header file: `ProjectName/Bridging-Header.h`</span></span>
4. <span data-ttu-id="93735-143">建立專案 (⌘ + B) 以確認 Xcode 已收取橋接標頭。</span><span class="sxs-lookup"><span data-stu-id="93735-143">Build the project (⌘+B) to verify that the bridging header was picked up by Xcode.</span></span>
5. <span data-ttu-id="93735-144">直接在任何 Swift 檔案中開始使用程式庫，就不需要匯入陳述式。</span><span class="sxs-lookup"><span data-stu-id="93735-144">Start using the library directly in any Swift file, there is no need for import statements.</span></span>

[!INCLUDE [storage-mobile-authentication-guidance](../../includes/storage-mobile-authentication-guidance.md)]

## <a name="asynchronous-operations"></a><span data-ttu-id="93735-145">非同步作業</span><span class="sxs-lookup"><span data-stu-id="93735-145">Asynchronous Operations</span></span>
> [!NOTE]
> <span data-ttu-id="93735-146">所有對服務執行要求的方法，都是非同步作業。</span><span class="sxs-lookup"><span data-stu-id="93735-146">All methods that perform a request against the service are asynchronous operations.</span></span> <span data-ttu-id="93735-147">在程式碼範例中，您會發現這些方法具有完成處理常式。</span><span class="sxs-lookup"><span data-stu-id="93735-147">In the code samples, you'll find that these methods have a completion handler.</span></span> <span data-ttu-id="93735-148">完成處理常式內的程式碼會在要求完成 **之後** 執行。</span><span class="sxs-lookup"><span data-stu-id="93735-148">Code inside the completion handler will run **after** the request is completed.</span></span> <span data-ttu-id="93735-149">完成處理常式後面的程式碼會在進行要求 **期間** 執行。</span><span class="sxs-lookup"><span data-stu-id="93735-149">Code after the completion handler will run **while** the request is being made.</span></span>
> 
> 

## <a name="create-a-container"></a><span data-ttu-id="93735-150">建立容器</span><span class="sxs-lookup"><span data-stu-id="93735-150">Create a container</span></span>
<span data-ttu-id="93735-151">儲存體 Blob 中的每個 Blob 必須位於一個容器中。</span><span class="sxs-lookup"><span data-stu-id="93735-151">Every blob in Azure Storage must reside in a container.</span></span> <span data-ttu-id="93735-152">下列範例說明如何在您的儲存體帳戶中建立名為 *newcontainer*的容器 (如果還不存在)。</span><span class="sxs-lookup"><span data-stu-id="93735-152">The following example shows how to create a container, called *newcontainer*, in your Storage account if it doesn't already exist.</span></span> <span data-ttu-id="93735-153">為您的容器選擇名稱時，請留意上面提到的命名規則。</span><span class="sxs-lookup"><span data-stu-id="93735-153">When choosing a name for your container, be mindful of the naming rules mentioned above.</span></span>

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

    // Create container in your Storage account if the container doesn't already exist
    [blobContainer createContainerIfNotExistsWithCompletionHandler:^(NSError *error, BOOL exists) {
        if (error){
            NSLog(@"Error in creating container.");
        }
    }];
}
```

<span data-ttu-id="93735-154">您可以查看 [Microsoft Azure 儲存體總管](http://storageexplorer.com) ，並驗證 *newcontainer* 位於儲存體帳戶的容器清單中，以確認運作正常。</span><span class="sxs-lookup"><span data-stu-id="93735-154">You can confirm that this works by looking at the [Microsoft Azure Storage Explorer](http://storageexplorer.com) and verifying that *newcontainer* is in the list of containers for your Storage account.</span></span>

## <a name="set-container-permissions"></a><span data-ttu-id="93735-155">設定容器權限</span><span class="sxs-lookup"><span data-stu-id="93735-155">Set Container Permissions</span></span>
<span data-ttu-id="93735-156">依預設會針對 [私人]  存取設定容器的權限。</span><span class="sxs-lookup"><span data-stu-id="93735-156">A container's permissions are configured for **Private** access by default.</span></span> <span data-ttu-id="93735-157">不過，容器會提供幾個不同的容器存取選項：</span><span class="sxs-lookup"><span data-stu-id="93735-157">However, containers provide a few different options for container access:</span></span>

* <span data-ttu-id="93735-158">**私人**：只有帳戶擁有者可以讀取容器和 Blob 資料。</span><span class="sxs-lookup"><span data-stu-id="93735-158">**Private**: Container and blob data can be read by the account owner only.</span></span>
* <span data-ttu-id="93735-159">**Blob**：您可以透過匿名要求讀取此容器內的 Blob 資料，但您無法使用容器資料。</span><span class="sxs-lookup"><span data-stu-id="93735-159">**Blob**: Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="93735-160">用戶端無法透過匿名要求列舉容器內的 Blob。</span><span class="sxs-lookup"><span data-stu-id="93735-160">Clients cannot enumerate blobs within the container via anonymous request.</span></span>
* <span data-ttu-id="93735-161">**容器**：可以透過匿名要求讀取容器和 Blob 資料。</span><span class="sxs-lookup"><span data-stu-id="93735-161">**Container**: Container and blob data can be read via anonymous request.</span></span> <span data-ttu-id="93735-162">用戶端可以透過匿名要求列舉容器內的 Blob，但無法列舉儲存體帳戶內的容器。</span><span class="sxs-lookup"><span data-stu-id="93735-162">Clients can enumerate blobs within the container via anonymous request, but cannot enumerate containers within the storage account.</span></span>

<span data-ttu-id="93735-163">下列範例說明如何建立具有 [容器]  存取權限，而允許網際網路上的所有使用者進行公用、唯讀存取的容器：</span><span class="sxs-lookup"><span data-stu-id="93735-163">The following example shows you how to create a container with **Container** access permissions, which will allow public, read-only access for all users on the Internet:</span></span>

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

    // Create container in your Storage account if the container doesn't already exist
    [blobContainer createContainerIfNotExistsWithAccessType:AZSContainerPublicAccessTypeContainer requestOptions:nil operationContext:nil completionHandler:^(NSError *error, BOOL exists){
        if (error){
            NSLog(@"Error in creating container.");
        }
    }];
}
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="93735-164">將 Blob 上傳至容器</span><span class="sxs-lookup"><span data-stu-id="93735-164">Upload a blob into a container</span></span>
<span data-ttu-id="93735-165">如 [Blob 服務概念](#blob-service-concepts) 一節中所述，Blob 儲存體提供三種不同類型的 Blob：區塊 Blob、附加 Blob 和分頁 Blob。</span><span class="sxs-lookup"><span data-stu-id="93735-165">As mentioned in the [Blob service concepts](#blob-service-concepts) section, Blob Storage offers three different types of blobs: block blobs, append blobs, and page blobs.</span></span> <span data-ttu-id="93735-166">Azure 儲存體 iOS 程式庫支援三種類型的 Blob。</span><span class="sxs-lookup"><span data-stu-id="93735-166">The Azure Storage iOS library supports all three types of blobs.</span></span> <span data-ttu-id="93735-167">在大部分情況下，建議使用區塊 Blob 的類型。</span><span class="sxs-lookup"><span data-stu-id="93735-167">In most cases, block blob is the recommended type to use.</span></span>

<span data-ttu-id="93735-168">下列範例說明如何從 NSString 上傳區塊 Blob。</span><span class="sxs-lookup"><span data-stu-id="93735-168">The following example shows how to upload a block blob from an NSString.</span></span> <span data-ttu-id="93735-169">如果此容器中有相同名稱的 Blob 存在，此 Blob 的內容將會被覆寫。</span><span class="sxs-lookup"><span data-stu-id="93735-169">If a blob with the same name already exists in this container, the contents of this blob will be overwritten.</span></span>

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

                // Upload blob to Storage
                [blockBlob uploadFromText:@"This text will be uploaded to Blob Storage." completionHandler:^(NSError *error) {
                    if (error){
                        NSLog(@"Error in creating blob.");
                    }
                }];
            }
        }];
}
```

<span data-ttu-id="93735-170">您可以查看 [Microsoft Azure 儲存體總管](http://storageexplorer.com)，並驗證容器 *containerpublic* 包含 Blob *sampleblob*，以確認運作正常。</span><span class="sxs-lookup"><span data-stu-id="93735-170">You can confirm that this works by looking at the [Microsoft Azure Storage Explorer](http://storageexplorer.com) and verifying that the container, *containerpublic*, contains the blob, *sampleblob*.</span></span> <span data-ttu-id="93735-171">在此範例中我們使用公用容器，所以您也可以移至 Blob URI 來確認應用程式運作是否正常：</span><span class="sxs-lookup"><span data-stu-id="93735-171">In this sample, we used a public container so you can also verify that this application worked by going to the blobs URI:</span></span>

    https://nameofyourstorageaccount.blob.core.windows.net/containerpublic/sampleblob

<span data-ttu-id="93735-172">除了從 NSString 上傳區塊 Blob 以外，NSData、NSInputStream 或本機檔案也有類似的方法。</span><span class="sxs-lookup"><span data-stu-id="93735-172">In addition to uploading a block blob from an NSString, similar methods exist for NSData, NSInputStream, or a local file.</span></span>

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="93735-173">列出容器中的 Blob</span><span class="sxs-lookup"><span data-stu-id="93735-173">List the blobs in a container</span></span>
<span data-ttu-id="93735-174">下列範例說明如何列出容器中的所有 Blob。</span><span class="sxs-lookup"><span data-stu-id="93735-174">The following example shows how to list all blobs in a container.</span></span> <span data-ttu-id="93735-175">執行此作業時，請留意下列參數：</span><span class="sxs-lookup"><span data-stu-id="93735-175">When performing this operation, be mindful of the following parameters:</span></span>     

* <span data-ttu-id="93735-176">**continuationToken** - 接續權杖表示列出作業應從哪裡開始。</span><span class="sxs-lookup"><span data-stu-id="93735-176">**continuationToken** - The continuation token represents where the listing operation should start.</span></span> <span data-ttu-id="93735-177">如果未提供權杖，則會從頭列出 Blob。</span><span class="sxs-lookup"><span data-stu-id="93735-177">If no token is provided, it will list blobs from the beginning.</span></span> <span data-ttu-id="93735-178">可以列出任何數目的 Blob，從零到設定的最大值皆可。</span><span class="sxs-lookup"><span data-stu-id="93735-178">Any number of blobs can be listed, from zero up to a set maximum.</span></span> <span data-ttu-id="93735-179">即使此方法傳回零個結果，如果 `results.continuationToken` 不是 nil，則可能會有服務上的更多 Blob 未列出。</span><span class="sxs-lookup"><span data-stu-id="93735-179">Even if this method returns zero results, if `results.continuationToken` is not nil, there may be more blobs on the service that have not been listed.</span></span>
* <span data-ttu-id="93735-180">**prefix** -您可以指定要用於 Blob 列出作業的前置詞。</span><span class="sxs-lookup"><span data-stu-id="93735-180">**prefix** - You can specify the prefix to use for blob listing.</span></span> <span data-ttu-id="93735-181">只有開頭為此前置詞的 Blob 才會列出。</span><span class="sxs-lookup"><span data-stu-id="93735-181">Only blobs that begin with this prefix will be listed.</span></span>
* <span data-ttu-id="93735-182">**useFlatBlobListing** - 如 [命名與參考容器和 Blob](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata) 一節中所述，雖然 Blob 服務是一般儲存體配置，雖然您可以路徑資訊為 Blob 命名，以建立虛擬階層。</span><span class="sxs-lookup"><span data-stu-id="93735-182">**useFlatBlobListing** - As mentioned in the [Naming and referencing containers and blobs](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata) section, although the Blob service is a flat storage scheme, you can create a virtual hierarchy by naming blobs with path information.</span></span> <span data-ttu-id="93735-183">不過目前不支援非一般列出。</span><span class="sxs-lookup"><span data-stu-id="93735-183">However, non-flat listing is currently not supported.</span></span> <span data-ttu-id="93735-184">不久後將有此功能。</span><span class="sxs-lookup"><span data-stu-id="93735-184">This feature is coming soon.</span></span> <span data-ttu-id="93735-185">目前，此值應為 **YES**。</span><span class="sxs-lookup"><span data-stu-id="93735-185">For now, this value should be **YES**.</span></span>

* <span data-ttu-id="93735-186">**blobListingDetails** - 您可以指定列出 Blob 時所要包含的項目</span><span class="sxs-lookup"><span data-stu-id="93735-186">**blobListingDetails** - You can specify which items to include when listing blobs</span></span>
  * <span data-ttu-id="93735-187">_AZSBlobListingDetailsNone_：僅列出已認可的 Blob，且不傳回 Blob 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="93735-187">_AZSBlobListingDetailsNone_: List only committed blobs, and do not return blob metadata.</span></span>
  * <span data-ttu-id="93735-188">_AZSBlobListingDetailsSnapshots_︰列出已認可的 Blob 和 Blob 快照。</span><span class="sxs-lookup"><span data-stu-id="93735-188">_AZSBlobListingDetailsSnapshots_: List committed blobs and blob snapshots.</span></span>
  * <span data-ttu-id="93735-189">_AZSBlobListingDetailsMetadata_：為清單中傳回的每個 Blob 擷取 Blob 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="93735-189">_AZSBlobListingDetailsMetadata_: Retrieve blob metadata for each blob returned in the listing.</span></span>
  * <span data-ttu-id="93735-190">_AZSBlobListingDetailsUncommittedBlobs_︰列出已認可和未認可的 Blob。</span><span class="sxs-lookup"><span data-stu-id="93735-190">_AZSBlobListingDetailsUncommittedBlobs_: List committed and uncommitted blobs.</span></span>
  * <span data-ttu-id="93735-191">_AZSBlobListingDetailsCopy_：在清單中包含複製屬性。</span><span class="sxs-lookup"><span data-stu-id="93735-191">_AZSBlobListingDetailsCopy_: Include copy properties in the listing.</span></span>
  * <span data-ttu-id="93735-192">_AZSBlobListingDetailsAll_：列出所有可用的已認可 Blob、未認可的 Blob 和快照，並傳回這些 Blob 的所有中繼資料和複製狀態。</span><span class="sxs-lookup"><span data-stu-id="93735-192">_AZSBlobListingDetailsAll_: List all available committed blobs, uncommitted blobs, and snapshots, and return all metadata and copy status for those blobs.</span></span>
* <span data-ttu-id="93735-193">**maxResults** - 要為此作業傳回的結果數目上限。</span><span class="sxs-lookup"><span data-stu-id="93735-193">**maxResults** - The maximum number of results to return for this operation.</span></span> <span data-ttu-id="93735-194">使用 -1 則不會設定限制。</span><span class="sxs-lookup"><span data-stu-id="93735-194">Use -1 to not set a limit.</span></span>
* <span data-ttu-id="93735-195">**completionHandler** - 要執行的程式碼區塊與列出作業的結果。</span><span class="sxs-lookup"><span data-stu-id="93735-195">**completionHandler** - The block of code to execute with the results of the listing operation.</span></span>

<span data-ttu-id="93735-196">在此範例中，將會在每次傳回接續權杖時使用 Helper 方法以遞迴方式呼叫列出 Blob 方法。</span><span class="sxs-lookup"><span data-stu-id="93735-196">In this example, a helper method is used to recursively call the list blobs method every time a continuation token is returned.</span></span>

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

## <a name="download-a-blob"></a><span data-ttu-id="93735-197">下載 Blob</span><span class="sxs-lookup"><span data-stu-id="93735-197">Download a blob</span></span>
<span data-ttu-id="93735-198">下列範例說明如何將 Blob 下載到 NSString 物件。</span><span class="sxs-lookup"><span data-stu-id="93735-198">The following example shows how to download a blob to a NSString object.</span></span>

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

## <a name="delete-a-blob"></a><span data-ttu-id="93735-199">刪除 Blob</span><span class="sxs-lookup"><span data-stu-id="93735-199">Delete a blob</span></span>
<span data-ttu-id="93735-200">下列範例說明如何刪除 Blob。</span><span class="sxs-lookup"><span data-stu-id="93735-200">The following example shows how to delete a blob.</span></span>

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

## <a name="delete-a-blob-container"></a><span data-ttu-id="93735-201">刪除 Blob 容器</span><span class="sxs-lookup"><span data-stu-id="93735-201">Delete a blob container</span></span>
<span data-ttu-id="93735-202">下列範例說明如何刪除容器。</span><span class="sxs-lookup"><span data-stu-id="93735-202">The following example shows how to delete a container.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="93735-203">後續步驟</span><span class="sxs-lookup"><span data-stu-id="93735-203">Next steps</span></span>
<span data-ttu-id="93735-204">您現在已經了解如何從 iOS 中使用 Blob 儲存體，請參考下列連結以深入了解 iOS 程式庫和儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="93735-204">Now that you've learned how to use Blob Storage from iOS, follow these links to learn more about the iOS library and the Storage service.</span></span>

* [<span data-ttu-id="93735-205">Azure Storage Client Library for iOS</span><span class="sxs-lookup"><span data-stu-id="93735-205">Azure Storage Client Library for iOS</span></span>](https://github.com/azure/azure-storage-ios)
* [<span data-ttu-id="93735-206">Azure 儲存體 iOS 參考文件</span><span class="sxs-lookup"><span data-stu-id="93735-206">Azure Storage iOS Reference Documentation</span></span>](http://azure.github.io/azure-storage-ios/)
* [<span data-ttu-id="93735-207">Azure 儲存體服務 REST API</span><span class="sxs-lookup"><span data-stu-id="93735-207">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="93735-208">Azure 儲存體團隊部落格</span><span class="sxs-lookup"><span data-stu-id="93735-208">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage)

<span data-ttu-id="93735-209">如果您有關於此程式庫的問題，歡迎您貼文到我們的 [MSDN Azure 論壇](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata)或 [Stack Overflow](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files)。</span><span class="sxs-lookup"><span data-stu-id="93735-209">If you have questions regarding this library, feel free to post to our [MSDN Azure forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) or [Stack Overflow](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).</span></span>
<span data-ttu-id="93735-210">如果您有 Azure 儲存體功能方面的建議，請貼文到 [Azure 儲存體意見反應](https://feedback.azure.com/forums/217298-storage/)。</span><span class="sxs-lookup"><span data-stu-id="93735-210">If you have feature suggestions for Azure Storage, please post to [Azure Storage Feedback](https://feedback.azure.com/forums/217298-storage/).</span></span>

