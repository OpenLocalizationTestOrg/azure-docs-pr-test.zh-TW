---
title: "到 iOS 應用程式的 Azure AD aaaIntegrate |Microsoft 文件"
description: "如何 toobuild 與 Azure AD 進行登入並呼叫 Azure AD 整合的 iOS 應用程式會將使用 OAuth 保護應用程式開發介面。"
services: active-directory
documentationcenter: ios
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: 42303177-9566-48ed-8abb-279fcf1e6ddb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 01/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: 6e05745b2b2b122995dcba896ab0f2ed32509e3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-an-ios-app"></a>將 Azure AD 整合至 iOS 應用程式
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> 嘗試的新 hello 預覽[開發人員入口網站](https://identity.microsoft.com/Docs/iOS)，以協助您與 Azure Active Directory 取得啟動且正在執行，在短短幾分鐘內 ！  hello 開發人員入口網站會引導您完成註冊應用程式與 Azure AD 整合您的程式碼 hello 程序。  當您完成時，您會有可驗證租用戶中使用者的簡單應用程式，以及可接受權杖並執行驗證的後端。 
> 
> 

Azure Active Directory (Azure AD) 提供 Active Directory 驗證程式庫或 ADAL，hello，iOS 用戶端需要 tooaccess 受保護的資源。 ADAL 可簡化您的應用程式使用 tooobtain 的存取權杖的 hello 程序。 toodemonstrate 多麼容易的是，在這篇文章中我們建置目標 C 待辦事項清單應用程式，以：

* 取得存取權杖來呼叫 hello Azure AD Graph API 使用 hello [OAuth 2.0 驗證通訊協定](https://msdn.microsoft.com/library/azure/dn645545.aspx)。
* 在目錄中搜尋具有指定別名的使用者。

toobuild hello 完整運作應用程式，您需要：

1. 向 Azure AD 註冊您的應用程式。
2. 安裝及設定 ADAL。
3. 使用來自 Azure AD 的 ADAL tooget 語彙基元。

啟動，tooget[下載 hello 應用程式的基本架構](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip)或[下載完成的 hello 範例](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip)。 您還需要一個可以建立使用者並註冊應用程式的 Azure AD 租用戶。 如果您還沒有租用戶，[深入了解如何 tooget 一個](active-directory-howto-tenant.md)。


> [!TIP]
> 嘗試的新 hello 預覽[開發人員入口網站](https://identity.microsoft.com/Docs/iOS)，以協助您獲得 Azure AD 在短短幾分鐘內啟動且正在執行。 hello 開發人員入口網站會引導您完成註冊應用程式與 Azure AD 整合您的程式碼 hello 程序。 當您完成時，您會有可驗證租用戶中使用者的簡單應用程式，以及可接受權杖並執行驗證的後端。 
> 
> 

## <a name="1-determine-what-your-redirect-uri-is-for-ios"></a>1.決定您 iOS 的重新導向 URI
toosecurely 啟動您的應用程式特定 SSO 案例中，您必須建立*重新導向 URI*以特定的格式。 重新導向 URI 是 hello 語彙基元傳回 toohello 正確的應用程式要求的它們的使用的 tooensure。


hello iOS 格式重新導向 URI 是：

```
<app-scheme>://<bundle-id>
```

* **aap-scheme** - 這已在您的 XCode 專案中註冊。 它是其他應用程式呼叫您的方式。 您可以在 Info.plist -> URL types -> URL Identifier 下找到此項目。 如果您尚未設定任何一個，建議您建立一個。
* **套件組合識別碼**-這是 「 識別 」 下找到的配套識別碼 hello 取消您的專案設定，在 XCode 中。

此 QuickStart 程式碼的範例：***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***

## <a name="2-register-hello-directorysearcher-application"></a>2.註冊 hello DirectorySearcher 應用程式
註冊您的應用程式 tooget 語彙基元 tooset，您必須先 tooregister 在您的 Azure AD 租用戶，並授與權限 tooaccess hello Azure AD Graph API:

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. Hello 頂端列上，按一下您的帳戶。 在 hello**目錄**清單中，選擇您想要 tooregister hello Active Directory 租用戶應用程式。
3. 按一下**更服務**在 hello 最左邊的瀏覽窗格中，然後選取  **Azure Active Directory**。
4. 按一下 [應用程式註冊]，然後選取 [新增]。
5. 請遵循 hello 提示新 toocreate**原生用戶端應用程式**。
  * hello**名稱**hello 的應用程式描述您的應用程式 tooend 使用者。
  * hello**重新導向 Uri**是配置和字串的組合，Azure AD 使用 tooreturn 權杖回應。  輸入的值，是特定 tooyour 應用程式，而根據 hello 先前重新導向 URI 資訊。
6. Hello 註冊完成之後，Azure AD 會指派給您的應用程式是唯一的應用程式識別碼。  您將需要此值在 hello 下一步 區段中，因此將它複製從 hello 應用程式 索引標籤。
7. 從 hello**設定**頁面上，選取**必要的使用權限**，然後選取 **新增**。 選取**Microsoft Graph**為 hello 應用程式開發介面，然後再加入 hello**讀取目錄資料**權限下的**委派的權限**。  這會設定使用者您應用程式 tooquery hello Azure AD Graph API。

## <a name="3-install-and-configure-adal"></a>3.安裝及設定 ADAL
既然您在 Azure AD 中已經擁有應用程式，您可以安裝 ADAL，並撰寫身分識別相關程式碼。  您需要 tooprovide ADAL 與 Azure AD toocommunicate，它與您的應用程式註冊的一些資訊。

1. 開始使用 CocoaPods 加入 ADAL toohello DirectorySearcher 專案。

    ```
    $ vi Podfile
    ```
2. 加入下列 toothis podfile hello:

    ```
    source 'https://github.com/CocoaPods/Specs.git'
    link_with ['QuickStart']
    xcodeproj 'QuickStart'

    pod 'ADALiOS'
    ```

3. 現在使用 CocoaPods 載入 hello podfile。 此步驟會建立您會載入的新 XCode 工作區。

    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

4. 在 hello 快速入門專案，開啟 hello plist 檔案`settings.plist`。  Hello 中的項目 hello 區段 tooreflect hello 您輸入值 hello Azure 入口網站中的 hello 值取代。 每當您的程式碼使用 ADAL 時，都會參考這些值。
  * hello`tenant`是 hello Azure AD 租用戶，例如 contoso.onmicrosoft.com 網域。
  * hello `clientId` hello 您複製從 hello 入口網站應用程式的用戶端識別碼。
  * hello`redirectUri`是您註冊 hello 入口網站中的 hello 重新導向 URL。

## <a name="4----use-adal-tooget-tokens-from-azure-ad"></a>4.  使用 ADAL tooget 語彙基元從 Azure AD
hello ADAL 背後的基本原則是，只要您的應用程式需要存取權杖，它只會呼叫 completionBlock `+(void) getToken : `，ADAL 沒有 hello rest 和。  

1. 在 hello`QuickStart`專案中，開啟`GraphAPICaller.m`並找出 hello `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` hello 頂端附近的註解。  這是您傳遞透過 CompletionBlock 時，使用 Azure AD，toocommunicate ADAL hello 座標和告訴它如何 toocache 語彙基元。

    ```ObjC
    +(void) getToken : (BOOL) clearCache
               parent:(UIViewController*) parent
    completionHandler:(void (^) (NSString*, NSError*))completionBlock;
    {
        AppData* data = [AppData getInstance];
        if(data.userItem){
            completionBlock(data.userItem.accessToken, nil);
            return;
        }

        ADAuthenticationError *error;
        authContext = [ADAuthenticationContext authenticationContextWithAuthority:data.authority error:&error];
        authContext.parentController = parent;
        NSURL *redirectUri = [[NSURL alloc]initWithString:data.redirectUriString];

        [ADAuthenticationSettings sharedInstance].enableFullScreen = YES;
        [authContext acquireTokenWithResource:data.resourceId
                                     clientId:data.clientId
                                  redirectUri:redirectUri
                               promptBehavior:AD_PROMPT_AUTO
                                       userId:data.userItem.userInformation.userId
                        extraQueryParameters: @"nux=1" // if this strikes you as strange it was legacy toodisplay hello correct mobile UX. You most likely won't need it in your code.
                             completionBlock:^(ADAuthenticationResult *result) {

                                  if (result.status != AD_SUCCEEDED)
                                  {
                                     completionBlock(nil, result.error);
                                  }
                                  else
                                  {
                                      data.userItem = result.tokenCacheStoreItem;
                                      completionBlock(result.tokenCacheStoreItem.accessToken, nil);
                                  }
                             }];
    }

    ```

2. 現在我們需要 toouse 這個語彙基元 toosearch hello 圖形中的使用者。 尋找 hello`// TODO: implement SearchUsersList`註解。 這個方法可以讓的使用者的 UPN 開頭指定搜尋詞彙的 hello GET 要求 Azure AD Graph API toohello tooquery。  tooquery hello Azure AD Graph API，您需要在 hello access_token tooinclude `Authorization` hello 要求標頭。 這就是 ADAL 的切入點。

    ```ObjC
    +(void) searchUserList:(NSString*)searchString
                    parent:(UIViewController*) parent
          completionBlock:(void (^) (NSMutableArray* Users, NSError* error)) completionBlock
    {
        if (!loadedApplicationSettings)
       {
            [self readApplicationSettings];
        }
        
        AppData* data = [AppData getInstance];

        NSString *graphURL = [NSString stringWithFormat:@"%@%@/users?api-version=%@&$filter=startswith(userPrincipalName, '%@')", data.taskWebApiUrlString, data.tenant, data.apiversion, searchString];

        [self craftRequest:[self.class trimString:graphURL]
                    parent:parent
         completionHandler:^(NSMutableURLRequest *request, NSError *error) {

             if (error != nil)
             {
                 completionBlock(nil, error);
             }
             else
             {

                 NSOperationQueue *queue = [[NSOperationQueue alloc]init];

                 [NSURLConnection sendAsynchronousRequest:request queue:queue completionHandler:^(NSURLResponse *response, NSData *data, NSError *error) {

                     if (error == nil && data != nil){

                         NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:data options:0 error:nil];

                         // We can grab hello JSON node at hello top tooget our graph data.
                         NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                         // Don't be thrown off by hello key name being "value". It really is hello name of the
                         // first node. :-)

                         // Each object is a key value pair
                         NSDictionary *keyValuePairs;
                         NSMutableArray* Users = [[NSMutableArray alloc]init];

                         for(int i =0; i < graphDataArray.count; i++)
                         {
                             keyValuePairs = [graphDataArray objectAtIndex:i];

                             User *s = [[User alloc]init];
                             s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                             s.name =[keyValuePairs valueForKey:@"givenName"];

                             [Users addObject:s];
                         }

                         completionBlock(Users, nil);
                     }
                     else
                     {
                         completionBlock(nil, error);
                     }

                }];
             }
         }];

    }

    ```


3. 當您的應用程式藉由呼叫要求語彙基元`getToken(...)`，ADAL 會嘗試 tooreturn 語彙基元不要求 hello 使用者認證。  ADAL 會判斷該 hello 使用者需要 toosign tooget 語彙基元中的，如果它會顯示登入 對話方塊、 收集 hello 使用者的認證，以及接著在成功驗證之後傳回語彙基元。  如果 ADAL 不能 tooreturn 語彙基元因為任何原因，就會擲回`AdalException`。

> [!Note] 
> hello`AuthenticationResult`物件包含`tokenCacheStoreItem`可以是您的應用程式可能需要使用的 toocollect hello 資訊的物件。 在 hello 快速入門，`tokenCacheStoreItem`如果驗證已完成，則使用的 toodetermine。
>
>

## <a name="5-build-and-run-hello-application"></a>5.建置並執行 hello 應用程式
恭喜！ 現在您已經有可用的 iOS 應用程式，可以驗證使用者，安全地使用 OAuth 2.0 來呼叫 Web Api 取得 hello 使用者的基本資訊。  如果您還沒有這麼做，現在是 hello 時間 toopopulate 與某些使用者的租用戶。  啟動 QuickStart 應用程式，然後使用其中一個使用者登入。  根據 UPN 搜尋其他使用者。  關閉 hello 應用程式，並重新啟動它。  請注意 hello 使用者工作階段會保持不變。

ADAL 可讓您輕鬆 tooincorporate 所有這些常見的身分識別功能到您的應用程式。  它會負責所有 hello dirty 工作，例如快取管理 OAuth 通訊協定支援，呈現給在中，UI toosign hello 使用者和重新整理過期的權杖。  您只需 tooknow 是單一的應用程式開發介面呼叫， `getToken`。

如需參考上, 提供 （不含您的組態值） 的 hello 完成範例[GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip)。  

## <a name="next-steps"></a>後續步驟
您現在可以移動 tooadditional 案例。  您可能想 tootry:

* [使用 Azure AD 保護 Node.js Web API](active-directory-devquickstarts-webapi-nodejs.md)
* 深入了解[如何 tooenable 跨應用程式使用 ADAL 的 iOS 上的 SSO](active-directory-sso-ios.md)  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

