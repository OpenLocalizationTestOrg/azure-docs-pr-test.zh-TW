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
# <a name="add-authentication-tooyour-ios-app"></a><span data-ttu-id="98756-103">新增驗證 tooyour iOS 應用程式</span><span class="sxs-lookup"><span data-stu-id="98756-103">Add authentication tooyour iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="98756-104">在此教學課程中，您要加入驗證 toohello [iOS 快速啟動]使用支援的身分識別提供者的專案。</span><span class="sxs-lookup"><span data-stu-id="98756-104">In this tutorial, you add authentication toohello [iOS quick start] project using a supported identity provider.</span></span> <span data-ttu-id="98756-105">本教學課程根據 hello [iOS 快速啟動]教學課程中，您必須先完成。</span><span class="sxs-lookup"><span data-stu-id="98756-105">This tutorial is based on hello [iOS quick start] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="98756-106"><a name="register"></a>註冊您的應用程式進行驗證並設定 hello 應用程式服務</span><span class="sxs-lookup"><span data-stu-id="98756-106"><a name="register"></a>Register your app for authentication and configure hello App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="98756-107"><a name="redirecturl"></a>新增您的應用程式 toohello 允許外部重新導向 Url</span><span class="sxs-lookup"><span data-stu-id="98756-107"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="98756-108">安全的驗證會要求您為應用程式定義新的 URL 配置。</span><span class="sxs-lookup"><span data-stu-id="98756-108">Secure authentication requires that you define a new URL scheme for your app.</span></span>  <span data-ttu-id="98756-109">Hello 驗證程序完成之後，這可讓 hello 驗證系統 tooredirect 後 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="98756-109">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span>  <span data-ttu-id="98756-110">我們會在這整個教學課程中使用 URL 配置 appname。</span><span class="sxs-lookup"><span data-stu-id="98756-110">In this tutorial, we use the URL scheme _appname_ throughout.</span></span>  <span data-ttu-id="98756-111">不過，您可以使用任何您選擇的 URL 結構描述。</span><span class="sxs-lookup"><span data-stu-id="98756-111">However, you can use any URL scheme you choose.</span></span>  <span data-ttu-id="98756-112">它應該是唯一的 tooyour 行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="98756-112">It should be unique tooyour mobile application.</span></span>  <span data-ttu-id="98756-113">th 伺服器端 tooenable hello 重新導向：</span><span class="sxs-lookup"><span data-stu-id="98756-113">tooenable hello redirection on th server side:</span></span>

1. <span data-ttu-id="98756-114">在 hello [Azure 入口網站]，選取您的應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="98756-114">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="98756-115">按一下 hello**驗證 / 授權**功能表選項。</span><span class="sxs-lookup"><span data-stu-id="98756-115">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="98756-116">按一下**Azure Active Directory**下 hello**驗證提供者**> 一節。</span><span class="sxs-lookup"><span data-stu-id="98756-116">Click **Azure Active Directory** under hello **Authentication Providers** section.</span></span>

4. <span data-ttu-id="98756-117">設定 hello**管理模式**太**進階**。</span><span class="sxs-lookup"><span data-stu-id="98756-117">Set hello **Management mode** too**Advanced**.</span></span>

5. <span data-ttu-id="98756-118">在 hello**允許外部重新導向 Url**，輸入`appname://easyauth.callback`。</span><span class="sxs-lookup"><span data-stu-id="98756-118">In hello **Allowed External Redirect URLs**, enter `appname://easyauth.callback`.</span></span>  <span data-ttu-id="98756-119">hello _appname_這個字串中為 行動應用程式的 hello URL 配置。</span><span class="sxs-lookup"><span data-stu-id="98756-119">hello _appname_ in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="98756-120">它必須遵循通訊協定的標準 URL 規格 (只使用字母和數字，並以字母為開頭)。</span><span class="sxs-lookup"><span data-stu-id="98756-120">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="98756-121">請記下您選擇將會需要 tooadjust hello 在幾個位置的 URL 配置您的行動應用程式程式碼的 hello 字串。</span><span class="sxs-lookup"><span data-stu-id="98756-121">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

6. <span data-ttu-id="98756-122">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="98756-122">Click **OK**.</span></span>

7. <span data-ttu-id="98756-123">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="98756-123">Click **Save**.</span></span>

## <span data-ttu-id="98756-124"><a name="permissions"></a>限制 tooauthenticated 使用者權限</span><span class="sxs-lookup"><span data-stu-id="98756-124"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="98756-125">在 Xcode 中，按**執行**toostart hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="98756-125">In Xcode, press **Run** toostart hello app.</span></span> <span data-ttu-id="98756-126">因為 hello 應用程式嘗試 tooaccess 身為未經驗證的使用者後, 端，會引發例外狀況，但 hello *TodoItem*資料表現在需要驗證。</span><span class="sxs-lookup"><span data-stu-id="98756-126">An exception is raised because hello app attempts tooaccess the backend as an unauthenticated user, but hello *TodoItem* table now requires authentication.</span></span>

## <span data-ttu-id="98756-127"><a name="add-authentication"></a>新增驗證 tooapp</span><span class="sxs-lookup"><span data-stu-id="98756-127"><a name="add-authentication"></a>Add authentication tooapp</span></span>
<span data-ttu-id="98756-128">**Objective-C**：</span><span class="sxs-lookup"><span data-stu-id="98756-128">**Objective-C**:</span></span>

1. <span data-ttu-id="98756-129">在您的 Mac 上開啟*QSTodoListViewController.m*在 Xcode 中，新增下列方法 hello:</span><span class="sxs-lookup"><span data-stu-id="98756-129">On your Mac, open *QSTodoListViewController.m* in Xcode and add hello following method:</span></span>

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

    <span data-ttu-id="98756-130">變更*google*太*microsoftaccount*， *twitter*， *facebook*，或*windowsazureactivedirectory*如果您不使用 Google 作為身分識別提供者。</span><span class="sxs-lookup"><span data-stu-id="98756-130">Change *google* too*microsoftaccount*, *twitter*, *facebook*, or *windowsazureactivedirectory* if you are not using Google as your identity provider.</span></span> <span data-ttu-id="98756-131">如果您使用 Facebook，則必須在應用程式中[將 Facebook 網域列入白名單][1]。</span><span class="sxs-lookup"><span data-stu-id="98756-131">If you use Facebook, you must [whitelist Facebook domains][1] in your app.</span></span>

    <span data-ttu-id="98756-132">取代 hello **urlScheme**與您的應用程式的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="98756-132">Replace hello **urlScheme** with a unique name for your application.</span></span>  <span data-ttu-id="98756-133">hello urlScheme 應該是 hello 相同 hello hello 中所指定的 URL 配置通訊協定為**允許外部重新導向 Url** hello Azure 入口網站中的欄位。</span><span class="sxs-lookup"><span data-stu-id="98756-133">hello urlScheme should be hello same as hello URL Scheme protocol that you specified in hello **Allowed External Redirect URLs** field in hello Azure portal.</span></span> <span data-ttu-id="98756-134">hello 驗證回呼 tooswitch 後 tooyour 應用程式驗證要求完成之後，會使用 hello urlScheme。</span><span class="sxs-lookup"><span data-stu-id="98756-134">hello urlScheme is used by hello authentication callback tooswitch back tooyour application after the authentication request is complete.</span></span>

2. <span data-ttu-id="98756-135">取代`[self refresh]`中`viewDidLoad`中*QSTodoListViewController.m*以下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="98756-135">Replace `[self refresh]` in `viewDidLoad` in *QSTodoListViewController.m* with hello following code:</span></span>

    ```Objective-C
    [self loginAndGetData];
    ```

3. <span data-ttu-id="98756-136">開啟 hello`QSAppDelegate.h`檔案，然後加入下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="98756-136">Open hello `QSAppDelegate.h` file and add hello following code:</span></span>

    ```Objective-C
    #import "QSTodoService.h"

    @property (strong, nonatomic) QSTodoService *qsTodoService;
    ```

4. <span data-ttu-id="98756-137">開啟 hello`QSAppDelegate.m`檔案，然後加入下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="98756-137">Open hello `QSAppDelegate.m` file and add hello following code:</span></span>

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

   <span data-ttu-id="98756-138">加入下列程式碼直接讀取之前，先 hello 列`#pragma mark - Core Data stack`。</span><span class="sxs-lookup"><span data-stu-id="98756-138">Add this code directly before hello line reading `#pragma mark - Core Data stack`.</span></span>  <span data-ttu-id="98756-139">取代_appname_ wih hello urlScheme 值，您在步驟 1 中使用。</span><span class="sxs-lookup"><span data-stu-id="98756-139">Replace the _appname_ wih hello urlScheme value that you used in step 1.</span></span>

5. <span data-ttu-id="98756-140">開啟 hello`AppName-Info.plist`檔 （與 hello 應用程式名稱取代應用程式名稱），並加入下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="98756-140">Open hello `AppName-Info.plist` file (replacing AppName with hello name of your app), and add hello following code:</span></span>

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

    <span data-ttu-id="98756-141">這個程式碼應該放置在 hello`<dict>`項目。</span><span class="sxs-lookup"><span data-stu-id="98756-141">This code should be placed inside hello `<dict>` element.</span></span>  <span data-ttu-id="98756-142">取代 hello _appname_字串 (在陣列中**CFBundleURLSchemes**) 與您在步驟 1 中選擇的 hello 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="98756-142">Replace hello _appname_ string (within the array for **CFBundleURLSchemes**) with hello app name you chose in step 1.</span></span>  <span data-ttu-id="98756-143">您也可以進行這些變更在 hello plist 編輯器-請按一下 hello `AppName-Info.plist` XCode tooopen hello plist 編輯器中的檔案。</span><span class="sxs-lookup"><span data-stu-id="98756-143">You can also make these changes in hello plist editor - click on hello `AppName-Info.plist` file in XCode tooopen hello plist editor.</span></span>

    <span data-ttu-id="98756-144">取代 hello`com.microsoft.azure.zumo`字串**CFBundleURLName**和您的 Apple 配套識別碼。</span><span class="sxs-lookup"><span data-stu-id="98756-144">Replace hello `com.microsoft.azure.zumo` string for **CFBundleURLName** with your Apple bundle identifier.</span></span>

6. <span data-ttu-id="98756-145">按*執行*toostart hello 應用程式後再登入。</span><span class="sxs-lookup"><span data-stu-id="98756-145">Press *Run* toostart hello app, and then log in.</span></span> <span data-ttu-id="98756-146">當您登入時，您也應該能夠 tooview hello Todo 清單並進行更新。</span><span class="sxs-lookup"><span data-stu-id="98756-146">When you are logged in, you should be able tooview hello Todo list and make updates.</span></span>

<span data-ttu-id="98756-147">**Swift**：</span><span class="sxs-lookup"><span data-stu-id="98756-147">**Swift**:</span></span>

1. <span data-ttu-id="98756-148">在您的 Mac 上開啟*ToDoTableViewController.swift*在 Xcode 中，新增下列方法 hello:</span><span class="sxs-lookup"><span data-stu-id="98756-148">On your Mac, open *ToDoTableViewController.swift* in Xcode and add hello following method:</span></span>

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

    <span data-ttu-id="98756-149">變更*google*太*microsoftaccount*， *twitter*， *facebook*，或*windowsazureactivedirectory*如果您不使用 Google 作為身分識別提供者。</span><span class="sxs-lookup"><span data-stu-id="98756-149">Change *google* too*microsoftaccount*, *twitter*, *facebook*, or *windowsazureactivedirectory* if you are not using Google as your identity provider.</span></span> <span data-ttu-id="98756-150">如果您使用 Facebook，則必須在應用程式中[將 Facebook 網域列入白名單][1]。</span><span class="sxs-lookup"><span data-stu-id="98756-150">If you use Facebook, you must [whitelist Facebook domains][1] in your app.</span></span>

    <span data-ttu-id="98756-151">取代 hello **urlScheme**與您的應用程式的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="98756-151">Replace hello **urlScheme** with a unique name for your application.</span></span>  <span data-ttu-id="98756-152">hello urlScheme 應該是 hello 相同 hello hello 中所指定的 URL 配置通訊協定為**允許外部重新導向 Url** hello Azure 入口網站中的欄位。</span><span class="sxs-lookup"><span data-stu-id="98756-152">hello urlScheme should be hello same as hello URL Scheme protocol that you specified in hello **Allowed External Redirect URLs** field in hello Azure portal.</span></span> <span data-ttu-id="98756-153">hello 驗證回呼 tooswitch 後 tooyour 應用程式驗證要求完成之後，會使用 hello urlScheme。</span><span class="sxs-lookup"><span data-stu-id="98756-153">hello urlScheme is used by hello authentication callback tooswitch back tooyour application after the authentication request is complete.</span></span>

2. <span data-ttu-id="98756-154">移除 hello 行`self.refreshControl?.beginRefreshing()`和`self.onRefresh(self.refreshControl)`結尾`viewDidLoad()`中*ToDoTableViewController.swift*。</span><span class="sxs-lookup"><span data-stu-id="98756-154">Remove hello lines `self.refreshControl?.beginRefreshing()` and `self.onRefresh(self.refreshControl)` at the end of `viewDidLoad()` in *ToDoTableViewController.swift*.</span></span> <span data-ttu-id="98756-155">加入呼叫太`loginAndGetData()`在其位置：</span><span class="sxs-lookup"><span data-stu-id="98756-155">Add a call too`loginAndGetData()` in their place:</span></span>

    ```swift
    loginAndGetData()
    ```

3. <span data-ttu-id="98756-156">開啟 hello`AppDelegate.swift`檔案，然後加入下列行 toohello hello`AppDelegate`類別：</span><span class="sxs-lookup"><span data-stu-id="98756-156">Open hello `AppDelegate.swift` file and add hello following line toohello `AppDelegate` class:</span></span>

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

    <span data-ttu-id="98756-157">取代 hello _appname_ wih hello urlScheme 值，您在步驟 1 中使用。</span><span class="sxs-lookup"><span data-stu-id="98756-157">Replace hello _appname_ wih hello urlScheme value that you used in step 1.</span></span>

4. <span data-ttu-id="98756-158">開啟 hello`AppName-Info.plist`檔 （與 hello 應用程式名稱取代應用程式名稱），並加入下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="98756-158">Open hello `AppName-Info.plist` file (replacing AppName with hello name of your app), and add hello following code:</span></span>

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

    <span data-ttu-id="98756-159">這個程式碼應該放置在 hello`<dict>`項目。</span><span class="sxs-lookup"><span data-stu-id="98756-159">This code should be placed inside hello `<dict>` element.</span></span>  <span data-ttu-id="98756-160">取代 hello _appname_字串 (在陣列中**CFBundleURLSchemes**) 與您在步驟 1 中選擇的 hello 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="98756-160">Replace hello _appname_ string (within the array for **CFBundleURLSchemes**) with hello app name you chose in step 1.</span></span>  <span data-ttu-id="98756-161">您也可以進行這些變更在 hello plist 編輯器-請按一下 hello `AppName-Info.plist` XCode tooopen hello plist 編輯器中的檔案。</span><span class="sxs-lookup"><span data-stu-id="98756-161">You can also make these changes in hello plist editor - click on hello `AppName-Info.plist` file in XCode tooopen hello plist editor.</span></span>

    <span data-ttu-id="98756-162">取代 hello`com.microsoft.azure.zumo`字串**CFBundleURLName**和您的 Apple 配套識別碼。</span><span class="sxs-lookup"><span data-stu-id="98756-162">Replace hello `com.microsoft.azure.zumo` string for **CFBundleURLName** with your Apple bundle identifier.</span></span>

5. <span data-ttu-id="98756-163">按*執行*toostart hello 應用程式後再登入。</span><span class="sxs-lookup"><span data-stu-id="98756-163">Press *Run* toostart hello app, and then log in.</span></span> <span data-ttu-id="98756-164">當您登入時，您也應該能夠 tooview hello Todo 清單並進行更新。</span><span class="sxs-lookup"><span data-stu-id="98756-164">When you are logged in, you should be able tooview hello Todo list and make updates.</span></span>

<span data-ttu-id="98756-165">App Service 驗證會使用 Apples Inter-App Communication。</span><span class="sxs-lookup"><span data-stu-id="98756-165">App Service Authentication uses Apples Inter-App Communication.</span></span>  <span data-ttu-id="98756-166">如需有關這個主題的詳細資訊，請參閱 toohello [Apple 文件][2]</span><span class="sxs-lookup"><span data-stu-id="98756-166">For more details on this subject, refer toohello [Apple Documentation][2]</span></span>
<!-- URLs. -->

[1]: https://developers.facebook.com/docs/ios/ios9#whitelist
[2]: https://developer.apple.com/library/content/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Inter-AppCommunication/Inter-AppCommunication.html
[Azure 入口網站]: https://portal.azure.com

[iOS 快速啟動]: app-service-mobile-ios-get-started.md

