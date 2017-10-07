---
title: "aaaAdd authentication tooyour 通用 Windows 平台 (UWP) 應用程式 |Microsoft 文件"
description: "深入了解如何使用各種不同的身分識別提供者，包括通用 Windows 平台 (UWP) 應用程式的 toouse Azure App Service Mobile App tooauthenticate 使用者： AAD、 Google、 Facebook、 Twitter 和 Microsoft。"
services: app-service\mobile
documentationcenter: windows
author: ggailey777
manager: panarasi
editor: 
ms.assetid: 6cffd951-893e-4ce5-97ac-86e3f5ad9466
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: panarasi
ms.openlocfilehash: ad4477e9509f1c40c33e71818e268f6857fe1e80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-windows-app"></a><span data-ttu-id="19da6-103">新增驗證 tooyour Windows 應用程式</span><span class="sxs-lookup"><span data-stu-id="19da6-103">Add authentication tooyour Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="19da6-104">本主題說明如何 tooadd 雲端為基礎的驗證 tooyour 行動裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="19da6-104">This topic shows you how tooadd cloud-based authentication tooyour mobile app.</span></span> <span data-ttu-id="19da6-105">在本教學課程中，您可以加入驗證 toohello 通用 Windows 平台 (UWP) 快速入門專案使用身分識別提供者支援的 Azure App Service 行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="19da6-105">In this tutorial, you add authentication toohello Universal Windows Platform (UWP) quickstart project for Mobile Apps using an identity provider that is supported by Azure App Service.</span></span> <span data-ttu-id="19da6-106">正在順利通過驗證，並由您的行動裝置應用程式後端授權之後, 會顯示 hello 使用者識別碼的值。</span><span class="sxs-lookup"><span data-stu-id="19da6-106">After being successfully authenticated and authorized by your Mobile App backend, hello user ID value is displayed.</span></span>

<span data-ttu-id="19da6-107">本教學課程根據 hello 行動應用程式快速入門。</span><span class="sxs-lookup"><span data-stu-id="19da6-107">This tutorial is based on hello Mobile Apps quickstart.</span></span> <span data-ttu-id="19da6-108">您必須先完成 hello 教學課程[開始使用行動應用程式](app-service-mobile-windows-store-dotnet-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="19da6-108">You must first complete hello tutorial [Get started with Mobile Apps](app-service-mobile-windows-store-dotnet-get-started.md).</span></span>

## <span data-ttu-id="19da6-109"><a name="register"></a>註冊您的應用程式進行驗證並設定 hello 應用程式服務</span><span class="sxs-lookup"><span data-stu-id="19da6-109"><a name="register"></a>Register your app for authentication and configure hello App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="19da6-110"><a name="redirecturl"></a>新增您的應用程式 toohello 允許外部重新導向 Url</span><span class="sxs-lookup"><span data-stu-id="19da6-110"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="19da6-111">安全的驗證會要求您為應用程式定義新的 URL 配置。</span><span class="sxs-lookup"><span data-stu-id="19da6-111">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="19da6-112">Hello 驗證程序完成之後，這可讓 hello 驗證系統 tooredirect 後 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="19da6-112">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="19da6-113">在本教學課程中，我們使用 hello URL 配置_appname_整個。</span><span class="sxs-lookup"><span data-stu-id="19da6-113">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="19da6-114">不過，您可以使用任何您選擇的 URL 結構描述。</span><span class="sxs-lookup"><span data-stu-id="19da6-114">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="19da6-115">它應該是唯一的 tooyour 行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="19da6-115">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="19da6-116">hello 伺服器端 tooenable hello 重新導向：</span><span class="sxs-lookup"><span data-stu-id="19da6-116">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="19da6-117">在 hello [Azure 入口網站]，選取您的應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="19da6-117">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="19da6-118">按一下 hello**驗證 / 授權**功能表選項。</span><span class="sxs-lookup"><span data-stu-id="19da6-118">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="19da6-119">在 hello**允許外部重新導向 Url**，輸入`url_scheme_of_your_app://easyauth.callback`。</span><span class="sxs-lookup"><span data-stu-id="19da6-119">In hello **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="19da6-120">hello **url_scheme_of_your_app**這個字串中為 行動應用程式的 hello URL 配置。</span><span class="sxs-lookup"><span data-stu-id="19da6-120">hello **url_scheme_of_your_app** in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="19da6-121">它必須遵循通訊協定的標準 URL 規格 (只使用字母和數字，並以字母為開頭)。</span><span class="sxs-lookup"><span data-stu-id="19da6-121">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="19da6-122">請記下您選擇將會需要 tooadjust hello 在幾個位置的 URL 配置您的行動應用程式程式碼的 hello 字串。</span><span class="sxs-lookup"><span data-stu-id="19da6-122">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="19da6-123">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="19da6-123">Click **OK**.</span></span>

5. <span data-ttu-id="19da6-124">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="19da6-124">Click **Save**.</span></span>

## <span data-ttu-id="19da6-125"><a name="permissions"></a>限制 tooauthenticated 使用者權限</span><span class="sxs-lookup"><span data-stu-id="19da6-125"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="19da6-126">現在，您可以確認已停用該匿名存取 tooyour 後端。</span><span class="sxs-lookup"><span data-stu-id="19da6-126">Now, you can verify that anonymous access tooyour backend has been disabled.</span></span> <span data-ttu-id="19da6-127">Hello UWP 應用程式專案設定為 hello 啟始專案，部署和執行 hello 應用程式。請確認 hello 應用程式啟動之後，會引發未處理的例外狀況並顯示狀態碼 401 （未經授權）。</span><span class="sxs-lookup"><span data-stu-id="19da6-127">With hello UWP app project set as hello start-up project, deploy and run hello app; verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="19da6-128">這是因為 hello 應用程式嘗試 tooaccess 行動應用程式程式碼是未經驗證的使用者，但 hello *TodoItem*資料表現在需要驗證。</span><span class="sxs-lookup"><span data-stu-id="19da6-128">This happens because hello app attempts tooaccess your Mobile App Code as an unauthenticated user, but hello *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="19da6-129">接下來，您將從您的應用程式的服務要求的資源之前更新 hello tooauthenticate 的應用程式使用者。</span><span class="sxs-lookup"><span data-stu-id="19da6-129">Next, you will update hello app tooauthenticate users before requesting resources from your App Service.</span></span>

## <span data-ttu-id="19da6-130"><a name="add-authentication"></a>新增驗證 toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="19da6-130"><a name="add-authentication"></a>Add authentication toohello app</span></span>
1. <span data-ttu-id="19da6-131">在 hello UWP 應用程式專案檔 MainPage.xaml.cs，並加入下列程式碼片段的 hello:</span><span class="sxs-lookup"><span data-stu-id="19da6-131">In hello UWP app project file MainPage.xaml.cs and add hello following code snippet:</span></span>
   
        // Define a member variable for storing hello signed-in user. 
        private MobileServiceUser user;
   
        // Define a method that performs hello authentication process
        // using a Facebook sign-in. 
        private async System.Threading.Tasks.Task<bool> AuthenticateAsync()
        {
            string message;
            bool success = false;
            try
            {
                // Change 'MobileService' toohello name of your MobileServiceClient instance.
                // Sign-in using Facebook authentication.
                user = await App.MobileService
                    .LoginAsync(MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                message =
                    string.Format("You are now signed in - {0}", user.UserId);
   
                success = true;
            }
            catch (InvalidOperationException)
            {
                message = "You must log in. Login Required";
            }
   
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
            return success;
        }
   
    <span data-ttu-id="19da6-132">此程式碼會驗證 hello 與 Facebook 登入的使用者。</span><span class="sxs-lookup"><span data-stu-id="19da6-132">This code authenticates hello user with a Facebook login.</span></span> <span data-ttu-id="19da6-133">如果您使用 Facebook 以外的身分識別提供者，變更 hello 值**MobileServiceAuthenticationProvider**高於 toohello 值提供者。</span><span class="sxs-lookup"><span data-stu-id="19da6-133">If you are using an identity provider other than Facebook, change hello value of **MobileServiceAuthenticationProvider** above toohello value for your provider.</span></span>
2. <span data-ttu-id="19da6-134">取代 hello **Mainpage.xaml.cs**在 mainpage.xaml.cs 中的方法。</span><span class="sxs-lookup"><span data-stu-id="19da6-134">Replace hello **OnNavigatedTo()** method in MainPage.xaml.cs.</span></span> <span data-ttu-id="19da6-135">接下來，您將加入**登入**觸發驗證按鈕 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="19da6-135">Next, you will add a **Sign in** button toohello app that triggers authentication.</span></span>

        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            if (e.Parameter is Uri)
            {
                App.MobileService.ResumeWithURL(e.Parameter as Uri);
            }
        }

3. <span data-ttu-id="19da6-136">加入下列程式碼片段 toohello MainPage.xaml.cs hello:</span><span class="sxs-lookup"><span data-stu-id="19da6-136">Add hello following code snippet toohello MainPage.xaml.cs:</span></span>
   
        private async void ButtonLogin_Click(object sender, RoutedEventArgs e)
        {
            // Login hello user and then load data from hello mobile app.
            if (await AuthenticateAsync())
            {
                // Switch hello buttons and load items from hello mobile app.
                ButtonLogin.Visibility = Visibility.Collapsed;
                ButtonSave.Visibility = Visibility.Visible;
                //await InitLocalStoreAsync(); //offline sync support.
                await RefreshTodoItems();
            }
        }
4. <span data-ttu-id="19da6-137">開啟 hello MainPage.xaml 專案檔，找出 hello 項目，定義 hello**儲存**按鈕，並取代為下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="19da6-137">Open hello MainPage.xaml project file, locate hello element that defines hello **Save** button and replace it with hello following code:</span></span>
   
        <Button Name="ButtonSave" Visibility="Collapsed" Margin="0,8,8,0" 
                Click="ButtonSave_Click">
            <StackPanel Orientation="Horizontal">
                <SymbolIcon Symbol="Add"/>
                <TextBlock Margin="5">Save</TextBlock>
            </StackPanel>
        </Button>
        <Button Name="ButtonLogin" Visibility="Visible" Margin="0,8,8,0" 
                Click="ButtonLogin_Click" TabIndex="0">
            <StackPanel Orientation="Horizontal">
                <SymbolIcon Symbol="Permissions"/>
                <TextBlock Margin="5">Sign in</TextBlock> 
            </StackPanel>
        </Button>
5. <span data-ttu-id="19da6-138">加入下列程式碼片段 toohello App.xaml.cs hello:</span><span class="sxs-lookup"><span data-stu-id="19da6-138">Add hello following code snippet toohello App.xaml.cs:</span></span>

        protected override void OnActivated(IActivatedEventArgs args)
        {
            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                Frame content = Window.Current.Content as Frame;
                if (content.Content.GetType() == typeof(MainPage))
                {
                    content.Navigate(typeof(MainPage), protocolArgs.Uri);
                }
            }
            Window.Current.Activate();
            base.OnActivated(args);
        }
6. <span data-ttu-id="19da6-139">開啟 Package.appxmanifest 檔案，瀏覽過**宣告**，請在**可用宣告**下拉式清單中選取**通訊協定**按一下**新增**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="19da6-139">Open Package.appxmanifest file, navigate too**Declarations**, in **Available Declarations** dropdown list, select **Protocol** and click **Add** button.</span></span> <span data-ttu-id="19da6-140">現在設定 hello**屬性**的 hello**通訊協定**宣告。</span><span class="sxs-lookup"><span data-stu-id="19da6-140">Now configure hello **Properties** of hello **Protocol** declaration.</span></span> <span data-ttu-id="19da6-141">在**顯示名稱**，新增您希望應用程式的 toodisplay toousers hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="19da6-141">In **Display name**, add hello name you wish toodisplay toousers of your application.</span></span> <span data-ttu-id="19da6-142">在 [名稱] 中，新增您的 {url_scheme_of_your_app}。</span><span class="sxs-lookup"><span data-stu-id="19da6-142">In **Name**, add your {url_scheme_of_your_app}.</span></span>
7. <span data-ttu-id="19da6-143">按 F5 鍵 toorun hello 應用程式 hello，請按一下 hello**登入** 按鈕，然後登入您所選擇的身分識別提供者的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="19da6-143">Press hello F5 key toorun hello app, click hello **Sign in** button, and sign into hello app with your chosen identity provider.</span></span> <span data-ttu-id="19da6-144">登入成功後，hello 應用程式執行無誤，而且您會無法 tooquery 後端，並進行更新 toodata。</span><span class="sxs-lookup"><span data-stu-id="19da6-144">After your sign-in is successful, hello app runs without errors and you are able tooquery your backend and make updates toodata.</span></span>

## <span data-ttu-id="19da6-145"><a name="tokens"></a>Hello 用戶端上的存放區 hello 驗證權杖</span><span class="sxs-lookup"><span data-stu-id="19da6-145"><a name="tokens"></a>Store hello authentication token on hello client</span></span>
<span data-ttu-id="19da6-146">hello 前一個範例示範在標準登入，這需要 hello 用戶端 toocontact 這兩個 hello 身分識別提供者和 hello 應用程式服務，每次啟動該 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="19da6-146">hello previous example showed a standard sign-in, which requires hello client toocontact both hello identity provider and hello App Service every time that hello app starts.</span></span> <span data-ttu-id="19da6-147">不僅沒有效率，您可以執行這個方法成使用量的相關問題許多客戶應該嘗試 toostart 您的應用程式在 hello 相同的時間。</span><span class="sxs-lookup"><span data-stu-id="19da6-147">Not only is this method inefficient, you can run into usage-relates issues should many customers try toostart you app at hello same time.</span></span> <span data-ttu-id="19da6-148">更好的方法是 toocache hello 授權權杖傳回您的應用程式服務並再試一次 toouse 這第一次使用之前在根據提供者的登入。</span><span class="sxs-lookup"><span data-stu-id="19da6-148">A better approach is toocache hello authorization token returned by your App Service and try toouse this first before using a provider-based sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="19da6-149">您可以快取不論您是否使用用戶端管理或服務管理驗證發行應用程式服務的 hello 權杖。</span><span class="sxs-lookup"><span data-stu-id="19da6-149">You can cache hello token issued by App Services regardless of whether you are using client-managed or service-managed authentication.</span></span> <span data-ttu-id="19da6-150">本教學課程使用服務管理驗證。</span><span class="sxs-lookup"><span data-stu-id="19da6-150">This tutorial uses service-managed authentication.</span></span>
> 
> 

[!INCLUDE [mobile-windows-universal-dotnet-authenticate-app-with-token](../../includes/mobile-windows-universal-dotnet-authenticate-app-with-token.md)]

## <a name="next-steps"></a><span data-ttu-id="19da6-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="19da6-151">Next steps</span></span>
<span data-ttu-id="19da6-152">現在，您完成本教學課程中基本驗證，請考慮 tooone hello 遵循教學課程的上繼續進行：</span><span class="sxs-lookup"><span data-stu-id="19da6-152">Now that you completed this basic authentication tutorial, consider continuing on tooone of hello following tutorials:</span></span>

* [<span data-ttu-id="19da6-153">新增推播通知 tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="19da6-153">Add push notifications tooyour app</span></span>](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  <span data-ttu-id="19da6-154">了解如何 tooadd 推播通知支援 tooyour 應用程式，並設定行動裝置應用程式後端 toouse Azure 通知中樞 toosend 推播通知。</span><span class="sxs-lookup"><span data-stu-id="19da6-154">Learn how tooadd push notifications support tooyour app and configure your Mobile App backend toouse Azure Notification Hubs toosend push notifications.</span></span>
* [<span data-ttu-id="19da6-155">啟用應用程式的離線同步處理</span><span class="sxs-lookup"><span data-stu-id="19da6-155">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="19da6-156">了解如何離線 tooadd 支援使用行動裝置應用程式後端應用程式。</span><span class="sxs-lookup"><span data-stu-id="19da6-156">Learn how tooadd offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="19da6-157">離線同步處理可讓使用者使用行動應用程式的 toointeract&mdash;檢視、 加入或修改資料&mdash;即使在沒有網路連線。</span><span class="sxs-lookup"><span data-stu-id="19da6-157">Offline sync allows end-users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- URLs. -->
[Get started with your mobile app]: app-service-mobile-windows-store-dotnet-get-started.md
