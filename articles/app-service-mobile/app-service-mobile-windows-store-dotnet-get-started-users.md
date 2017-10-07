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
# <a name="add-authentication-tooyour-windows-app"></a>新增驗證 tooyour Windows 應用程式
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

本主題說明如何 tooadd 雲端為基礎的驗證 tooyour 行動裝置應用程式。 在本教學課程中，您可以加入驗證 toohello 通用 Windows 平台 (UWP) 快速入門專案使用身分識別提供者支援的 Azure App Service 行動應用程式。 正在順利通過驗證，並由您的行動裝置應用程式後端授權之後, 會顯示 hello 使用者識別碼的值。

本教學課程根據 hello 行動應用程式快速入門。 您必須先完成 hello 教學課程[開始使用行動應用程式](app-service-mobile-windows-store-dotnet-get-started.md)。

## <a name="register"></a>註冊您的應用程式進行驗證並設定 hello 應用程式服務
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>新增您的應用程式 toohello 允許外部重新導向 Url

安全的驗證會要求您為應用程式定義新的 URL 配置。 Hello 驗證程序完成之後，這可讓 hello 驗證系統 tooredirect 後 tooyour 應用程式。 在本教學課程中，我們使用 hello URL 配置_appname_整個。 不過，您可以使用任何您選擇的 URL 結構描述。 它應該是唯一的 tooyour 行動應用程式。 hello 伺服器端 tooenable hello 重新導向：

1. 在 hello [Azure 入口網站]，選取您的應用程式服務。

2. 按一下 hello**驗證 / 授權**功能表選項。

3. 在 hello**允許外部重新導向 Url**，輸入`url_scheme_of_your_app://easyauth.callback`。  hello **url_scheme_of_your_app**這個字串中為 行動應用程式的 hello URL 配置。  它必須遵循通訊協定的標準 URL 規格 (只使用字母和數字，並以字母為開頭)。  請記下您選擇將會需要 tooadjust hello 在幾個位置的 URL 配置您的行動應用程式程式碼的 hello 字串。

4. 按一下 [確定] 。

5. 按一下 [儲存] 。

## <a name="permissions"></a>限制 tooauthenticated 使用者權限
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

現在，您可以確認已停用該匿名存取 tooyour 後端。 Hello UWP 應用程式專案設定為 hello 啟始專案，部署和執行 hello 應用程式。請確認 hello 應用程式啟動之後，會引發未處理的例外狀況並顯示狀態碼 401 （未經授權）。 這是因為 hello 應用程式嘗試 tooaccess 行動應用程式程式碼是未經驗證的使用者，但 hello *TodoItem*資料表現在需要驗證。

接下來，您將從您的應用程式的服務要求的資源之前更新 hello tooauthenticate 的應用程式使用者。

## <a name="add-authentication"></a>新增驗證 toohello 應用程式
1. 在 hello UWP 應用程式專案檔 MainPage.xaml.cs，並加入下列程式碼片段的 hello:
   
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
   
    此程式碼會驗證 hello 與 Facebook 登入的使用者。 如果您使用 Facebook 以外的身分識別提供者，變更 hello 值**MobileServiceAuthenticationProvider**高於 toohello 值提供者。
2. 取代 hello **Mainpage.xaml.cs**在 mainpage.xaml.cs 中的方法。 接下來，您將加入**登入**觸發驗證按鈕 toohello 應用程式。

        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            if (e.Parameter is Uri)
            {
                App.MobileService.ResumeWithURL(e.Parameter as Uri);
            }
        }

3. 加入下列程式碼片段 toohello MainPage.xaml.cs hello:
   
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
4. 開啟 hello MainPage.xaml 專案檔，找出 hello 項目，定義 hello**儲存**按鈕，並取代為下列程式碼的 hello:
   
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
5. 加入下列程式碼片段 toohello App.xaml.cs hello:

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
6. 開啟 Package.appxmanifest 檔案，瀏覽過**宣告**，請在**可用宣告**下拉式清單中選取**通訊協定**按一下**新增**  按鈕。 現在設定 hello**屬性**的 hello**通訊協定**宣告。 在**顯示名稱**，新增您希望應用程式的 toodisplay toousers hello 名稱。 在 [名稱] 中，新增您的 {url_scheme_of_your_app}。
7. 按 F5 鍵 toorun hello 應用程式 hello，請按一下 hello**登入** 按鈕，然後登入您所選擇的身分識別提供者的 hello 應用程式。 登入成功後，hello 應用程式執行無誤，而且您會無法 tooquery 後端，並進行更新 toodata。

## <a name="tokens"></a>Hello 用戶端上的存放區 hello 驗證權杖
hello 前一個範例示範在標準登入，這需要 hello 用戶端 toocontact 這兩個 hello 身分識別提供者和 hello 應用程式服務，每次啟動該 hello 應用程式。 不僅沒有效率，您可以執行這個方法成使用量的相關問題許多客戶應該嘗試 toostart 您的應用程式在 hello 相同的時間。 更好的方法是 toocache hello 授權權杖傳回您的應用程式服務並再試一次 toouse 這第一次使用之前在根據提供者的登入。

> [!NOTE]
> 您可以快取不論您是否使用用戶端管理或服務管理驗證發行應用程式服務的 hello 權杖。 本教學課程使用服務管理驗證。
> 
> 

[!INCLUDE [mobile-windows-universal-dotnet-authenticate-app-with-token](../../includes/mobile-windows-universal-dotnet-authenticate-app-with-token.md)]

## <a name="next-steps"></a>後續步驟
現在，您完成本教學課程中基本驗證，請考慮 tooone hello 遵循教學課程的上繼續進行：

* [新增推播通知 tooyour 應用程式](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  了解如何 tooadd 推播通知支援 tooyour 應用程式，並設定行動裝置應用程式後端 toouse Azure 通知中樞 toosend 推播通知。
* [啟用應用程式的離線同步處理](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  了解如何離線 tooadd 支援使用行動裝置應用程式後端應用程式。 離線同步處理可讓使用者使用行動應用程式的 toointeract&mdash;檢視、 加入或修改資料&mdash;即使在沒有網路連線。

<!-- URLs. -->
[Get started with your mobile app]: app-service-mobile-windows-store-dotnet-get-started.md
