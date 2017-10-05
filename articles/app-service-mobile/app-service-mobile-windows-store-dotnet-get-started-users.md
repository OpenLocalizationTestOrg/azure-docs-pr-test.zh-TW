---
title: "將驗證新增至您的通用 Windows 平台 (UWP) 應用程式 | Microsoft Docs"
description: "了解如何使用 Azure App Service Mobile Apps，透過眾多識別提供者驗證通用 Windows 平台 (UWP) 應用程式使用者，包括 AAD、Google、Facebook、Twitter 和 Microsoft。"
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
ms.openlocfilehash: 47da343d4ec956ec2e669757f56e853675f887a3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-windows-app"></a><span data-ttu-id="0d829-103">將驗證新增至您的 Windows 應用程式</span><span class="sxs-lookup"><span data-stu-id="0d829-103">Add authentication to your Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="0d829-104">本主題說明如何將雲端式驗證加入到您的行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="0d829-104">This topic shows you how to add cloud-based authentication to your mobile app.</span></span> <span data-ttu-id="0d829-105">在本教學課程中，您會使用 Azure App Service 所支援的身分識別提供者，將驗證新增至 Mobile Apps 的通用 Windows 平台 (UWP) 快速入門專案。</span><span class="sxs-lookup"><span data-stu-id="0d829-105">In this tutorial, you add authentication to the Universal Windows Platform (UWP) quickstart project for Mobile Apps using an identity provider that is supported by Azure App Service.</span></span> <span data-ttu-id="0d829-106">由行動應用程式後端成功驗證並授權之後，就會顯示使用者識別碼值。</span><span class="sxs-lookup"><span data-stu-id="0d829-106">After being successfully authenticated and authorized by your Mobile App backend, the user ID value is displayed.</span></span>

<span data-ttu-id="0d829-107">本教學課程以 Azure Mobile Apps 快速入門為基礎。</span><span class="sxs-lookup"><span data-stu-id="0d829-107">This tutorial is based on the Mobile Apps quickstart.</span></span> <span data-ttu-id="0d829-108">您必須先完成 [開始使用 Mobile Apps](app-service-mobile-windows-store-dotnet-get-started.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="0d829-108">You must first complete the tutorial [Get started with Mobile Apps](app-service-mobile-windows-store-dotnet-get-started.md).</span></span>

## <span data-ttu-id="0d829-109"><a name="register"></a>註冊應用程式進行驗證，並設定應用程式服務</span><span class="sxs-lookup"><span data-stu-id="0d829-109"><a name="register"></a>Register your app for authentication and configure the App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="0d829-110"><a name="redirecturl"></a>將您的應用程式新增至允許的外部重新導向 URL</span><span class="sxs-lookup"><span data-stu-id="0d829-110"><a name="redirecturl"></a>Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="0d829-111">安全的驗證會要求您為應用程式定義新的 URL 配置。</span><span class="sxs-lookup"><span data-stu-id="0d829-111">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="0d829-112">這讓驗證系統能夠在驗證程序完成之後，重新導向回到您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="0d829-112">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="0d829-113">我們會在這整個教學課程中使用 URL 配置 appname。</span><span class="sxs-lookup"><span data-stu-id="0d829-113">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="0d829-114">不過，您可以使用任何您選擇的 URL 結構描述。</span><span class="sxs-lookup"><span data-stu-id="0d829-114">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="0d829-115">它對於您的行動應用程式而言應該是唯一的。</span><span class="sxs-lookup"><span data-stu-id="0d829-115">It should be unique to your mobile application.</span></span> <span data-ttu-id="0d829-116">在伺服器端啟用重新導向：</span><span class="sxs-lookup"><span data-stu-id="0d829-116">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="0d829-117">在 [Azure 入口網站] 中，選取您的 App Service。</span><span class="sxs-lookup"><span data-stu-id="0d829-117">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="0d829-118">按一下 [驗證/授權] 功能表選項。</span><span class="sxs-lookup"><span data-stu-id="0d829-118">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="0d829-119">在 [允許的外部重新導向 URL] 中，輸入 `url_scheme_of_your_app://easyauth.callback`。</span><span class="sxs-lookup"><span data-stu-id="0d829-119">In the **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="0d829-120">此字串中的 **url_scheme_of_your_app** 是您行動應用程式的 URL 配置。</span><span class="sxs-lookup"><span data-stu-id="0d829-120">The **url_scheme_of_your_app** in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="0d829-121">它必須遵循通訊協定的標準 URL 規格 (只使用字母和數字，並以字母為開頭)。</span><span class="sxs-lookup"><span data-stu-id="0d829-121">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="0d829-122">請記下您選擇的字串，因為您將需要在數個位置中使用該 URL 配置來調整您的行動應用程式程式碼。</span><span class="sxs-lookup"><span data-stu-id="0d829-122">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="0d829-123">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="0d829-123">Click **OK**.</span></span>

5. <span data-ttu-id="0d829-124">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="0d829-124">Click **Save**.</span></span>

## <span data-ttu-id="0d829-125"><a name="permissions"></a>限制只有通過驗證的使用者具有權限</span><span class="sxs-lookup"><span data-stu-id="0d829-125"><a name="permissions"></a>Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="0d829-126">現在，您可以驗證是否已停用後端的匿名存取。</span><span class="sxs-lookup"><span data-stu-id="0d829-126">Now, you can verify that anonymous access to your backend has been disabled.</span></span> <span data-ttu-id="0d829-127">將 UWP 應用程式專案設定為啟始專案，部署並執行應用程式；應用程式啟動後，確認會引發狀態碼為 401 (未經授權) 的未處理例外狀況。</span><span class="sxs-lookup"><span data-stu-id="0d829-127">With the UWP app project set as the start-up project, deploy and run the app; verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="0d829-128">這是因為應用程式嘗試以未驗證的使用者身分存取您的行動應用程式程式碼，但 *TodoItem* 資料表現在需要驗證。</span><span class="sxs-lookup"><span data-stu-id="0d829-128">This happens because the app attempts to access your Mobile App Code as an unauthenticated user, but the *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="0d829-129">接下來，您要將應用程式更新為在要求 App Service 的資源之前必須驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="0d829-129">Next, you will update the app to authenticate users before requesting resources from your App Service.</span></span>

## <span data-ttu-id="0d829-130"><a name="add-authentication"></a>將驗證新增至應用程式</span><span class="sxs-lookup"><span data-stu-id="0d829-130"><a name="add-authentication"></a>Add authentication to the app</span></span>
1. <span data-ttu-id="0d829-131">在 UWP 應用程式專案檔案 MainPage.cs 中，新增下列程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="0d829-131">In the UWP app project file MainPage.xaml.cs and add the following code snippet:</span></span>
   
        // Define a member variable for storing the signed-in user. 
        private MobileServiceUser user;
   
        // Define a method that performs the authentication process
        // using a Facebook sign-in. 
        private async System.Threading.Tasks.Task<bool> AuthenticateAsync()
        {
            string message;
            bool success = false;
            try
            {
                // Change 'MobileService' to the name of your MobileServiceClient instance.
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
   
    <span data-ttu-id="0d829-132">此程式碼會使用 Facebook 登入來驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="0d829-132">This code authenticates the user with a Facebook login.</span></span> <span data-ttu-id="0d829-133">如果您打算使用除了 Facebook 以外的識別提供者，請將上方的 **MobileServiceAuthenticationProvider** 值變更成您提供者。</span><span class="sxs-lookup"><span data-stu-id="0d829-133">If you are using an identity provider other than Facebook, change the value of **MobileServiceAuthenticationProvider** above to the value for your provider.</span></span>
2. <span data-ttu-id="0d829-134">取代 MainPage.xaml.cs 中的 **OnNavigatedTo()** 方法。</span><span class="sxs-lookup"><span data-stu-id="0d829-134">Replace the **OnNavigatedTo()** method in MainPage.xaml.cs.</span></span> <span data-ttu-id="0d829-135">接下來，將 [登入]  按鈕新增至觸發驗證的應用程式。</span><span class="sxs-lookup"><span data-stu-id="0d829-135">Next, you will add a **Sign in** button to the app that triggers authentication.</span></span>

        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            if (e.Parameter is Uri)
            {
                App.MobileService.ResumeWithURL(e.Parameter as Uri);
            }
        }

3. <span data-ttu-id="0d829-136">將下列程式碼片段新增至 MainPage.xaml.cs：</span><span class="sxs-lookup"><span data-stu-id="0d829-136">Add the following code snippet to the MainPage.xaml.cs:</span></span>
   
        private async void ButtonLogin_Click(object sender, RoutedEventArgs e)
        {
            // Login the user and then load data from the mobile app.
            if (await AuthenticateAsync())
            {
                // Switch the buttons and load items from the mobile app.
                ButtonLogin.Visibility = Visibility.Collapsed;
                ButtonSave.Visibility = Visibility.Visible;
                //await InitLocalStoreAsync(); //offline sync support.
                await RefreshTodoItems();
            }
        }
4. <span data-ttu-id="0d829-137">開啟 MainPage.xaml 專案檔案，找到定義 **儲存** 按鈕的項目，並將它取代為下列程式碼︰</span><span class="sxs-lookup"><span data-stu-id="0d829-137">Open the MainPage.xaml project file, locate the element that defines the **Save** button and replace it with the following code:</span></span>
   
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
5. <span data-ttu-id="0d829-138">將下列程式碼片段新增至 App.xaml.cs：</span><span class="sxs-lookup"><span data-stu-id="0d829-138">Add the following code snippet to the App.xaml.cs:</span></span>

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
6. <span data-ttu-id="0d829-139">開啟 Package.appxmanifest 檔案，瀏覽至 [宣告]，在 [可用宣告] 下拉式清單中選取 [通訊協定] 並按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0d829-139">Open Package.appxmanifest file, navigate to **Declarations**, in **Available Declarations** dropdown list, select **Protocol** and click **Add** button.</span></span> <span data-ttu-id="0d829-140">立即設定 [通訊協定] 宣告的 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="0d829-140">Now configure the **Properties** of the **Protocol** declaration.</span></span> <span data-ttu-id="0d829-141">在 [顯示名稱] 中，新增您要對應用程式使用者顯示的名稱。</span><span class="sxs-lookup"><span data-stu-id="0d829-141">In **Display name**, add the name you wish to display to users of your application.</span></span> <span data-ttu-id="0d829-142">在 [名稱] 中，新增您的 {url_scheme_of_your_app}。</span><span class="sxs-lookup"><span data-stu-id="0d829-142">In **Name**, add your {url_scheme_of_your_app}.</span></span>
7. <span data-ttu-id="0d829-143">按 F5 鍵以執行應用程式、按一下 [登入]  按鈕，然後以您選擇的身分識別提供者登入應用程式。</span><span class="sxs-lookup"><span data-stu-id="0d829-143">Press the F5 key to run the app, click the **Sign in** button, and sign into the app with your chosen identity provider.</span></span> <span data-ttu-id="0d829-144">當您成功登入之後，應用程式應會正確無誤地執行，而且您應能夠查詢後端並更新資料。</span><span class="sxs-lookup"><span data-stu-id="0d829-144">After your sign-in is successful, the app runs without errors and you are able to query your backend and make updates to data.</span></span>

## <span data-ttu-id="0d829-145"><a name="tokens"></a>將驗證權杖儲存在用戶端上</span><span class="sxs-lookup"><span data-stu-id="0d829-145"><a name="tokens"></a>Store the authentication token on the client</span></span>
<span data-ttu-id="0d829-146">先前範例所示範的標準登入，在每次應用程式啟動時，皆需要用戶端連絡身分識別提供者和 App Service。</span><span class="sxs-lookup"><span data-stu-id="0d829-146">The previous example showed a standard sign-in, which requires the client to contact both the identity provider and the App Service every time that the app starts.</span></span> <span data-ttu-id="0d829-147">這個方法不只效率不彰，而且如果同時有許多用戶試圖啟用您的應用程式時，還可能遇到使用量相關的問題。</span><span class="sxs-lookup"><span data-stu-id="0d829-147">Not only is this method inefficient, you can run into usage-relates issues should many customers try to start you app at the same time.</span></span> <span data-ttu-id="0d829-148">更好的方法就是快取 App Service 傳回的授權權杖，然後嘗試在使用提供者形式登入前先使用此方法。</span><span class="sxs-lookup"><span data-stu-id="0d829-148">A better approach is to cache the authorization token returned by your App Service and try to use this first before using a provider-based sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="0d829-149">無論您使用用戶端管理型或服務管理型驗證，皆可以快取 App Services 發行的權杖。</span><span class="sxs-lookup"><span data-stu-id="0d829-149">You can cache the token issued by App Services regardless of whether you are using client-managed or service-managed authentication.</span></span> <span data-ttu-id="0d829-150">本教學課程使用服務管理驗證。</span><span class="sxs-lookup"><span data-stu-id="0d829-150">This tutorial uses service-managed authentication.</span></span>
> 
> 

[!INCLUDE [mobile-windows-universal-dotnet-authenticate-app-with-token](../../includes/mobile-windows-universal-dotnet-authenticate-app-with-token.md)]

## <a name="next-steps"></a><span data-ttu-id="0d829-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0d829-151">Next steps</span></span>
<span data-ttu-id="0d829-152">現在您已經完成了這個基本驗證的教學課程，可以考慮繼續進行下列其中一個教學課程：</span><span class="sxs-lookup"><span data-stu-id="0d829-152">Now that you completed this basic authentication tutorial, consider continuing on to one of the following tutorials:</span></span>

* [<span data-ttu-id="0d829-153">將推播通知新增至應用程式</span><span class="sxs-lookup"><span data-stu-id="0d829-153">Add push notifications to your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  <span data-ttu-id="0d829-154">了解如何將推播通知支援新增至應用程式，並設定行動應用程式後端以使用 Azure 通知中樞傳送推播通知。</span><span class="sxs-lookup"><span data-stu-id="0d829-154">Learn how to add push notifications support to your app and configure your Mobile App backend to use Azure Notification Hubs to send push notifications.</span></span>
* [<span data-ttu-id="0d829-155">啟用應用程式的離線同步處理</span><span class="sxs-lookup"><span data-stu-id="0d829-155">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="0d829-156">了解如何使用行動應用程式後端，將離線支援新增至應用程式。</span><span class="sxs-lookup"><span data-stu-id="0d829-156">Learn how to add offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="0d829-157">離線同步處理可讓使用者與行動應用程式進行互動&mdash;檢視、新增或修改資料&mdash;即使沒有網路連線進也可行。</span><span class="sxs-lookup"><span data-stu-id="0d829-157">Offline sync allows end-users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- URLs. -->
[Get started with your mobile app]: app-service-mobile-windows-store-dotnet-get-started.md
