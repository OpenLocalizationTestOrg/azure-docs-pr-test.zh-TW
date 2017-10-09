---
title: "aaaHow tooUse iOS SDK for Azure 行動應用程式"
description: "如何 tooUse iOS SDK for Azure 行動應用程式"
services: app-service\mobile
documentationcenter: ios
author: ysxu
manager: yochayk
editor: 
ms.assetid: 4e8e45df-c36a-4a60-9ad4-393ec10b7eb9
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/01/2016
ms.author: yuaxu
ms.openlocfilehash: fa299ab3f152bad12d821832fa9fb5495d1fa296
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-ios-client-library-for-azure-mobile-apps"></a>如何 tooUse iOS Azure 行動應用程式的用戶端程式庫
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

本指南將教導您 tooperform 常見的案例，使用最新的 hello [Azure 行動應用程式 iOS SDK][1]。 如果您是新 tooAzure 行動應用程式，請先完成[Azure 行動應用程式快速入門]toocreate 後端，建立資料表，並下載預先建立的 iOS Xcode 專案。 在本指南中，我們會著重在 hello 用戶端 iOS SDK。 toolearn 深入了解 hello hello 後端伺服器端 SDK，請參閱 hello 伺服器 SDK 來。

## <a name="reference-documentation"></a>參考文件
hello hello iOS 用戶端 SDK 的參考文件位於此處： [Azure 行動應用程式 iOS 用戶端參考][2]。

## <a name="supported-platforms"></a>支援的平台
hello iOS SDK 支援 iOS 8.0 或更新版本的版本 Objective C 專案、 Swift 2.2 專案和 Swift 2.3 專案。

hello 「 伺服器-流程 」 驗證會使用 WebView hello 呈現 UI。  如果 hello 裝置不能 toopresent WebView UI，則需要其他的驗證方法，則將 hello 範圍外的 hello 產品。  
因此，此 SDK 不適用於手錶類型或受到類似限制的裝置。

## <a name="Setup"></a>設定和必要條件
本指南假設您已建立包含資料表的後端。 本指南假設 hello 資料表具有在這些教學課程中的 hello 資料表相同的結構描述。 本指南也假設您在程式碼中，參考了 `MicrosoftAzureMobile.framework` 並匯入了 `MicrosoftAzureMobile/MicrosoftAzureMobile.h`。

## <a name="create-client"></a>作法：建立用戶端
在專案中，Azure 行動應用程式後端 tooaccess 建立`MSClient`。 取代`AppUrl`hello 應用程式 url。 您可以將 `gatewayURLString` 和 `applicationKey` 留白。 如果您設定閘道，以進行驗證時，擴展`gatewayURLString`與 hello gateway URL。

**Objective-C**：

```
MSClient *client = [MSClient clientWithApplicationURLString:@"AppUrl"];
```

**Swift**：

```
let client = MSClient(applicationURLString: "AppUrl")
```


## <a name="table-reference"></a>作法：建立資料表參考
tooaccess 或更新的資料，建立參考 toohello 後端的資料表。 取代`TodoItem`與資料表的名稱，hello

**Objective-C**：

```
MSTable *table = [client tableWithName:@"TodoItem"];
```

**Swift**：

```
let table = client.tableWithName("TodoItem")
```


## <a name="querying"></a>作法：查詢資料
toocreate 資料庫查詢，查詢 hello`MSTable`物件。 hello 下列查詢會取得所有 hello 項目`TodoItem`和記錄檔 hello 每個項目的文字。

**Objective-C**：

```
[table readWithCompletion:^(MSQueryResult *result, NSError *error) {
        if(error) { // error is nil if no error occured
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) { // items is NSArray of records that match query
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

**Swift**：

```
table.readWithCompletion { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```

## <a name="filtering"></a>作法：篩選傳回的資料
toofilter 結果中，有許多可用的選項。

使用述詞，而使用 toofilter`NSPredicate`和`readWithPredicate`。 hello 下列篩選傳回的資料 toofind 僅完整 Todo 項目。

**Objective-C**：

```
// Create a predicate that finds items where complete is false
NSPredicate * predicate = [NSPredicate predicateWithFormat:@"complete == NO"];
// Query hello TodoItem table
[table readWithPredicate:predicate completion:^(MSQueryResult *result, NSError *error) {
        if(error) {
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) {
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

**Swift**：

```
// Create a predicate that finds items where complete is false
let predicate =  NSPredicate(format: "complete == NO")
// Query hello TodoItem table
table.readWithPredicate(predicate) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```

## <a name="query-object"></a>作法：使用 MSQuery
建立複雜的查詢 （包括排序和分頁） tooperform`MSQuery`物件直接或使用述詞：

**Objective-C**：

```
MSQuery *query = [table query];
MSQuery *query = [table queryWithPredicate: [NSPredicate predicateWithFormat:@"complete == NO"]];
```

**Swift**：

```
let query = table.query()
let query = table.queryWithPredicate(NSPredicate(format: "complete == NO"))
```

`MSQuery` 可讓您控制幾種查詢行為。

* 指定結果的順序
* 欄位 tooreturn 的限制
* 限制的記錄數 tooreturn
* 指定回應中的總計數
* 在要求中指定自訂查詢字串參數
* 套用其他函式

執行`MSQuery`查詢藉由呼叫`readWithCompletion`hello 物件上。

## <a name="sorting"></a>做法：使用 MSQuery 排序資料
toosort 結果，讓我們來看一個範例。 以遞增的欄位 'text'，然後依照 「 完成 」 遞減排列，toosort 叫用`MSQuery`就像這樣：

**Objective-C**：

```
[query orderByAscending:@"text"];
[query orderByDescending:@"complete"];
[query readWithCompletion:^(MSQueryResult *result, NSError *error) {
        if(error) {
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) {
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

**Swift**：

```
query.orderByAscending("text")
query.orderByDescending("complete")
query.readWithCompletion { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```


## <a name="selecting"></a><a name="parameters"></a>作法：使用 MSQuery 限制欄位和展開查詢字串參數
在查詢中，傳回 toolimit 欄位 toobe 指定 hello hello 欄位名稱在 hello **selectFields**屬性。 這個範例會傳回只 hello 文字和已完成的欄位：

**Objective-C**：

```
query.selectFields = @[@"text", @"complete"];
```

**Swift**：

```
query.selectFields = ["text", "complete"]
```

tooinclude 其他查詢字串參數中 hello 伺服器要求 （例如，因為自訂伺服器端指令碼使用它們），填入`query.parameters`就像這樣：

**Objective-C**：

```
query.parameters = @{
    @"myKey1" : @"value1",
    @"myKey2" : @"value2",
};
```

**Swift**：

```
query.parameters = ["myKey1": "value1", "myKey2": "value2"]
```

## <a name="paging"></a>如何：設定頁面大小
Azure 行動應用程式，與 hello 頁面大小控制項 hello 會提取從 hello 後端資料表一次的記錄數目。 呼叫太`pull`資料然後會批次處理資料，根據此頁面大小，直到沒有任何多個記錄 toopull 為止。

它會使用頁面大小可能 tooconfigure **MSPullSettings**如下所示。 hello 預設頁面大小為 50，且 hello 下面範例會變更 too3。

您可以基於效能的考量設定不同的頁面大小。 如果您有大量的小型資料記錄，較高的頁面大小會減少往返伺服器的 hello 數目。

此設定會控制只 hello 頁面大小 hello 用戶端。 如果 hello 用戶端要求較大的頁面大小高於 hello 行動應用程式後端支援，hello 頁面大小上限為 hello 最大 hello 後端是設定的 toosupport。

這項設定也是 hello*數目*資料記錄不 hello*位元組大小*。

如果您增加 hello 用戶端頁面大小，您也應該增加 hello hello 伺服器上的頁面大小。 請參閱["如何： 調整 hello 表格分頁大小 」](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) hello 步驟 toodo 這。

**Objective-C**：

```
  MSPullSettings *pullSettings = [[MSPullSettings alloc] initWithPageSize:3];
  [table  pullWithQuery:query queryId:@nil settings:pullSettings
                        completion:^(NSError * _Nullable error) {
                               if(error) {
                    NSLog(@"ERROR %@", error);
                }
                           }];
```


**Swift**：

```
let pullSettings = MSPullSettings(pageSize: 3)
table.pullWithQuery(query, queryId:nil, settings: pullSettings) { (error) in
    if let err = error {
        print("ERROR ", err)
    }
}
```

## <a name="inserting"></a>作法：插入資料
建立新的資料表資料列，tooinsert`NSDictionary`和叫用`table insert`。 如果[動態結構描述]已啟用，hello Azure App Service 行動後端會自動產生新資料行是根據 hello `NSDictionary`。

如果`id`未提供，hello 後端會自動產生新的唯一識別碼。 提供您自己`id`toouse 傳送電子郵件地址、 使用者名稱或您自己自訂的值為識別碼。 提供您自己的識別碼可以讓聯結和商務導向的資料庫邏輯變得更容易。

hello`result`包含插入的 hello 新項目。 根據您伺服器的邏輯，它可能有其他或已修改的資料比較 toowhat 已傳遞 toohello 伺服器。

**Objective-C**：

```
NSDictionary *newItem = @{@"id": @"custom-id", @"text": @"my new item", @"complete" : @NO};
[table insert:newItem completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

**Swift**：

```
let newItem = ["id": "custom-id", "text": "my new item", "complete": false]
table.insert(newItem) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

## <a name="modifying"></a>作法：修改資料
tooupdate 現有的資料列，修改項目並呼叫`update`:

**Objective-C**：

```
NSMutableDictionary *newItem = [oldItem mutableCopy]; // oldItem is NSDictionary
[newItem setValue:@"Updated text" forKey:@"text"];
[table update:newItem completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

**Swift**：

```
if let newItem = oldItem.mutableCopy() as? NSMutableDictionary {
    newItem["text"] = "Updated text"
    table2.update(newItem as [NSObject: AnyObject], completion: { (result, error) -> Void in
        if let err = error {
            print("ERROR ", err)
        } else if let item = result {
            print("Todo Item: ", item["text"])
        }
    })
}
```

或者，提供 hello 資料列識別碼和更新的 hello 欄位：

**Objective-C**：

```
[table update:@{@"id":@"custom-id", @"text":"my EDITED item"} completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

**Swift**：

```
table.update(["id": "custom-id", "text": "my EDITED item"]) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

最小值，hello`id`進行更新時，必須設定屬性。

## <a name="deleting"></a>作法：刪除資料
叫用的項目，toodelete`delete`與 hello 項目：

**Objective-C**：

```
[table delete:item completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

**Swift**：

```
table.delete(newItem as [NSObject: AnyObject]) { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

或者，提供資料列識別碼來進行刪除：

**Objective-C**：

```
[table deleteWithId:@"37BBF396-11F0-4B39-85C8-B319C729AF6D" completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

**Swift**：

```
table.deleteWithId("37BBF396-11F0-4B39-85C8-B319C729AF6D") { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

最小值，hello`id`進行刪除時，必須設定屬性。

## <a name="customapi"></a>如何：呼叫自訂 API
使用自訂 API，您可以公開任何後端功能。 它沒有 toomap tooa 資料表作業。 不只取得更多控制訊息，您甚至還可以讀取或設定標頭，並變更 hello 回應內文格式。 hello 後端，toocreate 自訂 API 的讀取方式 toolearn[自訂 Api](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)

toocall 自訂 API 中，呼叫`MSClient.invokeAPI`。 hello 要求和回應內容會被視為 JSON。 toouse 其他類型的媒體，[使用 hello 其他多載`invokeAPI` ] [ 5]。  toomake`GET`要求而不是`POST`要求，集參數`HTTPMethod`太`"GET"`和參數`body`太`nil`（因為 GET 要求並沒有訊息內文。）如果您的自訂 API 支援其他 HTTP 動詞命令，請適當地變更 `HTTPMethod`。

**Objective-C**：

```
[self.client invokeAPI:@"sendEmail"
                  body:@{ @"contents": @"Hello world!" }
            HTTPMethod:@"POST"
            parameters:@{ @"to": @"bill@contoso.com", @"subject" : @"Hi!" }
               headers:nil
            completion: ^(NSData *result, NSHTTPURLResponse *response, NSError *error) {
                if(error) {
                    NSLog(@"ERROR %@", error);
                } else {
                    // Do something with result
                }
            }];
```

**Swift**：

```
client.invokeAPI("sendEmail",
            body: [ "contents": "Hello World" ],
            HTTPMethod: "POST",
            parameters: [ "to": "bill@contoso.com", "subject" : "Hi!" ],
            headers: nil)
            {
                (result, response, error) -> Void in
                if let err = error {
                    print("ERROR ", err)
                } else if let res = result {
                          // Do something with result
                }
        }
```

## <a name="templates"></a>如何： 註冊推播範本 toosend 跨平台通知
tooregister 範本，將範本與您**client.push registerDeviceToken**用戶端應用程式中的方法。

**Objective-C**：

```
[client.push registerDeviceToken:deviceToken template:iOSTemplate completion:^(NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    }
}];
```

**Swift**：

```
    client.push?.registerDeviceToken(NSData(), template: iOSTemplate, completion: { (error) in
        if let err = error {
            print("ERROR ", err)
        }
    })
```

您的範本，屬於類型 NSDictionary，且可以包含多個範本中 hello 下列格式：

**Objective-C**：

```
NSDictionary *iOSTemplate = @{ @"templateName": @{ @"body": @{ @"aps": @{ @"alert": @"$(message)" } } } };
```

**Swift**：

```
let iOSTemplate = ["templateName": ["body": ["aps": ["alert": "$(message)"]]]]
```

所有標籤都都會從 hello 安全性要求。  tooadd 標記 tooinstallations 或內安裝的範本，請參閱[Azure 行動應用程式使用 hello.NET 後端伺服器 SDK][4]。  使用這些已註冊的範本，toosend 通知使用[通知中樞 Api][3]。

## <a name="errors"></a>作法：處理錯誤
當您呼叫 Azure App Service 行動後端時，hello 完成區塊包含`NSError`參數。 發生錯誤時，此參數便會傳回非 Nil。 在您的程式碼中，您應該檢查此參數，並處理 hello 錯誤，可以視 hello 前面程式碼片段所示。

hello 檔案[ `<WindowsAzureMobileServices/MSError.h>` ] [ 6]定義 hello 常數`MSErrorResponseKey`， `MSErrorRequestKey`，和`MSErrorServerItemKey`。 tooget 相關 toohello 錯誤的詳細資料：

**Objective-C**：

```
NSDictionary *serverItem = [error.userInfo objectForKey:MSErrorServerItemKey];
```

**Swift**：

```
let serverItem = error.userInfo[MSErrorServerItemKey]
```

此外，hello 檔案會定義每個錯誤碼的常數：

**Objective-C**：

```
if (error.code == MSErrorPreconditionFailed) {
```

**Swift**：

```
if (error.code == MSErrorPreconditionFailed) {
```

## <a name="adal"></a>如何： 驗證使用者以 hello Active Directory Authentication Library
您可以使用 hello Active Directory 驗證程式庫 (ADAL) toosign 使用者將使用 Azure Active Directory 應用程式。 使用身分識別提供者 SDK 用戶端流量驗證會偏好 toousing hello`loginWithProvider:completion:`方法。  用戶端流程驗證能提供較原生的 UX 風格，並允許進行其他自訂。

1. 設定下列 hello AAD 登入您的行動裝置應用程式後端[tooconfigure Active Directory 登入服務的應用程式如何][ 7]教學課程。 請確定 toocomplete hello 的選擇性步驟註冊原生用戶端應用程式。 對於 iOS，我們建議您該 hello 重新導向 URI 是 hello 表單的`<app-scheme>://<bundle-id>`。 如需詳細資訊，請參閱 hello [ADAL iOS 快速入門][8]。
2. 使用 Cocoapods 安裝 ADAL。 編輯下列定義，取代您 Podfile tooinclude hello**您專案**hello 名稱，為您的 Xcode 專案：

        source 'https://github.com/CocoaPods/Specs.git'
        link_with ['YOUR-PROJECT']
        xcodeproj 'YOUR-PROJECT'

   和 hello Pod:

        pod 'ADALiOS'
3. 使用執行 hello 終端機`pod install`hello 目錄從包含您的專案，然後再開啟 產生 hello Xcode 工作區 （非 hello 專案）。
4. 新增下列程式碼 tooyour 應用程式，根據您所使用的 toohello 語言 hello。 取代每個程式碼的以下項目：

   * 取代**插入授權這裡**hello 您佈建您的應用程式的 hello 租用戶名稱。 格式應該為 https://login.microsoftonline.com/contoso.onmicrosoft.com。從 Azure Active Directory hello [Azure 傳統入口網站] 中的 hello 網域] 索引標籤，可以複製此值。
   * 取代**插入資源 ID-這裡**與您的行動裝置應用程式後端的 hello 用戶端識別碼。 您可以取得用戶端識別碼，從 hello**進階**索引標籤底下**Azure Active Directory 設定**hello 入口網站中。
   * 取代**插入用戶端識別碼-這裡**hello 您所複製的 hello 原生用戶端應用程式的用戶端識別碼。
   * 取代**插入重新導向 URI-這裡**與您的網站*/.auth/login/done*使用 hello HTTPS 配置的端點。 此值太應該類似*https://contoso.azurewebsites.net/.auth/login/done*。

**Objective-C**：

    #import <ADALiOS/ADAuthenticationContext.h>
    #import <ADALiOS/ADAuthenticationSettings.h>
    // ...
    - (void) authenticate:(UIViewController*) parent
               completion:(void (^) (MSUser*, NSError*))completionBlock;
    {
        NSString *authority = @"INSERT-AUTHORITY-HERE";
        NSString *resourceId = @"INSERT-RESOURCE-ID-HERE";
        NSString *clientId = @"INSERT-CLIENT-ID-HERE";
        NSURL *redirectUri = [[NSURL alloc]initWithString:@"INSERT-REDIRECT-URI-HERE"];
        ADAuthenticationError *error;
        ADAuthenticationContext *authContext = [ADAuthenticationContext authenticationContextWithAuthority:authority error:&error];
        authContext.parentController = parent;
        [ADAuthenticationSettings sharedInstance].enableFullScreen = YES;
        [authContext acquireTokenWithResource:resourceId
                                     clientId:clientId
                                  redirectUri:redirectUri
                              completionBlock:^(ADAuthenticationResult *result) {
                                  if (result.status != AD_SUCCEEDED)
                                  {
                                      completionBlock(nil, result.error);;
                                  }
                                  else
                                  {
                                      NSDictionary *payload = @{
                                                                @"access_token" : result.tokenCacheStoreItem.accessToken
                                                                };
                                      [client loginWithProvider:@"aad" token:payload completion:completionBlock];
                                  }
                              }];
    }


**Swift**：

    // add hello following imports tooyour bridging header:
    //        #import <ADALiOS/ADAuthenticationContext.h>
    //        #import <ADALiOS/ADAuthenticationSettings.h>

    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let authority = "INSERT-AUTHORITY-HERE"
        let resourceId = "INSERT-RESOURCE-ID-HERE"
        let clientId = "INSERT-CLIENT-ID-HERE"
        let redirectUri = NSURL(string: "INSERT-REDIRECT-URI-HERE")
        var error: AutoreleasingUnsafeMutablePointer<ADAuthenticationError?> = nil
        let authContext = ADAuthenticationContext(authority: authority, error: error)
        authContext.parentController = parent
        ADAuthenticationSettings.sharedInstance().enableFullScreen = true
        authContext.acquireTokenWithResource(resourceId, clientId: clientId, redirectUri: redirectUri) { (result) in
                if result.status != AD_SUCCEEDED {
                    completion(nil, result.error)
                }
                else {
                    let payload: [String: String] = ["access_token": result.tokenCacheStoreItem.accessToken]
                    client.loginWithProvider("aad", token: payload, completion: completion)
                }
            }
    }

## <a name="facebook-sdk"></a>如何： 驗證使用者以 hello Facebook SDK for iOS
您可以使用 iOS toosign 使用者的 hello Facebook SDK 至使用 Facebook 應用程式。  使用用戶端流程驗證是比 toousing hello`loginWithProvider:completion:`方法。  hello 用戶端流程驗證，提供較原始的 UX 操作，並允許其他自訂。

1. 依照下列設定 Facebook 登入您的行動裝置應用程式後端[tooconfigure Facebook 登入服務應用程式如何][ 9]教學課程。
2. 安裝 hello Facebook SDK for iOS 的下列 hello [Facebook SDK iOS-快速入門][ 10]文件。 如果不建立應用程式，您可以加入 hello iOS 平台 tooyour 現有註冊。
3. Facebook 的文件包含一些 Objective C 程式碼中 hello 應用程式委派。 如果您使用**Swift**，您可以使用下列的 AppDelegate.swift 翻譯的 hello:

        // Add hello following import tooyour bridging header:
        //        #import <FBSDKCoreKit/FBSDKCoreKit.h>

        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            FBSDKApplicationDelegate.sharedInstance().application(application, didFinishLaunchingWithOptions: launchOptions)
            // Add any custom logic here.
            return true
        }

        func application(application: UIApplication, openURL url: NSURL, sourceApplication: String?, annotation: AnyObject?) -> Bool {
            let handled = FBSDKApplicationDelegate.sharedInstance().application(application, openURL: url, sourceApplication: sourceApplication, annotation: annotation)
            // Add any custom logic here.
            return handled
        }
4. 在加法 tooadding `FBSDKCoreKit.framework` tooyour 專案，也將參考加入太`FBSDKLoginKit.framework`hello 中相同的方式。
5. 新增下列程式碼 tooyour 應用程式，根據您所使用的 toohello 語言 hello。

**Objective-C**：

    #import <FBSDKLoginKit/FBSDKLoginKit.h>
    #import <FBSDKCoreKit/FBSDKAccessToken.h>
    // ...
    - (void) authenticate:(UIViewController*) parent
               completion:(void (^) (MSUser*, NSError*)) completionBlock;
    {        
        FBSDKLoginManager *loginManager = [[FBSDKLoginManager alloc] init];
        [loginManager
         logInWithReadPermissions: @[@"public_profile"]
         fromViewController:parent
         handler:^(FBSDKLoginManagerLoginResult *result, NSError *error) {
             if (error) {
                 completionBlock(nil, error);
             } else if (result.isCancelled) {
                 completionBlock(nil, error);
             } else {
                 NSDictionary *payload = @{
                                           @"access_token":result.token.tokenString
                                           };
                 [client loginWithProvider:@"facebook" token:payload completion:completionBlock];
             }
         }];
    }

**Swift**：

    // Add hello following imports tooyour bridging header:
    //        #import <FBSDKLoginKit/FBSDKLoginKit.h>
    //        #import <FBSDKCoreKit/FBSDKAccessToken.h>

    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let loginManager = FBSDKLoginManager()
        loginManager.logInWithReadPermissions(["public_profile"], fromViewController: parent) { (result, error) in
            if (error != nil) {
                completion(nil, error)
            }
            else if result.isCancelled {
                completion(nil, error)
            }
            else {
                let payload: [String: String] = ["access_token": result.token.tokenString]
                client.loginWithProvider("facebook", token: payload, completion: completion)
            }
        }
    }

## <a name="twitter-fabric"></a>作法：使用 Twitter Fabric for iOS 來驗證使用者
您可以用於網狀架構 iOS toosign 使用者使用 Twitter 的應用程式。 用戶端流程驗證是比 toousing hello`loginWithProvider:completion:`方法，因為它提供更原生的 UX 操作，並允許進行其他自訂。

1. Twitter 登入您的行動裝置應用程式後端設定下列 hello [tooconfigure Twitter 登入服務的應用程式如何](app-service-mobile-how-to-configure-twitter-authentication.md)教學課程。
2. 加入下列 hello 網狀架構 tooyour 專案[iOS-快速入門的網狀架構]文件和設定 TwitterKit。

   > [!NOTE]
   > 根據預設，網狀架構會為您建立 Twitter 應用程式。 您可以避免建立應用程式註冊 hello 取用者索引鍵與您先前使用下列程式碼片段的 hello 建立取用者密碼。    或者，您可以取代 hello 取用者索引鍵和取用者密碼值，提供以 hello tooApp 服務值請參閱在 hello[光纖儀表板]。 如果您選擇此選項，是確定 tooset hello 回呼 URL tooa 預留位置值，例如`https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`。
   >
   >

    如果您選擇 toouse 您稍早建立的 hello 機密資料，加入下列程式碼 tooyour 應用程式委派 hello:

    **Objective-C**：

        #import <Fabric/Fabric.h>
        #import <TwitterKit/TwitterKit.h>
        // ...
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
            [[Twitter sharedInstance] startWithConsumerKey:@"your_key" consumerSecret:@"your_secret"];
            [Fabric with:@[[Twitter class]]];
            // Add any custom logic here.
            return YES;
        }

    **Swift**：

        import Fabric
        import TwitterKit
        // ...
        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            Twitter.sharedInstance().startWithConsumerKey("your_key", consumerSecret: "your_secret")
            Fabric.with([Twitter.self])
            // Add any custom logic here.
            return true
        }
3. 新增下列程式碼 tooyour 應用程式，根據您所使用的 toohello 語言 hello。

**Objective-C**：

    #import <TwitterKit/TwitterKit.h>
    // ...
    - (void)authenticate:(UIViewController*)parent completion:(void (^) (MSUser*, NSError*))completionBlock
    {
        [[Twitter sharedInstance] logInWithCompletion:^(TWTRSession *session, NSError *error) {
            if (session) {
                NSDictionary *payload = @{
                                            @"access_token":session.authToken,
                                            @"access_token_secret":session.authTokenSecret
                                        };
                [client loginWithProvider:@"twitter" token:payload completion:completionBlock];
            } else {
                completionBlock(nil, error);
            }
        }];
    }

**Swift**：

    import TwitterKit
    // ...
    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let client = self.table!.client
        Twitter.sharedInstance().logInWithCompletion { session, error in
            if (session != nil) {
                let payload: [String: String] = ["access_token": session!.authToken, "access_token_secret": session!.authTokenSecret]
                client.loginWithProvider("twitter", token: payload, completion: completion)
            } else {
                completion(nil, error)
            }
        }
    }

## <a name="google-sdk"></a>如何： 驗證使用者以 hello Google 登入 SDK 適用於 iOS
您可以使用 iOS toosign 使用者的 hello Google 登入 SDK 到應用程式使用 Google 帳戶。  Google 最近宣布變更 tootheir OAuth 安全性原則。  這些原則的變更將需要在未來的 hello Google SDK hello 使用。

1. 設定下列 hello Google 登入您的行動裝置應用程式後端[tooconfigure Google 登入服務應用程式如何](app-service-mobile-how-to-configure-google-authentication.md)教學課程。
2. 安裝 hello Google SDK 適用於 iOS 的下列 hello [Google 登入的 iOS-啟動整合](https://developers.google.com/identity/sign-in/ios/start-integrating)文件。 您可以略過 hello < 驗證與後端伺服器 > 一節。
3. 新增下列 tooyour 委派 hello`signIn:didSignInForUser:withError:`方法，根據您所使用的 toohello 語言。

**Objective-C**：

        NSDictionary *payload = @{
                                  @"id_token":user.authentication.idToken,
                                  @"authorization_code":user.serverAuthCode
                                  };

        [client loginWithProvider:@"google" token:payload completion:^(MSUser *user, NSError *error) {
            // ...
        }];

**Swift**：

        let payload: [String: String] = ["id_token": user.authentication.idToken, "authorization_code": user.serverAuthCode]
        client.loginWithProvider("google", token: payload) { (user, error) in
            // ...
        }

1. 請確定您也可以加入 hello 太遵循`application:didFinishLaunchingWithOptions:`應用程式中委派、"SERVER_CLIENT_ID"取代成 hello 相同識別碼使用您在步驟 1 中的 tooconfigure 應用程式服務。

**Objective-C**：

         [GIDSignIn sharedInstance].serverClientID = @"SERVER_CLIENT_ID";

 **Swift**：

        GIDSignIn.sharedInstance().serverClientID = "SERVER_CLIENT_ID"


1. 新增下列程式碼 tooyour 應用程式中實作 hello UIViewController hello`GIDSignInUIDelegate`通訊協定，根據您所使用的 toohello 語言。  同樣地，登入之前已登出，雖然您不需要 tooenter 認證一次，但您會看到同意對話方塊。  Hello 工作階段權杖已過期時，才可以呼叫這個方法。

   **Objective-C**：

       #import <Google/SignIn.h>
       // ...
       - (void)authenticate
       {
               [GIDSignIn sharedInstance].uiDelegate = self;
               [[GIDSignIn sharedInstance] signOut];
               [[GIDSignIn sharedInstance] signIn];
        }

   **Swift**：

       // ...
       func authenticate() {
           GIDSignIn.sharedInstance().uiDelegate = self
           GIDSignIn.sharedInstance().signOut()
           GIDSignIn.sharedInstance().signIn()
       }

<!-- Anchors. -->

[What is Mobile Services]: #what-is
[Concepts]: #concepts
[Setup and Prerequisites]: #Setup
[How to: Create hello Mobile Services client]: #create-client
[How to: Create a table reference]: #table-reference
[How to: Query data from a mobile service]: #querying
[Filter returned data]: #filtering
[Sort returned data]: #sorting
[Return data in pages]: #paging
[Select specific columns]: #selecting
[How to: Bind data toohello user interface]: #binding
[How to: Insert data into a mobile service]: #inserting
[How to: Modify data in a mobile service]: #modifying
[How to: Authenticate users]: #authentication
[Cache authentication tokens]: #caching-tokens
[How to: Upload images and large files]: #blobs
[How to: Handle errors]: #errors
[How to: Design unit tests]: #unit-testing
[How to: Customize hello client]: #customizing
[Customize request headers]: #custom-headers
[Customize data type serialization]: #custom-serialization
[Next Steps]: #next-steps
[How to: Use MSQuery]: #query-object

<!-- Images. -->

<!-- URLs. -->
[Azure 行動應用程式快速入門]: app-service-mobile-ios-get-started.md

[Add Mobile Services tooExisting App]: /develop/mobile/tutorials/get-started-data
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Validate and modify data in Mobile Services by using server scripts]: /develop/mobile/tutorials/validate-modify-and-augment-data-ios
[Mobile Services SDK]: https://go.microsoft.com/fwLink/p/?LinkID=266533
[Authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[iOS SDK]: https://developer.apple.com/xcode

[Handling Expired Tokens]: http://go.microsoft.com/fwlink/p/?LinkId=301955
[Live Connect SDK]: http://go.microsoft.com/fwlink/p/?LinkId=301960
[Permissions]: http://msdn.microsoft.com/library/windowsazure/jj193161.aspx
[Service-side Authorization]: mobile-services-javascript-backend-service-side-authorization.md
[Use scripts tooauthorize users]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
[動態結構描述]: http://go.microsoft.com/fwlink/p/?LinkId=296271
[How to: access custom parameters]: /develop/mobile/how-to-guides/work-with-server-scripts#access-headers
[Create a table]: http://msdn.microsoft.com/library/windowsazure/jj193162.aspx
[NSDictionary object]: http://go.microsoft.com/fwlink/p/?LinkId=301965
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[CLI toomanage Mobile Services tables]: /cli/azure/get-started-with-az-cli2
[Conflict-Handler]: mobile-services-ios-handling-conflicts-offline-data.md#add-conflict-handling

[光纖儀表板]: https://www.fabric.io/home
[iOS-快速入門的網狀架構]: https://docs.fabric.io/ios/fabric/getting-started.html
[1]: https://github.com/Azure/azure-mobile-apps-ios-client/blob/master/README.md#ios-client-sdk
[2]: http://azure.github.io/azure-mobile-apps-ios-client/
[3]: https://msdn.microsoft.com/library/azure/dn495101.aspx
[4]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags
[5]: http://azure.github.io/azure-mobile-services/iOS/v3/Classes/MSClient.html#//api/name/invokeAPI:data:HTTPMethod:parameters:headers:completion:
[6]: https://github.com/Azure/azure-mobile-services/blob/master/sdk/iOS/src/MSError.h
[7]: app-service-mobile-how-to-configure-active-directory-authentication.md
[8]: ../active-directory/active-directory-devquickstarts-ios.md
[9]: app-service-mobile-how-to-configure-facebook-authentication.md
[10]: https://developers.facebook.com/docs/ios/getting-started
