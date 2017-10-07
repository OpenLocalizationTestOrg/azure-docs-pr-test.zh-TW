---
title: "使用 Azure 行動應用程式在 iOS 上 aaaAdd 驗證"
description: "深入了解如何 toouse Azure 行動應用程式 tooauthenticate 使用者的 iOS 應用程式透過不同的身分識別提供者，包括 AAD、 Google、 Facebook、 Twitter 和 Microsoft。"
services: app-service\mobile
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: ef3d3cbe-e7ca-45f9-987f-80c44209dc06
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: glenga
ms.openlocfilehash: df129e1c7517582db0e4705e0a6e98345ac8a48c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-ios-app"></a>新增驗證 tooyour iOS 應用程式
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

在此教學課程中，您要加入驗證 toohello [iOS 快速啟動]使用支援的身分識別提供者的專案。 本教學課程根據 hello [iOS 快速啟動]教學課程中，您必須先完成。

## <a name="register"></a>註冊您的應用程式進行驗證並設定 hello 應用程式服務
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>新增您的應用程式 toohello 允許外部重新導向 Url

安全的驗證會要求您為應用程式定義新的 URL 配置。  Hello 驗證程序完成之後，這可讓 hello 驗證系統 tooredirect 後 tooyour 應用程式。  我們會在這整個教學課程中使用 URL 配置 appname。  不過，您可以使用任何您選擇的 URL 結構描述。  它應該是唯一的 tooyour 行動應用程式。  th 伺服器端 tooenable hello 重新導向：

1. 在 hello [Azure 入口網站]，選取您的應用程式服務。

2. 按一下 hello**驗證 / 授權**功能表選項。

3. 按一下**Azure Active Directory**下 hello**驗證提供者**> 一節。

4. 設定 hello**管理模式**太**進階**。

5. 在 hello**允許外部重新導向 Url**，輸入`appname://easyauth.callback`。  hello _appname_這個字串中為 行動應用程式的 hello URL 配置。  它必須遵循通訊協定的標準 URL 規格 (只使用字母和數字，並以字母為開頭)。  請記下您選擇將會需要 tooadjust hello 在幾個位置的 URL 配置您的行動應用程式程式碼的 hello 字串。

6. 按一下 [確定] 。

7. 按一下 [儲存] 。

## <a name="permissions"></a>限制 tooauthenticated 使用者權限
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

在 Xcode 中，按**執行**toostart hello 應用程式。 因為 hello 應用程式嘗試 tooaccess 身為未經驗證的使用者後, 端，會引發例外狀況，但 hello *TodoItem*資料表現在需要驗證。

## <a name="add-authentication"></a>新增驗證 tooapp
**Objective-C**：

1. 在您的 Mac 上開啟*QSTodoListViewController.m*在 Xcode 中，新增下列方法 hello:

    ```Objective-C
    - (void)loginAndGetData
    {
        QSAppDelegate *appDelegate = (QSAppDelegate *)[UIApplication sharedApplication].delegate;
        appDelegate.qsTodoService = self.todoService;

        [self.todoService.client loginWithProvider:@"google" urlScheme:@"appname" controller:self animated:YES completion:^(MSUser * _Nullable user, NSError * _Nullable error) {
            if (error) {
                NSLog(@"Login failed with error: %@, %@", error, [error userInfo]);
            }
            else {
                self.todoService.client.currentUser = user;
                NSLog(@"User logged in: %@", user.userId);

                [self refresh];
            }
        }];
    }
    ```

    變更*google*太*microsoftaccount*， *twitter*， *facebook*，或*windowsazureactivedirectory*如果您不使用 Google 作為身分識別提供者。 如果您使用 Facebook，則必須在應用程式中[將 Facebook 網域列入白名單][1]。

    取代 hello **urlScheme**與您的應用程式的唯一名稱。  hello urlScheme 應該是 hello 相同 hello hello 中所指定的 URL 配置通訊協定為**允許外部重新導向 Url** hello Azure 入口網站中的欄位。 hello 驗證回呼 tooswitch 後 tooyour 應用程式驗證要求完成之後，會使用 hello urlScheme。

2. 取代`[self refresh]`中`viewDidLoad`中*QSTodoListViewController.m*以下列程式碼的 hello:

    ```Objective-C
    [self loginAndGetData];
    ```

3. 開啟 hello`QSAppDelegate.h`檔案，然後加入下列程式碼的 hello:

    ```Objective-C
    #import "QSTodoService.h"

    @property (strong, nonatomic) QSTodoService *qsTodoService;
    ```

4. 開啟 hello`QSAppDelegate.m`檔案，然後加入下列程式碼的 hello:

    ```Objective-C
    - (BOOL)application:(UIApplication *)application openURL:(NSURL *)url options:(NSDictionary<UIApplicationOpenURLOptionsKey,id> *)options
    {
        if ([[url.scheme lowercaseString] isEqualToString:@"appname"]) {
            // Resume login flow
            return [self.qsTodoService.client resumeWithURL:url];
        }
        else {
            return NO;
        }
    }
    ```

   加入下列程式碼直接讀取之前，先 hello 列`#pragma mark - Core Data stack`。  取代_appname_ wih hello urlScheme 值，您在步驟 1 中使用。

5. 開啟 hello`AppName-Info.plist`檔 （與 hello 應用程式名稱取代應用程式名稱），並加入下列程式碼的 hello:

    ```XML
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLName</key>
            <string>com.microsoft.azure.zumo</string>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>appname</string>
            </array>
        </dict>
    </array>
    ```

    這個程式碼應該放置在 hello`<dict>`項目。  取代 hello _appname_字串 (在陣列中**CFBundleURLSchemes**) 與您在步驟 1 中選擇的 hello 應用程式名稱。  您也可以進行這些變更在 hello plist 編輯器-請按一下 hello `AppName-Info.plist` XCode tooopen hello plist 編輯器中的檔案。

    取代 hello`com.microsoft.azure.zumo`字串**CFBundleURLName**和您的 Apple 配套識別碼。

6. 按*執行*toostart hello 應用程式後再登入。 當您登入時，您也應該能夠 tooview hello Todo 清單並進行更新。

**Swift**：

1. 在您的 Mac 上開啟*ToDoTableViewController.swift*在 Xcode 中，新增下列方法 hello:

    ```swift
    func loginAndGetData() {

        guard let client = self.table?.client, client.currentUser == nil else {
            return
        }

        let appDelegate = UIApplication.shared.delegate as! AppDelegate
        appDelegate.todoTableViewController = self

        let loginBlock: MSClientLoginBlock = {(user, error) -> Void in
            if (error != nil) {
                print("Error: \(error?.localizedDescription)")
            }
            else {
                client.currentUser = user
                print("User logged in: \(user?.userId)")
            }
        }

        client.login(withProvider:"google", urlScheme: "appname", controller: self, animated: true, completion: loginBlock)

    }
    ```

    變更*google*太*microsoftaccount*， *twitter*， *facebook*，或*windowsazureactivedirectory*如果您不使用 Google 作為身分識別提供者。 如果您使用 Facebook，則必須在應用程式中[將 Facebook 網域列入白名單][1]。

    取代 hello **urlScheme**與您的應用程式的唯一名稱。  hello urlScheme 應該是 hello 相同 hello hello 中所指定的 URL 配置通訊協定為**允許外部重新導向 Url** hello Azure 入口網站中的欄位。 hello 驗證回呼 tooswitch 後 tooyour 應用程式驗證要求完成之後，會使用 hello urlScheme。

2. 移除 hello 行`self.refreshControl?.beginRefreshing()`和`self.onRefresh(self.refreshControl)`結尾`viewDidLoad()`中*ToDoTableViewController.swift*。 加入呼叫太`loginAndGetData()`在其位置：

    ```swift
    loginAndGetData()
    ```

3. 開啟 hello`AppDelegate.swift`檔案，然後加入下列行 toohello hello`AppDelegate`類別：

    ```swift
    var todoTableViewController: ToDoTableViewController?

    func application(_ application: UIApplication, openURL url: NSURL, options: [UIApplicationOpenURLOptionsKey : Any] = [:]) -> Bool {
        if url.scheme?.lowercased() == "appname" {
            return (todoTableViewController!.table?.client.resume(with: url as URL))!
        }
        else {
            return false
        }
    }
    ```

    取代 hello _appname_ wih hello urlScheme 值，您在步驟 1 中使用。

4. 開啟 hello`AppName-Info.plist`檔 （與 hello 應用程式名稱取代應用程式名稱），並加入下列程式碼的 hello:

    ```xml
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLName</key>
            <string>com.microsoft.azure.zumo</string>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>appname</string>
            </array>
        </dict>
    </array>
    ```

    這個程式碼應該放置在 hello`<dict>`項目。  取代 hello _appname_字串 (在陣列中**CFBundleURLSchemes**) 與您在步驟 1 中選擇的 hello 應用程式名稱。  您也可以進行這些變更在 hello plist 編輯器-請按一下 hello `AppName-Info.plist` XCode tooopen hello plist 編輯器中的檔案。

    取代 hello`com.microsoft.azure.zumo`字串**CFBundleURLName**和您的 Apple 配套識別碼。

5. 按*執行*toostart hello 應用程式後再登入。 當您登入時，您也應該能夠 tooview hello Todo 清單並進行更新。

App Service 驗證會使用 Apples Inter-App Communication。  如需有關這個主題的詳細資訊，請參閱 toohello [Apple 文件][2]
<!-- URLs. -->

[1]: https://developers.facebook.com/docs/ios/ios9#whitelist
[2]: https://developer.apple.com/library/content/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Inter-AppCommunication/Inter-AppCommunication.html
[Azure 入口網站]: https://portal.azure.com

[iOS 快速啟動]: app-service-mobile-ios-get-started.md

