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
# <a name="how-toouse-blob-storage-from-ios"></a>如何 toouse iOS 從 Blob 儲存體
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>概觀
這篇文章將示範如何使用 Microsoft Azure Blob 儲存體 tooperform 常見案例。 hello 範例以 OBJECTIVE-C 所撰寫並使用 hello[適用於 iOS 的 Azure 儲存體用戶端程式庫](https://github.com/Azure/azure-storage-ios)。 hello 涵蓋案例包括**上載**，**列出**，**下載**，和**刪除**blob。 如需有關 blob 的詳細資訊，請參閱 hello[接下來的步驟](#next-steps)> 一節。 您也可以下載 hello[範例應用程式](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample)tooquickly 看到 hello iOS 應用程式中的使用 Azure 儲存體。

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="import-hello-azure-storage-ios-library-into-your-application"></a>Hello Azure 儲存體 iOS 的程式庫匯入您的應用程式
Hello Azure 儲存體 iOS 的程式庫匯入您的應用程式使用 hello [Azure 儲存體 CocoaPod](https://cocoapods.org/pods/AZSClient)或匯入 hello **Framework**檔案。 CocoaPod 為建議的方式，因為它會讓整合 hello 庫較為簡單，不過匯入從 hello 架構檔案是較不干擾現有專案的 hello。

toouse 此程式庫，您需要遵循的 hello:
- iOS 8+
- Xcode 7+

## <a name="cocoapod"></a>CocoaPod
1. 如果您沒有這樣做，[安裝 CocoaPods](https://guides.cocoapods.org/using/getting-started.html#toc_3)上開啟終端機視窗，然後執行下列命令的 hello 電腦
    
    ```shell   
    sudo gem install cocoapods
    ```

2. 接下來，在 hello 專案目錄中 （hello 目錄包含.xcodeproj 檔案），建立新的檔案，稱為_Podfile_（沒有副檔名）。 新增下列 too_Podfile_ hello 和儲存。

    ```ruby
    platform :ios, '8.0'

    target 'TargetName' do
      pod 'AZSClient'
    end
    ```

3. 在 hello 終端機視窗，瀏覽 toohello 專案目錄並執行下列命令的 hello

    ```shell    
    pod install
    ```

4. 如果您已在 Xcode 中開啟 .xcodeproj，請將它關閉。 專案目錄開啟 hello 新建立的專案檔中將有 hello.xcworkspace 延伸模組。 這是您將從現在在運作的 hello 檔案。

## <a name="framework"></a>Framework
hello toouse hello 程式庫手動是 toobuild hello 架構，另一種方式：

1. 第一個、 下載或複製 hello [azure 儲存體 ios 儲存機制](https://github.com/azure/azure-storage-ios)。
2. 移至 *azure-storage-ios* -> *Lib* -> *Azure 儲存體用戶端程式庫*，然後在 Xcode 中開啟 `AZSClient.xcodeproj`。
3. 在 hello 左上方的 Xcode 變更 hello active 配置從 「 Azure 儲存體用戶端程式庫 」 太 < Framework >。
4. 建置 hello 專案 （⌘ + B）。 這會在您的桌面上建立 `AZSClient.framework` 檔案。

您接著可以 hello 架構檔案匯入您的應用程式執行 hello 下列：

1. 建立新的專案，或在 Xcode 中開啟現有的專案。
2. 拖放 hello`AZSClient.framework`到您的 Xcode 專案導覽器。
3. 選取 [必要時複製項目]，然後按一下 [完成]。
4. Hello 左側導覽中的專案上按一下，然後按一下 hello*一般*在 hello hello 專案編輯器頂端的索引標籤。
5. 在 [hello*連結架構和程式庫*區段中，按一下 hello 新增] 按鈕 （+）。
6. 在 [hello] 清單中已經提供的程式庫，搜尋`libxml2.2.tbd`並將它加入 tooyour 專案。

## <a name="import-hello-library"></a>匯入 hello 程式庫 
```objc
// Include hello following import statement toouse blob APIs.
#import <AZSClient/AZSClient.h>
```

如果您使用 Swift 時，您將需要 toocreate 橋接標頭，並那里匯入 < AZSClient/AZSClient.h >:

1. 建立標頭檔`Bridging-Header.h`，並加入 hello 上方匯入陳述式。
2. 移 toohello*組建設定*索引標籤，並搜尋*OBJECTIVE-C 橋接標頭*。
3. Hello 欄位上按兩下*OBJECTIVE-C 橋接標頭*將 hello 路徑 tooyour 標頭檔：`ProjectName/Bridging-Header.h`
4. Hello 橋接標頭的組建 hello 專案 （⌘ + B） tooverify Xcode 已收取。
5. 開始使用 hello 程式庫直接在任何 Swift 檔案中，不需要匯入陳述式。

[!INCLUDE [storage-mobile-authentication-guidance](../../../includes/storage-mobile-authentication-guidance.md)]

## <a name="asynchronous-operations"></a>非同步作業
> [!NOTE]
> 執行對 hello 服務提出之要求的所有方法都是非同步作業。 在 hello 程式碼範例中，您會發現這些方法已完成處理常式。 Hello 完成處理常式內部的程式碼會執行**之後**hello 要求完成。 程式碼會執行 hello 完成處理常式之後**時**hello 要求所針對。
> 
> 

## <a name="create-a-container"></a>建立容器
儲存體 Blob 中的每個 Blob 必須位於一個容器中。 hello 下列範例顯示如何 toocreate 容器使用時，呼叫*newcontainer*，在儲存體帳戶，如果不存在。 選擇您的容器的名稱，留意 hello 命名上面所述的規則。

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

您可以確認其運作藉由查看 hello [Microsoft Azure 儲存體總管](http://storageexplorer.com)並確認*newcontainer* hello 容器使用的儲存體帳戶清單中。

## <a name="set-container-permissions"></a>設定容器權限
依預設會針對 [私人]  存取設定容器的權限。 不過，容器會提供幾個不同的容器存取選項：

* **私用**: hello 帳戶擁有者可以讀取容器和 blob 資料。
* **Blob**：您可以透過匿名要求讀取此容器內的 Blob 資料，但您無法使用容器資料。 用戶端無法列舉 hello 透過匿名要求的容器中的 blob。
* **容器**：可以透過匿名要求讀取容器和 Blob 資料。 用戶端透過匿名要求，hello 容器內的 blob，但無法列舉 hello 儲存體帳戶中的容器。

hello 下列範例會示範如何與容器的 toocreate**容器**存取允許 hello 網際網路上的所有使用者公開的唯讀存取權限：

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

## <a name="upload-a-blob-into-a-container"></a>將 Blob 上傳至容器
Hello 中所述[Blob 服務概念](#blob-service-concepts) 區段中，Blob 儲存體提供三種不同的 blob： 區塊 blob、 附加 blob 和分頁 blob。 hello Azure 儲存體 iOS 的程式庫支援所有的三種類型的 blob。 在大部分情況下，區塊 blob 是建議的型別 toouse hello。

hello 下列範例會顯示從 NSString tooupload 區塊 blob 的方式。 如果此容器中已經有名稱相同的 hello 的 blob，此 blob 的 hello 內容會被覆寫。

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

您可以確認其運作藉由查看 hello [Microsoft Azure 儲存體總管](http://storageexplorer.com)及驗證 hello 程序*containerpublic*，包含 hello blob *sampleblob*. 在此範例中，我們會使用公用容器，因此您也可以驗證，此應用程式的工作移 toohello blob URI:

    https://nameofyourstorageaccount.blob.core.windows.net/containerpublic/sampleblob

此外 toouploading NSString 從區塊 blob，類似的方法有 NSData、 NSInputStream 或本機檔案。

## <a name="list-hello-blobs-in-a-container"></a>列出容器中的 hello blob
下列範例會示範如何 toolist 所有 blob 容器中的 hello。 當執行這項作業，請留意 hello 下列參數：     

* **continuationToken** -hello 接續 token 代表 hello 列出作業應該在此處開始。 如果未不提供任何 token，則它會列出從 hello 開頭的 blob。 可以列出任何數目的 blob，從零向上 tooa 設定最大值。 即使這個方法會傳回零個結果，如果`results.continuationToken`不是 nil，可能有 hello 服務上未列出的多個 blob。
* **前置詞**-您可以指定 blob 清單的 hello 前置詞 toouse。 只有開頭為此前置詞的 Blob 才會列出。
* **useFlatBlobListing** -hello 中所述[命名和參考容器和 blob](#naming-and-referencing-containers-and-blobs)  區段中，雖然 hello Blob 服務是一般儲存體配置，您可以建立虛擬階層所命名的 blob 路徑資訊。 不過目前不支援非一般列出。 不久後將有此功能。 目前，此值應為 **YES**。
* **blobListingDetails** -列出 blob 時，您可以指定哪些項目 tooinclude
  * _AZSBlobListingDetailsNone_：僅列出已認可的 Blob，且不傳回 Blob 中繼資料。
  * _AZSBlobListingDetailsSnapshots_︰列出已認可的 Blob 和 Blob 快照。
  * _AZSBlobListingDetailsMetadata_: hello 清單中傳回擷取每一個 blob 的 blob 中繼資料。
  * _AZSBlobListingDetailsUncommittedBlobs_︰列出已認可和未認可的 Blob。
  * _AZSBlobListingDetailsCopy_： 包含複製 hello 清單中的屬性。
  * _AZSBlobListingDetailsAll_：列出所有可用的已認可 Blob、未認可的 Blob 和快照，並傳回這些 Blob 的所有中繼資料和複製狀態。
* **maxResults** -hello 結果 tooreturn 這項作業的最大數目。 使用-1 toonot 設定的限制。
* **completionHandler** -hello 區塊的程式碼 tooexecute hello 的 hello 列出作業的結果。

在此範例中，協助程式方法是使用的 toorecursively 呼叫 hello 清單 blob 方法每次會傳回接續 token。

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

## <a name="download-a-blob"></a>下載 Blob
下列範例會示範如何 hello toodownload blob tooa NSString 物件。

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

## <a name="delete-a-blob"></a>刪除 Blob
下列範例會示範如何 hello toodelete blob。

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

## <a name="delete-a-blob-container"></a>刪除 Blob 容器
下列範例會示範如何 hello toodelete 容器。

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

## <a name="next-steps"></a>後續步驟
既然您已經學會如何 toouse Blob 儲存體從 iOS，請遵循這些連結 toolearn 更多關於 hello iOS 的程式庫及 hello 儲存體服務。

* [Azure Storage Client Library for iOS](https://github.com/azure/azure-storage-ios)
* [Azure 儲存體 iOS 參考文件](http://azure.github.io/azure-storage-ios/)
* [Azure 儲存體服務 REST API](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Azure 儲存體團隊部落格](http://blogs.msdn.com/b/windowsazurestorage)

如果您有此文件庫有關的問題，則可以免費 toopost tooour [MSDN Azure 論壇](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata)或[堆疊溢位](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files)。
如果您有 Azure 儲存體的功能建議，請張貼太[Azure 儲存體的意見反應](https://feedback.azure.com/forums/217298-storage/)。

