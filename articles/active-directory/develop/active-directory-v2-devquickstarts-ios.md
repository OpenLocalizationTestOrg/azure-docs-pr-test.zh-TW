---
title: "aaaAdd 登入 tooan iOS 應用程式使用 hello Azure AD v2.0 端點 |Microsoft 文件"
description: "如何 toobuild iOS 應用程式的登入具有兩個人的 Microsoft 帳戶的使用者和工作或學校帳戶透過協力廠商文件庫。"
services: active-directory
documentationcenter: 
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: fd3603c0-42f7-438c-87b5-a52d20d6344b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 01/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: a384062e6e4bd398a2b12318800728e627e05c32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-ios-app-using-a-third-party-library-with-graph-api-using-hello-v20-endpoint"></a>新增登入 tooan iOS 應用程式使用 Graph API 使用 hello v2.0 端點使用協力廠商程式庫
hello Microsoft 識別身分平台中使用 OAuth2 和 OpenID Connect 等的開放標準。 開發人員可以使用任何文件庫，他們想 toointegrate 與我們的服務。 toohelp 開發人員會使用我們的平台與其他程式庫，我們已經撰寫這個一個 toodemonstrate 像幾個逐步解說如何 tooconfigure 協力廠商程式庫 tooconnect toohello Microsoft 識別平台。 實作的大部分程式庫[hello RFC6749 OAuth2 規格](https://tools.ietf.org/html/rfc6749)可以連接 toohello Microsoft 識別平台。

這個逐步解說會建立 hello 應用程式，才能登入 tootheir 組織使用者，並將其然後搜尋其他組織中使用 hello Graph API 中。

如果您是新 tooOAuth2 或 OpenID Connect，此範例組態中的許多可能不會有意義 tooyou。 建議您閱讀 [v2.0 通訊協定 - OAuth 2.0 授權碼流程](active-directory-v2-protocols-oauth-code.md)以瞭解背景。

> [!NOTE]
> 平台的 hello OAuth2 或 OpenID Connect 標準，例如條件式存取和 Intune 原則管理 中的運算式具有某些功能需要您 toouse 我們的開放原始碼 Microsoft Azure 身分識別的程式庫。
> 
> 

hello v2.0 端點不支援所有的 Azure Active Directory 的案例和功能。

> [!NOTE]
> toodetermine 如果應該使用 hello v2.0 端點，閱讀有關[v2.0 限制](active-directory-v2-limitations.md)。
> 
> 

## <a name="download-code-from-github"></a>從 GitHub 下載程式碼
此教學課程中的 hello 程式碼會維護[GitHub 上](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2)。  您可以沿著 toofollow，[下載為.zip 的 hello 應用程式的基本架構](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip)或再製 hello 基本架構：

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

您也可以下載 hello 範例，並立即開始：

```
git clone git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

## <a name="register-an-app"></a>註冊應用程式
建立新的應用程式在 hello[應用程式註冊入口網站](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)，或遵循 hello 詳細的步驟，網址[如何 tooregister 應用程式，但 hello v2.0 端點](active-directory-v2-app-registration.md)。  請確定：

* 複製 hello**應用程式識別碼**這是指派的 tooyour 應用程式因為很快就需要它。
* 新增 hello**行動**平台應用程式。
* 複製 hello**重新導向 URI**從 hello 入口網站。 您必須使用預設值 hello `urn:ietf:wg:oauth:2.0:oob`。

## <a name="download-hello-third-party-nxoauth2-library-and-create-a-workspace"></a>下載 hello 第三方 NXOAuth2 程式庫，並建立工作區
這個逐步解說中，您將使用 hello OAuth2Client 從 GitHub，是適用於 Mac OS X 和 iOS （Cocoa 和 Cocoa touch） 的 OAuth2 程式庫。 此程式庫為基礎的 hello OAuth2 規格草稿 10。它會實作 hello 原生應用程式設定檔，並支援 hello 的 hello 使用者的授權端點。 這些是您將需要 toointegrate hello Microsoft 身分識別平台的所有 hello 項目時。

### <a name="add-hello-library-tooyour-project-by-using-cocoapods"></a>使用 CocoaPods 新增 hello 庫 tooyour 專案
CocoaPods 是 Xcode 專案的相依性管理員。 它會自動管理 hello 先前的安裝步驟。

```
$ vi Podfile
```
1. 加入下列 toothis podfile hello:
   
    ```
     platform :ios, '8.0'
   
     target 'QuickStart' do
   
     pod 'NXOAuth2Client'
   
     end
    ```
2. 使用 CocoaPods 載入 hello podfile。 這會建立您將載入的新 XCode Workspace。
   
    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

## <a name="explore-hello-structure-of-hello-project"></a>瀏覽 hello hello 專案結構
下列結構的 hello 是我們在 hello 基本架構中的專案設定：

* 具有 UPN 搜尋功能的「主要檢視」
* Hello 資料 hello 選使用者的相關詳細資料檢視
* 登入檢視，使用者可以登入 toohello 應用程式 tooquery hello 圖形中

我們將在 hello 基本架構 tooadd 驗證 toovarious 檔案。 Hello 的程式碼，例如 hello 視覺效果程式碼的其他部分 tooidentity 無關，但是提供給您。

## <a name="set-up-hello-settingsplst-file-in-hello-library"></a>設定 hello 文件庫中的 hello settings.plst 檔案
* 在 hello 快速入門專案，開啟 hello`settings.plist`檔案。 Hello hello 中的項目 hello 區段 tooreflect hello 值 hello Azure 入口網站中所用的值取代。 它使用 hello Active Directory 驗證程式庫時，您的程式碼會參考這些值。
  * hello `clientId` hello 您複製從 hello 入口網站應用程式的用戶端識別碼。
  * hello`redirectUri`提供該 hello 入口網站是 hello 重新導向 URL。

## <a name="set-up-hello-nxoauth2client-library-in-your-loginviewcontroller"></a>設定您 LoginViewController 中的 hello NXOAuth2Client 文件庫
hello NXOAuth2Client 程式庫需要設定一些值 tooget。 完成該工作之後，您可以使用 hello 取得語彙基元 toocall hello Graph API。 因為`LoginView`會隨時呼叫我們需要 tooauthenticate，合理 tooput 組態值 toothat 檔案中。

* 讓我們加入一些值 toohello`LoginViewController.m`檔案 tooset hello 內容進行驗證和授權。 Hello 值的相關詳細資訊，請遵循 hello 程式碼。
  
    ```objc
    NSString *scopes = @"openid offline_access User.Read";
    NSString *authURL = @"https://login.microsoftonline.com/common/oauth2/v2.0/authorize";
    NSString *loginURL = @"https://login.microsoftonline.com/common/login";
    NSString *bhh = @"urn:ietf:wg:oauth:2.0:oob?code=";
    NSString *tokenURL = @"https://login.microsoftonline.com/common/oauth2/v2.0/token";
    NSString *keychain = @"com.microsoft.azureactivedirectory.samples.graph.QuickStart";
    static NSString * const kIDMOAuth2SuccessPagePrefix = @"session_state=";
    NSURL *myRequestedUrl;
    NSURL *myLoadedUrl;
    bool loginFlow = FALSE;
    bool isRequestBusy;
    NSURL *authcode;
    ```

讓我們看看 hello 程式碼的相關詳細資料。

hello 第一個字串是`scopes`。  hello`User.Read`值可讓您 tooread hello 的基本設定檔 hello 登入的使用者。

您可以進一步了解在的 hello 可用範圍[Microsoft Graph 權限範圍](https://graph.microsoft.io/docs/authorization/permission_scopes)。

如`authURL`， `loginURL`， `bhh`，和`tokenURL`，您應該使用先前提供的 hello 值。 如果您使用 hello 開放原始碼 Microsoft Azure 身分識別的程式庫，我們提取這個資料為您使用我們的中繼資料端點。 我們所做過 hello 困難工作，讓您擷取這些值。

hello`keychain`值為 hello NXOAuth2Client 程式庫的 hello 容器將會使用 toocreate keychain toostore 您語彙基元。 如果您想要 tooget 單一登入 (SSO) 跨多個應用程式，您可以指定 hello 相同的金鑰鏈中每個應用程式，並要求 hello 使用 Xcode 權利中的金鑰鏈。 在 hello Apple 文件中的說明。

hello 其餘的這些值是必要的 toouse hello 程式庫，並為您 toocarry 值 toohello 內容建立位置。

### <a name="create-a-url-cache"></a>建立 URL 快取
內部`(void)viewDidLoad()`，這一律會呼叫 hello 檢視載入後，hello 下列程式碼 primes 我們使用的快取。

加入下列程式碼的 hello:

```objc
- (void)viewDidLoad {
    [super viewDidLoad];
    self.loginView.delegate = self;
    [self setupOAuth2AccountStore];
    [self requestOAuth2Access];
    NSURLCache *URLCache = [[NSURLCache alloc] initWithMemoryCapacity:4 * 1024 * 1024
                                                         diskCapacity:20 * 1024 * 1024
                                                             diskPath:nil];
    [NSURLCache setSharedURLCache:URLCache];

}
```

### <a name="create-a-webview-for-sign-in"></a>建立用於登入的 Web 檢視
WebView 可以提示 hello 使用者，提供其他的因素，例如 SMS 文字訊息 （若已設定），或傳回錯誤訊息 toohello 使用者。 這裡您將會建立 hello WebView 和之後再寫入 hello 即將發生的狀況的程式碼 toohandle hello 回呼 hello WebView 中從 hello 識別服務。

```objc
-(void)requestOAuth2Access {
    //toosign in tooMicrosoft APIs using OAuth2, we must show an embedded browser (UIWebView)
    [[NXOAuth2AccountStore sharedStore] requestAccessToAccountWithType:@"myGraphService"
                                   withPreparedAuthorizationURLHandler:^(NSURL *preparedURL) {
                                       //navigate toohello URL returned by NXOAuth2Client

                                       NSURLRequest *r = [NSURLRequest requestWithURL:preparedURL];
                                       [self.loginView loadRequest:r];
                                   }];
}
```

### <a name="override-hello-webview-methods-toohandle-authentication"></a>覆寫 hello WebView 方法 toohandle 驗證
tootell hello WebView 當使用者需要在 toosign，如先前所討論，會發生什麼情況，您可以貼上下列程式碼的 hello。

```objc
- (void)resolveUsingUIWebView:(NSURL *)URL {

    // We get hello auth token from a redirect so we need toohandle that in hello webview.

    if (![NSThread isMainThread]) {
        [self performSelectorOnMainThread:@selector(resolveUsingUIWebView:) withObject:URL waitUntilDone:YES];
        return;
    }

    NSURLRequest *hostnameURLRequest = [NSURLRequest requestWithURL:URL cachePolicy:NSURLRequestUseProtocolCachePolicy timeoutInterval:10.0f];
    isRequestBusy = YES;
    [self.loginView loadRequest:hostnameURLRequest];

    NSLog(@"resolveUsingUIWebView ready (status: UNKNOWN, URL: %@)", self.loginView.request.URL);
}

- (BOOL)webView:(UIWebView *)webView shouldStartLoadWithRequest:(NSURLRequest *)request navigationType:(UIWebViewNavigationType)navigationType {

    NSLog(@"webView:shouldStartLoadWithRequest: %@ (%li)", request.URL, (long)navigationType);

    // hello webview is where all hello communication happens. Slightly complicated.

    myLoadedUrl = [webView.request mainDocumentURL];
    NSLog(@"***Loaded url: %@", myLoadedUrl);

    //if hello UIWebView is showing our authorization URL or consent URL, show hello UIWebView control
    if ([request.URL.absoluteString rangeOfString:authURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:loginURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide hello UIWebView, we've left hello authorization flow
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:bhh options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide hello UIWebView, we've left hello authorization flow
        self.loginView.hidden = YES;
        [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }
    else {
        self.loginView.hidden = NO;
        //read hello Location from hello UIWebView, this is how Microsoft APIs is returning the
        //authentication code and relation information. This is controlled by hello redirect URL we chose toouse from Microsoft APIs
        //continue hello OAuth2 flow
       // [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }

    return YES;

}
```

### <a name="write-code-toohandle-hello-result-of-hello-oauth2-request"></a>寫入 hello OAuth2 要求的程式碼 toohandle hello 結果
hello 下列程式碼會處理 hello redirectURL hello WebView 從傳回的。 如果驗證未成功，hello 程式碼會再試一次。 同時，hello 程式庫會提供 hello 錯誤，您可以在 hello 主控台中看到或非同步方式處理。

```objc
- (void)handleOAuth2AccessResult:(NSString *)accessResult {

    AppData* data = [AppData getInstance];

    //parse hello response for success or failure
     if (accessResult)
    //if success, complete hello OAuth2 flow by handling hello redirect URL and obtaining a token
     {
         [[NXOAuth2AccountStore sharedStore] handleRedirectURL:accessResult];
    } else {
        //start over
        [self requestOAuth2Access];
    }
}
```

### <a name="set-up-hello-oauth-context-called-account-store"></a>設定 hello OAuth 內容 （稱為帳戶存放區）
您可以在這裡呼叫`-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]`上每個服務的 hello 應用程式 toobe 無法 tooaccess hello 共用的帳戶存放區。 hello 帳戶類型是字串做為識別項用於特定服務。 因為您正在存取 hello Graph API，hello 程式碼會參考做為 tooit `"myGraphService"`。 您再設定會告訴您任何項目會變更與 hello 語彙基元觀察者。 取得 hello 語彙基元之後，您會返回 hello 使用者回復 toohello `masterView`。

```objc
- (void)setupOAuth2AccountStore {


        AppData* data = [AppData getInstance];

    [[NXOAuth2AccountStore sharedStore] setClientID:data.clientId
                                             secret:data.secret
                                              scope:[NSSet setWithObject:scopes]
                                   authorizationURL:[NSURL URLWithString:authURL]
                                           tokenURL:[NSURL URLWithString:tokenURL]
                                        redirectURL:[NSURL URLWithString:data.redirectUriString]
                                      keyChainGroup: keychain
                                     forAccountType:@"myGraphService"];

    [[NSNotificationCenter defaultCenter] addObserverForName:NXOAuth2AccountStoreAccountsDidChangeNotification
                                                      object:[NXOAuth2AccountStore sharedStore]
                                                       queue:nil
                                                  usingBlock:^(NSNotification *aNotification) {
                                                      if (aNotification.userInfo) {
                                                          //account added, we have access
                                                          //we can now request protected data
                                                          NSLog(@"Success!! We have an access token.");
                                                          dispatch_async(dispatch_get_main_queue(),^ {

                                                              MasterViewController* masterViewController = [self.storyboard instantiateViewControllerWithIdentifier:@"masterView"];
                                                              [self.navigationController pushViewController:masterViewController animated:YES];
                                                          });
                                                      } else {
                                                          //account removed, we lost access
                                                      }
                                                  }];

    [[NSNotificationCenter defaultCenter] addObserverForName:NXOAuth2AccountStoreDidFailToRequestAccessNotification
                                                      object:[NXOAuth2AccountStore sharedStore]
                                                       queue:nil
                                                  usingBlock:^(NSNotification *aNotification) {
                                                      NSError *error = [aNotification.userInfo objectForKey:NXOAuth2AccountStoreErrorKey];
                                                      NSLog(@"Error!! %@", error.localizedDescription);
                                                  }];
}
```

## <a name="set-up-hello-master-view-toosearch-and-display-hello-users-from-hello-graph-api"></a>設定主版檢視 toosearch hello 及顯示 hello hello Graph API 的使用者
顯示 hello hello 方格中傳回資料的主要檢視控制器 (MVC) 應用程式已超出本逐步解說，hello 範圍和許多線上教學課程說明如何 toobuild 其中一個。 所有這段程式碼是 hello 基本架構檔案中。 不過，您需要 toodeal 與 MVC 應用程式中的幾件事：

* 當使用者輸入的項目 hello [搜尋] 欄位中的截距
* 因此，它會顯示 hello 結果 hello 方格中提供資料回復 toohello MasterView 的物件

我們會在下方進行這些動作。

### <a name="add-a-check-toosee-if-youre-logged-in"></a>如果您登入，加入核取 toosee
hello 應用程式會少如果 hello 使用者未登入，因此它智慧 toocheck 如果 hello 快取中已經有語彙基元。 如果不是，您將重新導向的 hello 使用者 toosign toohello LoginView 中。 如果您還記得，hello 最佳方式 toodo 動作檢視載入時為 toouse hello `viewDidLoad()` Apple 提供的方法。

```objc
- (void)viewDidLoad {
    [super viewDidLoad];


    NXOAuth2AccountStore *store = [NXOAuth2AccountStore sharedStore];
    NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];

        if (accounts.count == 0) {

        dispatch_async(dispatch_get_main_queue(),^ {

            LoginViewController* userSelectController = [self.storyboard instantiateViewControllerWithIdentifier:@"LoginUserView"];
            [self.navigationController pushViewController:userSelectController animated:YES];
        });
        }
```

### <a name="update-hello-table-view-when-data-is-received"></a>收到資料時，更新 hello 資料表檢視
當 hello Graph API 傳回的資料時，您會需要 toodisplay hello 資料。 為了簡單起見，以下是所有 hello 程式碼 tooupdate hello 資料表。 您只可以貼 MVC 未定案程式碼中的 hello 正確的值。

```objc
#pragma mark - Table View

- (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView {
    return 1;
}

- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section {

        return [upnArray count];
}

- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath {

    UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:@"TaskPrototypeCell" forIndexPath:indexPath];

    if ( cell == nil ) {
        cell = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleDefault reuseIdentifier:@"TaskPrototypeCell"];
    }

    User *user = nil;
     user = [upnArray objectAtIndex:indexPath.row];


    // Configure hello cell
    cell.textLabel.text = user.name;
    [cell setAccessoryType:UITableViewCellAccessoryDisclosureIndicator];

    return cell;
}

```

### <a name="provide-a-way-toocall-hello-graph-api-when-someone-types-in-hello-search-field"></a>提供方式 toocall hello Graph API，當有人 hello 搜尋欄位中的類型
當使用者會在 [hello] 方塊中輸入搜尋時，您需要 tooshove 會隨著 toohello Graph API。 hello`GraphAPICaller`類別，您將建立 hello 下列程式碼中，分隔從 hello 簡報 hello 查閱功能。 現在，讓我們寫 hello 摘要任何搜尋字元 toohello Graph API 的程式碼。 執行此作業，提供方法，稱為`lookupInGraph`，這樣會帶我們想要針對 toosearch 的 hello 字串。

```objc

-(void)lookupInGraph:(NSString *)searchText {
if (searchText.length > 0) {

    };



        [GraphAPICaller searchUserList:searchText completionBlock:^(NSMutableArray* returnedUpns, NSError* error) {
            if (returnedUpns) {


                upnArray = returnedUpns;


            }
            else
            {
                UIAlertView *alertView = [[UIAlertView alloc]initWithTitle:nil message:[[NSString alloc]initWithFormat:@"Error : %@", error.localizedDescription] delegate:nil cancelButtonTitle:@"Retry" otherButtonTitles:@"Cancel", nil];

                [alertView setDelegate:self];

                dispatch_async(dispatch_get_main_queue(),^ {
                    [alertView show];
                });
            }


        }];


}
```

## <a name="write-a-helper-class-tooaccess-hello-graph-api"></a>撰寫協助程式類別 tooaccess hello Graph API
這是我們的應用程式的核心是 hello。 Hello rest 從 Apple hello 預設 MVC 模式在插入程式碼，而這裡您撰寫程式碼 tooquery hello 圖形 hello 使用者輸入，然後再傳回資料。 Hello 程式碼，如下，它後面的詳細的說明。

### <a name="create-a-new-objective-c-header-file"></a>建立新的 Objective C 標頭檔
名稱 hello 檔`GraphAPICaller.h`，並加入下列程式碼的 hello。

```objc
@interface GraphAPICaller : NSObject<NSURLConnectionDataDelegate>

+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray*, NSError* error))completionBlock;

@end
```

如您所見，指定的方法會取得字串並傳回 completionBlock。 此 completionBlock，您可能已經猜到，將會更新 hello 資料表 hello 使用者進行搜尋，提供物件填入即時資料。

### <a name="create-a-new-objective-c-file"></a>建立新的 Objective C 檔案
名稱 hello 檔`GraphAPICaller.m`，並加入下列方法 hello。

```objc
+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray* Users, NSError* error)) completionBlock
{
    if (!loadedApplicationSettings)
    {
        [self readApplicationSettings];
    }

    AppData* data = [AppData getInstance];

    NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];

    NXOAuth2AccountStore *store = [NXOAuth2AccountStore sharedStore];
    NSDictionary* params = [self convertParamsToDictionary:searchString];

    NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];
    [NXOAuth2Request performMethod:@"GET"
                        onResource:[NSURL URLWithString:graphURL]
                   usingParameters:params
                       withAccount:accounts[0]
               sendProgressHandler:^(unsigned long long bytesSend, unsigned long long bytesTotal) {
                   // e.g., update a progress indicator
               }
                   responseHandler:^(NSURLResponse *response, NSData *responseData, NSError *error) {
                       // Process hello response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by hello key name being "value". It really is hello name of the
                           // first node. :-)

                           //each object is a key value pair
                           NSDictionary *keyValuePairs;
                           NSMutableArray* Users = [[NSMutableArray alloc]init];

                           for(int i =0; i < graphDataArray.count; i++)
                           {
                               keyValuePairs = [graphDataArray objectAtIndex:i];

                               User *s = [[User alloc]init];
                               s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                               s.name =[keyValuePairs valueForKey:@"displayName"];
                               s.mail =[keyValuePairs valueForKey:@"mail"];
                               s.businessPhones =[keyValuePairs valueForKey:@"businessPhones"];
                               s.mobilePhones =[keyValuePairs valueForKey:@"mobilePhone"];


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

```

我們會詳細解說這個方法。

此程式碼的 hello 核心處於 hello `NXOAuth2Request`，方法會採用 hello 參數，您已經定義 hello settings.plist 檔案中。

hello 第一個步驟是 tooconstruct hello right Graph API 呼叫。 因為您正在呼叫`/users`，您指定的方式是將它附加 hello 版本以及 toohello Graph API 資源。 它讓意義 tooput 這些外部設定檔中因為這些可能會演變 hello API 變更。

```objc
NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];
```

接下來，您需要 toospecify 參數，您也會提供 toohello Graph API 呼叫。 它是*非常重要*您不要讓 hello 參數加在 hello 資源端點中，因為，會清除所有的非 URI 符合字元在執行階段。 Hello 參數中必須提供所有的查詢程式碼。

```objc

NSDictionary* params = [self convertParamsToDictionary:searchString];
```

您可能發現這會呼叫您尚未撰寫的 `convertParamsToDictionary` 方法。 讓我們來立即執行 hello hello 檔案結尾：

```objc
+(NSDictionary*) convertParamsToDictionary:(NSString*)searchString
{
    NSMutableDictionary* dictionary = [[NSMutableDictionary alloc]init];

        NSString *query = [NSString stringWithFormat:@"startswith(givenName, '%@')", searchString];

           [dictionary setValue:query forKey:@"$filter"];



    return dictionary;
}

```
接下來，我們將使用 hello`NXOAuth2Request`方法 tooget 資料將從 hello API 以 JSON 格式。

```objc
NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];
    [NXOAuth2Request performMethod:@"GET"
                        onResource:[NSURL URLWithString:graphURL]
                   usingParameters:params
                       withAccount:accounts[0]
               sendProgressHandler:^(unsigned long long bytesSend, unsigned long long bytesTotal) {
                   // e.g., update a progress indicator
               }
                   responseHandler:^(NSURLResponse *response, NSData *responseData, NSError *error) {
                       // Process hello response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];
```

最後，讓我們看看您如何傳回 hello 資料 toohello MasterViewController。 hello 資料傳回為序列化且需要還原序列化的 toobe 和該 hello MainViewController 可取載入物件中。 基於此目的，有 hello 基本架構`User.m/h`建立使用者物件的檔案。 您的使用者將資訊填入物件 hello 圖形中。

```objc
                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by hello key name being "value". It really is hello name of the
                           // first node. :-)

                           //each object is a key value pair
                           NSDictionary *keyValuePairs;
                           NSMutableArray* Users = [[NSMutableArray alloc]init];

                           for(int i =0; i < graphDataArray.count; i++)
                           {
                               keyValuePairs = [graphDataArray objectAtIndex:i];

                               User *s = [[User alloc]init];
                               s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                               s.name =[keyValuePairs valueForKey:@"displayName"];
                               s.mail =[keyValuePairs valueForKey:@"mail"];
                               s.businessPhones =[keyValuePairs valueForKey:@"businessPhones"];
                               s.mobilePhones =[keyValuePairs valueForKey:@"mobilePhone"];


                               [Users addObject:s];
```


## <a name="run-hello-sample"></a>執行 hello 範例
如果您已使用 hello 基本架構，或與您的應用程式現在應該執行的 hello 逐步解說後面。 啟動 hello 模擬器，然後按一下**登入**toouse hello 應用程式。

## <a name="get-security-updates-for-our-product"></a>取得產品的安全性更新
我們鼓勵您的瀏覽 hello 的安全性事件發生時的 tooget 通知[資訊安全技術中心](https://technet.microsoft.com/security/dd252948)及訂閱 tooSecurity 諮詢警示。

